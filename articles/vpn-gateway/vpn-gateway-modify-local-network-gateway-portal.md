---
title: 로컬 네트워크 게이트웨이 IP 주소 접두사 및 VPN Gateway IP 주소 수정 | Azure | Portal | Microsoft Docs
description: 이 문서는 Azure Portal을 사용하여 로컬 네트워크 게이트웨이에 대한 IP 주소 접두사를 변경하는 방법을 안내합니다.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 12f1f8bbcb103d0882059cadc12bc1a8b9d40bdb
ms.sourcegitcommit: 07a09da0a6cda6bec823259561c601335041e2b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2018
ms.locfileid: "49404548"
---
# <a name="modify-local-network-gateway-settings-using-the-azure-portal"></a>Azure Portal을 사용하여 로컬 네트워크 게이트웨이 설정 수정

때로는 로컬 네트워크 게이트웨이 AddressPrefix 또는 GatewayIPAddress에 대한 설정을 변경합니다. 이 문서는 로컬 네트워크 게이트웨이 설정을 수정하는 방법을 안내합니다. 다음 목록에서 다른 옵션을 선택해 다른 방법으로 이러한 설정을 수정할 수도 있습니다.

연결을 삭제하기 전에 정의된 PSK를 가져오기 위해 연결 장치에 대한 구성을 다운로드할 수도 있습니다. 이런 방식으로 다른 쪽에서는 재정의할 필요가 없습니다.

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure CLI](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>IP 주소 접두사 수정

IP 주소 접두사를 수정하는 경우 수행하는 단계는 로컬 네트워크 게이트웨이에 에 연결이 있는지 여부에 따라 달라집니다.

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>게이트웨이 IP 주소 수정

연결하려는 VPN 장치의 공용 IP 주소가 변경된 경우 해당 변경 내용을 반영하도록 로컬 네트워크 게이트웨이를 수정해야 합니다. 공용 IP 주소를 변경하는 경우 수행하는 단계는 로컬 네트워크 게이트웨이에 에 연결이 있는지 여부에 따라 달라집니다.

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>다음 단계

게이트웨이 연결을 확인할 수 있습니다. [게이트웨이 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.
