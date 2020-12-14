---
title: 오버레이
seo-title: 오버레이
description: AEM에서는 오버레이의 원칙을 사용하여 콘솔 및 기타 기능을 확장 및 사용자 정의할 수 있습니다
seo-description: AEM에서는 오버레이의 원칙을 사용하여 콘솔 및 기타 기능을 확장 및 사용자 정의할 수 있습니다
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# 오버레이{#overlays}

AEM(및 그 이전에는, CQ)는 오버레이의 원칙을 오랫동안 사용하여 [콘솔](/help/sites-developing/customizing-consoles-touch.md) 및 기타 기능(예: [페이지 작성](/help/sites-developing/customizing-page-authoring-touch.md))을 확장 및 사용자 정의할 수 있도록 했습니다.

오버레이는 많은 컨텍스트에서 사용할 수 있는 용어입니다. 이 컨텍스트(확장 AEM)에서 오버레이는 사전 정의된 기능을 가져와 표준 기능을 사용자 정의하기 위해 해당 기능에 사용자 정의 정의를 추가하는 것을 의미합니다.

표준 인스턴스에서 사전 정의된 기능은 `/libs` 아래에 있으며, `/apps` 분기 아래에 오버레이(사용자 지정)를 정의하는 것이 좋습니다. AEM에서는 검색 경로를 사용하여 리소스를 찾습니다. 먼저 `/apps` 분기를 검색한 다음 `/libs` 분기([검색 경로를 구성할 수 있음](#configuring-the-search-paths)). 이 메커니즘은 오버레이(및 여기에 정의된 사용자 지정)에 우선 순위가 있음을 의미합니다.

AEM 6.0 이후 오버레이의 구현 및 사용 방법이 변경되었습니다.

* AEM 6.0 이상 - [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 관련 오버레이(즉, 터치 지원 UI)용

   * 메서드

      * `/apps` 아래에 적절한 `/libs` 구조를 재구성합니다.

         이것은 1:1 사본이 필요하지 않으며, [Sling 리소스 합병](/help/sites-developing/sling-resource-merger.md)은 필요한 원래 정의를 상호 참조하는 데 사용됩니다. Sling 리소스 합병은 차이(차이) 메커니즘을 통해 리소스에 액세스하고 병합하는 서비스를 제공합니다.

      * `/apps`에서 변경합니다.
   * 이점

      * `/libs` 아래의 변경 사항에 더욱 강력해졌습니다.
      * 실제로 필요한 것만 재정의합니다.


* AEM 6.0 이전의 비화강암 오버레이 및 오버레이

   * 메서드

      * `/libs`에서 `/apps`로 콘텐트 복사

         속성을 포함하여 전체 하위 분기를 복사해야 합니다.

      * `/apps`에서 변경합니다.
   * 단점

      * `/libs` 아래에 어떤 내용이 변경되어도 변경 내용이 손실되지 않지만, `/apps` 아래의 오버레이에서 발생하는 특정 변경 내용을 다시 만들어야 할 수 있습니다.


>[!CAUTION]
>
>[Sling 리소스 합병](/help/sites-developing/sling-resource-merger.md) 및 관련 메서드는 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)에서만 사용할 수 있습니다. 즉, 골격 구조로 오버레이를 만드는 것은 표준 터치 지원 UI에만 적합합니다.
>
>다른 영역에 대한 오버레이(클래식 UI 포함)는 해당 노드 및 전체 하위 구조를 복사한 다음 필요한 변경 작업을 수행합니다.

오버레이는 콘솔[ 또는 ](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)콘솔 구성[의 자산 브라우저에 선택 카테고리 만들기(페이지 작성 시 사용)와 같이 많은 변경 사항에 대해 권장되는 방법입니다. ](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) 필수 항목:

* ***은(는) `/libs` 분기&#x200B;**에서 변경할 수 없습니다.
이 분기는 다음을 수행할 때마다 변경될 수 있으므로 변경한 내용이 손실될 수 있습니다.*

   * 인스턴스에서 업그레이드
   * 핫픽스 적용
   * 기능 팩 설치

* 한 위치에서 변경 사항을 집중적으로 적용합니다.필요에 따라 변경 내용을 추적, 마이그레이션, 백업 및/또는 디버깅할 수 있습니다.

## 검색 경로 구성 {#configuring-the-search-paths}

오버레이의 경우 배달된 리소스는 정의할 수 있는 검색 경로에 따라 검색된 리소스와 속성의 집합입니다.

* **Apache Sling 리소스 해결 프로그램 팩토리**&#x200B;에 대한 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)에 정의된 리소스 **확인자 검색 경로**&#x200B;입니다.

   * 검색 경로의 하향식 순서는 각 우선 순위를 나타냅니다.
   * 표준 설치에서 기본 기본값은 `/apps`, `/libs`이므로 `/apps`의 컨텐츠가 `/libs`보다 우선 순위가 높습니다(예: *overlays*).

* 두 서비스 사용자는 스크립트가 저장되는 위치에 대한 JCR:READ 액세스가 필요합니다. 이러한 사용자는 다음과 같습니다.components-search-service(com.day.cq.wcm.coreto access/cache 구성 요소에 의해 사용됨) 및 sling-scripting(org.apache.sling.servlets.resolver에서 servlet을 찾는 데 사용됨).
* 스크립트를 넣는 위치(이 예에서는 /etc, /libs 또는 /apps 아래)에 따라 다음 구성을 구성해야 합니다.

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 마지막으로 Servlet Resolver도 구성해야 합니다(이 예에서는 /etc도 추가하려면).

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## {#example-of-usage} 사용 예

몇 가지 예는 다음과 같은 경우에 다룹니다.

* [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)
* [페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md)

