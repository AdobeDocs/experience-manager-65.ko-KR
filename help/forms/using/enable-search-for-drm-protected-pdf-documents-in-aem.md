---
title: AEM에서 문서 보안 보호된 PDF 문서를 검색할 수 있도록 설정
seo-title: AEM에서 문서 보안 보호된 PDF 문서를 검색할 수 있도록 설정
description: '기본 AEM 검색을 활성화하여 DRM으로 보호된 PDF 문서에서 전체 텍스트 검색을 수행하는 방법을 알아봅니다.  '
seo-description: '기본 AEM 검색을 활성화하여 DRM으로 보호된 PDF 문서에서 전체 텍스트 검색을 수행하는 방법을 알아봅니다.  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---


# AEM에서 문서 보안 보호된 PDF 문서를 검색할 수 있도록 설정{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM 검색은 AEM 자산을 검색 및 찾고 일반 텍스트 파일, Microsoft Office 문서 및 PDF 문서와 같이 일반적으로 사용되는 다양한 문서 형식에서 텍스트 검색을 수행할 수 있습니다. 기본 검색을 확장하여 AEM Document 보안으로 보호되는 [PDF 문서에서 전체 텍스트 검색을 수행할 수도 있습니다](../../forms/using/admin-help/document-security.md). AEM에서 이러한 문서에서 전체 텍스트 검색을 수행하려면 다음 단계를 수행하십시오.

1. 보안 연결 설정
1. 정책으로 보호된 샘플 PDF 문서 색인화

## 전제 조건 {#prerequisites}

* OSGi에서 AEM Forms을 사용하는 경우:

   * AEM Forms 서버에 [AEM Forms Document Security Indexer 패키지를](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 설치합니다.

   * JEE 서버의 AEM Forms이 작동 중이고 문서 보안이 JEE 서버의 해당 AEM Forms에 설치되어 있는지 확인합니다. 보호된 문서를 색인화하려면 JEE 서버의 AEM Form이 필요합니다.

* JEE 서버에서 AEM Forms만 사용하는 경우 인덱서 패키지가 이미 설치되어 있습니다.
* 모든 번들이 실행되고 있는지 확인합니다. 모든 번들이 활성 상태가 아니면 모든 번들이 실행되고 있을 때까지 기다리십시오.

   * OSGi의 AEM Forms의 경우 번들은 https://&#39;[server]:[port]&#39;/system/console/bundles에 나열되어 있습니다.
   * JEE의 AEM Forms의 경우 번들은 https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles에 나열되어 있습니다. 예: https://localhost:8080/lc/system/console/bundles.

* allowlist에 *sun.util.calendar* 패키지를 추가합니다. allowlist에 패키지를 추가하려면 다음 단계를 수행하십시오.

   1. AEM 웹 콘솔을 엽니다. URL은 https://&#39;[server]:[port]&#39;/system/console/configMgr입니다.
   1. Deserialization **방화벽 구성을 찾아 엽니다**.

   1. sun.util.calendar 패키지를 Allowlisted 클래스 또는 패키지 접두어 필드에 추가하고 저장을 **클릭합니다**.

### AEM Forms JEE와 OSGi 스택 간의 안전한 연결 설정 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

다음 방법 중 하나를 사용하여 보안 연결을 설정할 수 있습니다.

* JEE 관리자 자격 증명에 AEM Forms이 포함된 Adobe LiveCycle Client SDK 번들 구성
* 상호 인증을 사용하여 Adobe LiveCycle Client SDK 번들 구성

#### JEE 관리자 자격 증명에 AEM Forms이 포함된 Adobe LiveCycle Client SDK 번들 구성 {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM 웹 콘솔을 엽니다. URL은 https://&#39;[server]:[port]&#39;/system/console/configMgr입니다.
1. Adobe LiveCycle **Client SDK 번들을 찾아 엽니다**. 다음 필드에 값을 지정합니다.

   * **서버 URL:** JEE 서버에서 AEM Forms의 HTTPS URL을 지정합니다. https를 통한 통신을 활성화하려면 -Djavax.net.ssl.trustStore=&lt;JEE keystore 파일의 AEM Forms 경로> 매개 변수를 사용하여 서버를 다시 시작하십시오.
   * **서비스 이름**: 지정된 서비스 목록에 RightsManagementService를 추가합니다.
   * **사용자 이름:** AEM 서버로부터의 호출을 시작하는 데 사용할 JEE 계정의 AEM Forms의 사용자 이름을 지정합니다. 지정한 계정에는 JEE 서버의 AEM Forms에서 문서 서비스를 시작할 수 있는 권한이 있어야 합니다.
   * **암호**: 사용자 이름 필드에 언급된 JEE 계정의 AEM Forms 암호를 지정합니다.

   **저장**&#x200B;을 클릭합니다. AEM이 문서 보안 보호된 PDF 문서를 검색할 수 있도록 설정되어 있습니다.

#### 상호 인증을 사용하여 Adobe LiveCycle Client SDK 번들 구성 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. JEE에서 AEM Forms에 대한 상호 인증 활성화 자세한 내용은 [CAC 및 상호 인증을 참조하십시오](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. AEM 웹 콘솔을 엽니다. URL은 https://&#39;[server]:[port]&#39;/system/console/configMgr입니다.
1. Adobe LiveCycle Client SDK **번들을 찾아** 엽니다. 다음 속성의 값을 지정합니다.

   * **서버 URL**: JEE 서버에서 AEM Forms의 HTTPS URL을 지정합니다. https를 통한 통신을 활성화하려면 -Djavax.net.ssl.trustStore=&lt;JEE keystore 파일의 AEM Forms 경로> 매개 변수를 사용하여 AEM 서버를 다시 시작하십시오.
   * **양방향 SSL 활성화**: 양방향 SSL 활성화 옵션을 활성화합니다.
   * **KeyStore 파일 URL**: 키 저장소 파일의 URL을 지정합니다.
   * **TrustStore URL**: truststore 파일의 URL을 지정합니다.
   * **키 저장소 암호**: 키 저장소 파일의 암호를 지정합니다.
   * **TrustStorePassword**: truststore 파일의 암호를 지정합니다.
   * **서비스 이름**: 지정된 서비스 목록에 RightsManagementService를 추가합니다.

   **저장**&#x200B;을 클릭합니다. AEM이 문서 보안 보호된 PDF 문서를 검색하도록 활성화되어 있습니다.

### 정책으로 보호된 샘플 PDF 문서 색인화 {#index-a-sample-policy-protected-pdf-document}

1. 관리자로 AEM Assets에 로그인합니다.
1. AEM Digital Asset Manager에서 폴더를 만들고 정책으로 보호된 PDF 문서를 새로 만든 폴더에 업로드합니다.

   이제 AEM 검색을 사용하여 정책으로 보호된 문서를 검색할 수 있습니다.

