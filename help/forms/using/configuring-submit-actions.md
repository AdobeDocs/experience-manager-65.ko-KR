---
title: 제출 작업 구성
seo-title: 제출 작업 구성
description: Forms에서는 제출 작업을 구성하여 제출 후 적응형 양식이 처리되는 방식을 정의할 수 있습니다. 내장된 제출 동작을 사용하거나 직접 작성할 수 있습니다.
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
feature: 적응형 양식
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 1%

---


# 제출 작업 구성{#configuring-the-submit-action}

## 작업 제출 소개 {#introduction-to-submit-actions}

사용자가 적응형 양식의 제출 단추를 클릭하면 제출 작업이 트리거됩니다. 적응형 양식에 제출 작업을 구성할 수 있습니다. 적응형 양식에서는 즉시 실행 작업을 몇 가지 제공합니다. 기본 제출 작업을 복사하고 확장하여 고유한 제출 작업을 만들 수 있습니다. 그러나 요구 사항에 따라 본인의 실행 동작을 작성하여 등록하면 제출된 양식에서 데이터를 처리할 수 있습니다. 제출 작업에서는 [동기 또는 비동기 제출](../../forms/using/asynchronous-submissions-adaptive-forms.md)을 사용할 수 있습니다.

세로 막대의 응용 양식 컨테이너 속성의 **제출** 섹션에서 제출 작업을 구성할 수 있습니다.

![제출 작업 구성](assets/thank-you-setting.png)

제출 작업 구성

적응형 양식에 사용할 수 있는 기본 제출 작업은 다음과 같습니다.

* REST 끝점에 제출
* 이메일 보내기
* 이메일을 통해 PDF 보내기
* Forms Workflow 호출
* 양식 데이터 모델을 사용하여 제출
* Forms 포털 제출 작업
* AEM 워크플로우 호출

>[!NOTE]
>
>전자 메일로 PDF 보내기 작업은 XFA 템플릿을 양식 모델로 사용하는 적응형 양식에만 적용할 수 있습니다.

>[!NOTE]
>
>[AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>존재함. 첨부 파일을 일시적으로 저장하려면 디렉토리가 필요합니다. 디렉토리가 없는 경우 디렉토리를 만듭니다.

>[!CAUTION]
>
>[양식 템플릿, 양식 데이터 모델 또는 XML 또는 JSON 데이터 불만 사항이 있는 스키마(XML 스키마, JSON 스키마, 양식 템플릿 또는 양식 데이터 모델)에 ](../../forms/using/prepopulate-adaptive-form-fields.md), &lt;afBoundData> 및 &lt;/afUnbinedData> 태그를 포함하지 않는 스키마(XML 스키마, JSON 스키마, 양식 템플릿 또는 양식 데이터 모델)를 미리 채우기 한 경우 경계 없는 필드(경계 없는 필드는 적응형 양식의 [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) 속성이 없는 적응형 양식 필드)가 손실됩니다.

적응형 양식에 대한 사용자 정의 제출 동작을 작성하여 사용 사례를 준수할 수 있습니다. 자세한 내용은 적응형 양식](../../forms/using/custom-submit-action-form.md)에 대한 사용자 정의 제출 작업 쓰기를 참조하십시오.[

## REST 끝점 {#submit-to-rest-endpoint}에 제출

**REST 끝점에 제출** 제출 옵션은 HTTP GET 요청의 일부로 양식에 입력된 데이터를 구성된 확인 페이지로 전달합니다. 요청할 필드의 이름을 추가할 수 있습니다. 요청의 형식은 다음과 같습니다.

`{fieldName}={request parameter name}`

아래 이미지에 표시된 대로, 다음 작업을 위해 **textbox** 및 **숫자 상자** 필드에서 복사한 값을 사용하여 `param1` 및 `param2`이(가) 매개 변수로 전달됩니다.

또한 **POST 요청 활성화**&#x200B;와 요청을 게시할 URL을 제공할 수도 있습니다. 양식을 호스팅하는 Experience Manager 서버에 데이터를 전송하려면 Experience Manager 서버의 루트 경로에 해당하는 상대 경로를 사용합니다. 예: /content/forms/af/SampleForm.html. 데이터를 다른 서버에 제출하려면 절대 경로를 사용합니다.

![나머지 끝점 제출 작업 구성](assets/action-config.png)

나머지 끝점 제출 작업 구성

>[!NOTE]
필드를 REST URL의 매개 변수로 전달하려면 필드가 다른 패널에 배치되더라도 모든 필드에 요소 이름이 달라야 합니다.

### 리소스 또는 외부 REST 엔드 포인트에 제출된 데이터 게시  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

**REST 끝점에 제출** 작업을 사용하여 제출된 데이터를 나머지 URL에 게시합니다. URL은 내부(양식이 렌더링되는 서버) 또는 외부 서버일 수 있습니다.

내부 서버에 데이터를 게시하려면 리소스의 경로를 제공합니다. 데이터는 리소스의 경로에 게시됩니다. 예: /content/restEndPoint. 이러한 게시물 요청의 경우 제출 요청의 인증 정보가 사용됩니다.

외부 서버에 데이터를 게시하려면 URL을 제공합니다. URL의 형식은 https://host:port/path_to_rest_end_point입니다. POST 요청을 익명으로 처리하도록 경로를 구성해야 합니다.

![감사 인사 페이지 매개 변수로 전달된 필드 값에 대한 매핑](assets/post-enabled-actionconfig.png)

위의 예에서, `textbox`에 입력한 정보는 매개 변수 `param1`을 사용하여 캡처됩니다. `param1`을(를) 사용하여 캡처한 데이터를 게시하는 구문은 다음과 같습니다.

`String data=request.getParameter("param1");`

마찬가지로 XML 데이터 및 첨부 파일을 게시하는 데 사용하는 매개 변수는 `dataXml` 및 `attachments`입니다.

예를 들어 스크립트에서 이 두 매개 변수를 사용하여 데이터를 나머지 끝점으로 구문 분석할 수 있습니다. 다음 구문을 사용하여 데이터를 저장하고 분석합니다.

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

이 예에서 `data`은 XML 데이터를 저장하고 `att`은 첨부 데이터를 저장합니다.

## 이메일 보내기 {#send-email}

**전자 메일 보내기** 전송 작업은 양식을 성공적으로 제출할 때 하나 이상의 받는 사람에게 전자 메일을 보냅니다. 생성된 이메일에는 양식 데이터가 사전 정의된 형식으로 포함될 수 있습니다.

>[!NOTE]
전자 메일에 양식 데이터를 포함하려면 모든 양식 필드에 다른 요소 이름이 있어야 합니다(다른 패널에 배치되었더라도).

## 이메일 {#send-pdf-via-email}을(를) 통해 PDF 보내기

**전자 메일**&#x200B;을 통해 PDF 보내기 작업은 양식 데이터가 포함된 PDF가 포함된 이메일을 하나 이상의 수신자에게 보내어 양식을 성공적으로 제출합니다.

>[!NOTE]
이 전송 작업은 기록 문서 템플릿이 있는 XFA 기반 적응형 양식 및 XSD 기반 적응형 양식에 사용할 수 있습니다.

## Forms Workflow {#invoke-a-forms-workflow} 호출

**Forms Workflow에 제출** 제출 옵션은 데이터 xml 및 첨부 파일(있는 경우)을 JEE 프로세스에서 기존 Adobe LiveCycle 또는 AEM Forms으로 보냅니다.

Forms Workflow 제출 작업을 구성하는 방법에 대한 자세한 내용은 [양식 워크플로우를 사용하여 양식 데이터 제출 및 처리](../../forms/using/submit-form-data-livecycle-process.md)를 참조하십시오.

## 양식 데이터 모델을 사용하여 제출 {#submit-using-form-data-model}

**양식 데이터 모델을 사용하여 제출** 작업을 제출하면 양식 데이터 모델의 지정된 데이터 모델 개체에 대해 제출된 적응형 양식 데이터를 해당 데이터 소스에 기록합니다. 제출 작업을 구성할 때 데이터 소스에 다시 쓸 데이터를 포함하는 데이터 모델 개체를 선택할 수 있습니다.

또한 양식 데이터 모델과 기록 문서(DoR)를 사용하여 양식 첨부 파일을 데이터 소스에 제출할 수 있습니다.

양식 데이터 모델에 대한 자세한 내용은 [AEM Forms 데이터 통합](../../forms/using/data-integration.md)을 참조하십시오.

## Forms 포털 제출 작업 {#forms-portal-submit-action}

**Forms Portal 제출 작업** 옵션은 AEM Forms Portal을 통해 양식 데이터를 사용할 수 있도록 합니다.

Forms 포털 및 제출 작업에 대한 자세한 내용은 [초안 및 제출 구성 요소](../../forms/using/draft-submission-component.md)를 참조하십시오.

## AEM 작업 과정 호출 {#invoke-an-aem-workflow}

**AEM Workflow 호출** 제출 작업은 AEM Workflow에 적응형 양식을 연결합니다. 양식이 제출되면 연관된 워크플로우는 처리 노드에서 자동으로 시작됩니다. 또한 데이터 파일, 첨부 파일 및 기록 문서(해당하는 경우)를 워크플로우의 페이로드 위치에 배치합니다.

**AEM Workflow** 제출 작업을 호출하기 전에 [Experience Manager DS 설정](../../forms/using/configuring-the-processing-server-url-.md)을 구성합니다. AEM 워크플로우 만들기에 대한 자세한 내용은 OSGi](../../forms/using/aem-forms-workflow.md)의 양식 중심 워크플로우를 참조하십시오.[

## 응용 양식 {#server-side-revalidation-in-adaptive-form}의 서버측 재유효성 검사

일반적으로 모든 온라인 데이터 캡처 시스템에서 개발자는 일부 JavaScript 유효성 검사를 클라이언트측에 배치하여 몇 가지 비즈니스 규칙을 적용합니다. 그러나 최신 브라우저에서 최종 사용자는 이러한 유효성 검사를 건너뛰고 웹 브라우저 개발 도구 콘솔과 같은 다양한 기법을 사용하여 수동으로 제출 작업을 수행할 수 있습니다. 이러한 기법은 적응형 양식에 대해서도 유효한 a입니다. 양식 개발자는 다양한 유효성 검사 논리를 만들 수 있지만 기술적으로 최종 사용자는 유효성 검사 논리를 우회하여 잘못된 데이터를 서버에 제출할 수 있습니다. 잘못된 데이터는 양식 작성자가 적용한 비즈니스 규칙을 위반합니다.

서버측 재유효성 검사 기능은 적응형 양식 작성자가 서버에서 적응형 양식을 디자인하는 동안 제공한 유효성 검사를 실행하는 기능도 제공합니다. 양식 유효성 검사 측면에서 표현되는 데이터 제출 및 비즈니스 규칙 위반의 발생 가능성을 차단합니다.

### 서버에서 유효성을 검사하는 방법{#what-to-validate-on-server-br}

서버에서 다시 실행되는 응용 양식의 OTB(즉시 사용 가능한 필드 유효성 검사) 모두 다음과 같습니다.

* 필수
* 유효성 검사 그림 절
* 유효성 검사 표현식

### 서버측 유효성 검사 활성화 {#enabling-server-side-validation-br}

사이드바의 응용 양식 컨테이너 아래에 있는 **서버의 유효성 검사**&#x200B;를 사용하여 현재 양식에 대한 서버측 유효성 검사를 활성화하거나 비활성화합니다.

![서버측 유효성 검사 활성화](assets/revalidate-on-server.png)

서버측 유효성 검사 활성화

최종 사용자가 이러한 유효성 검사를 무시하고 양식을 제출하면 서버가 다시 유효성 검사를 수행합니다. 서버 끝에 유효성 검사가 실패하면 제출 트랜잭션이 중지됩니다. 최종 사용자에게 원본 양식이 다시 표시됩니다. 캡처한 데이터와 제출된 데이터가 오류로 표시됩니다.

>[!NOTE]
서버측 유효성 검사는 양식 모델의 유효성을 검사합니다. 유효성 검사를 위해 별도의 클라이언트 라이브러리를 만들고 동일한 클라이언트 라이브러리에서 HTML 스타일 및 DOM 조작 등의 다른 작업과 함께 사용하지 않는 것이 좋습니다.

### 유효성 검사 표현식에서 사용자 지정 함수 지원 {#supporting-custom-functions-in-validation-expressions-br}

복잡한 유효성 검사 규칙이 있는 경우 정확한 유효성 검사 스크립트가 사용자 지정 함수에 존재하며 작성자는 필드 유효성 검사 표현식에서 이러한 사용자 지정 함수를 호출합니다. 양식 작성자는 서버측 유효성 검사를 수행하는 동안 이 사용자 지정 함수 라이브러리를 알리고 사용할 수 있도록 하려면 아래 표시된 대로 응용 양식 컨테이너 속성의 **기본** 탭 아래에 AEM 클라이언트 라이브러리의 이름을 구성할 수 있습니다.

![유효성 검사 표현식에서 사용자 지정 함수 지원](assets/clientlib-cat.png)

유효성 검사 표현식에서 사용자 지정 함수 지원

작성자는 적응형 양식당 customJavaScript 라이브러리를 구성할 수 있습니다. 라이브러리에서 재사용할 수 있는 함수만 유지하면 jquery 및 belline.js 타사 라이브러리에 종속됩니다.

## 제출 작업 {#error-handling-on-submit-action} 처리 오류

Experience Manager 보안 및 강화 지침의 일부로, 404.jsp 및 500.jsp와 같은 사용자 정의 오류 페이지를 구성합니다. 이러한 핸들러는 양식 제출 시 404 또는 500 오류가 나타날 때 호출됩니다. 이러한 오류 코드가 게시 노드에서 트리거될 때도 핸들러가 호출됩니다.

자세한 내용은 오류 처리기](/help/sites-developing/customizing-errorhandler-pages.md)에 표시된 페이지 사용자 지정을 참조하십시오.[
