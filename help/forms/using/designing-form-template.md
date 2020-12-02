---
title: HTML5 양식의 양식 템플릿 디자인
seo-title: HTML5 양식의 양식 템플릿 디자인
description: AEM Forms은 XFA 양식 템플릿을 HTML5 형식으로 렌더링합니다. 양식 디자이너는 Designer를 사용하여 양식 템플릿을 디자인하고 HTML5 변환 기능을 사용할 수 있습니다.
seo-description: AEM Forms은 XFA 양식 템플릿을 HTML5 형식으로 렌더링합니다. 양식 디자이너는 Designer를 사용하여 양식 템플릿을 디자인하고 HTML5 변환 기능을 사용할 수 있습니다.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# HTML5 양식의 양식 템플릿 디자인{#designing-form-templates-for-html-forms}

AEM의 HTML5 양식 구성 요소는 XFA 양식 템플릿을 HTML5 형식으로 렌더링합니다. 양식 디자이너는 [Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63)를 사용하여 양식 템플릿을 디자인하고 HTML5 변환 기능을 사용할 수 있습니다. 이러한 양식 템플릿은 자산과 함께 AEM 저장소, 파일 시스템에 상주하거나 http를 통해 노출할 수 있습니다. 그러나 Forms 관리자를 사용하여 양식을 관리할 계획인 경우 템플릿과 자산은 AEM 저장소에 상주해야 합니다.

HTML5 양식은 PDF forms의 비헤이비어와 상당히 일치하지만 두 형식 모두에서 다른 형식에 적용할 수 없는 기능이 있습니다. 예를 들어 Adobe Reader의 PDF 양식에 바코드가 적용되는 방법은 모바일 양식이나 양식에 따라 다르며, 양식에 디지털로 서명하는 방법도 서식에 따라 다릅니다. 이러한 변형에 대한 자세한 내용은 [HTML5 양식과 PDF forms 간 기능 차이](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)를 참조하십시오.

일반적인 XFA 기능을 살펴보려면 두 형식 모두에서 작동하는 양식을 디자인하기 위한 다음 모범 사례 및 지침을 참조하십시오.

## 우수 사례 {#best-practices}

스키마 바인딩 또는 양식 논리 작성과 같은 양식 템플릿을 디자인하는 대부분의 단계는 동일합니다. 그러나 Adobe Reader과 같은 굵은 클라이언트의 렌더링 및 스크립팅 엔진과 브라우저 기반 양식의 고유한 차이로 인해 [우수 사례](/help/forms/using/design-accessible-html5-forms.md) 문서에 설명된 몇 가지 권장 사항이 있습니다. 이러한 우수 사례는 두 형식 모두에서 예상대로 작동하도록 양식 템플릿을 디자인하는 데 도움이 됩니다.

### AEM Forms 디자이너의 HTML5 Forms 기능 {#capabilities-in-aem-forms-designer-for-html-forms}

#### HTML {#preview-html} 미리 보기

양식 디자이너가 디자인 프로세스 동안 HTML5 형식으로 양식을 미리 볼 수 있도록 양식 디자이너가 디자인 모드에 HTML 미리 보기 탭이 추가됩니다. AEM Forms 디자이너에서 이 기능을 활성화하고 구성하는 방법에 대한 자세한 내용은 [HTML 미리 보기](../../forms/using/preview-xdp-forms-html.md)를 참조하십시오.

#### 스크리블 서명 {#scribble-signature}

HTML5 양식의 주요 목표는 터치 디바이스입니다. 따라서 AEM Forms 디자이너에 새로운 문지르기 서명 컨트롤이 추가됩니다. 양식 템플릿에서 문지르기 서명 컨트롤을 클릭하거나 드래그하여 놓고 구성할 수 있습니다. HTML5 변환에서 낙서 필드로 렌더링되며 터치 디바이스에서 서명을 자유롭게 하는 데 사용할 수 있습니다. 데스크톱 컴퓨터에서는 마우스 컨트롤을 사용하여 자유 필드로 사용할 수 있습니다. 이 기능 사용 방법에 대한 자세한 내용은 [XFA 스크리블 필드](../../forms/using/scribble-signature.md)를 참조하십시오.

![4](assets/4.png)

#### 서식 있는 텍스트 형식 {#rich-text-format}

텍스트 필드를 리치 텍스트 필드로 변환할 수 있습니다. 텍스트 필드에 서식 옵션 목록이 추가됩니다. 변환하려면 Forms 디자이너를 열고 **[!UICONTROL 디자인 뷰]**&#x200B;에서 텍스트 필드를 누릅니다. **[!UICONTROL 필드]** 탭에서 **[!UICONTROL 필드 형식]** 드롭다운 목록에서 **[!UICONTROL 서식 있는 텍스트]**&#x200B;을 선택합니다. 이제 XFA 양식이 HTML5 양식으로 렌더링되면 필드가 리치 텍스트 필드로 렌더링됩니다. 추가 서식 옵션을 보려면 ![Maximize](assets/maximize_icon.svg)을 누릅니다.
