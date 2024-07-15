---
title: 유효성 검사 메시지 구성
description: 웹 브라우저에서 반환되는 양식을 기준으로 유효성 검사 메시지가 표시되는 방식과 위치를 지정하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 14314383-5228-4904-98c1-586f48a1142c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# 유효성 검사 메시지 구성 {#configuring-validation-messages}

HTML으로 렌더링되는 양식의 경우 사용자에게 발생한 양식 유효성 검사 오류가 표시됩니다. 유효성 검사 메시지가 표시되는 방식을 사용자 지정할 수 있습니다. 유효성 검사 메시지가 표시되는 위치에 따라 폼에서 메시지 위치와 프레임 테두리 크기를 제어할 수도 있습니다.

## 유효성 검사 메시지가 표시되는 방식 지정 {#specify-how-validation-messages-are-displayed}

1. 관리 콘솔에서 서비스 > 양식을 클릭합니다.
1. [검증 출력]의 [보고] 목록에서 다음 옵션 중 하나를 선택합니다.

   **메시지 상자:** 유효성 검사 메시지를 별도의 대화 상자에 표시합니다.

   **프레임:** 같은 창의 프레임 내에 유효성 검사 메시지를 표시합니다.

   **프레임 없음:** 같은 창에 유효성 검사 메시지를 표시합니다. 이 값은 기본값입니다.

   **API를 통해(데이터 포함):** API를 통해(데이터 포함) 유효성 검사 메시지를 반환합니다. 유효성 검사 메시지가 화면에 표시되지 않습니다.

   **API를 통해(양식 포함):** API를 통해(양식 포함) 유효성 검사 메시지를 반환합니다. 유효성 검사 메시지가 화면에 표시되지 않습니다.

   **없음:** 유효성 검사 메시지를 표시하지 않습니다.

1. 저장을 클릭합니다.

## 웹 브라우저에서 반환되는 양식을 기준으로 유효성 검사 메시지의 위치를 지정하십시오. {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

[보고]가 [프레임] 또는 [프레임 없음]으로 설정된 경우 유효성 검사 메시지의 위치를 지정할 수 있습니다.

1. 검증 출력(Validation Output)의 위치(Position) 목록에서 다음 옵션 중 하나를 선택합니다.

   **왼쪽:** 웹 브라우저의 왼쪽에 유효성 검사 메시지를 표시합니다.

   **오른쪽:** 웹 브라우저의 오른쪽에 유효성 검사 메시지를 표시합니다.

   **위쪽**: 웹 브라우저 맨 위에 유효성 검사 메시지를 표시합니다. 이 값은 기본값입니다.

   **아래쪽**: 웹 브라우저 아래쪽에 유효성 검사 메시지를 표시합니다.

1. 저장을 클릭합니다.

## 프레임 테두리 크기 지정 {#specify-the-frame-border-size}

[보고]를 [프레임]으로 설정하면 프레임 테두리 크기를 지정할 수 있습니다.

1. [유효성 검사 출력]의 [테두리 크기] 상자에 프레임 테두리 크기를 픽셀 단위로 입력합니다.

   테두리 크기는 0보다 크거나 같아야 합니다. 기본값은 1입니다.

1. 저장을 클릭합니다.
