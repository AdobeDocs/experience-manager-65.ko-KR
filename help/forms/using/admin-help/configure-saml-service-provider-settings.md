---
title: SAML 서비스 공급자 설정 구성
seo-title: SAML 서비스 공급자 설정 구성
description: 사용자가 지정된 타사 ID 공급자(IDP)를 통해 AEM 양식에 로그인하고 인증할 수 있도록 SAML 서비스 공급자 설정을 구성할 수 있습니다.
seo-description: 사용자가 지정된 타사 ID 공급자(IDP)를 통해 AEM 양식에 로그인하고 인증할 수 있도록 SAML 서비스 공급자 설정을 구성할 수 있습니다.
uuid: 14c706ad-8b1c-4c03-9cd4-97424f2162bc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1169d0d1-cbfb-486b-acca-9b9de3d410dc
exl-id: dd302cfb-eae1-4189-aa7b-9f2533ebd164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# SAML 서비스 공급자 설정 구성{#configure-saml-service-provider-settings}

SAML(Security Assertion Markup Language)은 엔터프라이즈 또는 하이브리드 도메인에 대한 인증을 구성할 때 선택할 수 있는 옵션 중 하나입니다. SAML은 주로 여러 도메인에서 SSO를 지원하는 데 사용됩니다. SAML이 인증 공급자로 구성된 경우 사용자는 로그인하고 지정된 타사 ID 공급자(IDP)를 통해 AEM 양식을 인증합니다.

SAML에 대한 설명은 [보안 검증 마크업 언어(SAML) V2.0 기술 개요](https://www.oasis-open.org/committees/download.php/20645/sstc-saml-tech-overview-2%200-draft-10.pdf)를 참조하십시오.

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > SAML 서비스 공급자 설정 을 클릭합니다.
1. 서비스 공급자 엔티티 ID 상자에서 AEM Forms 서비스 공급자 구현의 식별자로 사용할 고유 ID를 입력합니다. IDP를 구성할 때 이 고유 ID를 지정합니다(예: `um.lc.com`). AEM 양식에 액세스하는 데 사용되는 URL을 사용할 수도 있습니다(예: `https://AEMformsserver`).
1. 서비스 공급자 기본 URL 상자에 양식 서버의 기본 URL(예: `https://AEMformsserver:8080`)을 입력합니다.
1. (선택 사항) AEM Forms에서 IDP에 서명된 인증 요청을 보낼 수 있도록 하려면 다음 작업을 수행합니다.

   * 신뢰 저장소 유형으로 선택된 문서 서명 자격 증명을 사용하여 PKCS #12 형식으로 자격 증명을 가져오려면 신뢰 관리자를 사용하십시오. ([로컬 자격 증명 관리](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials) 참조)
   * 서비스 공급자 자격 증명 키 별칭 목록에서 신뢰 저장소에서 자격 증명에 할당한 별칭을 선택합니다.
   * 내보내기 를 클릭하여 URL 컨텐츠를 파일에 저장한 다음 해당 파일을 IDP로 가져옵니다.

1. (선택 사항) 서비스 공급자 이름 ID 정책 목록에서 IDP가 SAML 검증에서 사용자를 식별하는 데 사용하는 이름 형식을 선택합니다. 옵션은 지정되지 않음, 전자 메일 및 Windows 도메인 정규화된 이름입니다.

   >[!NOTE]
   >
   >이름 형식은 대/소문자를 구분하지 않습니다.

1. (선택 사항) 로컬 사용자에 대해 인증 프롬프트 활성화 를 선택합니다. 이 옵션을 선택하면 사용자에게 다음 두 개의 링크가 표시됩니다.

   * Enterprise 도메인에 속한 사용자가 인증할 수 있는 타사 SAML ID 공급자의 로그인 페이지에 대한 링크.
   * 로컬 도메인에 속한 사용자가 인증할 수 있는 AEM forms 로그인 페이지에 대한 링크.

   이 옵션을 선택하지 않으면 사용자는 Enterprise 도메인에 속한 사용자가 인증할 수 있는 타사 SAML ID 공급자의 로그인 페이지로 직접 이동됩니다.

1. (선택 사항) 객체 바인딩 지원을 사용하려면 객체 바인딩 사용을 선택합니다. 기본적으로 POST 바인딩은 SAML과 함께 사용됩니다. 그러나 객체 바인딩을 구성한 경우 이 옵션을 선택합니다. 이 옵션을 선택하면 실제 사용자 검증이 브라우저 요청을 통해 전달되지 않습니다. 대신, 검증에 대한 포인터가 전달되고 백 엔드 웹 서비스 호출을 사용하여 검증이 검색됩니다.
1. (선택 사항) 리디렉션을 사용하는 SAML 바인딩을 지원하려면 재직접 바인딩 사용을 선택합니다.
1. (선택 사항) 사용자 지정 속성에서 추가 속성을 지정합니다. 추가 속성은 새 행으로 구분된 이름=값 쌍입니다.

   * 타사 확정의 유효 기간과 일치하는 유효 기간에 대해 SAML 검증을 실행하도록 AEM Forms를 구성할 수 있습니다. 타사 SAML 어설션 시간 제한을 준수하려면 사용자 지정 속성에 다음 줄을 추가합니다.

      `saml.sp.honour.idp.assertion.expiry=true`

   * RelayState를 사용하기 위한 다음 사용자 지정 속성을 추가하여 인증 성공 후 사용자가 리디렉션되는 URL을 결정합니다.

      `saml.sp.use.relaystate=true`

   * 다음 사용자 지정 속성을 추가하여 등록된 ID 공급자 목록을 렌더링하는 데 사용할 사용자 지정 JSP(Java Server Pages)의 URL을 구성합니다. 사용자 지정 웹 응용 프로그램을 배포하지 않은 경우 기본 사용자 관리 페이지에서 목록을 렌더링합니다.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. 저장을 클릭합니다.
