---
title: 코드 및 사용자 정의 업그레이드
seo-title: 코드 및 사용자 정의 업그레이드
description: AEM에서 사용자 정의 코드를 업그레이드하는 방법에 대해 자세히 알아보십시오.
seo-description: AEM에서 사용자 정의 코드를 업그레이드하는 방법에 대해 자세히 알아보십시오.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: 업그레이드
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 0%

---


# 코드 및 사용자 지정 업그레이드{#upgrading-code-and-customizations}

업그레이드를 계획할 때 다음 구현 영역을 조사하고 해결해야 합니다.

* [코드 기준 업그레이드](#upgrade-code-base)
* [6.5 저장소 구조에 정렬](#align-repository-structure)
* [AEM 사용자 정의](#aem-customizations)
* [테스트 절차](#testing-procedure)

## 개요 {#overview}

1. **패턴**  탐지기 - 업그레이드 계획에 설명되어 있고  [이 페이지에 자세히 설명된 대로 패턴 탐지기](/help/sites-deploying/pattern-detector.md) 를 실행하여 AEM의 Target 버전에서 사용할 수 없는 API/번들뿐만 아니라 해결해야 하는 영역에 대한 자세한 내용을 포함하는 패턴 탐지 보고서를 받습니다. 패턴 감지 보고서는 코드에 비호환성 여부를 표시해야 합니다. 배포가 이미 6.5와 호환되는 소프트웨어가 없는 경우에도 6.5 기능을 활용하도록 새로운 개발을 선택할 수 있지만 호환성을 유지하기 위한 목적으로만 개발을 수행할 필요는 없습니다. 보고된 호환되지 않는 문제가 있는 경우 a) 호환성 모드에서 실행하고 새로운 6.5 기능 또는 호환성을 위해 개발을 연기하거나, b) 업그레이드 후 개발을 수행하고 2단계로 이동할 수 있습니다. 자세한 내용은 AEM 6.5](/help/sites-deploying/backward-compatibility.md)의 이전 버전과의 호환성을 참조하십시오.[

1. **6.5용 코드 베이스 개발 ** - Target 버전에 대한 코드 베이스에 대한 전용 분기 또는 저장소를 만듭니다. 업그레이드 전 호환성 정보를 사용하여 업데이트할 코드 영역을 계획합니다.
1. **6.5 Uber jar **로 컴파일 - 6.5 uber jar를 가리키고 코드를 이 항목에 대해 컴파일하려면 코드 기반 POM을 업데이트합니다.
1. **AEM 사용자 정의** 업데이트* - *AEM에 대한 모든 사용자 정의 또는 익스텐션은 6.5에서 작동하도록 업데이트/유효성이 검사되어야 하며 6.5 코드 베이스에 추가됩니다. UI 검색 Forms, 자산 사용자 지정, /mnt/overlay 사용 항목 포함

1. **6.5 환경에 배포**  - AEM 6.5(작성자 + 게시)의 깔끔한 인스턴스는 개발/QA 환경에 있어야 합니다. 업데이트된 코드 베이스와 현재 프로덕션에서 제공하는 대표적인 컨텐츠 샘플을 배포해야 합니다.
1. **QA 유효성 검사 및 버그 수정**  - QA가 작성자 및 게시 인스턴스 6.5에서 모두 애플리케이션의 유효성을 검사해야 합니다. 검색된 모든 버그를 수정하고 6.5 코드 베이스에 커밋해야 합니다. 모든 버그가 수정될 때까지 필요에 따라 Dev-Cycle을 반복합니다.

업그레이드를 진행하기 전에 AEM의 대상 버전에 대해 철저하게 테스트된 안정적인 애플리케이션 코드 베이스가 있어야 합니다. 테스트에 수행된 보고에 따라 사용자 지정 코드를 최적화하는 방법이 있을 수 있습니다. 저장소 탐색을 피하도록 코드를 리팩토링하거나, 검색을 최적화하기 위한 사용자 정의 색인 지정 또는 JCR에서 순서가 없는 노드를 다른 이름 중에서 사용하지 않도록 하는 등의 기능이 있을 수 있습니다.

코드 기준 및 사용자 지정을 업그레이드하여 새 AEM 버전으로 작업할 수 있는 옵션 외에도 6.5는 [이 페이지](/help/sites-deploying/backward-compatibility.md)에 설명된 대로 이전 버전과의 호환성 기능을 사용하여 사용자 지정을 보다 효율적으로 관리할 수 있도록 도와줍니다.

위에 언급되어 있고 아래 다이어그램에 표시된 것처럼, 첫 번째 단계에서 [패턴 탐지기](/help/sites-deploying/pattern-detector.md)를 실행하면 업그레이드의 전반적인 복잡성을 평가하고 호환성 모드에서 실행할지 또는 모든 새로운 AEM 6.5 기능을 사용하도록 사용자 지정을 업데이트할지 여부를 평가하는 데 도움이 됩니다. 자세한 내용은 [AEM 6.5](/help/sites-deploying/backward-compatibility.md)의 이전 호환성 페이지를 참조하십시오.
[ ![opt_cropped](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## 코드 기준 {#upgrade-code-base} 업그레이드

### 버전 제어 {#create-a-dedicated-branch-for-6.5-code-in-version-control}에서 6.5 코드에 대한 전용 분기 만들기

AEM 구현에 필요한 모든 코드 및 구성은 일부 버전 제어 형식을 사용하여 관리해야 합니다. AEM의 대상 버전에서 코드 베이스에 필요한 변경 사항을 관리하기 위해 버전 관리의 전용 분기를 만들어야 합니다. AEM의 대상 버전에 대한 코드 베이스의 반복적인 테스트 및 후속 버그 수정은 이 분기에서 관리됩니다.

### AEM Uber Jar 버전 {#update-the-aem-uber-jar-version} 업데이트

AEM Uber jar에는 Maven 프로젝트의 `pom.xml`에 단일 종속성으로 모든 AEM API가 포함되어 있습니다. 개별 AEM API 종속성을 포함하는 대신 Uber Jar를 단일 종속성으로 포함하는 것이 가장 좋습니다. 코드 베이스를 업그레이드할 때 Uber Jar 버전을 AEM의 대상 버전으로 가리키도록 변경해야 합니다. 프로젝트가 Uber Jar가 존재하기 전에 AEM 버전으로 개발된 경우 모든 개별 AEM API 종속성을 제거하고 AEM의 대상 버전에 대해 Uber Jar를 한 번 포함하여 대체해야 합니다. 그런 다음 새 버전의 Uber Jar에 대해 코드 베이스를 다시 컴파일해야 합니다. 가치가 떨어진 모든 API 또는 메서드를 AEM의 대상 버전과 호환되도록 업데이트해야 합니다.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 관리 리소스 확인자 위상 사용 {#phase-out-use-of-administrative-resource-resolver}

`SlingRepository.loginAdministrative()` 및 `ResourceResolverFactory.getAdministrativeResourceResolver()`을(를) 통한 관리 세션의 사용은 AEM 6.0 이전의 코드 베이스에서 매우 일반적입니다. 이러한 메서드는 너무 광범위한 액세스 수준을 제공하므로 보안상의 이유로 사용되지 않습니다. [이후 버전의 Sling에서는 이러한 메서드가 제거됩니다](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication). 서비스 사용자를 대신 사용하기 위해 모든 코드를 리팩터링하는 것이 좋습니다. 서비스 사용자 및 [관리 세션을 단계적으로 종료하는 방법에 대한 자세한 내용은 ](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions)에서 참조할 수 있습니다.

### 쿼리 및 Oak 인덱스 {#queries-and-oak-indexes}

코드 베이스를 업그레이드하기 위해 코드 베이스에 있는 모든 쿼리 사용을 철저히 테스트해야 합니다. Jackrabbit 2(6.0 이전 버전의 AEM)에서 업그레이드한 고객의 경우 Oak가 자동으로 컨텐츠를 색인화하지 않고 사용자 정의 인덱스를 만들어야 하므로 특히 중요합니다. AEM 6.x 버전에서 업그레이드하면 Oak 색인 정의가 변경되었을 수 있으며 기존 쿼리에 영향을 줄 수 있습니다.

쿼리 성능을 분석 및 검사하는 여러 도구를 사용할 수 있습니다.

* [AEM 색인 도구](/help/sites-deploying/queries-and-indexing.md)

* [작업 진단 도구 - 쿼리 성능](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [Oak Utils](https://oakutils.appspot.com/). Adobe에서 유지 관리되지 않는 오픈 소스 도구입니다.

### 클래식 UI 작성 {#classic-ui-authoring}

클래식 UI 작성은 여전히 AEM 6.5에서 사용할 수 있지만 더 이상 사용되지 않습니다. 자세한 내용은 [여기](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release)를 참조하십시오. 응용 프로그램이 현재 클래식 UI 작성 환경에서 실행 중인 경우 AEM 6.5로 업그레이드하고 클래식 UI를 계속 사용하는 것이 좋습니다. 그런 다음 터치 UI로의 마이그레이션을 개별 프로젝트로 계획하여 여러 개발 주기에 걸쳐 완료할 수 있습니다. AEM 6.5에서 클래식 UI를 사용하려면 코드 베이스에 커밋해야 할 여러 OSGi 구성이 있습니다. 구성 방법에 대한 자세한 내용은 [여기](/help/sites-administering/enable-classic-ui.md)를 참조하십시오.

## 6.5 저장소 구조에 정렬 {#align-repository-structure}

업그레이드를 보다 쉽게 하고 업그레이드 중에 구성을 덮어쓰지 않도록 저장소를 6.4에서 재구성하여 구성 콘텐츠와 분리합니다.

따라서 이전에 있었던 것처럼 여러 설정을 `/etc` 아래에 더 이상 있지 않게 이동해야 합니다. AEM 6.4로 업데이트한 내용을 검토하고 수용해야 하는 전체 저장소 구조 조정 문제를 검토하려면 AEM 6.4의 [리포지토리 재구성](/help/sites-deploying/repository-restructuring.md)을 참조하십시오.

## AEM 사용자 지정 {#aem-customizations}

AEM 소스 버전의 AEM 저작 환경에 대한 모든 사용자 정의 설정을 식별해야 합니다. 식별된 각 사용자 정의 설정은 버전 제어에 저장되거나 컨텐츠 패키지의 일부로 최소한 백업되는 것이 좋습니다. 모든 사용자 정의는 프로덕션 업그레이드 전에 AEM의 대상 버전을 실행하는 QA 또는 스테이징 환경에서 배포하고 검증해야 합니다.

### 일반 {#overlays-in-general}의 오버레이

/apps 아래의 추가 노드가 있는 /libs 아래에 있는 노드 및/또는 파일을 오버레이하여 AEM 기능을 확장할 수 있는 일반적인 방법입니다. 이러한 오버레이는 버전 제어에서 추적되고 AEM의 대상 버전에 대해 테스트되어야 합니다. 파일(JS, JSP, HTL 등)이 오버레이된 경우, AEM의 대상 버전에서 회귀 테스트를 더 쉽게 하기 위해 어떤 기능이 보강되었는지에 대한 주석을 남겨 두는 것이 좋습니다. 일반적으로 오버레이에 대한 자세한 내용은 [여기](/help/sites-developing/overlays.md)를 참조하십시오. 특정 AEM 오버레이에 대한 지침은 아래에 나와 있습니다.

### 사용자 지정 검색 Forms {#upgrading-custom-search-forms} 업그레이드

사용자 지정 검색 패싯을 사용하려면 업그레이드 후 몇 가지 수동 조정이 필요합니다. 자세한 내용은 [사용자 정의 검색 Forms 업그레이드](/help/sites-deploying/upgrading-custom-search-forms.md)를 참조하십시오.

### 자산 UI 사용자 지정 {#assets-ui-customizations}

>[!NOTE]
>
>이 절차는 AEM 6.2 이전 버전에서 업그레이드하는 경우에만 필요합니다.

자산 배포를 사용자 정의한 인스턴스는 업그레이드를 준비해야 합니다. 이는 사용자 지정된 모든 컨텐츠가 새로운 6.4 노드 구조와 호환되도록 하는 데 필요합니다.

다음을 수행하여 자산 UI에 대한 사용자 지정을 준비할 수 있습니다.

1. 업그레이드해야 하는 인스턴스에서 *https://server:port/crx/de/index.jsp*&#x200B;으로 이동하여 CRXDE Lite을 엽니다.

1. 다음 노드로 이동합니다.

   * `/apps/dam/content`

1. 콘텐트 노드의 이름을 **content_backup**&#x200B;으로 바꿉니다. 창의 왼쪽에 있는 탐색기 창을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**&#x200B;를 선택하면 이 작업을 수행할 수 있습니다.

1. 노드의 이름이 변경되었으면 `/apps/dam` 아래에 **content**&#x200B;라는 이름의 새 노드를 만들고 해당 노드 유형을 **sling:Folder**&#x200B;로 설정합니다.

1. **content_backup**&#x200B;의 모든 하위 노드를 새로 만든 콘텐트 노드로 이동합니다. 탐색기 창에서 각 하위 노드를 마우스 오른쪽 단추로 클릭하고 **이동**&#x200B;을 선택하면 이 작업을 수행할 수 있습니다.

1. **content_backup** 노드를 삭제합니다.

1. 올바른 노드 유형이 `sling:Folder`인 `/apps/dam` 아래에 업데이트된 노드는 버전 제어에 저장되고 코드 베이스 또는 컨텐츠 패키지로 백업된 최소 크기로 배포되어야 합니다.

### 기존 자산에 대한 자산 ID 생성 {#generating-asset-ids-for-existing-assets}

기존 자산에 대한 자산 ID를 생성하려면 AEM 인스턴스를 업그레이드하여 AEM 6.5를 실행할 수 있도록 자산을 업그레이드하십시오. [자산 인사이트 기능](/help/assets/asset-insights.md)을(를) 활성화하려면 이 작업이 필요합니다. 자세한 내용은 [포함 코드 추가](/help/assets/use-page-tracker.md#add-embed-code)를 참조하십시오.

자산을 업그레이드하려면 JMX 콘솔에서 자산 ID 연결 패키지를 구성합니다. 저장소의 자산 수에 따라 `migrateAllAssets`이(가) 시간이 오래 걸릴 수 있습니다. 우리의 내부 테스트는 TarMK에 있는 125,000개의 자산에 대해 대략 한 시간 가량 측정됩니다.

![1487758945977](assets/1487758945977.png)

전체 자산의 하위 세트에 대해 자산 ID가 필요한 경우 `migrateAssetsAtPath` API를 사용하십시오.

기타 모든 목적으로 `migrateAllAssets()` API를 사용하십시오.

### InDesign 스크립트 사용자 지정 {#indesign-script-customizations}

Adobe은 사용자 정의 스크립트를 `/apps/settings/dam/indesign/scripts` 위치에 놓는 것이 좋습니다. InDesign 스크립트 사용자 지정에 대한 자세한 내용은 [여기](/help/assets/indesign.md#configuring-the-aem-assets-workflow)를 참조하십시오.

### ContextHub 구성 복구 중 {#recovering-contexthub-configurations}

ContextHub 구성은 업그레이드의 영향을 받습니다. 기존 ContextHub 구성을 복구하는 방법에 대한 지침은 [여기](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading)에 있습니다.

### 워크플로 사용자 지정 {#workflow-customizations}

필요하지 않은 기능을 추가하거나 제거하기 위해 즉시 수정 워크플로우를 업데이트하는 것이 일반적인 방법입니다. 사용자 지정된 일반적인 워크플로우는 [!UICONTROL DAM 자산 업데이트] 워크플로입니다. 사용자 정의 구현에 필요한 모든 워크플로우는 업그레이드 중에 덮어쓰여질 수 있으므로 백업되고 버전 제어에 저장해야 합니다.

### 편집 가능한 템플릿 {#editable-templates}

>[!NOTE]
>
>이 절차는 AEM 6.2에서 편집 가능한 템플릿을 사용하는 사이트 업그레이드에만 필요합니다.

편집 가능한 템플릿의 구조가 AEM 6.2와 6.3 사이에 변경되었습니다. 6.2 이전 버전에서 업그레이드하는 경우 사이트 컨텐츠가 편집 가능한 템플릿을 사용하여 빌드된 경우 [응답형 노드 정리 도구](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration)를 사용해야 합니다. 이 도구는 콘텐트를 정리하기 위해 **after** 업그레이드를 실행하도록 되어 있습니다. 작성자 및 게시 계층 모두에서 실행되어야 합니다.

### CUG 구현 변경 사항 {#cug-implementation-changes}

이전 버전의 AEM에서 성능 및 확장성 제한을 해결하기 위해 닫힌 사용자 그룹 구현이 크게 변경되었습니다. 이전 버전의 CUG는 6.3에서 더 이상 사용되지 않으며 새 구현은 터치 UI에서만 지원됩니다. 6.2 이상에서 업그레이드하는 경우 새 CUG 구현으로 마이그레이션하기 위한 지침은 [여기](/help/sites-administering/closed-user-groups.md#upgradetoaem63)에 있습니다.

## 테스트 절차 {#testing-procedure}

업그레이드 테스트를 위한 포괄적인 테스트 계획을 준비해야 합니다. 업그레이드된 코드 베이스와 애플리케이션을 먼저 낮은 환경에서 테스트해야 합니다. 발견된 모든 버그는 코드 베이스가 안정될 때까지 반복적인 방식으로 수정되어야 하며, 그 이후에야 더 높은 수준의 환경을 업그레이드해야 합니다.

### 업그레이드 절차 테스트 {#testing-the-upgrade-procedure}

여기에 설명된 대로 업그레이드 절차는 사용자 정의된 실행 장부에 설명된 대로 개발 및 QA 환경에 대해 테스트되어야 합니다([업그레이드 계획](/help/sites-deploying/upgrade-planning.md) 참조). 업그레이드 실행 설명서에 모든 단계가 기록되고 업그레이드 프로세스가 원활하게 진행될 때까지 업그레이드 절차를 반복해야 합니다.

### 구현 테스트 영역 {#implementation-test-areas-}

다음은 환경이 업그레이드되고 업그레이드된 코드 베이스가 배포되면 테스트 계획의 적용을 받아야 하는 AEM 구현의 중요한 영역입니다.

<table>
 <tbody>
  <tr>
   <td><strong>기능 테스트 영역</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>게시된 사이트</td>
   <td>디스패처를 통해 게시 계층<br />에서 AEM 구현 및 관련 코드를 테스트합니다. 페이지 업데이트 및 <br /> 캐시 무효화에 대한 기준을 포함해야 합니다.</td>
  </tr>
  <tr>
   <td>작성</td>
   <td>작성자 계층에서 AEM 구현 및 관련 코드를 테스트합니다. 페이지, 구성 요소 작성 및 대화 상자를 포함해야 합니다.</td>
  </tr>
  <tr>
   <td>Marketing Cloud 솔루션과의 통합</td>
   <td>Analytics, DTM 및 Target과 같은 제품과의 통합 유효성을 검사합니다.</td>
  </tr>
  <tr>
   <td>타사 시스템과의 통합</td>
   <td>모든 타사 통합은 작성자 및 게시 계층 모두에서 유효성이 검사되어야 합니다.</td>
  </tr>
  <tr>
   <td>인증, 보안 및 권한</td>
   <td>LDAP/SAML과 같은 모든 인증 메커니즘의 유효성을 검사해야 합니다.<br /> 권한 및 그룹은 작성자 및 게시 계층 모두에서 테스트되어야 <br /> 합니다.</td>
  </tr>
  <tr>
   <td>쿼리</td>
   <td>사용자 지정 색인 및 쿼리는 쿼리 성능과 함께 테스트해야 합니다.</td>
  </tr>
  <tr>
   <td>UI 사용자 지정</td>
   <td>작성 환경에서 AEM UI에 대한 모든 확장 또는 사용자 정의.</td>
  </tr>
  <tr>
   <td>워크플로우</td>
   <td>사용자 정의 및/또는 즉시 사용 가능한 워크플로우 및 기능</td>
  </tr>
  <tr>
   <td>성능 테스트</td>
   <td>실제 시나리오를 시뮬레이션하는 작성자 및 게시 계층 모두에서 로드 테스트를 수행해야 합니다.</td>
  </tr>
 </tbody>
</table>

### 문서 테스트 계획 및 결과 {#document-test-plan-and-results}

위의 구현 테스트 영역을 포함하는 테스트 계획을 만들어야 합니다. 대부분의 경우 작성자 및 게시 작업 목록별로 테스트 계획을 구분하는 것이 적절합니다. 이 테스트 계획은 프로덕션 환경을 업그레이드하기 전에 개발, QA 및 스테이지 환경에서 실행해야 합니다. 스테이지 및 프로덕션 환경을 업그레이드할 때 비교할 수 있도록 낮은 환경에서 테스트 결과와 성능 지표를 캡처해야 합니다.
