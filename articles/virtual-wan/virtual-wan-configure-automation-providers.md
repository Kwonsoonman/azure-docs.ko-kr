---
title: Azure Virtual WAN 파트너 | Microsoft Docs
description: 이 문서에서는 파트너가 Azure Virtual WAN 자동화를 설정하도록 돕습니다.
services: virtual-wan
author: cherylmc
ms.service: virtual-wan
ms.topic: conceptual
ms.date: 10/04/2018
ms.author: cherylmc
Customer intent: As a Virtual WAN software-defined connectivity provider, I want to set up a provisioning environment.
ms.openlocfilehash: a4664e628af5824b7b197cbdb5c5af602a3a4476
ms.sourcegitcommit: 5c00e98c0d825f7005cb0f07d62052aff0bc0ca8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2018
ms.locfileid: "49958689"
---
# <a name="virtual-wan-partners"></a>Virtual WAN 파트너

이 문서는 Azure Virtual WAN의 분기 장치(고객 온-프레미스 VPN 장치 또는 SDWAN CPE)를 연결 및 구성하기 위해 자동화 환경을 설정하는 방법을 이해하는 데 도움이 됩니다. 이 문서는 IPsec/IKEv2 또는 IPsec/IKEv1을 통해 VPN 연결을 수용할 수 있는 분기 장치를 제공하는 공급자를 대상으로 합니다.

분기 장치(고객 온-프레미스 VPN 장치 또는 SDWAN CPE)는 일반적으로 프로비전될 컨트롤러/장치 대시보드를 사용합니다. SD-WAN 솔루션 관리자는 종종 네트워크로 연결하기 전에 관리 콘솔을 사용하여 장치를 사전 프로비전할 수 있습니다. 이 VPN 지원 장치는 컨트롤러에서 해당 컨트롤 평면 논리를 가져옵니다. VPN 장치 또는 SD-WAN 컨트롤러는 Azure API를 사용하여 Azure Virtual WAN에 대한 연결을 자동화할 수 있습니다. 이 연결 유형은 할당된 외부 연결 공용 IP 주소를 갖고 있는 온-프레미스 장치를 필요로 합니다.

## <a name ="before"></a>자동화를 시작하기 전에

* 장치에서 IPsec IKEv1/IKEv2를 지원하는지 확인합니다. [기본 정책](#default)을 참조하세요.
* Azure Virtual WAN에 대한 연결을 자동화하는 데 사용하는 [REST API](https://docs.microsoft.com/rest/api/azure/)를 참조하세요.
* Azure Virtual WAN의 포털 환경을 테스트합니다.
* 그런 다음, 자동화하려는 연결 단계의 부분을 결정합니다. 최소한 자동화하는 것이 좋습니다.

  * Access Control
  * Azure Virtual WAN에 분기 장치 정보 업로드
  * Azure 구성 다운로드 및 분기 장치에서 Azure Virtual WAN으로 연결 설정

* Azure Virtual WAN과 함께 예상되는 고객 환경을 이해합니다.

  1. 일반적으로 가상 WAN 사용자는 Virtual WAN 리소스를 만들어 프로세스를 시작합니다.
  2. 사용자는 온-프레미스 시스템(사용자의 분기 컨트롤러 또는 VPN 장치 프로비저닝 소프트웨어)에 대한 서비스 주체 기반 리소스 그룹 액세스를 설정하여 Azure Virtual WAN으로 분기 정보를 작성합니다.
  3. 사용자는 이 때 UI에 로그인하고 서비스 주체 자격 증명을 설정하도록 결정할 수 있습니다. 완료되면 컨트롤러는 제공하는 자동화를 사용하여 분기 정보를 업로드할 수 있어야 합니다. Azure 측에서 동일한 수동 작업은 '사이트 만들기'입니다.
  4. 사이트(분기 장치) 정보를 Azure에서 사용할 수 있으면 사용자는 허브에 사이트를 연결합니다. 가상 허브는 Microsoft에서 관리하는 가상 네트워크입니다. 허브는 온-프레미스 네트워크(vpnsite)에서 연결을 활성화하는 다양한 서비스 엔드포인트를 포함합니다. 허브는 지역에서 네트워크의 핵심입니다. Azure 지역당 하나의 허브만 있을 수 있으며 그 안의 vpn 엔드포인트(vpngateway)가 이 프로세스 중 생성됩니다. VPN 게이트웨이는 대역폭 및 연결 요구 사항에 따라 적절하게 크기가 조정되는 확장 가능한 게이트웨이입니다. 분기 장치 컨트롤러 대시보드에서 가상 허브 및 vpngateway 생성을 자동화하도록 선택할 수 있습니다.
  5. 가상 허브가 사이트에 연결되면 사용자가 수동으로 다운로드할 수 있도록 구성 파일이 생성됩니다. 자동화가 들어오는 위치이며 사용자 환경을 원활하게 만듭니다. 사용자가 수동으로 다운로드하고 분기 장치를 구성하는 대신 자동화를 설정하고 UI에서 최소 클릭 환경을 제공할 수 있으므로 공유 키 불일치, IPSec 매개 변수 불일치, 구성 파일 가독성 등과 같은 일반적인 연결 문제를 완화합니다.
  6. 솔루션의 이 단계 끝에서 사용자는 분기 장치와 가상 허브 간의 원활한 사이트 간 연결을 갖게 됩니다. 다른 허브에서 추가 연결을 설정할 수도 있습니다. 각 연결은 활성-활성 터널입니다. 고객은 터널에 대한 각 링크에 다른 ISP를 사용하도록 선택할 수 있습니다.

## <a name ="understand"></a>자동화 세부 정보 이해


###  <a name="access"></a>액세스 제어

고객은 장치 UI에서 Virtual WAN에 적절한 액세스 제어를 설정할 수 있어야 합니다. 이 경우, Azure 서비스 주체를 사용하는 것이 좋습니다. 서비스 주체 기반 액세스는 분기 정보 업로드에 적합한 인증을 장치 컨트롤러에 제공합니다. 자세한 내용은 [서비스 주체 만들기](../active-directory/develop/howto-create-service-principal-portal.md#create-an-azure-active-directory-application)를 참조하세요. 이 기능은 Azure Virtual WAN 제품의 외부이지만 관련 세부 정보가 장치 관리 대시보드에 입력된 후 Azure에서 액세스를 설정하는 데 수행되는 일반적인 단계를 아래에 나열합니다.

* 온-프레미스 장치 컨트롤러에 대한 Azure Active Directory 응용 프로그램을 만듭니다.
* 응용 프로그램 ID 및 인증 키 가져오기
* 테넌트 ID 가져오기
* 응용 프로그램을 “기여자”에 할당

###  <a name="branch"></a>분기 장치 정보 업로드

Azure에 분기(온-프레미스 사이트) 정보를 업로드하도록 사용자 환경을 디자인합니다. VPNSite의[REST API](https://docs.microsoft.com/rest/api/virtualwan/vpnsites)를 사용하여 Virtual WAN에서 사이트 정보를 작성할 수 있습니다. 모든 분기 SDWAN/VPN 장치를 제공하거나 적절하게 장치 사용자 지정을 선택할 수 있습니다.


### <a name="device"></a>장치 구성 다운로드 및 연결

이 단계는 Azure 구성 다운로드 및 분기 장치에서 Azure Virtual WAN으로 연결 설정을 포함합니다. 이 단계에서는 공급자를 사용하지 않는 고객은 수동으로 Azure 구성을 다운로드하고 온-프레미스 SDWAN/VPN 장치에 적용합니다. 공급자는 이 단계를 자동화해야 합니다. 장치 컨트롤러는 'GetVpnConfiguration' REST API를 호출하여 일반적으로 다음 파일과 비슷하게 표시되는 Azure 구성을 다운로드할 수 있습니다.

**구성 정보**

  * 가상 허브에 연결된 Azure VNet은 ConnectedSubnet으로 표시됩니다.
  * VPN 연결에는 경로 기반 구성 및 IKEv2/IKEv1이 사용됩니다.

#### <a name="understanding-the-device-configuration-file"></a>장치 구성 파일 이해

장치 구성 파일에는 온-프레미스 VPN 장치를 구성할 때 사용할 설정이 포함되어 있습니다. 이 파일을 볼 때 다음 정보를 확인합니다.

* **vpnSiteConfiguration -** 이 섹션은 Virtual WAN에 연결된 사이트로 설정된 장치 정보를 나타냅니다. 여기에는 분기 장치의 이름 및 공용 IP 주소가 포함됩니다.
* **vpnSiteConnections -** 이 섹션에서는 다음 정보를 제공합니다.

    * 가상 허브 VNet의 **주소 공간**.<br>예제:
 
        ```
        "AddressSpace":"10.1.0.0/24"
        ```
    * 허브에 연결된 VNet의 **주소 공간**.<br>예제:

         ```
        "ConnectedSubnets":["10.2.0.0/16","10.30.0.0/16"]
         ```
    * 가상 허브 vpngateway의 **IP 주소**. vpngateway에는 활성-활성 구성의 2개 터널로 구성된 각 연결이 있기 때문에 이 파일에 두 IP 주소가 모두 나열됩니다. 이 예제에서는 각 사이트에 대한 “Instance0” 및 “Instance1”이 표시됩니다.<br>예제:

        ``` 
        "Instance0":"104.45.18.186"
        "Instance1":"104.45.13.195"
        ```
    * BGP, 미리 공유한 키 등의 **Vpngateway 연결 구성 세부 정보**. PSK는 자동으로 생성되는 미리 공유한 키입니다. 사용자 지정 PSK의 개요 페이지에서 연결을 언제든지 편집할 수 있습니다.
  
#### <a name="example-device-configuration-file"></a>예제 장치 구성 파일

  ```
  { 
      "configurationVersion":{ 
         "LastUpdatedTime":"2018-07-03T18:29:49.8405161Z",
         "Version":"r403583d-9c82-4cb8-8570-1cbbcd9983b5"
      },
      "vpnSiteConfiguration":{ 
         "Name":"testsite1",
         "IPAddress":"73.239.3.208"
      },
      "vpnSiteConnections":[ 
         { 
            "hubConfiguration":{ 
               "AddressSpace":"10.1.0.0/24",
               "Region":"West Europe",
               "ConnectedSubnets":[ 
                  "10.2.0.0/16",
                  "10.30.0.0/16"
               ]
            },
            "gatewayConfiguration":{ 
               "IpAddresses":{ 
                  "Instance0":"104.45.18.186",
                  "Instance1":"104.45.13.195"
               }
            },
            "connectionConfiguration":{ 
               "IsBgpEnabled":false,
               "PSK":"bkOWe5dPPqkx0DfFE3tyuP7y3oYqAEbI",
               "IPsecParameters":{ 
                  "SADataSizeInKilobytes":102400000,
                  "SALifeTimeInSeconds":3600
               }
            }
         }
      ]
   },
   { 
      "configurationVersion":{ 
         "LastUpdatedTime":"2018-07-03T18:29:49.8405161Z",
         "Version":"1f33f891-e1ab-42b8-8d8c-c024d337bcac"
      },
      "vpnSiteConfiguration":{ 
         "Name":" testsite2",
         "IPAddress":"66.193.205.122"
      },
      "vpnSiteConnections":[ 
         { 
            "hubConfiguration":{ 
               "AddressSpace":"10.1.0.0/24",
               "Region":"West Europe"
            },
            "gatewayConfiguration":{ 
               "IpAddresses":{ 
                  "Instance0":"104.45.18.187",
                  "Instance1":"104.45.13.195"
               }
            },
            "connectionConfiguration":{ 
               "IsBgpEnabled":false,
               "PSK":"XzODPyAYQqFs4ai9WzrJour0qLzeg7Qg",
               "IPsecParameters":{ 
                  "SADataSizeInKilobytes":102400000,
                  "SALifeTimeInSeconds":3600
               }
            }
         }
      ]
   },
   { 
      "configurationVersion":{ 
         "LastUpdatedTime":"2018-07-03T18:29:49.8405161Z",
         "Version":"cd1e4a23-96bd-43a9-93b5-b51c2a945c7"
      },
      "vpnSiteConfiguration":{ 
         "Name":" testsite3",
         "IPAddress":"182.71.123.228"
      },
      "vpnSiteConnections":[ 
         { 
            "hubConfiguration":{ 
               "AddressSpace":"10.1.0.0/24",
               "Region":"West Europe"
            },
            "gatewayConfiguration":{ 
               "IpAddresses":{ 
                  "Instance0":"104.45.18.187",
                  "Instance1":"104.45.13.195"
               }
            },
            "connectionConfiguration":{ 
               "IsBgpEnabled":false,
               "PSK":"YLkSdSYd4wjjEThR3aIxaXaqNdxUwSo9",
               "IPsecParameters":{ 
                  "SADataSizeInKilobytes":102400000,
                  "SALifeTimeInSeconds":3600
               }
            }
         }
      ]
   }
  ```

## <a name="default"></a>IPsec 연결에 대한 기본 정책

### <a name="initiator"></a>시작자

다음 섹션에는 Azure가 터널의 시작자인 경우, 지원되는 정책 조합이 나와 있습니다.

**1단계**

* AES_256, SHA1, DH_GROUP_2
* AES_256, SHA_256, DH_GROUP_2
* AES_128, SHA1, DH_GROUP_2
* AES_128, SHA_256, DH_GROUP_2
* 3DES, SHA1, DH_GROUP_2
* 3DES, SHA_256, DH_GROUP_2

**2단계**

* GCM_AES_256, GCM_AES_256, PFS_NONE
* AES_256, SHA_1, PFS_NONE
* CBC_3DES, SHA_1, PFS_NONE
* AES_256, SHA_256, PFS_NONE
* AES_128, SHA_1, PFS_NONE
* CBC_3DES, SHA_256, PFS_NONE

### <a name="responder"></a>응답자

다음 섹션에는 Azure가 터널의 응답자인 경우, 지원되는 정책 조합이 나와 있습니다.

**1단계**

* AES_256, SHA1, DH_GROUP_2
* AES_256, SHA_256, DH_GROUP_2
* AES_128, SHA1, DH_GROUP_2
* AES_128, SHA_256, DH_GROUP_2
* 3DES, SHA1, DH_GROUP_2
* 3DES, SHA_256, DH_GROUP_2

**2단계**

* GCM_AES_256, GCM_AES_256, PFS_NONE
* AES_256, SHA_1, PFS_NONE
* CBC_3DES, SHA_1, PFS_NONE
* AES_256, SHA_256, PFS_NONE
* AES_128, SHA_1, PFS_NONE
* CBC_3DES, SHA_256, PFS_NONE
* CBC_DES, SHA_1, PFS_NONE 
* AES_256, SHA_1, PFS_1
* AES_256, SHA_1, PFS_2
* AES_256, SHA_1, PFS_14
* AES_128, SHA_1, PFS_1
* AES_128, SHA_1, PFS_2
* AES_128, SHA_1, PFS_14
* CBC_3DES, SHA_1, PFS_1
* CBC_3DES, SHA_1, PFS_2
* CBC_3DES, SHA_256, PFS_2
* AES_256, SHA_256, PFS_1
* AES_256, SHA_256, PFS_2
* AES_256, SHA_256, PFS_14
* AES_256, SHA_1, PFS_24
* AES_256, SHA_256, PFS_24
* AES_128, SHA_256, PFS_NONE
* AES_128, SHA_256, PFS_1
* AES_128, SHA_256, PFS_2
* AES_128, SHA_256, PFS_14
* CBC_3DES, SHA_1, PFS_14

### <a name="does-everything-need-to-match-between-the-virtual-hub-vpngateway-policy-and-my-on-premises-sdwanvpn-device-or-sd-wan-configuration"></a>가상 허브 vpngateway 정책과 온-프레미스 SDWAN/VPN 장치 또는 SD-WAN 구성 간에 모든 항목이 일치해야 하나요?

온-프레미스 SDWAN/VPN 장치 또는 SD-WAN 구성은 Azure IPsec/IKE 정책에서 지정한 다음과 같은 알고리즘 및 매개 변수와 일치하거나 해당 항목을 포함해야 합니다.

* IKE 암호화 알고리즘
* IKE 무결성 알고리즘
* DH 그룹
* IPsec 암호화 알고리즘
* IPsec 무결성 알고리즘
* PFS 그룹

## <a name="next-steps"></a>다음 단계

Virtual WAN에 대한 자세한 내용은 [Azure Virtual WAN 정보](virtual-wan-about.md) 및 [Azure Virtual WAN FAQ](virtual-wan-faq.md)를 참조하세요.

추가 정보는 <azurevirtualwan@microsoft.com>으로 이메일을 보내세요. 제목 줄에서 “[]”에 회사 이름을 적어주세요.
