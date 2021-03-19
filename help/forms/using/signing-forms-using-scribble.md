---
title: 자유롭게 서명을 사용하여 양식에 전자 서명 적용
seo-title: 자유롭게 서명을 사용하여 양식에 전자 서명 적용
description: 자유롭게 서명을 사용하여 양식 서명
seo-description: 자유롭게 서명을 사용하여 양식 서명
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: 적응형 양식
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 자유 서명{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}을 사용하여 양식에 전자 서명 적용

**자유 서명** 구성 요소 및 **서명 단계** 구성 요소를 사용하여 적응형 양식에 서명을 그리기(스크리블)할 수 있습니다. 서명 단계 구성 요소는 적응형 양식의 PDF 버전을 표시합니다. 서명 단계 구성 요소를 사용하려면 기록 문서 옵션이 활성화되어 있거나 양식 템플릿 기반 적응형 양식이 필요합니다.

두 구성 요소 모두 아래 표시된 대로 양식에 서명할 윈도우를 제공합니다. 지리적 위치 아이콘 ![aem_6_3_geolocation](assets/aem_6_3_geolocation.png)을 클릭하여 서명에 지리적 위치를 추가할 수도 있습니다.

![문지르기 기호 대화 상자](assets/scribble-signature.png)

## 자유 서명 {#configure-an-adaptive-form-to-use-scribble-signature}을 사용하도록 적응형 양식을 구성합니다.

1. 기록 문서 만들기 옵션을 활성화하거나 적응형 양식을 기반으로 양식 템플릿을 만듭니다. 단계별 정보는 [적응형 양식 만들기](../../forms/using/creating-adaptive-form.md)를 참조하십시오.
1. 구성 요소 브라우저에서 적응형 양식으로 **자유 서명** 구성 요소를 드래그하여 놓습니다.
1. **구성** ![구성](assets/configure.png) 아이콘을 누릅니다. 속성 브라우저를 열고 [자유롭게 서명] 구성 요소의 속성을 표시합니다. 스크리블 서명 구성 요소의 속성을 구성합니다.
1. 서명 단계 구성 요소를 구성 요소 브라우저에서 적응형 양식으로 드래그하여 놓습니다.

   >[!NOTE]
   >
   >서명 단계 구성 요소는 양식에 사용할 수 있는 전체 너비를 차지합니다. 서명 단계 구성 요소를 포함하는 섹션에는 다른 구성 요소가 없는 것이 좋습니다.

1. 컨텐츠 브라우저에서 **양식 컨테이너**&#x200B;를 누르고 **구성** ![](/help/forms/using/assets/configure.png) 아이콘을 누릅니다. 속성 브라우저를 열고 적응형 양식 컨테이너 속성을 표시합니다. **적응형 양식 컨테이너** > **전자 서명**&#x200B;으로 이동하고 **Adobe Sign 사용** 옵션을 선택 취소합니다. 완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 눌러 변경 내용을 저장합니다.

   >[!NOTE]
   >
   >적응형 양식에 서명 단계 구성 요소를 추가하면 Adobe Sign 활성화 옵션이 자동으로 선택됩니다.

1. **구성** ![구성](assets/configure.png) 아이콘을 누릅니다. 속성 브라우저를 열고 서명 단계 속성을 표시합니다. 다음 속성을 구성합니다.

   * **요소 이름**:구성 요소의 이름을 지정합니다.

   * **제목:** 구성 요소의 고유한 제목을 지정합니다.
   * **템플릿 메시지:** 서명 PDF를 로드하는 동안 표시할 메시지를 지정합니다. Adobe Sign 서비스는 서명 PDF를 준비하고 로드하는 데 시간이 다소 소요됩니다.
   * **서명 서비스:** [ **자유롭게 서명]** 옵션을 선택합니다.

   * **CSS 클래스**:클라이언트 라이브러리의 CSS 클래스(있는 경우)를 지정합니다. CSS 클래스 대신 [테마](../../forms/using/themes.md) 및 [인라인 스타일](../../forms/using/inline-style-adaptive-forms.md)을 사용하는 것이 좋습니다.

   완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 눌러 변경 내용을 저장합니다. 서명이 성공적으로 구성되었습니다.

   이제 양식을 채울 때 PDF 버전의 적응형 양식이 표시되고 PDF 문서에 서명할 수 있는 옵션이 제공됩니다. 자세한 내용은 [스크리블 서명을 사용하여 적응형 양식 서명](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)을 참조하십시오.

## 자유 서명 {#sign-an-adaptive-form-using-scribble-signature}을(를) 사용하여 적응형 양식에 서명

1. 적응형 양식을 채우고 [서명 단계] 페이지에 도달하면 서명 화면이 표시됩니다.

   ![EchoSign 페이지의 서명 화면](assets/esignscribblesign.jpg)

1. **[!UICONTROL 서명]**&#x200B;을 클릭합니다. 문지르기 기호 대화 상자가 나타납니다. 양식에 서명하고 완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 클릭하여 서명을 저장합니다.

   ![문지르기 기호 대화 상자](assets/scribblewidget.jpg)

1. 완료를 클릭하여 서명 프로세스를 완료합니다.

   ![서명 프로세스 완료](assets/scribblecomplete.jpg)

서명이 양식에 추가되고 양식 컨트롤이 다음 패널로 이동합니다.

