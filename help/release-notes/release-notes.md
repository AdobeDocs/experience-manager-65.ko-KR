---
title: 의 릴리스 정보 [!DNL Adobe Experience Manager] 6.5
description: 에 대한 릴리스 정보, 새로운 기능, 설치 방법 및 자세한 변경 목록을 확인하십시오. [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
exl-id: a52311b9-ed7a-432e-8f35-d045c0d8ea4c
source-git-commit: 7f150219bce3036c0e330b7349e679fdf19797d1
workflow-type: tm+mt
source-wordcount: '3688'
ht-degree: 4%

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
| 버전 | 6.5.20.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2024년 2월 22일 목요일 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 다운로드 URL | [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 에 포함된 항목 [!DNL Experience Manager] 6.5.20.0 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] 6.5.20.0에는 2019년 4월 6.5의 최초 출시 이후 릴리스된 새로운 기능, 주요 고객 요청 개선 사항, 버그 수정 사항 및 성능, 안정성, 보안 개선 사항이 포함되어 있습니다. [이 서비스 팩 설치](#install) 날짜 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## 주요 기능 및 개선 사항

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

이 릴리스의 몇 가지 주요 기능 및 개선 사항은 다음과 같습니다.

* 이제 Dynamic Media은 Apple iOS/iPadOS에 대해 무손실 HEIC 이미지 형식을 지원합니다. 다음을 참조하십시오 [fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=en) Dynamic Media 이미지 제공 및 렌더링 API에서.

* 이제 MSM(Multisite Manager)은 경험 조각을 라이브 카피로 효율적으로 대량 롤아웃하기 위해 폴더 및 하위 폴더를 포함한 경험 조각 구조를 지원합니다.

### [!DNL Forms]

* **JEE의 AEM Forms에서 거래 보고**: JEE의 AEM Forms에 트랜잭션 보고 기능이 도입되어 전환, 변환 및 제출과 같은 문서 트랜잭션을 종합적으로 기록할 수 있습니다. 이러한 향상된 기능은 효율성을 향상시키고 기록 보관을 용이하게 합니다. 이 기능은 기본적으로 비활성화되어 있습니다. 관리자 UI에서 활성화할 수 있습니다.
* **ECDSA 지원을 통해 보안 강화**: 이제 AEM Forms은 JEE와 OSGi 스택 모두에서 ECDSA(Elliptic Curve Digital Signature Algorithm)를 강력하게 지원합니다. 이제 사용자는 강화된 보안으로 PDF 문서에 서명, 인증 및 확인할 수 있습니다. 지원되는 EC 곡선 알고리즘은 다음과 같습니다.
   * SHA256 다이제스트 알고리즘을 사용한 ECDSA 타원 곡선 P256
   * SHA384 다이제스트 알고리즘을 사용한 ECDSA 타원 곡선 P384
   * SHA512 다이제스트 알고리즘을 사용한 ECDSA 타원 곡선 P512
* **Forms Designer용 Windows 11과의 원활한 호환성**: 이제 AEM Forms Designer에서 Windows 11을 지원하여 원활한 설치 및 운영을 보장합니다. 사용자는 Forms Designer를 다시 설치하거나 호환성 문제에 대한 걱정 없이 Windows 11로 자신 있게 업그레이드할 수 있으므로 워크플로우가 중단되지 않습니다.
* **AEM Forms Designer에서 사용자 지정 &quot;캡션&quot; 역할을 사용하여 접근성을 개선했습니다**: 이제 AEM Forms Designer에는 &quot;캡션&quot;이라는 사용자 정의 접근성 역할이 포함되어 사용자가 개인화된 캡션 요소로 XDP를 만들 수 있습니다. 이 기능을 사용하면 사용자가 사용자 정의 캡션을 문서 디자인에 통합하여 포괄성과 사용자 경험을 향상시킬 수 있으므로 접근성을 향상시킬 수 있습니다.

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 서비스 팩 20의 문제가 해결되었습니다. {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### 관리 사용자 인터페이스{#sites-adminui-6520}

* 다음 `Workflow Title` 필드가 로 표시됨 `*` 필수 사항이지만 유효성 검사가 없습니다. (SITES-16491)

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* 중첩된 구성 폴더는 더 이상 지원되지 않으며 AEM 6.5.18 또는 AEM 6.5.19로 업그레이드한 후에는 콘텐츠 조각 모델 폴더가 더 이상 표시되지 않습니다. (SITES-18110)
* 일부 하위 폴더는 상속된 콘텐츠 조각 모델에서 선택할 수 없습니다. 이 구성 요소는 `jcr:content` 사용자 인터페이스를 통해 생성된 DAM 폴더에 이러한 노드가 있는 경우에도 속성을 사용할 수 있습니다. (SITES-17943)

#### [!DNL Content Fragments] - GRAPHQL API {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* GraphQL 쿼리를 실행할 때 [결과 필터링](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) 특정 값이 다음과 같은 경우 선택적 변수 사용 **아님** 선택 변수에 제공된 경우 변수는 필터 평가에서 무시됩니다. (SITES-17051)

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - 나머지 API{#sites-restapi-6520}

* 를 업그레이드하여 `org.json` 라이브러리에서 10진수가 deserialize되는 방식이 변경되었습니다. Double로 &quot;기본적으로&quot; 변환되기 전에는 이제 BigDecimals로 변환되었습니다. 대신 REST API를 통해 저장된 메타데이터 속성 값은 BigDecimal에서 Double로 변환되어야 합니다. (SITES-16857)

#### 핵심 백엔드{#sites-core-backend-6520}

* 콘텐츠 조각의 빠른 게시 를 사용하면 계속해서 로드되고 게시되지 않습니다. 즉, AEM 6.5.7에서 AEM 6.5.17로 서비스 팩을 업그레이드한 후 콘텐츠 조각에 대해 빠른 게시가 작동하지 않습니다. 사용자가 관리 게시를 시도하면 제대로 작동합니다. 그러나 빠른 게시를 시도했을 때 게시되지 않았습니다. 특히, `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` 이(가) 시스템을 스래쉬(thrash)했습니다. (SITES-17311)
* 컨텐츠 조각은 Jackson Exporter를 사용하여 직렬화할 수 없습니다. 페이지에서 참조된 컨텐츠 조각(Jackson Exporter 코드 사용)과 컨텐츠 조각에 추가된 태그가 있으면 페이지 로드가 중단됩니다. (SITES-18096)

#### 핵심 구성 요소{#sites-core-components-6520}

* AEM에 CIF 핵심 구성 요소 패키지를 설치하면 다음과 같은 문제가 발생합니다. `:type` 변경할 기존 구성 요소의 값입니다. 이 변경 사항은 추가된 페이지에서 더 이상 렌더링하지 않음을 의미합니다. (SITES-17601)

#### Campaign 통합{#sites-campaign-integration-6520}

* AEM은 허용 목록에 추가하다를 사용하고 있었다. `whitelist`- 취약성 보고서로 인해. 허용 목록에 추가하다으로 인해 고객이 필요한 기능을 사용할 수 없었습니다. (SITES-16822)

#### 경험 조각{#sites-experiencefragments-6520}

* 이제 경험 조각용 MSM은 폴더 및 하위 폴더를 포함한 경험 조각 콘텐츠 구조에 대한 벌크 롤아웃을 지원합니다. (SITES-16004)

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM - 라이브 카피{#sites-msm-live-copies-6520}

* An &quot;`Is not modifiable`구성 요소를 롤아웃할 때 예외가 throw됩니다. 특히, `org.apache.sling.servlets.post.impl.operations.ModifyOperation` 응답을 처리하는 동안 예외가 발생했습니다. (SITES-18809)
* 경험 조각의 특정 라이브 카피에 변경 사항을 롤아웃할 수 없습니다. (SITES-17930)
* 사용자가 블루프린트 페이지의 구성 요소에 주석을 추가한 다음 롤아웃하면 라이브 카피의 주석 수가 잘못 표시됩니다. (SITES-17099)
* 터치 그래픽 사용자 인터페이스에서 상위 페이지에서 하위 페이지로의 MSM 롤아웃 버튼이 중단됩니다. 이 버튼을 선택하면 다음 오류가 표시됩니다. `Uncaught TypeError: _g.shared is undefined`. (SITES-16991)

#### 페이지 편집기{#sites-pageeditor-6520}

* Forms 테마 편집기 미리보기가 손상되었습니다. 미리보기를 선택하면 로드 아이콘만 표시됩니다. (SITES-17164)

### [!DNL Assets]{#assets-6520}

* 메타데이터 편집기 도우미에서 규칙 기반 필드를 확인할 수 없으며 &quot;필수 필드 누락&quot; 오류 메시지를 표시합니다. (ASSETS-31396)
* PDF을 다른 위치로 이동한 후 **[!UICONTROL 페이지 보기]** 옵션이 사라집니다. (ASSETS-30538)
* 읽기 권한이 있는 이미지를 선택할 수 없습니다. (ASSETS-32199)
* 보기 설정에서 카드 크기를 변경할 수 없습니다. (ASSETS-31667)
* .oft 파일 형식을 업로드하는 동안 업로드가 실패합니다. (ASSETS-30109)
* 사용자 지정 메타데이터 필드를 보고서에 추가 열로 추가하려고 하면 확인란이 선택되지 않습니다. (ASSETS-31671)
* 에셋 이동 작업이 Experience Manager 서비스 팩 16에서 제대로 작동하지 않습니다. (ASSETS-30598)

#### [!DNL Dynamic Media]{#assets-dm-6520}

* 에셋이 AEM에 업로드되면 `Update_asset` 워크플로우가 트리거됩니다. 그러나 워크플로우는 완료되지 않습니다. 워크플로우는 제품 업로드 단계까지만 완료됩니다. 다음 단계는 Scene7 일괄 업로드이지만 해당 프로세스를 AEM으로 가져오지는 않습니다. (ASSETS-30443)
* Dynamic Media 구성 요소에서 Dynamic Media이 아닌 비디오를 우아하게 처리하는 더 나은 방법이 필요합니다. 이 문제로 인해 인스턴스화하는 동안 예외가 발생했습니다. `dynamicmedia_sly.js`. (ASSETS-31301)
* 미리 보기는 모든 에셋, 적응형 비디오 세트 및 비디오에 대해 작동합니다. 하지만 다음에 대해 403 오류가 발생합니다. `.m3u8` 파일(부수적으로, 여전히 공개 링크를 통해 작동함). (ASSETS-31882)
* 다음 `scene7SmartCropProcessingStatus` 상태가 수정되었습니다. 성공한 경우에도 실패를 표시하는 데 사용되는 스마트 자르기 비디오 메타데이터입니다. (ASSETS-31255)

### [!DNL Forms]{#forms-6520}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* 사용자가 AEM Forms을 AEM에 게시된 URL이 있는 메일링 플랫폼에 통합하려고 할 때 AEM Forms이 를 추가하지 않습니다 `method=post` 페이지를 렌더링하는 동안. 이 문제는 다음과 같은 경우에도 발생합니다 `POST` 은 URL이 있는 제출 액션에 설정됩니다. 이로 인해 메일링 플랫폼에서는 이를 양식으로 인식하지 못합니다. (FORMS-12614)
* 사용자가 AEM Form 서비스 팩 6.5.18.0에서 표시 패턴이 있는 날짜 필드를 선택할 때 키보드를 사용하여 현재 날짜를 선택할 수 없습니다. (FORMS-12736)
* AEM Forms 서비스 팩 6.5.17.0 및 서비스 팩 6.5.18.0에서 사용자가 달력 위젯에서 월 간을 전환할 때 날짜 선택기 구성 요소에 추가 행이 표시됩니다. (FORMS-11869)
* 사용자가 iOS 장치의 첨부 구성 요소에서 &quot;사진 찍기&quot;를 사용하여 이미지를 클릭하면 모든 이미지가 동일한 이름으로 폴더에 추가됩니다. (FORMS-12224)
* 사용자가 라디오 버튼 그룹의 기존 옵션을 업데이트할 때 잘못된 번역 값이 게시됩니다. (FORMS-12575)
* 사용자가 Android™ 장치의 적응형 양식에 문자를 추가하면 Android™ 장치에서 포커스가 맞춰질 때 텍스트 필드에 정의된 최대 문자 수보다 많은 문자를 입력할 수 있습니다. 단, 사용자가 HTML5 입력 유형을 선택하면 작동합니다. (FORMS-12748)
* 일치하는 레이블 Arial® labelledby 및 Arial® 레이블로 인해 화면 판독기에서 이 두 레이블을 구별할 수 없습니다. 이 문제를 해결하려면 양식 필드에 대해 &quot;aria-labelledby&quot;라는 레이블이 &quot;aria-describedby&quot;로 대체됩니다. (FORMS-12436)
* 작성자가 &quot;적응형 Forms - 임베드(v2)&quot; 구성 요소를 사용하여 사이트 페이지에 적응형 양식을 임베드하고 임베드된 양식에 CAPTCHA 구성 요소가 포함된 경우(CAPTCHA 서비스 -> reCAPTCHA, 설정 -> reCAPTCHA-v2), 사용자가 작성자 인스턴스에서 &quot;게시됨으로 보기&quot;를 사용하여 사이트 페이지를 보려고 할 때 사이트 페이지가 렌더링되지 않습니다. 다음 오류가 (FORMS-11859)로 표시됩니다.
  `Failed to construct 'URL': Invalid base URL at Object.renderRecaptcha`

* 사용자가 날짜 선택기 구성 요소를 사용하여 날짜를 선택하려고 하면 값이 업데이트되지 않고 NULL이 표시됩니다. (FORMS-12742, FORMS-12736)

* 사용자가 AEM Form 서비스 팩 6.5.19.0으로 업그레이드할 때 새 언어를 기존 사전에 업데이트한 후 양식에 로케일을 추가하기 위해 &quot;guideContainer&quot; 행과 병합되지 않습니다. (FORMS-12947)

* AEM Forms 서비스 팩 6.5.19.0에서 Java™ 11에서 호출된 웹 서비스 작업이 오류로 실패합니다(FORMS-12329).
  `java.lang.NoClassDefFoundError message:sun/misc/BASE64Decoder`

* 사용자가 AEM Forms 서비스 팩 6.5.18.0에서 &quot;EmailService&quot;에 대한 &quot;receive&quot; 작업을 호출하면 예외가 발생합니다(FORMS-12050).
  `java.util.ServiceConfigurationError: javax.mail.Provider: Provider com.sun.mail.imap.IMAPProvider not a subtype`

* AEM Forms 서비스 팩 6.5.18.0에서 FIPS 모드가 활성화되면 다음 오류가 발생하여 기본 DOM에서 사용자를 만들 수 없습니다(FORMS-11857).
  `com.adobe.idp.cx.a: error seeding random number generator`

* 사용자가 경로 아래에서 ADMINUI의 글꼴을 선택할 때 `Home>Services>PDF Generator>Adobe PDF Settings`, 선택되지 않습니다. 또한 표준 또는 개인화된 프로필에서는 사용할 수 있는 글꼴 목록 상자가 비어 있습니다. 따라서 의 하위 목록을 개인화할 수는 없습니다. **항상 포함** 또는 **임베드 안 함**. PDF Generator PDF에 대한 글꼴을 구성할 수 없습니다. 로그에는 관련 오류 메시지가 표시되지 않습니다. (FORMS-12095)

* AEM Forms 서비스 팩 6.5.18.0에서 사용자는 보안 설정을 만들 수 없으며 오류나 서버 로그가 표시되지 않지만 화면에 팝업 오류 메시지가 표시됩니다. (FORMS-12212)

* AEM Forms 서비스 팩 6.5.18.0의 사용자가 JEE 워크플로우에서 적응형 양식을 제출할 때 적응형 양식의 첨부 파일이 JEE 프로세스로 전송되지 않아 애플리케이션 오류가 발생합니다. (FORMS-12232, FORMS-12228)

* 사용자가 PDF을 PDF/A-2b 또는 PDF/A-3B로 변환할 때 변환하지 않으면 오류가 (FORMS-12790)로 표시됩니다.

  ```
  OCCD contains Order key that does not reference all layers.
  -> Optional content configuration dictionary has no Name entry.
  -> Font not embedded (and text rendering mode not 3).
  obj(65, 0)
  Page: 1
  -> Font not embedded (and text rendering mode not 3).
  obj(67, 0)
  Page: 1
  -> PDF/A entry missing. 
  -> PDF/A entry missing.
  ```

* AEM Forms 6.5.18.0에서 적응형 양식이 게시되면 정책을 포함한 모든 종속 항목이 수정 사항이 없더라도 다시 게시됩니다. (FORMS-10454)

* 사용자가 JBoss® 턴키 설정이 있는 AEM Forms 6.5.19.1에서 구성 관리자를 실행하는 동안 &quot;Microsoft SharePoint&quot;를 선택하면 JBoss® EAR LiveCycle 설치에 실패하고 다음 오류가 표시됩니다. (FORMS-12463)

  ` Caused by: org.jboss.as.server.deployment.DeploymentUnitProcessingException: WFLYEE0031: Unable to process modules in application.xml for EAR ["/C:/AEM/jboss/bin/content/ adobe-livecycle-jboss.ear "], module file adobe-connectorformssharepoint-config-ejb.jar not found.`

* 사용자가 AEM Forms 서비스 팩 6.5.19.0의 양식 데이터 모델을 사용하여 문서 조각을 만들 때 측면 패널에 변수 이름이 정의되지 않은 것처럼 표시되지만, 양식 패널에 끌어 놓거나 클릭할 때 변수 이름이 표시됩니다. (FORMS-13238)


#### [!DNL Forms Designer] {#forms-designer-6520}


* 사용자가 AEM Forms 서비스 팩 6.5.18.0으로 업그레이드할 때 예외 처리가 누락되면 태그 지정된 PDF 옵션이 활성화된 상태로 출력 서비스를 통해 전달되는 XDP가 실패합니다. (LC-3921757)

* 사용자가 AEM Forms Designer를 사용하여 PDF을 생성할 때 액세스 가능성 트리에서 제목 수준에 그래픽 요소(예: 사각형 상자)와 함께 태그가 지정됩니다. (LC-3921687)

* Workbench를 통해 설치된 AEM Forms Designer의에서 버전 정보가 명시적이지 않습니다. `Control Panel/Programs/Programs and Features`. (LC-3921976)

<!--* When a user creates an XDP on AEM Forms Designer, the user is not able to add the custom Caption Tag. (LC-3921246)-->

* 사용자가 AEM Forms Designer에서 XDP를 만들 때 PDF 출력 시 단추 양식 태그가 상위 단락 태그(p-태그)에 중첩되지 않습니다. (LC-3921719)

* 사용자가 AEM Forms Designer에서 XDP를 만들 때, 사용자가 양식 태그를 탐색할 때 PDF 출력 시 배경 개체에도 태그가 지정됩니다. (LC-3921687)

### Foundation {#foundation-6520}

#### 커뮤니티 {#communities-6520}

* 사용자 동기화를 구성한 후 사용자 동기화 진단에 실패했습니다. (NPR-41693)

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### 통합{#integrations-6520}

* AEM 6.5에서 Adobe Search&amp;Promote의 모든 코드와 종속성을 제거합니다. (NPR-40856)

#### 현지화{#localization-6520}

* Aria 레이블 &quot;close&quot;가에 현지화되지 않았습니다. **[!UICONTROL 에셋]** > **[!UICONTROL 파일]**&#x200B;폴더를 선택한 다음 도구 모음에서 를 선택합니다. **[!UICONTROL 속성]** > **[!UICONTROL 권한]** 탭 > 멤버 이름입니다. (NPR-41705)
* 에 대해 잘린 툴팁이 있습니다. **[!UICONTROL 키 저장소 암호]** 로케일 ENG, FRA, KOR, DEU 및 PTB에 대한 SSL 설정 페이지의 필드입니다. (NPR-41367)

#### Platform{#foundation-platform-6520}

* /api 서블릿이 href json에 올바른 스키마를 반환하지 않아 AEM과 Campaign을 통합하는 문제가 발생했습니다. AEM이 X-Forward-Proto 헤더를 받지 못해서 HTTPS 대신 HTTP 스키마로 요청을 응답해야 했기 때문입니다. 따라서 OSGI 구성을 기반으로 구성표 선택을 전환하는 기능이 추가되어야 합니다. (GRANITE-48454)

#### 슬링{#foundation-sling-6520}

* 다음 `org.apache.sling.resourceMerger` 번들 1.4.2는 AEM 6.5, 서비스 팩 17 이상에서 예외를 throw합니다. Sling 리소스 병합 1.4.4는 서비스 팩 20에 포함되어야 합니다. (NPR-41630)

#### 번역{#foundation-translation-6520}

* AEM 6.5 서비스 팩 18을 배포한 후 번역 규칙 편집기의 필터 탭에 문제가 발생했습니다. 컨텍스트를 선택하고 편집 > 저장을 클릭하면 다음에 동일한 컨텍스트를 열 때 큰따옴표를 HTML 문자로 표시합니다. 기본적으로 번역 규칙이 올바르게 저장되지 않았습니다. (NPR-41624)
* 번역된 문자열이 번역 공급자에서 AEM으로 다시 전송되지만 중단된 콘텐츠 조각 번역과 관련된 문제 `/content/projects` 콘텐츠 조각 레벨이며 업데이트되지 않습니다. (NPR-41516)
* 언어 사본을 만들 때 오류 메시지가 표시됩니다. 이 문제는 페이지 속성에서 참조된 콘텐츠 조각이 있는 페이지에서 콘텐츠 조각 모델을 사용하여 발생합니다. (NPR-41441)
* 언어 복사 중에 경험 조각의 링크가 올바른 언어로 조정되지 않습니다. 대신 경험 조각은 기본 로케일을 가리킵니다. (NPR-41343)

#### 사용자 인터페이스{#foundation-ui-6520}

* AEM 6.5, 서비스 팩 18로 업그레이드한 후 콘솔 오류가 발생합니다. 오류가 다음에 있습니다. `coralUI3.js` 이 이벤트는 AEM에서 드롭다운을 선택할 때 발생합니다. 특히 다음과 같은 경우에 발생합니다. `onOverlayToggle` 이벤트. 오류 `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` 이 표시됩니다. (NPR-41467)
* AEM에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL 태깅]** > **[!UICONTROL 만들기]** > **[!UICONTROL 태그 만들기]**, 다음에 라틴어가 아닌 문자 입력 **제목** 필드는 다음을 발생시킵니다. **이름** 하이픈 문자로만 채울 필드( `-` ). (NPR-41623)
* 다음에서 저작권 연도가 올바르지 않음 `About Adobe Experience Manager` 대화 상자. (NPR-41526)
* 번역되지 않은 항목이 있습니다. **[!UICONTROL 프로필 속성]** 사용자 설정을 편집할 때의 문자열입니다. 모든 로케일에서 발생합니다. (NPR-41365)

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## 설치 [!DNL Experience Manager] 6.5.20.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0을 사용하려면 [!DNL Experience Manager] 6.5. 참조 [업그레이드 설명서](/help/sites-deploying/upgrade.md) 자세한 지침은 을 참조하십시오. <!-- UPDATE FOR EACH NEW RELEASE -->
* 서비스 팩은 Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip)에서 다운로드할 수 있습니다.
* MongoDB 및 여러 인스턴스가 포함된 배포에서 다음을 설치합니다. [!DNL Experience Manager] 패키지 관리자를 사용하는 작성자 인스턴스 중 하나에서 6.5.20.0.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe은 를 제거하거나 제거하지 않는 것이 좋습니다. [!DNL Experience Manager] 6.5.20.0 패키지. 따라서 팩을 설치하기 전에 `crx-repository` 혹시라도 돌려주셔야 할 것 같은데요 <!-- UPDATE FOR EACH NEW RELEASE -->
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

를 사용하여 자동으로 설치할 수 있는 두 가지 방법이 있습니다 [!DNL Experience Manager] 6.5.20.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 패키지 배치 위치 `../crx-quickstart/install` 폴더를 사용하십시오. 패키지가 자동으로 설치됩니다.
* 사용 [패키지 관리자의 HTTP API](/help/sites-administering/package-manager.md#package-share). 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

>[!NOTE]
>
>Experience Manager 6.5.20.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 다음을 참조하십시오. [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`) 업데이트된 버전 문자열을 표시합니다 `Adobe Experience Manager (6.5.20.0)` 아래에 [!UICONTROL 설치된 제품]. <!-- UPDATE FOR EACH NEW RELEASE -->

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

에 대한 UberJar [!DNL Experience Manager] 6.5.20.0은 [Maven Central 저장소](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven 프로젝트에서 UberJar를 사용하려면 [uberJar 사용 방법](/help/sites-developing/ht-projects-maven.md) 프로젝트 POM에 다음 종속성을 포함하십시오. <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.20</version>
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


### AEM Forms의 알려진 문제 {#known-issues-aem-forms-6520}

* 대화형 통신에서 미리 채우기 서비스가 실패하고 null 포인터 예외가 발생합니다. (CQDOC-21355)
* 적응형 Forms을 사용하면 ECMAScript 버전 5 이하에 사용자 지정 기능을 사용할 수 있습니다. 사용자 지정 함수에서 &#39;let&#39;, &#39;const&#39; 또는 화살표 함수와 같은 ECMAScript 버전 6 이상을 사용하는 경우 규칙 편집기가 제대로 열리지 않을 수 있습니다.
* 서신 관리 편지를 만들 수 없습니다. 사용자가 문자를 만들 때 &quot;Object Object&quot; 설명과 함께 오류가 나타나고 문자가 만들어지지 않습니다. 레이아웃의 축소판도 편지 만들기 화면에서 로드되지 않습니다. 다음을 설치할 수 있습니다. [최신 AEM 6.5 양식 서비스 팩 20(6.5.20.0)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 을 클릭하여 문제를 해결하십시오. (FORMS-13496)
* 대화형 통신 서비스에서 PDF 문서를 만들지만 사용자의 데이터가 양식 필드에 자동으로 채워지지 않습니다. 미리 채우기 서비스가 예상대로 작동하지 않습니다. 다음을 설치할 수 있습니다. [최신 AEM 6.5 양식 서비스 팩 20(6.5.20.0)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 을 클릭하여 문제를 해결하십시오. (FORMS-13413, FORMS-13493)
* automated forms conversion 서비스의 RnC(Review and Correct) 편집기를 로드하지 못했습니다. 다음을 설치할 수 있습니다. [최신 AEM 6.5 양식 서비스 팩 20(6.5.20.0)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 을 클릭하여 문제를 해결하십시오. (FORMS-13491)
* AEM 6.5 Forms 서비스 팩 18(6.5.18.0) 또는 AEM 6.5 Forms 서비스 팩 19(6.5.19.0)에서 AEM 6.5 Forms 서비스 팩 20(6.5.20.0)으로 업데이트한 후 사용자에게 JSP 컴파일 오류가 발생합니다. 적응형 양식을 열거나 만들 수 없고 페이지 편집기, AEM Forms UI 및 AEM Workflow 편집기와 같은 다른 AEM 인터페이스에서 오류가 발생합니다. 다음을 설치할 수 있습니다. [최신 AEM 6.5 양식 서비스 팩 20(6.5.20.0)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 을 클릭하여 문제를 해결하십시오. (FORMS-13492)

<!--Customers can install the  latest AEM 6.5 Forms Service Pack to resolve the aforementioned issues.  Here are the direct links for the supported operating systems:
* [AEM 6.5 Forms Service Pack 20 for Apple macOS](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/ADOBE-AEMFD-OSX-PKG-6.0.1192.zip)
* [AEM 6.5 Forms Service Pack 20 for Microsoft Windows](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/ADOBE-AEMFD-WIN-PKG-6.0.1192.zip)
* [AEM 6.5 Forms Service Pack 20 for Linux](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/ADOBE-AEMFD-LINUX-PKG-6.0.1192.zip)
-->

<!--Known issues in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of known issues for forms is added to this section post the release.-->

<!--
#### Install the servlet fragment (AEM Service Pack 6.5.14.0 or earlier)

* If you are upgrading to AEM Service Pack 6.5.15.0 or higher, and your AEM instance is operating on Tomcat 8.5.88, it is mandatory that you install the servlet fragment *before* you proceed with the installation of Service Pack 6.5.15.0 or higher.
* It is mandatory that you install the servlet fragment for all application servers except those running on JBoss&reg; EAP 7.4.0.

**To install the servlet fragment:**

1. Download the servlet fragment from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Start the application server. 
1. Wait for the logs to stabilize and check the bundle state.
1. Open Web Console Bundles. The default URL is `http://[Server]:[Port]/system/console/bundles`.
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Select the downloaded fragment 
`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` 
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Wait for the application server to stabilize.
1. Stop the application server.

-->

## OSGi 번들 및 콘텐츠 패키지가 포함됨{#osgi-bundles-and-content-packages-included}

다음 텍스트 문서에는 이에 포함된 OSGi 번들 및 콘텐츠 패키지가 기재되어 있습니다. [!DNL Experience Manager] 6.5 서비스 팩 릴리스:

* [Experience Manager 6.5.20.0에 포함된 OSGi 번들 목록](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.20.0에 포함된 컨텐츠 패키지 목록](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 제한된 웹 사이트{#restricted-sites}

이러한 웹 사이트는 고객만 사용할 수 있습니다. 고객이고 액세스 권한이 필요한 경우 Adobe 계정 관리자에게 문의하십시오.

* [licensing.adobe.com에서 제품 다운로드](https://licensing.adobe.com/)
* [Adobe 고객 지원 문의](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 제품 페이지](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Adobe 우선 순위 제품 업데이트 구독](https://www.adobe.com/kr/subscription/priority-product-update.html)
