---
title: AKS(Azure Kubernetes Service)에서 여러 Pod용 Files 볼륨을 동적으로 만들기
description: Azure Files를 사용하여 AKS(Azure Kubernetes Service)에서 여러 Pod에 동시에 사용할 영구 볼륨을 동적으로 만드는 방법에 대해 알아봅니다.
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 10/08/2018
ms.author: iainfou
ms.openlocfilehash: 022ffeaf75f8f03447b931ed9c3a474286a17f89
ms.sourcegitcommit: 7b0778a1488e8fd70ee57e55bde783a69521c912
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "49067808"
---
# <a name="dynamically-create-and-use-a-persistent-volume-with-azure-files-in-azure-kubernetes-service-aks"></a>AKS(Azure Kubernetes Service)에서 Azure Files를 사용하여 영구 볼륨을 동적으로 만들어 사용

영구적 볼륨은 Kubernetes Pod와 함께 사용하기 위해 프로비전된 저장소 부분을 나타냅니다. 하나 이상의 Pod에서 영구적 볼륨을 사용할 수 있으며 동적 또는 정적으로 프로비전할 수 있습니다. 여러 Pod가 같은 저장소 볼륨에 동시에 액세스해야 하는 경우 Azure Files를 사용하여 [SMB(서버 메시지 블록) 프로토콜][smb-overview]을 통해 연결할 수 있습니다. 이 문서에서는 AKS(Azure Kubernetes Service) 클러스터에서 여러 Pod에 사용할 Azure Files공유를 동적으로 만드는 방법을 설명합니다.

Kubernetes 영구적 볼륨에 대한 자세한 내용은 [Kubernetes 영구적 볼륨][kubernetes-volumes]을 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에

이 문서에서는 기존 AKS 클러스터가 있다고 가정합니다. AKS 클러스터가 필요한 경우 AKS 빠른 시작[Azure CLI 사용][aks-quickstart-cli] 또는 [Azure Portal 사용][aks-quickstart-portal]을 참조하세요.

또한 Azure CLI 버전 2.0.46 이상이 설치되고 구성되어 있어야 합니다. `az --version`을 실행하여 버전을 찾습니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 설치][install-azure-cli]를 참조하세요.

## <a name="create-a-storage-account"></a>저장소 계정 만들기

Azure Files 공유를 Kubernetes 볼륨으로 동적으로 만들면 AKS **노드** 리소스 그룹에 들어 있는 모든 저장소 계정을 사용할 수 있습니다. 이 그룹은 AKS 클러스터에 대한 리소스 프로비전에서 만들어진 *MC_* 접두사가 있는 계정입니다. [az aks show][az-aks-show] 명령을 사용하여 리소스 그룹 이름을 가져옵니다.

```azurecli
$ az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv

MC_myResourceGroup_myAKSCluster_eastus
```

[az storage account create][az-storage-account-create] 명령을 사용하여 저장소 계정을 만듭니다.

이전 단계에서 수집한 리소스 그룹의 이름으로 `--resource-group`을, 사용자가 원하는 이름으로 `--name`을 업데이트합니다. 사용자 고유의 저장소 계정 이름을 제공합니다.

```azurecli
az storage account create --resource-group MC_myResourceGroup_myAKSCluster_eastus --name mystorageaccount --sku Standard_LRS
```

> [!NOTE]
> Azure Files는 현재 표준 저장소에서만 작동합니다. Premium Storage를 사용하는 경우 볼륨이 프로비전되지 않습니다.

## <a name="create-a-storage-class"></a>저장소 클래스 만들기

저장소 클래스는 Azure 파일 공유를 만드는 방법을 정의하는 데 사용됩니다. 클래스에 저장소 계정을 지정할 수 있습니다. 저장소 계정을 지정하지 않으면 *skuName* 및 *location*을 지정해야 하고, 연결된 리소스 그룹의 모든 저장소 계정이 일치하는지 평가됩니다. Azure 파일의 Kubernetes 저장소 클래스에 대한 자세한 내용은 [Kubernetes 저장소 클래스][kubernetes-storage-classes]를 참조하세요.

`azure-file-sc.yaml` 파일을 만들고 다음 예제 매니페스트를 복사합니다. *storageAccount* 값을 이전 단계에서 만든 저장소 계정의 이름으로 바꿉니다. *mountOptions*에 대한 자세한 내용은 [탑재 옵션][mount-options] 섹션을 참조하세요.

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: azurefile
provisioner: kubernetes.io/azure-file
mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
parameters:
  skuName: Standard_LRS
  storageAccount: mystorageaccount
```

[kubectl apply][kubectl-apply] 명령을 사용하여 저장소 클래스를 만듭니다.

```console
kubectl apply -f azure-file-sc.yaml
```

## <a name="create-a-cluster-role-and-binding"></a>클러스터 역할 및 바인딩 만들기

AKS 클러스터는 Kubernetes RBAC(역할 기반 액세스 제어)를 사용하여 수행할 수 있는 작업을 제한합니다. *역할*은 부여할 사용 권한을 정의하고 *바인딩*은 원하는 사용자에게 역할을 적용합니다. 이러한 할당은 주어진 네임스페이스 또는 전체 클러스터에 적용될 수 있습니다. 자세한 내용은 [RBAC 권한 부여 사용][kubernetes-rbac]을 참조하세요.

필요한 저장소 리소스를 만들도록 Azure 플랫폼을 허용하려면 *ClusterRole* 및 *ClusterRoleBinding*을 만듭니다. `azure-pvc-roles.yaml`이라는 파일을 만들고 다음 YAML에 복사합니다.

```yaml
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: system:azure-cloud-provider
rules:
- apiGroups: ['']
  resources: ['secrets']
  verbs:     ['get','create']
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: system:azure-cloud-provider
roleRef:
  kind: ClusterRole
  apiGroup: rbac.authorization.k8s.io
  name: system:azure-cloud-provider
subjects:
- kind: ServiceAccount
  name: persistent-volume-binder
  namespace: kube-system
```

[kubectl apply][kubectl-apply] 명령을 사용하여 권한을 할당합니다.

```console
kubectl apply -f azure-pvc-roles.yaml
```

## <a name="create-a-persistent-volume-claim"></a>영구적 볼륨 클레임 만들기

PVC(영구적 볼륨 클레임)는 저장소 클래스 개체를 사용하여 Azure 파일 공유를 동적으로 프로비전합니다. 다음 YAML을 사용하여 크기가 *5GB*이고 *ReadWriteMany* 액세스 권한을 가진 영구적 볼륨 클레임을 만들 수 있습니다. 액세스 모드에 대한 자세한 내용은 [Kubernetes 영구 볼륨][access-modes] 설명서를 참조하세요.

이제 `azure-file-pvc.yaml`이라는 파일을 만들고 다음 YAML에 복사합니다. *storageClassName*이 마지막 단계에서 만든 저장소 클래스와 일치하는지 확인합니다.

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azurefile
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: azurefile
  resources:
    requests:
      storage: 5Gi
```

[kubectl apply][kubectl-apply] 명령을 사용하여 영구 볼륨 클레임을 만듭니다.

```console
kubectl apply -f azure-file-pvc.yaml
```

완료되면 파일 공유가 생성됩니다. 연결 정보 및 자격 증명을 포함하고 있는 Kubernetes 비밀도 생성됩니다. [kubectl get][kubectl-get] 명령을 사용하여 PVC의 상태를 볼 수 있습니다.

```
$ kubectl get pvc azurefile

NAME        STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
azurefile   Bound     pvc-8436e62e-a0d9-11e5-8521-5a8664dc0477   5Gi        RWX            azurefile      5m
```

## <a name="use-the-persistent-volume"></a>영구적 볼륨 사용

다음 YAML은 영구적 볼륨 클레임 *azurefile*을 사용하여 */mnt/azure* 경로에 Azure 파일 공유를 탑재하는 Pod를 만듭니다.

`azure-pvc-files.yaml` 파일을 만들고 다음 YAML에 복사합니다. *claimName*이 마지막 단계에서 만든 PVC와 일치하는지 확인합니다.

```yaml
kind: Pod
apiVersion: v1
metadata:
  name: mypod
spec:
  containers:
  - name: mypod
    image: nginx:1.15.5
    resources:
      requests:
        cpu: 100m
        memory: 128Mi
      limits:
        cpu: 250m
        memory: 256Mi
    volumeMounts:
    - mountPath: "/mnt/azure"
      name: volume
  volumes:
    - name: volume
      persistentVolumeClaim:
        claimName: azurefile
```

[kubectl apply][kubectl-apply] 명령을 사용하여 Pod를 만듭니다.

```console
kubectl apply -f azure-pvc-files.yaml
```

이제 Azure 디스크가 */mnt/azure* 디렉터리에 탑재된 Pod가 실행되고 있습니다. 이 구성은 `kubectl describe pod mypod`를 통해 Pod를 검사할 때 볼 수 있습니다. 압축된 다음 예제 출력에서는 컨테이너에 탑재된 볼륨을 보여 줍니다.

```
Containers:
  mypod:
    Container ID:   docker://053bc9c0df72232d755aa040bfba8b533fa696b123876108dec400e364d2523e
    Image:          nginx:1.15.5
    Image ID:       docker-pullable://nginx@sha256:d85914d547a6c92faa39ce7058bd7529baacab7e0cd4255442b04577c4d1f424
    State:          Running
      Started:      Wed, 15 Aug 2018 22:22:27 +0000
    Ready:          True
    Mounts:
      /mnt/azure from volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-8rv4z (ro)
[...]
Volumes:
  volume:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  azurefile
    ReadOnly:   false
[...]
```

## <a name="mount-options"></a>탑재 옵션

다음 표에 설명된 대로 Kubernetes 버전마다 기본 *fileMode* 및 *dirMode* 값이 다릅니다.

| 버전 | 값 |
| ---- | ---- |
| v1.6.x, v1.7.x | 0777 |
| v1.8.0-v1.8.5 | 0700 |
| v1.8.6 이상 | 0755 |
| v1.9.0 | 0700 |
| v1.9.1 이상 | 0755 |

클러스터 버전 1.8.5 이상을 사용하고 저장소 클래스를 사용하여 동적으로 영구적 볼륨을 만드는 경우 저장소 클래스 개체에서 마운트 옵션을 지정할 수 있습니다. 다음 예제에서는 *0777*을 설정합니다.

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: azurefile
provisioner: kubernetes.io/azure-file
mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
parameters:
  skuName: Standard_LRS
```

클러스터 버전 1.8.5 이상을 사용하고 정적으로 영구적 볼륨 개체를 만드는 경우 *PersistentVolume* 개체에서 마운트 옵션을 지정해야 합니다. 정적으로 영구 볼륨을 만드는 방법에 대한 자세한 내용은 [정적 영구적 볼륨][pv-static]을 참조하세요.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: azurefile
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteMany
  azureFile:
    secretName: azure-secret
    shareName: azurefile
    readOnly: false
  mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
```

버전 1.8.0 - 1.8.4의 클러스터를 사용하는 경우 *runAsUser* 값을 *0*으로 설정하여 보안 컨텍스트를 지정할 수 있습니다. Pod 보안 컨텍스트에 대한 자세한 내용은 [보안 컨텍스트 구성][kubernetes-security-context]을 참조하세요.

## <a name="next-steps"></a>다음 단계

Azure Files를 사용하는 Kubernetes 영구적 볼륨에 대해 자세히 알아봅니다.

> [!div class="nextstepaction"]
> [Azure Files용 Kubernetes 플러그 인][kubernetes-files]

<!-- LINKS - external -->
[access-modes]: https://kubernetes.io/docs/concepts/storage/persistent-volumes
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubectl-describe]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-files]: https://github.com/kubernetes/examples/blob/master/staging/volumes/azure_file/README.md
[kubernetes-secret]: https://kubernetes.io/docs/concepts/configuration/secret/
[kubernetes-security-context]: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/
[kubernetes-storage-classes]: https://kubernetes.io/docs/concepts/storage/storage-classes/#azure-file
[kubernetes-volumes]: https://kubernetes.io/docs/concepts/storage/persistent-volumes/
[pv-static]: https://kubernetes.io/docs/concepts/storage/persistent-volumes/#static
[kubernetes-rbac]: https://kubernetes.io/docs/reference/access-authn-authz/rbac/
[smb-overview]: /windows/desktop/FileIO/microsoft-smb-protocol-and-cifs-protocol-overview

<!-- LINKS - internal -->
[az-group-create]: /cli/azure/group#az-group-create
[az-group-list]: /cli/azure/group#az-group-list
[az-resource-show]: /cli/azure/aks#az-aks-show
[az-storage-account-create]: /cli/azure/storage/account#az-storage-account-create
[az-storage-create]: /cli/azure/storage/account#az-storage-account-create
[az-storage-key-list]: /cli/azure/storage/account/keys#az-storage-account-keys-list
[az-storage-share-create]: /cli/azure/storage/share#az-storage-share-create
[mount-options]: #mount-options
[aks-quickstart-cli]: kubernetes-walkthrough.md
[aks-quickstart-portal]: kubernetes-walkthrough-portal.md
[install-azure-cli]: /cli/azure/install-azure-cli
[az-aks-show]: /cli/azure/aks#az-aks-show
