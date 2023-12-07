---
title: SAML 서비스 공급자 설정 구성
description: 사용자가 지정된 타사 ID 공급자(IDP)를 통해 AEM Forms에 로그인하고 인증할 수 있도록 SAML 서비스 공급자 설정을 구성할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# SAML 서비스 공급자 설정 구성{#configure-saml-service-provider-settings}

SAML(Security Assertion Markup Language)은 엔터프라이즈 또는 하이브리드 도메인에 대한 인증을 구성할 때 선택할 수 있는 옵션 중 하나입니다. SAML은 주로 여러 도메인에서 SSO를 지원하는 데 사용됩니다. SAML이 인증 공급자로 구성된 경우 사용자는 지정된 타사 ID 공급자(IDP)를 통해 AEM Forms에 로그인하고 인증합니다.

SAML에 대한 설명은 [SAML(Security Assertion Markup Language) V2.0 기술 개요](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf).

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > SAML 서비스 공급자 설정 을 클릭합니다.
1. 서비스 공급자 엔티티 ID 상자에 AEM forms 서비스 공급자 구현에 대한 식별자로 사용할 고유 ID를 입력합니다. 또한 IDP를 구성할 때 이 고유 ID를 지정합니다(예: `um.lc.com`.) AEM 양식에 액세스하는 데 사용되는 URL을 사용할 수도 있습니다(예: `https://AEMformsserver`).
1. 서비스 공급자 기본 URL 상자에 Forms 서버의 기본 URL을 입력합니다(예: `https://AEMformsserver:8080`).
1. (선택 사항) AEM Forms에서 서명된 인증 요청을 IDP로 보낼 수 있도록 하려면 다음 작업을 수행하십시오.

   * Trust Manager를 사용하여 PKCS #12 형식의 자격 증명을 Trust Store 유형으로 선택한 문서 서명 자격 증명으로 가져옵니다. (참조: [로컬 자격 증명 관리](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * 서비스 공급자 자격 증명 키 별칭 목록에서 Trust Store의 자격 증명에 할당한 별칭을 선택합니다.
   * 내보내기 를 클릭하여 URL 내용을 파일에 저장한 다음 해당 파일을 IDP로 가져옵니다.

1. (선택 사항) 서비스 공급자 이름 ID 정책 목록에서 IDP가 SAML 어설션에서 사용자를 식별하는 데 사용하는 이름 형식을 선택합니다. 옵션은 지정되지 않음, 이메일 및 Windows 도메인 정규화된 이름입니다.

   >[!NOTE]
   >
   >이름 형식은 대/소문자를 구분하지 않습니다.

1. (선택 사항) 로컬 사용자에 대해 인증 프롬프트 사용을 선택합니다. 이 옵션을 선택하면 다음과 같은 두 개의 링크가 표시됩니다.

   * Enterprise 도메인에 속한 사용자가 인증할 수 있는 서드파티 SAML ID 공급자의 로그인 페이지에 대한 링크.
   * 로컬 도메인에 속한 사용자가 인증할 수 있는 AEM forms 로그인 페이지에 대한 링크.

   이 옵션을 선택하지 않으면 사용자는 타사 SAML ID 공급자의 로그인 페이지로 바로 이동하며, 여기서 Enterprise 도메인에 속한 사용자를 인증할 수 있습니다.

1. (선택 사항) 아티팩트 바인딩 활성화를 선택하여 아티팩트 바인딩 지원을 활성화합니다. 기본적으로 POST 바인딩은 SAML과 함께 사용됩니다. 그러나 아티팩트 바인딩을 구성한 경우 이 옵션을 선택합니다. 이 옵션을 선택하면 실제 사용자 어설션이 브라우저 요청을 통해 전달되지 않습니다. 대신 어설션에 대한 포인터가 전달되고 백엔드 웹 서비스 호출을 사용하여 어설션이 검색됩니다.
1. (선택 사항) 리디렉션을 사용하는 SAML 바인딩을 지원하려면 [리디렉션 바인딩 활성화]를 선택합니다.
1. (선택 사항) 사용자 지정 속성에서 추가 속성을 지정합니다. 추가 속성은 새 줄로 구분된 이름=값 쌍입니다.

   * 타사 어설션의 유효 기간과 일치하는 유효 기간에 대해 SAML 어설션을 발행하도록 AEM Forms를 구성할 수 있습니다. 타사 SAML 어설션 시간 제한을 적용하려면 사용자 지정 속성에 다음 줄을 추가합니다.

     `saml.sp.honour.idp.assertion.expiry=true`

   * RelayState를 사용하기 위해 다음 사용자 지정 속성을 추가하여 인증 성공 후 사용자가 리디렉션될 URL을 결정합니다.

     `saml.sp.use.relaystate=true`

   * 다음 사용자 지정 속성을 추가하여 등록된 ID 공급자 목록을 렌더링하는 데 사용되는 사용자 지정 JSP(Java Server Pages)에 대한 URL을 구성합니다. 사용자 지정 웹 응용 프로그램을 배포하지 않은 경우 기본 사용자 관리 페이지를 사용하여 목록을 렌더링합니다.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 저장을 클릭합니다.
