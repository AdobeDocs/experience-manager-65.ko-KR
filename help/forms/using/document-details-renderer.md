---
title: 렌더러에 대한 문서 세부 정보
seo-title: 렌더러에 대한 문서 세부 정보
description: AEM Forms 작업 공간에서 렌더링이 작동하는 방식으로 지원되는 다양한 양식 및 파일 유형을 렌더링하는 방법에 대한 개념적 정보입니다.
seo-description: AEM Forms 작업 공간에서 렌더링이 작동하는 방식으로 지원되는 다양한 양식 및 파일 유형을 렌더링하는 방법에 대한 개념적 정보입니다.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# 렌더러 {#document-details-for-renderer}에 대한 문서 세부 정보

## 소개 {#introduction}

AEM Forms 작업 공간에서 여러 양식 유형이 원활하게 지원됩니다. 이러한 쿠키에는 다음이 포함됩니다.

* PDF forms(XDP/Acrobat/Flat PDF)
* 새 HTML 양식
* 이미지
* 타사 애플리케이션(예: 서신 관리)

이 문서에서는 의미론적 사용자 지정/구성 요소 재사용 관점에서 이러한 렌더러의 작업을 설명하므로 변환 없이 고객 요구 사항을 충족할 수 있습니다. AEM Forms 작업 공간에서는 모든 사용자 인터페이스/시맨틱 변경을 허용하지만, 다른 양식 유형의 렌더링 로직은 변경하지 않는 것이 좋습니다. 그렇지 않으면 결과를 예측할 수 없습니다. 이 문서는 동일한 양식 렌더링을 지원하고, 서로 다른 포털에서 동일한 작업 공간 구성 요소를 사용하며, 렌더링 논리 자체를 수정하는 것이 아닌,

## PDF forms {#pdf-forms}

PDF forms은 `PdfTaskForm View`에 의해 렌더링됩니다.

XDP 양식이 PDF로 렌더링되면 FormsAugmenter 서비스에 `FormBridge` JavaScript™이 추가됩니다. 이 JavaScript™(PDF 양식 내부)는 양식 제출, 양식 저장 또는 양식 오프라인과 같은 작업을 수행하는 데 도움이 됩니다.

AEM Forms 작업 영역에서 PDFTaskForm 보기는 `FormBridge`Javascript와 통신하며, `/lc/libs/ws/libs/ws/pdf.html`에 있는 중간 HTML을 통해 전달됩니다. 흐름은 다음과 같습니다.

**PDFTaskForm 보기 - pdf.html**

`window.postMessage` / `window.attachEvent('message')`을 사용하여 통신합니다.

이 방법은 상위 프레임과 iframe 간의 표준 통신 방법입니다. 이전에 연 PDF forms의 기존 이벤트 리스너는 새 이벤트를 추가하기 전에 제거됩니다. 이 삭제는 작업 세부 사항 보기의 양식 탭과 기록 탭 간의 전환을 고려합니다.

**pdf.html -  `FormBridge`렌더링된 PDF 내의 javascript**

`pdfObject.postMessage` / `pdfObject.messageHandler`을 사용하여 통신합니다.

이 메서드는 HTML에서 PDFJavaScript와 통신하는 표준 방법입니다. 또한 PdfTaskForm 보기에서 일반 PDF를 관리하고 명확하게 렌더링합니다.

>[!NOTE]
>
>PdfTaskForm 보기의 pdf.html / 컨텐츠를 수정하지 않는 것이 좋습니다.

## 새 HTML Forms {#new-html-forms}

새 HTML 양식이 NewHTMLTaskForm 보기에 의해 렌더링됩니다.

XDP Form이 CRX에 배포된 모바일 양식 패키지를 사용하여 HTML로 렌더링되면 양식에 추가 `FormBridge`JavaScript도 추가되며, 이는 양식 데이터를 저장하고 제출하는 다른 방법을 노출합니다.

이 JavaScript는 위의 PDF forms에서 참조한 것과는 다르지만 비슷한 목적을 제공합니다.

>[!NOTE]
>
>NewHTMLTaskForm 보기의 내용은 수정하지 않는 것이 좋습니다.

## Flex Forms 및 안내서 {#flex-forms-and-guides}

Flex Forms은 SwfTaskForm으로 렌더링되고 가이드는 각각 HtmlTaskForm 보기로 렌더링됩니다.

AEM Forms 작업 영역에서 이러한 뷰는 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`에 있는 중간 SWF를 사용하여 플렉스 양식/가이드를 구성하는 실제 SWF와 통신합니다

통신은 `swfObject.postMessage` / `window.flexMessageHandler`을 사용하여 발생합니다.

이 프로토콜은 `WsNextAdapter.swf`에 의해 정의됩니다. 이전에 연 SWF Forms의 기존 `flexMessageHandlers`는 새 SWF Forms를 추가하기 전에 제거됩니다. 논리는 작업 세부 사항 보기의 양식 탭과 기록 탭 간의 전환을 고려합니다. `WsNextAdapter.swf` 저장 또는 제출과 같은 다양한 양식 작업을 수행하는 데 사용됩니다.

>[!NOTE]
>
>`WSNextAdapter.swf` 또는 SwfTaskForm / HtmlTaskForm 보기의 내용을 수정하지 않는 것이 좋습니다.

## 타사 애플리케이션(예: 서신 관리) {#third-party-applications-for-example-correspondence-management}

타사 응용 프로그램이 ExtAppTaskForm 보기를 사용하여 렌더링됩니다.

**AEM Forms 작업 공간 커뮤니케이션에 대한 타사 애플리케이션**

AEM Forms 작업 영역이 `window.global.postMessage([Message],[Payload])`에서 수신 대기합니다.

[] 메시지는  `SubmitMessage`|  `CancelMessage`|  `ErrorMessage`|  `actionEnabledMessage`in  `runtimeMap`. 타사 애플리케이션은 이 인터페이스를 사용하여 AEM Forms 작업 공간에 필요에 따라 알려야 합니다. 작업 창을 정리할 수 있도록 작업이 제출된 시점을 AEM Forms 작업 영역에서 알고 있어야 하므로 이 인터페이스를 사용하는 것은 필수입니다.

**AEM Forms 작업 공간과 타사 애플리케이션 통신**

AEM Forms 작업 공간의 직접 작업 단추가 표시되면 `window.[External-App-Name].getMessage([Action])`을 호출합니다. 여기서 `[Action]`은 `routeActionMap`에서 읽습니다. 타사 애플리케이션은 이 인터페이스를 수신한 다음 `postMessage ()` API를 통해 AEM Forms 작업 공간에 알려야 합니다.

예를 들어 Flex 애플리케이션에서 이 통신을 지원하도록 `ExternalInterface.addCallback('getMessage', listener)`을 정의할 수 있습니다. 타사 응용 프로그램이 자체 단추를 통해 양식 제출을 처리하려는 경우 `hideDirectActions = true() in the runtimeMap` 을 지정해야 하며 이 수신기를 건너뛸 수 있습니다. 따라서 이 구문은 선택 사항입니다.

[AEM Forms 작업 공간에서 서신 관리 통합](/help/forms/using/integrating-correspondence-management-html-workspace.md)에서 서신 관리와 관련된 타사 애플리케이션 통합에 대해 자세히 읽어볼 수 있습니다.
