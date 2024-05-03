---
title: HTML5 양식에서 액세스 가능한 복잡한 표 만들기
description: HTML5 양식에서 액세스 가능한 테이블을 만드는 방법을 알아봅니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# HTML5 양식에서 액세스 가능한 복잡한 표 만들기 {#create-accessible-complex-tables-in-html-forms}

HTML5 Forms의 기본 테이블 구현에서는 HTML DIV 요소를 사용하여 테이블을 렌더링합니다. 렌더링에는 접근성 요구 사항을 충족하기 위해 ARIA 역할을 사용하는 작업이 포함됩니다.

데이터 테이블에 사용되는 ARIA 역할을 완전히 지원하지 않는 화면 판독기의 접근성 문제를 방지하기 위해 HTML5 Forms에서는 테이블에 대한 대체 렌디션을 제공합니다. 이러한 테이블은 디자이너에 소개된 새로운 테이블 형식을 기반으로 합니다.

* 행 머리글
* 행 범위

HTML5 Forms에서 새 형식을 사용하려면 표를 복잡하게 표시합니다. 표를 복잡하게 표시하려면 을 추가합니다 `extras` 태그는 다음과 같이 테이블 하위 양식의 XML 원본에 있습니다.

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

(으)로 표시된 테이블 *complexTable* 기본 HTML 렌디션을 따르고 특정 화면 판독기에 대해 더 나은 접근성 지원을 제공합니다.  행 범위를 만들려면 동일한 열에서 표의 연속 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 를 클릭합니다 **[!UICONTROL 셀 병합]**.

>[!NOTE]
>
>행 범위 만들기는 맨 왼쪽 셀에서만 작동합니다.

행을 행 머리글로 표시하려면 행의 모든 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 머리글 표시]**.

셀을 열 머리글로 표시하려면 열에서 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 를 클릭합니다 **[!UICONTROL 머리글 표시]**.

새로운 의 제한 사항 *AccessibleTable* 형식:

* 테이블에서 rowspan을 사용하는 경우 성장 가능 필드에 대한 지원 부족
* 중첩된 표(표 셀 내의 표)는 지원되지 않습니다.
* rowspan 지원은 헤더 행 및 헤더 셀로 제한됩니다
* 일반 테이블로 지원이 제한됩니다.
* rowspan >이 1인 테이블의 데이터 미리 채우기는 지원되지 않음
