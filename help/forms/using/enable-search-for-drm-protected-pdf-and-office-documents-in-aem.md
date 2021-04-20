---
title: AEM에서 보호된 PDF 및 Microsoft Office 문서를 검색할 수 있습니다.
seo-title: AEM에서 보호된 PDF 및 Microsoft Office 문서를 검색할 수 있습니다.
description: 기본 AEM 검색을 활성화하여 DRM으로 보호된 PDF 문서에서 전체 텍스트 검색을 수행하는 방법을 살펴봅니다.
seo-description: 기본 AEM 검색을 활성화하여 DRM으로 보호된 PDF 문서에서 전체 텍스트 검색을 수행하는 방법을 살펴봅니다.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---


# AEM에서 문서 보안 보호 PDF 및 Microsoft Office 문서를 검색할 수 있도록 설정{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager은 AEM에 저장된 다양한 에셋을 검색하고 찾을 수 있는 사용자 인터페이스를 제공합니다. 기본 검색을 통해 AEM 에셋을 검색 및 찾을 수 있으며 일반 텍스트 파일, Microsoft Office 문서 및 PDF 문서와 같이 일반적으로 사용되는 다양한 문서 포맷에서 텍스트 검색을 수행할 수 있습니다. DRM으로 보호된 PDF 및 Microsoft Office 문서에서 전체 텍스트를 검색할 수 있도록 기본 검색을 확장하고 활성화할 수도 있습니다.

AEM에서 보호된 PDF 및 Microsoft Office 문서를 검색할 수 있도록 하려면 다음 단계를 수행하십시오.

## {#before-you-start}을(를) 시작하기 전에

* AEM Forms 문서 보안 설치 및 구성
* 패키지 sun.util.calendar를 **Deserialization 방화벽 구성허용 목록에 추가하다의 라이브러리에 추가합니다.** 구성은  `https://'[server]:[port]'/system/console/configMgr`
* 모든 AEM 번들이 실행되고 있는지 확인합니다. 번들은 `https://'[server]:[port]'/system/console/bundles`에 나열됩니다. 모든 번들이 활성 상태가 아니면 잠시 기다린 후 번들의 상태를 확인합니다.

## AEM Forms 워크플로우(JEE의 AEM Forms) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee} 내에 보안 연결 설정

안전한 연결을 통해 JEE의 AEM Forms과 동일한 서버에서 실행되는 OSGi 서비스 간에 정보를 원활하게 전달할 수 있습니다. 다음 방법 중 하나를 사용하여 보안 연결을 설정합니다.

* JEE 관리자 자격 증명에 AEM Forms이 포함된 AEM Forms Client SDK 번들 구성
* 상호 인증을 사용하여 AEM Forms Client SDK 번들 구성

### JEE 관리자 자격 증명 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}에 AEM Forms이 포함된 AEM Forms Client SDK 번들 구성

1. AEM 구성 관리자를 열고 관리자로 로그인합니다. 기본 URL은 https://&lt;serverName>:&lt;port>/lc/system/console/configMgr입니다.
1. AEM Forms Client SDK 번들을 검색하고 엽니다. 다음 속성에 대한 값을 지정합니다.

   * **서버 URL:** JEE 서버에서 AEM Forms의 HTTP URL을 지정합니다. https를 통한 통신을 활성화하려면 -Djavax.net.ssl.trustStore=&lt;JEE 키 저장소 파일의 AEM Forms 경로> 매개 변수를 사용하여 JEE 서버에서 AEM Forms을 다시 시작합니다.
   * **서비스 이름**:지정된 서비스 목록에 RightsManagementService를 추가합니다.
   * **사용자 이름:** JEE 서버의 AEM Forms에서 전화를 거는 데 사용할 JEE 계정의 AEM Forms 사용자 이름을 지정합니다. 지정된 계정에는 JEE 서버의 AEM Forms에서 문서 서비스를 호출할 수 있는 권한이 있어야 합니다.
   * **암호**:사용자 이름 필드에 언급된 JEE 계정의 AEM Forms 암호를 지정합니다.

   **저장**&#x200B;을 클릭합니다. AEM은 문서 보안 보호 PDF 및 Microsoft Office 문서를 검색할 수 있도록 설정되어 있습니다.

### 상호 인증 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}을(를) 사용하여 AEM Forms Client SDK 번들 구성

1. JEE에서 AEM Forms에 대한 상호 인증을 활성화합니다. 자세한 내용은 [CAC 및 상호 인증](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)을 참조하십시오.
1. AEM 구성 관리자를 열고 관리자로 로그인합니다. 기본 URL은 https://&lt;serverName>:&lt;port>/lc/system/console/configMgr입니다.
1. AEM Forms Client SDK 번들을 검색하고 엽니다. 다음 속성에 대한 값을 지정합니다.

   * **서버 URL:** JEE 서버에서 AEM Forms의 HTTPS URL을 지정합니다. https를 통한 통신을 활성화하려면 -Djavax.net.ssl.trustStore=&lt;JEE 키 저장소 파일의 AEM Forms 경로> 매개 변수를 사용하여 JEE 서버에서 AEM Forms을 다시 시작합니다.
   * **2 방향 SSL** 사용:2 방향 SSL 활성화 옵션을 활성화합니다.
   * **키 저장소 파일 URL**:키 저장소 파일의 URL을 지정합니다.
   * **TrustStore URL**:truststore 파일의 URL을 지정합니다.
   * **키 저장소 암호**:키 저장소 파일의 암호를 지정합니다.
   * **TrustStorePassword**:truststore 파일의 암호를 지정합니다.
   * **서비스 이름**:지정된 서비스 목록에 RightsManagementService를 추가합니다.

   **저장**&#x200B;을 클릭합니다. AEM에서 문서 보안 보호 PDF 및 Microsoft Office 문서를 검색할 수 있습니다.

## 정책으로 보호된 샘플 PDF 또는 Microsoft Office 문서 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document} 색인화

1. AEM Assets에 관리자로 로그인합니다.
1. AEM Digital Asset Manager에서 폴더를 만들고 정책으로 보호된 PDF 또는 Microsoft Office 문서를 새로 만든 폴더에 업로드합니다. 이제 AEM 검색을 사용하여 정책으로 보호된 문서의 컨텐츠를 검색할 수 있습니다. 검색된 텍스트가 포함된 문서를 반환해야 합니다.

