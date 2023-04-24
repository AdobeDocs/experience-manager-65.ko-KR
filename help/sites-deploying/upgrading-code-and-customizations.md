---
title: 코드 및 사용자 지정 업그레이드
seo-title: Upgrading Code and Customizations
description: AEM에서 사용자 지정 코드를 업그레이드하는 방법에 대해 자세히 알아보십시오.
seo-description: Learn more about upgrading custom code in AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 0%

---

# 코드 및 사용자 지정 업그레이드{#upgrading-code-and-customizations}

업그레이드를 계획할 때 구현의 다음 영역을 조사하고 해결해야 합니다.

* [코드 기본 업그레이드](#upgrade-code-base)
* [6.5 저장소 구조와 정렬](#align-repository-structure)
* [AEM 사용자 지정](#aem-customizations)
* [테스트 절차](#testing-procedure)

## 개요 {#overview}

1. **패턴 탐지기** - 업그레이드 계획에 설명된 대로 패턴 탐지기를 실행하고 [이 페이지](/help/sites-deploying/pattern-detector.md). AEM Target 버전에서 사용할 수 없는 API/번들 외에 해결해야 하는 영역에 대한 자세한 내용을 포함하는 패턴 탐지기 보고서가 제공됩니다. 패턴 감지 보고서는 코드에서 호환되지 않는 것을 알려줍니다. 존재하지 않는 경우 배포는 이미 6.5와 호환됩니다. 여전히 6.5 기능을 사용하기 위해 새로운 개발 작업을 수행하도록 선택할 수 있지만 호환성을 유지하기 위해서만 필요하지 않습니다. 호환되지 않는 기능이 보고된 경우 호환성 모드에서 실행을 선택하고 새로운 6.5 기능 또는 호환성에 대한 개발을 연기할 수 있습니다. 또는 업그레이드 후 개발을 수행하고 2단계로 이동할 수도 있습니다. 자세한 내용은 [AEM 6.5의 이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md) 자세한 내용

1. **6.5용 코드 베이스 개발 ** - Target 버전에 대한 코드 베이스에 대한 전용 분기 또는 저장소를 만듭니다. 업데이트할 코드 영역을 계획하려면 업그레이드 전 호환성 정보를 사용하십시오.
1. **6.5 Uber jar로 컴파일합니다 **- 코드 기본 POM을 업데이트하여 6.5 uber jar를 가리키고 그에 대해 코드를 컴파일합니다.
1. **AEM 사용자 지정 업데이트*** - *AEM에 대한 모든 사용자 지정 또는 확장은 6.5에서 작동하도록 업데이트/검증하고 6.5 코드 베이스에 추가해야 합니다. UI 검색 Forms, 자산 사용자 지정, /mnt/overlay를 사용하는 모든 항목 포함

1. **6.5 환경에 배포** - AEM 6.5(작성자 + 게시)의 클린 인스턴스는 개발/QA 환경에서 일어나야 합니다. 업데이트된 코드 베이스와 현재 프로덕션에서 제공하는 대표적인 컨텐츠 샘플을 배포해야 합니다.
1. **QA 유효성 검사 및 버그 수정** - QA는 6.5의 작성자 및 게시 인스턴스에서 모두 애플리케이션의 유효성을 확인해야 합니다. 발견된 버그는 모두 수정하고 6.5 코드 베이스에 커밋해야 합니다. 모든 버그가 수정될 때까지 필요에 따라 개발 주기를 반복합니다.

업그레이드를 진행하기 전에 AEM의 대상 버전에 대해 철저하게 테스트한 안정적인 애플리케이션 코드 베이스가 있어야 합니다. 테스트의 관찰을 기반으로 사용자 지정 코드를 최적화하는 방법이 있을 수 있습니다. 예를 들어, 저장소 탐지를 방지하기 위해 코드 리팩터링, 검색을 최적화하기 위한 사용자 지정 색인 지정 또는 JCR에서 순서가 없는 노드를 사용하는 등의 작업이 포함될 수 있습니다.

6.5는 코드 베이스와 사용자 지정을 선택적으로 업그레이드하여 새로운 AEM 버전에서 작업할 수 있을 뿐만 아니라 다음과 같이 이전 버전과의 호환성 기능을 사용하여 사용자 지정을 보다 효율적으로 관리할 수도 있습니다 [이 페이지](/help/sites-deploying/backward-compatibility.md).

위에서 언급했듯이 아래 다이어그램에 표시된 대로 [패턴 탐지기](/help/sites-deploying/pattern-detector.md) 첫 번째 단계에서는 업그레이드의 전반적인 복잡성을 평가하는 데 도움이 될 수 있습니다. 또한 호환성 모드에서 실행할지 또는 모든 새로운 AEM 6.5 기능을 사용하도록 사용자 지정을 업데이트할지 여부를 결정하는 데 도움이 될 수 있습니다. 자세한 내용은 [AEM 6.5의 이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md) 페이지를 참조하십시오.
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## 코드 기본 업그레이드 {#upgrade-code-base}

### 버전 제어에서 6.5 코드용 전용 분기 만들기 {#create-a-dedicated-branch-for-6.5-code-in-version-control}

AEM 구현에 필요한 모든 코드와 구성은 일부 버전의 제어를 사용하여 관리해야 합니다. AEM의 대상 버전에서 코드 베이스에 필요한 변경 사항을 관리하기 위해 버전 제어의 전용 분기를 만들어야 합니다. AEM의 Target 버전에 대해 코드 베이스에 대한 반복적인 테스트 및 후속 버그 수정은 이 분기에서 관리됩니다.

### AEM Uber Jar 버전 업데이트 {#update-the-aem-uber-jar-version}

AEM Uber jar에는 Maven 프로젝트의 단일 종속으로 모든 AEM API가 포함됩니다 `pom.xml`. 개별 AEM API 종속성을 포함하지 않고 항상 Uber Jar를 단일 종속으로 포함하는 것이 좋습니다. 코드 베이스를 업그레이드할 때 Uber Jar 버전을 변경하여 AEM의 대상 버전으로 가리킵니다. 프로젝트가 Uber Jar가 존재하기 전에 AEM 버전에서 개발된 경우 모든 개별 AEM API 종속성을 제거합니다. AEM의 대상 버전에 대한 Uber Jar의 단일 포함으로 대체합니다. 새 버전의 Uber Jar에 대해 코드 베이스를 다시 컴파일합니다. 더 이상 사용되지 않는 API 또는 메서드가 AEM의 target 버전과 호환되도록 업데이트합니다.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 관리 리소스 확인자의 단계 사용 중단 {#phase-out-use-of-administrative-resource-resolver}

를 통해 관리 세션 사용 `SlingRepository.loginAdministrative()` 및 `ResourceResolverFactory.getAdministrativeResourceResolver()` 는 AEM 6.0 이전의 코드 베이스에서 일반적이었습니다. 이러한 메서드는 너무 광범위한 액세스 수준을 제공하므로 보안상의 이유로 사용되지 않습니다. [향후 버전의 Sling에서는 이러한 방법이 제거됩니다](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). 대신 서비스 사용자를 사용하도록 모든 코드를 리팩터링하는 것이 좋습니다. 서비스 사용자에 대한 자세한 정보 및 [관리 세션을 단계적으로 종료하는 방법은 여기에서 찾을 수 있습니다.](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions).

### 쿼리 및 Oak 색인 {#queries-and-oak-indexes}

코드 베이스에서 쿼리의 모든 사용은 코드 베이스를 업그레이드하는 과정의 일부로 철저히 테스트해야 합니다. Jackrabbit 2(6.0 이전 버전의 AEM)에서 업그레이드하는 고객의 경우 Oak가 컨텐츠를 자동으로 색인화하지 않으며 사용자 지정 인덱스를 만들어야 하므로 이 테스트가 특히 중요합니다. AEM 6.x 버전에서 업그레이드하는 경우 기본 Oak 색인 정의가 변경되었으며 기존 쿼리에 영향을 줄 수 있습니다.

다음 도구는 쿼리 성능을 분석 및 검사하는 데 사용할 수 있습니다.

* [AEM 색인 도구](/help/sites-deploying/queries-and-indexing.md)

* [작업 진단 도구 - 쿼리 성능](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### 클래식 UI 작성 {#classic-ui-authoring}

클래식 UI 작성은 AEM 6.5에서 계속 사용할 수 있지만 더 이상 사용되지 않습니다. 자세한 내용 [여기](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release). 애플리케이션이 클래식 UI 작성 환경에서 실행 중인 경우 AEM 6.5로 업그레이드하고 클래식 UI를 계속 사용하는 것이 좋습니다. 그런 다음 터치 UI로의 마이그레이션을 여러 개발 주기에 걸쳐 완료할 수 있도록 별도의 프로젝트로 계획할 수 있습니다. AEM 6.5에서 클래식 UI를 사용하려면 코드 베이스에 몇 가지 OSGi 구성을 커밋해야 합니다. 구성 방법에 대한 자세한 내용은 [여기](/help/sites-administering/enable-classic-ui.md).

## 6.5 저장소 구조와 정렬 {#align-repository-structure}

업그레이드를 보다 쉽게 하고 업그레이드 중에 구성을 덮어쓰지 않도록 하기 위해 리포지토리는 6.4에서 재구성되어 구성에서 컨텐츠를 분리합니다.

따라서 더 이상 다음 위치에 있지 않도록 여러 설정을 이동해야 합니다 `/etc` 과거에 그랬던 것처럼. 업데이트된 AEM 6.4로 검토 및 수용해야 하는 전체 저장소 구조 변경 문제를 검토하려면 다음을 참조하십시오 [AEM 6.4의 저장소 구조 변경](/help/sites-deploying/repository-restructuring.md).

## AEM 사용자 지정  {#aem-customizations}

AEM 소스 버전의 AEM 작성 환경에 대한 모든 사용자 지정을 식별해야 합니다. 식별되면 각 사용자 지정을 버전 제어에 저장하거나 컨텐츠 패키지의 일부로 백업되는 최소 상태로 저장하는 것이 좋습니다. 모든 사용자 지정 사항은 프로덕션 업그레이드 전에 AEM의 대상 버전을 실행하는 QA 또는 스테이징 환경에서 배포하고 검증해야 합니다.

### 일반적으로 오버레이 {#overlays-in-general}

/apps 아래의 추가 노드와 함께 /libs 아래에 노드 및/또는 파일을 오버레이하여 기본 제공 AEM 기능을 확장하는 것이 일반적입니다. 이러한 오버레이는 버전 제어에서 추적되고 AEM의 대상 버전에 대해 테스트해야 합니다. 파일(예: JS, JSP, HTL)을 오버레이하는 경우 AEM의 대상 버전에서 보다 쉽게 회귀 테스트를 위해 보강된 기능에 대해 주석을 달 것을 권장합니다. 일반적으로 오버레이에 대한 자세한 내용은 [여기](/help/sites-developing/overlays.md). 특정 AEM 오버레이에 대한 지침은 아래에 나와 있습니다.

### 사용자 지정 검색 Forms 업그레이드 {#upgrading-custom-search-forms}

사용자 정의 검색 패싯을 사용하려면 업그레이드 후 올바르게 조정해야 합니다. 자세한 내용은 [사용자 지정 검색 Forms 업그레이드](/help/sites-deploying/upgrading-custom-search-forms.md).

### 자산 UI 사용자 지정 {#assets-ui-customizations}

>[!NOTE]
>
>이 절차는 AEM 6.2 이전 버전에서 업그레이드하는 경우에만 필요합니다.

사용자 지정된 Assets 배포를 가진 인스턴스는 업그레이드를 준비해야 합니다. 이 작업은 사용자 지정된 모든 컨텐츠가 새 6.4 노드 구조와 호환되도록 하는 데 필요합니다.

다음을 수행하여 자산 UI에 대한 사용자 지정을 준비할 수 있습니다.

1. 업그레이드되는 인스턴스에서 다음 위치로 이동하여 CRXDE Lite을 엽니다 *https://server:port/crx/de/index.jsp*

1. 다음 노드로 이동합니다.

   * `/apps/dam/content`

1. 컨텐츠 노드 이름을 다음으로 변경합니다. **content_backup** 창의 왼쪽에 있는 탐색기 창을 마우스 오른쪽 단추로 클릭하고 **이름 변경**.

1. 노드의 이름이 변경된 후에는 아래에 content 라는 노드를 만드십시오. `/apps/dam` 명명된 이름 **콘텐츠** 노드 유형을 로 설정하고 **sling:Folder**.

1. 의 모든 하위 노드 이동 **content_backup** 탐색기 창에서 각 하위 노드를 마우스 오른쪽 단추로 클릭하고 을 선택하여 새로 만든 컨텐츠 노드로 이동합니다 **이동**.

1. 삭제 **content_backup** 노드 아래에 있어야 합니다.

1. 아래의 업데이트된 노드 `/apps/dam` 올바른 노드 유형 사용 `sling:Folder` 버전 제어에 저장되고 코드 베이스와 함께 또는 컨텐츠 패키지로 최소 백업되는 상태로 배포해야 합니다.

### 기존 자산에 대한 자산 ID 생성 {#generating-asset-ids-for-existing-assets}

기존 자산에 대한 자산 ID를 생성하려면 AEM 인스턴스를 업그레이드하여 AEM 6.5를 실행할 때 자산을 업그레이드하십시오. 이 단계는 [자산 통찰력 기능](/help/assets/asset-insights.md). 자세한 내용은 [포함 코드 추가](/help/assets/use-page-tracker.md#add-embed-code).

자산을 업그레이드하려면 JMX 콘솔에서 자산 ID 연결 패키지를 구성합니다. 저장소의 자산 수에 따라, `migrateAllAssets` 시간이 오래 걸릴 수 있습니다 Adobe의 내부 테스트는 TarMK의 125000 자산에 대해 약 1시간 동안 측정됩니다.

![1487758945977](assets/1487758945977.png)

전체 자산의 하위 세트에 대해 자산 ID가 필요한 경우, `migrateAssetsAtPath` API.

다른 모든 목적으로 `migrateAllAssets()` API.

### InDesign 스크립트 사용자 지정 {#indesign-script-customizations}

Adobe은 사용자 지정 스크립트를 `/apps/settings/dam/indesign/scripts` 위치. InDesign 스크립트 사용자 지정에 대한 자세한 내용을 찾을 수 있습니다 [여기](/help/assets/indesign.md#configuring-the-aem-assets-workflow).

### ContextHub 구성 복구 {#recovering-contexthub-configurations}

ContextHub 구성은 업그레이드의 영향을 받습니다. 기존 ContextHub 구성 복구 방법에 대한 지침을 찾을 수 있습니다 [여기](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading).

### 워크플로우 사용자 지정 {#workflow-customizations}

기본 워크플로우를 편집하여 불필요한 기능을 추가하거나 제거하는 일반적인 방법입니다. 사용자 지정된 일반적인 워크플로우는 [!UICONTROL DAM 자산 업데이트] 워크플로우. 사용자 지정 구현에 필요한 모든 워크플로우는 업그레이드 중에 덮어쓸 수 있으므로 백업 및 버전 제어에 저장해야 합니다.

### 편집 가능한 템플릿 {#editable-templates}

>[!NOTE]
>
>이 절차는 AEM 6.2에서 편집 가능한 템플릿을 사용하여 사이트 업그레이드에만 필요합니다

편집 가능한 템플릿의 구조가 AEM 6.2와 6.3 간에 변경되었습니다. 6.2 이전 버전에서 업그레이드하는 경우 사이트 컨텐츠가 편집 가능한 템플릿을 사용하여 빌드되는 경우 [응답형 노드 정리 도구](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration). 이 도구는 **after** 컨텐츠 정리를 위한 업그레이드. 작성 계층과 게시 계층 모두에서 실행합니다.

### CUG 구현 변경 {#cug-implementation-changes}

닫힌 사용자 그룹 구현이 이전 버전의 AEM의 성능 및 확장성 제한을 해결하기 위해 크게 변경되었습니다. 이전 버전의 CUG는 6.3에서 더 이상 사용되지 않으며, 새 구현은 Touch UI에서만 지원됩니다. 6.2 이전 버전에서 업그레이드하는 경우 새 CUG 구현으로 마이그레이션하는 지침을 찾을 수 있습니다 [여기](/help/sites-administering/closed-user-groups.md#upgradetoaem63).

## 테스트 절차 {#testing-procedure}

업그레이드 테스트 등을 위한 종합적인 테스트 계획을 세워야 한다. 업그레이드된 코드 베이스와 응용 프로그램을 테스트하려면 먼저 낮은 환경에서 수행해야 합니다. 발견된 모든 버그는 코드 베이스가 안정될 때까지 반복적으로 수정해야 하며, 이후 상위 수준 환경만 업그레이드해야 합니다.

### 업그레이드 프로시저 테스트 {#testing-the-upgrade-procedure}

여기에 설명된 대로 업그레이드 절차는 사용자 지정된 실행 문서에 설명된 대로 개발 및 QA 환경에서 테스트되어야 합니다( 참조) [업그레이드 계획](/help/sites-deploying/upgrade-planning.md)). 업그레이드 실행 장부에 모든 단계가 기록되고 업그레이드 프로세스가 매끄럽게 수행될 때까지 업그레이드 절차를 반복해야 합니다.

### 구현 테스트 영역  {#implementation-test-areas-}

다음은 환경이 업그레이드되고 업그레이드된 코드 베이스가 배포되면 테스트 계획에서 적용해야 하는 AEM 구현의 중요한 영역입니다.

<table>
 <tbody>
  <tr>
   <td><strong>기능 테스트 영역</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>게시된 사이트</td>
   <td>게시 계층에서 AEM 구현 및 관련 코드 테스트<br /> Dispatcher를 통해 페이지 업데이트 및<br /> 캐시 무효화.</td>
  </tr>
  <tr>
   <td>작성</td>
   <td>작성자 계층에서 AEM 구현 및 관련 코드 테스트 페이지, 구성 요소 작성 및 대화 상자가 포함되어야 합니다.</td>
  </tr>
  <tr>
   <td>Experience Cloud 솔루션과 통합</td>
   <td>Analytics, DTM 및 Target과 같은 제품과의 통합 유효성을 검사합니다.</td>
  </tr>
  <tr>
   <td>타사 시스템과의 통합</td>
   <td>작성 계층과 게시 계층 모두에서 타사 통합의 유효성을 검사합니다.</td>
  </tr>
  <tr>
   <td>인증, 보안 및 권한</td>
   <td>LDAP/SAML과 같은 인증 메커니즘의 유효성을 검사해야 합니다.<br /> 권한 및 그룹은 작성자와 게시 모두에서 테스트되어야 합니다<br /> 계층.</td>
  </tr>
  <tr>
   <td>쿼리</td>
   <td>사용자 지정 인덱스 및 쿼리는 쿼리 성능과 함께 테스트해야 합니다.</td>
  </tr>
  <tr>
   <td>UI 사용자 지정</td>
   <td>작성 환경에서 AEM UI에 대한 모든 확장 또는 사용자 지정.</td>
  </tr>
  <tr>
   <td>워크플로</td>
   <td>사용자 지정 및/또는 즉시 사용 가능한 워크플로우 및 기능.</td>
  </tr>
  <tr>
   <td>성능 테스트</td>
   <td>로드 테스트는 실제 상황을 시뮬레이션하는 작성자 및 게시 계층 모두에서 수행해야 합니다.</td>
  </tr>
 </tbody>
</table>

### 문서 테스트 계획 및 결과 {#document-test-plan-and-results}

위의 구현 테스트 영역을 포함하는 테스트 계획을 만들어야 합니다. 종종 테스트 계획을 작성 및 게시 작업 목록별로 구분하는 것이 적절합니다. 이 테스트 계획은 프로덕션 환경을 업그레이드하기 전에 개발, QA 및 스테이지 환경에서 실행해야 합니다. 스테이지 및 프로덕션 환경을 업그레이드할 때 비교할 수 있도록 테스트 결과 및 성능 지표를 낮은 환경에서 캡처해야 합니다.
