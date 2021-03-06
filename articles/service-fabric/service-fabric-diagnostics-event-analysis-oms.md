---
title: Log Analytics를 사용하여 Azure Service Fabric 이벤트 분석 | Microsoft Docs
description: Azure Service Fabric 클러스터의 모니터링 및 진단을 위해 Log Analytics를 사용하여 이벤트를 시각화 및 분석하는 방법에 대해 알아봅니다.
services: service-fabric
documentationcenter: .net
author: srrengar
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2018
ms.author: srrengar
ms.openlocfilehash: 332939710517e99aaa77642dc5e67256b476bd66
ms.sourcegitcommit: c8088371d1786d016f785c437a7b4f9c64e57af0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52634578"
---
# <a name="event-analysis-and-visualization-with-log-analytics"></a>Log Analytics를 사용하여 이벤트 분석 및 시각화
 Log Analytics는 클라우드에서 호스팅되는 서비스 및 응용 프로그램에서 원격 분석 데이터를 수집 및 분석하고 가용성 및 성능을 극대화하는 데 도움이 되는 분석 도구를 제공합니다. 이 문서에서는 Log Analytics에서 쿼리를 실행하여 인사이트를 얻는 방법과 클러스터에서 발생하는 문제를 해결하는 방법에 대해 설명합니다. 다음과 같은 일반적인 질문을 해결합니다.

* 상태 이벤트 문제는 어떻게 해결하나요?
* 노드 작동이 중단되면 어떻게 알 수 있나요?
* 내 응용 프로그램의 서비스가 시작되거나 중지되는지 어떻게 알 수 있나요?

## <a name="log-analytics-workspace"></a>Log Analytics 작업 영역

>[!NOTE] 
>클러스터 생성 시 진단 스토리지가 기본으로 사용하도록 설정되어 있는 경우에도 진단 스토리지에서 읽도록 Log Analytics 작업 영역을 설정해야 합니다.

Log Analytics는 Azure Storage 테이블이나 에이전트를 비롯한 관리 리소스에서 데이터를 수집하여 중앙 리포지토리에서 유지 관리합니다. 그런 다음 데이터를 분석, 경고 및 시각화하거나 내보낼 수 있습니다. Log Analytics는 이벤트, 성능 데이터 또는 기타 사용자 지정 데이터를 지원합니다. 데이터가 Log Analytics로 흐르도록 하려면 [이벤트를 집계하도록 진단 확장을 구성하는 단계](service-fabric-diagnostics-event-aggregation-wad.md) 및 [저장소의 이벤트에서 읽을 Log Analytics 작업 영역을 만드는 단계](service-fabric-diagnostics-oms-setup.md)를 확인하세요.

Log Analytics가 데이터를 수신한 후 Azure에는 여러 시나리오로 사용자 지정된 들어오는 데이터를 모니터링하기 위해 미리 패키지화된 솔루션 또는 운영 대시보드인 다양한 *관리 솔루션*이 있습니다. 여기에는 Service Fabric 클러스터를 사용할 때 진단 및 모니터링과 가장 관련된 두 개의 솔루션인 *Service Fabric 분석* 솔루션과 *컨테이너* 솔루션이 포함됩니다. 이 문서에서는 작업 영역을 사용하여 만든 Service Fabric 분석 솔루션을 사용하는 방법을 설명합니다.

## <a name="access-the-service-fabric-analytics-solution"></a>Service Fabric 분석 솔루션에 액세스

1. Azure Portal에서 Service Fabric 분석 솔루션을 만든 리소스 그룹으로 이동합니다.

2. **ServiceFabric\<nameOfOMSWorkspace\>** 리소스를 선택합니다.

2. `Summary`에는 Service Fabric용 타일을 포함하여 활성화된 각 솔루션에 대해 그래프 형태의 타일이 표시됩니다. **Service Fabric** 그래프(아래 첫 번째 이미지)를 클릭하여 Service Fabric 분석 솔루션(아래 두 번째 이미지)을 계속합니다.

    ![Service Fabric 솔루션](media/service-fabric-diagnostics-event-analysis-oms/oms_service_fabric_summary.PNG)

    ![Service Fabric 솔루션](media/service-fabric-diagnostics-event-analysis-oms/oms_service_fabric_solution.PNG)

위 이미지는 Service Fabric 분석 솔루션의 홈 페이지입니다. 클러스터에서 수행되는 작업의 스냅샷 보기입니다. 클러스터를 만들 때 진단을 활성화하면 다음에 대한 이벤트를 볼 수 있습니다. 

* [Service Fabric 클러스터 이벤트](service-fabric-diagnostics-event-generation-operational.md)
* [Reliable Actors 프로그래밍 모델 이벤트](service-fabric-reliable-actors-diagnostics.md)
* [Reliable Services 프로그래밍 모델 이벤트](service-fabric-reliable-services-diagnostics.md)

>[!NOTE]
>즉시 사용이 가능한 Service Fabric 이벤트 외에도, [진단 확장 프로그램의 구성을 업데이트](service-fabric-diagnostics-event-aggregation-wad.md#log-collection-configurations)하여 더 자세한 시스템 이벤트를 수집할 수 있습니다.

### <a name="view-service-fabric-events-including-actions-on-nodes"></a>노드에 대한 작업을 비롯한 Service Fabric 이벤트 보기

1. Service Fabric 분석 페이지에서 **Service Fabric 이벤트**에 대한 그래프를 클릭합니다.

    ![Service Fabric 솔루션 조작 채널](media/service-fabric-diagnostics-event-analysis-oms/oms_service_fabric_events_selection.png)

2. **목록**을 클릭하여 목록에서 이벤트를 봅니다. 일단 여기에 수집된 모든 시스템 이벤트가 표시됩니다. 참고로, 이러한 항목은 Azure Storage 계정의 WADServiceFabricSystemEventsTable에서 가져오고 이와 유사하게 다음에 표시되는 Reliable Services 및 Actors 이벤트는 해당 테이블에서 가져옵니다.
    
    ![쿼리 조작 채널](media/service-fabric-diagnostics-event-analysis-oms/oms_service_fabric_events.png)

또는 왼쪽에 있는 돋보기를 클릭하고 Kusto 쿼리 언어를 사용하여 원하는 항목을 찾을 수 있습니다. 예를 들어 클러스터의 노드에서 수행된 모든 작업을 찾으려면 다음 쿼리를 사용하면 됩니다. 아래에 사용된 이벤트 ID는 [운영 채널 이벤트 참조](service-fabric-diagnostics-event-generation-operational.md)에서 찾을 수 있습니다.

```kusto
ServiceFabricOperationalEvent
| where EventId < 25627 and EventId > 25619 
```

특정 노드(컴퓨터), 시스템 서비스(TaskName) 같은 더 많은 필드를 쿼리할 수 있습니다.

### <a name="view-service-fabric-reliable-service-and-actor-events"></a>Service Fabric Reliable Service 및 Actor 이벤트 보기

1. Service Fabric 분석 페이지에서 **Reliable Services**에 대한 그래프를 클릭합니다.

    ![Service Fabric 솔루션 Reliable Services](media/service-fabric-diagnostics-event-analysis-oms/oms_reliable_services_events_selection.png)

2. **목록**을 클릭하여 목록에서 이벤트를 봅니다. 여기에서 Reliable Services의 이벤트를 볼 수 있습니다. 일반적으로 배포 및 업그레이드에서 발생하는 서비스 RunAsync가 언제 시작되고 완료되는지에 대한 다양한 이벤트를 볼 수 있습니다. 

    ![쿼리 Reliable Services](media/service-fabric-diagnostics-event-analysis-oms/oms_reliable_service_events.png)

Reliable Actors 이벤트는 비슷한 방식으로 볼 수 있습니다. Reliable Actors에 대한 자세한 이벤트를 구성하려면 진단 확장(아래 참조)에 대한 구성에서 `scheduledTransferKeywordFilter`를 변경해야 합니다. 이러한 값에 대한 세부 정보는 [Reliable Actors 이벤트 참조](service-fabric-reliable-actors-diagnostics.md#keywords)를 참조하세요.

```json
"EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
```

Kusto 쿼리 언어는 강력합니다. 실행 가능한 또 다른 중요한 쿼리는 가장 많은 이벤트를 생성하는 노드를 확인하는 것입니다. 아래 스크린샷의 쿼리는 특정 서비스 및 노드와 통합된 Service Fabric 운영 이벤트를 보여 줍니다.

![노드당 쿼리 이벤트](media/service-fabric-diagnostics-event-analysis-oms/oms_kusto_query.png)

## <a name="next-steps"></a>다음 단계

* 인프라 모니터링, 즉 성능 카운터를 사용하려면 [Log Analytics 에이전트 추가](service-fabric-diagnostics-oms-agent.md)를 참조하세요. 에이전트는 성능 카운터를 수집하여 기존 작업 영역에 추가합니다.
* 온-프레미스 클러스터의 경우 Log Analytics는 Log Analytics로 데이터를 보내는 데 사용할 수 있는 게이트웨이(HTTP 전달 프록시)를 제공합니다. 자세한 내용은 [Log Analytics 게이트웨이를 사용하여 인터넷 액세스 없이 Log Analytics에 컴퓨터 연결](../azure-monitor/platform/gateway.md)을 참조하세요.
* 감지 및 진단에 도움이 되는 [자동 경고](../log-analytics/log-analytics-alerts.md)를 구성합니다.
* Log Analytics의 일부로 제공되는 [로그 검색 및 쿼리](../log-analytics/log-analytics-log-searches.md) 기능을 알아봅니다.
* Log Analytics에 대한 자세한 개요와 제공되는 사항을 보려면 [Log Analytics란?](../operations-management-suite/operations-management-suite-overview.md)을 참조하세요.
