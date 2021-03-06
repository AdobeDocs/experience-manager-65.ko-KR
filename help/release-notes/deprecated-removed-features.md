---
title: Adobe Experience Manager 6.5 릴리스에서 사용 중단되거나 제거된 기능.
description: Adobe Experience Manager 6.5의 더 이상 사용되지 않는 및 제거된 기능에 관한 릴리스 노트입니다.
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 68%

---

# 이제 사용되지 않는 기능과 제거된 기능 {#deprecated-and-removed-features}

Adobe는 항상 이전 기능과의 호환성을 신중하게 고려하면서 전반적인 고객 가치를 향상하도록 오랜 시간에 걸쳐 오래된 기능을 새롭게 만들거나 더 현대적인 대안으로 교체하기 위해 제품 기능을 지속해서 평가합니다.

AEM 기능을 제거하거나 교체하기 위해 다음 규칙이 적용됩니다.

1. 사용 중지 공지가 먼저 표시됩니다. 사용 중지 중에도 기능이 계속 지원되지만 더 이상 개선되지는 않습니다.
1. 사용 중단되는 기능은 빠른 시일 내에 다음 주요 릴리스에서 제거됩니다. 실제 제거 대상일이 공지됩니다.

이 프로세스에서 고객에게 하나 이상의 릴리스 주기를 제공하여, 실제 제거 전에 더 이상 사용되지 않는 기능의 새 버전이나 후속 버전에 대한 구현을 채택할 수 있도록 합니다.

## 이제 사용되지 않는 기능 {#deprecated-features}

이 섹션에서는 AEM 6.5에서 더 이상 사용되지 않는 것으로 표시된 기능을 제시합니다. 일반적으로 이후 릴리스에서 제거될 예정인 기능은 먼저 사용 중지로 설정되고 대체 기능과 함께 제공됩니다.

고객은 현재 배포에서 기능을 사용할지 검토하고 대체 기능을 사용할 수 있도록 구현 변경을 계획하는 것이 좋습니다.

| 영역 | 기능 | 대체 | 버전 (SP) |
|---|---|---|---|
| [!DNL Sites] | **소셜 미디어 상태**&#x200B;에 대한 경험 조각 속성. |  | 6.5.11.0 |
| [!DNL Sites] | 단순 컨텐츠 조각을 만드는 컨텐츠 조각 템플릿. | 현재는 [모델 기반 구조 콘텐츠 조각](/help/assets/content-fragments/content-fragments-models.md)입니다. | 6.5.11.0 |
| Creative Cloud 통합 | AEM에서 Creative Cloud으로 폴더 공유 는 Creative 사용자에게 AEM의 자산에 대한 액세스 권한을 부여하는 방법으로 AEM 6.2에서 도입되어, [!DNL Creative Cloud] 애플리케이션을 실행하고 새 파일을 업로드하거나 AEM에 변경 사항을 저장합니다. Creative Cloud 애플리케이션에서 새롭게 출시된 기능인 Adobe Asset Link는 Photoshop, InDesign 및 Illustrator에서 직접 AEM 자산에 액세스할 수 있는 강력한 권한과 함께 우수한 사용자 경험을 제공합니다. Adobe는 향후 Creative Cloud 폴더 공유 통합을 위해 AEM을 개선할 계획이 없습니다. 고객은 AEM에 해당 기능이 포함되어 있는 동안 교체 솔루션을 사용해 보시기 바랍니다. | 또한 Adobe Assset Link 또는 AEM 데스크탑 앱을 비롯한 새로운 Creative Cloud 통합 기능으로 전환하는 것이 좋습니다. |  |
| 에셋 | `AssetDownloadServlet` 게시 인스턴스에 대해 기본적으로 가 비활성화되어 있습니다. 자세한 내용은 [AEM 보안 검사 목록](/help/sites-administering/security-checklist.md)을 참조하십시오. | [AEM 보안 검사 목록](/help/sites-administering/security-checklist.md)에 설명된 구성입니다. |  |
| 에셋 | 사용자에게 `/content/dam/collections`를 채울 수 없습니다. | 사용자의 액세스 제어 설정을 적용하고 적합한 권한을 확인하십시오. |  |
| Adobe Search &amp; Promote | Adobe Search &amp; Promote와의 통합이 더 이상 사용되지 않습니다. Adobe는 향후 Search &amp; Promote 통합을 개선할 계획이 없습니다. Search &amp; Promote 통합이 더 이상 사용되지 않는 동안에도 계속 지원됩니다. |  |  |
| DTM 태그 관리자 | DTM(다이내믹 태그 관리자)과의 통합이 더 이상 사용되지 않습니다. | Adobe Experience Platform Launch를 태그 관리자로 사용하도록 전환. |  |
| Adobe Target | AEM에서 다음을 사용하여 Adobe Target 서비스에 연결할 수 있는 기능 추가 [!DNL Adobe I/O] AEM 6.5의 Adobe Target Standard API(Rest API) 기반의 Target Classic API(XML) 방식은 더 이상 사용되지 않습니다. | 통합 재구성 대상 [새 API 사용](https://helpx.adobe.com/kr/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html). |  |
| Adobe Target | 사용 `mbox.js` AEM에서 Adobe Target과의 통합 기능은 더 이상 사용되지 않습니다. | 사용할 전환 `at.js` 1.x |  |
| 상거래 | [CIF REST](https://github.com/adobe/commerce-cif-api)는 AEM과 상거래 엔진 간의 통합을 가능하게 하기 위해 마이크로 서비스 세트로 2018년에 제공되었습니다. Adobe이 2018년 중반에 Magento을 인수한 후, Adobe은 두 가지 이유로 접근 방식을 변경하기로 결정했습니다. Magento에는 고유한 상거래 API(REST 및 GraphQL) 세트가 있으며 두 개의 API 세트를 유지 관리하는 것은 좋지 않습니다. 시장 트렌드는 GraphQL이 데이터를 쿼리하는 보다 효율적인 방법이므로 고객이 GraphQL로 이동하고 있음을 나타냅니다. Adobe는 2019년 Magento의 GraphQL API를 소스로 사용하여 새로운 상거래 통합 프레임워크를 발표했습니다. Adobe는 더 이상 CIF REST에 투자할 계획이 없습니다. 고객은 교체 솔루션을 사용해야 합니다. | AEM-Magento 통합의 경우 로 전환합니다. [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype) 및 [AEM CIF 코어 구성 요소](https://github.com/adobe/aem-core-cif-components). AEM 및 Adobe Commerce 통합 을 참조하십시오 [commerce Integration Framework 사용](/help/commerce/cif/integrating/magento.md). 새로운 접근 방식과 타사(Magento 제외) 통합 지원이 로드맵에 있습니다. |  |
| 구성 요소(AEM Sites) | Adobe은 다음에 저장된 대부분의 기초 구성 요소를 추가로 개선할 계획이 없습니다 `/libs/foundation/components`. 을(를) 찾습니다. `cq:deprecated` 및 `cq:deprecatedReason` 구성 요소 폴더의 속성입니다. AEM 6.5에는 기초 구성 요소가 포함되어 있으며 이전 릴리스에서 업그레이드하는 고객은 있는 그대로 사용할 수 있습니다. 또한, 기초 구성 요소는 더 이상 사용되지 않더라도 완전히 지원됩니다. | Adobe은 향후 프로젝트에 코어 구성 요소 를 사용할 것을 권장합니다. 기존 사이트는 그대로 유지되거나 [AEM Modernize Tools 제품군](https://github.com/adobe/aem-modernize-tools)을 사용하여 코어 구성 요소를 사용하도록 사이트를 리팩터링할 수 있습니다. |  |
| 구성 요소(AEM Sites) | 디자인 Importer 구성 요소 `/libs/wcm/designimporter/components` 이 6.5부터 더 이상 사용되지 않는 것으로 표시되었습니다. Adobe은 디자인 가져오기 구현에 대해 더 이상 개선을 계획하지 않습니다. | Adobe은 향후 릴리스에서 사용 사례에 대한 대체 구현을 제공할 계획입니다. |  |
| Foundation | Granite 오프로드 프레임워크. Adobe은 자산 처리를 외부화하기 위해 CQ 5.6.1에 도입된 오프로딩 프레임워크를 추가로 개선할 계획이 없습니다. | Adobe는 차세대 클라우드 기반 오프로드 프레임워크에서 작동합니다. |  |
| 개발자 | `Hobbes.js`. Adobe은 향후 을 개선할 계획이 없습니다 `hobbes.js` 사용자 인터페이스 테스트 프레임워크. | 고객이 Selenium 자동화를 사용하는 것이 좋습니다. |  |
| 개발자 | jQuery UI 클라이언트 라이브러리. Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 jQuery UI 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다. | 코드에 여전히 jQuery UI가 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | jQuery Animation 클라이언트 라이브러리(`granite.jquery.animation`). Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 jQuery Animation 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다. | 코드에 여전히 jQuery Animation이 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | Handlebars 클라이언트 라이브러리. Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 Handlebars 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다. | 코드에 여전히 Handlebars가 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | Lawnchair 클라이언트 라이브러리. Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 Lawnchair 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다. | 코드에 여전히 Lawnchair가 필요한 고객은 코드를 해당 프로젝트 코드 베이스에 추가하시기 바랍니다. |  |
| 개발자 | `Granite.Sling.js` 클라이언트 라이브러리. Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 Granite.Sling.js 클라이언트 라이브러리를 개선할 계획이 없습니다. | 코드를 리팩토링하는 라이브러리 기능에 의존하고 있는 고객들은 더 이상 해당 기능을 사용할 수 없습니다. |  |
| 개발자 | YUI를 사용하여 JavaScript 클라이언트 라이브러리를 압축/축소할 수 있습니다. Adobe는 향후 YUI 라이브러리를 업데이트할 계획이 없습니다. AEM 6.4가 출시되기 이전까지, YUI는 기본적으로 GCC(Google Closure Compiler)로 전환할 수 있는 옵션과 함께 JavaScript를 축소할 수 있었습니다. AEM 6.5부터는 GCC가 기본값입니다. | 고객은 이러한 구현에 따라 GCC로 전환하기 위해 AEM 6.5로 업그레이드하는 것이 좋습니다. |  |
| 개발자 | CRXDE Lite의 클래식 UI 대화 상자 편집기. Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 클래식 UI 대화 상자 편집기를 개선할 계획이 없습니다. | 교체할 수 없습니다. |  |
| Forms | AEM Mobile과의 AEM Forms 통합은 더 이상 사용되지 않습니다. | 교체할 수 없습니다. |  | 개발자 | CRXDE Lite의 클래식 UI 대화 상자 편집기. Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 클래식 UI 대화 상자 편집기를 개선할 계획이 없습니다. | 교체할 수 없습니다. |  |
| 개발자 | 클라이언트 라이브러리 로드 대시/밑줄. Adobe은 배포(빠른 시작)의 일부로 제공되는 Lodash/underscore 클라이언트 라이브러리를 추가로 유지 및 업데이트할 계획이 없습니다. | Adobe은 코드에 여전히 Logdash/underscore가 필요한 고객에게 해당 코드를 해당 프로젝트 코드 베이스에 추가할 것을 권장합니다. |  |

## 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5에서 제거된 기능이 나와 있습니다. 이전 릴리스에는 이러한 기능이 더 이상 사용되지 않는 것으로 표시되었습니다.

| 영역 | 기능 | 대체 | 버전 (SP) |
|--- |--- |--- |--- |
| 통합 [!DNL Experience Cloud] | 자산을 와 동기화할 수 있습니다 [!DNL Experience Cloud] 를 통해 구성 사용 [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] 이전에 [!DNL Adobe Marketing Cloud]. | 문의 사항이 있으면, [고객 지원에 문의](https://www.adobe.com/kr/account/sign-in.supportportal.html). |  |
| Analytics Activity Map | AEM 내에 포함된 Activity Map 버전입니다. | Adobe Analytics API의 보안 변경 사항으로 인해, AEM 내에 포함된 Activity Map 버전을 더는 사용할 수 없습니다. 를 사용하십시오 [Adobe Analytics에서 제공하는 ActivityMap 플러그인](https://docs.adobe.com/content/help/ko-KR/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |  |
| 통합 | ExactTarget 통합이 기본 배포(빠른 시작)에서 제거되어 더 이상 사용할 수 없습니다. | 교체 없음. |  |
| 통합 | Salesforce Force API 통합이 기본 배포(빠른 시작)에서 제거되었으며 이제 설치할 추가 패키지입니다. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | 이 기능은 계속 사용할 수 있습니다. |
| 양식 | Adobe Central 제품이 더 이상 지원되지 않아 Adobe Central Migration Bridge 서비스 지원이 제거되었습니다. | 교체 없음. |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 교체 없음. |  |
| 양식 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 교체 없음 |  |
| 양식 | LiveCycle ES4 SP1에서 JEE의 AEM 6.5 Forms로 한 번에 업그레이드할 수 없음 | AEM Forms 업그레이드 설명서의 [사용 가능한 업그레이드 경로](../forms/using/upgrade.md)를 참조하십시오. |  |
| 양식 | JEE의 AEM Forms에서 UPD 기반 클러스터링 지원을 제거했습니다. | JEE의 AEM Forms에서는 TCP 기반 클러스터링만 사용할 수 있습니다. UDP 멀티캐스트 서버를 이전 버전에서 JEE의 AEM 5.5 Forms로 업그레이드하는 경우 수동 구성을 수행하여 TCP 기반 Gemfire 클러스터로 전환합니다. 자세한 지침은 [JEE의 AEM 6.5 양식으로 업그레이드](../forms/using/upgrade-forms-jee.md)를 참조하십시오. |  |
| 개발자 | Firebug Lite가 기본 배포(빠른 시작)에서 제거되었습니다. | 브라우저 내장 개발자 콘솔 사용 |
| 개발자 | HTML 클라이언트 라이브러리 관리자에서 `customJavaScriptPath` 지원을 제거합니다. | 교체 없음 |  |
| [!DNL Assets] | 자산 오프로딩 기능이에서 제거됩니다. [!DNL Adobe Experience Manager] 6.5. | 교체할 수 없습니다. |  |
| 캐시 | `system/console/slingjsp`가 제거되어 AEM 6.5에서 더 이상 사용할 수 없습니다. | 클래스 및 Slightly 캐시는 Apache Sling Commons FileSystem ClassLoader 번들 아래에 저장됩니다. AEM 웹 콘솔에서 번들 번호를 확인하고 파일 시스템(`crx-quickstart/launchpad/felix/bundle<ID>`)에서 직접 캐시 폴더를 제거할 수 있습니다. |  |

## 다음 릴리스에 대한 사전 공지 {#pre-announcement-for-next-release}

이 섹션은 향후 릴리스에서 예정된 변경 사항을 미리 알리는 데 사용됩니다. 발표된 변경 사항은 아직 유효하지 않지만 고객에게 영향을 줄 것입니다. 예를 들어 기능은 아직 더 이상 사용되지 않지만 사용 중단 후 사용자에게 영향을 줍니다. 이러한 업데이트는 계획용으로 제공됩니다.

| 영역 | 기능 | 공지 |
|--- |--- |--- |
| Foundation | UI 프레임워크 | Adobe는 2019년에 Coral UI 2 구성 요소를 더 이상 사용하지 않을 계획입니다. Coral UI 3이 AEM 6.2에서 도입되었으며, AEM 6.5는 Coral 3을 기반으로 합니다. Coral 2를 사용하여 사용자 지정 UI를 구축하는 고객 및 파트너는 Coral 3으로 리팩토링할 것을 권장합니다. Adobe는 Coral 2 대화 상자를 Coral 3으로 변환하는 도구를 제공하고 있습니다. - [자세히 보기](/help/sites-developing/modernization-tools.md) |
