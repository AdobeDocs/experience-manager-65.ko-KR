---
title: 앱 템플릿 및 구성 요소
description: 이 페이지를 따라 앱 템플릿 및 구성 요소에 대해 알아보십시오. 템플릿 구조에 대한 자세한 정보를 제공합니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# 앱 템플릿 및 구성 요소{#app-templates-and-components}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

템플릿은 페이지를 만드는 데 사용되며, 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다. 템플릿은 만들 페이지와 구조가 동일하지만 실제 컨텐츠는 없는 노드의 계층입니다.

각 템플릿에는 사용할 수 있는 구성 요소 선택 사항이 표시됩니다.

* 템플릿은 다음으로 구성됩니다. [구성 요소](/help/sites-developing/components.md);
* 구성 요소는 위젯을 사용하고 이에 대한 액세스를 허용하며, 위젯은 콘텐츠를 렌더링하는 데 사용됩니다.

>[!NOTE]
>
>CRXDE Lite을 사용하여 Adobe Experience Manager(AEM) 애플리케이션을 개발하는 방법에 대해 알아보려면 다음을 참조하십시오. [CRXDE Lite을 사용한 개발](/help/sites-developing/developing-with-crxde-lite.md).

템플릿은 페이지의 기초입니다.

페이지를 만들려면 템플릿을 복사해야 합니다(노드 트리) **/apps/&lt;myapp>/templates/&lt;mytemplate>**)를 사이트 트리의 해당 위치에 추가합니다. 이렇게 하는 것은 페이지를 **웹 사이트** 탭.

또한 이 복사 작업은 페이지에 초기 콘텐츠(일반적으로 최상위 수준의 콘텐츠만 해당) 및 속성 sling:resourceType을 제공합니다. sling:resourceType은 페이지를 렌더링하는 데 사용되는 페이지 구성 요소의 경로(하위 노드 jcr:content에 있는 모든 항목)입니다.

## 템플릿 구조 {#structure-of-a-template}

고려해야 할 두 가지 측면이 있습니다.

* 템플릿 자체의 구조
* 템플릿 사용 시 생성되는 콘텐츠 구조

템플릿은 유형의 노드 아래에 만들어집니다. **cq:Template**.

다양한 속성을 설정할 수 있습니다. 특히

* **jcr:title** - 템플릿 제목이며 페이지를 만들 때 대화 상자에 표시됩니다.
* **jcr:description** - 템플릿에 대한 설명. 페이지를 만들 때 대화 상자에 표시됩니다.

이 노드에는 다음 항목이 포함됩니다. *jcr:content (cq:PageContent)* 결과 페이지의 콘텐츠 노드의 기반으로 사용되는 노드입니다. 이 참조는 *sling:resourceType*: 새 페이지의 실제 콘텐츠를 렌더링하는 데 사용할 구성 요소입니다.

>[!NOTE]
>
>AEM의 템플릿 및 구성 요소에 대한 기본 사항을 알아보려면 아래 리소스를 참조하십시오.
>
>* [템플릿](/help/sites-developing/templates.md)
>* [구성 요소](/help/sites-developing/components.md)
>

템플릿 및 구성 요소에 대한 기본 사항을 이해했으면 다음 리소스를 참조하십시오.

* [템플릿 및 구성 요소 생성 및 추가](/help/mobile/mobile-ondemand-app-templates.md)
* [컨텐츠 속성을 사용하여 컨텐츠 내보내기](/help/mobile/on-demand-content-properties-exporting.md)
* [모범 사례](/help/mobile/best-practices-aem-mobile.md)
* [AEM Mobile 컨텐츠 서비스 개발](/help/mobile/developing-content-services.md)

### 추가 리소스 {#additional-resources}

모바일 앱에 대한 추가 주제에 대해 알아보려면 아래 링크를 참조하십시오.

* [콘텐츠 동기화가 있는 모바일](/help/mobile/mobile-ondemand-contentsync.md)
* [모바일 앱 테스트](/help/mobile/develop-mobile-apps-testing.md)
