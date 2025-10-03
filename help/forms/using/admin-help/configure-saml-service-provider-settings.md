---
title: SAML 서비스 공급자 설정 구성
description: SAML 서비스 공급자 설정을 구성하여 사용자가 지정된 서드파티 ID 공급자(IDP)를 통해 AEM Forms에 로그인하고 인증하도록 할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '607'
ht-degree: 100%

---

# SAML 서비스 공급자 설정 구성{#configure-saml-service-provider-settings}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

SAML(Security Assertion Markup Language)은 엔터프라이즈 또는 하이브리드 도메인에 대한 인증을 구성할 때 선택할 수 있는 옵션 중 하나입니다. SAML은 주로 여러 도메인에서 SSO를 지원하는 데 사용됩니다. SAML이 인증 공급자로 구성된 경우 사용자는 지정된 서드파티 ID 공급자(IDP)를 통해 AEM Forms에 로그인하고 인증합니다.

SAML에 대한 설명은 [SAML(Security Assertion Markup Language) V2.0 기술 개요](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html)를 참조하십시오.

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > SAML 서비스 공급자 설정을 클릭합니다.
1. 서비스 공급자 엔터티 ID 상자에 AEM Forms 서비스 공급자 구현에 대한 식별자로 사용할 고유 ID를 입력합니다. IDP를 구성할 때도 이 고유 ID를 지정합니다(예: `um.lc.com`). AEM Forms에 액세스하는 데 사용되는 URL을 사용할 수도 있습니다(예: `https://AEMformsserver`).
1. 서비스 공급자 기본 URL 상자에 Forms 서버의 기본 URL을 입력합니다(예: `https://AEMformsserver:8080`).
1. (선택 사항) AEM Forms가 IDP에 서명된 인증 요청을 보낼 수 있도록 하려면 다음 작업을 수행합니다.

   * 신뢰 관리자를 사용하여 Trust Store 유형으로 문서 서명 자격 증명을 선택하고 PKCS #12 형식의 자격 증명을 가져옵니다. ([로컬 자격 증명 관리](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials)를 참조하십시오.)
   * 서비스 공급자 자격 증명 키 별칭 목록에서 Trust Store의 자격 증명에 할당한 별칭을 선택합니다.
   * 내보내기를 클릭하면 URL 콘텐츠를 파일로 저장한 후 해당 파일을 IDP로 가져올 수 있습니다.

1. (선택 사항) 서비스 공급자 이름 ID 정책 목록에서 IDP가 SAML 어설션에서 사용자를 식별하는 데 사용하는 이름 형식을 선택합니다. 옵션으로는 지정되지 않음, 이메일, Windows 도메인 정규화된 이름이 있습니다.

   >[!NOTE]
   >
   >이름 형식은 대소문자를 구분하지 않습니다.

1. (선택 사항) 로컬 사용자에 대한 인증 프롬프트 활성화를 선택합니다. 이 옵션을 선택하면 사용자에게 다음과 같은 링크 두 개가 표시됩니다.

   * 서드파티 SAML ID 공급자의 로그인 페이지 링크이며, 엔터프라이즈 도메인에 속한 사용자는 해당 페이지에서 인증을 받을 수 있습니다.
   * AEM Forms 로그인 페이지 링크이며, 로컬 도메인에 속한 사용자는 해당 페이지에서 인증을 받을 수 있습니다.

   이 옵션을 선택하지 않으면 사용자는 서드파티 SAML ID 공급자의 로그인 페이지로 바로 이동하게 되며, 엔터프라이즈 도메인에 속한 사용자는 해당 페이지에서 인증을 받을 수 있습니다.

1. (선택 사항) 아티팩트 바인딩 지원을 활성화하려면 아티팩트 바인딩 활성화를 선택합니다. 기본적으로 POST 바인딩은 SAML과 함께 사용됩니다. 하지만 아티팩트 바인딩을 구성한 경우 이 옵션을 선택하십시오. 이 옵션을 선택하면 실제 사용자 어설션이 브라우저 요청을 통해 전달되지 않습니다. 대신 어설션에 대한 포인터가 전달되고 백엔드 웹 서비스 호출을 사용하여 어설션을 가져옵니다.
1. (선택 사항) 리디렉션을 사용하는 SAML 바인딩을 지원하려면 리디렉션 바인딩 활성화를 선택합니다.
1. (선택 사항) 사용자 정의 속성에서 추가 속성을 지정합니다. 추가 속성은 새 줄로 구분된 이름=값 쌍입니다.

   * AEM Forms를 구성하여 서드파티 어설션의 유효 기간과 일치하는 유효 기간 동안 SAML 어설션을 발급할 수 있습니다. 서드파티 SAML 어설션 시간 초과를 준수하려면 사용자 정의 속성에 다음 줄을 추가합니다.

     `saml.sp.honour.idp.assertion.expiry=true`

   * 다음과 같이 RelayState를 사용하는 사용자 정의 속성을 추가하여 사용자가 인증에 성공한 후 리디렉션될 URL을 결정합니다.

     `saml.sp.use.relaystate=true`

   * 다음과 같은 사용자 정의 속성을 추가하여 등록된 ID 공급자 목록을 렌더링하는 데 사용되는 사용자 정의 JSP(Java™ Server Pages)의 URL을 구성할 수 있습니다. 사용자 정의 웹 애플리케이션을 배포하지 않은 경우 기본 사용자 관리 페이지를 사용하여 해당 목록을 렌더링합니다.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 저장을 클릭합니다.
