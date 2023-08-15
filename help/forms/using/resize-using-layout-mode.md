---
title: 레이아웃 모드를 사용하여 적응형 양식의 구성 요소 크기 조정
description: 레이아웃 모드에서 사용할 수 있는 응답형 그리드를 사용하여 구성 요소의 위치를 정의합니다.
feature: Adaptive Forms
exl-id: 5cf76cb1-c92c-4aed-9945-37494fef2d29
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 7%

---

# 레이아웃 모드를 사용하여 구성 요소 크기 변경 {#use-layout-mode-to-resize-components}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [코어 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/resize-using-layout-mode.html?) |
| AEM 6.5 | 이 문서 |


적응형 양식 작성 인터페이스를 사용하면 레이아웃 모드를 사용하여 구성 요소의 크기를 조정할 수 있습니다. 열 내에 파란색 점을 드래그 앤 드롭하여 구성 요소를 배치할 시작점과 끝점을 정의합니다. 응답형 격자 내에서 구성 요소를 탭하면 파란색 점이 표시됩니다. 응답형 격자는 12개의 동일한 열로 구성됩니다. 대체 열의 흰색과 파란색 색상 음영은 한 열을 다른 열과 구분합니다.

레이아웃 모드를 사용하여 데스크탑, 태블릿, 휴대폰 및 기타 작은 장치와 같은 모든 장치 유형에 대한 구성 요소의 크기를 조정할 수 있습니다. 태블릿은 자동으로 데스크탑 버전에서 레이아웃 구성을 파생시키고 작은 장치는 전화에서 레이아웃 구성을 파생시킵니다. 그러나 자동으로 파생된 구성을 재정의하여 각 장치 유형에 대해 다른 구성을 정의할 수 있습니다.

## 레이아웃 모드 액세스 {#access-layout-mode}

선택 **레이아웃** 적응형 양식 작성 인터페이스 옆에 나타나는 드롭다운 목록에서 **미리 보기** 옵션을 선택합니다. 양식이 레이아웃 모드로 표시됩니다.

1. AEM 작성자 인스턴스에 로그인하고 다음으로 이동합니다. **Adobe Experience Manager** > **Forms** > **Forms 및 문서**.
1. 새로 만들기 또는 기존 열기 [적응형 양식](../../forms/using/creating-adaptive-form.md).
1. 선택 **레이아웃** (이)가 표시되는 드롭다운 목록에서 **미리 보기** 옵션을 선택합니다. 양식이 레이아웃 모드로 표시됩니다.

   ![레이아웃 모드](assets/layout_mode_ic_new.png)

## 구성 요소 크기 조정 {#resize-components}

1. 레이아웃 모드에서 구성 요소를 탭하여 크기를 조정합니다. 파란색 점은 응답형 격자의 시작과 끝에 표시됩니다.
1. 파란색 점을 드래그 앤 드롭하여 응답형 격자에서 구성 요소의 위치를 정의합니다.

   ![레이아웃 모드를 사용한 크기 조정](assets/layout_mode_resize_new_updated1.png)

   구성 요소를 탭한 후 표시되는 도구 모음은 다음 옵션으로 구성됩니다.

   * **[!UICONTROL 상위]**: 구성 요소의 상위 항목을 선택합니다.
   * **[!UICONTROL 중단점 레이아웃 되돌리기]**: 모든 크기 변경 내용을 실행 취소하고 구성 요소에 기본 레이아웃을 적용합니다.
   * **[!UICONTROL 새 라인으로 이동]**: 동일한 행 내에 여러 구성 요소가 있는 경우 구성 요소를 다음 행으로 이동합니다.

   다음을 사용할 수도 있습니다 **[!UICONTROL 중단점 레이아웃 되돌리기]** ( ![중단점 되돌리기](assets/reverttopreviouslypublishedversion.png)) 모든 크기 변경 내용을 실행 취소할 수 있는 패널 수준의 옵션입니다.

   >[!NOTE]
   >
   >레이아웃 모드를 사용하여 표 열, 도구 모음, 도구 모음 단추 및 대상 영역 구성 요소의 크기를 조정할 수 없습니다. 이러한 구성 요소의 크기를 조정하려면 스타일 모드를 사용하십시오.

### 예 {#example}

**목표:** 테이블 구성 요소와 이미지 구성 요소를 삽입하고 적응형 양식에서 서로 평행하게 배치하려고 합니다.

1. 적응형 양식의 편집 모드를 사용하여 표 및 이미지 구성 요소를 삽입합니다. 이미지 구성 요소가 테이블 구성 요소 뒤에 표시됩니다.
1. 레이아웃 모드로 전환하고 표 구성 요소를 탭합니다. 구성 요소 크기를 조정하기 위한 파란색 점이 1열과 12열에 표시됩니다.
1. 12열에서 응답형 격자의 6열로 파란색 점을 드래그 앤 드롭합니다.

   ![테이블의 끝점 정의](assets/layout_mode_end_point_table_new.png)

1. 마찬가지로 이미지 구성 요소를 선택하고 1열에서 응답형 격자의 7열로 파란색 점을 드래그 앤 드롭합니다. 테이블 및 이미지 구성 요소는 서로 평행하게 표시됩니다.

   ![레이아웃 모드에서 병렬 표 및 이미지](assets/table_image_parallel_new.png)

   이미지 구성 요소를 선택하고 **새 라인으로 이동** 도구 모음에서 다음 줄로 이미지 구성 요소를 이동할 수 있는 옵션을 사용할 수 있습니다.

## 패널 크기 조정 {#resize-panels-layout-mode}

개별 구성 요소 대신 전체 패널의 크기를 조정하려면 다음 단계를 수행하십시오.

1. 패널에서 크기를 조정할 구성 요소를 탭하고 선택합니다 ![상위 선택](assets/select_parent_icon.svg)패널 이 구성 요소의 바로 상위 항목인 경우 드롭다운 목록에서 첫 번째 옵션을 선택합니다.

   파란색 점은 응답형 격자의 시작과 끝에 표시됩니다.

1. 파란색 점을 드래그 앤 드롭하여 응답형 격자에서 패널의 위치를 정의합니다.
1단계와 2단계를 반복하고 를 선택할 수 있습니다 ![상위 선택](assets/float_to_new_line_icon.svg) 크기 조정된 패널을 다음 줄로 이동합니다.

## 패널의 다중 열 레이아웃 정의

다음 단계를 실행하여 패널의 열 수를 정의합니다.

1. 위치 **[!UICONTROL 편집]** 모드, 패널을 탭하고 선택 ![구성](assets/configure_icon.png), 및 선택 **[!UICONTROL 응답형 - 탐색 없이 페이지에 있는 모든 항목]** 옵션에서 **[!UICONTROL 패널 레이아웃]** 드롭다운 목록입니다.

1. ![저장](assets/save_icon.svg)을 탭하여 변경 내용을 저장합니다.

1. 다음에서 **[!UICONTROL 레이아웃]** 모드, 패널에서 구성 요소 중 하나를 탭하고 ![상위 선택](assets/select_parent_icon.svg)을 누르고 패널을 선택합니다.

1. 누르기 ![다중 열](assets/multi-column.svg) 드롭다운 목록에서 열 수를 선택합니다. 열의 수는 1에서 12 사이일 수 있습니다. 패널은 여러 열로 구성된 레이아웃으로 나뉩니다.

![레이아웃 모드의 다중 열](assets/multi-column-layout.png)

## 이전 반응형 레이아웃에 새 반응형 그리드 활성화 {#enableresponsivegrid}

AEM Forms 6.4 이하 버전을 사용하여 만든 양식의 새 반응형 그리드를 활성화하여 구성 요소의 크기를 조정할 수 있습니다.

>[!NOTE]
>
>새 반응형 격자로 전환하면 양식에 사용된 구성 요소에 대해 이미 정의된 레이아웃 속성이 삭제됩니다.

새 응답형 격자를 활성화하려면 다음 단계를 수행하십시오.

1. 선택 **레이아웃** (이)가 표시되는 드롭다운 목록에서 **미리 보기** 옵션을 선택합니다. 레이아웃 모드 활성화 확인이 표시됩니다.
1. 누르기 **예** 을(를) 활성화하려면 **레이아웃** 를 입력합니다.

### 새 반응형 레이아웃을 통해 적응형 양식에 이전 단편 포함 {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

적응형 양식에 대한 새 반응형 레이아웃을 사용하면 이전 반응형 레이아웃이 포함된 적응형 양식 조각을 양식에 추가할 수 있습니다. 그러나 새 레이아웃은 조각에 사용된 구성 요소에 대해 이미 정의된 레이아웃 속성을 삭제합니다. 레이아웃 모드로 전환하여 조각에 사용된 구성 요소의 레이아웃 속성을 정의할 수 있습니다.

### 이전 적응형 양식에 새 반응형 레이아웃이 포함된 단편 포함 {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

새 반응형 레이아웃이 포함된 조각을 이전 반응형 레이아웃이 있는 적응형 양식에 포함하는 경우, 양식에 대해 레이아웃 모드를 활성화하고 조각을 다시 포함할 것인지 묻는 메시지가 표시됩니다.

레이아웃 모드를 활성화하려면 **레이아웃** (이)가 표시되는 드롭다운 목록에서 **미리 보기** 옵션 및 탭 **예** 확인할 수 있습니다. 선택 **편집** 를 입력하여 조각을 다시 포함할 수 있습니다.

## 이전 반응형 레이아웃이 있는 양식의 레이아웃 모드 비활성화 {#disable-layout-mode-for-forms-with-old-responsive-layout}

양식에 사용된 템플릿의 속성을 편집하여 이전 반응형 레이아웃이 있는 양식의 레이아웃 모드를 비활성화할 수 있습니다.

레이아웃 모드를 비활성화하려면 다음 단계를 수행하십시오.

1. 선택 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL 템플릿]** 및 의 양식에 사용된 템플릿 열기 **[!UICONTROL 편집]** 모드.
1. 왼쪽 창에서 문서 컨테이너 를 선택하고 을 누릅니다 **[!UICONTROL 정책.]**

   ![레이아웃 모드 비활성화](assets/policy_disable_layout_mode.png)

1. 탭 **[!UICONTROL 레이아웃 설정]** 탭하고 선택 **[!UICONTROL 레이아웃 모드 비활성화]**.
1. 누르기 ![변경 내용 저장](assets/save_icon.png) 템플릿 속성을 저장합니다.
