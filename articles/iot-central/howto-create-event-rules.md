---
title: Azure IoT Central 응용 프로그램에서 이벤트 규칙 만들기 및 관리 | Microsoft Docs
description: Azure IoT Central 이벤트 규칙을 사용하여 장치를 거의 실시간으로 모니터링하고, 규칙이 트리거되면 이메일 보내기 등의 작업을 자동으로 호출합니다.
author: ankitgupta
ms.author: ankitgup
ms.date: 08/14/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 889f3928ee72c035035abb635eb71ec0b06a3b45
ms.sourcegitcommit: 1b561b77aa080416b094b6f41fce5b6a4721e7d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2018
ms.locfileid: "45730163"
---
# <a name="create-an-event-rule-and-set-up-notifications-in-your-azure-iot-central-application"></a>Azure IoT Central 응용 프로그램에서 이벤트 규칙을 만들고 알림 설정

*이 문서는 운영자, 빌더 및 관리자에게 적용됩니다.*

Azure IoT Central을 사용하여 원격으로 연결된 장치를 모니터링할 수 있습니다. Azure IoT Central 규칙을 사용하여 장치를 거의 실시간으로 모니터링하고, 이메일 보내기 또는 Microsoft Flow 트리거 등의 작업을 자동으로 호출합니다. 클릭 몇 번으로 장치 데이터를 모니터링하는 조건을 정의하고 해당 작업을 구성할 수 있습니다. 이 문서에서는 장치에서 보낸 이벤트를 모니터링하는 규칙을 만드는 방법을 설명합니다.

장치는 이벤트 측정을 사용하여 중요하거나 정보 제공용 장치 이벤트를 보낼 수 있습니다. 선택한 장치 이벤트를 장치에서 보고하면 이벤트 규칙이 트리거됩니다.

## <a name="create-an-event-rule"></a>이벤트 규칙 만들기

이벤트 규칙을 만들려면 장치 템플릿에 하나 이상의 이벤트 측정이 정의되어 있어야 합니다. 이 예제에서는 팬 모터 오류 이벤트를 보고하는 냉장 자동 판매기 장치를 사용합니다. 이 규칙은 장치에서 보고한 이벤트를 모니터링하다가 이벤트가 보고될 때마다 이메일을 보냅니다.

1. Device Explorer를 사용하여 규칙을 추가하려는 장치 템플릿으로 이동합니다.

1. 선택한 템플릿에서 기존 장치를 클릭합니다. 

    >[!TIP] 
    >템플릿에 장치가 없는 경우 새 장치를 먼저 추가합니다.

1. 아직 규칙을 하나도 만들지 않은 경우 다음 화면이 표시됩니다.

    ![규칙 없음](media\howto-create-event-rules\Rules_Landing_Page.png)


1. **규칙** 탭에서 **템플릿 편집**을 클릭한 후 **+ 새 규칙**을 클릭하여 만들 수 있는 규칙 유형을 확인합니다.


1. **이벤트** 타일을 클릭하여 이벤트 모니터링 규칙을 만듭니다.

    ![규칙 유형](media\howto-create-event-rules\Rule_Types.png)

    
1. 이 장치 템플릿에서 규칙을 식별하는 데 도움이 되는 이름을 입력합니다.

1. 이 템플릿에서 만든 모든 장치에 즉시 규칙을 사용하려면 **이 템플릿의 모든 장치에 규칙 사용**으로 전환합니다.

    ![규칙 세부 정보](media\howto-create-event-rules\Rule_Detail.png)

    규칙은 장치 템플릿 아래에 있는 모든 장치에 자동으로 적용됩니다.

### <a name="configure-the-rule-conditions"></a>규칙 조건 구성

조건은 규칙이 모니터링하는 기준을 정의합니다.

1. 새 조건을 추가하려면 **조건** 옆에 있는 **+** 를 선택합니다.

1. 단위 드롭다운에서 모니터링하려는 이벤트를 선택합니다. 이 예제에서는 **팬 모터 오류** 이벤트를 선택했습니다.

   ![조건](media\howto-create-event-rules\Condition_Filled_Out.png) 


1. 필요에 따라 **집계**로 **Count**를 설정하고 해당 임계값을 제공할 수도 있습니다.

    - 집계를 사용하지 않으면 조건을 충족하는 각 이벤트 데이터 요소에 대해 규칙이 트리거됩니다. 예를 들어 '팬 모터 오류' 이벤트가 발생할 때 트리거할 규칙의 조건을 구성하는 경우 장치에서 해당 이벤트를 보고하는 경우 거의 즉시 규칙이 트리거됩니다.
    - 집계 함수로 Count가 사용되는 경우 사용자는 조건을 평가할 **임계값** 및 **집계 기간**을 제공해야 합니다. 이 경우 이벤트 수가 집계되고 집계된 이벤트 수가 임계값과 일치하는 경우에만 규칙이 트리거됩니다.
 
    예를 들어 5분 내에 세 개 초과의 장치 이벤트가 있을 때 경고하려는 경우 이벤트를 선택하고 집계 함수를 "count"로, 연산자를 "greater than"으로, "임계값"을 3으로 설정합니다. "집계 기간"을 "5분"으로 설정합니다. 5분 내에 세 개 초과의 이벤트가 장치에서 전송되면 규칙이 트리거됩니다. 규칙 평가 주기는 **집계 기간**과 동일합니다. 즉, 이 예제에서 규칙은 5분에 한 번 평가됩니다. 

    ![이벤트 조건 추가](media\howto-create-event-rules\Aggregate_Condition_Filled_Out.png)

    >[!NOTE] 
    >**조건** 아래에 둘 이상의 이벤트 측정값을 추가할 수 있습니다. 조건을 여러 개 지정하는 경우 모든 조건을 충족해야 규칙이 트리거됩니다. 각 조건은 'AND' 절을 사용하여 암시적으로 조인됩니다. 집계를 사용할 경우 모든 측정값이 집계되어야 합니다.

### <a name="configure-actions"></a>작업 구성

이 섹션에서는 규칙이 실행될 때 수행할 작업을 설정하는 방법을 보여줍니다. 규칙에 지정된 모든 조건이 true로 평가될 경우 작업이 호출됩니다.

1. **작업** 옆에 있는 **+** 기호를 선택합니다. 사용 가능한 작업 목록을 표시됩니다. 

    ![작업 추가](media\howto-create-event-rules\Add_Action.png)

1. **이메일** 작업을 선택하고, **받는 사람** 필드에 유효한 이메일 주소를 입력하고, 규칙이 트리거될 때 이메일 본문에 표시할 메모를 입력합니다.

    > [!NOTE]
    > 응용 프로그램에 추가되어 한 번 이상 로그인한 사용자에게만 이메일이 발송됩니다. Azure IoT Central에서 [사용자 관리](howto-administer.md)에 대해 자세히 알아보세요.

   ![작업 구성](media\howto-create-event-rules\Configure_Action.png)

1. 규칙을 저장하려면 **저장**을 선택합니다. 몇 분 이내에 규칙이 적용되어 응용 프로그램으로 전송되는 이벤트의 모니터링이 시작됩니다. 규칙에 지정된 조건이 일치하는 경우 규칙이 구성된 이메일 작업을 트리거합니다.

1. **완료**를 선택하여 **템플릿 편집** 모드를 종료합니다.

Microsoft Flow 및 webhook와 같은 다른 작업을 규칙에 추가할 수 있습니다. 규칙당 최대 5개의 작업을 추가할 수 있습니다.

- [Microsoft Flow 작업](howto-add-microsoft-flow.md): 규칙이 트리거되면 Microsoft Flow에서 워크플로를 시작합니다. 
- [웹후크 작업](howto-create-webhooks.md): 규칙이 트리거되면 다른 서비스에 알립니다.

## <a name="parameterize-the-rule"></a>규칙 매개 변수화

**장치 속성**을 매개 변수로 사용하여 작업을 구성할 수도 있습니다. 이메일 주소가 장치 속성으로 저장되는 경우 **받는 사람** 주소를 정의할 때 사용할 수 있습니다.

## <a name="delete-a-rule"></a>규칙 삭제

규칙이 더 이상 필요 없으면 해당 규칙을 열고 **삭제**를 선택하여 삭제할 수 있습니다. 규칙을 삭제하면 장치 템플릿 및 모든 관련 장치에서 해당 규칙이 제거됩니다.

## <a name="enable-or-disable-a-rule-for-a-device-template"></a>장치 템플릿에 규칙을 사용하도록 또는 사용하지 않도록 설정

해당 장치로 이동하여 사용하도록 또는 사용하지 않도록 설정할 규칙을 선택합니다. **이 템플릿의 모든 장치에 규칙 사용** 단추를 누르면 장치 템플릿과 연결된 모든 장치에 규칙을 사용하도록 또는 사용하지 않도록 설정됩니다.

## <a name="enable-or-disable-a-rule-for-a-device"></a>장치에 규칙을 사용하도록 또는 사용하지 않도록 설정

해당 장치로 이동하여 사용하도록 또는 사용하지 않도록 설정할 규칙을 선택합니다. **이 장치에 규칙 사용** 단추를 눌러 해당 장치에 규칙을 사용하도록 또는 사용하지 않도록 설정합니다.

## <a name="next-steps"></a>다음 단계

Azure IoT Central 응용 프로그램에서 규칙을 만드는 방법을 알아보았으니, 다음과 같은 후속 단계를 진행하시기 바랍니다.

- [규칙에 Microsoft Flow 작업 추가](howto-add-microsoft-flow.md)
- [규칙에 Webhook 작업 추가](howto-create-webhooks.md)
- [장치를 관리하는 방법](howto-manage-devices.md)
