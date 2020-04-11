---
title: 렌더러를 위한 문서 세부 사항
seo-title: 렌더러를 위한 문서 세부 사항
description: AEM Forms 작업 영역에서 렌더링하여 지원되는 다양한 양식 및 파일 유형을 렌더링하는 방법에 대한 개념 정보입니다.
seo-description: AEM Forms 작업 영역에서 렌더링하여 지원되는 다양한 양식 및 파일 유형을 렌더링하는 방법에 대한 개념 정보입니다.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 렌더러를 위한 문서 세부 사항 {#document-details-for-renderer}

## 소개 {#introduction}

AEM Forms 작업 영역에서 여러 양식 유형이 매끄럽게 지원됩니다. 이러한 쿠키에는 다음이 포함됩니다.

* PDF 양식(XDP / Acrobat / 일반 PDF)
* 새로운 HTML 양식
* 이미지
* 타사 애플리케이션(예: 통신 관리)

이 문서에서는 의미론적 사용자 지정/구성 요소 재사용의 관점에서 이러한 렌더러의 작업을 설명하므로 변환의 중단 없이 고객 요구 사항을 충족할 수 있습니다. AEM Forms 작업 영역에서 모든 사용자 인터페이스/의미 변경을 허용하지만, 다른 양식 유형의 렌더링 논리를 변경하지 않는 것이 좋습니다. 그렇지 않으면 결과를 예측할 수 없습니다. 이 문서는 다른 포털에서 동일한 작업 영역 구성 요소를 사용하고 렌더링 논리 자체를 수정하는 것이 아니라 동일한 양식을 렌더링하는 것을 지원하기 위한 안내 및 지식을 위한 것입니다.

## PDF 양식 {#pdf-forms}

PDF 양식은 로 렌더링됩니다 `PdfTaskForm View`.

XDP 양식이 PDF로 렌더링되면 FormsAugmenter `FormBridge` 서비스에서 JavaScript™가 추가됩니다. 이 JavaScript™(PDF 양식 내부)는 양식 제출, 양식 저장 또는 양식 오프라인과 같은 작업을 수행하는 데 도움이 됩니다.

AEM Forms 작업 영역에서 PDFTaskForm 보기는 에 있는 중간 HTML을 통해 `FormBridge`javascript와 통신합니다 `/lc/libs/ws/libs/ws/pdf.html`. 흐름은 다음과 같습니다.

**PDFTaskForm 보기 - pdf.html**

/를 사용하여 `window.postMessage` 커뮤니케이션 `window.attachEvent('message')`

이 메서드는 부모 프레임과 iframe 사이의 통신 표준 방식입니다. 이전에 연 PDF 양식의 기존 이벤트 리스너는 새 양식을 추가하기 전에 제거됩니다. 이 제거는 작업 세부 사항 보기에서 양식 탭과 작업 내역 탭 간 전환을 고려합니다.

**pdf.html -`FormBridge`렌더링된 PDF 내의 javascript**

/를 사용하여 `pdfObject.postMessage` 커뮤니케이션 `pdfObject.messageHandler`

이 방법은 HTML의 PDF javascript를 사용하는 표준 통신 방법입니다. 또한 PdfTaskForm 보기에서는 일반 PDF를 관리하고 선명하게 렌더링할 수 있습니다.

>[!NOTE]
>
>PdfTaskForm 보기의 pdf.html / 내용을 수정하는 것은 권장되지 않습니다.

## 새 HTML 양식 {#new-html-forms}

새 HTML 양식은 NewHTMLTaskForm 보기로 렌더링됩니다.

XDP 양식이 CRX에 배포된 모바일 양식 패키지를 사용하여 HTML 파섹 `FormBridge`

이 javascript는 위에서 언급한 PDF Forms와 다르지만 유사한 용도로 사용됩니다.

>[!NOTE]
>
>NewHTMLTaskForm 보기의 내용은 수정하지 않는 것이 좋습니다.

## Flex 양식 및 가이드 {#flex-forms-and-guides}

Flex Forms는 SwfTaskForm으로 렌더링되고 안내선은 HtmlTaskForm 보기에서 각각 렌더링됩니다.

AEM Forms 작업 영역에서 이러한 보기는 다음 위치에 있는 중간 SWF를 사용하여 flex 양식/안내서를 구성하는 실제 SWF와 통신합니다. `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

통신은 `swfObject.postMessage` /를 사용하여 `window.flexMessageHandler`이루어집니다.

이 프로토콜은 에 의해 정의됩니다 `WsNextAdapter.swf`. 이전에 `flexMessageHandlers`연 SWF 양식의 창 오브젝트는 새 양식을 추가하기 전에 제거됩니다. 또한 로직은 작업 세부 사항 보기에서 양식 탭과 작업 내역 탭 간 전환을 고려합니다. `WsNextAdapter.swf` 는 저장 또는 제출과 같은 다양한 양식 작업을 수행하는 데 사용됩니다.

>[!NOTE]
>
>SwfTaskForm/HtmlTaskForm `WSNextAdapter.swf` 보기의 내용이나 내용을 수정하는 것은 권장되지 않습니다.

## 타사 애플리케이션(예: 통신 관리) {#third-party-applications-for-example-correspondence-management}

타사 애플리케이션은 ExtAppTaskForm 보기를 사용하여 렌더링됩니다.

**AEM Forms 작업 영역 통신에 대한 타사 애플리케이션**

AEM Forms 작업 영역은 `window.global.postMessage([Message],[Payload])`

[메시지는]`SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`in the `runtimeMap`. 타사 애플리케이션은 이 인터페이스를 사용하여 필요에 따라 AEM Forms 작업 영역을 알려야 합니다. 작업 창을 정리할 수 있도록 AEM Forms 작업 영역에서 작업이 제출되는 시기를 알아야 하므로 이 인터페이스를 사용하는 것은 필수입니다.

**타사 애플리케이션 커뮤니케이션에 대한 AEM Forms 작업 영역**

AEM Forms 작업 영역의 직접 작업 단추가 표시되면 `window.[External-App-Name].getMessage([Action])`여기서 [ `Action]` ]를 `routeActionMap`읽습니다. 타사 애플리케이션은 이 인터페이스를 수신한 다음 API를 통해 AEM Forms 작업 영역에 알려야 `postMessage ()` 합니다.

예를 들어 Flex 애플리케이션은 이러한 커뮤니케이션을 `ExternalInterface.addCallback('getMessage', listener)` 지원하도록 정의할 수 있습니다. 타사 응용 프로그램이 자체 단추를 통해 양식 제출을 처리하려는 경우 이 수신기를 `hideDirectActions = true() in the runtimeMap` 지정해야 합니다. 따라서 이 구문은 선택 사항입니다.

AEM Forms 작업 영역의 [](/help/forms/using/integrating-correspondence-management-html-workspace.md)통신 관리 통합에서 서드 파티 애플리케이션 통합에 대한 자세한 내용을 살펴볼 수 있습니다.
