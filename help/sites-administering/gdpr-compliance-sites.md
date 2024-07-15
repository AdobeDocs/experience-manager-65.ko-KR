---
title: AEM Sites - GDPR 준비 완료
description: AEM Sites에서 GDPR 요청을 처리하는 절차 및 사용 방법에 대해 알아봅니다.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Architect, Developer, Leader, User, Data Architect, Data Engineer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 92%

---

# AEM Sites - GDPR 준비 완료{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>아래 섹션에서는 GDPR이 예로 사용되지만, 포함된 세부 사항은 GDPR, CCPA 등과 같은 모든 데이터 보호 및 개인 정보 보호 규정에 적용됩니다.

데이터 사생활 보호권에 관한 유럽 연합의 GDPR(일반 데이터 보호 규정)은 2018년 5월에 발효됩니다.

AEM Sites는 GDPR 준수 의무와 관련하여 고객을 지원할 준비가 되어 있습니다. 이 페이지에서는 고객에게 AEM Sites에서 GDPR 요청을 처리하는 절차를 안내합니다. 저장된 개인 데이터의 위치와 수동으로 또는 코드로 해당 데이터를 제거하는 방법에 대해서도 설명합니다.

자세한 내용은 [Adobe 개인 정보 보호 센터의 GDPR 페이지](https://www.adobe.com/privacy/general-data-protection-regulation.html)를 참조하십시오.

>[!NOTE]
>
>자세한 내용은 [AEM GDPR 준비 완료](/help/managing/data-protection-and-privacy.md)를 참조하십시오.

## 작성자 서버 {#author-server}

작성자 서버의 사용자 계정 및 UGC 컨텐츠는 [플랫폼 GDPR 설명서](/help/managing/data-protection-and-privacy.md)에서 다룹니다.

## Publish 서버 {#publish-server}

사이트에서 방문자를 인증하는 데 사용되는 사용자 계정과 게시 서버의 UGC 컨텐츠는 [플랫폼 GDPR 설명서](/help/managing/data-protection-and-privacy.md)에서 다룹니다.

기본적으로 AEM Sites 구성 요소는 게시 서버에서 방문자가 입력한 양식 데이터를 저장하지 않습니다. 추가적인 처리가 필요하면 데이터를 서드파티 시스템 또는 Adobe Campaign에 전달하는 것이 좋습니다.

## 옵트인/옵트아웃 {#opt-in-opt-out}

AEM에는 사용자에 대한 옵트인/옵트아웃을 관리하는 데 사용할 수 있는 [쿠키 옵트아웃 서비스](/help/sites-developing/cookie-optout.md)가 있습니다.

## Analytics의 Enhanced Insights {#enhanced-insights-by-analytics}

AEM Sites에는 Adobe Analytics 온디맨드 서비스 내에서 기능을 사용하는 Analytics의 Enhanced Insights와의 선택적 통합이 포함되어 있습니다.

Adobe Analytics와 관련된 GDPR 데이터 주체 요청 관리에 대한 자세한 내용은 [Adobe Analytics 및 GDPR](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html)을 참조하십시오.

## Target의 향상된 Personalization {#enhanced-personalization-by-target}

AEM Sites에는 Adobe Target 온디맨드 서비스 내에서 기능을 사용하는 Target의 Enhanced Personalization과의 선택적 통합이 포함되어 있습니다.

Adobe Target과 관련된 GDPR 데이터 주체 요청 관리에 대한 자세한 내용은 [Adobe Target - 개인 정보 보호 및 일반 데이터 보호 규정](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)을 참조하십시오.

## ContextHub {#contexthub}

AEM에서는 [ContextHub](/help/sites-developing/contexthub.md)와 관련하여 선택적 데이터 계층을 제공합니다. 이렇게 하면 규칙 기반 개인화에 사용할 방문자별 데이터가 브라우저에 유지됩니다.

기본적으로 이 방문자 데이터는 AEM에 저장되지 않습니다. AEM은 브라우저에서 규칙을 데이터 계층에 보내 개인화를 결정합니다.

>[!NOTE]
>
>Adobe CQ 5.6 이전의 Client Context(ContextHub의 이전 버전)는 데이터를 서버에 전송했지만 저장하지는 않았습니다.
>
>Adobe CQ 5.5 및 이전 버전은 현재 수명이 종료되었으며 이 설명서에서 다루지 않습니다.

### 옵트인/옵트아웃 구현 {#implementing-opt-in-opt-out}

사이트 소유자는 다음 지침에 따라 옵트아웃 구성 요소를 구현해야 합니다.

이 지침은 기본적으로 옵트인을 구현합니다. 따라서, 개인 데이터가 브라우저에서(클라이언트측) 지속적으로 저장되려면 먼저 웹 사이트 방문자가 명확히 동의해야 합니다.

* 옵트아웃 구성 요소는 ContextHub 구성 요소가 포함될 때마다 포함되어야 합니다.
* 웹 사이트의 GDPR과 관련된 약관은 웹 사이트 방문자가 다음 중 하나를 선택할 수 있도록 웹 사이트 방문자에게 표시되어야 합니다.

   * 동의
   * 거부
   * 이전 옵션 변경

* 사이트 방문자가 사이트의 약관에 동의하면 ContextHub 옵트아웃 쿠키가 제거됩니다.

  ```
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* 사이트 방문자가 사이트의 약관에 동의하지 않으면 ContextHub 옵트아웃 쿠키가 설정됩니다.

  ```
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* ContextHub가 옵트아웃 모드에서 실행되고 있는지 확인하려면 브라우저의 콘솔에서 다음 호출을 수행해야 합니다.

  ```
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### ContextHub의 지속성 미리보기 {#previewing-persistence-of-contexthub}

ContextHub에서 사용한 지속성을 미리 보려면 다음 작업을 수행할 수 있습니다.

* 브라우저의 콘솔 사용. 예를 들어

   * Chrome:

      * Developer Tools > Application > Storage를 엽니다.

         * Local Storage > (웹 사이트) > ContextHubPersistence
         * Session Storage > (웹 사이트) > ContextHubPersistence
         * Cookies > (웹 사이트) > SessionPersistence

   * Firefox:

      * Developer Tools > Storage를 엽니다.

         * Local Storage > (웹 사이트) > ContextHubPersistence
         * Session Storage > (웹 사이트) > ContextHubPersistence
         * Cookies > (웹 사이트) > SessionPersistence

   * Safari:

      * 메뉴 막대에서 Preferences > Advanced > Show Develop 메뉴를 엽니다.
      * Develop > Show JavaScript Console을 엽니다.

         * Console > Storage > Local Storage > (웹 사이트) > ContextHubPersistence
         * Console > Storage > Session Storage > (웹 사이트) > ContextHubPersistence
         * Console > Storage > Cookies > (웹 사이트) > ContextHubPersistence

   * Internet Explorer:

      * 개발자 도구 > 콘솔을 엽니다.

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie

* 브라우저 콘솔에서 ContextHub API 사용.

   * ContextHub에서는 다음 데이터 지속성 계층을 제공합니다.

      * ContextHub.Utils.Persistence.Modes.LOCAL(기본값)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     ContextHub 저장소는 사용할 지속성 계층을 정의하므로 현재 지속성 상태를 보려면 모든 계층을 검사해야 합니다.

예를 들어 localStorage에 저장된 데이터를 보려는 경우

ContextHub에서 사용한 지속성을 미리 보려면 다음 작업을 수행할 수 있습니다.

* 브라우저의 콘솔 사용:

   * Chrome - Developer Tools > Application > Storage 열기:

      * Local Storage > (웹 사이트) > ContextHubPersistence
      * Session Storage > (웹 사이트) > ContextHubPersistence
      * Cookies > (웹 사이트) > SessionPersistence

   * Firefox - Developer Tools > Storage 열기:

      * Local Storage > (웹 사이트) > ContextHubPersistence
      * Session Storage > (웹 사이트) > ContextHubPersistence
      * Cookies > (웹 사이트) > SessionPersistence

* 브라우저 콘솔에서 ContextHub API 사용.

   * ContextHub에서는 다음 데이터 지속성 계층을 제공합니다.

      * ContextHub.Utils.Persistence.Modes.LOCAL(기본값)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     ContextHub 저장소는 사용할 지속성 계층을 정의하므로 현재 지속성 상태를 보려면 모든 계층을 검사해야 합니다.

예를 들어 localStorage에 저장된 데이터를 보려는 경우

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### ContextHub의 지속성 지우기 {#clearing-persistence-of-contexthub}

ContextHub 지속성 지우기:

* 현재 로드된 저장소의 지속성을 지우려면

  ```
  // to be able to fully access persistence layer, Opt-Out must be turned off
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  
  // following call asks all currently loaded stores to clear their data
  ContextHub.cleanAllStores();
  
  // following call asks all currently loaded stores to set back default values (provided in their configs)
  ContextHub.resetAllStores();
  ```

* 특정 지속성 계층을 지우려면(예: sessionStorage):

  ```
  var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
  storage.setItem('/store', null);
  storage.setItem('/_', null);
  
  // to confirm that nothing is stored:
  console.log(storage.getTree());
  ```

* 모든 ContextHub 지속성 계층을 지우려면 모든 레이어에 대해 적절한 코드를 호출해야 합니다.

   * ContextHub.Utils.Persistence.Modes.LOCAL(기본값)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
