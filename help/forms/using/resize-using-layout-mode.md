---
title: 레이아웃 모드를 사용하여 적응형 양식의 구성 요소 크기 조정
description: 레이아웃 모드에서 사용할 수 있는 응답형 그리드를 사용하여 구성 요소의 위치를 정의합니다.
feature: Adaptive Forms,Foundation Components
exl-id: 5cf76cb1-c92c-4aed-9945-37494fef2d29
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 6%

---

# 레이아웃 모드를 사용하여 구성 요소 크기 변경 {#use-layout-mode-to-resize-components}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/resize-using-layout-mode.html?) |
| AEM 6.5 | 이 문서 |


적응형 양식 작성 인터페이스를 사용하면 레이아웃 모드를 사용하여 구성 요소의 크기를 조정할 수 있습니다. 열 내에 파란색 점을 드래그 앤 드롭하여 구성 요소를 배치할 시작점과 끝점을 정의합니다. 응답형 격자 내에서 구성 요소를 탭하면 파란색 점이 표시됩니다. 응답형 격자는 12개의 동일한 열로 구성됩니다. 대체 열의 흰색과 파란색 색상 음영은 한 열을 다른 열과 구분합니다.

레이아웃 모드를 사용하여 데스크탑, 태블릿, 휴대폰 및 기타 작은 장치와 같은 모든 장치 유형에 대한 구성 요소의 크기를 조정할 수 있습니다. 태블릿은 자동으로 데스크탑 버전에서 레이아웃 구성을 파생시키고 작은 장치는 전화에서 레이아웃 구성을 파생시킵니다. 그러나 자동으로 파생된 구성을 재정의하여 각 장치 유형에 대해 다른 구성을 정의할 수 있습니다.

## 레이아웃 모드 액세스 {#access-layout-mode}

**미리 보기** 옵션 옆에 있는 적응형 양식 작성 인터페이스 맨 위에 표시되는 드롭다운 목록에서 **레이아웃**&#x200B;을(를) 선택합니다. 양식이 레이아웃 모드로 표시됩니다.

1. AEM 작성자 인스턴스에 로그인하고 **Adobe Experience Manager** > **Forms** > **Forms 및 문서**&#x200B;로 이동합니다.
1. [적응형 양식](../../forms/using/creating-adaptive-form.md)을 만들거나 기존 양식을 여십시오.
1. **미리 보기** 옵션 옆 맨 위에 표시되는 드롭다운 목록에서 **레이아웃**&#x200B;을 선택합니다. 양식이 레이아웃 모드로 표시됩니다.

   ![레이아웃 모드](assets/layout_mode_ic_new.png)

## 구성 요소 크기 조정 {#resize-components}

1. 레이아웃 모드에서 크기를 조정할 구성 요소를 선택합니다. 파란색 점은 응답형 격자의 시작과 끝에 표시됩니다.
1. 파란색 점을 드래그 앤 드롭하여 응답형 격자에서 구성 요소의 위치를 정의합니다.

   ![레이아웃 모드를 사용하여 크기 조정](assets/layout_mode_resize_new_updated1.png)

   구성 요소를 탭한 후 표시되는 도구 모음은 다음 옵션으로 구성됩니다.

   * **[!UICONTROL 상위]**: 구성 요소의 상위 항목을 선택하십시오.
   * **[!UICONTROL 중단점 레이아웃 되돌리기]**: 모든 크기 변경 내용을 실행 취소하고 기본 레이아웃을 구성 요소에 적용합니다.
   * **[!UICONTROL 새 줄로 이동]**: 같은 줄에 여러 구성 요소가 있는 경우 구성 요소를 다음 줄로 이동합니다.

   또한 패널 수준에서 **[!UICONTROL 중단점 레이아웃 되돌리기]**(![중단점 되돌리기](assets/reverttopreviouslypublishedversion.png)) 옵션을 사용하여 모든 크기 조정 변경 내용을 실행 취소할 수 있습니다.

   >[!NOTE]
   >
   >레이아웃 모드를 사용하여 표 열, 도구 모음, 도구 모음 단추 및 대상 영역 구성 요소의 크기를 조정할 수 없습니다. 이러한 구성 요소의 크기를 조정하려면 스타일 모드를 사용하십시오.

### 예 {#example}

**목표:** 테이블 구성 요소와 이미지 구성 요소를 삽입하고 적응형 양식에서 서로 평행하게 배치하려고 합니다.

1. 적응형 양식의 편집 모드를 사용하여 표 및 이미지 구성 요소를 삽입합니다. 이미지 구성 요소가 테이블 구성 요소 뒤에 표시됩니다.
1. 레이아웃 모드로 전환하고 테이블 구성 요소를 선택합니다. 구성 요소 크기를 조정하기 위한 파란색 점이 1열과 12열에 표시됩니다.
1. 12열에서 응답형 격자의 6열로 파란색 점을 드래그 앤 드롭합니다.

   ![테이블의 끝점을 정의합니다](assets/layout_mode_end_point_table_new.png)

1. 마찬가지로 이미지 구성 요소를 선택하고 1열에서 응답형 격자의 7열로 파란색 점을 드래그 앤 드롭합니다. 테이블 및 이미지 구성 요소는 서로 평행하게 표시됩니다.

   레이아웃 모드에서 ![테이블 및 이미지를 동시에 표시](assets/table_image_parallel_new.png)

   이미지 구성 요소를 선택하고 도구 모음에서 **새 줄로 이동** 옵션을 선택하여 이미지 구성 요소를 다음 줄로 이동할 수 있습니다.

## 패널 크기 조정 {#resize-panels-layout-mode}

개별 구성 요소 대신 전체 패널의 크기를 조정하려면 다음 단계를 수행하십시오.

1. 패널에서 크기를 조정할 구성 요소를 선택하고 ![상위 선택](assets/select_parent_icon.svg)을 선택한 다음 패널이 구성 요소의 바로 상위 패널인 경우 드롭다운 목록에서 첫 번째 옵션을 선택합니다.

   파란색 점은 응답형 격자의 시작과 끝에 표시됩니다.

1. 파란색 점을 드래그 앤 드롭하여 응답형 격자에서 패널의 위치를 정의합니다.
1단계와 2단계를 반복하고 ![상위 선택](assets/float_to_new_line_icon.svg)을 선택하여 크기 조정된 패널을 다음 줄로 이동할 수 있습니다.

## 패널의 다중 열 레이아웃 정의

다음 단계를 실행하여 패널의 열 수를 정의합니다.

1. **[!UICONTROL 편집]** 모드에서 패널을 선택하고 ![구성](assets/configure_icon.png)을 선택한 다음 **[!UICONTROL 패널 레이아웃]** 드롭다운 목록에서 **[!UICONTROL 응답형 - 탐색 없이 페이지에 있는 모든 항목]** 옵션을 선택합니다.

1. 속성을 저장하려면 ![저장](assets/save_icon.svg)을(를) 선택하십시오.

1. **[!UICONTROL 레이아웃]** 모드에서 패널의 구성 요소를 선택하고 ![상위 선택](assets/select_parent_icon.svg)을 선택한 다음 패널을 선택합니다.

1. ![다중 열](assets/multi-column.svg)을(를) 선택하고 드롭다운 목록에서 열 수를 선택합니다. 열의 수는 1에서 12 사이일 수 있습니다. 패널은 여러 열로 구성된 레이아웃으로 나뉩니다.

![레이아웃 모드의 다중 열](assets/multi-column-layout.png)

## 이전 반응형 레이아웃에 새 반응형 그리드 활성화 {#enableresponsivegrid}

AEM Forms 6.4 이하 버전을 사용하여 만든 양식의 새 반응형 그리드를 활성화하여 구성 요소의 크기를 조정할 수 있습니다.

>[!NOTE]
>
>새 반응형 격자로 전환하면 양식에 사용된 구성 요소에 대해 이미 정의된 레이아웃 속성이 삭제됩니다.

새 응답형 격자를 활성화하려면 다음 단계를 수행하십시오.

1. **미리 보기** 옵션 옆 맨 위에 표시되는 드롭다운 목록에서 **레이아웃**&#x200B;을 선택합니다. 레이아웃 모드 활성화 확인이 표시됩니다.
1. 양식에 대해 **레이아웃** 모드를 활성화하려면 **예**&#x200B;를 선택하십시오.

### 새 반응형 레이아웃을 통해 적응형 양식에 이전 단편 포함 {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

적응형 양식에 대한 새 반응형 레이아웃을 사용하면 이전 반응형 레이아웃이 포함된 적응형 양식 조각을 양식에 추가할 수 있습니다. 그러나 새 레이아웃은 조각에 사용된 구성 요소에 대해 이미 정의된 레이아웃 속성을 삭제합니다. 레이아웃 모드로 전환하여 조각에 사용된 구성 요소의 레이아웃 속성을 정의할 수 있습니다.

### 이전 적응형 양식에 새 반응형 레이아웃이 포함된 단편 포함 {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

새 반응형 레이아웃이 포함된 조각을 이전 반응형 레이아웃이 있는 적응형 양식에 포함하는 경우, 양식에 대해 레이아웃 모드를 활성화하고 조각을 다시 포함할 것인지 묻는 메시지가 표시됩니다.

레이아웃 모드를 활성화하려면 **미리 보기** 옵션 옆에 맨 위에 표시되는 드롭다운 목록에서 **레이아웃**&#x200B;을(를) 선택하고 **예**&#x200B;를(를) 선택하여 확인하십시오. 조각을 다시 포함하려면 **편집** 모드를 선택하십시오.

## 이전 반응형 레이아웃이 있는 양식의 레이아웃 모드 비활성화 {#disable-layout-mode-for-forms-with-old-responsive-layout}

양식에 사용된 템플릿의 속성을 편집하여 이전 반응형 레이아웃이 있는 양식의 레이아웃 모드를 비활성화할 수 있습니다.

레이아웃 모드를 비활성화하려면 다음 단계를 수행하십시오.

1. **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL 서식 파일]**&#x200B;을 선택하고 **[!UICONTROL 편집]** 모드에서 양식에 사용된 서식 파일을 엽니다.
1. 왼쪽 창에서 문서 컨테이너를 선택하고 **[!UICONTROL 정책을 선택합니다.]**

   ![레이아웃 모드 비활성화](assets/policy_disable_layout_mode.png)

1. **[!UICONTROL 레이아웃 설정]** 탭을 선택하고 **[!UICONTROL 레이아웃 모드 비활성화]**&#x200B;를 선택합니다.
1. 템플릿 속성을 저장하려면 ![변경 내용 저장](assets/save_icon.png)을 선택합니다.
