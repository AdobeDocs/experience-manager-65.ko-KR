---
title: 업그레이드 후 확인 및 문제 해결
seo-title: 업그레이드 후 확인 및 문제 해결
description: 업그레이드 후 발생할 수 있는 문제를 해결하는 방법을 알아봅니다.
seo-description: 업그레이드 후 발생할 수 있는 문제를 해결하는 방법을 알아봅니다.
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 0%

---


# 업그레이드 후 확인 및 문제 해결{#post-upgrade-checks-and-troubleshooting}

## 업그레이드 후 검사 {#post-upgrade-checks}

[In-Place 업그레이드](/help/sites-deploying/in-place-upgrade.md)에 따라 업그레이드를 완료하기 위해 다음 활동을 실행해야 합니다. 6.5 jar로 AEM이 시작되었으며 업그레이드된 코드 베이스가 배포되었다고 가정합니다.

* [업그레이드 성공 로그 확인](#main-pars-header-290365562)

* [OSGi 번들 확인](#main-pars-header-1637350649)

* [Oak 버전 확인](#main-pars-header-1293049773)

* [PreUpgradeBackup 폴더 Inspect](#main-pars-header-988995987)

* [페이지의 초기 유효성 검사](#main-pars-header-20827371)
* [AEM 서비스 팩 적용](#main-pars-header-215142387)

* [AEM 기능 마이그레이션](#main-pars-header-1434457709)

* [예약된 유지 관리 구성 확인](#main-pars-header-1552730183)

* [복제 에이전트 사용](#main-pars-header-823243751)

* [사용자 지정 예약 작업 활성화](#main-pars-header-244535083)

* [테스트 계획 실행](#main-pars-header-1167972233)

### 업그레이드 성공 로그 확인 {#verify-logs-for-upgrade-success}

**upgrade.log**

이전에는 인스턴스의 업그레이드 후 상태를 검사하기 위해 다양한 로그 파일, 저장소의 일부 및 실행 패드에 대해 신중하게 검사해야 했습니다. 업그레이드 후 보고서를 생성하면 라이브하기 전에 결함이 있는 업그레이드를 감지할 수 있습니다.

이 기능의 주요 목적은 업그레이드의 성공을 검증하는 데 필요한 여러 엔드포인트에서 수동 해석 또는 복잡한 구문 분석 로직을 줄이는 것입니다. 이 솔루션은 외부 자동화 시스템이 성공이나 업데이트의 확인된 실패에 반응하도록 하기 위해 모호한 정보를 제공하는 것을 목표로 합니다.

보다 구체적으로 다음을 보장합니다.

* 업그레이드 프레임워크에서 감지한 업그레이드 실패가 단일 업그레이드 보고서에서 중앙 집중화할 수 있습니다.
* 업그레이드 보고서에는 필요한 수동 개입에 대한 지표가 포함되어 있습니다.

이를 수용하기 위해 `upgrade.log` 파일에서 로그가 생성되는 방식을 변경했습니다.

다음은 업그레이드 중 오류가 발생하지 않는 샘플 보고서입니다.

![148787443006](assets/1487887443006.png)

다음은 업그레이드 프로세스 동안 설치되지 않은 번들을 보여주는 예제 보고서입니다.

![148787532730](assets/1487887532730.png)

**error.log**

target 버전 jar를 사용하여 AEM을 시작하는 동안 그리고 다음에 error.log를 신중하게 검토해야 합니다. 경고나 오류는 검토해야 합니다. 일반적으로 로그를 시작할 때 문제를 찾는 것이 가장 좋습니다. 나중에 로그에서 발생하는 오류는 사실 파일에서 초기에 호출된 근본 문제의 부작용일 수 있습니다. [업그레이드](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade)에 대한 거듭된 오류와 경고가 발생하는 경우 아래를 참조하십시오.

### OSGi 번들 확인 {#verify-osgi-bundles}

OSGi 콘솔 `/system/console/bundles`로 이동하여 번들이 시작되지 않았는지 확인합니다. 번들이 설치된 상태인 경우 루트 문제를 확인하려면 `error.log`에 문의하십시오.

### Oak 버전 확인 {#verify-oak-version}

업그레이드 후에 Oak 버전이 **1.10.2**&#x200B;로 업데이트되었습니다. Oak 버전을 확인하려면 OSGi 콘솔로 이동하고 Oak 번들과 연결된 버전을 확인합니다.Oak Core, Oak Commons, Oak Segment Tar.

### Inspect PreUpgradeBackup 폴더 {#inspect-preupgradebackup-folder}

업그레이드 동안 AEM에서 사용자 지정 항목을 백업하고 `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>` 아래에 저장합니다. CRXDE Lite에서 이 폴더를 보려면 [CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md)을(를) 일시적으로 활성화해야 할 수 있습니다.

타임스탬프가 있는 폴더에는 `mergeStatus`이라는 이름의 값이 `COMPLETED`이어야 합니다. **to-process** 폴더는 비어 있어야 하며 **overwrite** 노드는 업그레이드 동안 덮어쓴 노드를 나타냅니다. **furites** 노드 아래의 콘텐트는 업그레이드 중 안전하게 병합할 수 없는 콘텐트를 나타냅니다. 구현이 업그레이드된 코드 패키지에 의해 아직 설치되지 않은 하위 노드에 종속되어 있는 경우 수동으로 병합해야 합니다.

스테이지 또는 프로덕션 환경에서 이 연습 다음의 CRXDE Lite을 비활성화합니다.

### 페이지 {#initial-validation-of-pages}의 초기 유효성 검사

AEM의 여러 페이지에 대해 초기 유효성 검사를 수행합니다. 작성 환경을 업그레이드하는 경우 시작 페이지 및 시작 페이지( `/aem/start.html`, `/libs/cq/core/content/welcome.html`)가 열립니다. 작성자 및 게시 환경 모두에서 몇 개의 애플리케이션 페이지를 열고 올바르게 렌더링되는 테스트를 실행합니다. 문제가 발생하면 `error.log`에 문의하여 문제를 해결하십시오.

### AEM 서비스 팩 적용 {#apply-aem-service-packs}

관련 AEM 6.5 서비스 팩을 출시한 경우 적용합니다.

### AEM 기능 마이그레이션 {#migrate-aem-features}

AEM의 여러 기능에는 업그레이드 후 추가 단계가 필요합니다. AEM 6.5에서 마이그레이션하기 위한 이러한 기능 및 단계의 전체 목록은 [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md) 페이지에서 확인할 수 있습니다.

### 예약된 유지 관리 구성 확인 {#verify-scheduled-maintenance-configurations}

#### 데이터 저장소 가비지 컬렉션 사용 {#enable-data-store-garbage-collection}

파일 데이터 저장소를 사용하는 경우 데이터 저장소 가비지 수집 작업이 활성화되고 주별 유지 관리 목록에 추가되어 있는지 확인합니다. 지침은 [여기](/help/sites-administering/data-store-garbage-collection.md)에 요약되어 있습니다.

>[!NOTE]
>
>이는 S3 사용자 지정 데이터 저장소 설치 또는 공유 데이터 저장소 사용 시 권장되지 않습니다.

#### 온라인 개정 정리 사용 {#enable-online-revision-cleanup}

MongoMK 또는 새로운 TarMK 세그먼트 형식을 사용하는 경우, 개정 정리 작업이 활성화되고 일별 유지 관리 목록에 추가되는지 확인합니다. 지침은 [여기](/help/sites-deploying/revision-cleanup.md)에 요약되어 있습니다.

### 테스트 계획 실행 {#execute-test-plan}

**테스트 프로시저** 섹션 아래에 정의된 [업그레이드 코드 및 사용자 지정](/help/sites-deploying/upgrading-code-and-customizations.md)에 대해 자세한 테스트 계획을 실행합니다.

### 복제 에이전트 사용 {#enable-replication-agents}

게시 환경이 완전히 업그레이드되고 검증되면 작성 환경에서 복제 에이전트를 활성화합니다. 에이전트가 각 게시 인스턴스에 연결할 수 있는지 확인합니다. 이벤트 순서에 대한 자세한 내용은 [업그레이드 프로시저](/help/sites-deploying/upgrade-procedure.md)를 참조하십시오.

### 사용자 지정 예약 작업 사용 {#enable-custom-scheduled-jobs}

이 시점에서 코드 베이스의 일부로 예약된 작업을 활성화할 수 있습니다.

## 업그레이드 {#analyzing-issues-with-upgrade} 관련 문제 분석

이 섹션에는 AEM 6.3으로 업그레이드 절차를 따라 발생할 수 있는 몇 가지 문제 시나리오가 포함되어 있습니다.

이러한 시나리오는 업그레이드와 관련된 문제의 근본 원인을 추적하는 데 도움이 되며 프로젝트 또는 제품별 문제를 식별하는 데 도움이 됩니다.

### 저장소 마이그레이션 실패 {#repository-migration-failing-}

CRX2에서 Oak로 데이터 마이그레이션은 CQ 5.4를 기반으로 소스 인스턴스로 시작하는 모든 시나리오에 대해 실행할 수 있어야 합니다. `repository.xml`의 준비를 포함하는 이 문서의 업그레이드 지침을 정확하게 따르고 JAAS를 통해 사용자 정의 인증자가 시작되지 않고 인스턴스가 마이그레이션을 시작하기 전에 불일치를 확인했는지 확인하십시오.

마이그레이션이 여전히 실패할 경우 `upgrade.log`을 검사하여 근본 원인을 파악할 수 있습니다. 문제가 아직 알려지지 않은 경우 고객 지원에 보고하십시오.

### 업그레이드가 {#the-upgrade-did-not-run}을(를) 실행하지 않았습니다.

준비 단계를 시작하기 전에 먼저 java -jar aem-quickstart.jar 명령을 사용하여 **source** 인스턴스를 실행하여 실행해야 합니다. quickstart.properties 파일이 제대로 생성되는지 확인하려면 이 값이 필요합니다. 없는 경우 업그레이드가 작동하지 않습니다. 또는 소스 인스턴스의 설치 폴더에서 `crx-quickstart/conf` 아래를 보면서 파일이 있는지 확인할 수 있습니다. 또한 AEM을 시작하여 업그레이드를 시작할 때 java -jar aem-quickstart.jar 명령을 사용하여 실행해야 합니다. 시작 스크립트에서 시작하는 것은 업그레이드 모드에서 AEM을 시작하지 않습니다.

### 패키지 및 번들을 업데이트하지 못했습니다. {#packages-and-bundles-fail-to-update-}

업그레이드 중 패키지가 설치되지 않는 경우, 패키지에 포함된 번들 중 하나만 업데이트되지는 않습니다. 이 문제 카테고리는 일반적으로 데이터 저장소 구성이 잘못되어 발생합니다. 또한 error.log에 **ERROR** 및 **WARN** 메시지로 나타납니다. 대부분의 경우 기본 로그인이 작동하지 않을 수 있으므로 구성 문제를 검사하고 찾기 위해 CRXDE를 직접 사용할 수 있습니다.

### 일부 AEM 번들이 활성 상태 {#some-aem-bundles-are-not-switching-to-the-active-state}로 전환되지 않습니다.

번들이 시작되지 않을 경우 충족되지 않은 종속성을 확인해야 합니다.

이 문제가 있는 경우, 이 문제는 업그레이드가 되지 않는 번들 제품을 만드는 실패한 패키지 설치를 기반으로 합니다. 이 경우 새로운 버전에 호환되지 않는 것으로 간주됩니다. 이 문제를 해결하는 방법에 대한 자세한 내용은 위의 **패키지 및 번들 업데이트 실패**&#x200B;를 참조하십시오.

업그레이드되지 않은 번들을 감지하려면 새 AEM 6.5 인스턴스의 번들 목록을 업그레이드된 인스턴스와 비교하는 것이 좋습니다. 그러면 `error.log`에서 검색할 항목의 범위가 더 가깝게 표시됩니다.

### 활성 상태 {#custom-bundles-not-switching-to-the-active-state}으로 전환되지 않은 사용자 지정 번들

사용자 지정 번들이 활성 상태로 전환되지 않는 경우 변경 API를 가져오지 않는 코드가 있을 수 있습니다. 이것은 종종 충족되지 않은 의존성을 초래합니다.

제거된 API는 이전 릴리스 중 하나에서 더 이상 사용되지 않는 것으로 표시되어야 합니다. 이 사용 중단 알림에서 직접 코드 마이그레이션에 대한 지침을 찾을 수 있습니다. Adobe은 버전이 변경 사항을 표시할 수 있도록 가능한 의미 체계 버전 지정을 목표로 합니다.

문제를 일으킨 변경이 절대적으로 필요한지, 그렇지 않다면 되돌릴 수도 있다. 또한 엄격한 의미 체계 버전 관리를 통해 패키지 내보내기의 버전 증가가 필요 이상으로 증가했는지 확인하십시오.

### 잘못된 플랫폼 UI {#malfunctioning-platform-ui}

업그레이드 후 제대로 작동하지 않는 특정 UI 기능의 경우 먼저 인터페이스의 사용자 지정 오버레이를 확인해야 합니다. 일부 구조가 변경되었을 수 있으며 오버레이에 업데이트가 필요하거나 더 이상 사용되지 않습니다.

다음으로 클라이언트 라이브러리에 연결된 사용자 정의 추가 확장 프로그램으로 추적할 수 있는 Javascript 오류를 확인합니다. AEM 레이아웃에 문제를 일으킬 수 있는 사용자 지정 CSS에도 동일하게 적용할 수 있습니다.

마지막으로 Javascript에서 처리할 수 없는 구성 오류를 확인하십시오. 일반적으로 비활성화된 익스텐션이 부적절하게 있는 경우입니다.

### 사용자 지정 구성 요소, 템플릿 또는 UI 확장 기능 {#malfunctioning-custom-components-templates-or-ui-extensions}

대부분의 경우 이러한 문제의 근본 원인은 시작되지 않은 번들 또는 처음 구성 요소를 사용할 때 발생되는 문제점과 함께 설치되지 않은 패키지의 경우와 동일합니다.

잘못된 사용자 지정 코드를 처리하는 방법은 먼저 연기 테스트를 수행하여 원인을 확인하는 것입니다. 찾은 경우 아티클의 [link] 섹션에 있는 권장 사항을 참조하여 수정할 수 있습니다.

### /etc {#missing-customizations-under-etc}에 사용자 지정 없음

`/apps` 업그레이드 `/libs` 를 통해 원활하게 처리되지만 업그레이드  `/etc` 후 변경 사항을 수동으로 복원해야  `/var/upgrade/PreUpgradeBackup` 할 수 있습니다. 수동으로 병합해야 하는 컨텐츠는 이 위치를 확인하십시오.

### error.log 및 upgrade.log {#analyzing-the-error.log-and-upgrade.log} 분석

대부분의 경우 문제의 원인을 찾기 위해 로그에 오류가 있는지 확인해야 합니다. 그러나 업그레이드 시 이전 번들이 제대로 업그레이드되지 않을 수 있으므로 종속성 문제를 모니터링해야 합니다.

가장 좋은 방법은 해당 문제와 관련이 없을 것으로 예상되는 모든 메시지를 제거하여 error.log를 제거하는 것입니다. grep와 같은 도구를 사용하여 다음을 수행할 수 있습니다.

```shell
grep -v UnrelatedErrorString
```

일부 오류 메시지는 즉시 설명되지 않을 수 있습니다. 이 경우 오류가 발생한 컨텍스트를 보면 오류가 발생한 위치를 이해하는 데에도 도움이 됩니다. 다음을 사용하여 오류를 분리할 수 있습니다.

* `grep -B` 를 참조하십시오.

또는

* `grep -A` 을 참조하십시오.

이 상태로 이어지는 유효한 사례가 있을 수 있고 응용 프로그램이 실제 오류인지 확인할 수 없기 때문에 일부 경우 WARN 메시지도 찾을 수 있습니다. 이 메시지들도 반드시 참고하세요.

### Adobe 지원 문의 {#contacting-adobe-support}

이 페이지의 충고에 따라 계속 문제가 표시되는 경우 Adobe 지원 센터에 문의하십시오. 해당 케이스에 종사하는 지원 엔지니어에게 가능한 많은 정보를 제공하려면 업그레이드의 upgrade.log 파일을 포함해야 합니다.
