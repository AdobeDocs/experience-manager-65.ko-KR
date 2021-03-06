---
title: 레이아웃 모드를 사용하여 적응형 양식의 구성 요소 크기 조정
description: '레이아웃 모드에서 사용할 수 있는 응답형 그리드를 사용하여 구성 요소의 위치를 정의합니다 '
feature: 적응형 양식
exl-id: 5cf76cb1-c92c-4aed-9945-37494fef2d29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# 레이아웃 모드를 사용하여 구성 요소 {#use-layout-mode-to-resize-components} 크기 조정

적응형 양식 작성 인터페이스를 사용하면 레이아웃 모드를 사용하여 구성 요소의 크기를 조정할 수 있습니다. 열 내에 파란색 점을 드래그하여 놓아 구성 요소를 배치할 시작 및 종료 점을 정의합니다. 응답형 그리드 내에서 구성 요소를 탭하면 파란색 점이 표시됩니다. 응답형 격자는 12개의 동일한 열로 구성됩니다. 대체 열의 흰색 및 파란색 음영은 한 열과 다른 열을 구별합니다.

레이아웃 모드를 사용하여 데스크톱, 태블릿, 휴대폰 및 기타 작은 장치와 같은 모든 장치 유형에 대한 구성 요소의 크기를 조정할 수 있습니다. 태블릿은 데스크탑 버전에서 레이아웃 구성을 자동으로 파생하고 작은 장치는 휴대폰에서 레이아웃 구성을 파생시킵니다. 그러나 자동으로 파생된 구성을 재정의하여 각 장치 유형에 대해 다른 구성을 정의할 수 있습니다.

## 레이아웃 모드 {#access-layout-mode} 액세스

**미리 보기** 옵션 옆에 있는 적응형 양식 작성 인터페이스 맨 위에 표시되는 드롭다운 목록에서 **레이아웃**&#x200B;을 선택합니다. 양식은 레이아웃 모드로 표시됩니다.

1. AEM 작성자 인스턴스에 로그인하고 **Adobe Experience Manager** > **Forms** > **Forms 및 문서**&#x200B;로 이동합니다.
1. 새 양식을 만들거나 기존 [적응형 양식](../../forms/using/creating-adaptive-form.md)을 엽니다.
1. **미리 보기** 옵션 옆의 맨 위에 표시되는 드롭다운 목록에서 **레이아웃**&#x200B;을 선택합니다. 양식은 레이아웃 모드로 표시됩니다.

   ![레이아웃 모드](assets/layout_mode_ic_new.png)

## 구성 요소 크기 조정 {#resize-components}

1. 레이아웃 모드에서 구성 요소를 탭하여 크기를 조정합니다. 응답형 그리드의 시작 및 끝에 파란색 점이 표시됩니다.
1. 파란색 점을 드래그하여 놓아 응답형 그리드에서 구성 요소의 위치를 정의합니다.

   ![레이아웃 모드를 사용한 크기 조정](assets/layout_mode_resize_new_updated1.png)

   구성 요소를 탭한 후 표시되는 도구 모음은 다음 옵션으로 구성됩니다.

   * **[!UICONTROL 상위]**:구성 요소의 상위 항목을 선택합니다.
   * **[!UICONTROL 중단점 레이아웃 되돌리기]**:모든 크기 변경 사항을 실행 취소하고 구성 요소에 기본 레이아웃을 적용합니다.
   * **[!UICONTROL 새 라인으로 이동]**:동일한 라인 내에 여러 구성 요소가 있는 경우 구성 요소를 다음 라인으로 이동합니다.

   또한 패널 수준에서 **[!UICONTROL 중단점 레이아웃 되돌리기]**( ![중단점 되돌리기](assets/reverttopreviouslypublishedversion.png)) 옵션을 사용하여 모든 크기 조정 변경 사항을 실행 취소할 수 있습니다.

   >[!NOTE]
   >
   >레이아웃 모드를 사용하여 표 열, 도구 모음, 도구 모음 단추 및 대상 영역 구성 요소의 크기를 조정할 수 없습니다. 스타일 모드를 사용하여 이러한 구성 요소의 크기를 조정할 수 있습니다.

### 예 {#example}

**목표:** 표 구성 요소와 이미지 구성 요소를 삽입하고 적응형 양식으로 나란히 배치하려는 경우.

1. 적응형 양식의 편집 모드를 사용하여 테이블 및 이미지 구성 요소를 삽입합니다. 이미지 구성 요소는 표 구성 요소 뒤에 표시됩니다.
1. 레이아웃 모드로 전환하고 표 구성 요소를 탭합니다. 구성 요소 크기를 조정할 파란색 점은 1 및 12열에 표시됩니다.
1. 열 12에 있는 파란색 점을 응답형 그리드의 열 6으로 끌어다 놓습니다.

   ![테이블의 끝점 정의](assets/layout_mode_end_point_table_new.png)

1. 마찬가지로 이미지 구성 요소를 선택하고 1열에 있는 파란색 점을 응답형 격자의 열 7로 드래그하여 놓습니다. 테이블 및 이미지 구성 요소가 서로 평행하게 표시됩니다.

   ![표 및 이미지가 레이아웃 모드에서 동시에 표시됨](assets/table_image_parallel_new.png)

   이미지 구성 요소를 선택하고 도구 모음에서 사용할 수 있는 **새 라인으로 이동** 옵션을 탭하여 이미지 구성 요소를 다음 라인으로 이동할 수 있습니다.

## 패널 크기 조정 {#resize-panels-layout-mode}

개별 구성 요소 대신 전체 패널의 크기를 조정하려면 다음 단계를 실행합니다.

1. 패널에서 크기를 조정할 구성 요소를 탭하고 ![부모 선택](assets/select_parent_icon.svg) 을 선택한 다음, 패널이 구성 요소의 바로 위 상위 패널인 경우 드롭다운 목록에서 첫 번째 옵션을 선택합니다.

   응답형 그리드의 시작 및 끝에 파란색 점이 표시됩니다.

1. 파란색 점을 드래그하여 놓아 응답형 그리드에서 패널의 위치를 정의합니다.
1단계와 2단계를 반복하고 ![상위 선택](assets/float_to_new_line_icon.svg)을 선택하여 크기가 조정된 패널을 다음 행으로 이동할 수 있습니다.

## 패널에 대한 다중 열 레이아웃 정의

다음 단계를 실행하여 패널의 열 수를 정의합니다.

1. **[!UICONTROL 편집]** 모드에서 패널을 탭하고 ![구성](assets/configure_icon.png)을 선택한 다음, **[!UICONTROL 패널 레이아웃]** 드롭다운 목록에서 탐색 없이 페이지에서 **[!UICONTROL 응답형 - 모든 항목 선택.]**

1. ![저장](assets/save_icon.svg)을 눌러 속성을 저장합니다.

1. **[!UICONTROL 레이아웃]** 모드에서 패널의 구성 요소 중 하나를 탭하고 ![상위 선택](assets/select_parent_icon.svg)을 선택하고 패널을 선택합니다.

1. ![다중 열](assets/multi-column.svg)을 탭하고 드롭다운 목록에서 열 수를 선택합니다. 열 수는 1부터 12까지입니다. 패널은 다중 열 레이아웃으로 분할됩니다.

![레이아웃 모드에서 다중 열](assets/multi-column-layout.png)

## 이전 반응형 레이아웃을 위한 새로운 응답형 그리드 활성화 {#enableresponsivegrid}

AEM Forms 6.4 이하 버전을 사용하여 만드는 양식에 대해 새로운 반응형 그리드를 활성화하여 구성 요소의 크기를 조정할 수 있습니다.

>[!NOTE]
>
>새 응답형 그리드로 전환하면 양식에 사용된 구성 요소에 이미 정의된 레이아웃 속성이 무시됩니다.

새 응답형 그리드를 활성화하려면 다음 단계를 수행하십시오.

1. **미리 보기** 옵션 옆의 맨 위에 표시되는 드롭다운 목록에서 **레이아웃**&#x200B;을 선택합니다. 레이아웃 모드 활성화 확인이 표시됩니다.
1. **Yes** 를 탭하여 양식에 대해 **레이아웃** 모드를 활성화합니다.

### 새 응답형 레이아웃 {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}을 사용하여 이전 조각을 적응형 양식에 포함합니다

적응형 양식에 대한 새로운 응답형 레이아웃을 사용하면 이전 응답형 레이아웃이 포함된 적응형 양식 조각을 양식에 추가할 수 있습니다. 하지만 새 레이아웃은 조각에서 사용되는 구성 요소에 이미 정의된 레이아웃 속성을 삭제합니다. 레이아웃 모드로 전환하여 조각에 사용되는 구성 요소의 레이아웃 속성을 정의할 수 있습니다.

### 새 응답형 레이아웃이 있는 조각을 이전 적응형 양식 {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}에 포함

이전 응답형 레이아웃이 있는 적응형 양식에 새 응답형 레이아웃으로 조각을 포함하는 경우 양식에 대한 레이아웃 모드를 활성화하여 조각을 다시 포함하라는 메시지가 표시됩니다.

레이아웃 모드를 활성화하려면 **미리 보기** 옵션 옆에 있는 드롭다운 목록에서 **레이아웃**&#x200B;을 선택하고 **예**&#x200B;를 탭하여 확인합니다. **편집** 모드 를 선택하여 조각을 다시 포함합니다.

## 이전 응답형 레이아웃 {#disable-layout-mode-for-forms-with-old-responsive-layout}이 있는 양식의 레이아웃 모드를 비활성화합니다

양식에 사용된 템플릿에 대한 속성을 편집하여 이전 응답형 레이아웃이 있는 양식의 레이아웃 모드를 비활성화할 수 있습니다.

레이아웃 모드를 비활성화하려면 다음 단계를 수행하십시오.

1. **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL 템플릿]**&#x200B;을 선택하고 양식에 사용된 템플릿을 **[!UICONTROL 편집]** 모드로 엽니다.
1. 왼쪽 창에서 문서 컨테이너를 선택하고 **[!UICONTROL 정책을 누릅니다.]**

   ![레이아웃 모드 비활성화](assets/policy_disable_layout_mode.png)

1. **[!UICONTROL 레이아웃 설정]** 탭을 탭하고 **[!UICONTROL 레이아웃 모드 비활성화]**&#x200B;를 선택합니다.
1. ![변경 내용 저장](assets/save_icon.png)을 눌러 템플릿 속성을 저장합니다.
