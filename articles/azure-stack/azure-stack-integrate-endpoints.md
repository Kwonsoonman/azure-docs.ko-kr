---
title: Azure 데이터 센터 통합 Stack-끝점을 게시 | Microsoft Docs
description: 데이터 센터에서 Azure Stack 끝점을 게시 하는 방법 알아보기
services: azure-stack
author: jeffgilb
manager: femila
ms.service: azure-stack
ms.topic: article
ms.date: 12/06/2018
ms.author: jeffgilb
ms.reviewer: wamota
keywords: ''
ms.openlocfilehash: 1800ab19e2d99eb639ef4064e64d7bc475aa0c36
ms.sourcegitcommit: 698ba3e88adc357b8bd6178a7b2b1121cb8da797
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53014874"
---
# <a name="azure-stack-datacenter-integration---publish-endpoints"></a>Azure 데이터 센터 통합 스택-끝점 게시

Azure Stack 인프라 역할에 대 한 가상 IP 주소 (Vip)를 설정합니다. 이러한 Vip의 공용 IP 주소 풀에서 할당 됩니다. 각 VIP는 소프트웨어 정의 네트워크 계층에서 액세스 제어 목록 (ACL)을 사용 하 여 보호 됩니다. Acl은 솔루션 강화 (에서 및 BMC) 실제 스위치 간에 사용 됩니다. 배포 시 지정 된 외부 DNS 영역에서 각 끝점에 대 한 DNS 항목을 생성 됩니다.


다음 아키텍처 다이어그램은 서로 다른 네트워크 레이어 및 Acl을 보여 줍니다.

![구조적 그림](media/azure-stack-integrate-endpoints/Integrate-Endpoints-01.png)

## <a name="ports-and-protocols-inbound"></a>포트 및 프로토콜 (인바운드)

인프라 집합이 Vip 외부 네트워크에 Azure Stack 끝점 게시에 필요 합니다. 합니다 *끝점 (VIP)* 표에서 각 끝점에서 필요한 포트 및 프로토콜입니다. SQL 리소스 공급자와 같은 추가 리소스 공급자를 필요로 하는 끝점에 대 한 특정 리소스 공급자 배포 설명서를 참조 하십시오.

내부 인프라 Vip 게시 Azure Stack에 대 한 필수 이기 때문에 표시 되지 않습니다.

> [!Note]  
> 사용자 Vip는 Azure Stack 연산자가 없는 컨트롤을 사용 하 여 사용자가 정의 하는 동적입니다.

|끝점 (VIP)|DNS 호스트 A 레코드|프로토콜|포트|
|---------|---------|---------|---------|
|AD FS|Adfs.*&lt;region>.&lt;fqdn>*|HTTPS|443|
|포털 (관리자)|Adminportal 합니다.  *&lt;지역 >.&lt; fqdn >*|HTTPS|443<br>12495<br>12499<br>12646<br>12647<br>12648<br>12649<br>12650<br>13001<br>13003<br>13010<br>13011<br>13012<br>13020<br>13021<br>13026<br>30015|
|Adminhosting | *.adminhosting 합니다. \<지역 >. \<fqdn > | HTTPS | 443 |
|Azure 리소스 관리자 (관리자)|Adminmanagement 합니다.  *&lt;지역 >.&lt; fqdn >*|HTTPS|443<br>30024|
|포털 (사용자)|Portal.*&lt;region>.&lt;fqdn>*|HTTPS|443<br>12495<br>12649<br>13001<br>13010<br>13011<br>13012<br>13020<br>13021<br>30015<br>13003|
|Azure Resource Manager (사용자)|Management.*&lt;region>.&lt;fqdn>*|HTTPS|443<br>30024|
|그래프|Graph.*&lt;region>.&lt;fqdn>*|HTTPS|443|
|인증서 해지 목록|Crl.*&lt;region>.&lt;fqdn>*|HTTP|80|
|DNS|&#42;.*&lt;region>.&lt;fqdn>*|TCP 및 UDP|53|
|Hosting | *.hosting 합니다. \<지역 >. \<fqdn > | HTTPS | 443 |
|Key Vault (사용자)|&#42;.vault.*&lt;region>.&lt;fqdn>*|HTTPS|443|
|Key Vault (관리자)|&#42;.adminvault.*&lt;region>.&lt;fqdn>*|HTTPS|443|
|저장소 큐|&#42;.queue.*&lt;region>.&lt;fqdn>*|HTTP<br>HTTPS|80<br>443|
|저장소 테이블|&#42;.table.*&lt;region>.&lt;fqdn>*|HTTP<br>HTTPS|80<br>443|
|저장소 Blob|&#42;.blob.*&lt;region>.&lt;fqdn>*|HTTP<br>HTTPS|80<br>443|
|SQL 리소스 공급자|sqladapter.dbadapter.*&lt;region>.&lt;fqdn>*|HTTPS|44300-44304|
|MySQL 리소스 공급자|mysqladapter.dbadapter.*&lt;region>.&lt;fqdn>*|HTTPS|44300-44304|
|App Service|&#42;.appservice.*&lt;region>.&lt;fqdn>*|TCP|80 (HTTP)<br>443 (HTTPS)<br>8172 (MSDeploy)|
|  |&#42;.scm.appservice.*&lt;region>.&lt;fqdn>*|TCP|443 (HTTPS)|
|  |api.appservice.*&lt;region>.&lt;fqdn>*|TCP|443 (HTTPS)<br>44300 (azure Resource Manager)|
|  |ftp.appservice.*&lt;region>.&lt;fqdn>*|TCP, UDP|21, 1021, 10001-10100 (FTP)<br>990 (FTPS)|
|VPN Gateway|     |     |[VPN gateway FAQ를 참조 하세요.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq#can-i-traverse-proxies-and-firewalls-using-point-to-site-capability)합니다.|
|     |     |     |     |

## <a name="ports-and-urls-outbound"></a>포트 및 Url (아웃 바운드)

Azure Stack은 투명 프록시 서버만 지원 합니다. 배포의 경우 기존 프록시 서버에 투명 프록시 업링크를 허용 해야 합니다 다음 포트 및 Url 아웃 바운드 통신에:

> [!Note]  
> Azure Stack 다음 표에 나열 된 Azure 서비스에 연결할 Expressroute를 사용 하는 것을 지원 하지 않습니다.

|목적|URL|프로토콜|포트|
|---------|---------|---------|---------|
|ID|login.windows.net<br>login.microsoftonline.com<br>graph.windows.net<br>https://secure.aadcdn.microsoftonline-p.com<br>office.com|HTTP<br>HTTPS|80<br>443|
|마켓플레이스 배포|https://management.azure.com<br>https://&#42;.blob.core.windows.net<br>https://*.azureedge.net<br>https://&#42;.microsoftazurestack.com|HTTPS|443|
|패치 및 업데이트|https://&#42;.azureedge.net|HTTPS|443|
|등록|https://management.azure.com|HTTPS|443|
|사용 현황|https://&#42;.microsoftazurestack.com<br>https://*.trafficmanager.net|HTTPS|443|
|Windows Defender|. wdcp.microsoft.com<br>. wdcpalt.microsoft.com<br>*. updates.microsoft.com<br>*. download.microsoft.com<br>https://msdl.microsoft.com/download/symbols<br>http://www.microsoft.com/pkiops/crl<br>http://www.microsoft.com/pkiops/certs<br>http://crl.microsoft.com/pki/crl/products<br>http://www.microsoft.com/pki/certs<br>https://secure.aadcdn.microsoftonline-p.com<br>|HTTPS|80<br>443|
|NTP|(IP의 NTP 서버 배포에 대 한 제공)|UDP|123|
|DNS|(배포에 대해 제공 된 IP의 DNS 서버)|TCP<br>UDP|53|
|CRL|(인증서에 CRL 배포 지점 URL)|HTTP|80|
|인프라 백업|(IP 또는 FQDN 외부 대상 파일 서버)|SMB|445|
|     |     |     |     |

> [!Note]  
> 아웃 바운드 Url은 부하가 분산 된 Azure traffic manager를 사용 하 여 지리적 위치에 따라 가능한 최적의 연결을 제공 합니다. 부하 분산된 Url을 Microsoft에서 업데이트 하 고 고객에 게 영향을 주지 않고 백 엔드 끝점을 변경할 수 있습니다. Microsoft는 부하 분산 Url에 대 한 IP 주소 목록을 공유 하지 않습니다. IP 대신 하 여 URL 필터링을 지 원하는 장치를 사용 해야 합니다.

> [!Note]  
> 1809, 인프라 백업 서비스는 외부 파일 서버에 공용 VIP 네트워크에서 통신합니다. 1809를 하기 전에 서비스는 공용 인프라 네트워크를 통해 통신 합니다. 환경 액세스 인프라 리소스에 공용 VIP 네트워크에서 허용 하지 않으면 적용 최신 [1809 핫픽스](azure-stack-update-1809.md#post-update-steps) Azure Stack에 대 한 합니다. 이 핫픽스 공용 인프라 네트워크에 인프라 백업 서비스를 다시 이동 됩니다. 1811에서 1809 핫픽스를 적용 하는 경우 인프라 백업 서비스는 공용 인프라 네트워크에 남아 있습니다. 핫픽스를 적용 하지 않는 경우 업데이트를 다시 이동 공용 인프라 네트워크에 합니다.

## <a name="next-steps"></a>다음 단계

[Azure Stack PKI 요구 사항](azure-stack-pki-certs.md)
