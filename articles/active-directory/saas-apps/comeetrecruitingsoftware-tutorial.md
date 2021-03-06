---
title: '자습서: Comeet Recruiting Software와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory 및 Comeet Recruiting Software 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 75f51dc9-9525-4ec6-80bf-28374f0c8adf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2018
ms.author: jeedes
ms.openlocfilehash: 137ba7a7e82ff3e57d862868859e8049838701a3
ms.sourcegitcommit: 1fb353cfca800e741678b200f23af6f31bd03e87
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43311504"
---
# <a name="tutorial-azure-active-directory-integration-with-comeet-recruiting-software"></a>자습서: Comeet Recruiting Software와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Comeet Recruiting Software를 통합하는 방법에 대해 알아봅니다.

Comeet Recruiting Software를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

- Comeet Recruiting Software에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
- 사용자가 해당 Azure AD 계정으로 Comeet Recruiting Software에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.
- 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](../manage-apps/what-is-single-sign-on.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

Comeet Recruiting Software와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

- Azure AD 구독
- Comeet Recruiting Software Single Sign-On이 설정된 구독

이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.

- Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다. 이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.

1. 갤러리에서 Comeet Recruiting Software 추가
2. Azure AD Single Sign-on 구성 및 테스트

## <a name="adding-comeet-recruiting-software-from-the-gallery"></a>갤러리에서 Comeet Recruiting Software 추가

Comeet Recruiting Software의 Azure AD 통합을 구성하려면 갤러리의 Comeet Recruiting Software를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Comeet Recruiting Software를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)** 의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다. 

    ![Azure Active Directory 단추][1]

2. **엔터프라이즈 응용 프로그램**으로 이동합니다. 그런 후 **모든 응용 프로그램**으로 이동합니다.

    ![엔터프라이즈 응용 프로그램 블레이드][2]

3. 새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.

    ![새 응용 프로그램 단추][3]

4. 검색 상자에 **Comeet Recruiting Software**를 입력하고 결과 패널에서 **Comeet Recruiting Software**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.

    ![결과 목록의 Comeet Recruiting Software](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Comeet Recruiting Software에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

Single Sign-on이 작동되려면 Azure AD는 Azure AD의 사용자에 해당하는 Comeet Recruiting Software의 사용자가 누군지 알고 있어야 합니다. 즉, Azure AD 사용자와 Comeet Recruiting Software의 관련 사용자 간에 연결이 형성되어야 합니다.

Comeet Recruiting Software에서 Azure AD Single Sign-on을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
3. **[Comeet Recruiting Software 테스트 사용자 만들기](#create-a-comeet-recruiting-software-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Comeet Recruiting Software에 만듭니다.
4. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Comeet Recruiting Software 응용 프로그램에서 Single Sign-On을 구성합니다.

**Comeet Recruiting Software에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**

1. Azure Portal의 **Comeet Recruiting Software** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.

    ![Single Sign-On 구성 링크][4]

2. **Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.

    ![Single Sign-On 대화 상자](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_samlbase.png)

3. **Comeet Recruiting Software 도메인 및 URL** 섹션에서 **IDP** 시작 모드로 응용 프로그램을 구성하려는 경우 다음 단계를 수행합니다.

    ![Comeet 도메인 및 URL Single Sign-On 정보](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_url1.png)

    a. **식별자** 텍스트 상자에서 `https://app.comeet.co/adfs_auth/acs/<UNIQUEID>/` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에 다음 패턴으로 URL을 입력합니다.`https://app.comeet.co/adfs_auth/acs/<UNIQUEID>/`

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자, 회신 URL로 해당 값을 업데이트합니다. [지원 페이지](https://support.comeet.co/knowledgebase/adfs-single-sign-on/)에 표시된 대로 Comeet Recruiting Software 포털에서 이러한 값을 가져옵니다.

4. **SP** 시작 모드에서 응용 프로그램을 구성하려면 **고급 URL 설정 표시**를 확인하고 다음 단계를 수행합니다.

    ![Comeet Recruiting Software 도메인 및 URL Single Sign-On 정보](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_url2.png)

    **로그온 URL** 텍스트 상자에서 URL `https://app.comeet.co`을 입력합니다.

5. Comeet Recruiting Software 응용 프로그램은 특정 서식에서 SAML 어설션을 예상하며 이는 SAML 토큰 특성 구성에 사용자 할당 특성 매핑을 추가합니다. 다음 스크린샷은 이에 대한 예제를 보여 줍니다. **사용자 ID**의 기본값은 **user.userprincipalname**이지만 **Comeet Recruiting Software**에는 이것이 사용자의 이메일 주소와 매핑되어야 합니다. 목록에서 **user.mail** 특성을 사용하거나 조직 구성을 기반으로 적절한 특성 값을 사용할 수 있기 위해서입니다.

    ![Configure Single Sign-On](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_attribute.png)

6. **사용자 특성** 섹션에서 **기타 모든 사용자 특성 보기 및 편집**을 클릭하고 특성을 확장합니다. 표시된 각 특성에 대해 다음 단계를 수행합니다.

    | 특성 이름 | 특성 값 |
    | ---------------| --------------- |
    | comeet_id | user.userprincipalname |

    a. **특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.

    ![Configure Single Sign-On](./media/comeetrecruitingsoftware-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/comeetrecruitingsoftware-tutorial/tutorial_attribute_05.png)

    b. **이름** 텍스트 상자에서 해당 행에 표시된 **특성 이름**을 입력합니다.

    다. **값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.

    d. **Ok**를 클릭합니다.

7. **SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.

    ![인증서 다운로드 링크](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_certificate.png)

8. **저장** 단추를 클릭합니다.

    ![Single Sign-On 구성 저장 단추](./media/comeetrecruitingsoftware-tutorial/tutorial_general_400.png)

9. **Comeet Recruiting Software** 쪽에서 Single Sign-On을 구성하려면 [지원 페이지](https://support.comeet.co/knowledgebase/adfs-single-sign-on/)에 표시된 대로 다운로드한 메타데이터 XML의 콘텐츠를 Comeet Recruiting Software에 붙여넣습니다.

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.

   ![Azure AD 테스트 사용자 만들기][100]

**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.

    ![Azure Active Directory 단추](./media/comeetrecruitingsoftware-tutorial/create_aaduser_01.png)

2. 사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/comeetrecruitingsoftware-tutorial/create_aaduser_02.png)

3. **사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.

    ![추가 단추](./media/comeetrecruitingsoftware-tutorial/create_aaduser_03.png)

4. **사용자** 대화 상자에서 다음 단계를 수행합니다.

    ![사용자 대화 상자](./media/comeetrecruitingsoftware-tutorial/create_aaduser_04.png)

    a. **이름** 상자에 **BrittaSimon**을 입력합니다.

    나. **사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.

    다. **암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.

    d. **만들기**를 클릭합니다.

### <a name="create-a-comeet-recruiting-software-test-user"></a>Comeet Recruiting Software 테스트 사용자 만들기

이 섹션에서는 Comeet Recruiting Software에서 Britta Simon이라는 사용자를 만듭니다. Comeet Recruiting Software 플랫폼에 사용자를 추가하려면 [Comeet Recruiting Software 지원 팀](mailto:support@comeet.co)에 문의하세요. Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Comeet Recruiting Software에 대한 액세스 권한을 부여합니다.

![사용자 역할 할당][200]

**Britta Simon을 Comeet Recruiting Software에 할당하려면 다음 단계를 수행합니다.**

1. Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.

    ![사용자 할당][201]

2. 응용 프로그램 목록에서 **Comeet Recruiting Software**를 선택합니다.

    ![응용 프로그램 목록의 Comeet Recruiting Software 링크](./media/comeetrecruitingsoftware-tutorial/tutorial_comeetrecruitingsoftware_app.png)  

3. 왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.

    !["사용자 및 그룹" 링크][202]

4. **추가** 단추를 클릭합니다. 그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.

    ![할당 추가 창][203]

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.

6. **사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 Comeet Recruiting Software 타일을 클릭하면 Comeet Recruiting Software 응용 프로그램에 자동으로 로그온됩니다.
액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/active-directory-saas-access-panel-introduction.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

* [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](tutorial-list.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_01.png
[2]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_02.png
[3]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_03.png
[4]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_04.png

[100]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_100.png

[200]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_200.png
[201]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_201.png
[202]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_202.png
[203]: ./media/comeetrecruitingsoftware-tutorial/tutorial_general_203.png