---
title: HTML5 양식에서 액세스 가능한 복잡한 표 만들기
seo-title: HTML5 양식에서 액세스 가능한 복잡한 표 만들기
description: HTML5 양식에서 액세스 가능한 표를 만드는 방법을 알아봅니다.
seo-description: HTML5 양식에서 액세스 가능한 표를 만드는 방법을 알아봅니다.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---


# HTML5 양식 {#create-accessible-complex-tables-in-html-forms}에서 액세스 가능한 복잡한 표 만들기

HTML5 Forms에서 표의 기본 구현은 HTML DIV 요소를 사용하여 표를 렌더링합니다. 렌더링에는 액세스 가능성 요구 사항을 충족하기 위해 ARIA 역할을 사용하는 것이 포함됩니다.

데이터 테이블과 함께 사용되는 ARIA 역할을 완벽하게 지원하지 않는 화면 판독기에서 액세스 가능성 문제를 방지하기 위해 HTML5 Forms은 표에 대한 대체 변환을 제공합니다. 다음 표는 Designer에서 도입된 새 표 형식이며 다음과 같은 기능도 지원합니다.

* 행 머리글
* 행 범위

HTML5 Forms에서 새 형식을 사용하려면 표를 복잡하게 표시합니다. 표를 복잡하게 표시하려면 다음과 같이 테이블 하위 양식의 XML 소스에 `extras` 태그를 추가합니다.

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

*complexTable*&#x200B;으로 표시된 표는 기본 HTML 변환을 따르고 특정 화면 판독기에 대한 액세스 가능성 지원을 제공합니다.  행 범위를 만들려면 같은 열에서 표의 연속적인 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 셀 병합]**&#x200B;을 클릭합니다.

>[!NOTE]
>
>행 범위를 만드는 것은 가장 왼쪽 셀에만 작동합니다.

행을 행 머리글로 표시하려면 행의 모든 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 머리글 표시]**&#x200B;를 클릭합니다.

셀을 열 머리글로 표시하려면 열의 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 머리글 표시]**&#x200B;를 클릭합니다.

새 *AccessibleTable* 형식의 제한 사항:

* 표에서 행 범위를 사용하는 경우 확장 가능한 필드를 지원하지 않음
* 중첩된 표에 대한 지원 없음(표 셀 내의 표)
* 행 범위에 대한 지원은 머리글 행 및 머리글 셀로 제한됩니다.
* 지원은 일반 테이블로 제한됩니다.
* 행 범위 > 1이 있는 표의 데이터 프리플라이트 기능은 지원되지 않습니다.

