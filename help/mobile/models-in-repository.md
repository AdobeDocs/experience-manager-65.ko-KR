---
title: 저장소의 모델
seo-title: 저장소의 모델
description: 'null'
seo-description: 'null'
uuid: 54f81180-4178-4e33-a6f0-e9e6ea50798e
contentOwner: User
content-type: reference
discoiquuid: ae1a72f4-d8c1-4c75-ba2c-7322f3743b17
noindex: true
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/administer-mobile-apps
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 1%

---


# 저장소의 모델{#models-in-repository}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

모델에는 궁극적으로 컨텐츠 서비스에서 렌더링할 속성을 정의하는 데이터 유형 세트가 포함되어 있습니다. 또한 모델은 데이터 무결성을 적용하기 위해 다른 모델 간의 관계를 정의합니다.

개발자는 리포지토리의 모델 구조를 잘 알고 있어야 합니다. 앱 요구 사항에 따라 고유한 모델 및 엔티티를 만들 수 있습니다.

## 모델 유형 만들기 {#creating-model-types}

*/libs/settings/mobileapps/model-types* 아래에 두 가지 시스템 제공 모델 유형이 있습니다. 시스템 모델 유형을 재정의하려면 재정의가 수행되도록 하는 구성 노드 아래에 *mobileapps/model-types* 노드를 만들어야 합니다.

예를 들어, */conf/myconf1* 및 */conf/myconf2*&#x200B;에 구성을 만들고 *conf1*&#x200B;에서만 시스템 모델 유형을 재정의하려면 *conf1* 설정 아래에 *mobileapps/model-types* 노드를 만듭니다.

모델에 데이터 유형을 추가할 수 있도록 하려면 모델 유형에 &#39;cq:Page&#39; 유형의 &#39;scaffolding&#39;이라는 하위 노드와 *wcm/scaffolding/components/scaffolding*&#x200B;의 리소스 유형이 있어야 합니다.

스캐폴딩 페이지에는 이 유형에서 만든 데이터 형식 모델을 사용할 수 있음을 나타내는 *dataTypesConfig* 속성도 포함되어야 합니다.

>[!NOTE]
>
>**Scaffolding**&#x200B;은 모델을 기반으로 엔티티가 편집할 수 있는 데이터 유형을 정의하는 페이지입니다. 각 데이터 유형은 UI에 필드가 표시되는 방식과 데이터 값이 유지되는 방식을 정의하도록 구성할 수도 있습니다.

### 데이터 유형 구성 {#data-types-config}

데이터 유형 구성 노드에는 데이터 유형 항목 목록이 포함되어 있습니다. 각 데이터 유형 항목은 데이터 유형이 모델 편집기에 표시되는 방식과 엔티티에 의한 최종 렌더링을 위해 지속되어야 하는 방법을 지정합니다.

| **속성 이름** | **설명** |
|---|---|
| fieldIcon | 데이터 유형을 나타내는 CoralUI 아이콘 클래스 |
| fieldPropResourceType | 데이터 유형을 구성하기 위한 모든 속성을 렌더링하는 구성 요소 |
| fieldProperties | fieldPropResourceType이 *mobileapps/caas/gui/components/models/editor/datatypes/field*&#x200B;일 때 사용되는 속성 구성 요소의 다중 값 목록입니다 |
| fieldResourceType | resourceType데이터 형식(즉, 엔티티 편집기에서 속성을 렌더링할 구성 요소)에 대해 지속된 노드의 유형입니다 |
| fieldViewResourceType | 모델 편집기 보기에서 데이터 유형을 렌더링하는 데 사용할 구성 요소입니다(이 속성을 생략하면 fieldResourceType이 사용됩니다.) |
| fieldTitle | 모델 편집기에 표시할 데이터 유형의 이름입니다. |
| multiFieldResourceType | 다중 값을 선택한 경우 지속형 노드에서 사용할 리소스 유형입니다 |
| renderType | 클라이언트측 렌더링에 대한 렌더링 단서 |

### 데이터 유형 구성 오버레이 {#data-types-config-overlay}

&#39;dataTypesConfig&#39; 속성은 Sling 리소스 병합을 지원합니다. 즉, 시스템 모델 유형(또는 사용자 지정 모델 유형)에서 사용되는 데이터 유형은 오버레이 노드를 사용하여 사용자 지정할 수 있습니다.

*/libs/settings/mobileapps/mobileapps/mobiledapps/formbuilderconfig/datatypes*&#x200B;의 오버레이를 만든 다음 원하는 대로 사용자 지정해야 합니다.

예를 들어 fieldResourceType을 사용자 지정 구성 요소로 변경하기 위해 String 데이터 유형에 대한 오버레이를 추가할 수 있습니다.

Sling 리소스 병합에 대한 자세한 내용은 [AEM](/help/sites-developing/sling-resource-merger.md)에서 Sling 리소스 합병 사용 을 참조하십시오.

![chlimage_1-7](assets/chlimage_1-7.png)

### 데이터 유형 {#data-types}

모델 데이터 유형은 양식을 게시할 때 포함할 데이터를 포함할 수 있는 양식 구성 요소입니다. 데이터 유형 구성 요소는 원하는 만큼 복잡할 수 있습니다. 사용자 지정 데이터 유형의 예는 특정 국가의 주소 블록일 수 있으며, 기본 데이터 유형을 사용하여 항상 사용자 지정 데이터를 다시 만들어야 하는 경우를 방지할 수 있습니다.

사용자 지정 데이터 유형의 예로 &#39;/libs/mobileapps/caas/components/form/contentreference&#39;를 참조하십시오.

모든 기본 데이터 형식은 기존 Granite 양식 구성 요소를 사용합니다. 다음을 참조하십시오.[https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/index.html)

그런 다음 모델 편집기에서 사용할 데이터 유형 구성에 모든 사용자 지정 데이터 유형을 추가할 수 있습니다.

## 모델 만들기 {#creating-models}

원하는 모델 유형과 데이터 유형이 모두 개발되면 모델 생성을 시작할 수 있습니다. 작성자는 궁극적으로 모델을 사용하여 컨텐츠 서비스에서 데이터를 렌더링하는 데 사용하는 엔티티를 만듭니다.

모델을 만드는 작업은 현재 구성을 기반으로 허용되는 모델 유형을 선택한 다음 제목과 설명을 제공하는 것으로 구성됩니다.

대시보드에서 모델을 만들고 관리하는 방법에 대한 자세한 내용은 모바일 앱용 작성 섹션에서 [모델 만들기](/help/mobile/administer-mobile-apps.md)를 참조하십시오.

### 모델 {#properties-of-a-model} 속성

다음 표에서는 모델에 대해 정의된 속성을 보여 줍니다.

| **속성 이름** | **설명** |
|---|---|
| 모델 제목 | 모델 이름 |
| 설명 | 모델에 대한 설명 |
| 썸네일 | 모델의 축소판 이미지 |
| 모델 유형 | 모델 유형(단순 문자열 또는 실제 구성 요소에 대한 경로일 수 있음) |
| 허용된 하위 | 이 템플릿의 하위로 허용되는 템플릿의 경로입니다 |
| 허용된 상위 | 이 템플릿의 상위 항목일 수 있는 템플릿의 경로입니다 |

>[!NOTE]
>
>*허용되는 하위* 및 *허용되는 부모* 속성은 페이지 템플릿과 동일한 규칙을 따릅니다. 자세한 내용은 [페이지 템플릿](/help/sites-developing/page-templates-static.md)을 참조하십시오.
>
>*모델 유형* 속성을 참조하면서 모든 모델은 *mobileapps/caas/components/data/entity*&#x200B;의 슈퍼 유형이 있어야 하지만 컨텐츠 전달을 사용자 지정할 수 있는 하위 유형이 있을 수 있습니다. 모든 모델 유형이 고유한지 확인하면 컨텐츠 서비스 클라이언트가 데이터의 개체를 구분하는 데 도움이 될 수 있습니다.

### 모델 편집 {#editing-a-model}

모델 편집에는 편집할 모델과 연결된 스캐폴딩 대화 상자 양식이 열립니다. 일반적으로 스캐폴딩은 모델의 하위 노드이지만 &#39;cq:scaffolding&#39; 속성을 사용하여 경로를 지정하여 원하는 경우 모델 외부에 배치할 수 있습니다. 속성이 달라야 하는 여러 모델 간에 동일한 스캐폴딩을 공유하려는 경우 유용합니다.

모델에 대한 스캐폴딩이 있으면 모델 편집기가 &#39;jcr:content/cq:dialog/content&#39; 아래에 있는 모든 것을 렌더링합니다. 현재는 클라이언트측 양식 빌더 엔진에서 최대 3열 고정 레이아웃만 지원됩니다. 렌더링된 양식 대화 상자의 오른쪽에는 데이터 유형 구성에 지정된 모든 데이터 유형의 목록이 표시됩니다. 데이터 유형을 클릭하여 편집할 수 있습니다. 오른쪽 레일이 선택한 데이터 유형에 대한 속성 탭으로 전환합니다. 새 데이터 유형을 미리 보기 캔버스로 드래그하여 추가할 수 있습니다. 저장 을 클릭하면 변경 사항이 서버에 전파됩니다. 취소(Cancel)를 클릭하면 모델 편집기가 닫힙니다.

>[!NOTE]
>
>모든 모델은 템플릿이므로 모든 AEM 템플릿 규칙을 따릅니다. 이렇게 하면 *allowedParent*&#x200B;및 *allowedChildren* 속성과 같은 속성을 사용할 수 있습니다. 모델을 기반으로 새 엔티티를 생성할 때 효과적입니다. 템플릿 규칙을 사용하면 엔티티가 계층 구조에 따라 특정 모델만 기반으로 할 수 있습니다.
>
>대시보드에서 모델을 편집하는 방법에 대한 자세한 내용은 모바일 앱용 작성 섹션에서 [모델 만들기](/help/mobile/administer-mobile-apps.md)를 참조하십시오.

### 시스템 모델 {#system-models}

간단한 컨텐츠 재사용을 위해 사전 정의된 시스템 모델의 두 유형이 제공됩니다. 이러한 모델은 편집할 수 없습니다.

**페이지** 모델페이지 모델은 콘텐츠 서비스별로 전달하기 위해 사이트에서 기존 콘텐츠를 다시 사용하는 빠른 방법을 제공합니다.

페이지 모델을 기반으로 하는 엔티티의 resourceType은 다음과 같습니다.mobileapps/caas/components/data/pages

경로:사이트 페이지의 경로입니다. 이 경로 및 그 하위 경로의 콘텐츠는 콘텐츠 서비스 핸들러에 의해 렌더링됩니다.

**자산** 모델Assets 모델은 콘텐츠 서비스에서 전달하는 데 자산의 기존 콘텐츠를 다시 사용하는 빠른 방법을 제공합니다.

페이지 모델을 기반으로 하는 엔티티의 resourceType은 다음과 같습니다.*mobileapps/caas/components/data/assets*

자산 목록:자산의 경로 목록입니다. 각 자산은 resourceType *wcm/foundation/components/image*&#x200B;의 하위 엔티티 노드로 추가됩니다.

>[!NOTE]
>
>대시보드에서 모델을 만드는 데 이러한 템플릿을 사용하는 방법에 대한 자세한 내용은 모바일 앱용 작성 섹션에서 [모델 만들기](/help/mobile/administer-mobile-apps.md) 를 참조하십시오.
