---
title: Azure CLI 예제 – Azure Media Services | Microsoft Docs
description: Azure Media Services 서비스용 Azure CLI 예제를 제공합니다.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.custom: ''
ms.date: 10/15/2018
ms.author: juliako
ms.openlocfilehash: 5559f9055da3a2a852427c0f27d367159cdc7655
ms.sourcegitcommit: f20e43e436bfeafd333da75754cd32d405903b07
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49388513"
---
# <a name="azure-cli-examples-for-azure-media-services"></a>Azure Media Services에 대한 Azure CLI 예제

다음 표에는 Azure Media Services용 Azure CLI 예제의 링크가 포함되어 있습니다.

|  |  |
|---|---|
|**계정**||
| [Media Services 계정 만들기](./scripts/cli-create-account.md) | Azure Media Services 계정을 만듭니다. 또한 프로그래밍 방식으로 계정을 관리하기 위해 API에 액세스하는 데 사용할 수 있는 서비스 주체를 만듭니다. |
| [계정 자격 증명 다시 설정](./scripts/cli-reset-account-credentials.md)|계정 자격 증명을 다시 설정하고 app.config 설정을 되돌립니다.|
|**Assets**||
| [자산 만들기](./scripts/cli-create-asset.md)|콘텐츠를 업로드 할 Media Services Asset을 만듭니다.|
| [파일 업로드](./scripts/cli-upload-file-asset.md)|저장소 컨테이너에 로컬 파일을 업로드합니다.|
| [자산 게시](./scripts/cli-publish-asset.md)| 스트리밍 로케이터를 만들고 스트리밍 URL을 다시 가져옵니다. |
| **Transforms** 및 **Jobs**||
| [변환 만들기](./scripts/cli-create-transform.md)|변환을 만드는 방법을 보여줍니다. Transform은 비디오 또는 오디오 파일(흔히 "레시피"라고도 함)을 처리하는 간단한 작업 워크플로를 설명합니다.<br/> 원하는 이름 및 "레시피"를 가진 Transform이 이미 존재하는지 항상 확인해야 합니다. 그렇지 않으면 다시 사용합니다. |
| [작업 만들기](./scripts/cli-create-jobs.md)|HTTPs URL을 사용하여 작업을 간단한 인코딩 Transform에 제출합니다.|
| [EventGrid 만들기](./scripts/cli-create-event-grid.md)|Job State Changes에 대한 계정 수준 Event Grid 구독을 만듭니다.|

## <a name="see-also"></a>참고 항목

[Azure CLI](https://docs.microsoft.com/cli/azure/ams?view=azure-cli-latest)
