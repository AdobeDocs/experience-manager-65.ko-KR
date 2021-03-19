---
title: 리디렉션 페이지 구성
seo-title: 리디렉션 페이지 구성
description: 적응형 양식을 작성한 후 사용자는 양식을 만드는 동안 양식 작성자가 구성할 수 있는 웹 페이지로 리디렉션할 수 있습니다.
seo-description: 적응형 양식을 작성한 후 사용자는 양식을 만드는 동안 양식 작성자가 구성할 수 있는 웹 페이지로 리디렉션할 수 있습니다.
uuid: f9d304b4-920d-4e50-a674-40eca48c530c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0ffbb4d3-9371-4705-8496-f98e22d9c4a6
docset: aem65
feature: 적응형 양식
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 리디렉션 페이지 {#configuring-redirect-page} 구성

양식 작성자는 양식을 제출한 후 사용자가 리디렉션되는 각 양식에 대한 페이지를 구성할 수 있습니다.

1. 편집 모드에서 구성 요소를 선택한 다음 ![필드 수준](assets/field-level.png) > **적응형 양식 컨테이너**&#x200B;를 클릭한 다음 ![cmppr](assets/cmppr.png)을 클릭합니다.

1. 세로 막대에서 **제출**&#x200B;을 클릭합니다.

1. 제출 섹션의 감사 페이지 아래에 리디렉션 페이지의 URL을 제공합니다.
1. 선택적으로, REST에 제출 끝점 작업에 대해 [작업 제출] 아래에서 리디렉션 페이지로 전달될 매개 변수를 구성할 수 있습니다.

![리디렉션 페이지 구성](assets/thank-you-setting-1.png)

리디렉션 페이지 구성

양식 작성자는 감사 인사 페이지에 전달되는 다음 매개 변수를 사용할 수 있습니다. 사용 가능한 모든 제출 작업에 대해 `status` 및 `owner` 매개 변수가 전달됩니다. 이 두 매개 변수 외에도 다음과 같은 제출 작업에 대해 몇 가지 추가 매개 변수가 전달됩니다.

* **콘텐츠 저장 작업** (더 이상 사용되지 않음): `contentPath`—제출된 데이터가 저장되는 저장소의 노드 경로가 전달됩니다.

* **PDF 저장 작업** (더 이상 사용되지 않음): `contentPath`- PDF 파일을 저장소에 저장하는 노드 경로 및 전송된 데이터 중 하나가 전달됩니다.

* **Forms 작업 과정에 제출**:양식 워크플로우에서 반환된 출력 매개 변수가 전달됩니다.

* **REST 끝점에 제출**:in-field에서 매개 변수 매핑에 추가된 매개 변수가 전달됩니다. `status` 및  `owner` 매개 변수는 이 전송 작업에서 전달되지 않습니다. 자세한 내용은 [REST에 제출 종단점의 제출 작업 ](../../forms/using/configuring-submit-actions.md) 구성을 참조하십시오.

