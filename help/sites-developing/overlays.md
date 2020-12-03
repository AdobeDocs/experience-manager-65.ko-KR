---
title: 오버레이
seo-title: 오버레이
description: AEM에서는 오버레이의 원칙을 사용하여 콘솔 및 기타 기능을 확장하고 사용자 정의할 수 있습니다
seo-description: AEM에서는 오버레이의 원칙을 사용하여 콘솔 및 기타 기능을 확장하고 사용자 정의할 수 있습니다
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

AEM(및 이에 앞서 CQ)은 오버레이의 원칙을 오랫동안 사용하여 [consoles](/help/sites-developing/customizing-consoles-touch.md) 및 기타 기능(예: [page authoring](/help/sites-developing/customizing-page-authoring-touch.md))을 확장하고 사용자 정의할 수 있도록 했습니다.

오버레이는 많은 컨텍스트에서 사용될 수 있는 용어입니다. 이 컨텍스트(AEM 확장)에서 오버레이는 사전 정의된 기능을 가져와서 표준 기능을 사용자 정의하기 위해 해당 기능에 사용자 정의 정의를 추가하는 것을 의미합니다.

표준 인스턴스에서 사전 정의된 기능은 `/libs` 아래에 있으며, `/apps` 분기 아래에 오버레이(사용자 지정)를 정의하는 것이 좋습니다. AEM에서는 검색 경로를 사용하여 리소스를 찾은 다음 먼저 `/apps` 분기를 검색한 다음 `/libs` 분기([검색 경로를 구성할 수 있습니다](#configuring-the-search-paths)). 이 메커니즘은 오버레이(및 여기에 정의된 사용자 지정)에 우선 순위가 지정됨을 의미합니다.

AEM 6.0 이후 오버레이가 구현되고 사용되는 방법이 변경되었습니다.

* AEM 6.0 이상 - [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 관련 오버레이(즉, 터치 지원 UI)용

   * 메서드

      * `/apps` 아래에 적절한 `/libs` 구조를 재구성합니다.

         여기에는 1:1 사본이 필요하지 않으며, [Sling 리소스 합병](/help/sites-developing/sling-resource-merger.md)이 필요한 원본 정의를 상호 참조하는 데 사용됩니다. Sling Resource Combination은 차이(차이) 메커니즘을 통해 리소스에 액세스하고 병합하는 서비스를 제공합니다.

      * `/apps` 아래에서 변경합니다.
   * 장점

      * `/libs` 아래에서 변경 사항이 더욱 강력해졌습니다.
      * 실제로 필요한 것만 재정의합니다.


* AEM 6.0 이전의 [화강암] 오버레이 및 오버레이

   * 메서드

      * `/libs`에서 `/apps`(으)로 콘텐트 복사

         속성을 포함하여 전체 하위 분기를 복사해야 합니다.

      * `/apps` 아래에서 변경합니다.
   * 단점

      * `/libs` 아래에 변경 사항이 있을 때 변경 내용이 손실되지는 않지만, 오버레이에서 `/apps` 아래에 발생하는 특정 변경 사항을 다시 만들어야 할 수 있습니다.


>[!CAUTION]
>
>[Sling 리소스 합병](/help/sites-developing/sling-resource-merger.md) 및 관련 메서드는 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)에서만 사용할 수 있습니다. 즉, 골격 구조를 갖는 오버레이를 만드는 것은 표준 터치 가능 UI에만 적합합니다.
>
>다른 영역에 대한 오버레이(클래식 UI 포함)에는 해당 노드 및 전체 하위 구조를 복사한 다음 필요한 변경을 수행하는 것이 포함됩니다.

오버레이는 콘솔[ 또는 ](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)을 구성하는 것과 같이, 많은 변경 사항에 대해 사이드 패널[의 자산 브라우저에 선택 카테고리 만들기(페이지 작성 시 사용)와 같은 권장 방법입니다. ](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) 이러한 요구 사항은 다음과 같습니다.

* ***은(는) `/libs` 분기&#x200B;**에서 변경할 수 없습니다.
이 분기는 다음과 같이 언제든지 변경할 수 있으므로 변경 사항이 손실될 수 있습니다.*

   * 인스턴스에서 업그레이드
   * 핫픽스 적용
   * 기능 팩 설치

* 한 곳에서 변경 사항을 집중적으로 적용를 사용하면 필요에 따라 변경 사항을 추적, 마이그레이션, 백업 및/또는 디버깅할 수 있습니다.

## 검색 경로 구성 {#configuring-the-search-paths}

오버레이의 경우 제공되는 리소스는 정의할 수 있는 검색 경로에 따라 검색된 리소스와 속성의 집합입니다.

* **Apache Sling Resource Resolver Factory**&#x200B;에 대한 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)에 정의된 리소스 **확인자 검색 경로**&#x200B;입니다.

   * 검색 경로의 하향식 순서는 각 우선 순위를 나타냅니다.
   * 표준 설치에서 기본 기본값은 `/apps`, `/libs`이므로 `/apps`의 컨텐츠의 우선 순위가 `/libs`보다 높습니다(즉, *overlays*).

* 두 서비스 사용자는 스크립트가 저장된 위치에 대한 JCR:READ 액세스 권한이 필요합니다. 이러한 사용자는 다음과 같습니다.components-search-service(com.day.cq.wcm.coreto access/cache components에서 사용) 및 sling-scripting(org.apache.sling.servlets.resolver에서 servlets를 찾는 데 사용).
* 스크립트를 넣는 위치(이 예에서는 /etc, /libs 또는 /apps)에 따라 다음 구성을 구성해야 합니다.

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

다음은 몇 가지 예입니다.

* [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)
* [페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md)

