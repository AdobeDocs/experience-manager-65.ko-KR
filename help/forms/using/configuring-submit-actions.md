---
title: 제출 작업 구성
seo-title: Configuring the Submit action
description: Forms을 사용하면 제출 후 적응형 양식을 처리하는 방법을 정의하기 위한 제출 작업을 구성할 수 있습니다. 내장된 제출 작업을 사용하거나 처음부터 직접 작성할 수 있습니다.
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
feature: Adaptive Forms
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 0%

---

# 제출 작업 구성{#configuring-the-submit-action}

## 작업 제출 소개 {#introduction-to-submit-actions}

사용자가 적응형 양식에서 제출 단추를 클릭하면 제출 작업이 트리거됩니다. 적응형 양식에서 제출 작업을 구성할 수 있습니다. 적응형 양식은 즉시 제출 작업을 제공합니다. 기본 제출 작업을 복사 및 확장하여 고유한 제출 작업을 만들 수 있습니다. 그러나 요구 사항에 따라 고유한 제출 작업을 작성하고 등록하여 제출된 양식의 데이터를 처리할 수 있습니다. 제출 작업은 [동기 또는 비동기 제출](../../forms/using/asynchronous-submissions-adaptive-forms.md).

에서 제출 작업을 구성할 수 있습니다 **제출** 섹션에 있는 세로 막대에서 적응형 양식 컨테이너 속성의 섹션을 참조하십시오.

![제출 작업 구성](assets/thank-you-setting.png)

제출 작업 구성

적응형 양식에서 사용할 수 있는 기본 제출 작업은 다음과 같습니다.

* REST 엔드포인트에 제출
* 이메일 보내기
* 이메일을 통해 PDF 보내기
* Forms Workflow 호출
* 양식 데이터 모델을 사용하여 제출
* Forms 포털 제출 작업
* AEM 워크플로우 호출

>[!NOTE]
>
>이메일 제출 작업을 통해 PDF 전송 작업은 XFA 템플릿을 양식 모델로 사용하는 적응형 양식에만 적용할 수 있습니다.

>[!NOTE]
>
>다음을 확인합니다. [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>존재함. 첨부 파일을 임시 저장하려면 디렉터리가 필요합니다. 디렉토리가 없는 경우 디렉토리를 만듭니다.

>[!CAUTION]
>
>만약 [미리 채우기](../../forms/using/prepopulate-adaptive-form-fields.md) 데이터가 포함되지 않은 스키마(XML 스키마, JSON 스키마, 양식 템플릿 또는 양식 데이터 모델 또는 양식 데이터 모델)에 대한 XML 또는 JSON 데이터 불만 사항이 있는 양식 템플릿, 양식 데이터 모델 또는 스키마 기반의 적응형 양식 &lt;afdata>, &lt;afbounddata>, 및 &lt;/afunbounddata> 태그를 만든 다음 경계 없는 필드의 데이터(경계 없는 필드는 다음과 같은 내용이 없는 적응형 양식 필드입니다 [빙드레이](../../forms/using/prepopulate-adaptive-form-fields.md) 적응형 양식의 속성)이 손실됩니다.

적응형 양식에 대한 사용자 지정 제출 작업을 작성하여 사용 사례를 이행할 수 있습니다. 자세한 내용은 [적응형 양식에 대한 사용자 지정 제출 작업 쓰기](../../forms/using/custom-submit-action-form.md).

## REST 엔드포인트에 제출 {#submit-to-rest-endpoint}

다음 **REST 엔드포인트에 제출** 제출 옵션은 HTTP GET 요청의 일부로 양식에 입력된 데이터를 구성된 확인 페이지에 전달합니다. 요청할 필드의 이름을 추가할 수 있습니다. 요청 형식은 다음과 같습니다.

`{fieldName}={request parameter name}`

아래 이미지에 표시된 대로, `param1` 및 `param2` 에서 복사한 값을 사용하여 매개 변수로 전달됩니다 **텍스트 상자** 및 **숫자 상자** 다음 작업에 대한 필드입니다.

다음을 수행할 수도 있습니다 **POST 요청 활성화** 요청을 게시할 URL을 제공합니다. 양식을 호스팅하는 Experience Manager 서버에 데이터를 제출하려면 Experience Manager 서버의 루트 경로에 해당하는 상대 경로를 사용합니다. 예: /content/forms/af/SampleForm.html 다른 서버에 데이터를 제출하려면 절대 경로를 사용합니다.

![Rest 끝점 전송 작업 구성](assets/action-config.png)

Rest 끝점 전송 작업 구성

>[!NOTE]
필드를 REST URL에서 매개 변수로 전달하려면 필드가 다른 패널에 배치되더라도 모든 필드에 다른 요소 이름이 있어야 합니다.

### 리소스 또는 외부 rest 엔드포인트에 제출된 데이터 게시  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

를 사용하십시오 **REST 끝점에 제출** 작업을 수행하여 제출된 데이터를 rest URL에 게시합니다. URL은 내부(양식이 렌더링되는 서버) 또는 외부 서버일 수 있습니다.

내부 서버에 데이터를 게시하려면 리소스의 경로를 제공합니다. 데이터는 리소스의 경로를 게시합니다. 예: /content/restEndPoint. 이러한 post 요청의 경우 제출 요청의 인증 정보가 사용됩니다.

외부 서버에 데이터를 게시하려면 URL을 제공합니다. URL의 형식은 https://host:port/path_to_rest_end_point입니다. POST 요청을 익명으로 처리하도록 경로를 구성해야 합니다.

![감사 인사 페이지 매개 변수로 전달된 필드 값에 대한 매핑](assets/post-enabled-actionconfig.png)

위의 예에서는 사용자가 `textbox` 는 매개 변수를 사용하여 캡처됩니다. `param1`. 를 사용하여 캡처한 데이터를 게시하기 위한 구문 `param1` is:

`String data=request.getParameter("param1");`

마찬가지로 XML 데이터 및 첨부 파일을 게시하는 데 사용하는 매개변수는 다음과 같습니다 `dataXml` 및 `attachments`.

예를 들어, 스크립트에서 이 두 매개 변수를 사용하여 데이터를 나머지 종료 지점으로 구문 분석합니다. 다음 구문을 사용하여 데이터를 저장하고 구문 분석합니다.

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

이 예제에서는 `data` 는 XML 데이터를 저장하고 `att` 첨부 파일 데이터를 저장합니다.

## 이메일 보내기 {#send-email}

다음 **이메일 보내기** 제출 작업은 양식을 성공적으로 제출할 때 하나 이상의 수신자에게 이메일을 보냅니다. 생성된 이메일에는 양식 데이터가 사전 정의된 형식으로 포함될 수 있습니다.

>[!NOTE]
전자 메일에 양식 데이터를 포함할 모든 양식 필드에는 다른 패널에 배치되더라도 다른 요소 이름이 있어야 합니다.

## 이메일을 통해 PDF 보내기 {#send-pdf-via-email}

다음 **이메일을 통해 PDF 보내기** 제출 작업은 양식 데이터가 포함된 PDF이 있는 이메일을 하나 이상의 수신자에게 전송하여 양식을 성공적으로 제출합니다.

>[!NOTE]
이 제출 작업은 레코드 문서 템플릿이 있는 XFA 기반 적응형 양식 및 XSD 기반 적응형 양식에 사용할 수 있습니다.

## Forms Workflow 호출 {#invoke-a-forms-workflow}

다음 **Forms Workflow에 제출** 제출 옵션은 데이터 xml 및 파일 첨부 파일(있는 경우)을 JEE 프로세스의 기존 Adobe LiveCycle 또는 AEM Forms에 전송합니다.

제출 대상 Forms Workflow 제출 작업을 구성하는 방법에 대한 자세한 내용은 [양식 워크플로우를 사용하여 양식 데이터 제출 및 처리](../../forms/using/submit-form-data-livecycle-process.md).

## 양식 데이터 모델을 사용하여 제출 {#submit-using-form-data-model}

다음 **양식 데이터 모델을 사용하여 제출** 제출 작업은 양식 데이터 모델의 지정된 데이터 모델 개체에 대해 제출된 적응형 양식 데이터를 해당 데이터 소스에 기록합니다. 제출 작업을 구성할 때 제출된 데이터를 해당 데이터 소스에 다시 쓸 데이터 모델 개체를 선택할 수 있습니다.

또한 양식 데이터 모델과 DoR(레코드 문서)을 사용하여 양식 첨부 파일을 데이터 소스에 제출할 수 있습니다.

양식 데이터 모델에 대한 자세한 내용은 [AEM Forms 데이터 통합](../../forms/using/data-integration.md).

## Forms 포털 제출 작업 {#forms-portal-submit-action}

다음 **Forms 포털 제출 작업** 옵션을 사용하면 AEM Forms 포털을 통해 양식 데이터를 사용할 수 있습니다.

Forms 포털 및 제출 작업에 대한 자세한 내용은 [초안 및 제출 구성 요소](../../forms/using/draft-submission-component.md).

## AEM 워크플로우 호출 {#invoke-an-aem-workflow}

다음 **[!UICONTROL AEM 워크플로우 호출]** 제출 작업은 적응형 양식을 [AEM 워크플로우](/help/sites-developing/workflows-models.md). 양식이 제출되면 연결된 워크플로우가 작성자 인스턴스에서 자동으로 시작됩니다. 데이터 파일, 첨부 파일 및 기록 문서를 워크플로우의 페이로드 또는 변수에 대한 상대적 폴더 또는 위치에 저장할 수 있습니다. 워크플로우가 외부 데이터 저장소에 대해 표시되면 페이로드 옵션이 아닌 변수 옵션을 사용할 수 있습니다. 워크플로우 모델에 사용할 수 있는 변수 목록에서 선택할 수 있습니다. 워크플로우가 워크플로우 생성 시점이 아니라 이후 단계에서 외부 데이터 스토리지에 대해 표시된다면 필요한 변수 구성이 있는지 확인합니다.

를 사용하기 전에 **AEM 워크플로우 호출** 작업 제출, [Experience Manager DS 설정 구성](../../forms/using/configuring-the-processing-server-url-.md). AEM 워크플로우 만들기에 대한 자세한 내용은 [OSGi의 양식 중심의 워크플로우](../../forms/using/aem-forms-workflow.md).

제출 작업은 워크플로우의 페이로드 위치에 다음 사항을 지정합니다. 하지만 워크플로우 모델이 외부 데이터 저장소에 대해 표시된 경우 페이로드 옵션이 아닌 변수 옵션만 표시됩니다.

* **데이터 파일**: 여기에는 적응형 양식에 전송된 데이터가 포함되어 있습니다. 를 사용할 수 있습니다 **[!UICONTROL 데이터 파일 경로]** 옵션을 사용하여 페이로드를 기준으로 파일 이름과 파일 경로를 지정합니다. 예: `/addresschange/data.xml` 경로: 라는 폴더를 만듭니다. `addresschange` 페이로드를 기준으로 하여 배치합니다. 만 지정할 수도 있습니다 `data.xml` 폴더 계층 구조를 만들지 않고 제출된 데이터만 보냅니다. 변수 옵션을 사용하고 워크플로우 모델에 사용할 수 있는 변수 목록에서 변수를 선택합니다.

>[!NOTE]
워크플로우 모델이 외부 데이터 저장소에 대해 표시되는지 여부에 관계없이 변수를 사용할 수 있습니다.

* **첨부 파일**: 를 사용할 수 있습니다 **[!UICONTROL 첨부 경로]** 적응형 양식에 업로드된 첨부 파일을 저장할 폴더 이름을 지정하는 옵션. 페이로드를 기준으로 폴더가 만들어집니다. 워크플로우가 외부 데이터 저장소에 대해 표시된 경우 변수 옵션을 사용하고 워크플로우 모델에 사용할 수 있는 변수 목록에서 변수를 선택합니다.

* **기록 문서**: 여기에는 적응형 양식에 대해 생성된 레코드 문서가 포함되어 있습니다. 를 사용할 수 있습니다 **[!UICONTROL 레코드 경로 문서]** [레코드 문서] 파일의 이름과 페이로드를 기준으로 파일 경로를 지정하는 옵션입니다. 예: `/addresschange/DoR.pdf` 경로: 라는 폴더를 만듭니다. `addresschange` 를 페이로드에 대해 관련되고, `DoR.pdf` 을 페이로드에 대해 상대적으로 설정합니다. 만 지정할 수도 있습니다 `DoR.pdf` 폴더 계층을 만들지 않고 레코드 문서만 저장하려면 워크플로우가 외부 데이터 저장소에 대해 표시된 경우 변수 옵션을 사용하고 워크플로우 모델에 사용할 수 있는 변수 목록에서 변수를 선택합니다.

## 적응형 양식의 서버측 재유효성 검사 {#server-side-revalidation-in-adaptive-form}

일반적으로 온라인 데이터 캡처 시스템에서 개발자는 일부 JavaScript 유효성 검사를 클라이언트 측에 배치하여 몇 가지 비즈니스 규칙을 적용합니다. 그러나 최신 브라우저에서 최종 사용자는 이러한 유효성 검사를 건너뛰고 웹 브라우저 개발 도구 콘솔 등의 다양한 기술을 사용하여 수동으로 제출을 수행할 수 있습니다. 이러한 기법은 적응형 양식에 대해서도 유효합니다. Forms 개발자는 다양한 유효성 검사 논리를 만들 수 있지만, 기술적으로 최종 사용자는 이러한 유효성 검사 논리를 무시하고 잘못된 데이터를 서버에 제출할 수 있습니다. 잘못된 데이터는 양식 작성자가 적용한 비즈니스 규칙을 손상시킵니다.

서버측 유효성 검사 기능은 서버에서 적응형 양식을 디자인하는 동안 적응형 양식 작성자가 제공한 유효성 검사를 실행하는 기능도 제공합니다. 양식 유효성 검사 측면에서 나타내는 데이터 제출 및 비즈니스 규칙 위반의 발생 가능성을 방지합니다.

### 서버에서 유효성을 검사하려면 어떻게 해야 합니까? {#what-to-validate-on-server-br}

서버에서 다시 실행되는 적응형 양식의 모든 기본(OOTB) 필드 유효성 검사는 다음과 같습니다.

* 필수
* 유효성 검사 그림 절
* 유효성 검사 표현식

### 서버측 유효성 검사 활성화 {#enabling-server-side-validation-br}

를 사용하십시오 **서버에서 유효성 검사** 사이드바의 적응형 양식 컨테이너 아래에 있는 현재 양식에 대한 서버측 유효성 검사를 활성화하거나 비활성화합니다.

![서버측 유효성 검사 활성화](assets/revalidate-on-server.png)

서버측 유효성 검사 활성화

최종 사용자가 이러한 유효성 검사를 무시하고 양식을 제출하면 서버에서 다시 유효성 검사를 수행합니다. 서버 끝에서 유효성 검사가 실패하면 제출 트랜잭션이 중지됩니다. 최종 사용자에게 원본 양식이 다시 표시됩니다. 캡처된 데이터와 제출된 데이터가 오류로 사용자에게 표시됩니다.

>[!NOTE]
서버측 유효성 검사는 양식 모델의 유효성을 검사합니다. 유효성 검사를 위해 별도의 클라이언트 라이브러리를 만들고 동일한 클라이언트 라이브러리에서 HTML 스타일 및 DOM 조작과 같은 다른 항목과 혼합하지 않는 것이 좋습니다.

### 유효성 검사 표현식에서 사용자 지정 함수 지원 {#supporting-custom-functions-in-validation-expressions-br}

경우에 따라 복잡한 유효성 검사 규칙이 있으면 정확한 유효성 검사 스크립트는 사용자 지정 함수에 상주하고 작성자는 필드 유효성 검사 표현식에서 이러한 사용자 지정 함수를 호출합니다. 서버측 유효성 검사를 수행하는 동안 이 사용자 지정 함수 라이브러리를 알고 사용할 수 있도록 하기 위해 양식 작성자는 아래에 AEM 클라이언트 라이브러리의 이름을 구성할 수 있습니다. **기본** 아래에 표시된 것처럼 적응형 양식 컨테이너 속성의 탭입니다.

![유효성 검사 표현식에서 사용자 지정 함수 지원](assets/clientlib-cat.png)

유효성 검사 표현식에서 사용자 지정 함수 지원

작성자는 적응형 양식별로 사용자 지정 JavaScript 라이브러리를 구성할 수 있습니다. 라이브러리에서는 jquery 및 underscore.js 타사 라이브러리에 대한 종속성이 있는 재사용 가능한 함수만 유지합니다.

## 제출 작업 시 오류 처리 {#error-handling-on-submit-action}

Experience Manager 보안 및 강화 지침의 일부로, 404.jsp 및 500.jsp와 같은 사용자 지정 오류 페이지를 구성합니다. 이러한 핸들러는 양식 제출 시 404 또는 500 오류가 나타날 때 호출됩니다. 이러한 오류 코드가 게시 노드에서 트리거될 때도 핸들러가 호출됩니다.

자세한 내용은 [오류 핸들러로 표시된 페이지 사용자 지정](/help/sites-developing/customizing-errorhandler-pages.md).
