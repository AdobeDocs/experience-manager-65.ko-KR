---
title: AEM에서 문서 보안으로 보호된 PDF 문서를 검색할 수 있도록 설정
description: DRM 보호 PDF 문서에서 전체 텍스트 검색을 수행할 수 있도록 기본 AEM 검색을 활성화하는 방법에 대해 알아봅니다.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
source-git-commit: d195ac80ee59439bab5b1219a2c1f16e93e3d22b
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# AEM에서 문서 보안으로 보호된 PDF 문서를 검색할 수 있도록 설정{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM search는 AEM assets를 검색 및 찾고 일반 텍스트 파일, Microsoft Office 문서 및 PDF 문서와 같이 일반적으로 사용되는 다양한 문서 형식에 대해 텍스트 검색을 수행할 수 있습니다. 기본 검색을 확장하여 전체 텍스트 검색을 수행할 수도 있습니다 [AEM Document Security로 보호된 문서 PDF](../../forms/using/admin-help/document-security.md). AEM에서 이러한 문서에 대해 전체 텍스트 검색을 수행할 수 있도록 하려면 다음 단계를 수행합니다.

1. 보안 연결 설정
1. 정책으로 보호된 샘플 PDF 문서 색인화

## 사전 요구 사항 {#prerequisites}

* OSGi에서 AEM Forms을 사용하는 경우:

   * 설치 [AEM Forms Document Security Indexer 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) AEM Forms 서버에서 확인할 수 있습니다.

   * JEE 서버의 AEM Forms이 실행 중이고 JEE 서버의 해당 AEM Forms에 문서 보안이 설치되어 있는지 확인합니다. 보호된 문서를 인덱싱하려면 JEE 서버의 AEM Form이 필요합니다.

* JEE 서버에서 AEM Forms만 사용하는 경우 인덱서 패키지가 이미 설치되어 있습니다.
* 모든 번들이 실행 중인지 확인합니다. 모든 번들이 활성화되지 않은 경우 모든 번들이 실행되고 실행될 때까지 기다립니다.

   * OSGi의 AEM Forms에 대한 번들은 https://&#39;에 나열되어 있습니다.[server]:[포트]&#39;/system/console/bundles.
   * JEE의 AEM Forms의 경우, 번들은 https://&#39;에 나열되어 있습니다.[server]:[포트]&#39;/[context-path]/system/console/bundles. 예: https://localhost:8080/lc/system/console/bundles.

* 추가 *sun.util.calendar* 패키지가 허용 목록에 전송됩니다. 패키지를 허용 목록에 추가하다에 추가하려면 다음 단계를 수행하십시오.

   1. AEM 웹 콘솔을 엽니다. URL은 https://&#39; 입니다.[server]:[포트]&#39;/system/console/configMgr.
   1. 찾기 및 열기 **역직렬화 방화벽 구성**.

   1. 허용 목록에추가된 클래스 또는 패키지 접두사 필드에 sun.util.calendar 패키지를 추가하고 **저장**.

### AEM Forms JEE와 OSGi 스택 간의 보안 연결을 설정합니다. {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

다음 방법 중 하나를 사용하여 보안 연결을 설정할 수 있습니다.

* JEE 관리자 자격 증명에서 AEM Forms으로 Adobe LiveCycle 클라이언트 SDK 번들 구성
* 상호 인증을 사용하여 Adobe LiveCycle 클라이언트 SDK 번들 구성

#### JEE 관리자 자격 증명에서 AEM Forms으로 Adobe LiveCycle 클라이언트 SDK 번들 구성 {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM 웹 콘솔을 엽니다. URL은 https://&#39; 입니다.[server]:[포트]&#39;/system/console/configMgr.
1. 을(를) 찾아 엽니다. **Adobe LiveCycle 클라이언트 SDK 번들**. 다음 필드에 대한 값을 지정하십시오.

   * **서버 URL:** JEE 서버에서 AEM Forms의 HTTPS URL을 지정합니다. https를 통해 통신을 활성화하려면 -Djavax.net.ssl.trustStore=를 사용하여 서버를 다시 시작하십시오.&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 매개 변수.
   * **서비스 이름**: 지정된 서비스 목록에 RightsManagementService를 추가합니다.
   * **사용자 이름:** AEM 서버에서 호출을 시작하는 데 사용할 AEM Forms on JEE 계정의 사용자 이름을 지정합니다. 지정된 계정에 JEE 서버의 AEM Forms에서 문서 서비스를 시작할 수 있는 권한이 있어야 합니다.
   * **암호**: 사용자 이름 필드에 언급된 JEE의 AEM Forms 계정에 대한 암호를 지정합니다.

   **저장**&#x200B;을 클릭합니다. AEM은 문서 보안으로 보호된 PDF 문서를 검색할 수 있도록 활성화됩니다.

#### 상호 인증을 사용하여 Adobe LiveCycle 클라이언트 SDK 번들 구성 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. JEE에서 AEM Forms에 대한 상호 인증을 활성화합니다. 자세한 내용은 [CAC 및 상호 인증](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. AEM 웹 콘솔을 엽니다. URL은 https://&#39; 입니다.[server]:[포트]&#39;/system/console/configMgr.
1. 을(를) 찾아 엽니다. **Adobe LiveCycle 클라이언트 SDK** 번들. 다음 속성에 대한 값을 지정합니다.

   * **서버 URL**: JEE 서버에서 AEM Forms의 HTTPS URL을 지정합니다. https를 통해 통신을 활성화하려면 -Djavax.net.ssl.trustStore=를 사용하여 AEM 서버를 다시 시작합니다.&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> 매개 변수.
   * **양방향 SSL 활성화**: 양방향 SSL 활성화 옵션을 활성화합니다.
   * **키 저장소 파일 URL**: 키 저장소 파일의 URL을 지정합니다.
   * **TrustStore 파일 URL**: truststore 파일의 URL을 지정합니다.
   * **KeyStore 암호**: 키 저장소 파일의 암호를 지정합니다.
   * **트러스트 스토어 암호**: truststore 파일의 암호를 지정합니다.
   * **서비스 이름**: 지정된 서비스 목록에 RightsManagementService를 추가합니다.

   **저장**&#x200B;을 클릭합니다. AEM을 사용하면 문서 보안으로 보호된 PDF 문서를 검색할 수 있습니다.

### 정책으로 보호된 샘플 PDF 문서 색인화 {#index-a-sample-policy-protected-pdf-document}

1. 관리자로 AEM Assets에 로그인합니다.
1. AEM Digital Asset Manager에서 폴더를 만들고 정책으로 보호된 PDF 문서를 새로 만든 폴더에 업로드합니다.

   이제 AEM 검색을 사용하여 정책으로 보호된 문서를 검색할 수 있습니다.

   >[!NOTE]
   >
   > SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.
