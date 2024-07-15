---
title: OSGi 구성
description: OSGi는 Adobe Experience Manager(AEM)의 기술 스택에 있는 기본 요소입니다. AEM의 복합 번들과 해당 구성을 제어하는 데 사용됩니다. 이 문서에서는 이러한 번들에 대한 구성 설정을 관리하는 방법에 대해 자세히 설명합니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 0%

---

# OSGi 구성{#configuring-osgi}

[OSGi](https://www.osgi.org/)은(는) AEM(Adobe Experience Manager)의 기술 스택에 있는 기본 요소입니다. AEM의 복합 번들과 해당 구성을 제어하는 데 사용됩니다.

OSGi &quot;*은(는) 응용 프로그램을 작고 재사용 가능한 공동 작업 구성 요소에서 구성할 수 있는 표준화된 기본 형식을 제공합니다. 이러한 구성 요소는 응용 프로그램으로 구성하고*&quot;을(를) 배포할 수 있습니다.

이렇게 하면 번들을 개별적으로 중지, 설치 또는 시작할 수 있으므로 쉽게 관리할 수 있습니다. 상호 종속성이 자동으로 처리됩니다. 각 OSGi 구성 요소([OSGi 사양](https://docs.osgi.org/specification/) 참조)는 다양한 번들 중 하나에 포함되어 있습니다.

다음 방법 중 하나를 사용하여 이러한 번들에 대한 구성 설정을 관리할 수 있습니다.

* [Adobe CQ 웹 콘솔 사용](#osgi-configuration-with-the-web-console)
* [구성 파일](#osgi-configuration-with-configuration-files) 사용
* 저장소에서 [콘텐츠 노드(`sling:OsgiConfig`) 구성](#osgi-configuration-in-the-repository)

주로 [실행 모드](/help/sites-deploying/configure-runmodes.md)와 관련하여 약간의 차이가 있더라도 두 방법 중 하나를 사용할 수 있습니다.

* [Adobe CQ 웹 콘솔](#osgi-configuration-with-the-web-console)

   * 웹 콘솔은 OSGi 구성을 위한 표준 인터페이스입니다. 사전 정의된 목록에서 가능한 값을 선택할 수 있는 다양한 속성을 편집하기 위한 UI를 제공합니다.

     따라서 가장 사용하기 쉬운 방법입니다.

   * 웹 콘솔에서 수행된 모든 구성은 현재 실행 모드나 그 이후의 실행 모드 변경 사항에 관계없이 즉시 적용되며 현재 인스턴스에 적용할 수 있습니다.

* [구성 파일](#osgi-configuration-with-configuration-files)

   * 웹 콘솔에 정의된 설정을 포함합니다.
   * 다른 인스턴스에서 사용할 수 있도록 콘텐츠 패키지에 포함될 수 있습니다.

* [저장소의 content-nodes (sling:osgiConfig)](#osgi-configuration-in-the-repository)

   * CRXDE Lite을 사용하여 수동으로 구성해야 합니다.
   * `sling:OsgiConfig` 노드의 명명 규칙으로 인해 구성을 특정 [실행 모드](/help/sites-deploying/configure-runmodes.md)에 연결할 수 있습니다. 동일한 저장소에서 두 개 이상의 실행 모드에 대한 구성을 저장할 수도 있습니다.
   * 실행 모드에 따라 적절한 구성이 즉시 적용됩니다.

어떤 방법을 사용하든 다음 모든 구성 방법을 사용합니다.

* 저장소 콘텐츠를 복사하거나 복제하면 동일한 구성이 다시 생성됩니다.
* 보안이나 추가 업데이트를 위해 FileVault 또는 Subversion에 대한 구성을 체크 아웃할 수 있습니다.
* 다른 인스턴스를 설정할 때 사용할 수 있도록 패키지에 저장할 수 있습니다.
* 스크립트를 사용하여 구성 롤아웃을 수행하여 구성 세부 정보를 전파할 수 있습니다.

>[!NOTE]
>
>특정 중요한 설정에 대한 자세한 내용은 [OSGi 구성 설정](/help/sites-deploying/osgi-configuration-settings.md)에 나와 있습니다.

## 웹 콘솔을 사용한 OSGi 구성 {#osgi-configuration-with-the-web-console}

AEM의 [웹 콘솔](/help/sites-deploying/web-console.md)은(는) 번들을 구성하기 위한 표준화된 인터페이스를 제공합니다. **구성** 탭은 OSGi 번들을 구성하는 데 사용되므로 AEM 시스템 매개 변수를 구성하는 기본 메커니즘입니다.

수행된 모든 변경 사항은 즉시 관련 OSGi 구성에 적용되며, 다시 시작할 필요가 없습니다.

>[!NOTE]
>
>웹 콘솔에서 수행한 변경 내용은 저장소에 [구성 파일](#osgi-configuration-with-configuration-files)(으)로 저장됩니다. 이러한 파일은 추가 설치에서 재사용하기 위해 콘텐츠 패키지에 포함할 수 있습니다.

>[!NOTE]
>
>웹 콘솔에서 기본 설정을 언급하는 모든 설명은 Sling 기본값과 관련되어 있습니다.
>
>Adobe Experience Manager에는 자체 기본값이 있으므로 설정된 기본값이 콘솔에 문서화된 기본값과 다를 수 있습니다.

웹 콘솔로 구성을 업데이트하려면 다음을 수행하십시오.

1. 다음 방법 중 하나를 사용하여 웹 콘솔의 **구성** 탭에 액세스합니다.

   * **도구 > 작업** 메뉴의 링크에서 웹 콘솔을 엽니다. 콘솔에 로그인하면 의 드롭다운 메뉴를 사용할 수 있습니다.

     **OSGi >**

   * 직접 URL. 예:

     `http://localhost:4502/system/console/configMgr`

   목록이 표시됩니다.

1. 다음 중 하나로 구성할 번들을 선택합니다.

   * 해당 번들에 대한 **편집** 아이콘을 클릭합니다.
   * 번들의 **이름**&#x200B;을(를) 클릭합니다.

1. 대화 상자가 열립니다. 여기에서 필요에 따라 편집할 수 있습니다. 예를 들어 **로그 수준**&#x200B;을(를) `INFO`(으)로 설정합니다.

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >업데이트는 저장소에 [구성 파일](#osgi-configuration-with-configuration-files)(으)로 저장됩니다. 나중에 이러한 파일을 찾아 다른 인스턴스에서 사용할 콘텐츠 패키지에 포함시키려면 예를 들어 영구 ID(`PID`)를 메모하십시오.

1. **저장**&#x200B;을 클릭합니다.

   변경 사항은 실행 중인 시스템의 관련 OSGi 구성에 즉시 적용되므로 다시 시작할 필요가 없습니다.

   >[!NOTE]
   >
   >이제 관련 [구성 파일](#osgi-configuration-with-configuration-files)을 찾을 수 있습니다. 예를 들어 다른 인스턴스에서 사용할 콘텐츠 패키지에 를 포함합니다.

## 구성 파일이 있는 OSGi 구성 {#osgi-configuration-with-configuration-files}

웹 콘솔을 사용하여 수행한 구성 변경 내용은 다음 아래의 구성 파일(`.config`)로 리포지토리에 유지됩니다.

`/apps`

이러한 파일은 콘텐츠 패키지에 포함되어 다른 인스턴스에서 재사용할 수 있습니다.

>[!NOTE]
>
>구성 파일의 형식은 고유합니다. 다음에 대한 Sling Apache 설명서를 참조하십시오.
>* [Apache Sling 프로비저닝 모델 및 Apache SlingStart](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)에 대한 전체 세부 정보.
>* [Sling에서 리소스 및 속성을 가져오는 중](https://sling.apache.org/documentation/tutorials-how-tos/getting-resources-and-properties-in-sling.html)의 튜토리얼과 예입니다.
>
>따라서 웹 콘솔에서 실제 변경 작업을 수행하여 구성 파일을 만들고 유지 관리하는 것이 좋습니다.

웹 콘솔에는 변경 사항이 저장되었지만 저장소 내 위치를 나타내는 표시가 없지만 쉽게 찾을 수 있습니다.

1. [웹 콘솔에서 초기 변경](#osgi-configuration-with-the-web-console)하여 구성 파일을 만듭니다.
1. CRXDE Lite를 엽니다.
1. **도구** 메뉴에서 **쿼리...** 을 선택합니다.
1. 업데이트한 구성의 PID를 검색하려면 **Type** `SQL` 쿼리를 제출하십시오.

   예를 들어 **Apache Felix OSGi 관리 콘솔**&#x200B;에는 다음과 같은 영구 ID(PID)가 있습니다.

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   따라서 SQL 쿼리는 다음과 같을 수 있습니다.

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 구성 파일 노드가 표시됩니다.

   위의 예에서는 다음과 같습니다.

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >이 파일을 열어 변경 사항을 볼 수 있지만 입력 오류를 방지하려면 콘솔을 사용하여 실제 변경 작업을 수행하는 것이 좋습니다.

1. 이제 이 노드를 포함하는 콘텐츠 패키지를 빌드하고 다른 인스턴스에서 필요에 따라 를 사용할 수 있습니다.

## 저장소의 OSGi 구성 {#osgi-configuration-in-the-repository}

웹 콘솔을 사용할 수 있을 뿐만 아니라 저장소에서 구성 세부 정보를 정의할 수도 있습니다. 이렇게 하면 서로 다른 실행 모드를 쉽게 구성할 수 있습니다.

이러한 구성은 시스템이 참조할 수 있도록 저장소에 `sling:OsgiConfig`개의 노드를 만들어 수행됩니다. 이러한 노드는 OSGi 구성을 미러링하고, 사용자 인터페이스가 형성된다. 구성 데이터를 업데이트하려면 노드 속성을 업데이트합니다.

저장소에서 구성 데이터를 수정하면 변경 사항이 관련 OSGi 구성에 즉시 적용됩니다. 적절한 유효성 검사와 일관성 검사를 통해 웹 콘솔을 사용하여 변경한 것과 같습니다. 이 워크플로는 `/libs/`에서 `/apps/`(으)로 구성을 복사하는 작업에도 적용됩니다.

동일한 구성 매개변수가 여러 위치에 있으므로 시스템은 다음과 같이 합니다.

* `sling:OsgiConfig` 유형의 모든 노드를 검색합니다.
* 서비스 이름에 따른 필터
* 실행 모드에 따른 필터

>[!NOTE]
>
>[특정 인스턴스에만 리포지토리 기반 구성을 정의하는 방법](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html)도 읽어 보십시오.

### 저장소에 새 구성 추가 {#adding-a-new-configuration-to-the-repository}

#### 알아야 할 사항 {#what-you-need-to-know}

저장소에 구성을 추가하려면 다음을 알고 있어야 합니다.

1. 서비스의 **영구 ID**(PID)입니다.

   웹 콘솔에서 **구성** 필드를 참조합니다. 이름은 번들 이름 뒤에 대괄호로 표시됩니다(또는 페이지 아래쪽의 **구성 정보**&#x200B;에).

   예를 들어 `com.day.cq.wcm.core.impl.VersionManagerImpl.` 노드를 만들어 **AEM WCM 버전 관리자**&#x200B;를 구성하십시오.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 특정 [실행 모드](/help/sites-deploying/configure-runmodes.md)가 필요합니까? 폴더를 만듭니다.

   * `config` - 모든 실행 모드에 대해
   * `config.author` - 작성자 환경용
   * `config.publish` - 게시 환경용
   * `config.<run-mode>` - 해당되는 경우

1. **구성** 또는 **팩터리 구성**&#x200B;이 필요합니까?
1. 다시 만들어야 하는 기존 매개 변수 정의를 포함하여 구성할 개별 매개 변수입니다.

   웹 콘솔에서 개별 매개 변수 필드를 참조합니다. 이름은 각 매개 변수에 대해 대괄호로 표시됩니다.

   예를 들어 속성을 만듭니다
   `versionmanager.createVersionOnActivation`에서 **활성화 시 버전 만들기**&#x200B;를 구성할 수 있습니다.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. `/libs`에 구성이 있습니까? 인스턴스의 모든 구성을 나열하려면 CRXDE Lite의 **쿼리** 도구를 사용하여 다음 SQL 쿼리를 제출하십시오.

   `select * from sling:OsgiConfig`

   이 경우 이 구성을 ` /apps/<yourProject>/`에 복사한 다음 새 위치에서 사용자 지정할 수 있습니다.

#### 저장소에서 구성 만들기 {#creating-the-configuration-in-the-repository}

저장소에 새 구성을 실제로 추가하려면 다음 작업을 수행하십시오.

1. CRXDE Lite을 사용하여 다음으로 이동:

   ` /apps/<yourProject>`

1. 존재하지 않는 경우 `config` 폴더(`sling:Folder`)를 만듭니다.

   * `config` - 모든 실행 모드에 적용 가능
   * `config.<run-mode>` - 특정 실행 모드별

1. 이 폴더 아래에 노드를 만듭니다.

   * 유형: `sling:OsgiConfig`
   * 이름: 영구 ID(PID);

     예를 들어 AEM WCM 버전 관리자의 경우 `com.day.cq.wcm.core.impl.VersionManagerImpl`을(를) 사용합니다.

   >[!NOTE]
   >
   >팩터리 구성을 만들 때 이름에 `-<identifier>`을(를) 추가합니다.
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-<identifier>`(으)로
   >
   >`<identifier>`은(는) 인스턴스를 식별하기 위해 입력해야 하는 자유 텍스트로 대체됩니다(이 정보는 생략할 수 없음). 예를 들면 다음과 같습니다.
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 구성할 각 매개 변수에 대해 이 노드에 속성을 만듭니다.

   * 이름: 웹 콘솔에 표시되는 매개 변수 이름입니다. 이 이름은 필드 설명의 끝에 대괄호로 표시됩니다. 예를 들어 `Create Version on Activation`의 경우 `versionmanager.createVersionOnActivation`을(를) 사용합니다.
   * 적절한 경우 를 입력합니다.
   * 값: 필요에 따라.

   구성할 매개 변수에 대한 속성만 만들어야 하며 다른 매개 변수는 AEM에서 설정한 대로 기본값을 사용합니다.

1. 모든 변경 사항을 저장합니다.

   웹 콘솔의 변경 사항과 마찬가지로 서비스를 다시 시작하여 노드를 업데이트하면 변경 사항이 적용됩니다.

>[!CAUTION]
>
>`/libs` 경로에서 아무 것도 변경하지 마십시오.

>[!CAUTION]
>
>시작 시 읽으려면 구성의 전체 경로가 올바른지 확인해야 합니다.

## 구성 세부 정보 {#configuration-details}

### 시작 시 해결 순서 {#resolution-order-at-startup}

다음 우선 순위가 사용됩니다.

1. 유형 `sling:OsgiConfig` 또는 속성 파일이 있는 `/apps/*/config...` 아래의 저장소 노드입니다.

1. `/libs/*/config...`에서 유형이 `sling:OsgiConfig`인 저장소 노드입니다. (기본 정의).

1. `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`의 모든 `.config`개 파일. 로컬 파일 시스템에서 사용할 수 있습니다.

`/libs`의 일반 구성은 `/apps`의 프로젝트별 구성에 의해 마스킹될 수 있습니다.

### 런타임 시 해결 순서 {#resolution-order-at-runtime}

시스템이 실행되는 동안 구성을 변경하면 수정된 구성으로 다시 로드를 트리거합니다.

그러면 다음 우선 순위가 적용됩니다.

1. 웹 콘솔의 구성 수정은 런타임 시 우선적으로 적용되므로 즉시 적용됩니다.
1. `/apps`에서 구성을 수정하면 즉시 적용됩니다.
1. `/apps`의 구성에 의해 마스킹되지 않는 한 `/libs`의 구성 수정은 즉시 적용됩니다.

### 여러 실행 모드 해결 방법 {#resolution-of-multiple-run-modes}

실행 모드별 구성의 경우 여러 실행 모드를 결합할 수 있습니다. 예를 들어 다음 스타일의 구성 폴더를 만들 수 있습니다.

`/apps/*/config.<runmode1>.<runmode2>/`

이러한 폴더의 구성은 모든 실행 모드가 시작 시 정의된 실행 모드와 일치하는 경우 적용됩니다.

예를 들어 인스턴스가 실행 모드 `author,dev,emea`(으)로 시작된 경우 `/apps/*/config.emea`, `/apps/*/config.author.dev/` 및 `/apps/*/config.author.emea.dev/`의 구성 노드가 적용되지만 `/apps/*/config.author.asean/` 및 `/config/author.dev.emea.noldap/`의 구성 노드는 적용되지 않습니다.

동일한 PID에 대해 여러 구성을 적용할 수 있는 경우 일치하는 실행 모드 수가 가장 많은 구성이 적용됩니다.

예를 들어 인스턴스가 실행 모드 `author,dev,emea`(으)로 시작되고 `/apps/*/config.author/` 및 `/apps/*/config.emea.author/` 모두 구성을 정의하는 경우
`com.day.cq.wcm.core.impl.VersionManagerImpl`, `/apps/*/config.emea.author/`의 구성이 적용됩니다.

이 규칙의 세부 기간은 PID 수준입니다.
`/apps/*/config.author/`의 동일한 PID에 대한 일부 속성과 같은 PID에 대한 `/apps/*/config.emea.author/`의 더 구체적인 속성을 정의할 수 없습니다.
일치 실행 모드 수가 가장 많은 구성은 전체 PID에 유효합니다.

### 표준 구성 {#standard-configurations}

다음 목록은 저장소에서 사용할 수 있는(표준 설치에서) 몇 가지 구성을 보여줍니다.

* 작성자 - AEM WCM 필터:

  `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Publish - AEM WCM 필터:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Publish - AEM WCM 페이지 통계:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>이러한 구성은 `/libs`에 있으므로 직접 편집하지 말고 사용자 지정 전에 응용 프로그램 영역(`/apps`)에 복사해야 합니다.

CRXDE Lite의 모든 구성 노드를 나열하려면 인스턴스의 **쿼리** 기능을 사용하여 다음 SQL 쿼리를 제출하십시오.

`select * from sling:OsgiConfig`

### 구성 지속성 {#configuration-persistence}

* 웹 콘솔을 통해 구성을 변경하는 경우 이 구성은 (일반적으로) 다음 위치의 저장소에 기록됩니다.

  `/apps/{somewhere}`

   * 기본적으로 `{somewhere}`은(는) `system/config`이므로 구성이

     `/apps/system/config`

   * 그러나 처음 저장소의 다른 위치에서 가져온 구성을 편집하는 경우: 예를 들면 다음과 같습니다.

     /libs/foo/config/someconfig

     그런 다음 업데이트된 구성이 원래 위치 아래에 기록됩니다. 예를 들면 다음과 같습니다.

     `/apps/foo/config/someconfig`

* `admin`이(가) 변경한 설정은 아래의 `*.config` 파일에 저장됩니다.

  ```
     /crx-quickstart/launchpad/config
  ```

   * 이 영역은 OSGi 구성 관리자의 개인 데이터이며, 시스템에 어떻게 입력되었는지에 관계없이 `admin`에서 지정한 모든 구성 세부 정보를 포함합니다.
   * 이 영역은 구현 세부 사항이므로 이 디렉터리를 직접 편집해서는 안 됩니다.
   * 그러나 백업, 여러 설치 또는 두 가지 모두를 위해 복제본을 만들 수 있도록 이러한 구성 파일의 위치를 파악하는 것이 유용합니다.

      * Apache Felix OSGi 관리 콘솔

        `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling 클라이언트 저장소

        `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>아래의 폴더 또는 파일을 편집하지 마십시오.
>
>`/crx-quickstart/launchpad/config`
