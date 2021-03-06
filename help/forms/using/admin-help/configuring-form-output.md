---
title: 양식 출력 구성
seo-title: 양식 출력 구성
description: 양식 출력을 구성하는 방법을 알아봅니다.
seo-description: 양식 출력을 구성하는 방법을 알아봅니다.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# 양식 출력 구성{#configuring-form-output}

## 웹 브라우저 {#specify-the-type-of-html-output-returned-to-the-web-browser}에 반환된 HTML 출력 유형을 지정합니다

1. 관리 콘솔에서 서비스 > 양식을 클릭합니다.
1. 양식 출력의 출력 유형 목록에서 다음 옵션 중 하나를 선택합니다.

   **전체 HTML:** 전체 HTML 태그 내에 양식을 렌더링하려면(전체 HTML 페이지). 이 값이 기본값입니다.

   **양식 본문:** 태그 내에 양식을  `<BODY>` 렌더링하려면(전체 HTML 페이지가 아님).

1. 저장을 클릭합니다.

## PDF 컨텐츠가 렌더링되는 위치를 {#specify-the-location-where-pdf-content-is-rendered} 지정합니다

1. [양식 출력]의 [렌더링 위치] 목록에서 다음 옵션 중 하나를 선택합니다.

   **클라이언트:** Adobe Acrobat 또는 Adobe Reader 내에서 PDF forms을 렌더링하려면 클라이언트측 렌더링은 AEM Forms의 성능을 향상시키고 PDFForm 변환에만 적용됩니다.

   **서버:** 애플리케이션 서버에서 PDF forms을 렌더링하려면 다음을 수행하십시오.

   **자동:** XDP 파일의  `dynamicRender` 구성 값으로 지정된 위치에서 PDF 양식을 렌더링하려면 다음과 같이 하십시오. 이 값이 기본값입니다.

1. 저장을 클릭합니다.

## 양식 제출 {#configuring-invocation-of-custom-scripts-before-form-submit} 전에 사용자 지정 스크립트의 호출 구성

다음 단계를 수행하여 기능을 활성화합니다.

1. 관리 콘솔에 로그인합니다.
1. **서비스** > **forms**&#x200B;로 이동합니다.
1. 출력 유형을 양식 본문으로 지정합니다.
1. 설정을 저장합니다.
1. HTML 코드의 head 섹션에서 JavaScript 변수 __CUSTOM_SCRIPTS_VERSION을 선언하고 해당 값을 1로 설정합니다.

   >[!NOTE]
   >
   >*이 기능을 비활성화하려면 JavaScript 변수를 제거하거나 값을 0으로 설정할 수 있습니다.*
