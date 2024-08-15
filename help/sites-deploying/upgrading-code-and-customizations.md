---
title: 코드 및 사용자 지정 업그레이드
description: AEM의 코드 및 사용자 지정 업그레이드에 대해 자세히 알아보십시오.
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '2143'
ht-degree: 0%

---

# 코드 및 사용자 지정 업그레이드{#upgrading-code-and-customizations}

업그레이드를 계획할 때 다음과 같은 구현 영역을 조사하고 해결해야 합니다.

* [코드 베이스 업그레이드](#upgrade-code-base)
* [6.5 저장소 구조와 일치](#align-repository-structure)
* [AEM 사용자 지정](#aem-customizations)
* [테스트 절차](#testing-procedure)

## 개요 {#overview}

1. **패턴 탐지기** - 업그레이드 계획에 설명되어 있고 [패턴 탐지기를 사용한 업그레이드 복잡성 평가](/help/sites-deploying/pattern-detector.md) 페이지에 자세히 설명되어 있는 대로 패턴 탐지기 실행 AEM의 Target 버전에서 사용할 수 없는 API/번들 외에 해결해야 하는 영역에 대한 자세한 내용을 포함하는 패턴 탐지기 보고서를 가져옵니다. 패턴 감지 보고서는 코드의 비호환성을 나타냅니다. 존재하지 않는 경우 배포는 이미 6.5와 호환됩니다. 6.5 기능을 사용하기 위해 새로운 개발을 수행하도록 선택할 수는 있지만, 단순히 호환성을 유지하기 위해 필요한 것은 아닙니다. 비호환성이 보고되면 호환성 모드에서 실행을 선택하고 새 6.5 기능이나 호환성에 대한 개발을 연기할 수 있습니다. 또는 업그레이드 후 개발을 결정하고 2단계로 이동할 수 있습니다. 자세한 내용은 [AEM 6.5의 이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md)을 참조하세요.

1. **6.5용 코드 베이스 개발 **- Target 버전의 코드 베이스에 대한 전용 분기 또는 저장소를 만듭니다. 업그레이드 전 호환성의 정보를 사용하여 업데이트할 코드 영역을 계획합니다.
1. **6.5 Uber jar로 컴파일 **- 6.5 uber jar를 가리키도록 코드 기반 POM을 업데이트하고 그에 대한 코드를 컴파일합니다.
1. **AEM 사용자 지정 업데이트*** - *AEM에 대한 모든 사용자 지정 또는 확장은 6.5에서 작동하도록 업데이트/유효성을 검사하고 6.5 코드 베이스에 추가해야 합니다. UI 검색 Forms, Assets 사용자 지정, /mnt/overlay를 사용하는 모든 항목을 포함합니다.

1. **6.5 환경에 배포** - 개발/QA 환경에서 AEM 6.5(작성자 + Publish)의 깨끗한 인스턴스를 설정해야 합니다. 업데이트된 코드 베이스와 대표적인 콘텐츠 샘플(현재 프로덕션)을 배포해야 합니다.
1. **QA 유효성 검사 및 버그 수정** - QA가 6.5의 작성자 및 Publish 인스턴스 모두에서 응용 프로그램의 유효성을 검사해야 합니다. 발견된 모든 버그를 수정하고 6.5 코드 베이스에 커밋해야 합니다. 모든 버그가 수정될 때까지 필요에 따라 개발-주기를 반복합니다.

업그레이드를 진행하기 전에 대상 버전의 AEM에 대해 철저하게 테스트된 안정적인 애플리케이션 코드 베이스가 있어야 합니다. 테스트에서 수행한 관찰을 기반으로 사용자 지정 코드를 최적화하는 방법이 있을 수 있습니다. 예를 들어 저장소 트래버스를 피하도록 코드를 리팩터링하는 작업, 검색을 최적화하는 사용자 지정 색인화 또는 JCR의 비순차 노드 사용 등이 포함될 수 있습니다.

새 AEM 버전에서 작동하도록 코드 기반 및 사용자 지정을 선택적으로 업그레이드할 수 있을 뿐만 아니라, 6.5는 [AEM 6.5의 이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md)에 설명된 대로 이전 버전과의 호환성 기능을 통해 사용자 지정을 보다 효율적으로 관리하는 데 도움이 됩니다.

위에서 언급하고 아래 다이어그램에 표시된 대로 첫 번째 단계에서 [패턴 탐지기](/help/sites-deploying/pattern-detector.md)를 실행하면 업그레이드의 전체 복잡성을 평가하는 데 도움이 될 수 있습니다. 또한 호환 모드에서 실행할지 또는 새로운 AEM 6.5 기능을 모두 사용하도록 사용자 지정을 업데이트할지를 결정하는 데 도움이 될 수 있습니다. 자세한 내용은 AEM 6.5](/help/sites-deploying/backward-compatibility.md) 페이지의 [이전 버전과의 호환성을 참조하십시오.
[![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## 코드 베이스 업그레이드 {#upgrade-code-base}

### 버전 제어 {#create-a-dedicated-branch-for-6.5-code-in-version-control}에서 6.5 코드에 대한 전용 분기 만들기

AEM 구현에 필요한 모든 코드 및 구성은 일부 버전의 제어를 사용하여 관리되어야 합니다. AEM의 대상 버전에서 코드 베이스에 필요한 변경 사항을 관리하기 위해 버전 제어의 전용 분기를 만들어야 합니다. AEM의 대상 버전 및 후속 버그 수정에 대한 코드 베이스의 반복적인 테스트는 이 분기에서 관리됩니다.

### AEM Uber Jar 버전 업데이트 {#update-the-aem-uber-jar-version}

AEM Uber jar에는 모든 AEM API가 Maven 프로젝트의 `pom.xml`에 단일 종속으로 포함되어 있습니다. 개별 AEM API 종속성을 포함하는 대신 Uber Jar를 단일 종속성으로 포함하는 것이 항상 모범 사례입니다. 코드 베이스를 업그레이드할 때 AEM의 대상 버전을 가리키도록 Uber Jar 버전을 변경합니다. Uber Jar가 존재하기 전 버전의 AEM에서 프로젝트를 개발한 경우 모든 개별 AEM API 종속성을 제거합니다. 대상 버전의 AEM에 대한 Uber Jar를 단일 포함으로 대체합니다. 새 버전의 Uber Jar에 대해 코드 베이스를 다시 컴파일합니다. 더 이상 사용되지 않는 API 또는 메서드를 AEM의 target 버전과 호환되도록 업데이트합니다.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 관리 리소스 확인자 사용 중단 {#phase-out-use-of-administrative-resource-resolver}

`SlingRepository.loginAdministrative()` 및 `ResourceResolverFactory.getAdministrativeResourceResolver()`을(를) 통한 관리 세션의 사용은 AEM 6.0 이전의 코드 기반에서 일반적이었습니다. 이러한 메서드는 액세스 수준을 너무 광범위하게 제공하므로 보안상의 이유로 더 이상 사용되지 않습니다. [이후 버전의 Sling에서는 이러한 메서드가 제거됩니다](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). 대신 서비스 사용자를 사용하도록 코드를 리팩터링하는 것이 좋습니다. 서비스 사용자 및 관리 세션을 단계적으로 중단하는 방법에 대한 자세한 내용은 [Adobe Experience Manager(AEM)의 서비스 사용자](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions)를 참조하십시오.

### 쿼리 및 Oak 색인 {#queries-and-oak-indexes}

코드 베이스의 모든 쿼리 사용은 코드 베이스를 업그레이드하는 과정에서 철저하게 테스트되어야 합니다. Jackrabbit 2(6.0 이전 버전의 AEM)에서 업그레이드하는 고객의 경우 Oak에서 콘텐츠를 자동으로 색인화하지 않으며 사용자 지정 색인을 만들어야 하므로 이 테스트가 특히 중요합니다. AEM 6.x 버전에서 업그레이드하는 경우 기본 Oak 색인 정의가 변경되었을 수 있으며 기존 쿼리에 영향을 줄 수 있습니다.

다음 도구는 쿼리 성능을 분석 및 검사하는 데 사용할 수 있습니다.

* [AEM 색인 도구](/help/sites-deploying/queries-and-indexing.md)

* [작업 진단 도구 - 쿼리 성능](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### 클래식 UI 작성 {#classic-ui-authoring}

클래식 UI 작성은 AEM 6.5에서 계속 사용할 수 있지만 더 이상 사용되지 않습니다. 자세한 내용은 [사용되지 않거나 제거된 기능](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release)을 참조하십시오. 애플리케이션이 클래식 UI 작성자 환경에서 실행 중인 경우 AEM 6.5로 업그레이드하고 클래식 UI를 계속 사용하는 것이 좋습니다. 그런 다음 Touch UI로의 마이그레이션을 별도의 프로젝트로 계획하여 여러 개발 주기에 걸쳐 완료할 수 있습니다. AEM 6.5에서 클래식 UI를 사용하려면 여러 OSGi 구성을 코드 베이스에 커밋해야 합니다. 구성을 수행하는 방법에 대한 자세한 내용은 [클래식 UI에 대한 액세스 활성화](/help/sites-administering/enable-classic-ui.md)에서 확인할 수 있습니다.

## 6.5 저장소 구조와 일치 {#align-repository-structure}

업그레이드를 보다 쉽게 하고 업그레이드 중에 구성을 덮어쓰지 않도록 6.4에서 저장소를 재구성하여 콘텐츠와 구성을 구분합니다.

따라서 여러 설정을 이전과 같이 `/etc` 아래에 더 이상 있지 않도록 이동해야 합니다. AEM 6.4로 업데이트된 내용을 검토하고 수용해야 하는 전체 저장소 재구성 관련 사항을 검토하려면 [AEM 6.4의 저장소 재구성](/help/sites-deploying/repository-restructuring.md)을 참조하십시오.

## AEM 사용자 지정  {#aem-customizations}

AEM 소스 버전의 AEM 작성 환경에 대한 모든 사용자 지정을 식별해야 합니다. 식별되면 각 사용자 지정을 버전 제어에 저장하거나 최소한 콘텐츠 패키지의 일부로 백업하는 것이 좋습니다. 프로덕션 업그레이드 전에 AEM의 대상 버전을 실행하는 QA 또는 스테이징 환경에서 모든 사용자 지정을 배포하고 확인해야 합니다.

### 일반 오버레이 {#overlays-in-general}

/libs 아래의 노드 및/또는 파일을 /apps 아래의 추가 노드와 오버레이하여 즉시 사용 가능한 AEM 기능을 확장하는 것이 일반적인 방법입니다. 이러한 오버레이는 버전 제어에서 추적하고 AEM의 대상 버전에 대해 테스트해야 합니다. Adobe 파일(예: JS, JSP, HTL)이 오버레이되면 AEM의 대상 버전에서 보다 쉬운 회귀 테스트를 위해 보강된 기능에 주석을 남기는 것이 좋습니다. 일반 정보는 [오버레이](/help/sites-developing/overlays.md)를 참조하십시오. 특정 AEM 오버레이에 대한 지침은 아래에 나와 있습니다.

### 사용자 정의 검색 Forms 업그레이드 {#upgrading-custom-search-forms}

사용자 정의 검색 패싯이 제대로 작동하려면 업그레이드 후 몇 가지 수동 조정이 필요합니다. 자세한 내용은 [사용자 지정 검색 Forms 업그레이드](/help/sites-deploying/upgrading-custom-search-forms.md)를 참조하십시오.

### Assets UI 사용자 지정 {#assets-ui-customizations}

>[!NOTE]
>
>이 절차는 AEM 6.2 이전 버전에서 업그레이드하는 경우에만 필요합니다.

Assets 배포를 사용자 지정한 인스턴스는 업그레이드를 준비해야 합니다. 이 작업은 사용자 지정된 모든 콘텐츠가 새 6.4 노드 구조와 호환되는지 확인하는 데 필요합니다.

다음을 수행하여 Assets UI에 대한 사용자 지정을 준비할 수 있습니다.

1. 업그레이드되는 인스턴스에서 *https://server:port/crx/de/index.jsp*(으)로 이동하여 CRXDE Lite을 엽니다.

1. 다음 노드로 이동합니다.

   * `/apps/dam/content`

1. 창의 왼쪽에 있는 탐색기 창을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**&#x200B;를 선택하여 콘텐츠 노드의 이름을 **content_backup**(으)로 변경합니다.

1. 노드의 이름이 바뀌면 `/apps/dam` 아래 **content**(이)라는 이름의 content 노드를 만들고 해당 노드 유형을 **sling:Folder**(으)로 설정하십시오.

1. 탐색기 창에서 각 자식 노드를 마우스 오른쪽 단추로 클릭하고 **이동**&#x200B;을 선택하여 **content_backup**&#x200B;의 모든 자식 노드를 새로 만든 콘텐츠 노드로 이동합니다.

1. **content_backup** 노드를 삭제합니다.

1. 올바른 노드 유형이 `sling:Folder`인 `/apps/dam` 아래의 업데이트된 노드는 버전 제어에 저장하고 코드 베이스를 사용하여 배포하거나 최소한 콘텐츠 패키지로 백업해야 합니다.

### 기존 Assets에 대한 자산 ID 생성 {#generating-asset-ids-for-existing-assets}

기존 에셋에 대한 에셋 ID를 생성하려면 AEM 인스턴스를 업그레이드하여 AEM 6.5를 실행할 때 에셋을 업그레이드하십시오. 이 단계는 [Assets Insights 기능](/help/assets/asset-insights.md)을 사용하도록 설정하는 데 필요합니다. 자세한 내용은 [포함 코드 추가](/help/assets/use-page-tracker.md#add-embed-code)를 참조하십시오.

자산을 업그레이드하려면 JMX 콘솔에서 자산 ID 연결 패키지를 구성합니다. 저장소의 자산 수에 따라 `migrateAllAssets`에 시간이 오래 걸릴 수 있습니다. Adobe의 내부 테스트에서는 TarMK에 있는 125000 자산에 대해 약 1시간 정도를 예상합니다.

![1487758945977](assets/1487758945977.png)

전체 자산의 하위 집합에 자산 ID가 필요한 경우 `migrateAssetsAtPath` API를 사용하십시오.

다른 모든 용도로는 `migrateAllAssets()` API를 사용하십시오.

### InDesign 스크립트 사용자 정의 {#indesign-script-customizations}

Adobe은 `/apps/settings/dam/indesign/scripts` 위치에 사용자 지정 스크립트를 배치하는 것을 권장합니다. InDesign 스크립트 사용자 지정에 대한 자세한 내용은 [Adobe InDesign Server과 Adobe Experience Manager Assets 통합](/help/assets/indesign.md#configuring-the-aem-assets-workflow)에서 확인할 수 있습니다.

### ContextHub 구성 복구 {#recovering-contexthub-configurations}

ContextHub 구성은 업그레이드의 영향을 받습니다. 기존 ContextHub 구성을 복구하는 방법에 대한 지침은 [ContextHub 구성](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading)을 참조하십시오.

### 워크플로우 사용자 지정 {#workflow-customizations}

일반적으로 필요 없는 기능을 추가하거나 제거하기 위해 기본 제공 워크플로우를 편집하는 것입니다. 사용자 지정된 일반적인 워크플로는 [!UICONTROL DAM 자산 업데이트] 워크플로입니다. 사용자 지정 구현에 필요한 모든 워크플로는 업그레이드 중에 덮어쓸 수 있으므로 버전 제어에 백업하고 저장해야 합니다.

### 편집 가능한 템플릿 {#editable-templates}

>[!NOTE]
>
>이 절차는 AEM 6.2에서 편집 가능한 템플릿을 사용하여 사이트를 업그레이드하는 경우에만 필요합니다

편집 가능한 템플릿의 구조가 AEM 6.2와 6.3 사이에서 변경되었습니다. 6.2 이전 버전에서 업그레이드하고 편집 가능한 템플릿을 사용하여 사이트 콘텐츠를 빌드한 경우 [응답형 노드 정리 도구](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration)를 사용해야 합니다. 이 도구는 **after** 업그레이드를 실행하여 콘텐츠를 정리하기 위한 것입니다. 작성자 및 Publish 계층 모두에서 실행합니다.

### CUG 구현 변경 사항 {#cug-implementation-changes}

폐쇄형 사용자 그룹 구현은 이전 버전의 AEM에서 성능 및 확장성 제한을 해결하기 위해 크게 변경되었습니다. 이전 버전의 CUG는 6.3에서 더 이상 사용되지 않으며 새 구현은 Touch UI에서만 지원됩니다.

## 테스트 절차 {#testing-procedure}

업그레이드를 테스트할 수 있는 포괄적인 테스트 계획을 마련해야 합니다. 업그레이드된 코드 베이스와 애플리케이션을 먼저 낮은 환경에서 테스트해야 합니다. 발견된 모든 버그는 코드 베이스가 안정될 때까지 반복적인 방식으로 수정해야 하며 상위 수준의 환경만 업그레이드해야 합니다.

### 업그레이드 프로시저 테스트 {#testing-the-upgrade-procedure}

여기에 설명된 업그레이드 절차는 사용자 지정된 실행 설명서에 설명된 대로 개발 및 QA 환경에서 테스트해야 합니다([업그레이드 계획](/help/sites-deploying/upgrade-planning.md) 참조). 업그레이드 절차는 업그레이드 실행 설명서에 모든 단계가 문서화되고 업그레이드 프로세스가 원활해질 때까지 반복해야 합니다.

### 구현 테스트 영역  {#implementation-test-areas-}

다음은 환경이 업그레이드되고 업그레이드된 코드 베이스가 배포된 후 테스트 계획에서 다루어야 하는 AEM 구현의 중요한 영역입니다.

<table>
 <tbody>
  <tr>
   <td><strong>기능 테스트 영역</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>게시된 사이트</td>
   <td>Dispatcher을 통해 게시 계층 <br />에서 AEM 구현 및 관련 코드를 테스트하는 중입니다. 페이지 업데이트 및 <br /> 캐시 무효화에 대한 기준을 포함해야 합니다.</td>
  </tr>
  <tr>
   <td>작성</td>
   <td>작성자 계층에서 AEM 구현 및 관련 코드 테스트. 페이지, 구성 요소 작성 및 대화 상자를 포함해야 합니다.</td>
  </tr>
  <tr>
   <td>Experience Cloud 솔루션과 통합</td>
   <td>Analytics, DTM 및 Target과 같은 제품과의 통합 확인.</td>
  </tr>
  <tr>
   <td>서드파티 시스템과 통합</td>
   <td>작성자 및 Publish 계층 모두에서 서드파티 통합의 유효성을 검사합니다.</td>
  </tr>
  <tr>
   <td>인증, 보안 및 권한</td>
   <td>LDAP/SAML과 같은 모든 인증 메커니즘은 유효성을 검사해야 합니다.<br />개의 권한 및 그룹을 작성자 및 Publish<br /> 계층 모두에서 테스트해야 합니다.</td>
  </tr>
  <tr>
   <td>쿼리</td>
   <td>쿼리 성능과 함께 사용자 지정 인덱스 및 쿼리를 테스트해야 합니다.</td>
  </tr>
  <tr>
   <td>UI 사용자 지정</td>
   <td>작성 환경에서 AEM UI에 대한 모든 확장 또는 사용자 정의.</td>
  </tr>
  <tr>
   <td>워크플로</td>
   <td>사용자 지정 및/또는 기본 제공 워크플로 및 기능입니다.</td>
  </tr>
  <tr>
   <td>성능 테스트</td>
   <td>로드 테스트는 실제 시나리오를 시뮬레이션하는 작성자 및 Publish 계층 모두에서 수행해야 합니다.</td>
  </tr>
 </tbody>
</table>

### 문서 테스트 계획 및 결과 {#document-test-plan-and-results}

위의 구현 테스트 영역을 다루는 테스트 계획을 만들어야 합니다. 종종 테스트 계획을 작성자와 Publish 작업 목록으로 구분하는 것이 적절합니다. 프로덕션 환경을 업그레이드하기 전에 개발, QA 및 스테이징 환경에서 이 테스트 계획을 실행해야 합니다. 스테이지 및 프로덕션 환경을 업그레이드할 때 비교할 수 있도록 테스트 결과 및 성능 지표를 낮은 환경에서 캡처해야 합니다.
