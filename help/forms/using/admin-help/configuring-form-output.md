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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# 양식 출력 구성{#configuring-form-output}

## 웹 브라우저에 반환된 HTML 출력 유형 지정 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 관리 콘솔에서 서비스 > 양식을 클릭합니다.
1. 양식 출력 아래의 출력 유형 목록에서 다음 옵션 중 하나를 선택합니다.

   **전체 HTML:** 전체 HTML 태그 내에서 양식을 렌더링하려면(전체 HTML 페이지) 이 값이 기본값입니다.

   **양식 본문:** 양식을  `<BODY>` 태그 내에 렌더링하려면(전체 HTML 페이지가 아님)

1. 저장을 클릭합니다.

## PDF 컨텐츠가 렌더링되는 위치 지정 {#specify-the-location-where-pdf-content-is-rendered}

1. 양식 출력의 렌더링 위치 목록에서 다음 옵션 중 하나를 선택합니다.

   **클라이언트:** Adobe Acrobat 또는 Adobe Reader 내에서 PDF forms을 렌더링하려면 클라이언트측 렌더링은 AEM 양식의 성능을 향상시키고 PDForm 변환에만 적용됩니다.

   **서버:** 응용 프로그램 서버에서 PDF forms을 렌더링하려면

   **자동:** XDP 파일의  `dynamicRender` 구성 값으로 지정된 위치에서 PDF 양식을 렌더링하려면 이 값이 기본값입니다.

1. 저장을 클릭합니다.

## 양식 제출 전에 사용자 지정 스크립트 호출 구성{#configuring-invocation-of-custom-scripts-before-form-submit}

다음 단계를 수행하여 기능을 활성화합니다.

1. 관리 콘솔에 로그인합니다.
1. **서비스** > **양식**&#x200B;으로 이동합니다.
1. 출력 유형을 양식 본문으로 지정합니다.
1. 설정을 저장합니다.
1. HTML 코드의 헤드 섹션에서 JavaScript 변수 __CUSTOM_SCRIPTS_VERSION을 선언하고 해당 값을 1로 설정합니다.

   >[!NOTE]
   >
   >*이 기능을 비활성화하려면 JavaScript 변수를 제거하거나 값을 0으로 설정할 수 있습니다.*

