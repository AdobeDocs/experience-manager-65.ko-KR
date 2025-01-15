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
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 1%

---

# 앱 템플릿 및 구성 요소{#app-templates-and-components}

{{ue-over-mobile}}

템플릿은 페이지를 만드는 데 사용되며, 선택한 범위 내에서 사용할 수 있는 구성 요소를 정의합니다. 템플릿은 만들 페이지와 구조가 동일하지만 실제 컨텐츠는 없는 노드의 계층입니다.

각 템플릿에는 사용할 수 있는 구성 요소 선택 사항이 표시됩니다.

* 템플릿은 [구성 요소](/help/sites-developing/components.md)(으)로 작성되었습니다.
* 구성 요소는 위젯을 사용하고 이에 대한 액세스를 허용하며, 위젯은 콘텐츠를 렌더링하는 데 사용됩니다.

>[!NOTE]
>
>CRXDE Lite을 사용하여 Adobe Experience Manager(AEM) 응용 프로그램을 개발하는 방법에 대해 알아보려면 [CRXDE Lite을 사용하여 개발](/help/sites-developing/developing-with-crxde-lite.md)을 참조하세요.

템플릿은 페이지의 기초입니다.

페이지를 만들려면 템플릿을 사이트 트리의 해당 위치에 복사해야 합니다(노드 트리 **/apps/&lt;myapp>/templates/&lt;mytemplate>**). 이는 **웹 사이트** 탭을 사용하여 페이지를 만드는 경우에 발생합니다.

또한 이 복사 작업은 페이지에 초기 콘텐츠(일반적으로 최상위 수준의 콘텐츠만 해당) 및 속성 sling:resourceType을 제공합니다. sling:resourceType은 페이지를 렌더링하는 데 사용되는 페이지 구성 요소의 경로(하위 노드 jcr:content에 있는 모든 항목)입니다.

## 템플릿 구조 {#structure-of-a-template}

고려해야 할 두 가지 측면이 있습니다.

* 템플릿 자체의 구조
* 템플릿 사용 시 생성되는 콘텐츠 구조

**cq:Template** 유형의 노드 아래에 템플릿이 만들어졌습니다.

다양한 속성을 설정할 수 있습니다. 특히

* **jcr:title** - 템플릿의 제목입니다. 페이지를 만들 때 대화 상자에 표시됩니다.
* **jcr:description** - 템플릿에 대한 설명. 페이지를 만들 때 대화 상자에 표시됩니다.

이 노드에는 결과 페이지의 콘텐츠 노드의 기반으로 사용되는 *jcr:content(cq:PageContent)* 노드가 포함되어 있습니다. 이 참조는 새 페이지의 실제 콘텐츠를 렌더링하는 데 사용할 구성 요소인 *sling:resourceType*&#x200B;을(를) 사용합니다.

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
