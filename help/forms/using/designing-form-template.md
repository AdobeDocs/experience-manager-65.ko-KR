---
title: HTML5 양식용 양식 템플릿 디자인
seo-title: Designing form templates for HTML5 forms
description: AEM Forms에서는 XFA 양식 템플릿을 HTML5 형식으로 렌더링합니다. 양식 디자이너는 디자이너를 사용하여 양식 템플릿을 디자인하고 HTML5 렌디션 기능을 사용할 수 있습니다.
seo-description: AEM Forms offers rendering XFA form template to HTML5 format. Form designers can design form templates using Designer and use the HTML5 rendition capability.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# HTML5 양식용 양식 템플릿 디자인{#designing-form-templates-for-html-forms}

AEM의 HTML5 양식 구성 요소는 XFA 양식 템플릿을 HTML5 형식으로 렌더링합니다. 양식 디자이너는 다음을 사용하여 양식 템플릿을 디자인할 수 있습니다. [Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63) HTML5 렌디션 기능을 사용하십시오. 이러한 양식 템플릿은 자산과 함께 AEM 저장소, 파일 시스템에 있거나 http를 통해 노출될 수 있습니다. 그러나 Forms Manager를 사용하여 양식을 관리하려는 경우 템플릿과 에셋이 AEM 저장소에 있어야 합니다.

HTML5 양식은 PDF forms의 동작과 거의 일치하지만 두 형식 모두에는 다른 형식에는 적용할 수 없는 몇 가지 기능이 있습니다. 예를 들어 Adobe Reader의 PDF 양식에 바코드를 적용하는 방법은 모바일 양식이나 양식에 디지털 서명을 하는 방법도 형식마다 다릅니다. 이러한 변형에 대한 자세한 내용은 [HTML 5 양식과 PDF forms 간의 차별화된 기능](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

일반적인 XFA 기능에 대해서는 다음 모범 사례 및 지침을 참조하여 두 형식으로 작동하는 양식을 디자인하십시오.

## 우수 사례 {#best-practices}

스키마 바인딩 또는 양식 논리 작성과 같은 양식 템플릿 디자인 관련 단계는 대부분 동일합니다. 그러나 Adobe Reader과 같은 두꺼운 클라이언트와 브라우저 기반 양식의 렌더링 및 스크립팅 엔진 간의 내재된 차이로 인해 다음에서 설명하는 몇 가지 권장 사항이 있습니다. [우수 사례](/help/forms/using/design-accessible-html5-forms.md) 기사. 이러한 우수 사례를 통해 양식 템플릿을 두 형식 모두에서 예상대로 작동하도록 디자인할 수 있습니다.

### HTML5 Forms용 AEM Forms Designer의 기능 {#capabilities-in-aem-forms-designer-for-html-forms}

#### 미리 보기 HTML {#preview-html}

[HTML 미리 보기] 탭이 디자인 모드에서 추가되어 양식 디자이너는 디자인 프로세스 중에 양식을 HTML5 형식으로 미리 볼 수 있습니다. AEM Forms Designer에서 이 기능을 활성화하고 구성하는 방법에 대한 자세한 내용은 [미리 보기 HTML](../../forms/using/preview-xdp-forms-html.md).

#### 스크리블 서명 {#scribble-signature}

HTML5 양식의 주요 대상은 터치 장치입니다. 따라서 새 스크리블 서명 컨트롤이 AEM Forms Designer에 추가됩니다. 양식 서식 파일에서 스크리블 서명 컨트롤을 클릭하거나 드래그 앤 드롭하여 구성할 수 있습니다. HTML5 렌디션의 스크리블 필드로 렌더링되어 터치 디바이스에서 스크리블 서명을 하는 데 사용할 수 있습니다. 데스크탑 컴퓨터에서는 마우스 컨트롤을 사용하여 스크리블 필드로 사용할 수 있습니다. 이 기능을 사용하는 방법에 대한 자세한 내용은 [XFA 스크리블 필드](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### 리치 텍스트 형식 {#rich-text-format}

텍스트 필드를 서식 있는 텍스트 필드로 변환할 수 있습니다. 텍스트 필드에 서식 옵션 목록을 추가합니다. 변환하려면 Forms 디자이너를 열고 의 텍스트 필드를 탭합니다. **[!UICONTROL 디자인 보기]**. 다음에서 **[!UICONTROL 필드]** 탭, 선택 **[!UICONTROL 리치 텍스트]** 다음에서 **[!UICONTROL 필드 형식]** 드롭다운 목록입니다. 이제 XFA 양식이 HTML5 양식으로 렌더링되면 필드가 리치 텍스트 필드로 렌더링됩니다. 누르기 ![최대화](assets/maximize_icon.svg) 추가 서식 옵션을 보려면
