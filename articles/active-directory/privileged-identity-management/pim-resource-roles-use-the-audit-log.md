---
title: PIM에서 Azure 리소스 역할에 대한 감사 기록 보기 | Microsoft Docs
description: Azure AD PIM(Privileged Identity Management)에서 Azure 리소스 역할에 대한 감사 기록을 보는 방법을 알아봅니다.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: pim
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: c0536423e9640f78149b612ec66b0a07cdcf24bb
ms.sourcegitcommit: 63613e4c7edf1b1875a2974a29ab2a8ce5d90e3b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43189314"
---
# <a name="view-audit-history-for-azure-resource-roles-in-pim"></a>PIM에서 Azure 리소스 역할에 대한 감사 기록 보기

리소스 감사에서는 리소스에 대한 모든 역할 활동에 대한 보기를 제공합니다. 미리 정의된 날짜 또는 사용자 지정 범위를 사용하여 정보를 필터링할 수 있습니다.
![필터 정보](media/azure-pim-resource-rbac/rbac-resource-audit.png)

또한 리소스 감사를 통해 사용자의 작업 세부 정보에 신속하게 액세스할 수 있습니다. **감사 형식**에서 **활성화**를 선택합니다. Azure 리소스에서 해당 사용자의 작업을 확인하려면 **(작업)** 을 선택합니다.
![작업 세부 정보](media/azure-pim-resource-rbac/rbac-audit-activity.png)

![더 많은 작업 세부 정보](media/azure-pim-resource-rbac/rbac-audit-activity-details.png)

## <a name="my-audit"></a>내 감사

내 감사에서는 사용자의 개인 역할 작업 보기를 제공합니다. 미리 정의된 날짜 또는 사용자 지정 범위를 사용하여 정보를 필터링할 수 있습니다.
![개인 역할 작업](media/azure-pim-resource-rbac/my-audit-time.png)

## <a name="view-activation-and-azure-resource-activity"></a>활성화 및 Azure 리소스 활동 보기

특정 사용자가 다양한 리소스에서 수행한 작업을 살펴보려면 특정 활성화 기간에 연결된 Azure 리소스 작업을 검토하면 됩니다. 먼저 **구성원** 보기 또는 특정 역할의 구성원 목록에서 사용자를 선택합니다. Azure 리소스에서 사용자가 수행한 작업이 날짜별로 그래픽으로 표시됩니다. 같은 기간에 이루어진 최근 역할 활성화도 표시됩니다.

![사용자 세부 정보](media/azure-pim-resource-rbac/rbac-user-details.png)

특정 역할 활성화를 선택하면 역할 활성화 세부 정보와 해당 사용자가 활성화된 동안 발생한 해당 Azure 리소스 작업이 표시됩니다.

![역할 활성화 선택](media/azure-pim-resource-rbac/rbac-user-resource-activity.png)

## <a name="next-steps"></a>다음 단계

- [PIM에서 Azure AD 디렉터리 역할에 대한 감사 기록 보기](pim-how-to-use-audit-log.md)
