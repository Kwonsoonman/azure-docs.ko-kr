---
title: Azure(대규모 인스턴스)의 SAP HANA 용어 알아보기 | Microsoft Docs
description: Azure(대규모 인스턴스)의 SAP HANA에 대한 용어를 살펴볼 수 있습니다.
services: virtual-machines-linux
documentationcenter: ''
author: RicksterCDN
manager: jeconnoc
editor: ''
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/20/2018
ms.author: saghorpa
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 902c4c94cc7366af342816e9b4776af603711c8b
ms.sourcegitcommit: 8d88a025090e5087b9d0ab390b1207977ef4ff7c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52275443"
---
# <a name="know-the-terms"></a>용어 알아보기

아키텍처 및 기술적 배포 가이드에는 여러 가지 일반적인 정의가 광범위하게 사용됩니다. 다음 용어와 의미에 유의합니다.

- **IaaS**: Infrastructure as a Service
- **PaaS**: Platform as a Service
- **SaaS**: Software as a service
- **SAP 구성 요소**: ECC(ERP 중앙 구성 요소), BW(비즈니스 웨어하우스), 솔루션 관리자 또는 EP(엔터프라이즈 포털)과 같은 개별 SAP 응용 프로그램입니다. SAP 구성 요소는 기존의 ABAP 또는 Java 기술을 기반으로 하거나 비즈니스 개체와 같은 비NetWeaver 기반 응용 프로그램을 기반으로 사용할 수 있습니다.
- **SAP 환경:** 개발, 품질 보증, 교육, 재해 복구 또는 프로덕션과 같은 비즈니스 기능을 수행하기 위해 논리적으로 그룹화된 하나 이상의 SAP 구성 요소입니다.
- **SAP 자산:** IT 환경의 SAP 자산 전체를 나타냅니다. SAP 지형에는 모든 프로덕션 및 비프로덕션 환경이 포함됩니다.
- **SAP 시스템**: DBMS 계층과 응용 프로그램 계층(예: SAP ERP 개발 시스템, SAP BW 테스트 시스템, SAP CRM 프로덕션 시스템)의 조합입니다. Azure 배포는 온-프레미스와 Azure 간에 이러한 두 계층의 분할을 지원하지 않습니다. SAP 시스템은 온-프레미스 또는 Azure에 배포됩니다. SAP 자산의 서로 다른 시스템은 Azure 또는 온-프레미스에 배포할 수 있습니다. 예를 들어 Azure에는 SAP CRM 개발 및 테스트 시스템을 배포하고, 온-프레미스에는 SAP CRM 프로덕션 시스템을 배포할 수 있습니다. SAP HANA on Azure(대규모 인스턴스)의 경우 VM에서 SAP 시스템의 SAP 응용 프로그램 계층을 호스팅하고, SAP HANA on Azure(대규모 인스턴스) 스탬프의 장치에서 관련된 SAP HANA 인스턴스를 호스팅하기 위한 것입니다.
- **대규모 인스턴스 스탬프:** SAP HANA TDI 인증을 받고 Azure 내에서 SAP HANA 인스턴스를 전용으로 실행하는 하드웨어 인프라 스택입니다.
- **SAP HANA on Azure(대규모 인스턴스):** 여러 Azure 지역의 대규모 인스턴스 스탬프에 배포된 SAP HANA TDI 인증 하드웨어에서 HANA 인스턴스를 실행하는 Azure 제품에 대한 공식 이름입니다. *HANA 대규모 인스턴스* 관련 용어는 *SAP HANA on Azure(대규모 인스턴스)* 의 약어이며 기술적 배포 가이드에서 널리 사용됩니다.
- **프레미스 간**: VM이 온-프레미스 데이터 센터와 Azure 간에 사이트 간, 다중 사이트 또는 ExpressRoute 방식으로 연결된 Azure 구독에 배포되는 시나리오를 설명합니다. 공통 Azure 설명서에서 이러한 종류의 배포를 크로스-프레미스 시나리오라고도 합니다. 이러한 연결은 온-프레미스 도메인, 온-프레미스 Azure Active Directory/OpenLDAP 및 온-프레미스 DNS를 Azure로 확장하기 위한 것입니다. 온-프레미스 배경은 Azure 구독의 Azure 자산으로 확장됩니다. 이 확장을 사용하면 VM이 온-프레미스 도메인에 속할 수 있습니다. 

   온-프레미스 도메인의 도메인 사용자는 서버에 액세스하고, 이러한 VM에서 서비스(예: DBMS 서비스)를 실행할 수 있습니다. 온-프레미스에 배포된 VM과 Azure에 배포된 VM 간의 통신 및 이름 확인이 가능합니다. 이 시나리오는 대부분의 SAP 자산이 배포되는 전형적인 방식입니다. 자세한 내용은 [Azure VPN Gateway 계획 및 설계](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 및 [Azure Portal을 사용하여 사이트 간 연결이 있는 가상 네트워크 만들기](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
- **테넌트:** HANA 대규모 인스턴스 스탬프에 배포된 고객은 *테넌트*로 격리됩니다. 테넌트는 네트워킹, 저장소 및 계산 계층에서 다른 테넌트로부터 격리됩니다. 다른 테넌트에 할당된 저장소 및 계산 장치는 HANA 대규모 인스턴스 스탬프 수준에서 서로 표시하거나 통신할 수 없습니다. 고객은 다양한 테넌트에 배포하도록 선택할 수 있습니다. 그러한 경우에도 HANA 대규모 인스턴스 스탬프 수준에서 테넌트 간 통신은 없습니다.
- **SKU 범주:** HANA 대규모 인스턴스의 경우 SKU는 다음 두 가지 범주로 제공됩니다.
    - **유형 I 클래스**: S72, S72m, S96, S144, S144m, S192, S192m 및 S192xm
    - **유형 II 클래스**: S384, S384m, S384xm, S384xxm, S576m, S576xm, S768m, S768xm 및 S960m


클라우드에서 SAP 워크로드를 배포하는 방법에 대해 다양한 추가 리소스를 사용할 수 있습니다. Azure에서 SAP HANA 배포를 실행하려는 경우, Azure IaaS의 원칙 및 Azure IaaS에 대한 SAP 워크로드 배포를 경험하고 숙지해야 합니다. 계속하기 전에 먼저 [Azure 가상 머신에서 SAP 솔루션 사용](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요. 

**다음 단계**
- [HLI 인증](hana-certification.md) 참조