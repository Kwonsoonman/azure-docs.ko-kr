---
title: 포함 파일
description: 포함 파일
services: batch
author: dlepow
ms.service: batch
ms.topic: include
ms.date: 10/11/2018
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: c98a2146a019817152be9fae76638dbaa4d9de3d
ms.sourcegitcommit: 4eddd89f8f2406f9605d1a46796caf188c458f64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49458860"
---
| **리소스** | **기본 제한** | **최대 제한** |
| --- | --- | --- |
| 구독당 지역별 Batch 계정 | 1 - 3 |50 |
| Batch 계정당 전용 코어 | 10 - 100 | 해당 없음<sup>1</sup> |
| Batch 계정당 낮은 우선 순위의 코어 수 | 10 - 100 | 해당 없음<sup>2</sup> |
| Batch 계정당 활성 작업 및 작업 일정<sup>3</sup> | 100 - 300 | 1000<sup>4</sup> |
| Batch 계정당 풀 | 20 - 100 | 500<sup>4</sup> |

> [!NOTE]
> 기본 제한은 Batch 계정을 만드는 데 사용되는 구독 유형에 따라 달라집니다. 표시된 코어 할당량은 Batch 서비스 모드의 Batch 계정에 대한 할당량입니다. [배치 계정에서 할당량을 봅니다](../articles/batch/batch-quota-limit.md#view-batch-quotas). 

<sup>1</sup> Batch 계정당 전용 코어 수는 늘릴 수 있지만, 최대 수는 지정되지 않습니다. 증가 옵션은 고객 지원에 문의하세요.

<sup>2</sup> Batch 계정당 낮은 우선 순위 코어 수는 늘릴 수 있지만, 최대 수는 지정되지 않습니다. 증가 옵션은 고객 지원에 문의하세요.

<sup>3</sup> 완료된 작업 및 작업 일정은 제한되지 않습니다.

<sup>4</sup> 이 제한을 초과하여 늘리려면 Azure 고객 지원에 문의합니다.
