---
title: 오버레이
description: Adobe Experience Manager은 오버레이 원리를 사용하여 콘솔 및 기타 기능을 확장하고 사용자 정의할 수 있습니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# 오버레이{#overlays}

Adobe Experience Manager(AEM) 및 그 이전 버전인 CQ에서는 오래 전부터 오버레이 원리를 사용하여 를 확장하고 맞춤화할 수 있었습니다. [콘솔](/help/sites-developing/customizing-consoles-touch.md) 및 기타 기능(예: [페이지 작성](/help/sites-developing/customizing-page-authoring-touch.md)).

오버레이는 여러 컨텍스트에서 사용되는 용어입니다. 이 컨텍스트(AEM 확장)에서 오버레이는 사전 정의된 기능을 가져와 고유한 정의를 적용합니다(표준 기능을 사용자 지정).

표준 인스턴스에서는 사전 정의된 기능이 `/libs` 및 아래에서 오버레이(사용자 정의)를 정의하는 것이 좋습니다. `/apps` 분기입니다. AEM은 검색 경로를 사용하여 리소스를 찾고 `/apps` 분기 및 다음 `/libs` 분기 ( [검색 경로를 구성할 수 있습니다.](#configuring-the-search-paths)). 이 메커니즘은 오버레이(및 그곳에서 정의된 맞춤화)에 우선순위가 있음을 의미합니다.

AEM 6.0 이후 오버레이가 구현되고 사용되는 방식이 변경되었습니다.

* AEM 6.0 이상 - 대상 [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)관련 오버레이(즉, 터치 지원 UI)

   * 메서드

      * 적절한 항목 재구성 `/libs` 아래 구조 `/apps`.

        1:1 사본은 필요하지 않습니다. [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md) 는 필요한 원래 정의를 상호 참조하는 데 사용됩니다. Sling 리소스 병합은 리소스를 액세스하고 차등(차이점 보관용) 메커니즘과 병합하는 서비스를 제공합니다.

      * 아래 `/apps`, 원하는 대로 변경합니다.

   * 장점

      * 다음 변경 사항에 더욱 강력함: `/libs`.
      * 필요한 사항만 재정의합니다.

* AEM 6.0 이전의 비 Granite 오버레이 및 오버레이

   * 메서드

      * 다음에서 콘텐츠 복사 `/libs` 끝 `/apps`

        속성을 포함한 전체 하위 분기를 복사합니다.

      * 아래 `/apps`, 원하는 대로 변경합니다.

   * 단점

      * 그러나 아래에 변경 사항이 있을 경우 변경 사항이 손실되지 않습니다. `/libs`, 오버레이에서 발생하는 특정 변경 사항을 아래에 다시 만들어야 할 수 있습니다. `/apps`.

>[!CAUTION]
>
>다음 [Sling 리소스 병합](/help/sites-developing/sling-resource-merger.md) 및 관련 메서드는 [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). 이는 뼈대 구조를 갖는 오버레이를 생성하는 것이 표준 터치 지원 UI에 대해서만 적절하다는 것을 의미한다.
>
>다른 영역(클래식 UI 포함)에 대한 오버레이에는 적절한 노드 및 전체 하위 구조를 복사한 다음 필요한 사항을 변경하는 작업이 포함됩니다.

다음과 같은 많은 변경 사항에 대해 권장되는 방법은 오버레이입니다. [콘솔 구성](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) 또는 [사이드 패널에서 에셋 브라우저에 선택 카테고리 만들기](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (페이지를 작성할 때 사용됩니다). 필요한 형식은 다음과 같습니다.

* ***금지* 에서 변경 `/libs` 분기&#x200B;**이 분기는 다음과 같은 경우 언제든지 변경될 수 있으므로 수행한 모든 변경 사항이 손실될 수 있습니다.

   * 인스턴스에서 업그레이드
   * 핫픽스 적용
   * 기능 팩 설치

* 한 위치에서 변경 내용을 집중하여 필요에 따라 변경 내용을 더 쉽게 추적, 마이그레이션, 백업 또는 디버깅할 수 있습니다.

## 검색 경로 구성 {#configuring-the-search-paths}

오버레이의 경우 게재된 리소스는 정의할 수 있는 검색 경로에 따라 검색된 리소스 및 속성의 집계입니다.

* 리소스 **확인자 검색 경로** 에 정의된대로 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 대상: **Apache Sling Resource Resolver Factory**.

   * 검색 경로의 하향식 순서는 해당 우선 순위를 나타냅니다.
   * 표준 설치에서 기본 기본값은 입니다. `/apps`, `/libs` - 따라서 의 콘텐츠 `/apps` 은(는) 보다 높은 우선 순위를 갖습니다. `/libs` (즉, *오버레이* it).

* 두 명의 서비스 사용자는 스크립트가 저장되는 위치에 대한 JCR:READ 액세스 권한이 필요합니다. 이러한 사용자는 components-search-service (com.day.cq.wcm.coreto 액세스/캐시 구성 요소에 의해 사용됨)와 sling-scripting (org.apache.sling.servlets.resolver에 의해 서블릿을 찾는 데 사용됨)입니다.
* 스크립트를 배치하는 위치에 따라 다음 구성도 구성해야 합니다(이 예제에서는 /etc, /libs 또는 /apps 아래).

  ```
  PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
  resource.resolver.searchpath=["/etc","/apps","/libs"]
  resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
  ```

* 마지막으로 Servlet Resolver도 구성해야 합니다(이 예에서는 /etc도 추가).

  ```
  PID = org.apache.sling.servlets.resolver.SlingServletResolver
  servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
  ```

## 사용 예 {#example-of-usage}

몇 가지 예는 다음과 같은 경우에 다룹니다.

* [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)
* [페이지 작성 사용자 지정](/help/sites-developing/customizing-page-authoring-touch.md)
