---
title: 적응형 양식의 오류 메시지 레이아웃 및 위치 지정
seo-title: 적응형 양식의 오류 메시지 레이아웃 및 위치 지정
description: '응용 프로그램의 레이아웃 및 오류 메시지 위치를 사용자 지정할 수 있습니다. '
seo-description: '응용 프로그램의 레이아웃 및 오류 메시지 위치를 사용자 지정할 수 있습니다. '
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 적응형 양식의 오류 메시지 레이아웃 및 위치 지정{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

적응형 양식의 오류 메시지 레이아웃 및 위치를 사용자 지정할 수 있습니다. 다음 사용자 지정을 수행할 수 있습니다.

* 해당 CSS 속성을 변경하지 않고 필드 캡션의 위치 및 레이아웃을 사용자 정의합니다.
* 인라인 오류 메시지 위치 사용자 정의
* 동적 도움말 표시기의 컨텐츠 사용자 정의
* 해당 CSS 속성을 변경하지 않고 필드 구성 요소(캡션, 위젯, 짧은 설명, 긴 설명 및 도움말 표시기 구성 요소)의 위치를 사용자 정의합니다.

## 필드 레이아웃 사용자 정의 {#customize-layout-of-fields}

단일 필드 또는 모든 필드의 레이아웃을 사용자 지정하여 캡션 및 오류 메시지의 위치를 변경할 수 있습니다. 사용자 지정 레이아웃을 필드에 적용하려면 다음 단계를 수행하십시오.

### 단일 필드의 레이아웃 사용자 정의 {#customize-layout-of-a-single-field}

사용자 지정 레이아웃을 단일 필드에 적용하려면 다음 단계를 수행하십시오.

1. 스타일 모드에서 양식을 **엽니다** . 스타일 모드에서 양식을 열려면 페이지 도구 모음에서 ![캔버스 드롭다운](assets/canvas-drop-down.png) > 스타일을 **누릅니다**.
1. 세로 막대의 양식 **개체**&#x200B;아래에서 필드를 선택하고 편집 단추를 ![누릅니다](assets/edit-button.png).
1. 사용자 정의할 필드의 상태를 선택하고 해당 상태에 대한 스타일을 지정합니다.

   ![필드의 인라인 스타일 지정](assets/edit-error-state.png)

### 양식의 모든 필드 레이아웃 사용자 정의 {#customize-layout-of-all-the-fields-of-a-form}

이제 AEM Forms를 사용하여 테마를 만들어 양식에 적용할 수 있습니다. 테마 편집기를 사용하면 양식 구성 요소의 스타일을 한 곳에서 지정할 수 있습니다. 테마를 만들 때 구성 요소 수준에서 스타일링을 지정합니다. 테마에 대한 자세한 내용은 AEM Forms [의 테마를 참조하십시오](../../forms/using/themes.md).

테마 편집기를 사용하여 테마를 만들어 양식에 있는 모든 필드의 레이아웃을 사용자 정의합니다. 테마를 만든 후 다음 단계를 수행하여 테마를 양식에 적용합니다.

1. 편집 모드에서 양식을 엽니다.
1. 편집 모드에서 구성 요소를 선택한 다음 ![필드 수준](assets/field-level.png) > 적응형 양식 **컨테이너를**&#x200B;탭한 다음 ![cmppr](assets/cmppr.png)을누릅니다.
1. 세로 막대의 적응형 양식 테마 아래에서 테마 편집기를 사용하여 만든 테마를 선택합니다.

## 사용자 정의 필드 레이아웃 만들기 {#create-a-custom-field-layout}

1. CRXDE lite를 엽니다. 기본 URL은 https://&#39;[server]:[port]&#39;/crx/de입니다.
1. /libs/fd/af/layouts/field 노드(예: defaultFieldLayout)에서 /apps 노드(예: /apps/af-field-layout)로 필드 레이아웃을 복사합니다.
1. 복사된 노드 및 defaultFieldLayout.jsp 파일의 이름을 변경합니다. 예: errorOnRight.jsp.

1. 복사한 노드의 qtip 및 jcr:description 속성의 값을 변경합니다. 예를 들어 속성 값을 [오른쪽 오류]로 변경합니다.

1. 새 스타일과 비헤이비어를 추가하려면 /etc 노드에서 클라이언트 라이브러리를 만듭니다.

   예를 들어 /etc/af-field-layout-clientlib 위치에서 노드 클라이언트 라이브러리를 만듭니다. 다음 코드와 함께 value af.field.errorOnRight 및 style.less 파일로 categories 속성을 추가합니다.

   ```css
   .widgetErrorWrapper {
   
    height: 38px;
    margin: 5px;
   
    .guideFieldWidget{
    width: 60%;
    float: left; 
    }
   
    .guideFieldError{
    overflow:hidden;
    width:40%; 
    }
   
   }
   ```

1. 모양과 비헤이비어를 향상시키려면 레이아웃 파일에 생성된 클라이언트 라이브러리(errorOnRight.jsp)를 포함합니다.
1. 필드의 편집 대화 상자를 열고 스타일 지정 **탭을 선택합니다** . 필드 **레이아웃 구성** 드롭다운 상자에서 새로 만든 레이아웃을 선택하고 확인을 **클릭합니다**.

ErrorOnRight.zip 패키지에는 필드 오른쪽에 오류 메시지를 표시하는 코드가 들어 있습니다.

[파일 가져오기](assets/erroronright.zip)
