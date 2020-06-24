---
title: AEM Sites - GDPR 준비
seo-title: AEM Sites - GDPR 준비
description: AEM Sites에 대한 GDPR 준비 사항에 대한 자세한 내용을 살펴보십시오.
seo-description: AEM Sites에 대한 GDPR 준비 사항에 대한 자세한 내용을 살펴보십시오.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---


# AEM Sites - GDPR 준비{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR은 아래 섹션에 나와 있지만, 자세히 설명된 내용은 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다. GDPR, CPA 등

2018년 5월 유럽연합(EU)의 데이터 보호(General Data Protection Regulation)이 발효된다.

AEM Sites은 고객이 GDPR 준수를 준수할 수 있도록 지원합니다. 이 페이지에서는 고객이 AEM Sites에서 GDPR 요청을 처리하는 절차를 안내합니다. 저장된 개인 데이터의 위치 및 수동으로 또는 코드로 해당 데이터를 제거하는 방법에 대해 설명합니다.

자세한 내용은 Adobe 개인 정보 보호 센터 [의 GDPR 페이지를 참조하십시오](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>자세한 [내용은 AEM GDPR 준비를](/help/managing/data-protection-and-privacy.md) 참조하십시오.

## 작성자 서버 {#author-server}

작성자 서버의 사용자 계정 및 UGC 컨텐츠는 [Platform GDPR 설명서에서 다룹니다](/help/managing/data-protection-and-privacy.md).

## 게시 서버 {#publish-server}

사이트에서 방문자를 인증하는 데 사용되는 사용자 계정과 게시 서버의 UGC 컨텐츠는 [Platform GDPR 설명서에서 다룹니다](/help/managing/data-protection-and-privacy.md).

기본적으로 AEM Sites 구성 요소는 방문자가 게시 서버에 입력한 양식 데이터를 저장하지 않습니다. 추가 처리를 위해 데이터를 타사 시스템 또는 Adobe Campaign으로 전달하는 것이 좋습니다.

## 옵트인/옵트아웃 {#opt-in-opt-out}

AEM에는 사용자에 대한 [옵트인/옵트아웃을 관리하는 데 사용할 수 있는 쿠키 옵트아웃 서비스가](/help/sites-developing/cookie-optout.md) 있습니다.

## Analytics의 향상된 인사이트 {#enhanced-insights-by-analytics}

AEM Sites에는 Adobe Analytics 온디맨드 서비스 내에서 기능을 사용하는 Analytics별 향상된 인사이트와의 선택적 통합이 포함되어 있습니다.

Adobe Analytics과 관련된 GDPR 데이터 주체의 요청 관리에 대한 자세한 내용은 [Adobe Analytics 및 GDPR을 참조하십시오](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html).

## Target의 향상된 개인화 {#enhanced-personalization-by-target}

AEM Sites에는 Target 온디맨드 서비스 내에서 기능을 사용하는 Adobe Target별 고급 개인화와의 선택적 통합이 포함되어 있습니다.

Adobe Target과 관련된 GDPR 데이터 주체의 요청 관리에 대한 자세한 내용은 [Adobe Target - 개인 정보 보호 및 개인 정보 보호 규정을 참조하십시오](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

AEM에서는 ContextHub에 선택적 데이터 레이어를 [제공합니다](/help/sites-developing/contexthub.md). 이렇게 하면 방문자별 데이터가 브라우저에 그대로 유지되므로 규칙 기반 개인화에 사용됩니다.

기본적으로 이 방문자 데이터는 AEM에 저장되지 않습니다. AEM은 브라우저에서 개인화를 결정하기 위해 규칙을 데이터 레이어로 보냅니다.

>[!NOTE]
>
>Adobe CQ 5.6 이전의 ClientContext(이전 버전의 ContextHub)는 데이터를 서버에 전송했지만 저장하지 않았습니다.
>
>Adobe CQ 5.5 및 이전 버전은 현재 EOL이며 이 설명서에서 다루지 않습니다.

### 옵트인/옵트아웃 구현 {#implementing-opt-in-opt-out}

사이트 소유자는 다음 지침에 따라 옵트아웃 구성 요소를 구현해야 합니다.

이러한 지침은 기본적으로 옵트인을 구현합니다. 따라서, 어떤 개인 데이터가 브라우저의 (클라이언트측) 지속성 내에 저장되기 전에 웹 사이트 방문자는 분명히 동의해야 합니다.

* 옵트아웃 구성 요소는 ContextHub 구성 요소가 포함될 때마다 포함되어야 합니다.
* 웹 사이트의 GDPR과 관련된 사용 약관은 웹 사이트 방문자에게 표시되어야 하며, 이를 통해 다음과 같은 작업을 할 수 있습니다.

   * accept
   * 거부
   * 이전 선택 변경

* 사이트 방문자가 사이트의 약관에 동의하는 경우 ContextHub 옵트아웃 쿠키는 제거해야 합니다.

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 사이트 방문자가 사이트의 약관에 동의하지 않으면 ContextHub 옵트아웃 쿠키를 설정해야 합니다.

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* ContextHub가 옵트아웃 모드에서 실행되고 있는지 확인하려면 브라우저 콘솔에서 다음 호출을 해야 합니다.

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### ContextHub 지속성 미리 보기 {#previewing-persistence-of-contexthub}

ContextHub에서 사용한 지속 상태를 미리 보려면 다음 작업을 수행할 수 있습니다.

* 브라우저 콘솔 사용; 예를 들면 다음과 같습니다.

   * Chrome:

      * 개발자 도구 > 응용 프로그램 > 저장소를 엽니다.

         * 로컬 저장소 > (웹 사이트) > ContextHubPersistence
         * 세션 저장소 > (웹 사이트) > ContextHubPersistence
         * 쿠키 > (웹 사이트) > 세션 지속성
   * Firefox:

      * 개발자 도구 열기 > 스토리지:

         * 로컬 저장소 > (웹 사이트) > ContextHubPersistence
         * 세션 저장소 > (웹 사이트) > ContextHubPersistence
         * 쿠키 > (웹 사이트) > 세션 지속성
   * Safari:

      * 메뉴 모음에서 환경 설정 > 고급 > 현상 표시 메뉴 열기
      * 현상 열기 > JavaScript 콘솔 표시

         * 콘솔 > 스토리지 > 로컬 스토리지 > (웹 사이트) > ContextHubPersistence
         * 콘솔 > 스토리지 > 세션 스토리지 > (웹 사이트) > ContextHubPersistence
         * 콘솔 > 스토리지 > 쿠키 > (웹 사이트) > ContextHubPersistence
   * Internet Explorer:

      * 개발자 도구 열기 > 콘솔

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* 브라우저 콘솔에서 ContextHub API를 사용합니다.

   * ContextHub에서는 다음과 같은 데이터 지속성 레이어를 제공합니다.

      * ContextHub.Utils.Persistence.Modes.LOCAL(기본값)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      ContextHub 저장소는 사용할 지속성 레이어를 정의하므로 모든 레이어를 선택해야 하는 지속성 현재 상태를 볼 수 있습니다.


예를 들어 localStorage에 저장된 데이터를 보려면 다음을 수행합니다.

ContextHub에서 사용한 지속 상태를 미리 보려면 다음 작업을 수행할 수 있습니다.

* 브라우저 콘솔 사용:

   * Chrome - [개발자 도구] > [응용 프로그램] > [저장소]를 엽니다.

      * 로컬 저장소 > (웹 사이트) > ContextHubPersistence
      * 세션 저장소 > (웹 사이트) > ContextHubPersistence
      * 쿠키 > (웹 사이트) > 세션 지속성
   * Firefox - 개발자 도구 > 스토리지 열기:

      * 로컬 저장소 > (웹 사이트) > ContextHubPersistence
      * 세션 저장소 > (웹 사이트) > ContextHubPersistence
      * 쿠키 > (웹 사이트) > 세션 지속성


* 브라우저 콘솔에서 ContextHub API를 사용합니다.

   * ContextHub에서는 다음과 같은 데이터 지속성 레이어를 제공합니다.

      * ContextHub.Utils.Persistence.Modes.LOCAL(기본값)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      ContextHub 저장소는 사용할 지속성 레이어를 정의하므로 모든 레이어를 선택해야 하는 지속성 현재 상태를 볼 수 있습니다.


예를 들어 localStorage에 저장된 데이터를 보려면 다음을 수행합니다.

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### ContextHub 지속성 지우기 {#clearing-persistence-of-contexthub}

ContextHub 지속성을 지우려면

* 현재 로드된 스토어의 지속성을 지우려면

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 특정 지속성 레이어를 지우려면 예: sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 모든 ContextHub 지속성 레이어를 지우려면 모든 레이어에 대해 적절한 코드를 호출해야 합니다.

   * ContextHub.Utils.Persistence.Modes.LOCAL(기본값)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW

