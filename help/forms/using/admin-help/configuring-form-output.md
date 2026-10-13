---
title: 양식 출력 구성
description: 양식 출력을 구성하는 방법을 알아봅니다. 양식 출력을 구성하고 해당 기능을 활성화하려면 양식을 제출하기 전에 사용자 정의 스크립트를 사용합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 100%
---
# 양식 출력 구성{#configuring-form-output}

## 웹 브라우저에 반환되는 HTML 출력 유형 지정 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 관리 콘솔에서 서비스 > Forms를 클릭합니다.
1. 양식 출력의 출력 유형 목록에서 다음 옵션 중 하나를 선택합니다.

   **전체 HTML:** 전체 HTML 태그(완전한 HTML 페이지) 내에서 양식을 렌더링합니다. 이 값은 기본값입니다.

   **양식 본문:** `<BODY>` 태그(완전한 HTML 페이지가 아님) 내에서 양식을 렌더링합니다.

1. 저장을 클릭합니다.

## PDF 콘텐츠가 렌더링되는 위치 지정 {#specify-the-location-where-pdf-content-is-rendered}

1. 양식 출력의 렌더링 위치 목록에서 다음 옵션 중 하나를 선택합니다.

   **클라이언트:** Adobe Acrobat 또는 Adobe Reader에서 PDF 양식을 렌더링합니다. 클라이언트측 렌더링은 AEM Forms의 성능을 향상하고 PDFForm 변환에만 적용됩니다.

   **서버:** 애플리케이션 서버에서 PDF 양식을 렌더링합니다.

   **자동:** XDP 파일의 `dynamicRender` 구성 값에서 지정된 위치에서 PDF 양식을 렌더링합니다. 이 값은 기본값입니다.

1. 저장을 클릭합니다.

## 양식 제출 전 사용자 정의 스크립트 호출 구성 {#configuring-invocation-of-custom-scripts-before-form-submit}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

해당 기능을 활성화하려면 다음 단계를 수행합니다.

1. 관리 콘솔에 로그인합니다.
1. **서비스** > **Forms**&#x200B;로 이동합니다.
1. 출력 유형을 양식 본문으로 지정합니다.
1. 설정을 저장합니다.
1. HTML 코드의 헤드 섹션에서 JavaScript 변수 __CUSTOM_SCRIPTS_VERSION을 선언하고 해당 값을 1로 설정합니다.

   >[!NOTE]
   >
   >*해당 기능을 비활성화하려면 JavaScript 변수를 제거하거나 해당 값을 0으로 설정하면 됩니다.*
