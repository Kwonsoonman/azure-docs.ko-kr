---
title: Azure Active Directory B2C를 사용하여 Google 계정으로 등록 설정 및 로그인 | Microsoft Docs
description: 고객에게 Azure Active Directory B2C를 사용하여 응용 프로그램에서 Google 계정으로 등록 및 로그인을 제공합니다.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 09/11/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 5f6ce3564cf4056dc9295e1885be425bbe3d7701
ms.sourcegitcommit: c282021dbc3815aac9f46b6b89c7131659461e49
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49165303"
---
# <a name="set-up-sign-up-and-sign-in-with-a-google-account-using-azure-active-directory-b2c"></a>Azure Active Directory B2C를 사용하여 Google 계정으로 등록 설정 및 로그인

## <a name="create-a-google-application"></a>Google 응용 프로그램 만들기

Azure AD(Azure Active Directory) B2C에서 Google 계정을 ID 공급자로 사용하려면 테넌트에 해당 계정을 나타내는 응용 프로그램을 만들어야 합니다. Google 계정이 없는 경우 [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)에서 얻을 수 있습니다.

1. Google 계정 자격 증명을 사용하여 [Google 개발자 콘솔](https://console.developers.google.com/)에 로그인합니다.
2. **프로젝트 만들기**를 선택하고 **만들기**를 클릭합니다. 이전에 프로젝트를 만들었으면 프로젝트 목록을 선택하고 **새 프로젝트**를 선택합니다.
3. **프로젝트 이름**을 입력하고 **만들기**를 클릭한 다음 새 프로젝트를 사용 중인지 확인합니다.
3. 왼쪽 메뉴에서 **자격 증명**을 선택하고 **자격 증명 만들기** > **Oauth 클라이언트 ID**를 선택합니다.
4. **동의 화면 구성**을 선택합니다.
5. 유효한 **메일 주소**를 선택하거나 지정하고 **사용자에게 표시되는 제품 이름**을 제공하고, **권한 있는 도메인**에 `b2clogin.com`을 추가하고, **저장**을 클릭합니다.
6. **응용 프로그램 형식**에서 **웹 응용 프로그램**을 선택합니다.
7. 응용 프로그램에 대한 **이름**을 입력하고 **권한이 부여된 JavaScript 원본**에 `https://your-tenant-name.b2clogin.com`을 입력하고 **권한이 부여된 리디렉션 URI**에 `https://your-tenant-name.b2clogin.com/your-tenant-name.onmicrosoft.com/oauth2/authresp`를 입력합니다. `your-tenant-name`을 테넌트 이름으로 바꿉니다. Azure AD B2C에서 테넌트가 대문자로 정의되어 있더라도 테넌트 이름을 입력할 때는 소문자만 사용해야 합니다.
8. **만들기**를 클릭합니다.
9. **클라이언트 ID** 및 **클라이언트 비밀** 값을 복사합니다. 테넌트에서 Google을 ID 공급자로 구성하려면 둘 모두가 필요합니다. **클라이언트 암호** 는 중요한 보안 자격 증명입니다.

## <a name="configure-a-google-account-as-an-identity-provider"></a>Google 계정을 ID 공급자로 구성

1. Azure AD B2C 테넌트의 전역 관리자로 [Azure Portal](https://portal.azure.com/)에 로그인합니다.
2. Azure AD B2C 테넌트를 포함하는 디렉터리를 사용하려면 위쪽 메뉴에서 **디렉터리 및 구독 필터**를 클릭하고 테넌트가 포함된 디렉터리를 선택합니다.
3. Azure Portal의 왼쪽 상단 모서리에서 **모든 서비스**를 선택하고 **Azure AD B2C**를 검색하여 선택합니다.
4. **ID 공급자**를 선택한 다음, **추가**를 선택합니다.
5. **이름**을 입력합니다. 예를 들어, *Google*을 입력합니다.
6. **ID 공급자 형식**을 선택하고 **Google**을 선택한 다음, **확인**을 클릭합니다.
7. **이 ID 공급자 설정**을 선택하고 이전에 기록한 클라이언트 ID를 **클라이언트 ID**로 입력한 후, 기록한 클라이언트 암호를 이전에 만든 Google 응용 프로그램의 **클라이언트 암호**로 입력합니다.
8. **확인**을 클릭한 다음 **만들기**를 클릭하여 Google 구성을 저장합니다.

