---
title: 렌더러를 위한 문서 세부 사항
seo-title: 렌더러를 위한 문서 세부 사항
description: AEM Forms 작업 영역에서 작업을 렌더링하여 지원되는 다양한 양식 및 파일 유형을 렌더링하는 방법에 대한 개념 정보입니다.
seo-description: AEM Forms 작업 영역에서 작업을 렌더링하여 지원되는 다양한 양식 및 파일 유형을 렌더링하는 방법에 대한 개념 정보입니다.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# 렌더러 {#document-details-for-renderer}에 대한 문서 세부 사항

## 소개 {#introduction}

AEM Forms 작업 영역에서 여러 양식 유형이 매끄럽게 지원됩니다. 이러한 쿠키에는 다음이 포함됩니다.

* PDF forms(XDP / Acrobat / 일반 PDF)
* 새로운 HTML 양식
* 이미지
* 제3자 응용 프로그램(예: 통신 관리)

이 문서에서는 의미론적 사용자 지정/구성 요소 재사용의 관점에서 이러한 렌더러의 작업을 설명하여 변환을 끊지 않고 고객 요구 사항을 충족할 수 있도록 합니다. AEM Forms 작업 영역에서 사용자 인터페이스/의미 변경을 허용하지만 서로 다른 양식 유형의 렌더링 논리를 변경하지 않는 것이 좋습니다. 그렇지 않으면 결과를 예측할 수 없습니다. 이 문서는 렌더링 논리 자체를 수정하지 않고 다른 포털에서 동일한 작업 영역 구성 요소를 사용하여 동일한 양식을 렌더링하는 것을 지원하는 지침/지식을 위한 것입니다.

## PDF forms {#pdf-forms}

PDF forms은 `PdfTaskForm View`에 의해 렌더링됩니다.

XDP 양식이 PDF로 렌더링될 때 FormsAugmenter 서비스에서 `FormBridge` JavaScript™이 추가됩니다. 이 JavaScript™(PDF 양식 내)는 양식 제출, 양식 저장 또는 오프라인 양식 작성과 같은 작업을 수행하는 데 도움이 됩니다.

AEM Forms 작업 영역에서 PDFTaskForm 보기는 `/lc/libs/ws/libs/ws/pdf.html`에 있는 중간 HTML을 통해 `FormBridge`javascript와 통신합니다. 흐름은 다음과 같습니다.

**PDFTaskForm 보기 - pdf.html**

`window.postMessage` / `window.attachEvent('message')`를 사용하여 통신합니다.

이 메서드는 부모 프레임과 iframe 사이의 통신 표준 방식입니다. 이전에 연 PDF forms의 기존 이벤트 리스너는 새 이벤트를 추가하기 전에 제거됩니다. 이 제거는 작업 세부 사항 보기에서 양식 탭과 작업 내역 탭 간의 전환도 고려합니다.

**pdf.html -  `FormBridge`렌더링된 PDF 내의 javascript**

`pdfObject.postMessage` / `pdfObject.messageHandler`를 사용하여 통신합니다.

이 메서드는 HTML에서 PDFJavaScript를 사용하는 표준 통신 방식입니다. 또한 PdfTaskForm 보기는 일반 PDF를 관리하고 선명하게 렌더링합니다.

>[!NOTE]
>
>PdfTaskForm 보기의 pdf.html / 내용을 수정하는 것은 권장되지 않습니다.

## 새 HTML Forms {#new-html-forms}

새 HTML 양식은 NewHTMLTaskForm 보기로 렌더링됩니다.

XDP 양식이 CRX에 배포된 모바일 양식 패키지를 사용하여 HTML로 렌더링될 때 양식 데이터를 저장하고 제출하는 다른 방법을 표시하는 추가 `FormBridge`JavaScript도 양식에 추가합니다.

이 JavaScript는 위의 PDF forms에서 참조한 것과 다르지만 유사한 용도로 사용됩니다.

>[!NOTE]
>
>NewHTMLTaskForm 보기의 내용은 수정하지 않는 것이 좋습니다.

## Flex Forms 및 안내선 {#flex-forms-and-guides}

Flex Forms은 SwfTaskForm으로 렌더링되고 안내선은 각각 HtmlTaskForm 보기로 렌더링됩니다.

AEM Forms 작업 영역에서 이러한 보기는 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`에 있는 중간 SWF를 사용하여 flex 양식/안내선을 구성하는 실제 SWF와 통신합니다.

통신은 `swfObject.postMessage` / `window.flexMessageHandler`을 사용하여 발생합니다.

이 프로토콜은 `WsNextAdapter.swf`에 의해 정의됩니다. 이전에 연 SWF 양식의 기존 `flexMessageHandlers`on window 객체는 새 양식을 추가하기 전에 제거됩니다. 또한 작업 세부 사항 보기에서 양식 탭과 작업 내역 탭 간의 전환을 고려합니다. `WsNextAdapter.swf` 는 저장 또는 제출과 같은 다양한 양식 작업을 수행하는 데 사용됩니다.

>[!NOTE]
>
>`WSNextAdapter.swf` 또는 SwfTaskForm/HtmlTaskForm 보기의 내용을 수정하는 것은 권장되지 않습니다.

## 타사 응용 프로그램(예: 통신 관리) {#third-party-applications-for-example-correspondence-management}

타사 애플리케이션은 ExtAppTaskForm 보기를 사용하여 렌더링됩니다.

**AEM Forms 작업 영역 커뮤니케이션에 대한 제3자 애플리케이션**

AEM Forms 작업 공간이 `window.global.postMessage([Message],[Payload])`에 수신됩니다.

[메시지] 는  `SubmitMessage`|  `CancelMessage`|  `ErrorMessage`|  `actionEnabledMessage`in the  `runtimeMap`. 필요에 따라 제3자 응용 프로그램에서 이 인터페이스를 사용하여 AEM Forms 작업 영역을 알려야 합니다. 작업 창을 정리할 수 있도록 AEM Forms 작업 영역에서 작업이 제출된 시점을 알고 있어야 하므로 이 인터페이스를 사용하는 것은 필수입니다.

**AEM Forms 작업 영역을 제3자 응용 프로그램 통신으로 변환**

AEM Forms 작업 영역의 직접 작업 단추가 표시되면 `window.[External-App-Name].getMessage([Action])`을 호출합니다. 여기서 `[Action]`은 `routeActionMap`에서 읽습니다. 제3자 응용 프로그램은 이 인터페이스를 수신한 다음 `postMessage ()` API를 통해 AEM Forms 작업 영역에 알려야 합니다.

예를 들어 Flex 응용 프로그램은 `ExternalInterface.addCallback('getMessage', listener)`을 정의하여 이 통신을 지원할 수 있습니다. 제3자 응용 프로그램이 자체 단추를 통해 양식 제출을 처리하려는 경우 `hideDirectActions = true() in the runtimeMap`을 지정해야 하며 이 리스너를 건너뛸 수 있습니다. 따라서 이 구문은 선택 사항입니다.

AEM Forms 작업 공간의 [메일 관리 통합에서 통신 관리와 관련하여 제3자 응용 프로그램 통합에 대해 자세히 읽을 수 있습니다](/help/forms/using/integrating-correspondence-management-html-workspace.md).
