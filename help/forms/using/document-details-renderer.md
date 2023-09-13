---
title: 렌더러에 대한 문서 세부 정보
description: AEM Forms 작업 영역에서 렌더링이 작동하여 지원되는 다양한 양식 및 파일 유형을 렌더링하는 방법에 대한 개념 정보입니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# 렌더러에 대한 문서 세부 정보 {#document-details-for-renderer}

## 소개 {#introduction}

AEM Forms 작업 영역에서는 여러 양식 유형이 원활하게 지원됩니다. 여기에는 다음이 포함됩니다.

* PDF forms(XDP / Acroform / Flat PDF)
* 새 HTML 양식
* 이미지
* 서드파티 애플리케이션(예: 서신 관리)

이 문서에서는 시맨틱 사용자 지정/구성 요소 재사용 관점에서 이러한 렌더러의 작업에 대해 설명하므로 렌디션을 손상시키지 않고 고객 요구 사항을 충족합니다. AEM Forms 작업 영역에서는 모든 사용자 인터페이스/의미 체계 변경을 허용하지만, 다른 양식 유형의 렌더링 논리는 변경하지 않는 것이 좋습니다. 그렇지 않으면 결과를 예측할 수 없습니다. 이 문서는 다른 포털에서 동일한 작업 영역 구성 요소를 사용하여 동일한 양식을 렌더링하는 것을 지원하는 지침/지식용이며 렌더링 논리 자체를 수정하는 것은 아닙니다.

## PDF forms {#pdf-forms}

PDF forms은 다음에 의해 렌더링됩니다. `PdfTaskForm View`.

XDP 양식이 PDF으로 렌더링될 때 `FormBridge` JavaScript™이 FormsAugmenter 서비스에 의해 추가됩니다. 이 JavaScript™(PDF 양식 내)는 양식 제출, 양식 저장, 양식 오프라인 수행과 같은 작업을 수행하는 데 도움이 됩니다.

AEM Forms 작업 영역에서 PDFTaskForm 보기는 와 통신합니다. `FormBridge`JavaScript, 의 중간 HTML 제공 `/lc/libs/ws/libs/ws/pdf.html`. 흐름은 다음과 같습니다.

**PDFTaskForm 보기 - pdf.html**

을 사용하여 통신 `window.postMessage` / `window.attachEvent('message')`

이 방법은 상위 프레임과 iframe 간의 표준 통신 방법입니다. 이전에 연 PDF forms의 기존 이벤트 리스너는 새 이벤트를 추가하기 전에 제거됩니다. 이 경우 작업 세부 정보 보기의 양식 탭과 내역 탭 간 전환도 고려됩니다.

**pdf.html - `FormBridge`렌더링된 PDF 내부의 JavaScript**

을 사용하여 통신 `pdfObject.postMessage` / `pdfObject.messageHandler`

이 메서드는 HTML에서 PDFJavaScript와 통신하는 표준 방법입니다. PdfTaskForm 뷰도 플랫 PDF을 처리하고 일반 렌더링합니다.

>[!NOTE]
>
>PdfTaskForm 보기의 pdf.html / 콘텐츠는 편집하지 않는 것이 좋습니다.

## 새 HTML Forms {#new-html-forms}

새 HTML 양식은 NewHTMLTaskForm View에 의해 렌더링됩니다.

XDP Form이 CRX에 배포된 모바일 양식 패키지를 사용하여 HTML으로 렌더링될 때 추가 기능도 추가됩니다 `FormBridge`양식에 JavaScript를 추가하여 양식 데이터를 저장하고 제출하는 다양한 메서드를 표시합니다.

이 JavaScript는 위의 PDF forms에서 참조된 JavaScript와 다르지만 유사한 목적을 제공합니다.

>[!NOTE]
>
>Adobe은 NewHTMLTaskForm 보기의 내용을 편집하지 않는 것이 좋습니다.

## Flex Forms 및 안내서 {#flex-forms-and-guides}

Flex Forms은 SwfTaskForm에 의해 렌더링되고 안내선은 HtmlTaskForm 뷰에 의해 각각 렌더링됩니다.

AEM Forms Workspace에서 이러한 보기는 의 중간 SWF을 사용하여 Flex® 양식/안내서를 구성하는 실제 SWF과 커뮤니케이션합니다 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

커뮤니케이션은 다음을 사용하여 수행됩니다. `swfObject.postMessage` / `window.flexMessageHandler`.

이 프로토콜은 `WsNextAdapter.swf`. 기존 `flexMessageHandlers`window 객체에서는 이전에 연 SWF 양식에서 새 양식을 추가하기 전에 이 양식이 제거됩니다. 또한 작업 세부 사항 보기의 양식 탭과 내역 탭 간 전환을 고려합니다. 다음 `WsNextAdapter.swf` 저장 또는 제출과 같은 다양한 양식 작업을 수행하는 데 사용됩니다.

>[!NOTE]
>
>수정하지 않는 것이 좋습니다. `WSNextAdapter.swf` 또는 SwfTaskForm/HtmlTaskForm 뷰의 내용을 볼 수 있습니다.

## 서드파티 애플리케이션(예: 서신 관리) {#third-party-applications-for-example-correspondence-management}

타사 응용 프로그램은 ExtAppTaskForm 보기를 사용하여 렌더링됩니다.

**AEM Forms 작업 영역 통신에 대한 서드파티 애플리케이션**

AEM Forms workspace는 `window.global.postMessage([Message],[Payload])`

[메시지] 은(는) (으)로 지정된 문자열일 수 있습니다 `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`다음에서 `runtimeMap`. 서드파티 애플리케이션은 필요에 따라 이 인터페이스를 사용하여 AEM Forms 작업 영역에 알려야 합니다. AEM Forms 작업 영역은 작업이 제출될 때 작업 창을 정리할 수 있음을 알아야 하므로 이 인터페이스를 사용해야 합니다.

**AEM Forms 작업 영역과 타사 애플리케이션 통신**

AEM Forms 작업 영역의 직접 작업 버튼이 표시되면 `window.[External-App-Name].getMessage([Action])`, 여기서 `[Action]` 에서 읽음 `routeActionMap`. 서드파티 애플리케이션은 이 인터페이스를 수신한 다음 를 통해 AEM Forms 작업 영역에 알려야 합니다. `postMessage ()` API.

예를 들어 Flex 애플리케이션은 `ExternalInterface.addCallback('getMessage', listener)` 이 커뮤니케이션을 지원합니다. 서드파티 애플리케이션이 자체 버튼을 통해 양식 제출을 처리하려는 경우 다음을 지정해야 합니다 `hideDirectActions = true() in the runtimeMap` 이 청취자를 건너뛸 수도 있습니다. 따라서 이 구문은 선택 사항입니다.

다음 위치에서 서신 관리와 관련된 타사 애플리케이션 통합에 대해 자세히 알아볼 수 있습니다. [AEM Forms 작업 영역에서 서신 관리 통합](/help/forms/using/integrating-correspondence-management-html-workspace.md).
