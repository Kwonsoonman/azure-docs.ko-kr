---
title: IoT Hub에 대한 Event Grid, 라우팅 비교 | Microsoft Docs
description: IoT Hub은 자체 메시지 라우팅 서비스를 제공하지만, 또한 Event Grid와 통합하여 이벤트 게시를 합니다. 두 기능을 비교합니다.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 01/30/2018
ms.author: kgremban
ms.openlocfilehash: 3d52ca0c7022e08655ece8775b5855f3ae985aca
ms.sourcegitcommit: 609c85e433150e7c27abd3b373d56ee9cf95179a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48247455"
---
# <a name="compare-message-routing-and-event-grid-for-iot-hub"></a>IoT Hub에 대한 메시지 라우팅과 Event Grid 비교

Azure IoT Hub는 연결된 장치에서 데이터를 스트림하고 해당 데이터를 비즈니스 응용 프로그램에 통합하는 기능을 제공합니다. IoT Hub는 IoT 이벤트를 다른 Azure 서비스 또는 비즈니스 응용 프로그램에 통합하기 위한 두 가지 방법을 제공합니다. 이 아티클에서는 이 기능을 제공하여 시나리오에 가장 적합한 옵션을 선택할 수 있도록 하는 두 가지 기능을 설명합니다.

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-partial.md)]

* **[IoT Hub 메시지 라우팅](iot-hub-devguide-messages-d2c.md)**: 이 IoT Hub 기능을 사용하면 사용자가 Azure Storage 컨테이너, Event Hubs, Service Bus 큐 및 Service Bus 토픽과 같은 서비스 엔드포인트에 장치-클라우드 메시지를 라우팅할 수 있습니다. 라우팅은 엔드포인트에 라우팅하기 전에 데이터를 필터링하는 쿼리 기능도 제공합니다. 장치 원격 분석 데이터 외에도 작업을 트리거하는 데 사용할 수 있는 [원격 분석 이외 이벤트](iot-hub-devguide-messages-d2c.md#non-telemetry-events)를 보낼 수도 있습니다. 

* **Event Grid와 IoT Hub 통합**: Azure Event Grid는 게시-구독 모델을 사용하여 완전히 관리되는 이벤트 라우팅 서비스입니다. IoT Hub 및 Event Grid는 거의 실시간으로 [IoT Hub 이벤트를 Azure 및 외부 Azure 서비스에 통합](iot-hub-event-grid.md)하기 위해 함께 작동합니다. 

## <a name="similarities-and-differences"></a>유사성 및 차이점

메시지 라우팅 및 Event Grid가 경고 구성을 사용하도록 설정하는 한편 둘 사이에는 몇 가지 주요 차이점이 있습니다. 자세한 내용은 다음 표를 참조하세요.

| 기능 | IoT Hub 메시지 라우팅 | Event Grid와 IoT Hub 통합 |
| ------- | --------------- | ---------- |
| **장치 메시지** | 예, 메시지 라우팅을 원격 분석 데이터에 사용할 수 있습니다. | 아니요, Event Grid는 비-원격 분석 IoT Hub 이벤트에만 사용할 수 있습니다. |
| **이벤트 유형** | 예, 메시지 라우팅은 쌍 변경 및 장치 수명 주기 이벤트를 보고할 수 있습니다. | 예, Event Grid는 IoT Hub에서 장치가 생성, 삭제, 연결 및 연결 해제되면 보고할 수 있습니다. |
| **순서 지정** | 예, 이벤트 순서가 유지 관리됩니다.  | 아니요, 이벤트 순서가 보장되지 않습니다. | 
| **최대 메시지 크기** | 256 KB, 장치-클라우드 | 64KB |
| **필터링** | 메시지 응용 프로그램 속성, 메시지 시스템 속성, 메시지 본문, 장치 쌍 태그 및 장치 쌍 속성에 대한 다양한 필터링입니다. 예를 보려면 [메시지 라우팅 쿼리 구문](iot-hub-devguide-routing-query-syntax.md)을 참조하세요. | 장치 ID의 접두사/접미사에 기반하는 필터링으로 저장소와 같은 계층적 서비스에서 잘 작동합니다. |
| **엔드포인트** | <ul><li>Event Hubs</li> <li>Azure Blob Storage</li> <li>Service Bus 큐</li> <li>Service Bus 토픽</li></ul><br>유료 IoT Hub SKU(S1, S2, S3)은 사용자 지정 엔드포인트 10개로 제한됩니다. IoT Hub당 100 경로를 만들 수 있습니다. | <ul><li>Azure 기능</li> <li>Azure Automation</li> <li>Event Hubs</li> <li>Logic Apps</li> <li>저장소 Blob</li> <li>사용자 지정 토픽</li> <li>Webhook 통한 다른 공급 업체 서비스</li></ul><br>엔드포인트 최신 목록은 [Event Grid 이벤트 처리기](../event-grid/overview.md#event-handlers)를 참조하세요. |
| **비용** | 메시지 라우팅에 대한 별도의 요금은 없습니다. IoT Hub로의 원격 분석 수신만 청구됩니다. 예를 들어 세 가지 다른 엔드포인트로 라우팅되는 메시지가 있을 경우 하나의 메시지에 대해서만 요금이 청구됩니다. | IoT Hub는 무료입니다. Event Grid는 월 당 첫 100,000 작업을 무료로 제공하고 그 후 백만 작업을 $0.60에 제공합니다. |

IoT Hub 메시지 라우팅 및 Event Grid는 또한 유사성을 가졌으며, 그 중 일부는 다음 테이블에 자세히 나와 있습니다.

| 기능 | IoT Hub 메시지 라우팅 | Event Grid와 IoT Hub 통합 |
| ------- | --------------- | ---------- |
| **신뢰성** | 높음: 각 경로에 대해 최소 한 번씩 엔드포인트에 각 메시지를 배달합니다. 한 시간 내에 배달되지 않는 모든 메시지에 만료됩니다. | 높음: 각 구독에 대해 각 메시지를 최소 한 번 웹후크에 배달합니다. 24시간 이내에 배달되지 않는 모든 이벤트 만료됩니다. | 
| **확장성** | 높음: 수백만 대의 동시에 연결된 장치가 수십억 개의 메시지를 보내는 것을 지원하도록 최적화됩니다. | 높음: 지역마다 초당 10,000,000 이벤트 라우팅이 가능합니다. |
| **대기 시간** | 낮음: 거의 실시간. | 낮음: 거의 실시간. |
| **여러 엔드포인트로 보냄** | 예, 단일 메시지를 여러 엔드포인트에 보냅니다. | 예, 단일 메시지를 여러 엔드포인트에 보냅니다.  | 
| **보안** | IoT Hub는 장치 단위 ID 및 취소 가능한 액세스 제어를 제공합니다. 자세한 내용은 [IoT Hub 액세스 제어](iot-hub-devguide-security.md)를 참조하세요. | Event Grid는 이벤트 구독, 이벤트 게시 및 웹후크 이벤트 전달이라는 세 지점에 대한 유효성 검사를 제공합니다. 자세한 내용은 [Event Grid 보안 및 인증](../event-grid/security-authentication.md)을 참조하세요. |

## <a name="how-to-choose"></a>선택 방법

IoT Hub 메시지 라우팅 및 Event Grid와 IoT Hub 통합은 비슷한 결과를 달성하기 위해 다른 작업을 수행합니다. 둘 다 IoT Hub 솔루션에서 정보를 받아 전달하여 다른 서비스가 반응할 수 있게 합니다. 어떤 것을 사용할지 어떻게 결정합니까? 결정을 하는 데 도움이 되도록 이전 섹션의 데이터 외에도 다음과 같은 질문을 사용합니다. 

* **엔드포인트에 어떤 종류의 데이터를 보냅니까?**

   원격 분석 데이터를 다른 서비스에 전송해야 할 경우 IoT Hub 메시지 라우팅을 사용합니다. 메시지 라우팅을 통해 메시지 응용 프로그램 및 시스템 속성, 메시지 본문, 장치 쌍 태그 및 장치 쌍 속성을 쿼리할 수도 있습니다.

   Event Grid와 IoT Hub 통합은 IoT Hub 서비스에서 발생하는 이벤트와 함께 작동합니다. 이러한 IoT Hub 이벤트에는 장치 생성, 삭제, 연결 및 연결 해제가 포함됩니다. 

* **이 정보를 수신하려면 어떤 엔드포인트가 필요하나요?**

   IoT Hub 메시지 라우팅은 제한된 엔드포인트를 지원하지만 커넥터가 데이터 및 이벤트를 추가 엔드포인트로 다시 라우팅하도록 빌드할 수 있습니다. 지원되는 엔드포인트의 전체 목록은, 이전 섹션의 테이블을 참조합니다. 

   Event Grid와 IoT Hub 통합은 더 많은 엔드포인트를 지원합니다. 또한 웹후크와 함께 작동하여 라우팅을 Azure 서비스 생태계 외부 및 타사 비즈니스 응용 프로그램으로 확장합니다. 

* **데이터가 순서대로 도착하는 것이 중요합니까?**

   IoT Hub 메시지 라우팅은 메시지를 보낸 순서를 유지 관리하여 같은 방식으로 도착하게 합니다.

   Event Grid는 발생했던 순서와 같은 순서로 엔드포인트가 이벤트를 받도록 보장하지 않습니다. 그러나 이벤트 스키마는 이벤트가 엔드포인트에 도착한 후에 순서를 식별하는 데 사용할 수 있는 타임스탬프를 포함합니다. 

## <a name="next-steps"></a>다음 단계

* [IoT Hub 메시지 라우팅](iot-hub-devguide-messages-d2c.md) 및 [IoT Hub 엔드포인트](iot-hub-devguide-endpoints.md)에 대해 자세히 알아봅니다.
* [Azure Event Grid](../event-grid/overview.md)에 대해 자세히 알아보기
* 메시지 경로를 만드는 방법에 대한 자세한 내용은 [경로를 사용하여 IoT Hub 장치-클라우드 메시지 처리](../iot-hub/tutorial-routing.md) 자습서를 참조하세요.
* [Logic Apps를 사용하여 Azure IoT Hub 이벤트에 관한 이메일 알림 보내기](../event-grid/publish-iot-hub-events-to-logic-apps.md)로 Event Grid 통합을 시도해 봅니다.