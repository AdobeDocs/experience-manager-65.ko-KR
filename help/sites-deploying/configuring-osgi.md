---
title: OSGi 구성
seo-title: OSGi 구성
description: OSGi는 AEM 파섹 AEM 및 해당 구성의 복합 번들을 제어하는 데 사용됩니다. 이 문서에서는 이러한 번들의 구성 설정을 관리하는 방법에 대해 자세히 설명합니다.
seo-description: OSGi는 AEM 파섹 AEM 및 해당 구성의 복합 번들을 제어하는 데 사용됩니다. 이 문서에서는 이러한 번들의 구성 설정을 관리하는 방법에 대해 자세히 설명합니다.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# OSGi 구성{#configuring-osgi}

[OSGi는](https://www.osgi.org/) Adobe Experience Manager(AEM 파섹)의 기술 스택에서 기본적인 요소입니다. AEM 및 해당 구성의 복합 번들을 제어하는 데 사용됩니다.

OSGi *는 &quot;애플리케이션이 작고 재사용 가능한 공동 작업 구성 요소로 구성될 수 있도록 하는 표준화된 프리미티브 방식을 제공합니다. 이러한 구성 요소를 애플리케이션으로 구성하고 배포할*&#x200B;수 있습니다.&quot;

이를 통해 번들은 개별적으로 시작, 중지, 설치 및 설치되므로 간편하게 관리할 수 있습니다. 상호 종속성은 자동으로 처리됩니다. 각 OSGi 구성 요소(OSGi [사양](https://www.osgi.org/Specifications/HomePage)참조)는 다양한 번들 중 하나에 포함되어 있습니다.

이러한 번들에 대한 구성 설정은 다음 방법 중 하나로 관리할 수 있습니다.

* adobe CQ [웹 콘솔 사용](#osgi-configuration-with-the-web-console)
* 구성 파일 [사용](#osgi-configuration-with-configuration-files)
* 저장소에서 [content-nodes( `sling:OsgiConfig`) 구성](#osgi-configuration-in-the-repository)

두 가지 방법 중 하나는 기본적으로 실행 모드와 관련하여 미묘한 차이가 있지만 사용할 [수 있습니다](/help/sites-deploying/configure-runmodes.md).

* [Adobe CQ 웹 콘솔](#osgi-configuration-with-the-web-console)

   * 웹 콘솔은 OSGi 구성을 위한 표준 인터페이스입니다. 미리 정의된 목록에서 가능한 값을 선택할 수 있는 다양한 속성을 편집할 수 있는 UI를 제공합니다.

      따라서 가장 사용하기 쉬운 방법입니다.

   * 웹 콘솔로 이루어진 모든 구성은 현재 실행 모드 또는 실행 모드에 대한 후속 변경에 관계없이 즉시 적용되며 현재 인스턴스에 적용됩니다.

* [구성 파일](#osgi-configuration-with-configuration-files)

   * 웹 콘솔에 정의된 설정을 포함합니다.
   * 다른 인스턴스에서 사용하기 위해 컨텐츠 패키지에 포함할 수 있습니다.

* [저장소의 content-nodes(sling:osgiConfig)](#osgi-configuration-in-the-repository)

   * 이를 위해서는 CRXDE Lite를 사용하는 수동 구성이 필요합니다.
   * 노드의 이름 지정 규칙 때문에 `sling:OsgiConfig` 구성을 특정 [실행 모드에](/help/sites-deploying/configure-runmodes.md)연결할 수 있습니다. 동일한 저장소에서 두 개 이상의 실행 모드에 대한 구성을 저장할 수도 있습니다.
   * 적절한 구성은 즉시(실행 모드에 따라 다름) 적용됩니다.

어떤 방법을 사용하든 다음 구성 방법 모두:

* 저장소 컨텐츠를 복사하거나 복제하면 동일한 구성이 다시 만들어집니다.
* FileVault 또는 Subversion으로 구성을 체크 아웃할 수 있습니다.를 참조하십시오.
* 다른 인스턴스를 설정할 때 사용하기 위해 패키지에 저장할 수 있습니다.
* 스크립트를 사용하여 구성 세부 사항을 프로파일링하는 구성 롤아웃을 수행할 수 있습니다.

>[!NOTE]
>
>특정 중요 설정에 대한 세부 사항은 OSGi 구성 [설정 아래에 나열되어 있습니다.](/help/sites-deploying/osgi-configuration-settings.md)

## 웹 콘솔을 사용한 OSGi 구성 {#osgi-configuration-with-the-web-console}

AEM [의 웹 콘솔은](/help/sites-deploying/web-console.md) 번들을 구성하기 위한 표준 인터페이스를 제공합니다. 구성 **탭은** OSGi 번들을 구성하는 데 사용되므로 AEM 시스템 매개 변수를 구성하는 기본 메커니즘입니다.

변경 사항은 관련 OSGi 구성에 즉시 적용되므로 다시 시작할 필요가 없습니다.

>[!NOTE]
>
>웹 콘솔에서 수행한 변경 사항은 [구성 파일로](#osgi-configuration-with-configuration-files)저장소에 저장됩니다. 이러한 구성 요소는 추가 설치 시 다시 사용하기 위해 컨텐츠 패키지에 포함될 수 있습니다.

>[!NOTE]
>
>웹 콘솔에서 기본 설정을 언급하는 설명은 Sling 기본값과 관련이 있습니다.
>
>Adobe Experience Manager에는 자체 기본값이 있으므로 기본값은 콘솔에 문서화된 기본값과 다를 수 있습니다.

웹 콘솔로 구성을 업데이트하려면:

1. 다음 방법 **중** 하나를 사용하여 웹 콘솔의 구성 탭에 액세스합니다.

   * 도구 -> 작업 **메뉴의 링크에서 웹 콘솔을** 엽니다. 콘솔에 로그인한 후 다음 드롭다운 메뉴를 사용할 수 있습니다.

      **OSGi >**

   * 직접 URL;예를 들면 다음과 같습니다.

      `http://localhost:4502/system/console/configMgr`
   목록이 표시됩니다.

1. 다음 중 하나로 구성할 번들을 선택합니다.

   * 해당 번들의 **편집** 아이콘 클릭
   * 번들의 **이름** 클릭

1. 대화 상자가 열립니다. 여기에서 필요에 따라 편집할 수 있습니다.예를 들어 로그 수준을 **다음으로** 설정합니다 `INFO`.

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >업데이트는 [구성 파일로](#osgi-configuration-with-configuration-files)저장소에 저장됩니다. 이후에 이러한 항목을 찾으려면(예: 다른 인스턴스에서 사용할 컨텐츠 패키지에 포함하려는 경우) 영구 ID( `PID`)를 기록해 두어야 합니다.

1. **저장**&#x200B;을 클릭합니다.

   변경 사항은 실행 중인 시스템의 관련 OSGi 구성에 즉시 적용되며 다시 시작할 필요가 없습니다.

   >[!NOTE]
   >
   >이제 관련 [구성 파일을 찾을 수 있습니다](#osgi-configuration-with-configuration-files).예를 들어, 다른 인스턴스에서 사용하기 위해 컨텐츠 패키지에 포함시킵니다.

## 구성 파일이 있는 OSGi 구성 {#osgi-configuration-with-configuration-files}

웹 콘솔을 사용하여 수행한 구성 변경 사항은 다음 아래에서 구성 파일( `.config`)로 보관소에 유지됩니다.

`/apps`

이러한 구성 요소는 컨텐츠 패키지에 포함할 수 있으며 다른 인스턴스에서 다시 사용할 수 있습니다.

>[!NOTE]
>
>구성 파일의 형식은 매우 구체적입니다. 자세한 내용은 [Sling Apache 설명서를](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) 참조하십시오.
>
>따라서 웹 콘솔에서 실제 변경을 수행하여 구성 파일을 만들고 유지하는 것이 좋습니다.

웹 콘솔에는 변경 사항이 저장되었는지 여부를 표시하지 않지만 쉽게 찾을 수 있습니다.

1. 웹 콘솔에서 [초기](#osgi-configuration-with-the-web-console)변경을 수행하여 구성 파일을 만듭니다.
1. CRXDE Lite를 엽니다.
1. **도구**&#x200B;메뉴에서&#x200B;**쿼리**...를 선택합니다..
1. 업데이트된 **구성의 PID를** 검색하려면 `SQL` 유형 쿼리를 제출합니다.

   예를 들어 Apache **Felix OSGi Management Console에는** 다음과 같은 PID(Persistent Identity)가 있습니다.

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   따라서 SQL 쿼리는 다음과 같습니다.

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 구성 파일 노드가 표시됩니다.

   위의 예제의 경우:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >이 파일을 열어 변경 내용을 볼 수 있지만 입력 오류를 방지하려면 콘솔을 사용하여 실제 변경하는 것이 좋습니다.

1. 이제 이 노드를 포함하는 컨텐츠 패키지를 만들고 다른 인스턴스에서 필요에 따라 사용할 수 있습니다.

## 저장소의 OSGi 구성 {#osgi-configuration-in-the-repository}

웹 콘솔을 사용하는 것 외에도 저장소에서 구성 세부 사항을 정의할 수도 있습니다. 따라서 다른 실행 모드를 쉽게 구성할 수 있습니다.

이러한 구성은 시스템에서 참조할 수 있도록 저장소에 `sling:OsgiConfig` 노드를 생성하여 만듭니다. 이러한 노드는 OSGi 구성을 미러링하고 사용자 인터페이스를 구성합니다. 구성 데이터를 업데이트하려면 노드 속성을 업데이트합니다.

저장소의 구성 데이터를 수정하는 경우 변경 사항은 웹 콘솔을 사용하여 변경한 것처럼 관련 OSGi 구성에 즉시 적용되며 적절한 유효성 검사 및 일관성 검사가 제공됩니다. 구성 복사 대상 `/libs/` 옵션에도 적용됩니다 `/apps/`.

동일한 구성 매개 변수가 여러 위치에 있을 수 있으므로 시스템은 다음과 같습니다.

* 모든 유형의 노드 검색 `sling:OsgiConfig`
* 서비스 이름에 따라 필터링
* 실행 모드에 따라 필터링

>[!NOTE]
>
>특정 인스턴스에만 [](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html)대한 저장소 기반 수용 정의 방법도 살펴볼 수 있습니다.

### 저장소에 새 구성 추가 {#adding-a-new-configuration-to-the-repository}

#### 알아야 할 사항 {#what-you-need-to-know}

저장소에 새 구성을 추가하려면 다음을 알아야 합니다.

1. 서비스의 **PID** (영구 ID)입니다.

   웹 **콘솔에서 구성** 필드를 참조하십시오. 번들 이름(또는 페이지 하단에 **있는 구성** 정보)의 뒤에 이름이 대괄호로 표시됩니다.

   예를 들어 AEM WCM 버전 관리자를 `com.day.cq.wcm.core.impl.VersionManagerImpl.` 구성할 **노드를 만듭니다**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 특정 [실행 모드가](/help/sites-deploying/configure-runmodes.md) 필요한지 여부. 폴더를 만듭니다.

   * `config` - 모든 실행 모드
   * `config.author` - 작성자 환경
   * `config.publish` - 게시 환경용
   * `config.<run-mode>` - 적절하

1. 구성 **또는** 출하 **시 구성이** 필요한지 여부.
1. 구성할 개별 매개 변수;를 포함하여 다시 만들어야 하는 기존 매개 변수 정의를 포함합니다.

   웹 콘솔에서 개별 매개 변수 필드를 참조합니다. 이 이름은 각 매개 변수에 대해 대괄호로 표시됩니다.

   예를 들어 속성을 만듭니다
   `versionmanager.createVersionOnActivation` 활성화 **시 버전 만들기를 구성합니다**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. 구성이 이미 에 `/libs`있습니까? 인스턴스의 모든 구성을 나열하려면 CRXDE Lite **의** 쿼리 도구를 사용하여 다음 SQL 쿼리를 제출합니다.

   `select * from sling:OsgiConfig`

   이 경우 이 구성을 복사한 다음 새 위치에서 사용자 지정할 수 ` /apps/<yourProject>/`있습니다.

#### 저장소에서 구성 만들기 {#creating-the-configuration-in-the-repository}

실제로 새 구성을 저장소에 추가하려면:

1. CRXDE Lite를 사용하여 다음 항목으로 이동합니다.

   ` /apps/<yourProject>`

1. 아직 존재하지 않는 경우 `config` 폴더( `sling:Folder`)를 만듭니다.

   * `config` - 모든 실행 모드 적용 가능
   * `config.<run-mode>` - 특정 실행 모드에만 해당

1. 이 폴더에서 노드를 만듭니다.

   * 유형: `sling:OsgiConfig`
   * 이름:영구 ID(PID);

      for example for AEM WCM Version Manager use `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >공장 구성을 만들 때 이름에 `-<identifier>` 추가합니다.
   >
   >As in: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >인스턴스를 식별하기 위해 입력해야 하는 자유 텍스트로 `<identifier>` 대체되는 경우(이 정보를 생략할 수 없음)예를 들면 다음과 같습니다.
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 구성할 각 매개 변수에 대해 이 노드에 속성을 만듭니다.

   * 이름:웹 콘솔에 표시된 대로 매개 변수 이름;필드 설명 끝에 대괄호로 이름이 표시됩니다. 예를 들어, `Create Version on Activation``versionmanager.createVersionOnActivation`
   * 유형:를 참조하십시오.
   * 값:를 참조하십시오.
   구성할 매개 변수에 대한 속성만 만들어야 하지만 다른 매개 변수는 AEM에서 설정한 대로 기본값을 사용합니다.

1. 모든 변경 내용을 저장합니다.

   변경 사항은 서비스를 다시 시작하여 노드가 업데이트되는 즉시 적용됩니다(웹 콘솔에서 수행한 변경 사항).

>[!CAUTION]
>
>패스에 있는 것은 변경할 수 `/libs` 없습니다.

>[!CAUTION]
>
>시작할 때 읽으려면 구성의 전체 경로가 정확해야 합니다.

## 구성 세부 사항 {#configuration-details}

### 시작 시 해상도 순서 {#resolution-order-at-startup}

다음 우선 순위 순서가 사용됩니다.

1. 형식 `/apps/*/config...`또는 속성 파일이 `sling:OsgiConfig` .either 아래에 있는 저장소 노드.

1. Repository nodes with type `sling:OsgiConfig` under `/libs/*/config...`. (기본 정의).

1. 모든 `.config` 파일 `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`제공 를 클릭합니다.

즉, 의 일반 구성은 의 프로젝트별 구성으로 `/libs` 마스크 처리할 수 `/apps`있습니다.

### 런타임 시 해상도 순서 {#resolution-order-at-runtime}

시스템 실행 중에 수행된 구성 변경 사항은 수정된 구성으로 다시 로드를 트리거합니다.

그런 다음 다음 우선 순위가 적용됩니다.

1. 웹 콘솔에서 구성을 수정하면 런타임 시 우선하므로 즉시 적용됩니다.
1. 구성 수정은 즉시 `/apps` 적용됩니다.
1. 에서 구성을 수정하면 에서 구성에 의해 마스크가 적용되지 않는 한 즉시 `/libs` 적용됩니다 `/apps`.

### 여러 실행 모드 해상도 {#resolution-of-multiple-run-modes}

실행 모드별 구성의 경우 여러 실행 모드를 결합할 수 있습니다. 예를 들어 다음 스타일로 구성 폴더를 만들 수 있습니다.

`/apps/*/config.<runmode1>.<runmode2>/`

이러한 폴더의 구성은 모든 실행 모드가 시작 시 정의된 실행 모드와 일치하는 경우 적용됩니다.

예를 들어, 인스턴스가 실행 모드로 시작된 경우 구성 `author,dev,emea`노드는 에 `/apps/*/config.emea``/apps/*/config.author.dev/` 있고 구성 노드는 `/apps/*/config.author.emea.dev/` 적용되며 `/apps/*/config.author.asean/` 적용되지 `/config/author.dev.emea.noldap/` 않습니다.

동일한 PID에 대해 여러 구성을 적용할 경우 일치하는 실행 모드가 가장 많은 구성이 적용됩니다.

예를 들어, 인스턴스가 실행 모드로 시작되었고 `author,dev,emea`에 대한 `/apps/*/config.author/` 구성을 `/apps/*/config.emea.author/` 모두`com.day.cq.wcm.core.impl.VersionManagerImpl`정의하고 `/apps/*/config.emea.author/` 를정의하면 에 구성이적용됩니다.

이 규칙의 세부기간은 PID 수준입니다.
동일한 PID에 대해 일부 속성을 정의할 수 `/apps/*/config.author/` 없으며, 같은 PID에 대해 더 구체적인 속성을 정의할 `/apps/*/config.emea.author/` 수 없습니다.
가장 많은 수의 일치하는 실행 모드를 가진 구성은 전체 PID에 적용됩니다.

### 표준 구성 {#standard-configurations}

다음 목록은 저장소에서 사용 가능한(표준 설치에서)의 작은 선택 구성을 보여줍니다.

* 작성자 - AEM WCM 필터:

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 게시 - AEM WCM 필터:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 게시 - AEM WCM 페이지 통계:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>이러한 구성이 내부에 있기 때문에 `/libs` `/apps`직접 편집할 수 없지만 사용자 정의 전에 애플리케이션 영역()에 복사해야 합니다.

인스턴스의 모든 구성 노드를 나열하려면 CRXDE Lite의 **쿼리** 기능을 사용하여 다음 SQL 쿼리를 제출합니다.

`select * from sling:OsgiConfig`

### 구성 지속성 {#configuration-persistence}

* 웹 콘솔을 통해 구성을 변경하면(일반적으로) 다음 위치에 보관소에 기록됩니다.

   `/apps/{somewhere}`

   * 기본적으로 `{somewhere}` `system/config` 구성이

      `/apps/system/config`

   * 그러나, 처음에 저장소의 다른 곳에서 가져온 구성을 편집하는 경우:예를 들면 다음과 같습니다.

      /libs/foo/config/someconfig

      업데이트된 구성은 원래 위치에 기록됩니다.예를 들면 다음과 같습니다.

      `/apps/foo/config/someconfig`

* 에 의해 변경된 `admin` 설정은 다음 `*.config` 파일에서 저장됩니다.

   ```
      /crx-quickstart/launchpad/config
   ```

   * OSGi 구성 관리자의 개인 데이터 영역이며 시스템 입력 방법에 관계없이 `admin`에서 지정한 모든 구성 세부 정보를 보유합니다.
   * 이 디렉토리는 구현 세부 사항이므로 직접 편집해서는 안 됩니다.
   * 그러나 이러한 구성 파일의 위치를 알면 백업 및/또는 다중 설치를 위해 복사본을 만들 수 있습니다.

      * Apache Felix OSGi Management Console

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling 클라이언트 저장소

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>다음 아래에서 폴더나 파일을 편집해서는 ***안*** 됩니다.
>
>`/crx-quickstart/launchpad/config`

