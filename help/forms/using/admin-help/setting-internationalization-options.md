---
title: 국제화 옵션 설정
description: 양식을 렌더링하는 데 사용되는 로케일을 지정하는 방법과 출력 스트림을 인코딩하는 데 사용되는 문자 세트를 지정하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '236'
ht-degree: 100%

---

# 국제화 옵션 설정{#setting-internationalization-options}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

## 양식을 렌더링하는 데 사용되는 로케일 지정 {#specify-the-locale-used-to-render-forms}

PDF 양식을 렌더링할 때 사용되는 로케일을 지정할 수 있습니다. PDF 양식의 필드에서는 지정된 로케일을 사용하여 데이터를 표시합니다. 예를 들어 로케일이 독일어로 설정된 경우 양식에서는 숫자 값에 독일어 소수 구분자를 사용합니다. 이 로케일은 HTML 변환의 일부로 웹 브라우저와 같은 클라이언트 장치에 유효성 검사 메시지를 보내는 데에도 사용됩니다.

1. 관리 콘솔에서 서비스 > Forms를 클릭합니다.
1. 국제화의 언어 목록에서 양식을 렌더링하는 데 사용되는 로케일을 선택합니다. 기본값은 영어(미국)입니다.
1. 저장을 클릭합니다.

## 출력 스트림을 인코딩하는 데 사용되는 문자 세트 지정 {#specify-the-character-set-used-to-encode-the-output-stream}

1. 국제화의 문자 세트 목록에서 문자 세트를 선택합니다. 이 설정은 renderHTMLForm 또는 renderPDFForm 중 사용하는 API에 따라 달라집니다. 나열된 문자 세트 외의 다른 문자 세트를 지정하려면 사용자 정의를 선택하고 표시되는 상자에서 인코딩 값을 지정합니다.

   HTML 변환의 경우 AEM Forms는 `java.nio.charset` 패키지에서 정의된 문자 인코딩 값을 지원합니다. sFormPreference가 PDFForm인 경우 특정 문자 세트만 지원됩니다. 문자 세트는 유효한 정식 이름이어야 합니다. 기본값은 ISO-8859-1입니다.

1. 저장을 클릭합니다.
