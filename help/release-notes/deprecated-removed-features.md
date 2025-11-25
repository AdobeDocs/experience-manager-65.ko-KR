---
title: Adobe Experience Manager 6.5 릴리스에서 더 이상 사용되지 않거나 제거된 기능.
description: Adobe Experience Manager 6.5에서 더 이상 사용되지 않으며 제거된 기능에 관련된 릴리스 정보입니다.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 32%

---

# 더 이상 사용되지 않는 기능과 제거된 기능 {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe는 항상 이전 기능과의 호환성을 신중하게 고려하면서 전반적인 고객 가치를 향상하도록 오랜 시간에 걸쳐 오래된 기능을 새롭게 만들거나 더 현대적인 대안으로 교체하기 위해 제품 기능을 지속해서 평가합니다.

Adobe Experience Manager(AEM) 기능의 제거 또는 대체 예정 사실을 알리기 위해 다음 규칙이 적용됩니다.

1. 사용 중지 공지가 먼저 표시됩니다. 사용 중지 중에도 기능이 계속 지원되지만 더 이상 개선되지는 않습니다.
1. 더 이상 사용되지 않는 기능은 이른 시일 내에 후속 주 릴리스에서 제거됩니다. 제거에 대한 실제 목표 날짜는 나중에 발표될 예정입니다.

이 프로세스에서 고객에게 하나 이상의 릴리스 주기를 제공하여, 실제 제거 전에 더 이상 사용되지 않는 기능의 새 버전이나 후속 버전에 대한 구현을 채택할 수 있도록 합니다.

## 더 이상 사용되지 않는 기능 {#deprecated-features}

이 섹션에는 AEM 6.5에서 더 이상 사용되지 않는다고 표시된 기능이 나열됩니다. 일반적으로 향후 릴리스에서 제거될 예정인 기능은 먼저 대체 기능을 제공하며 사용 중단되는 것으로 설정됩니다.

현재 배포에서 해당 기능을 사용 중인지 검토하고 이들 구현을 변경하여 제공되는 대체 기능을 사용하도록 계획을 세우는 것이 좋습니다.

| 영역 | 기능 | 대체 | 버전 (SP) |
|---|---|---|---|
| Sites | [SPA 편집기](/help/sites-developing/spa-editor-deprecation.md) | Headless 사용 사례의 경우 시각적 편집을 위해 [범용 편집기](/help/sites-developing/universal-editor/introduction.md)를 활용하거나 양식 기반 편집을 위해 [콘텐츠 조각 편집기](/help/sites-developing/universal-editor/introduction.md)를 활용하십시오. | 6.5.23 |
| Sites | **Adobe AEM 관리 폴링 구성** 서비스: `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | **Adobe AEM Analytics 보고서 Sling 가져오기** 서비스. Adobe Analytics 연결 및 프레임워크 만들기 - [가져오기 간격 구성](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval)을 참조하십시오. | 6.5.19.0 |
| Screens | Adobe Experience Manager(AEM)의 ActiveMQ. ActiveMQ는 두 AEM 게시 인스턴스 간의 통신에 사용되었습니다. | Adobe 이제 고객은 로드 밸런서를 사용하는 것이 좋습니다. | 6.5.18.0 |
| **소셜 미디어 상태**&#x200B;에 대한 경험 조각 속성. | |  | 6.5.11.0 |
| [!DNL Sites] | 콘텐츠 조각 템플릿(단순 콘텐츠 조각 생성) | 현재는 [모델 기반 구조 콘텐츠 조각](/help/assets/content-fragments/content-fragments-models.md)입니다. | 6.5.11.0 |
| Creative Cloud 통합 | Creative Cloud 폴더 공유에 대한 AEM은 AEM 6.2에 도입되었습니다. 창의적 사용자에게 AEM의 자산에 대한 액세스 권한을 부여하여 [!DNL Creative Cloud] 응용 프로그램에서 자산을 열고 새 파일을 업로드하거나 변경 내용을 AEM에 저장할 수 있도록 합니다. Creative Cloud 애플리케이션에 출시된 새로운 기능인 Adobe Asset Link는 더 나은 사용자 경험을 제공하고 Photoshop, InDesign 및 Illustrator 내부에서 직접 AEM의 자산에 액세스할 수 있는 강력한 권한을 제공합니다. Adobe은 Creative Cloud 폴더 공유 통합에 대한 AEM을 더 이상 개선할 계획이 없습니다. 이 기능은 AEM에 포함되어 있지만 고객은 대체 솔루션을 사용하는 것이 좋습니다. | 고객은 Adobe Asset Link 또는 Creative Cloud 데스크탑 앱을 비롯한 새로운 AEM 통합 기능으로 전환하는 것이 좋습니다. |  |
| 자산 | 게시 인스턴스에 대해 기본적으로 `AssetDownloadServlet`이(가) 비활성화되어 있습니다. 자세한 내용은 [AEM 보안 검사 목록](/help/sites-administering/security-checklist.md)을 참조하세요. | [AEM 보안 검사 목록](/help/sites-administering/security-checklist.md)에 설명된 구성입니다. |  |
| 통합 | **[!UICONTROL Experience Manager Cloud Services 옵트인]** 화면은 [!DNL Experience Manager] 6.5에서 [!DNL Adobe Target] 및 [!DNL Experience Manager] 통합이 업데이트되어 더 이상 사용되지 않습니다. 통합은 Adobe Target Standard API를 지원합니다. API는 Adobe IMS 및 [!DNL Adobe I/O Runtime]을(를) 통해 인증을 사용합니다. 분석 및 개인화를 위해 [!DNL Experience Manager] 페이지를 계측하는 Adobe Launch의 역할이 점차 커지고 있음을 지원합니다. 옵트인 마법사는 기능상 관련이 없습니다. | 해당 [!DNL Adobe I/O Runtime] 클라우드 서비스를 통해 시스템 연결, Adobe IMS 인증 및 [!DNL Experience Manager] 통합을 구성하십시오. | 6.5.7.0 |
| 커넥터 | Microsoft® SharePoint 2010 및 Microsoft® SharePoint 2013용 Adobe JCR 커넥터는 [!DNL Experience Manager] 6.5에서 더 이상 사용되지 않습니다. | 해당 사항 없음 |  |
| Dynamic Tag Manager (DTM) | DTM과의 통합은 더 이상 사용되지 않습니다. | Adobe Experience Platform Launch을 태그 관리자로 사용하도록 전환합니다. |   |
| Adobe Target | AEM 6.5에서 [!DNL Adobe I/O] 기반 Adobe Target AEM Standard API(Rest API)를 사용하여 Adobe Target 서비스에 연결할 수 있는 기능을 추가하면 Target Classic API(XML) 방식이 더 이상 사용되지 않습니다. | [새 API를 사용](/help/sites-administering/target.md)하도록 통합을 다시 구성하십시오. |  |
| Adobe Target | AEM에서 Adobe Target과 `mbox.js` 기반 통합을 사용하는 방법은 더 이상 사용되지 않습니다. | `at.js` 1.x을(를) 사용하도록 전환합니다. |  |
| 상거래 | [CIF REST](https://github.com/adobe/commerce-cif-api)은(는) AEM과 상거래 엔진 간의 통합을 가능하게 하기 위해 마이크로 서비스 세트로 2018년에 제공되었습니다. Adobe이 2018년 중반에 Adobe Commerce(이전 Magento)를 인수한 후 Adobe은 두 가지 이유로 접근 방식을 변경하기로 결정했습니다. Commerce에는 고유한 Commerce API(REST 및 GraphQL) 세트가 있으며 두 개의 API 세트를 유지 관리하는 것은 좋지 않습니다. 시장 동향은 데이터를 쿼리하는 보다 효율적인 방법이기 때문에 고객이 GraphQL으로 이동하고 있음을 나타냈습니다. 2019년 Adobe은 Commerce의 GraphQL API를 소스로 사용하여 새로운 Commerce integration framework을 출시했습니다. Adobe은 CIF REST에 더 이상 투자할 계획이 없습니다. 고객은 교체 솔루션을 사용하는 것이 좋습니다. | AEM-Commerce 통합의 경우 [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype) 및 [AEM CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components)&#x200B;(으)로 전환하십시오. AEM 및 Adobe Commerce 통합 [Commerce integration framework 사용](/help/commerce/cif/integrating/magento.md)을 참조하십시오. 새로운 접근 방식과 타사(Commerce 제외) 통합 지원은 Adobe 로드맵에 있습니다. |  |
| 구성 요소(AEM Sites) | Adobe은 `/libs/foundation/components`에 저장된 대부분의 기초 구성 요소를 추가로 개선할 계획이 없습니다. 구성 요소 폴더에서 `cq:deprecated` 및 `cq:deprecatedReason` 속성을 찾습니다. AEM 6.5에는 기초 구성 요소가 포함되어 있으며 이전 릴리스에서 업그레이드하는 고객은 있는 그대로 사용할 수 있습니다. 또한 기초 구성 요소는 더 이상 사용되지 않는 경우에도 지원됩니다. | Adobe에서는 향후 프로젝트를 위해 핵심 구성 요소를 사용하는 것이 좋습니다. 기존 사이트는 그대로 유지되거나 [AEM Modernize Tools 제품군](https://github.com/adobe/aem-modernize-tools)을 사용하여 코어 구성 요소를 사용하도록 사이트를 리팩터링할 수 있습니다. |  |
| 구성 요소(AEM Sites) | 디자인 가져오기 구성 요소 `/libs/wcm/designimporter/components`이(가) 6.5부터 더 이상 사용되지 않는 것으로 표시되었습니다. Adobe은 디자인 임포터의 해당 구현을 더 이상 개선할 계획이 없습니다. | Adobe은 향후 릴리스에서 사용 사례에 대한 대체 구현을 제공할 계획입니다. |  |
| 기초 | Granite 오프로딩 프레임워크. Adobe은 자산 처리를 외부화하기 위해 CQ 5.6.1에 도입된 오프로딩 프레임워크를 추가로 개선할 계획이 없습니다. | Adobe은 차세대 클라우드 기반 오프로딩 프레임워크에서 작업 중입니다. |  |
| 개발자 | `Hobbes.js`. Adobe은 `hobbes.js` 사용자 인터페이스 테스트 프레임워크를 추가로 개선할 계획이 없습니다. | 고객이 Selenium 자동화를 사용하는 것이 좋습니다. |  |
| 개발자 | jQuery UI 클라이언트 라이브러리 Adobe은 향후 배포(빠른 시작)의 일부로 제공되는 jQuery UI 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다. | 코드에 여전히 jQuery UI가 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | jQuery Animation 클라이언트 라이브러리(`granite.jquery.animation`). Adobe은 향후 배포(빠른 시작)의 일부로 제공되는 jQuery Animation 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다. | 코드에 여전히 jQuery Animation이 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | Handlebars 클라이언트 라이브러리. Adobe은 배포(빠른 시작)의 일부로 제공되는 Handlebar 클라이언트 라이브러리를 더 이상 유지 관리하고 업데이트할 계획이 없습니다. | Adobe에서는 코드에 여전히 `Handlebars`이(가) 필요한 고객에게 해당 코드를 프로젝트 코드 베이스에 추가하도록 권장합니다. |  |
| 개발자 | Lawnchair 클라이언트 라이브러리 Adobe은 배포(빠른 시작)의 일부로 제공되는 Lawnchair 클라이언트 라이브러리를 더 이상 유지 관리하고 업데이트할 계획이 없습니다. | 코드에 여전히 Lawnchair가 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | `Granite.Sling.js` 클라이언트 라이브러리입니다. Adobe은 배포(빠른 시작)의 일부로 제공되는 Granite.Sling.js 클라이언트 라이브러리를 더 강화하지 않을 계획입니다. | 코드를 리팩토링하는 라이브러리 기능에 의존하고 있는 고객들은 더 이상 해당 기능을 사용할 수 없습니다. |  |
| 개발자 | YUI를 사용하여 JavaScript 클라이언트 라이브러리를 압축/최소화. Adobe은 YUI 라이브러리를 더 이상 업데이트할 계획이 없습니다. AEM 6.4가 출시되기 이전까지, YUI는 기본적으로 GCC(Google Closure Compiler)로 전환할 수 있는 옵션과 함께 JavaScript를 축소할 수 있었습니다. AEM 6.5부터는 GCC가 기본값입니다. | 고객은 이러한 구현에 따라 GCC로 전환하기 위해 AEM 6.5로 업그레이드하는 것이 좋습니다. |  |
| 개발자 | CRXDE Lite의 클래식 UI 대화 상자 편집기. Adobe은 배포(빠른 시작)의 일부로 제공되는 클래식 UI 대화 상자 편집기를 더 이상 향상시킬 계획이 없습니다 | 대체할 수 없습니다. |  |
| 양식 | AEM Mobile과 AEM Forms 통합은 더 이상 사용되지 않습니다. | 대체할 수 없습니다. |  |
| 개발자 | CRXDE Lite의 클래식 UI 대화 상자 편집기. Adobe은 배포(빠른 시작)의 일부로 제공되는 클래식 UI 대화 상자 편집기를 더 이상 향상시킬 계획이 없습니다 | 대체할 수 없습니다. |  |
| 개발자 | Lodash/underscore 클라이언트 라이브러리입니다. Adobe은 배포(빠른 시작)의 일부로 제공되는 Lodash/underscore 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다. | Adobe에서는 코드에 여전히 Lodash/밑줄이 필요한 고객에게 이를 프로젝트 코드 베이스에 추가하도록 권장합니다. |  |

## 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5에서 제거된 기능이 나와 있습니다. 이전 릴리스에는 이러한 기능이 더 이상 사용되지 않는 것으로 표시되었습니다.

| 영역 | 기능 | 대체 | 버전 (SP) |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic이 제거되었습니다. | [AEM CIF](/help/commerce/cif/migration.md)로 마이그레이션해야 합니다. 여전히 CIF Classic이 필요한 경우 호환성 패키지를 만들었습니다. [Adobe 고객 지원 센터에 문의](https://experienceleague.adobe.com/ko?support-solution=General#support)하십시오. | 6.5.22.0 |
| [!DNL Experience Cloud]과(와) 통합 | [!DNL Experience Cloud]을(를) 통해 구성을 사용하여 자산을 [!DNL Adobe I/O]과(와) 동기화할 수 있습니다. [!DNL Adobe Experience Cloud]은(는) 이전에 [!DNL Adobe Experience Cloud]&#x200B;(으)로 불렸습니다. | 질문이 있는 경우 [Adobe 고객 지원 센터에 문의](https://experienceleague.adobe.com/ko?support-solution=General#support)하십시오. |  |
| Analytics Activity Map | AEM 내에 포함된 Activity Map 버전입니다. | Adobe Analytics API의 보안 변경 사항으로 인해, AEM 내에 포함된 Activity Map 버전을 더는 사용할 수 없습니다. Adobe Analytics에서 제공한 [ActivityMap 플러그인을 사용하십시오](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=ko). |  |
| 통합 | ExactTarget 통합이 기본 배포(빠른 시작)에서 제거되어 더 이상 사용할 수 없습니다. | 교체 없음. |  |
| 통합 | Salesforce Force API 통합이 기본 배포(빠른 시작)에서 제거되었으며 이제 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 설치할 추가 패키지입니다. | 기능은 계속 사용할 수 있습니다. |  |
| 양식 | Adobe Central 제품이 더 이상 지원되지 않아 Adobe Central 마이그레이션 Bridge 서비스에 대한 지원이 제거되었습니다. | 교체 없음. |  |
| 양식 | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 교체 없음. |  |
| 양식 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 교체 없음 |  |
| 양식 | LiveCycle ES4 SP1에서 JEE의 AEM 6.5 Forms로 한 번에 업그레이드할 수 없음 | AEM Forms 업그레이드 설명서의 [사용 가능한 업그레이드 경로](../forms/using/upgrade.md)를 참조하십시오. |  |
| 양식 | JEE의 AEM Forms에서 UPD 기반 클러스터링 지원을 제거했습니다. | JEE의 AEM Forms에서는 TCP 기반 클러스터링만 사용할 수 있습니다. UDP 멀티캐스트 서버를 이전 버전에서 JEE의 AEM 5.5 Forms으로 업그레이드하는 경우 수동 구성을 수행하여 TCP 기반 Gemfire 클러스터로 전환합니다. 자세한 지침은 [JEE의 AEM 6.5 양식으로 업그레이드](../forms/using/upgrade-forms-jee.md)를 참조하십시오. |  |
| 개발자 | Firebug Lite가 기본 배포(빠른 시작)에서 제거되었습니다. | 브라우저 내장 개발자 콘솔 사용 |  |
| 개발자 | HTML 클라이언트 라이브러리 관리자에서 `customJavaScriptPath` 지원을 제거합니다. | 교체 없음 |  |
| [!DNL Assets] | 자산 오프로딩 기능이 [!DNL Adobe Experience Manager] 6.5에서 제거되었습니다. | 대체할 수 없습니다. |  |
| 캐시 | `system/console/slingjsp`이(가) 제거되어 AEM 6.5에서 더 이상 사용할 수 없습니다. | 클래스 및 Slightly 캐시는 Apache Sling Commons FileSystem ClassLoader 번들 아래에 저장됩니다. AEM 웹 콘솔에서 번들 번호를 확인하고 파일 시스템(`crx-quickstart/launchpad/felix/bundle<ID>`)에서 직접 캐시 폴더를 제거할 수 있습니다. |  |
| Screens | Activemq 번들 지원 및 관련 구성이 제거되었습니다. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
