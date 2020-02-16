---
title: AEM에서 문서 보안 보호 PDF 및 Microsoft Office 문서를 검색할 수 있도록 설정
seo-title: AEM에서 문서 보안 보호 PDF 및 Microsoft Office 문서를 검색할 수 있도록 설정
description: 기본 AEM 검색을 활성화하여 DRM 보호 PDF 문서에서 전체 텍스트 검색을 수행하는 방법을 알아봅니다.
seo-description: 기본 AEM 검색을 활성화하여 DRM 보호 PDF 문서에서 전체 텍스트 검색을 수행하는 방법을 알아봅니다.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM에서 문서 보안 보호 PDF 및 Microsoft Office 문서를 검색할 수 있도록 설정{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager는 AEM에 저장된 다양한 자산을 검색하고 찾을 수 있는 사용자 인터페이스를 제공합니다. 기본 검색은 AEM 자산을 검색 및 찾고 일반 텍스트 파일, Microsoft Office 문서 및 PDF 문서와 같이 일반적으로 사용되는 다양한 문서 형식에서 텍스트 검색을 수행할 수 있습니다. DRM으로 보호된 PDF 및 Microsoft Office 문서에서 기본 검색을 확장하여 전체 텍스트 검색을 수행할 수도 있습니다.

AEM에서 문서 보안 보호 PDF 및 Microsoft Office 문서를 검색할 수 있도록 하려면 다음 단계를 수행하십시오.

## Before you start {#before-you-start}

* AEM Forms 문서 보안 설치 및 구성
* deserialization 방화벽 구성의 허용 목록에 sun.util.calendar 패키지를 **추가합니다.** 구성은 에 나와 `https://[server]:[port]/system/console/configMgr`있습니다.
* 모든 AEM 번들이 실행 중인지 확인합니다. 번들은 에 나와 `https://[server]:[port]/system/console/bundles`있습니다. 모든 번들이 활성화되지 않은 경우 잠시 기다렸다가 번들의 상태를 몇 분 동안 확인합니다.

## AEM Forms 워크플로우(JEE의 AEM Forms) 내에서 보안 연결 설정 {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

보안 연결을 통해 JEE의 AEM Forms와 동일한 서버에서 실행되는 OSGi 서비스 간에 정보를 매끄럽게 전달할 수 있습니다. 다음 방법 중 하나를 사용하여 보안 연결을 설정합니다.

* JEE 관리자 자격 증명에서 AEM Forms를 사용하여 AEM Forms 클라이언트 SDK 번들 구성
* 상호 인증을 사용하여 AEM Forms 클라이언트 SDK 번들 구성

### JEE 관리자 자격 증명에서 AEM Forms를 사용하여 AEM Forms 클라이언트 SDK 번들 구성 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM 구성 관리자를 열고 관리자로 로그인합니다. 기본 URL 파섹
1. AEM Forms 클라이언트 SDK 번들을 검색하고 엽니다. 다음 속성의 값을 지정합니다.

   * **** 서버 URL:JEE 서버에서 AEM Forms의 HTTP URL을 지정합니다. https를 통한 통신을 활성화하려면 -Djavax.net.ssl.trustStore=&lt;JEE 키 저장소 파일의 AEM Forms 경로> 매개 변수를 사용하여 JEE 서버에서 AEM Forms를 다시 시작합니다.
   * **서비스 이름**:지정된 서비스 목록에 RightsManagementService를 추가합니다.
   * **** 사용자 이름:JEE 서버의 AEM Forms에서 호출을 시작하는 데 사용할 JEE 계정의 AEM Forms 사용자 이름을 지정합니다. 지정된 계정에는 JEE 서버의 AEM Forms에서 Document Services를 호출하는 권한이 있어야 합니다.
   * **암호**:사용자 이름 필드에 언급된 JEE 계정의 AEM Forms 암호를 지정합니다.
   **저장**&#x200B;을 클릭합니다. AEM 파섹

### 상호 인증을 사용하여 AEM Forms 클라이언트 SDK 번들 구성 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. JEE 파섹 자세한 내용은 CAC 및 [상호 인증을 참조하십시오](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. AEM 구성 관리자를 열고 관리자로 로그인합니다. 기본 URL 파섹
1. AEM Forms 클라이언트 SDK 번들을 검색하고 엽니다. 다음 속성의 값을 지정합니다.

   * **** 서버 URL:JEE 서버에서 AEM Forms의 HTTPS URL을 지정합니다. https를 통한 통신을 활성화하려면 -Djavax.net.ssl.trustStore=&lt;JEE 키 저장소 파일의 AEM Forms 경로> 매개 변수를 사용하여 JEE 서버에서 AEM Forms를 다시 시작합니다.
   * **양방향 SSL 활성화**:양방향 SSL 활성화 옵션을 활성화합니다.
   * **KeyStore 파일 URL**:키 저장소 파일의 URL을 지정합니다.
   * **TrustStore URL**:truststore 파일의 URL을 지정합니다.
   * **KeyStore 암호**:키 저장소 파일의 암호를 지정합니다.
   * **TrustStorePassword**:truststore 파일의 암호를 지정합니다.
   * **서비스 이름**:지정된 서비스 목록에 RightsManagementService를 추가합니다.
   **저장**&#x200B;을 클릭합니다. AEM이 문서 보안 보호 PDF 및 Microsoft Office 문서를 검색할 수 있도록 설정되었습니다.

## 정책으로 보호된 샘플 PDF 또는 Microsoft Office 문서 색인화 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. AEM 자산에 관리자로 로그인합니다.
1. AEM Digital Asset Manager에서 폴더를 만들고 정책으로 보호된 PDF 또는 Microsoft Office 문서를 새로 만든 폴더에 업로드합니다. 이제 AEM 검색을 사용하여 정책으로 보호된 문서의 컨텐츠를 검색합니다. 검색된 텍스트가 포함된 문서를 반환해야 합니다.

