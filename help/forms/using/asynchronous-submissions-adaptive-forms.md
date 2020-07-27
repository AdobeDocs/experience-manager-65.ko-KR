---
title: 비동기 적응형 양식 제출
seo-title: 비동기 적응형 양식 제출
description: 적응형 양식에 대한 비동기 제출 구성에 대해 알아봅니다.
seo-description: 적응형 양식에 대한 비동기 제출 구성에 대해 알아봅니다.
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# 비동기 적응형 양식 제출{#asynchronous-submission-of-adaptive-forms}

일반적으로 웹 양식은 동기식으로 제출되도록 구성됩니다. 동시 제출 시 사용자가 양식을 제출하면 확인 페이지, 감사 인사 페이지 또는 제출 실패 시 오류 페이지로 리디렉션됩니다. 그러나 단일 페이지 애플리케이션과 같은 최신 웹 경험은 백그라운드에서 클라이언트-서버 상호 작용이 발생하는 동안 웹 페이지가 정적 상태로 유지되면서 큰 인기를 얻고 있습니다. 이제 비동기 제출을 구성하여 이 환경에 적응형 양식을 제공할 수 있습니다.

비동기 제출 시, 사용자가 양식을 제출하면 다른 양식 또는 웹 사이트의 별도의 섹션으로 리디렉션하는 것과 같은 별도의 환경에서 개발자 플러그를 사용합니다. 또한 작성자는 데이터를 다른 데이터 저장소에 전송하거나 사용자 지정 분석 엔진을 추가하는 것과 같은 별도의 서비스를 플러그 인할 수 있습니다. 비동기 제출 시, 적응형 양식은 양식이 다시 로드되지 않고 서버에서 전송된 양식 데이터의 유효성을 검사해도 해당 URL이 변경되지 않으므로 단일 페이지 응용 프로그램과 같이 작동합니다.

적응형 양식의 비동기 제출에 대한 자세한 내용은 을 참조하십시오.

## 비동기 제출 구성 {#configure}

적응형 양식의 비동기 제출을 구성하려면:

1. 적응형 양식 작성 모드에서 양식 컨테이너 개체를 선택하고 ![cmppr1을](assets/cmppr1.png) 눌러 속성을 엽니다.
1. 제출 **[!UICONTROL 속성]** 섹션에서 비동기 **[!UICONTROL 제출]**&#x200B;사용을 활성화합니다.
1. 제출 **[!UICONTROL 시]** 섹션에서 다음 옵션 중 하나를 선택하여 양식 제출 작업을 성공적으로 수행합니다.

   * **[!UICONTROL URL로 리디렉션]**: 양식 제출 시 지정된 URL 또는 페이지로 리디렉션합니다. URL을 지정하거나 [리디렉션 URL/경로] 필드에서 페이지의 경로를 **[!UICONTROL 찾아 선택할 수]** 있습니다.
   * **[!UICONTROL 메시지 표시]**: 양식 제출 시 메시지를 표시합니다. 메시지 표시 옵션 아래의 텍스트 필드에 메시지를 작성할 수 있습니다. 텍스트 필드는 리치 텍스트 서식을 지원합니다.

1. 속성을 저장하려면 ![check-button](assets/check-button1.png) 1을 누릅니다.

## 비동기 제출 작동 방식 {#how-asynchronous-submission-works}

AEM Forms은 양식 제출을 위한 기본 성공 및 오류 핸들러를 제공합니다. 처리기는 서버 응답을 기반으로 실행되는 클라이언트측 함수입니다. 양식이 전송되면 데이터가 서버로 전송되어 유효성 검사를 위해 클라이언트에 대한 응답과 함께 제출 시 성공 또는 오류 이벤트에 대한 정보를 반환합니다. 이 정보는 함수를 실행하기 위해 관련 처리기에 매개 변수로 전달됩니다.

또한 양식 작성자와 개발자는 양식 수준에서 규칙을 작성하여 기본 핸들러를 재정의할 수 있습니다. 자세한 내용은 규칙을 [사용하여 기본 핸들러 재정의를 참조하십시오](#custom).

먼저 성공 및 오류 이벤트에 대한 서버 응답을 검토하겠습니다.

### 제출 성공 이벤트에 대한 서버 응답 {#server-response-for-submission-success-event}

제출 성공 이벤트에 대한 서버 응답의 구조는 다음과 같습니다.

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

성공적인 양식 제출의 서버 응답에는 다음이 포함됩니다.

* 양식 데이터 형식: XML 또는 JSON
* XML 또는 JSON 형식의 양식 데이터
* 페이지로 리디렉션하거나 양식에 구성된 대로 메시지를 표시하는 선택 옵션
* 양식에 구성된 페이지 URL 또는 메시지 내용

성공 처리기는 서버 응답을 읽고 구성된 페이지 URL로 리디렉션하거나 메시지를 표시합니다.

### 제출 오류 이벤트에 대한 서버 응답 {#server-response-for-submission-error-event}

제출 오류 이벤트에 대한 서버 응답의 구조는 다음과 같습니다.

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

양식 제출 시 오류가 발생하는 경우 서버 응답에는 다음이 포함됩니다.

* 오류, 실패한 CAPTCHA 또는 서버측 유효성 검사 이유
* 유효성 검사에 실패한 필드의 SOM 표현식과 해당 오류 메시지가 포함된 오류 개체 목록

오류 처리기는 서버 응답을 읽고 이에 따라 양식에 오류 메시지를 표시합니다.

## 규칙을 사용하여 기본 핸들러 재정의 {#custom}

양식 개발자와 작성자는 코드 편집기에서 기본 핸들러를 무시하는 규칙을 양식 수준에서 작성할 수 있습니다. 성공 및 오류 이벤트에 대한 서버 응답은 개발자가 규칙에서 액세스할 수 있는 양식 수준 `$event.data` 에 표시됩니다.

성공 및 오류 이벤트를 처리하기 위해 코드 편집기에서 규칙을 작성하려면 다음 단계를 수행하십시오.

1. 작성 모드에서 응용 양식을 열고, 양식 개체를 선택한 다음 ![edit-rules1을](assets/edit-rules1.png) 눌러 규칙 편집기를 엽니다.
1. 양식 **[!UICONTROL 개체]** 트리에서 양식을 선택하고 만들기를 **[!UICONTROL 누릅니다]**.
1. 모드 **[!UICONTROL 선택 드롭다운에서]** 코드 편집기를 선택합니다.
1. 코드 편집기에서 코드 **[!UICONTROL 편집을 누릅니다]**. 확인 대화 **[!UICONTROL 상자에서]** 편집을 누릅니다.
1. 이벤트 **[!UICONTROL 드롭다운에서 제출]** 중 **[!UICONTROL 에]** 성공하 **[!UICONTROL 는 오류]** 를선택합니다.
1. 선택한 이벤트에 대한 규칙을 작성하고 **[!UICONTROL 완료를]** 눌러 규칙을 저장합니다.

