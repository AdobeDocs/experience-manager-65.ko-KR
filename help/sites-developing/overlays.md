---
title: 오버레이
seo-title: Overlays
description: AEM에서는 오버레이 원리를 사용하여 콘솔 및 기타 기능을 확장 및 사용자 지정할 수 있습니다
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 1%

---

# 오버레이{#overlays}

AEM(및 그 이전에는 CQ)에서 오랫동안 오버레이 원칙을 사용하여 확장을 허용 및 사용자 지정할 수 있었습니다 [콘솔](/help/sites-developing/customizing-consoles-touch.md) 및 기타 기능(예: [페이지 작성](/help/sites-developing/customizing-page-authoring-touch.md)).

오버레이는 많은 컨텍스트에서 사용할 수 있는 용어입니다. 이 컨텍스트(AEM 확장)에서 오버레이는 사전 정의된 기능을 가져와서 해당 기능에 대한 자체 정의를 적용합니다(표준 기능을 사용자 지정 하기 위해).

표준 인스턴스에서 사전 정의된 기능은 `/libs` 및 아래에서는 오버레이(사용자 지정)를 정의하는 것이 좋습니다. `/apps` 분기 AEM에서는 검색 경로를 사용하여 리소스를 찾고, 먼저 `/apps` 분기 및 `/libs` 분기 ( [검색 경로를 구성할 수 있습니다](#configuring-the-search-paths)). 이 메커니즘은 오버레이(및 여기에 정의된 사용자 지정)에 우선 순위가 지정됨을 의미합니다.

AEM 6.0 이후 오버레이 구현 및 사용 방법이 변경되었습니다.

* AEM 6.0 이상 - 대상 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)-관련 오버레이(즉, 터치 지원 UI)

   * 메서드

      * 적절한 `/libs` 구조 `/apps`.

         1:1 복사본이 필요하지 않으며 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) 필요한 원래 정의를 상호 참조하는 데 사용됩니다. Sling Resource Merger는 차이(차이점) 메커니즘을 통해 리소스에 액세스하고 병합하는 서비스를 제공합니다.

      * 에서 변경 작업을 수행합니다 `/apps`.
   * 장점

      * 의 변경 사항에 더욱 강력함 `/libs`.
      * 실제로 필요한 것만 재정의합니다.


* AEM 6.0 이전의 비 Granite 오버레이 및 오버레이

   * 메서드

      * 다음에서 컨텐츠 복사 `/libs` to `/apps`

         속성을 포함하여 전체 하위 분기를 복사해야 합니다.

      * 에서 변경 작업을 수행합니다 `/apps`.
   * 단점

      * 의 변경 사항이 변경되더라도 변경 사항이 유실되지는 않습니다 `/libs`로 지정하는 경우, 오버레이에서 발생하는 특정 변경 사항을 `/apps`.


>[!CAUTION]
>
>다음 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) 및 관련 메서드는 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). 즉, 뼈대 구조의 오버레이를 만드는 것은 터치 지원 표준 UI에만 적합합니다.
>
>다른 영역(클래식 UI 포함)에 대한 오버레이에는 적절한 노드 및 전체 하위 구조를 복사한 다음 필요한 변경을 수행하는 작업이 포함됩니다.

오버레이는 다음과 같은 많은 변경 사항에 권장되는 방법입니다 [콘솔 구성](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) 또는 [사이드 패널에서 자산 브라우저에 선택 카테고리 만들기](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (페이지를 작성할 때 사용됩니다.) 이 변수는 다음과 같이 필요합니다.

* 사용자 ***필수가 아니어야 합니다.* 에서 변경 `/libs` 분기&#x200B;**이 분기는 사용자가 변경할 때마다 변경되므로 변경한 내용이 손실될 수 있습니다.

   * 인스턴스에서 업그레이드
   * 핫픽스 적용
   * 기능 팩 설치

* 한 곳에 여러분의 변화를 집중합니다. 필요에 따라 변경 사항을 추적, 마이그레이션, 백업 및/또는 디버깅하는 것이 쉬워집니다.

## 검색 경로 구성 {#configuring-the-search-paths}

오버레이의 경우 제공된 리소스는 정의할 수 있는 검색 경로에 따라 검색된 리소스 및 속성의 합계입니다.

* 리소스 **확인자 검색 경로** 에 정의된 대로 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 대상 **Apache Sling Resource Resolver Factory**.

   * 검색 경로의 하향식 순서는 해당 우선 순위를 나타냅니다.
   * 표준 설치에서 기본 기본값은 다음과 같습니다 `/apps`, `/libs` - 따라서 `/apps` 의 우선 순위가 `/libs` (예: *오버레이* 참조).

* 두 서비스 사용자는 스크립트가 저장되는 위치에 대한 JCR:READ 액세스 권한이 필요합니다. 그러한 사용자는 components-search-service(com.day.cq.wcm.coreto access/cache 구성 요소에 사용됨)와 sling-scripting(org.apache.sling.servlets.resolver에서 서블릿을 찾기 위해 사용됨)입니다.
* 스크립트를 배치하는 위치에 따라 다음 구성을 구성해야 합니다(이 예제에서는 /etc, /libs 또는 /apps 아래).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 마지막으로 /etc를 추가하려면 Servlet Resolver를 구성해야 합니다

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 사용 예 {#example-of-usage}

다음 경우에 몇 가지 예를 다룹니다.

* [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)
* [페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md)
