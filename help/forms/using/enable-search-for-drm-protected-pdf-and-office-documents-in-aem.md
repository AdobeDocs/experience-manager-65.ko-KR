---
title: AEM에서 문서 보안으로 보호된 PDF 및 Microsoft Office 문서를 검색할 수 있도록 설정
description: DRM으로 보호된 AEM 문서에 대해 전체 텍스트 검색을 수행할 수 있도록 기본 PDF 검색을 활성화하는 방법을 알아봅니다.
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 9%
---
# AEM에서 문서 보안으로 보호된 PDF 및 Microsoft Office 문서를 검색할 수 있도록 설정{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager은 AEM에 저장된 다양한 에셋을 검색하고 찾을 수 있는 사용자 인터페이스를 제공합니다. 기본 검색은 AEM 에셋을 검색하고 찾고 일반 텍스트 파일, Microsoft Office 문서 및 PDF 문서와 같이 일반적으로 사용되는 다양한 문서 형식에 대해 텍스트 검색을 수행할 수 있습니다. DRM으로 보호된 PDF 및 Microsoft Office 문서에서 전체 텍스트 검색을 수행하도록 기본 검색을 확장 및 활성화할 수도 있습니다.

AEM에서 문서 보안으로 보호된 PDF 및 Microsoft Office 문서를 검색할 수 있도록 하려면 다음 단계를 수행하십시오.

## 시작하기 전 {#before-you-start}

* AEM Forms 문서 보안을 설치하고 구성합니다.
* 패키지 sun.util.calendar를 **직렬화 방화벽 구성**&#x200B;의 deserialization에 추가합니다. 구성이 `https://'[server]:[port]'/system/console/configMgr`에 나열됩니다.
* 모든 AEM 번들이 실행 중인지 확인합니다. 번들은 `https://'[server]:[port]'/system/console/bundles`에 나열됩니다. 모든 번들이 활성화되지 않은 경우 잠시 기다렸다가 몇 분 동안 번들 상태를 확인합니다.

## AEM Forms 워크플로 내에서 보안 연결 설정(JEE의 AEM Forms) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

보안 연결을 통해 JEE의 AEM Forms과 동일한 서버에서 실행되는 OSGi 서비스 간에 정보가 원활하게 전달될 수 있습니다. 다음 방법 중 하나를 사용하여 보안 연결을 설정하십시오.

* JEE 관리자 자격 증명에서 AEM Forms으로 AEM Forms 클라이언트 SDK 번들 구성
* 상호 인증을 사용하여 AEM Forms 클라이언트 SDK 번들 구성

### JEE 관리자 자격 증명에서 AEM Forms으로 AEM Forms 클라이언트 SDK 번들 구성 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM 구성 관리자를 열고 관리자로 로그인합니다. 기본 URL은 https://&lt;serverName>:&lt;port>/lc/system/console/configMgr입니다.
1. AEM Forms 클라이언트 SDK 번들을 검색하여 엽니다. 다음 속성에 대한 값을 지정합니다.

   * **서버 URL:** JEE 서버에서 AEM Forms의 HTTP URL을 지정합니다. https를 통해 통신하려면 -Djavax.net.ssl.trustStore=&lt;JEE 키 저장소 파일의 AEM Forms 경로> 매개 변수를 사용하여 JEE의 AEM Forms 서버를 다시 시작합니다.
   * **서비스 이름**: 지정된 서비스 목록에 RightsManagementService를 추가합니다.
   * **사용자 이름:** JEE 서버의 AEM Forms에서 호출을 시작하는 데 사용할 JEE 계정의 AEM Forms 사용자 이름을 지정합니다. 지정된 계정에는 JEE 서버의 AEM Forms에서 문서 서비스를 호출할 수 있는 권한이 있어야 합니다.
   * **암호**: 사용자 이름 필드에 언급된 JEE 계정의 AEM Forms 암호를 지정하십시오.

   **저장**&#x200B;을 클릭합니다. AEM은 문서 보안으로 보호된 PDF 및 Microsoft Office 문서를 검색할 수 있도록 활성화됩니다.

### 상호 인증을 사용하여 AEM Forms 클라이언트 SDK 번들 구성 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. JEE에서 AEM Forms에 대한 상호 인증을 활성화합니다. 자세한 내용은 [CAC 및 상호 인증](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)을 참조하십시오.
1. AEM 구성 관리자를 열고 관리자로 로그인합니다. 기본 URL은 https://&lt;serverName>:&lt;port>/lc/system/console/configMgr입니다.
1. AEM Forms 클라이언트 SDK 번들을 검색하여 엽니다. 다음 속성에 대한 값을 지정합니다.

   * **서버 URL:** JEE 서버에서 AEM Forms의 HTTPS URL을 지정합니다. https를 통해 통신하려면 -Djavax.net.ssl.trustStore=&lt;JEE 키 저장소 파일의 AEM Forms 경로> 매개 변수를 사용하여 JEE의 AEM Forms 서버를 다시 시작합니다.
   * **양방향 SSL 사용**: 양방향 SSL 사용 옵션을 사용합니다.
   * **KeyStore 파일 URL**: 키 저장소 파일의 URL을 지정하십시오.
   * **TrustStore 파일 URL**: Truststore 파일의 URL을 지정하십시오.
   * **KeyStore 암호**: 키 저장소 파일의 암호를 지정하십시오.
   * **TrustStorePassword**: truststore 파일의 암호를 지정하십시오.
   * **서비스 이름**: 지정된 서비스 목록에 RightsManagementService를 추가합니다.

   **저장**&#x200B;을 클릭합니다. AEM은 문서 보안으로 보호된 PDF 및 Microsoft Office 문서를 검색할 수 있도록 활성화됩니다

   >[!NOTE]
   >
   > SDK를 다시 시작하려면 &#39;Ctrl+C&#39; 명령을 사용하는 것이 좋습니다. 예를 들어 Java 프로세스를 중지하는 것과 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 수 있습니다.

## 정책으로 보호된 샘플 PDF 또는 Microsoft Office 문서 색인화 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 관리자로 AEM Assets에 로그인합니다.
1. AEM Digital Asset Manager에서 폴더를 만들고 정책으로 보호된 PDF 또는 Microsoft Office 문서를 새로 만든 폴더에 업로드합니다. 이제 AEM 검색을 사용하여 정책으로 보호된 문서의 콘텐츠를 검색합니다. 검색된 텍스트가 포함된 문서를 반환해야 합니다.
