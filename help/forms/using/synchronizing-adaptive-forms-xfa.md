---
title: 적응형 Forms을 XFA 양식 템플릿과 동기화
seo-title: 적응형 Forms을 XFA 양식 템플릿과 동기화
description: 적응형 양식을 XFA/XDP 파일과 동기화
seo-description: 적응형 양식을 XFA/XDP 파일과 동기화
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 0%

---


# 적응형 Forms을 XFA 양식 템플릿과 동기화{#synchronizing-adaptive-forms-with-xfa-form-templates}

## 소개 {#introduction}

XFA 양식 템플릿( `*.XDP` 파일)을 기반으로 적응형 양식을 만들 수 있습니다. 이렇게 재사용하면 기존 XFA 양식에 대한 투자를 보존할 수 있습니다. 적응형 양식을 만들기 위해 XFA 양식 템플릿을 사용하는 방법에 대한 자세한 내용은 [템플릿](../../forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p)을 기반으로 적응형 양식 만들기

적응형 양식의 XDP 파일의 필드를 재사용할 수 있습니다. 이러한 필드를 빈칸 필드라고 합니다. 바인딩 필드 속성(예: 스크립트, 레이블 및 표시 형식)이 XDP 파일에서 복사됩니다. 이러한 속성 중 일부의 값을 재정의하도록 선택할 수도 있습니다.

AEM Forms은 나중에 XDP 파일의 해당 필드에 수행한 변경 사항과 함께 적응형 양식의 필드를 동기화할 수 있는 방법을 제공합니다. 이 문서에서는 이 동기화를 활성화할 수 있는 방법에 대해 설명합니다.

![XFA 양식의 필드를 적응형 양식으로 드래그할 수 있습니다](assets/drag-drop-xfa.gif.gif)

AEM Forms 작성 환경에서는 XFA 양식(왼쪽)의 필드를 적응형 양식(오른쪽)으로 드래그할 수 있습니다

## 전제 조건 {#prerequisites}

이 문서의 정보를 사용하려면 다음 영역에 익숙해지는 것이 좋습니다.

* [적응형 양식 만들기](../../forms/using/creating-adaptive-form.md)

* XFA(XML Forms 아키텍처)

아티클에서 제공하는 에셋을 사용하려면 다음 섹션 [샘플 패키지](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-sample-package-p)에 설명된 대로 샘플 패키지를 다운로드하십시오.

## 샘플 패키지 {#sample-package}

이 문서에서는 예를 사용하여 업데이트된 XFA 양식 템플릿과 적응형 양식을 동기화하는 방법을 보여 줍니다. 예제에 사용된 자산은 패키지에 있으며, 이 아티클의 [다운로드](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-downloads-p) 섹션에서 다운로드할 수 있습니다.

패키지를 업로드한 후 AEM Forms UI에서 이러한 자산을 볼 수 있습니다.

패키지 관리자를 사용하여 패키지를 설치합니다.`https://<server>:<port>/crx/packmgr/index.jsp`

패키지에는 다음 에셋이 들어 있습니다.

1. `sample-form.xdp`:예제로 사용되는 XFA 양식 템플릿

1. `sample-xfa-af`:sample-form.xdp 파일을 기반으로 하는 적응형 양식입니다. 그러나 이 적응형 양식에는 필드가 포함되지 않습니다. 다음 단계에서는 이 적응형 양식에 컨텐츠를 추가합니다.

### 적응형 양식 {#add-content-to-adaptive-form-br}에 컨텐츠 추가

1. https://&lt;server>:&lt;port>/aem/forms.html으로 이동합니다. 필요한 경우 자격 증명을 입력합니다.
1. 작성 모드에서 편집할 샘플-af-xfa를 엽니다.
1. 세로 막대의 [콘텐트] 브라우저에서 [데이터 모델 개체] 탭을 선택합니다. NumericField1 및 TextField1을 적응형 양식으로 드래그합니다.
1. NumericField1의 제목을 **숫자 필드**&#x200B;에서 **AF 숫자 필드로 변경합니다.**

>[!NOTE]
>
>이전 단계에서는 XDP 파일에 필드 속성을 덮어썼습니다. 따라서 XDP 파일의 해당 속성이 나중에 수정될 경우 이 속성은 동기화되지 않습니다.

## XDP 파일 {#detecting-changes-in-xdp-file}에서 변경 사항을 감지하는 중

XDP 파일 또는 조각의 변경이 있을 때마다 AEM Forms UI는 XDP 파일 또는 조각을 기반으로 하는 모든 적응형 양식에 플래그를 지정합니다.

XDP 파일을 업데이트한 후 변경 사항이 플래그가 지정되도록 AEM Forms UI에서 다시 업로드해야 합니다.

예를 들어 다음 단계를 사용하여 `sample-form.xdp` 파일을 업데이트할 수 있습니다.

1. 메시지가 표시되면 `https://<server>:<port>/projects.html.` 자격 증명을 입력합니다.
1. 왼쪽의 Forms 탭을 클릭합니다.
1. 로컬 컴퓨터에서 `sample-form.xdp` 파일을 다운로드합니다. XDP 파일은 `.zip` 파일로 다운로드되며, 이 파일은 모든 파일 압축 해제 유틸리티를 사용하여 추출할 수 있습니다.

1. `sample-form.xdp` 파일을 열고 필드 TextField1의 제목을 **텍스트 필드**&#x200B;에서 **내 텍스트 필드**&#x200B;로 변경합니다.

1. `sample-form.xdp` 파일을 다시 AEM Forms UI에 업로드합니다.

XDP 파일이 업데이트되면 XDP 파일을 기반으로 적응형 양식을 편집할 때 편집기에 아이콘이 표시됩니다. 이 아이콘은 응용 양식이 XDP 파일과 동기화되지 않았음을 나타냅니다. 다음 이미지에서 세로 막대의 다음 아이콘을 참조하십시오.

![응용 양식이 XDP 파일과 동기화되지 않았음을 표시하는 아이콘](assets/sync-af-xfa.png)

## 적응형 양식을 최신 XDP 파일 {#synchronizing-adaptive-forms-with-the-latest-xdp-file}과 동기화

XDP 파일과 동기화되지 않은 응용 양식이 다음에 작성할 수 있도록 열려 있으면 다음 메시지가 표시됩니다.적응형 양식의 **스키마/양식 템플릿이 업데이트되었습니다. `Click Here` 를 새 버전으로 재설정합니다.**

메시지를 클릭하면 적응형 양식의 필드가 XDP 파일의 해당 필드와 동기화됩니다.

이 아티클에 사용된 예제의 경우 제작 모드에서 `sample-xfa-af`을(를) 엽니다. 메시지는 적응형 양식의 맨 아래에 표시됩니다.

![적응형 양식을 XDP 파일과 동기화하라는 메시지](assets/sync-af-xfa-1.png)

### {#updating-the-properties} 속성 업데이트

XDP 파일에서 응용 양식으로 복사되었던 모든 속성은 작성자가 응용 양식(구성 요소 대화 상자에서)에서 명시적으로 재정의한 속성을 제외하고 업데이트됩니다. 업데이트된 속성 목록은 서버 로그에서 사용할 수 있습니다.

응용 양식 예제의 속성을 업데이트하려면 메시지에서 링크(레이블 `"Click Here"`)를 클릭합니다. TextField1의 제목은 **텍스트 필드**&#x200B;에서 **내 텍스트 필드**&#x200B;로 변경됩니다.

![update-property](assets/update-property.png)

>[!NOTE]
>
>[적응형 양식에 내용 추가](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p)에 설명된 대로 구성 요소 속성 대화 상자에서 이 속성을 재정의했기 때문에 AF 숫자 필드 레이블이 변경되지 않았습니다.

### XDP 파일의 새 필드를 적응형 양식에 추가   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

나중에 원본 XDP 파일에 추가된 모든 필드는 양식 계층 탭에 나타나며 이러한 새 필드를 적응형 양식으로 드래그할 수 있습니다.

[양식 계층] 탭의 필드를 업데이트하려면 오류 메시지의 링크를 클릭할 필요가 없습니다.

### XDP 파일 {#deleted-fields-in-xdp-file}의 삭제된 필드

응용 양식으로 이전에 복사되었던 필드가 XDP 파일에서 삭제되면 XDP 파일에 해당 필드가 없다는 오류 메시지가 작성 모드에 표시됩니다. 이러한 경우 적응형 양식에서 필드를 수동으로 삭제하거나 구성 요소 대화 상자에서 `bindRef` 속성을 지웁니다.

다음 단계는 이 아티클에서 사용되는 예제의 에셋에 대한 이러한 사용 흐름을 보여 줍니다.

1. `sample-form.xdp` 파일을 업데이트하고 NumericField1을 삭제합니다.
1. AEM Forms UI에서 `sample-form.xdp` 파일 업로드
1. 작성을 위해 `sample-xfa-af` 적응형 양식을 엽니다. 다음 오류 메시지가 표시됩니다.적응형 양식의 스키마/양식 템플릿이 업데이트되었습니다. `Click Here` 를 새 버전으로 재설정합니다.

1. 메시지에서 링크(&quot; `Click Here`&quot; 레이블이 지정됨)를 클릭합니다. 필드가 XDP 파일에 더 이상 존재하지 않는다는 오류 메시지가 표시됩니다.

![XDP 파일에서 요소를 삭제할 때 나타나는 오류](assets/no-element-xdp.png)

삭제된 필드는 필드에 오류를 나타내는 아이콘도 표시됩니다.

![필드의 오류 아이콘](assets/error-field.png)

>[!NOTE]
>
>적응형 양식의 필드(편집 대화 상자에서 잘못된 `bindRef` 값)도 삭제된 필드로 간주됩니다. 작성자가 이러한 오류를 수정하지 않고 적응형 양식을 게시하지 않으면 이 필드는 바인딩되지 않은 일반 적응형 양식 필드로 취급되고 출력 XML 파일의 바인딩되지 않은 섹션에 포함됩니다.

## 다운로드 {#downloads}

이 문서의 예제에 대한 컨텐츠 패키지

[파일 가져오기](assets/sample-xfa-af-sync-1.0.zip)
