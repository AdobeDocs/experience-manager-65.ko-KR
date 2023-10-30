---
title: 양식 출력 구성
description: 양식 출력을 구성하는 방법에 대해 알아봅니다. 양식 출력을 구성하고 기능을 활성화하려면 양식을 제출하기 전에 사용자 지정 스크립트를 사용하십시오.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# 양식 출력 구성{#configuring-form-output}

## 웹 브라우저에 반환되는 HTML 출력의 유형을 지정합니다. {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 관리 콘솔에서 서비스 > 양식을 클릭합니다.
1. 양식 출력의 출력 유형 목록에서 다음 옵션 중 하나를 선택합니다.

   **전체 HTML:** 전체 HTML 태그(전체 HTML 페이지) 내에서 양식을 렌더링하려면 다음을 수행하십시오. 이 값은 기본값입니다.

   **양식 본문:** 다음 범위 내에서 양식을 렌더링하려면 `<BODY>` 태그(전체 HTML 페이지가 아님).

1. 저장을 클릭합니다.

## PDF 컨텐츠가 렌더링되는 위치를 지정합니다. {#specify-the-location-where-pdf-content-is-rendered}

1. [양식 출력]의 [렌더링 위치] 목록에서 다음 옵션 중 하나를 선택합니다.

   **클라이언트:** Adobe Acrobat 또는 Adobe Reader 내에서 PDF forms을 렌더링하려면 다음을 수행하십시오. 클라이언트측 렌더링은 AEM Forms의 성능을 개선하며 PDForm 변환에만 적용됩니다.

   **서버:** 응용 프로그램 서버에서 PDF forms을 렌더링합니다.

   **자동:** PDF 양식을 렌더링하는 방법: `dynamicRender` xdp 파일의 구성 값입니다. 이 값은 기본값입니다.

1. 저장을 클릭합니다.

## 양식 제출 전 사용자 지정 스크립트 호출 구성 {#configuring-invocation-of-custom-scripts-before-form-submit}

기능을 활성화하려면 다음 단계를 수행하십시오.

1. 관리 콘솔에 로그인합니다.
1. 다음으로 이동 **서비스** > **양식**.
1. 출력 유형을 양식 본문으로 지정합니다.
1. 설정을 저장합니다.
1. HTML 코드의 head 섹션에서 JavaScript 변수인 __CUSTOM_SCRIPTS_VERSION 을 선언하고 해당 값을 1로 설정합니다.

   >[!NOTE]
   >
   >*이 기능을 비활성화하려면 JavaScript 변수를 제거하거나 값을 0으로 설정할 수 있습니다.*
