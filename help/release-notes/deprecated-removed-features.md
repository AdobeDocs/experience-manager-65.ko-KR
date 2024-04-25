---
title: Adobe Experience Manager 6.5 릴리스에서 더 이상 사용되지 않는 기능 및 제거된 기능입니다.
description: Adobe Experience Manager 6.5의 더 이상 사용되지 않는 및 제거된 기능에 관한 릴리스 노트입니다.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 29%

---

# 이제 사용되지 않는 기능과 제거된 기능 {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe는 항상 이전 기능과의 호환성을 신중하게 고려하면서 전반적인 고객 가치를 향상하도록 오랜 시간에 걸쳐 오래된 기능을 새롭게 만들거나 더 현대적인 대안으로 교체하기 위해 제품 기능을 지속해서 평가합니다.

AEM(Adobe Experience Manager) 기능의 임박한 제거 또는 교체를 알리려면 다음 규칙이 적용됩니다.

1. 사용 중지 공지가 먼저 표시됩니다. 사용 중지 중에도 기능은 계속 사용할 수 있지만 더 이상 향상되지는 않습니다.
1. 더 이상 사용되지 않는 기능의 제거는 이르면 다음 주요 릴리스에서 실행됩니다. 실제 제거 타겟 날짜는 추후 공지될 예정입니다.

이 프로세스에서 고객에게 하나 이상의 릴리스 주기를 제공하여, 실제 제거 전에 더 이상 사용되지 않는 기능의 새 버전이나 후속 버전에 대한 구현을 채택할 수 있도록 합니다.

## 이제 사용되지 않는 기능 {#deprecated-features}

이 섹션에는 AEM 6.5에서 더 이상 사용되지 않는 것으로 표시된 기능이 나열되어 있습니다. 일반적으로 향후 릴리스에서 제거될 예정인 기능은 먼저 사용 중단으로 설정되고 대체 기능이 제공됩니다.

현재 배포에서 해당 기능을 사용 중인지 검토하고 이들 구현을 변경하여 제공되는 대체 기능을 사용하도록 계획을 세우는 것이 좋습니다.

| 영역 | 기능 | 대체 | 버전(SP) |
|---|---|---|---|
|   |   |   |   |
| Sites | **Adobe Systems AEM 관리 폴링 구성** 서비스는 다음과 같습니다.`com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | **Adobe Systems AEM Analytics Report Sling Importer** 서비스입니다. Adobe Analytics에 연결 및 프레임워크 만들기 - [가져오기 간격 구성을 참조하십시오.](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | Adobe Experience Manager의 ActiveMQ(AEM). ActiveMQ는 두 AEM Publish 인스턴스 간의 통신에 사용되었습니다. | Adobe Systems 고객은 이제 로드 밸런서를 사용할 것을 권장합니다. | 6.5.18.0 |
| **소셜 미디어 상태**&#x200B;에 대한 경험 조각 속성. |   | 6.5.11.0 |
| [!DNL Sites] | 콘텐츠 조각 템플릿(단순 콘텐츠 조각 생성) | 현재는 [모델 기반 구조 콘텐츠 조각](/help/assets/content-fragments/content-fragments-models.md)입니다. | 6.5.11.0 |
| Creative Cloud 통합 | Creative Cloud 폴더 공유에 대한 AEM은 AEM 6.2에서 도입되었습니다. 크리에이티브 사용자에게 AEM의 자산에 대한 액세스 권한을 부여하여 애플리케이션에서 [!DNL Creative Cloud] 자산을 열고 새 파일을 업로드하거나 변경 사항을 AEM에 저장할 수 있는 방법을 제공합니다. Creative Cloud 애플리케이션인 Adobe 에셋 링크에 출시된 새로운 기능은 Photoshop, InDesign 및 Illustrator 내에서 직접 AEM의 에셋에 액세스할 수 있도록 함으로써 사용자 경험을 향상시키고 에셋에 대한 강력한 액세스를 제공합니다. Adobe은 AEM의 Creative Cloud 폴더 공유 통합을 추가로 개선할 계획이 없습니다. 이 기능은 AEM에 포함되어 있지만 고객은 대체 솔루션을 사용하는 것이 좋습니다. | 고객은 Adobe Asset Link 또는 AEM 데스크탑 앱을 비롯한 새로운 Creative Cloud 통합 기능으로 전환하는 것이 좋습니다. |  |
| 자산 | `AssetDownloadServlet` 는 게시 인스턴스에 대해 기본적으로 비활성화되어 있습니다. 자세한 내용은 AEM 보안 검사 목록을](/help/sites-administering/security-checklist.md) 참조하십시오[. | AEM 보안 체크](/help/sites-administering/security-checklist.md)리스트에 설명된 구성입니다[. |  |
| 통합 | 화면 **[!UICONTROL Experience Manager Cloud Services 옵트인은]** 및 [!DNL Adobe Target] 통합이 6.5에서 [!DNL Experience Manager] 업데이트되었으므로 더 이상 사용되지 않습니다[!DNL Experience Manager]. 통합은 Adobe Target Standard API를 지원합니다. API는 Adobe Systems IMS 및 [!DNL Adobe I/O Runtime]. 분석 및 개인화용 계측 [!DNL Experience Manager] 페이지에 대한 Adobe Systems Launch의 증가하는 역할 지원하며 옵트인 마법사는 기능적으로 관련이 없습니다. | 각 [!DNL Experience Manager] 클라우드 서비스를 통해 시스템 연결, Adobe Systems IMS 인증 및 [!DNL Adobe I/O Runtime] 통합을 구성합니다. | 6.5.7.0 |
| 커넥터 | Microsoft® SharePoint 2010 및 Microsoft® SharePoint 2013용 Adobe JCR 커넥터는 더 이상 사용되지 않습니다. [!DNL Experience Manager] 6.5. | 해당 사항 없음 |  |
| Dynamic Tag Manager (DTM) | DTM과의 통합은 더 이상 사용되지 않습니다. | Adobe Experience Platform Launch을 태그 관리자로 사용하도록 전환합니다. |   |
| Adobe Target | 를 사용하여 AEM에서 Adobe Target 서비스에 연결할 수 있는 기능 추가 [!DNL Adobe I/O] AEM 6.5의 Adobe Target Standard API(Rest API) 기반의 Target Classic API(XML) 방법은 더 이상 사용되지 않습니다. | 통합을 다음으로 재구성 [새 API 사용](/help/sites-administering/target.md). |  |
| Adobe Target | `mbox.js` AEM에서 Adobe Target와의 기반 통합 사용은 더 이상 사용되지 않습니다. | 1.x를 사용하도록 `at.js` 전환합니다. |  |
| 상거래 | [CIF REST](https://github.com/adobe/commerce-cif-api) 는 2018년에 AEM 및 상거래 엔진 간의 통합을 지원하는 마이크로서비스 세트로 제공되었습니다. Adobe Systems가 2018년 중반에 Adobe Systems Commerce(구 Magento)를 인수한 후 Adobe Systems는 두 가지 이유로 접근 방식을 변경하기로 결정했습니다. 상거래에는 자체 상거래 API 세트(REST 및 GraphQL)가 있으며 두 개의 API 세트를 유지 관리하는 것은 좋지 않습니다. 시장 추세에 따르면 고객은 데이터를 쿼리하는 보다 효율적인 방법인 GraphQL로 이동하고 있습니다. 2019년 Adobe Systems 는 Commerce의 GraphQL API를 정보 소스로 사용하는 새로운 Commerce Integration Framework를 출시했습니다. Adobe Systems 는 CIF REST에 대한 추가 투자를 계획하고 있지 않습니다. 고객은 교체 솔루션을 사용하는 것이 좋습니다. | AEM-Commerce 통합의 경우 AEM CIF 원형](https://github.com/adobe/aem-cif-project-archetype) 및 AEM CIF 코어 구성 요소](https://github.com/adobe/aem-core-cif-components)로 전환하십시오[[. Commerce Integration Framework](/help/commerce/cif/integrating/magento.md)를 사용한 AEM 및 Adobe Systems Commerce 통합을 [참조하십시오. 새로운 접근 방식을 통한 서드파티(상거래 이외) 통합에 대한 지원은 Adobe Systems 로드맵에 있습니다. |  |
| 구성 요소(AEM Sites) | Adobe Systems 는 에 저장된 `/libs/foundation/components`대부분의 기초 구성 요소를 추가로 개선할 계획이 없습니다. 구성 요소 폴더의 `cq:deprecated` 및 `cq:deprecatedReason` 속성(Look)을 찾습니다. AEM 6.5에는 기초 구성 요소가 포함되어 있으며 이전 릴리스에서 업그레이드하는 고객은 있는 그대로 사용할 수 있습니다. 또한, 기초 구성 요소는 더 이상 사용되지 않지만 균일 지원됩니다. | Adobe Systems 향후 프로젝트에서는 코어 구성 요소를 사용할 것을 권장합니다. 기존 사이트는 그대로 유지되거나 [AEM Modernize Tools 제품군](https://github.com/adobe/aem-modernize-tools)을 사용하여 코어 구성 요소를 사용하도록 사이트를 리팩터링할 수 있습니다. |  |
| 구성 요소(AEM Sites) | 디자인 Importer 구성 요소 `/libs/wcm/designimporter/components` 이(가) 6.5부터 더 이상 사용되지 않는 것으로 표시되었습니다. Adobe은 디자인 임포터의 해당 구현을 더 이상 개선할 계획이 없습니다. | Adobe Systems 는 향후 릴리스에서 사용 사례의 대체 구현을 제공할 계획입니다. |  |
| Foundation | Granite 오프로드 프레임워크. Adobe Systems 는 자산 처리를 외부화하기 위해 CQ 5.6.1에 도입된 오프로딩 프레임워크를 더 이상 개선할 계획이 없습니다. | Adobe Systems는 차세대 클라우드 기본 오프로드 프레임워크에서 작동합니다. |  |
| 개발자 | `Hobbes.js`. Adobe Systems는 향후 사용자 인터페이스 테스트 프레임워크를 `hobbes.js` 개선할 계획이 없습니다. | 고객이 Selenium 자동화를 사용하는 것이 좋습니다. |  |
| 개발자 | jQuery UI 클라이언트 라이브러리. Adobe Systems는 배포의 일부로 제공되는 jQuery UI 클라이언트 라이브러리를 추가로 유지 관리 및 업데이트할 계획이 없습니다(빠른 시작). | 코드에 여전히 jQuery UI가 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | jQuery 애니메이션 클라이언트 라이브러리(`granite.jquery.animation`). Adobe Systems는 배포의 일부로 제공되는 jQuery 애니메이션 클라이언트 라이브러리를 추가로 유지 관리 및 업데이트할 계획이 없습니다(빠른 시작). | 코드에 여전히 jQuery Animation이 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | Handlebars 클라이언트 라이브러리. Adobe은 배포(빠른 시작)의 일부로 제공되는 Handlebar 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다. | Adobe은 여전히 다음을 필요로 하는 고객을 권장합니다. `Handlebars` 코드: 를 자신의 프로젝트 코드 베이스에 추가합니다. |  |
| 개발자 | Lawnchair 클라이언트 라이브러리 Adobe Systems 배포의 일부로 제공되는 Lawnchair 클라이언트 라이브러리를 더 이상 유지 관리 및 업데이트할 계획이 없습니다(Quickstart). | 코드에 여전히 Lawnchair가 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | `Granite.Sling.js` 클라이언트 라이브러리. Adobe Systems 배포의 일부로 제공되는 Granite.Sling.js 클라이언트 라이브러리를 더 이상 향상시킬 계획이 없습니다(빠른 시작). | 코드를 리팩토링하는 라이브러리 기능에 의존하고 있는 고객들은 더 이상 해당 기능을 사용할 수 없습니다. |  |
| 개발자 | YUI를 사용하여 JavaScript 클라이언트 라이브러리를 압축/축소할 수 있습니다. Adobe Systems 는 향후 YUI 라이브러리를 업데이트할 계획이 없습니다. AEM 6.4가 출시되기 이전까지, YUI는 기본적으로 GCC(Google Closure Compiler)로 전환할 수 있는 옵션과 함께 JavaScript를 축소할 수 있었습니다. AEM 6.5부터는 GCC가 기본값입니다. | 고객은 이러한 구현에 따라 GCC로 전환하기 위해 AEM 6.5로 업그레이드하는 것이 좋습니다. |  |
| 개발자 | CRXDE Lite의 클래식 UI 대화 상자 편집기입니다. Adobe Systems는 배포의 일부로 제공되는 클래식 UI 대화 상자 편집기를 더 이상 향상시킬 계획이 없습니다(빠른 시작) | 교체할 수 없습니다. |  |
| Forms | AEM Mobile과 AEM Forms 통합은 더 이상 사용되지 않습니다. | 대체할 수 없습니다. |
| 개발자 | CRXDE Lite의 클래식 UI 대화 상자 편집기. Adobe Systems는 배포의 일부로 제공되는 클래식 UI 대화 상자 편집기를 더 이상 향상시킬 계획이 없습니다(빠른 시작) | 대체할 수 없습니다. |  |
| 개발자 | Lodash/underscore 클라이언트 라이브러리입니다. Adobe은 배포(빠른 시작)의 일부로 제공되는 Lodash/underscore 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다. | Adobe은 코드에 여전히 Lodash/밑줄이 필요한 고객을 프로젝트 코드 베이스에 추가하도록 권장합니다. |  |

## 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5에서 제거된 기능이 나와 있습니다. 이전 릴리스에는 이러한 기능이 더 이상 사용되지 않는 것으로 표시되었습니다.

| 영역 | 기능 | 대체 | 버전(SP) |
|--- |--- |--- |--- |
| 통합 대상: [!DNL Experience Cloud] | 를 통한 [!DNL Adobe I/O]구성을 사용하여 자산을 [!DNL Experience Cloud] 동기화할 수 있습니다. [!DNL Adobe Experience Cloud] 이전에는 [!DNL Adobe Experience Cloud]. | 질문이 [있는 경우 Adobe Systems 고객 지원](https://experienceleague.adobe.com/?support-solution=General#support) 센터에 문의하십시오. |  |
| Analytics Activity Map | AEM 내에 포함된 Activity Map 버전입니다. | Adobe Analytics API의 보안 변경 사항으로 인해, AEM 내에 포함된 Activity Map 버전을 더는 사용할 수 없습니다. [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)에서 제공하는 ActivityMap 플러그인을 사용합니다. |  |
| 통합 | ExactTarget 통합이 기본 배포(빠른 시작)에서 제거되어 더 이상 사용할 수 없습니다. | 교체 없음. |  |
| 통합 | Salesforce Force API 통합은 기본 배포(빠른 시작)에서 제거되었으며 이제 Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 [설치할 수 있는 추가 패키지입니다. | 이 기능은 계속 사용할 수 있습니다. |
| 양식 | Adobe Systems Central 제품이 더 이상 지원되지 않으므로 Adobe Systems Central Migration Bridge 서비스에 대한 지원이 제거되었습니다. | 대체품이 없습니다. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 대체품이 없습니다. |  |
| 양식 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 교체 없음 |  |
| 양식 | LiveCycle ES4 SP1에서 JEE의 AEM 6.5 Forms로 한 번에 업그레이드할 수 없음 | AEM Forms 업그레이드 설명서의 [사용 가능한 업그레이드 경로](../forms/using/upgrade.md)를 참조하십시오. |  |
| 양식 | JEE의 AEM Forms에서 UPD 기반 클러스터링 지원을 제거했습니다. | JEE의 AEM Forms에서는 TCP 기반 클러스터링만 사용할 수 있습니다. UDP 멀티캐스트 서버를 이전 버전에서 JEE의 AEM 5.5 Forms로 업그레이드하는 경우 수동 구성을 수행하여 TCP 기반 gemfire 클러스터링으로 전환하십시오. 자세한 지침은 [JEE의 AEM 6.5 양식으로 업그레이드](../forms/using/upgrade-forms-jee.md)를 참조하십시오. |  |
| 개발자 | Firebug Lite가 기본 배포(빠른 시작)에서 제거되었습니다. | 브라우저 내장 개발자 콘솔 사용 |
| 개발자 | HTML 클라이언트 라이브러리 관리자에서 `customJavaScriptPath` 지원을 제거합니다. | 교체 없음 |  |
| [!DNL Assets] | 자산 오프로딩 기능은 6.5에서 [!DNL Adobe Experience Manager] 제거되었습니다. | 교체할 수 없습니다. |  |
| 캐시 | `system/console/slingjsp` 가 제거되어 AEM 6.5에서 더 이상 사용할 수 없습니다. | 클래스 및 Slightly 캐시는 Apache Sling Commons FileSystem ClassLoader 번들 아래에 저장됩니다. AEM 웹 콘솔에서 번들 번호를 확인하고 파일 시스템(`crx-quickstart/launchpad/felix/bundle<ID>`)에서 직접 캐시 폴더를 제거할 수 있습니다. |  |
| Screens | activemq 번들 지원 및 관련 구성이 제거되었습니다. |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
