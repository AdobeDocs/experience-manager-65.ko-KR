---
title: 의 릴리스 정보 [!DNL Adobe Experience Manager] 6.5
description: 에 대한 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 목록을 확인하십시오. [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: d6435255835d91729519f7822b9677608b6b9f1e
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 9%

---

# [!DNL Adobe Experience Manager] 6.5 최신 서비스 팩 릴리스 노트 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 릴리스 정보 {#release-information}

| 제품 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 버전 | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2024년 5월 23일 목요일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 에 포함된 항목 [!DNL Experience Manager] 6.5.21.0 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] 6.5.21.0에는 2019년 4월 6.5의 최초 출시 이후 릴리스된 새로운 기능, 주요 고객 요청 개선 사항, 버그 수정 사항 및 성능, 안정성, 보안 개선 사항이 포함되어 있습니다. [이 서비스 팩 설치](#install) 날짜 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## 주요 기능 및 개선 사항

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

이 릴리스의 몇 가지 주요 기능 및 개선 사항은 다음과 같습니다.

* 기존 서비스 계정(JWT) 자격 증명을 대체하여 서버 간 인증을 위해 새롭고 사용하기 쉬운 자격 증명. (NPR-41994) 메이저

### [!DNL Forms]

* A

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 서비스 팩 21의 문제가 해결되었습니다. {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### 접근성 {#sites-accessibility-6521}

* 다음 **[!UICONTROL 저장한 검색 결과]** 레이블이 지속되지 않습니다. 자리 표시자가 텍스트 필드에 대한 유일한 시각적 레이블로 사용되고 있습니다.(SITES-3050)

#### 관리 사용자 인터페이스{#sites-adminui-6521}

* 다음을 클릭: **[!UICONTROL 사이트]** > **[!UICONTROL 핵심 구성 요소]** > **[!UICONTROL 속성]** > **[!UICONTROL 권한]** 탭 > **[!UICONTROL 유효 권한]**, **유효 권한** 대화 상자가에 열리지 않습니다. (SITES-17378)

#### 클래식 UI{#sites-classicui-6521}

* 화

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* 양식 요소의 이중 포함을 수정했습니다. (SITES-21109) BLOCKER
* 콘텐츠 조각을 만들 때 닫기 버튼이 응답하지 않는 경우가 있어 전체 페이지가 동결되고 콘텐츠 조각을 닫으려면 페이지를 새로 고쳐야 합니다. 버전 생성 문제는 사용자가 변경하지 않은 경우에도 RTE 또는 텍스트 필드와 상호 작용하여 새로운 버전의 콘텐츠 조각을 만드는 것입니다. (SITES-21187) 메이저


#### [!DNL Content Fragments] - GRAPHQL API {#sites-graphql-api-6521}

* Adobe Experience Manager을 6.5.19.0에서 6.5.20.0으로 업그레이드하는 동안 다음 경로가 `/libs/cq/graphql/sites/graphiql` 이(가) 삭제되었습니다. (SITES-20098) 중요




#### [!DNL Content Fragments] - GraphQL 쿼리 편집기{#sites-graphql-query-editor-6521}

* 수

#### [!DNL Content Fragments] - 나머지 API{#sites-restapi-6521}

* 수

#### 핵심 백엔드{#sites-core-backend-6521}

* 수

#### 핵심 구성 요소{#sites-core-components-6521}

* I

#### Campaign 통합{#sites-campaign-integration-6521}

* A

#### 경험 조각{#sites-experiencefragments-6521}

* 에서 경험 조각 롤아웃 `masters/language` 끝 `country/language` 는 상호 참조를 업데이트하지 않습니다. (SITES-20559) BLOCKER
* 에 지정된 템플릿만 `cq:allowedTemplates`, 그러나 다음을 포함하는 템플릿 `allowedPaths` 템플릿 수준에서 구성한 은 새 경험 조각을 만들 때 옵션으로 나타납니다. (SITES-20855) 메이저

#### 기초 구성 요소 (기존){#sites-foundation-components-legacy-6521}

* 화

#### 론치{#sites-launches-6521}

* 다음 `sourceRootResource` CRXDE Lite 내의 Launch 구성에 더 이상 존재하지 않는 콘텐츠를 가리키도록 구성되어 있어 실행을 삭제하려고 할 때 오작동이 발생합니다. 페이지가 삭제되거나 경로가 동일하지 않은 경우에도 론치를 삭제할 수 있어야 합니다. (SITES-20750)

#### MSM - 라이브 카피{#sites-msm-live-copies-6521}

* 페이지 구성 요소를 오버레이하여 페이지 속성에 탭을 추가했습니다. 그 중 하나는 페이지 구성이며 경험 조각 URL을 추가할 수 있는 속성이 있습니다. 경험 조각의 페이지 속성에 구성된 링크는 해당 페이지에 대해 만들어진 언어 사본에 대해 변경되지 않습니다. 구성된 링크는 언어 사본 URL을 사용하여 변경해야 합니다. (SITES-19580) 메이저

#### 페이지 편집기{#sites-pageeditor-6521}

* 편집 모드는 WCAG(Web Content Accessibility Guidelines) 색상 대비 표준을 준수하지 않는 회색 배경을 일관성 없이 적용합니다. (SITES-20060)

### [!DNL Assets]{#assets-6521}

* U

#### [!DNL Dynamic Media]{#assets-dm-6521}

* 2024년 5월 1일부터 Dynamic Media Adobe은 다음 사항에 대한 지원을 종료합니다.
   * SSL(Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS(전송 계층 보안) 1.0 및 1.1
   * TLS 1.2의 약한 암호는 다음과 같습니다.
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

### [!DNL Forms]{#forms-6521}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.21.0 Forms add-on package release is scheduled for Thursday, May 30, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* 
  <!-- THIS BUG WAS ALREADY REPORTED IN 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


#### [!DNL Forms Designer] {#forms-designer-6521}

* 수


### Foundation {#foundation-6521}



#### Apache Felix {#felix-6521}

* SP19 설치 후 Apache Felix에 대한 권한 없는 요청에 대해 애플리케이션 서버 컨텍스트 루트 경로가 누락되는 AEM 6.5 서비스 팩 19(SP19)의 업그레이드 문제. Apache Felix Web Management Console 4.9.8로 업데이트합니다. (NPR-41933)

* U

#### 커뮤니티 {#communities-6521}

* 화

#### 컨텐츠 배포{#foundation-content-distribution-6521}

* 화

#### 통합{#integrations-6521}

* 서비스 계정(JSON 웹 토큰 또는 JWT) 자격 증명을 OAuth2 서버 간 자격 증명(서비스 주체)으로 바꿉니다.(NPR-41994) 메이저
* IMS(Identity Management System) 구성으로 대상 만들기 요청이 실패합니다. (NPR-41888) 메이저
* 고객이 페이로드 페이지를 보려고 할 때 잘못된 URL로 인해 콘텐츠가 제대로 표시되지 않습니다. 404 오류가 표시됩니다. 이(가) 쿼리 매개 변수 앞에 URL에 물음표 기호를 누락하여 오류가 발생합니다. 이 문제를 해결하려면 고객이 물음표 기호를 수동으로 삽입하여 페이로드 페이지를 올바르게 조회해야 합니다. (NPR-41957)
* AEM 6.5에서 다음 코드 및 Adobe Search&amp;Promote 종속성 제거 [공지 사항에 따라 2022년 9월 서비스 종료](https://experienceleague.adobe.com/en/docs/discontinued/using/search-promote). (NPR-41855)


#### 현지화{#localization-6521}

* 템플릿 편집기에서 텍스트 문자열 *`No video available.`* 은(는) 현지화되지 않습니다. (SITES-13190)

#### Platform{#foundation-platform-6521}

* 다음 `Unclosed resource resolver` 다음에 대한 오류가 발생했습니다. `com.day.cq.mailer.impl.DefaultMailService`. 다음 `MessageGatewayService` resource resolver 없이 기본 클래스인 클래스를 사용하고 있었습니다. 이 클래스를 사용하여 전자 메일을 보내는 양식 제출 단추가 있는 모든 페이지에서 문제가 발생했습니다. (NPR-41853)

#### 슬링{#foundation-sling-6521}

* 화

#### 번역{#foundation-translation-6521}

* 여러 구성을 만들고 번역 Cloud Service 구성으로 이동할 때 일부 요소가 UI에 표시되는 것은 아닙니다. 처음 40개 요소/폴더만 표시되고 소극적 로드가 트리거되지만 더 이상 컨텐츠를 추가하지 않습니다. (NPR-41829)

#### 사용자 인터페이스{#foundation-ui-6521}

* 더 그래닛 `pathfield` 구성 요소 `/libs/granite/ui/components/coral/foundation/form/pathfield` 을(를) 활성화하지 못했습니다. **[!UICONTROL 선택]** 자산을 선택할 때 단추입니다. pathfield가 팝업되고 에셋 확인란을 선택하면 **[!UICONTROL 선택]** 버튼이 활성화되지 않고 회색에서 파란색으로 변경되지 않습니다. (NPR-41970)
* AEM 내의 CFM(Content Fragment Model) 참조 필드에 문제가 있습니다. CFM 참조 필드가 필수로 설정되었더라도 특정 시나리오에서 사용자가 저장 을 클릭하여 CFM이 아닌 값으로 콘텐츠를 저장할 수 있습니다. 저장 버튼이 흐리게 표시됩니다(사용할 수 없음). (NPR-41894)

#### WCM{#wcm-6521}

* 화

#### 워크플로{#foundation-workflow-6521}

* 화

## 설치 [!DNL Experience Manager] 6.5.21.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0을 사용하려면 [!DNL Experience Manager] 6.5. 참조 [업그레이드 설명서](/help/sites-deploying/upgrade.md) 자세한 지침은 을 참조하십시오. <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 다음을 설치합니다. [!DNL Experience Manager] 패키지 관리자를 사용하는 작성자 인스턴스 중 하나에서 6.5.21.0.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe은 를 제거하거나 제거하지 않는 것이 좋습니다. [!DNL Experience Manager] 6.5.21.0 패키지. 따라서 팩을 설치하기 전에 `crx-repository` 혹시라도 돌려주셔야 할 것 같은데요 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 서비스 팩 설치 [!DNL Experience Manager] 6.5{#install-service-pack}

1. 인스턴스가 업데이트 모드에 있는 경우(인스턴스가 이전 버전에서 업데이트된 경우) 설치 전에 인스턴스를 다시 시작하십시오. Adobe은 인스턴스의 현재 가동 시간이 높을 경우 다시 시작할 것을 권장합니다.

1. 설치하기 전에 스냅샷 또는 새 백업을 [!DNL Experience Manager] 인스턴스.

1. 에서 서비스 팩 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 패키지 관리자를 열고 를 선택합니다 **[!UICONTROL 패키지 업로드]** 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md).

1. 패키지를 선택한 다음 를 선택합니다 **[!UICONTROL 설치]**.

1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 있는 새 이진 파일로 바꾼 다음 인스턴스를 다시 시작하십시오. 다음을 참조하십시오 [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>패키지 관리자 UI에 대한 대화 상자가 서비스 팩을 설치하는 동안 종료되는 경우가 있습니다. 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다리는 것이 좋습니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는에서 발생합니다. [!DNL Safari] 브라우저이지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

**자동 설치**

를 사용하여 자동으로 설치할 수 있는 두 가지 방법이 있습니다 [!DNL Experience Manager] 6.5.21.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 패키지 배치 위치 `../crx-quickstart/install` 폴더를 사용하십시오. 패키지가 자동으로 설치됩니다.
* 사용 [패키지 관리자의 HTTP API](/help/sites-administering/package-manager.md#package-share). 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.21.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 다음을 참조하십시오. [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`) 업데이트된 버전 문자열을 표시합니다 `Adobe Experience Manager (6.5.21.0)` 아래에 [!UICONTROL 설치된 제품]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

1. OSGi 번들 `org.apache.jackrabbit.oak-core` 는 버전 1.22.18 이상입니다(웹 콘솔 사용: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 서비스 팩 설치 [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Experience Manager Forms에 서비스 팩을 설치하는 방법은 다음을 참조하십시오. [Experience Manager Forms 서비스 팩 설치 지침](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>[AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html)에서 사용 가능한 적응형 양식 기능은 탐색 및 평가 목적으로만 사용하도록 설계되었습니다. 프로덕션 용도로 사용하려면 적응형 양식 기능에 적절한 라이선싱이 필요하므로 AEM Forms에 대해 유효한 라이선스를 확보해야 합니다.

### Experience Manager 콘텐츠 조각용 GraphQL 인덱스 패키지 설치{#install-aem-graphql-index-add-on-package}

GraphQL을 사용하는 고객은 [GraphQL 인덱스 패키지 1.1.1로 Experience Manager 컨텐츠 조각](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

이렇게 하면 필요한 인덱스 정의가 실제로 사용하는 기능을 기반으로 추가할 수 있습니다.

이 패키지를 설치하지 않으면 GraphQL 쿼리가 느려지거나 실패할 수 있습니다.

>[!NOTE]
>
>이 패키지는 인스턴스당 한 번만 설치하십시오. 모든 서비스 팩으로 다시 설치할 필요는 없습니다.

### UberJar{#uber-jar}

에 대한 UberJar [!DNL Experience Manager] 6.5.21.0은 [Maven Central 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven 프로젝트에서 UberJar를 사용하려면 [uberJar 사용 방법](/help/sites-developing/ht-projects-maven.md) 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.21</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar 및 기타 관련 아티팩트는 공개 Maven 저장소 Adobe 대신 Maven 중앙 저장소에서 사용할 수 있습니다(`repo.adobe.com`). 기본 UberJar 파일의 이름이 로 바뀝니다. `uber-jar-<version>.jar`. 그래서, `classifier`, 포함 `apis` 값으로, 을 사용합니다. `dependency` 태그에 가깝게 배치하십시오.


## 이제 사용되지 않는 기능과 제거된 기능{#removed-deprecated-features}

다음을 참조하십시오 [사용이 중단되거나 제거된 기능](/help/release-notes/deprecated-removed-features.md/).

## 알려진 문제{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


* **Oak 관련**
서비스 팩 13 이상부터 지속성 캐시에 영향을 주는 다음 오류 로그가 나타나기 시작했습니다.

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  또는

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  이 예외를 해결하려면 다음을 수행합니다.

   1. 에서 다음 두 폴더를 삭제합니다. `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. 서비스 팩을 설치하거나 Experience Manager을 as a Cloud Service으로 다시 시작합니다.
의 새 폴더 `cache` 및 `diff-cache` 이(가) 자동으로 만들어지므로 더 이상 과 관련된 예외가 발생하지 않습니다. `mvstore` 다음에서 `error.log`.

* 콘텐츠 모델의 기본 이름을 대신 사용하도록 콘텐츠 모델에 대해 사용자 지정 API 이름을 사용했을 수 있는 GraphQL 쿼리를 업데이트합니다.

* GraphQL 쿼리는 `damAssetLucene` 색인 대신 `fragments` 색인입니다. 이 작업으로 인해 GraphQL 쿼리가 실패하거나 실행하는 데 시간이 오래 걸릴 수 있습니다.

  문제를 해결하려면 `damAssetLucene` 다음 두 속성을 포함하도록 구성해야 합니다. `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  색인 정의를 변경한 후에는 리인덱싱이 필요합니다(`reindex` = `true`).

  이러한 단계 후에는 GraphQL 쿼리가 더 빨리 수행됩니다.

* 콘텐츠 조각, 사이트 또는 페이지를 이동, 삭제 또는 게시하려고 할 때 배경 쿼리가 실패하여 콘텐츠 조각 참조를 가져올 때 문제가 있습니다. 즉, 기능이 작동하지 않습니다.
올바른 작업을 위해 인덱스 정의 노드에 다음 속성을 추가해야 합니다 `/oak:index/damAssetLucene` (리인덱싱이 필요하지 않음):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 업그레이드 시 [!DNL Experience Manager] 6.5.0 - 6.5.4에서 Java™ 11의 최신 서비스 팩까지 인스턴스가 제공됩니다. `RRD4JReporter` 의 예외 `error.log` 파일. 예외를 중지하려면 인스턴스를 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 사용자는 의 계층 구조에서 폴더의 이름을 변경할 수 있습니다. [!DNL Assets] 중첩된 폴더 게시 위치 [!DNL Brand Portal]. 단, 폴더의 제목은에서 업데이트되지 않습니다. [!DNL Brand Portal] 루트 폴더가 다시 게시될 때까지.

* 설치 중에 다음과 같은 오류 및 경고 메시지가 표시될 수 있습니다. [!DNL Experience Manager] 6.5.x.x:
   * &quot;Adobe Target 통합이에서 구성된 경우 [!DNL Experience Manager] target Standard API(IMS 인증)를 사용한 다음 경험 조각을 Target으로 내보내면 잘못된 오퍼 유형이 생성됩니다. 경험 조각/소스 &quot;Adobe Experience Manager&quot; 유형 대신 Target은 &quot;HTML&quot;/소스 &quot;Adobe Target Classic&quot; 유형으로 여러 오퍼를 만듭니다.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: granite/operations/maintenance에 유지 관리 창이 없습니다.
   * SUM, MAX 및 MIN과 같은 집계 함수를 사용하는 경우 적용형 양식 서버측 유효성 검사가 실패합니다(CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance에 유지 관리 창이 없습니다.
   * 쇼퍼블 배너 뷰어를 통해 자산을 미리 볼 때 Dynamic Media 대화형 이미지의 핫스팟이 표시되지 않습니다.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 등록 변경이 등록 취소를 완료할 때까지 기다리는 동안 시간이 초과되었습니다.

* AEM 6.5.15부터 Rhino JavaScript Engine은 ```org.apache.servicemix.bundles.rhino``` 번들에 새로운 호스팅 동작이 있습니다. 엄격 모드를 사용하는 스크립트(```use strict;```) 변수를 올바르게 선언해야 합니다. 그렇지 않으면 런타임 오류가 발생하는 대신 실행되지 않습니다.

* 공식 업데이트 패키지(서비스 팩, 보안 서비스 팩, 확장 기능 팩, 누적 기능 팩, 패치 등)를 통해 태깅 관련 기본 제공 콘텐츠를 설치하면 의 언어 속성이 재설정됩니다. `/content/cq:tags` 노드를 기본값으로 설정합니다. 따라서 설치하기 전에 속성에서 추가해야 합니다.

### AEM Sites의 알려진 문제 {#known-issues-aem-sites-6521}

* SITES-17934 - 콘텐츠 조각 - 대용량 조각 트리에 대한 DoS 보호로 인해 미리보기가 실패합니다. 다음을 참조하십시오. [기본 GraphQL 쿼리 실행자 구성 옵션에 대한 KB 문서](https://experienceleague.adobe.com/ko/docs/experience-cloud-kcs/kbarticles/ka-23945)

### AEM Forms의 알려진 문제 {#known-issues-aem-forms-6521}

* 화

## OSGi 번들 및 콘텐츠 패키지가 포함됨{#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 이에 포함된 OSGi 번들 및 콘텐츠 패키지가 기재되어 있습니다. [!DNL Experience Manager] 6.5 서비스 팩 릴리스:

* [Experience Manager 6.5.21.0에 포함된 OSGi 번들 목록](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.21.0에 포함된 컨텐츠 패키지 목록](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 고객이고 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 문의](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Adobe 우선 순위 제품 업데이트 구독](https://www.adobe.com/kr/subscription/priority-product-update.html)
