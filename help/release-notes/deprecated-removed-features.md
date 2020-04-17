---
title: 더 이상 사용되지 않는 및 제거된 기능
description: Adobe Experience Manager 6.5의 더 이상 사용되지 않는 및 제거된 기능에 관한 릴리스 노트입니다.
uuid: 81d9a064-e712-4eff-bd3b-6e15513a5435
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: e8e2e01b-0117-48c3-86d8-609d29a147be
docset: aem65
translation-type: tm+mt
source-git-commit: 4be5286858b255a30983b5987ac54c4e71dd4f2f

---


# 더 이상 사용되지 않는 및 제거된 기능 {#deprecated-and-removed-features}

Adobe는 항상 이전 기능과의 호환성을 신중하게 고려하면서 전반적인 고객 가치를 향상하도록 오랜 시간에 걸쳐 오래된 기능을 새롭게 만들거나 더 현대적인 대안으로 교체하기 위해 제품 기능을 지속해서 평가합니다.

예정된 AEM 기능의 제거/교체를 알리려면 다음 규칙이 적용됩니다.

1. 사용 중지 공지가 먼저 표시됩니다. 더 이상 사용되지 않지만 기능은 계속 사용할 수 있지만 더 이상 향상되지 않습니다.
1. 더 이상 사용되지 않는 기능의 제거는 이르면 다음 주요 릴리스에서 실행됩니다. 실제 제거 대상일이 공지됩니다.

이 프로세스에서 고객에게 하나 이상의 릴리스 주기를 제공하여, 실제 제거 전에 더 이상 사용되지 않는 기능의 새 버전이나 후속 버전에 대한 구현을 채택할 수 있도록 합니다.

## 더 이상 사용되지 않는 기능 {#deprecated-features}

이 섹션에서는 AEM 6.5에서 더 이상 사용되지 않는 것으로 표시된 기능을 제시합니다. 일반적으로 이후 릴리스에서 제거될 예정인 기능은 먼저 사용 중지로 설정되고 대체 기능과 함께 제공됩니다.

고객은 현재 배포에서 기능을 사용할지 검토하고 대체 기능을 사용할 수 있도록 구현 변경을 계획하는 것이 좋습니다.

<table>
 <tbody>
  <tr>
   <td><b>영역</b></td>
   <td><b>기능</b></td>
   <td><b>대체</b></td>
  </tr>
  <tr>
   <td>Creative Cloud 통합</td>
   <td><p><a href="/help/assets/aem-cc-folder-sharing-best-practices.md">AEM에서 Creative Cloud</a> 폴더 공유에 대한 AEM은 크리에이티브 사용자가 AEM의 자산에 액세스할 수 있도록 하는 방법으로 AEM 6.2에서 도입되었으며, 이를 통해 CC 애플리케이션에서 열어 새 파일을 업로드하거나 AEM에 변경 내용을 저장할 수 있습니다. Creative Cloud 애플리케이션에서 새롭게 출시된 기능인 Adobe Asset Link는 Photoshop, InDesign 및 Illustrator에서 직접 AEM 자산에 액세스할 수 있는 강력한 권한과 함께 우수한 사용자 경험을 제공합니다.</p> <p>Adobe는 향후 Creative Cloud 폴더 공유 통합을 위해 AEM을 개선할 계획이 없습니다. 고객은 AEM에 해당 기능이 포함되어 있는 동안 교체 솔루션을 사용해 보시기 바랍니다.</p> </td>
   <td>고객은 Adobe Asset Link 또는 AEM 데스크탑 앱을 비롯한 새로운 Creative Cloud 통합 기능으로 전환해야 합니다. 자세한 내용은 <a href="/help/assets/aem-cc-integration-best-practices.md">AEM 및 Creative Cloud 통합 우수 사례</a>를 검토하십시오.</td>
  </tr>
  <tr>
   <td>자산</td>
   <td>
    <ol>
     <li>AssetDownloadServlet은 게시 인스턴스에 대해 기본적으로 사용 안함으로 설정됩니다. 자세한 내용은 <a href="/help/sites-administering/security-checklist.md">AEM 보안 검사 목록</a>을 참조하십시오.</li>
     <li>사용자에게 /content/dam/collections에 대한 충분한 (읽기 및 쓰기) 권한이 없는 경우 사용자는 컬렉션을 만들 수 없습니다.</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/sites-administering/security-checklist.md">AEM 보안 검사 목록</a>에 설명된 구성입니다.</li>
     <li>사용자의 액세스 제어 설정을 적용하고 적합한 권한을 확인하십시오.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Adobe Search &amp; Promote</td>
   <td><p>Adobe Search &amp; Promote와의 통합은 더 이상 사용되지 않습니다.</p> <p>Adobe는 향후 Search &amp; Promote 통합을 개선할 계획이 없습니다. Search &amp; Promote 통합이 더 이상 사용되지 않는 동안에도 계속 지원됩니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>DTM 태그 관리자</td>
   <td>DTM(다이내믹 태그 관리자)과의 통합이 더 이상 사용되지 않습니다.</td>
   <td>Adobe Experience Platform Launch를 태그 관리자로 사용하도록 전환</td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>AEM 6.5에서 Adobe I/O 기반 Adobe Target Standard API(Rest API)를 사용하여 AEM을 Adobe Target 서비스에 연결할 수 있는 기능이 추가됨에 따라 Target Classic API(XML) 방식은 더 이상 사용되지 않습니다.</td>
   <td><a href="https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html">새 API를 사용하도록 통합 재구성</a></td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>AEM에서 Adobe Target과 통합을 기반으로 한 mbox.js 사용이 더 이상 사용되지 않습니다.</td>
   <td>at.js 1.x를 사용하도록 전환</td>
  </tr>
  <tr>
   <td>상거래</td>
   <td><p><a href="https://github.com/adobe/commerce-cif-api" target="_blank">CIF REST는</a> AEM과 상거래 엔진 간의 통합을 활성화하는 마이크로 서비스 세트로 2018년에 제공되었습니다.</p> <p>Adobe는 2018년 중반에 Magento를 인수한 후 다음 두 가지 이유로 접근 방식을 변경하기로 결정했습니다. </p> <p><strong>1.</strong> Magento에는 고유한 상거래 API(REST 및 GraphQL) 세트가 있으며 두 개의 API 세트를 유지 관리하는 것은 좋지 않습니다 </p> <p><strong>2.</strong> 시장 트렌드는 데이터를 쿼리하는 보다 효율적인 방법이므로 고객이 GraphQL으로 이동하고 있음을 나타냅니다. Adobe는 2019년 Magento의 GraphQL API를 진실의 소스로 사용하여 새로운 상거래 통합 프레임워크를 발표했습니다.</p> <p>Adobe는 CIF REST에 더 이상 투자할 계획이 없습니다. 고객은 교체 솔루션을 사용해야 합니다.</p> </td>
   <td><p>AEM-Magento 통합의 경우 AEM <a href="https://github.com/adobe/aem-cif-project-archetype" target="_blank">CIF Tranype</a>및 AEM CIF <a href="https://github.com/adobe/aem-core-cif-components" target="_blank">핵심 구성 요소로 전환합니다</a></p> <p>자세한 내용은 Commerce <a href="https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md" target="_blank">Integration Framework를 사용한 AEM 및</a> Magento 통합을 참조하십시오.</p> <p>새로운 접근 방식과 타사(Magento 제외) 통합 지원이 로드맵에 있습니다.</p> </td>
  </tr>
  <tr>
   <td>구성 요소(AEM Sites)</td>
   <td><p>Adobe는 /libs/foundation/components에 저장된 기초 구성 요소의 대부분을 추가 개선할 계획이 없습니다.</p> <p>구성 요소 폴더에서 <strong>cq:deprecated</strong> 및 <strong>cq:deprecatedReason</strong> 속성을 찾습니다.</p> <p>AEM 6.5에는 Foundation 구성 요소가 포함되어 있으며 이전 릴리스에서 업그레이드하는 고객은 이를 그대로 계속 사용할 수 있습니다. 또한, 기본 구성 요소는 더 이상 사용하지 않는 동안 완전히 지원됩니다. </p> </td>
   <td>고객은 향후 프로젝트를 위해 코어 구성 요소를 사용하는 것이 좋습니다. Existing sites can remain as is or use the <a href="https://github.com/adobe/aem-modernize-tools">AEM Modernize Tools Suite</a> to refactor the site to use Core Components.</td>
  </tr>
  <tr>
   <td>구성 요소(AEM Sites)</td>
   <td>디자인 가져오기 프로그램 구성 요소 /libs/wcm/designimporter/components가 6.5부터 더 이상 사용되지 않음으로 표시되었습니다. Adobe는 디자인 가져오기 프로그램 구현을 추가 개선할 계획이 없습니다.</td>
   <td>Adobe는 향후 릴리스에서 사용 사례의 대체 구현을 제공할 계획입니다.</td>
  </tr>
  <tr>
   <td>구성 요소(AEM Forms)</td>
   <td><p>서명 단계에서는 사용자가 적응형 양식을 확인하고 서명할 수 있습니다. 이전 릴리스에서는 서명 단계에서 Adobe Sign과 Scribble Signature 구성 요소를 서명 필드로 사용할 수 있습니다. AEM 6.5 Forms에서 서명 단계의 서명 기반 서명 환경은 더 이상 사용되지 않습니다.</p> </td>
   <td>
    <ul>
     <li>새로 설치한 경우:
      <ul>
       <li>적응형 양식의 서명 단계에서 Adobe Sign 기반의 서명 경험을 사용할 수 있습니다.</li>
       <li>적응형 양식, 인터랙티브한 커뮤니케이션 및 HTML5 양식에 독립형 스크리블 서명 구성 요소를 사용할 수 있습니다.</li>
      </ul> </li>
     <li>이전 릴리스에서 AEM 6.5 양식으로 업그레이드한 경우<br />
      <ul>
       <li>이미 해당 기능을 사용하고 있는 양식에서 서명 단계의 문지르기 기반의 서명 경험을 계속 사용할 수 있습니다.<br /> </li>
       <li>새로운 양식을 만들 때 서명 단계에서 독립형 스크리블 서명 구성 요소 또는 Adobe Sign 기반의 서명 경험을 사용할 수 있습니다. </li>
      </ul> </li>
    </ul> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>Foundation</td>
   <td><p>Granite 오프로드 프레임워크</p> <p>Adobe는 향후 자산 처리를 구체화하기 위해 5.6.1에 도입된 오프로드 프레임워크를 개선할 계획이 없습니다. </p> </td>
   <td>Adobe는 차세대 클라우드 기반 오프로드 프레임워크에서 작동합니다.</td>
  </tr>
  <tr>
   <td>개발자</td>
   <td><p>Hobbes.js</p> <p>Adobe는 hobbes.js 사용자 인터페이스 테스트 프레임워크를 추가로 개선할 계획이 없습니다.</p> </td>
   <td>Adobe에서는 고객이 Selenium 자동화를 사용하는 것이 좋습니다.</td>
  </tr>
  <tr>
   <td>개발자</td>
   <td><p>jQuery UI 클라이언트 라이브러리</p> <p>Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 jQuery UI 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다.</p> </td>
   <td>Adobe에서는 코드에 jQuery UI가 필요한 고객이 프로젝트 코드 베이스에 추가할 것을 권장합니다.</td>
  </tr>
  <tr>
   <td>개발자</td>
   <td><p>jQuery 애니메이션 클라이언트 라이브러리(granite.jquery.animation)</p> <p>Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 jQuery Animation 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다.</p> </td>
   <td>Adobe에서는 코드에 jQuery 애니메이션을 필요로 하는 고객이 프로젝트 코드 베이스에 애니메이션을 추가할 것을 권장합니다.</td>
  </tr>
  <tr>
   <td>개발자</td>
   <td><p>Handlebars 클라이언트 라이브러리</p> <p>Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 Handlebars 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다.</p> </td>
   <td>Adobe에서는 코드에 Handlebars가 필요한 경우에도 프로젝트 코드 베이스에 추가할 것을 권장합니다.</td>
  </tr>
  <tr>
   <td>개발자</td>
   <td><p>Lawnchair 클라이언트 라이브러리</p> <p>Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 Lawnchair 클라이언트 라이브러리를 유지 및 업데이트할 계획이 없습니다.</p> </td>
   <td>Adobe에서는 프로젝트 코드 베이스에 코드를 추가해야 하는 고객에게 권장하고 있습니다.</td>
  </tr>
  <tr>
   <td>개발자</td>
   <td><p>Granite.Sling.js 클라이언트 라이브러리</p> <p>Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 Granite.Sling.js 클라이언트 라이브러리를 개선할 계획이 없습니다.</p> </td>
   <td>Adobe에서는 라이브러리의 기능에 의존하는 고객이 더 이상 코드를 사용하지 않도록 코드를 리팩터링할 것을 권장합니다.</td>
  </tr>
  <tr>
   <td>개발자</td>
   <td>YUI를 사용하여 JavaScript 클라이언트 라이브러리를 압축/축소할 수 있습니다. Adobe는 향후 YUI 라이브러리를 업데이트할 계획이 없습니다. AEM 6.4까지 YUI는 Google Closure Compiler(GCC 파섹)로 전환하는 옵션과 함께 JavaScript를 기본적으로 축소했습니다. AEM 6.5부터는 GCC가 기본값입니다.</td>
   <td>AEM 6.5로 업그레이드하여 GCC로 전환하는 것이 좋습니다.</td>
  </tr>
  <tr>
   <td>개발자</td>
   <td><p>CRXDE Lite의 클래식 UI 대화 상자 편집기</p> <p>Adobe는 향후 배포(빠른 시작)의 일부로 제공되는 클래식 UI 대화 상자 편집기를 개선할 계획이 없습니다.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>양식</td>
   <td><p>AEM Mobile과 AEM Forms 통합 사용 안 함 </p> </td>
   <td>교체 없음 </td>
  </tr>
 </tbody>
</table>

## 제거된 기능 {#removed-features}

이 섹션에는 AEM 6.5에서 제거된 기능 및 기능이 나열됩니다.이전 릴리스에는 이러한 기능이 더 이상 사용되지 않는 것으로 표시되었습니다.

| 영역 | 기능 | 대체 |
|--- |--- |--- |
| Analytics Activity Map | AEM 내에 포함된 Activity Map 버전. | Adobe Analytics API의 보안 변경 사항으로 인해, AEM 내에 포함된 Activity Map 버전을 더는 사용할 수 없습니다. Adobe Analytics [에서 제공하는 ActivityMap 플러그인을 사용합니다](https://docs.adobe.com/content/help/ko-KR/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| 통합 | ExactTarget 통합이 기본 배포(빠른 시작)에서 제거되었으며 더 이상 사용할 수 없습니다. | 교체 없음 |
| 통합 | Salesforce Force API 통합이 기본 배포(빠른 시작)에서 제거되었으며 이제 PackageShare에서 설치할 수 있는 추가 패키지입니다. | 기능은 계속 사용할 수 있습니다. |
| 양식 | Adobe Central 제품이 더 이상 지원되지 않아 Adobe Central Migration Bridge 서비스 지원이 제거되었습니다. | 교체 없음 |
| 양식 | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 교체 없음 |
| 양식 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 교체 없음 |
| 양식 | LiveCycle ES4 SP1에서 JEE의 AEM 6.5 Forms로 한 번에 업그레이드할 수 없습니다. | AEM Forms 업그레이드 설명서의 [사용 가능한 업그레이드 경로를](../forms/using/upgrade.md) 참조하십시오. |
| 개발자 | Firebug Lite가 기본 배포(빠른 시작)에서 제거되었습니다. | 브라우저 내장 개발자 콘솔 사용 |
| 개발자 | Remove `customJavaScriptPath` support in HTML Client Library Manager. | 교체 없음 |
| 자산 | 자산 오프로딩 기능이 AEM 6.5에서 제거되었습니다. | 교체 없음 |
| 캐시 | `system/console/slingjsp` 제거됨 은 AEM 6.5에서 더 이상 사용할 수 없습니다. | 클래스 및 Slightly 캐시는 Apache Sling Commons FileSystem ClassLoader 번들 아래에 저장됩니다. AEM 웹 콘솔에서 번들 번호를 확인하고 파일 시스템(`crx-quickstart/launchpad/felix/bundle<ID>`)에서 직접 캐시 폴더를 제거할 수 있습니다. |

## 다음 릴리스에 대한 사전 공지 {#pre-announcement-for-next-release}

이 섹션은 지원이 중단되지 않지만 고객에게 영향을 미치는 향후 릴리스의 변경 사항을 미리 알리기 위해 사용됩니다. 이 항목은 목표 계획용으로 제공됩니다.

| 영역 | 기능 | 공지 |
|--- |--- |--- |
| Foundation | UI 프레임워크 | Adobe는 2019년에 Coral UI 2 구성 요소를 더 이상 사용하지 않을 계획입니다. Coral UI 3이 AEM 6.2에서 도입되었으며, AEM 6.5는 Coral 3을 기반으로 합니다. Coral 2를 사용하여 사용자 지정 UI를 구축하는 고객 및 파트너는 Coral 3으로 리팩토링할 것을 권장합니다. Adobe는 Coral 2 대화 상자를 Coral 3으로 변환하는 도구를 제공하고 있습니다. - [자세히 보기](/help/sites-developing/dialog-conversion.md) |
