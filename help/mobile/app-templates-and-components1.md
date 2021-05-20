---
title: 앱 템플릿 및 구성 요소
seo-title: 앱 템플릿 및 구성 요소
description: 앱 템플릿 및 구성 요소에 대해 알려면 이 페이지를 따르십시오. 템플릿 구조에 대한 자세한 정보를 제공합니다.
seo-description: 앱 템플릿 및 구성 요소에 대해 알려면 이 페이지를 따르십시오. 템플릿 구조에 대한 자세한 정보를 제공합니다.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---

# 앱 템플릿 및 구성 요소{#app-templates-and-components}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

템플릿은 페이지를 만드는 데 사용되며 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다. 템플릿은 만들 페이지와 구조가 동일하지만 실제 컨텐츠는 없는 노드 계층 구조입니다.

각 템플릿에는 사용할 수 있는 구성 요소 선택 사항이 표시됩니다.

* 템플릿은 [구성 요소](/help/sites-developing/components.md);
* 구성 요소는 컨텐츠를 렌더링하는 데 사용, 액세스 허용 및 위젯을 사용합니다.

>[!NOTE]
>
>CRXDE Lite을 사용하여 AEM 애플리케이션을 개발하는 방법에 대해 알아보려면 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)을 사용하여 개발 을 참조하십시오.

템플릿은 페이지의 기반이 됩니다.

페이지를 만들려면 템플릿을 (node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**)사이트 트리의 해당 위치에 복사해야 합니다.페이지가 **웹 사이트** 탭을 사용하여 만들어지는 경우 이러한 작업이 수행됩니다.

또한 이 복사 작업은 페이지의 초기 컨텐츠(일반적으로 최상위 컨텐츠만 해당)와 페이지를 렌더링하는 데 사용되는 페이지 구성 요소의 경로(하위 노드 jcr:content의 모든 항목)인 sling:resourceType 속성을 제공합니다.

## 템플릿 {#structure-of-a-template} 구조

고려해야 할 두 가지 측면이 있습니다.

* 템플릿 자체의 구조
* 템플릿을 사용할 때 생성되는 컨텐츠의 구조

템플릿은 **cq:Template** 유형의 노드 아래에 만들어집니다.

특히 다음과 같은 다양한 속성을 설정할 수 있습니다.

* **jcr:title**  - 템플릿의 제목.페이지를 만들 때 대화 상자에 표시됩니다.
* **jcr:description**  - 템플릿에 대한 설명.페이지를 만들 때 대화 상자에 표시됩니다.

이 노드에는 결과 페이지의 컨텐츠 노드의 기반으로 사용되는 *jcr:content (cq:PageContent)* 노드가 포함되어 있습니다.새 페이지의 실제 컨텐츠를 렌더링하는 데 사용할 구성 요소인 *sling:resourceType*&#x200B;을 사용하여 를 참조합니다.

>[!NOTE]
>
>AEM의 템플릿 및 구성 요소에 대한 기본 사항을 알려면 아래 리소스를 참조하십시오.
>
>* [템플릿](/help/sites-developing/templates.md)
* [구성 요소](/help/sites-developing/components.md)



템플릿 및 구성 요소에 대한 기본 이해를 했으면 다음 리소스를 참조하십시오.

* [템플릿 및 구성 요소 만들기 및 추가](/help/mobile/mobile-ondemand-app-templates.md)
* [컨텐츠 속성을 사용하여 컨텐츠 내보내기](/help/mobile/on-demand-content-properties-exporting.md)
* [우수 사례](/help/mobile/best-practices-aem-mobile.md)
* [AEM Mobile 컨텐츠 서비스 개발](/help/mobile/developing-content-services.md)

### 추가 리소스 {#additional-resources}

모바일 앱에 대한 추가 주제에 대해 알아보려면 아래 링크를 참조하십시오.

* [콘텐츠 동기화가 있는 모바일](/help/mobile/mobile-ondemand-contentsync.md)
* [모바일 앱 테스트](/help/mobile/develop-mobile-apps-testing.md)
