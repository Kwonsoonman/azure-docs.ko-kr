---
title: '자습서: EPIM(EthicsPoint Incident Management)과 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory 및 EPIM(EthicsPoint Incident Management) 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c38c751701b323bf1c985a4127d0e9deac2c8eaa
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39446024"
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a>자습서: EPIM(EthicsPoint Incident Management)과 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 EPIM(EthicsPoint Incident Management)을 통합하는 방법에 대해 알아봅니다.

EPIM(EthicsPoint Incident Management)과 Azure AD를 통합하면 다음과 같은 이점이 제공됩니다.

- Azure AD에서 EPIM(EthicsPoint Incident Management)에 대한 액세스 권한이 있는 사용자를 제어할 수 있습니다.
- 사용자가 해당 Azure AD 계정으로 EPIM(EthicsPoint Incident Management)에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.
- 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](../manage-apps/what-is-single-sign-on.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

EPIM(EthicsPoint Incident Management)과의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

- Azure AD 구독
- EPIM(EthicsPoint Incident Management) Single Sign-On이 설정된 구독

> [!NOTE]
> 이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.

이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.

- 꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.
- Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명
이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 갤러리에서 EPIM(EthicsPoint Incident Management) 추가
1. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-ethicspoint-incident-management-epim-from-the-gallery"></a>갤러리에서 EPIM(EthicsPoint Incident Management) 추가
Azure AD로의 EPIM(EthicsPoint Incident Management) 통합을 구성하려면 갤러리의 EPIM(EthicsPoint Incident Management)을 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 EPIM(EthicsPoint Incident Management)을 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)** 의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다. 

    ![Active Directory][1]

1. **엔터프라이즈 응용 프로그램**으로 이동합니다. 그런 후 **모든 응용 프로그램**으로 이동합니다.

    ![응용 프로그램][2]
    
1. 새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.

    ![응용 프로그램][3]

1. 검색 상자에 **EPIM(EthicsPoint Incident Management)** 을 입력합니다.

    ![Azure AD 테스트 사용자 만들기](./media/ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

1. 결과 창에서 **EPIM(EthicsPoint Incident Management)** 을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.

    ![Azure AD 테스트 사용자 만들기](./media/ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD Single Sign-on 구성 및 테스트
이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 EPIM(EthicsPoint Incident Management)에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 EPIM(EthicsPoint Incident Management) 사용자가 누구인지 알고 있어야 합니다. 즉, Azure AD 사용자와 EPIM(EthicsPoint Incident Management)의 관련 사용자 간에 연결이 형성되어야 합니다.

EPIM(EthicsPoint Incident Management)에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.

EPIM(EthicsPoint Incident Management)에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
1. **[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On 테스트하는 데 사용합니다.
1. **[EPIM(EthicsPoint Incident Management) 테스트 사용자 만들기](#creating-a-ethicspoint-incident-management-epim-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 EPIM(EthicsPoint Incident Management)에 만듭니다.
1. **[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
1. **[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 EPIM(EthicsPoint Incident Management) 응용 프로그램에서 Single Sign-On을 구성합니다.

**EPIM(EthicsPoint Incident Management)과의 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**

1. Azure Portal의 **EPIM(EthicsPoint Incident Management)** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.

    ![Configure Single Sign-On][4]

1. **Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.
 
    ![Configure Single Sign-On](./media/ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

1. **EPIM(EthicsPoint Incident Management) 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.

    ![Configure Single Sign-On](./media/ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    a. **로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다.
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    나. **식별자** 텍스트 상자에서 `https://<companyname>.navexglobal.com/adfs/services/trust` 패턴을 사용하여 URL을 입력합니다.

    다. **회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://<servername>.navexglobal.com/adfs/ls/`

    > [!NOTE] 
    > 이러한 값은 실제 값이 아닙니다. 실제 회신 URL, 식별자 및 로그온 URL로 값을 업데이트합니다. 이러한 값을 얻으려면 [EPIM(EthicsPoint Incident Management) 클라이언트 지원 팀](http://www.navexglobal.com/company/contact-us)에 문의하세요. 

1. **SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.

    ![Configure Single Sign-On](./media/ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

1. **저장** 단추를 클릭합니다.

    ![Configure Single Sign-On](./media/ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
1. **EPIM(EthicsPoint Incident Management)** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [EPIM(EthicsPoint Incident Management) 지원 팀](http://www.navexglobal.com/company/contact-us)으로 보내야 합니다.

> [!TIP]
> 이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.  **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다. 포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.
> 

### <a name="creating-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기
이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.

![Azure AD 사용자 만들기][100]

**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**

1. **Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure AD 테스트 사용자 만들기](./media/ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

1. 사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.
    
    ![Azure AD 테스트 사용자 만들기](./media/ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

1. **사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

1. **사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.
 
    ![Azure AD 테스트 사용자 만들기](./media/ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    a. **이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.

    나. **사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.

    다. **암호 표시**를 선택하고 **암호** 값을 적어둡니다.

    d. **만들기**를 클릭합니다.
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a>EPIM(EthicsPoint Incident Management) 테스트 사용자 만들기

이 섹션에서는 EPIM(EthicsPoint Incident Management)에서 Britta Simon이라는 사용자를 만듭니다. [EPIM(EthicsPoint Incident Management) 지원 팀](http://www.navexglobal.com/company/contact-us)과 협의하여 EPIM(EthicsPoint Incident Management) 플랫폼에서 사용자를 추가하세요.

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 EPIM(EthicsPoint Incident Management)에 대한 액세스 권한을 부여합니다.

![사용자 할당][200] 

**EPIM(EthicsPoint Incident Management)에 Britta Simon을 할당하려면 다음 단계를 수행합니다.**

1. Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.

    ![사용자 할당][201] 

1. 응용 프로그램 목록에서 **EPIM(EthicsPoint Incident Management)** 을 선택합니다.

    ![Configure Single Sign-On](./media/ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

1. 왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.

    ![사용자 할당][202] 

1. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![사용자 할당][203]

1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.

1. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.
    
### <a name="testing-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.
액세스 패널에서 EPIM(EthicsPoint Incident Management) 타일을 클릭하면 EPIM(EthicsPoint Incident Management) 응용 프로그램에 자동으로 로그온되어야 합니다.

## <a name="additional-resources"></a>추가 리소스

* [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/ethicspoint-incident-management-tutorial/tutorial_general_203.png

