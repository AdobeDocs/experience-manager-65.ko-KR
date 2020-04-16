---
title: HTML5 양식에 액세스 가능한 복잡한 표 만들기
seo-title: HTML5 양식에 액세스 가능한 복잡한 표 만들기
description: HTML5 양식에서 액세스 가능한 표를 만드는 방법을 알아봅니다.
seo-description: HTML5 양식에서 액세스 가능한 표를 만드는 방법을 알아봅니다.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# HTML5 양식에 액세스 가능한 복잡한 표 만들기 {#create-accessible-complex-tables-in-html-forms}

The default implementation of tables in HTML5 Forms uses HTML DIV elements to render a table. Rendering involves using ARIA roles to satisfy the accessibility requirements.

To avoid accessibility issues with screen-readers which do not fully support the ARIA-roles used with data-tables, HTML5 Forms provides an alternate rendition for the tables. These tables are based on the new table format introduced in Designer which also supports:

* Row Headers
* Row-span

To use the new format in HTML5 Forms, mark the table as complex. 표를 복합 폼으로 표시하려면 다음과 같이 테이블 하위 폼의 XML 소스에 `extras` 태그를 추가하십시오.

```
</extras>
 <text name="complexTable">1</text>
 </extras>
```

complexTable로 표시된 *표는* 기본 HTML 변환을 따르며 특정 화면 판독기에 대한 향상된 액세스 가능성 지원을 제공합니다.  행 범위를 만들려면 같은 열에서 표의 연속 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 셀 **[!UICONTROL 병합을 클릭합니다]**.

>[!NOTE]
>
>행 범위 만들기는 맨 왼쪽 셀에만 작동합니다.

행을 행 머리글로 표시하려면 행의 모든 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 머리글 표시를 **[!UICONTROL 클릭합니다]**.

셀을 열 머리글로 표시하려면 열의 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 머리글 표시를 **[!UICONTROL 클릭합니다]**.

새로운 AccessibleTable *형식의* 제한 사항:

* 테이블에서 행 범위를 사용하는 경우 확장 가능한 필드를 지원하지 않음
* 중첩된 표에 대한 지원 없음(표 셀 내의 표)
* 행 범위 지원은 머리글 행 및 머리글 셀로 제한됩니다.
* 지원은 일반 테이블로 제한됩니다.
* 행 범위 > 1이 있는 표의 데이터 프리플라이트 지원 안 함

