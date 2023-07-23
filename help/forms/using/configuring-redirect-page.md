---
title: 리디렉션 페이지 구성
seo-title: Configuring redirect page
description: 적응형 양식을 작성한 후 사용자는 양식을 작성하는 동안 양식 작성자가 구성할 수 있는 웹 페이지로 리디렉션될 수 있습니다.
seo-description: After filling an adaptive form, users can be redirected to a webpage that form authors can configure while creating the form.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: Adaptive Forms
exl-id: be1a774f-5681-443f-b195-28e89a020547
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 5%

---

# 리디렉션 페이지 구성{#configuring-redirect-page}

<span class="preview"> Adobe은 현대적이고 확장 가능한 데이터 캡처를 사용할 것을 권장합니다 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 대상 [새 적응형 Forms 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 Forms 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 이러한 구성 요소는 적응형 Forms 작성의 중요한 발전을 나타내어 인상적인 사용자 경험을 보장합니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 Forms을 작성하는 이전 방법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html) |
| AEM 6.5 | 이 문서 |

양식 작성자는 양식을 제출한 후 양식 사용자가 리디렉션되는 각 양식에 대한 페이지를 구성할 수 있습니다.

1. 편집 모드에서 구성 요소를 선택하고 ![필드 수준](assets/field-level.png) > **적응형 양식 컨테이너**&#x200B;을 클릭한 다음 을 클릭합니다 ![cmppr](assets/cmppr.png).

1. 사이드바에서 를 클릭합니다. **제출**.

1. 제출 섹션의 감사 페이지 아래에 리디렉션 페이지의 URL을 입력합니다.
1. 선택 사항으로, 제출 작업에서 REST에 제출 엔드포인트 작업의 경우 리디렉션 페이지에 전달할 매개 변수를 구성할 수 있습니다.

![페이지 구성 리디렉션](assets/thank-you-setting-1.png)

페이지 구성 리디렉션

양식 작성자는 감사 인사 페이지에 전달되는 다음 매개 변수를 사용할 수 있습니다. 사용 가능한 모든 제출 작업의 경우 `status` 및 `owner` 매개 변수가 전달됩니다. 이 두 매개 변수 외에도 다음 제출 작업에 대해 몇 가지 추가 매개 변수가 전달됩니다.

* **컨텐츠 저장 작업** (더 이상 사용되지 않음) : `contentPath`- 제출된 데이터가 저장되는 저장소의 노드 경로가 전달됩니다.

* **PDF 작업 저장** (더 이상 사용되지 않음) : `contentPath`- 저장소에 PDF 파일을 저장하는 노드에 대한 제출된 데이터 및 경로 중 이 전달됩니다.

* **Forms 워크플로우에 제출**: 양식 워크플로우에서 반환된 출력 매개 변수가 전달됩니다.

* **REST 끝점에 제출**: 필드 내 매개 변수 매핑에 추가된 매개 변수가 전달됩니다. `status` 및 `owner` 매개 변수는 이 제출 액션에서 전달되지 않습니다. 자세한 내용은 [REST 끝점에 제출 작업 구성](../../forms/using/configuring-submit-actions.md).
