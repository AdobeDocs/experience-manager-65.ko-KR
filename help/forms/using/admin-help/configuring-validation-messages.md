---
title: 유효성 검사 메시지 구성
seo-title: Configuring validation messages
description: 웹 브라우저에서 반환되는 양식과 관련하여 유효성 검사 메시지가 표시되는 방식과 위치를 지정하는 방법을 알아봅니다.
seo-description: Learn how to specify how validation messages are displayed and their location relative to the form returned in the web browser.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 2%

---

# 유효성 검사 메시지 구성 {#configuring-validation-messages}

HTML으로 렌더링되는 양식의 경우 사용자에게 표시되는 양식 유효성 검사 오류가 표시됩니다. 유효성 검사 메시지가 표시되는 방식을 사용자 지정할 수 있습니다. 유효성 검사 메시지가 표시되는 위치에 따라 양식의 메시지 위치와 프레임 테두리의 크기를 제어할 수도 있습니다.

## 유효성 검사 메시지 표시 방법 지정 {#specify-how-validation-messages-are-displayed}

1. 관리 콘솔에서 서비스 > 양식을 클릭합니다.
1. 검증 출력의 보고 목록에서 다음 옵션 중 하나를 선택합니다.

   **메시지 상자:** 별도의 대화 상자에 검증 메시지를 표시하려면

   **프레임:** 같은 창의 프레임 내에 검증 메시지를 표시하려면

   **프레임 없음:** 같은 창에 검증 메시지를 표시하려면 이 값이 기본값입니다.

   **API를 통해(데이터 포함):** API(데이터 포함)를 통해 유효성 검사 메시지를 반환합니다. 유효성 검사 메시지는 화면에 표시되지 않습니다.

   **API(양식 포함)를 통해:** API(양식 사용)를 통해 유효성 검사 메시지를 반환하려면 다음을 수행하십시오. 유효성 검사 메시지는 화면에 표시되지 않습니다.

   **없음:** 검증 메시지를 표시하지 않습니다.

1. 저장을 클릭합니다.

## 웹 브라우저에서 반환된 양식에 상대적인 유효성 검사 메시지 위치를 지정합니다 {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

보고가 프레임 또는 프레임 없음으로 설정되면 유효성 검사 메시지의 위치를 지정할 수 있습니다.

1. 검증 출력의 위치 목록에서 다음 옵션 중 하나를 선택합니다.

   **왼쪽:** 웹 브라우저 왼쪽에 유효성 검사 메시지를 표시하려면 다음을 수행하십시오.

   **오른쪽:** 웹 브라우저 오른쪽에 유효성 검사 메시지를 표시하려면 다음을 수행하십시오.

   **상단**: 웹 브라우저의 맨 위에 유효성 검사 메시지를 표시하려면 다음을 수행하십시오. 이 값이 기본값입니다.

   **아래쪽**: 웹 브라우저 하단에 유효성 검사 메시지를 표시하려면 다음을 수행하십시오.

1. 저장을 클릭합니다.

## 프레임 테두리 크기를 지정합니다 {#specify-the-frame-border-size}

[보고]가 [프레임]으로 설정된 경우 프레임 테두리 크기를 지정할 수 있습니다.

1. [유효성 검사 출력]의 [테두리 크기] 상자에서 프레임 테두리의 크기를 픽셀 단위로 입력합니다.

   테두리 크기는 0보다 크거나 같아야 합니다. 기본값은 1입니다.

1. 저장을 클릭합니다.
