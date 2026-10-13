---
title: HTML5 양식에서 접근성 높은 복잡한 테이블 만들기
description: HTML5 Forms에서 액세스 가능한 테이블을 만드는 방법을 알아봅니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms,Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 5%
---
# HTML5 양식에서 접근성 높은 복잡한 테이블 만들기 {#create-accessible-complex-tables-in-html-forms}

HTML5 Forms의 기본 테이블 구현에서는 HTML DIV 요소를 사용하여 테이블을 렌더링합니다. 렌더링에는 접근성 요구 사항을 충족하기 위해 ARIA 역할을 사용하는 작업이 포함됩니다.

데이터 테이블에 사용되는 ARIA 역할을 완전히 지원하지 않는 화면 판독기의 접근성 문제를 방지하기 위해 HTML5 Forms은 테이블에 대한 대체 렌디션을 제공합니다. 이러한 테이블은 Designer에서 도입된 새로운 테이블 형식을 기반으로 하며,

* 행 머리글
* 행 범위

HTML5 Forms에서 새 형식을 사용하려면 표를 복잡하게 표시하십시오. 테이블을 복잡하게 표시하려면 다음과 같이 테이블 하위 양식의 XML 원본에 `extras` 태그를 추가하십시오.

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

*complexTable*(으)로 표시된 테이블은 기본 HTML 렌디션을 따르며 특정 화면 판독기에 더 나은 접근성을 지원합니다.  행 범위를 만들려면 동일한 열에서 표의 연속 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 셀 병합]**&#x200B;을 클릭합니다.

>[!NOTE]
>
>행 범위 만들기는 맨 왼쪽 셀에서만 작동합니다.

행을 행 머리글로 표시하려면 행의 모든 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 머리글 표시]**&#x200B;를 클릭합니다.

셀을 열 머리글로 표시하려면 열에서 셀을 선택하고 선택 항목을 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 머리글 표시]**&#x200B;를 클릭합니다.

새 *AccessibleTable* 형식의 제한 사항:

* 테이블에서 rowspan을 사용하는 경우 성장 가능 필드에 대한 지원 부족
* 중첩된 표(표 셀 내의 표)는 지원되지 않습니다.
* rowspan 지원은 헤더 행 및 헤더 셀로 제한됩니다
* 일반 테이블로 지원이 제한됩니다.
* rowspan >이 1인 테이블의 데이터 미리 채우기는 지원되지 않음
