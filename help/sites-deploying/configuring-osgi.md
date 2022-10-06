---
title: OSGi 구성
seo-title: Configuring OSGi
description: OSGi는 Adobe Experience Manager(AEM)의 기술 스택에서 기본적인 요소입니다. AEM의 복합 번들과 해당 구성을 제어하는 데 사용됩니다. 이 문서에서는 이러한 번들에 대한 구성 설정을 관리하는 방법을 자세히 설명합니다.
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---

# OSGi 구성{#configuring-osgi}

[OSGi](https://www.osgi.org/) 는 AEM(Adobe Experience Manager)의 기술 스택에서 기본적인 요소입니다. AEM의 복합 번들과 해당 구성을 제어하는 데 사용됩니다.

OSGi &quot;*작은 구성 요소, 재사용 가능한 공동 작업 구성 요소에서 응용 프로그램을 구축할 수 있도록 하는 표준화된 프리미티브(primitives)를 제공합니다. 이러한 구성 요소는 응용 프로그램으로 작성하고 배포할 수 있습니다*&quot;.

따라서 개별적으로 시작, 중지, 설치 및 설치가 가능하므로 번들을 쉽게 관리할 수 있습니다. 상호 종속성은 자동으로 처리됩니다. 각 OSGi 구성 요소( [OSGi 사양](https://www.osgi.org/Specifications/HomePage))은 다양한 번들 중 하나에 포함되어 있습니다.

다음 방법 중 하나로 이러한 번들에 대한 구성 설정을 관리할 수 있습니다.

* 사용 [Adobe CQ 웹 콘솔](#osgi-configuration-with-the-web-console)
* 사용 [구성 파일](#osgi-configuration-with-configuration-files)
* 구성 [content-nodes( `sling:OsgiConfig`) 내의 아무 곳에나 삽입할 수 있습니다.](#osgi-configuration-in-the-repository)

두 방법 중 하나는 주로 와 관련하여 미묘한 차이가 있더라도 사용할 수 있습니다 [실행 모드](/help/sites-deploying/configure-runmodes.md):

* [Adobe CQ 웹 콘솔](#osgi-configuration-with-the-web-console)

   * 웹 콘솔은 OSGi 구성을 위한 표준 인터페이스입니다. 미리 정의된 목록에서 가능한 값을 선택할 수 있는 다양한 속성을 편집하는 UI를 제공합니다.

      따라서 가장 사용하기 쉬운 방법입니다.

   * 웹 콘솔로 만든 모든 구성은 현재 실행 모드나 실행 모드에 대한 후속 변경 사항에 관계없이 즉시 적용되어 현재 인스턴스에 적용됩니다.

* [구성 파일](#osgi-configuration-with-configuration-files)

   * 웹 콘솔에 정의된 설정을 포함합니다.
   * 다른 인스턴스에서 사용할 컨텐츠 패키지에 포함할 수 있습니다.

* [저장소의 content-nodes(sling:osgiConfig)](#osgi-configuration-in-the-repository)

   * 이를 위해서는 CRXDE Lite을 사용한 수동 구성이 필요합니다.
   * 의 이름 지정 규칙 때문에 `sling:OsgiConfig` 노드, 특정 [실행 모드](/help/sites-deploying/configure-runmodes.md). 동일한 저장소에서 두 개 이상의 실행 모드에 대한 구성을 저장할 수도 있습니다.
   * 모든 적절한 구성이 즉시 적용됩니다(실행 모드에 따라 다름).

어떤 방법을 사용하든 다음 구성 방법을 모두 사용합니다.

* 저장소 컨텐츠를 복사하거나 복제하면 동일한 구성이 다시 작성되는지 확인합니다.
* FileVault 또는 Subversion에 대한 구성을 체크 아웃할 수 있습니다. 보안 또는 추가 업데이트를 위해 사용합니다.
* 다른 인스턴스를 설정할 때 사용할 패키지에 저장할 수 있습니다.
* 스크립트를 사용하여 구성 롤아웃을 수행하여 구성 세부 사항을 전달할 수 있습니다.

>[!NOTE]
>
>특정 중요 설정에 대한 세부 정보는 [OSGi 구성 설정.](/help/sites-deploying/osgi-configuration-settings.md)

## 웹 콘솔을 사용한 OSGi 구성 {#osgi-configuration-with-the-web-console}

다음 [웹 콘솔](/help/sites-deploying/web-console.md) AEM에서 번들 구성을 위한 표준화된 인터페이스를 제공합니다. 다음 **구성** 탭은 OSGi 번들을 구성하는 데 사용되며, 따라서 AEM 시스템 매개 변수를 구성하는 기본 메커니즘입니다.

변경한 사항이 해당 OSGi 구성에 즉시 적용되므로 다시 시작할 필요가 없습니다.

>[!NOTE]
>
>웹 콘솔에서 수행된 변경 내용은 [구성 파일](#osgi-configuration-with-configuration-files). 이러한 구성 요소는 추가 설치에서 다시 사용할 수 있도록 컨텐츠 패키지에 포함할 수 있습니다.

>[!NOTE]
>
>웹 콘솔에서 Sling 기본값과 관련된 기본 설정을 언급하는 설명이 있습니다.
>
>Adobe Experience Manager에는 자체 기본값이 있으므로 기본값 세트가 콘솔에 설명된 것과 다를 수 있습니다.

웹 콘솔로 구성을 업데이트하는 방법:

1. 액세스 권한 **구성** 다음 방법 중 하나로 웹 콘솔 탭

   * 의 링크에서 웹 콘솔 열기 **도구 -> 작업** 메뉴 아래의 제품에서 사용할 수 있습니다. 콘솔에 로그인하면 다음과 같은 드롭다운 메뉴를 사용할 수 있습니다.

      **OSGi >**

   * 직접 URL; 예:

      `http://localhost:4502/system/console/configMgr`
   목록이 표시됩니다.

1. 다음 방법 중 하나로 구성할 번들을 선택합니다.

   * 을(를) 클릭합니다. **편집** 해당 번들의 아이콘
   * 을(를) 클릭합니다. **이름** 번들

1. 대화 상자가 열립니다. 필요에 따라 편집할 수 있습니다. 예를 들어 **로그 수준** to `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >업데이트는 다음과 같이 저장소에 저장됩니다. [구성 파일](#osgi-configuration-with-configuration-files). 나중에 이러한 ID를 찾으려면(예: 다른 인스턴스에서 사용할 컨텐츠 패키지에 포함되도록) 영구 ID( `PID`).

1. **저장**&#x200B;을 클릭합니다.

   변경 사항은 실행 중인 시스템의 관련 OSGi 구성에 즉시 적용되므로 다시 시작할 필요가 없습니다.

   >[!NOTE]
   >
   >이제 관련 항목을 찾을 수 있습니다 [구성 파일](#osgi-configuration-with-configuration-files); 예를 들어 다른 인스턴스에서 사용할 컨텐츠 패키지에 를 포함하도록 하십시오.

## 구성 파일이 있는 OSGi 구성 {#osgi-configuration-with-configuration-files}

웹 콘솔을 사용하여 수행한 구성 변경 사항은 저장소에 구성 파일( `.config`) 아래의 를 참조하십시오.

`/apps`

이러한 구성 요소는 컨텐츠 패키지에 포함할 수 있으며 다른 인스턴스에서 다시 사용할 수 있습니다.

>[!NOTE]
>
>구성 파일의 형식은 매우 구체적입니다. 자세한 내용은 [Sling Apache 설명서](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) 자세한 내용
>
>이러한 이유로 웹 콘솔에서 실제 변경 작업을 수행하여 구성 파일을 만들고 유지 관리하는 것이 좋습니다.

웹 콘솔에는 변경 사항이 저장되었다는 표시가 없지만 쉽게 찾을 수 있습니다.

1. 다음 방법으로 구성 파일 만들기 [웹 콘솔에서 초기 변경](#osgi-configuration-with-the-web-console).
1. CRXDE Lite을 엽니다.
1. 에서 **도구** 메뉴 선택 **쿼리...** .
1. 쿼리 제출 **유형** `SQL` 업데이트한 구성의 PID를 검색하려면 다음을 수행하십시오.

   예, **Apache Felix OSGi Management Console** 에는 다음의 영구 ID(PID)가 있습니다.

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   따라서 SQL 쿼리는 다음과 같습니다.

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 구성 파일 노드가 표시됩니다.

   위의 예:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >이 파일을 열어 변경 사항을 볼 수 있지만 입력 오류를 방지하려면 콘솔을 사용하여 실제 변경 작업을 수행하는 것이 좋습니다.

1. 이제 이 노드를 포함하는 컨텐츠 패키지를 만들고 다른 인스턴스에서 필요에 따라 사용할 수 있습니다.

## 저장소의 OSGi 구성 {#osgi-configuration-in-the-repository}

웹 콘솔을 사용하는 것 외에도, 리포지토리에서 구성 세부 사항을 정의할 수도 있습니다. 이렇게 하면 다른 실행 모드를 쉽게 구성할 수 있습니다.

이러한 구성은 `sling:OsgiConfig` 시스템이 참조할 저장소의 노드입니다. 이러한 노드는 OSGi 구성을 미러링하고 사용자 인터페이스를 구성합니다. 구성 데이터를 업데이트하려면 노드 속성을 업데이트합니다.

저장소에서 구성 데이터를 수정하는 경우 해당 유효성 검사 및 일관성 검사를 통해 웹 콘솔을 사용하여 변경한 것처럼 변경 사항이 관련 OSGi 구성에 즉시 적용됩니다. 구성 복사 작업에도 적용됩니다. `/libs/` to `/apps/`.

동일한 구성 매개 변수가 여러 위치에 있을 수 있으므로 시스템은 다음과 같습니다.

* 유형의 모든 노드 검색 `sling:OsgiConfig`
* 서비스 이름에 따른 필터
* 실행 모드에 따라 필터

>[!NOTE]
>
>읽기 [특정 인스턴스에 대해서만 저장소 기반 보존 정의 방법](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html).

### 저장소에 새 구성 추가 {#adding-a-new-configuration-to-the-repository}

#### 알아야 할 사항 {#what-you-need-to-know}

저장소에 새 구성을 추가하려면 다음을 알아야 합니다.

1. 다음 **영구 ID** 서비스의 (PID).

   참조 **구성** 필드를 클릭합니다. 이 이름은 번들 이름(또는 **구성 정보** 를 클릭하여 제품에서 사용할 수 있습니다.

   예를 들어, 노드를 만듭니다 `com.day.cq.wcm.core.impl.VersionManagerImpl.` 를 **AEM WCM 버전 관리자**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 특정 [실행 모드](/help/sites-deploying/configure-runmodes.md) 는 필수입니다. 폴더를 만듭니다.

   * `config` - 모든 실행 모드
   * `config.author` - 작성 환경용
   * `config.publish` - 게시 환경의 경우
   * `config.<run-mode>` - 적절하

1. 다음 **구성** 또는 **출하 시 구성** 는 필수입니다.
1. 구성할 개별 매개 변수 다시 생성해야 하는 기존 매개 변수 정의를 모두 포함합니다.

   웹 콘솔에서 개별 매개 변수 필드를 참조합니다. 이 이름은 각 매개 변수에 대해 대괄호 안에 표시됩니다.

   예를 들어 속성을 만듭니다
   `versionmanager.createVersionOnActivation` 를 **활성화 시 버전 만들기**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. 구성이에 이미 있습니까? `/libs`? 인스턴스의 모든 구성을 나열하려면 **쿼리** 다음 SQL 쿼리를 제출하기 위한 CRXDE Lite 도구:

   `select * from sling:OsgiConfig`

   있는 경우 이 구성을 ` /apps/<yourProject>/`을 업데이트한 후 새 위치에서 사용자 지정되었습니다.

#### 리포지토리에서 구성 생성 {#creating-the-configuration-in-the-repository}

저장소에 새 구성을 실제로 추가하려면:

1. CRXDE Lite을 사용하여 다음 위치로 이동합니다.

   ` /apps/<yourProject>`

1. 아직 존재하지 않는 경우 `config` 폴더 ( `sling:Folder`):

   * `config` - 모든 실행 모드에 적용 가능
   * `config.<run-mode>` - 특정 실행 모드에 따라

1. 이 폴더에서 노드를 만듭니다.

   * 유형: `sling:OsgiConfig`
   * 이름: 영구 ID(PID);

      예를 들어 AEM WCM Version Manager 가 `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >출하 시 구성 추가 시 `-<identifier>` 를 클릭합니다.
   >
   >로서의: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >위치 `<identifier>` 는 인스턴스를 식별하기 위해 을 입력해야 하는 자유 텍스트로 대체됩니다(이 정보를 생략할 수 없음). 예:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 구성할 각 매개 변수에 대해 이 노드에서 속성을 만듭니다.

   * 이름: 웹 콘솔에 표시된 대로 매개 변수 이름 필드 설명 끝에 대괄호로 이름이 표시됩니다. 예, 예 `Create Version on Activation` 사용 `versionmanager.createVersionOnActivation`
   * 유형: 적절한 경우입니다.
   * 값: 필요한 경우.

   구성할 매개 변수에 대해서만 속성을 만들면 다른 매개 변수는 AEM에서 설정한 대로 기본값이 됩니다.

1. 모든 변경 내용을 저장합니다.

   서비스를 다시 시작하여 노드가 업데이트되는 즉시(웹 콘솔에서 수행된 변경 사항) 변경 사항이 적용됩니다.

>[!CAUTION]
>
>에서는 아무 것도 변경하지 마십시오 `/libs` 경로.

>[!CAUTION]
>
>구성 시작 시 읽으려면 구성 전체 경로가 정확해야 합니다.

## 구성 세부 사항 {#configuration-details}

### 시작 시 해상도 순서 {#resolution-order-at-startup}

다음 우선 순위 순서가 사용됩니다.

1. 아래의 저장소 노드 `/apps/*/config...`형식이 있는 .eth `sling:OsgiConfig` 또는 속성 파일을 포함할 수 없습니다.

1. 유형이 있는 저장소 노드 `sling:OsgiConfig` 아래에 `/libs/*/config...`. (기본 정의)

1. 임의 `.config` 파일 `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. 로컬 파일 시스템에 있을 때 사용됩니다.

즉, `/libs` 의 프로젝트 특정 구성으로 마스킹할 수 있습니다. `/apps`.

### 런타임 시 해결 순서 {#resolution-order-at-runtime}

시스템이 실행되는 동안 수행된 구성 변경 사항은 수정된 구성으로 다시 로드를 트리거합니다.

그런 다음 다음과 같은 우선 순위가 적용됩니다.

1. 웹 콘솔에서 구성을 수정하면 런타임 시 우선하므로 즉시 적용됩니다.
1. 에서 구성 수정 `/apps` 즉시 적용됩니다.
1. 에서 구성 수정 `/libs` 의 구성으로 마스킹되지 않는 한 즉시 적용됩니다. `/apps`.

### 여러 실행 모드의 해상도 {#resolution-of-multiple-run-modes}

실행 모드별 구성의 경우 여러 실행 모드를 결합할 수 있습니다. 예를 들어 다음 스타일로 구성 폴더를 만들 수 있습니다.

`/apps/*/config.<runmode1>.<runmode2>/`

모든 실행 모드가 시작 시 정의된 실행 모드와 일치하는 경우 이러한 폴더의 구성이 적용됩니다.

예를 들어 인스턴스가 실행 모드로 시작된 경우 `author,dev,emea`, 구성 노드 `/apps/*/config.emea`, `/apps/*/config.author.dev/` 및 `/apps/*/config.author.emea.dev/` 의 구성 노드가 적용되는 동안 `/apps/*/config.author.asean/` 및 `/config/author.dev.emea.noldap/` 적용되지 않습니다.

동일한 PID에 대해 여러 구성을 적용할 수 있으면 일치하는 실행 모드가 가장 많은 구성이 적용됩니다.

예를 들어 인스턴스가 실행 모드로 시작된 경우 `author,dev,emea`, 및 `/apps/*/config.author/` 및 `/apps/*/config.emea.author/` 에 대한 구성 정의
`com.day.cq.wcm.core.impl.VersionManagerImpl`, 의 구성 `/apps/*/config.emea.author/` 이 적용됩니다.

이 규칙의 세부기간은 PID 수준입니다.
에서 동일한 PID에 대해 일부 속성을 정의할 수 없습니다 `/apps/*/config.author/` 및 기타 `/apps/*/config.emea.author/` PID를 참조하십시오.
일치하는 실행 모드가 가장 많은 구성은 전체 PID에 적용됩니다.

### 표준 구성 {#standard-configurations}

다음 목록은 리포지토리에서 사용 가능한 구성(표준 설치)의 작은 선택을 보여 줍니다.

* 작성자 - AEM WCM 필터:

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 게시 - AEM WCM 필터:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 게시 - AEM WCM 페이지 통계:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>이러한 구성은 `/libs` 직접 편집하지 않지만 애플리케이션 영역에 복사해야 합니다( `/apps`) 내의 아무 곳에나 삽입할 수 있습니다.

인스턴스에 모든 구성 노드를 나열하려면 **쿼리** 다음 SQL 쿼리를 제출하기 위한 CRXDE Lite 기능:

`select * from sling:OsgiConfig`

### 구성 지속성 {#configuration-persistence}

* 웹 콘솔을 통해 구성을 변경하면(일반적으로) 다음 리포지토리에 기록됩니다.

   `/apps/{somewhere}`

   * 기본적으로 `{somewhere}` is `system/config` 따라서 구성을

      `/apps/system/config`

   * 그러나 처음에 리포지토리의 다른 위치에서 가져온 구성을 편집하는 경우: 예:

      /libs/foo/config/someconfig

      그런 다음 업데이트된 구성이 원래 위치에 기록됩니다. 예:

      `/apps/foo/config/someconfig`

* 에 의해 변경된 설정 `admin` 에 저장됨 `*.config` 파일 위치:

   ```
      /crx-quickstart/launchpad/config
   ```

   * OSGi 구성 관리자의 개인 데이터 영역이며, `admin`로 설정되어야 합니다.
   * 구현 세부 사항이므로 이 디렉토리를 직접 편집하지 않아야 합니다.
   * 그러나 이러한 구성 파일의 위치를 알고 있으면 백업 및/또는 여러 설치 시 복사본을 가져올 수 있습니다.

      * Apache Felix OSGi Management Console

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling Client Repository

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>다음을 수행해야 합니다. ***절대*** 폴더 또는 파일 편집:
>
>`/crx-quickstart/launchpad/config`
