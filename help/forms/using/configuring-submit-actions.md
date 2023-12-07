---
title: 제출 액션 구성
description: Forms을 사용하면 제출 액션을 구성하여 제출 후 적응형 양식이 처리되는 방식을 정의할 수 있습니다. 기본 제공 제출 액션을 사용하거나 직접 작성할 수 있습니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 51%

---

# 제출 액션 구성 {#configuring-the-submit-action}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html) |
| AEM 6.5 | 이 문서 |


## 제출 액션 소개 {#introduction-to-submit-actions}

제출 액션은 사용자가 적응형 양식에서 제출 단추를 클릭하면 트리거됩니다. 적응형 양식에서 제출 액션을 구성할 수 있습니다. 적응형 양식은 몇 가지 즉시 제출 액션을 제공합니다. 기본 제출 액션을 복사하고 확장하여 고유한 제출 액션을 만들 수 있습니다. 그러나 요구 사항에 따라 제출 액션을 작성하여 등록하면 제출된 양식의 데이터를 처리할 수 있습니다. 제출 액션은 [동기식 또는 비동기식 제출](../../forms/using/asynchronous-submissions-adaptive-forms.md).

에서 제출 액션을 구성할 수 있습니다. **제출** 섹션에 있는 섹션을 참조하십시오.

![제출 액션 구성](assets/thank-you-setting.png)

제출 액션 구성

적응형 양식에서 사용할 수 있는 기본 제출 작업은 다음과 같습니다.

* REST 엔드포인트에 제출
* 이메일 보내기
* 이메일을 통해 PDF 보내기
* Forms Workflow 호출
* 양식 데이터 모델을 사용하여 제출
* Forms 포털 제출 액션
* AEM 워크플로우 호출
* Power Automate에 제출

>[!NOTE]
>
>이메일 제출 액션을 통해 PDF 보내기 작업은 XFA 템플릿을 양식 모델로 사용하는 적응형 양식에만 적용할 수 있습니다.

>[!NOTE]
>
>다음을 확인합니다. [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM 폴더
>존재함. 첨부 파일을 임시로 저장하려면 디렉토리가 필요합니다. 디렉토리가 없으면 생성합니다.

>[!CAUTION]
>
>다음을 수행하는 경우 [미리 채우기](../../forms/using/prepopulate-adaptive-form-fields.md) 데이터에 포함되지 않은 스키마(XML 스키마, JSON 스키마, 양식 템플릿 또는 양식 데이터 모델)에 대한 XML 또는 JSON 데이터 컴플레인이 있는 양식 템플릿, 양식 데이터 모델 또는 스키마 기반 적응형 양식 &lt;afdata>, &lt;afbounddata>, 및 &lt;/afunbounddata> 태그 뒤에 묶이지 않은 필드의 데이터(묶이지 않은 필드는 없는 적응형 양식 필드임) [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) 적응형 양식의 속성)이 손실됩니다.

적응형 양식에 대한 사용자 지정 제출 액션을 작성하여 사용 사례를 충족할 수 있습니다. 자세한 내용은 [적응형 양식에 대한 사용자 정의 제출 액션 작성](../../forms/using/custom-submit-action-form.md).

## REST 엔드포인트에 제출 {#submit-to-rest-endpoint}

다음 **REST 끝점에 제출** 제출 옵션은 양식에 입력된 데이터를 HTTP GET 요청의 일부로 구성된 확인 페이지에 전달합니다. 요청할 필드 이름을 추가할 수 있습니다. 요청의 형식은 다음과 같습니다.

`{fieldName}={request parameter name}`

아래 이미지에 표시된 대로, `param1` 및 `param2` 에서 복사된 값을 사용하여 매개 변수로 전달됩니다. **텍스트 상자** 및 **숫자 상자** 다음 작업을 위한 필드입니다.

또한 **POST 요청을 활성화**&#x200B;하고 요청을 게시하는 URL을 제공할 수 있습니다. 양식을 호스팅하는 Experience Manager 서버에 데이터를 제출하려면 Experience Manager 서버의 루트 경로에 해당하는 상대 경로를 사용합니다. 예: /content/forms/af/SampleForm.html. 데이터를 다른 서버에 제출하려면 절대 경로를 사용합니다.

![REST 엔드포인트 제출 액션 구성](assets/action-config.png)

Rest 끝점 제출 작업 구성

>[!NOTE]
>
REST URL에서 필드를 매개변수로 전달하려면 필드가 다른 패널에 배치되는 경우에도 모든 필드의 요소 이름이 서로 달라야 합니다.

### 제출된 데이터를 리소스 또는 외부 나머지 끝점에 게시  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

**REST 엔드포인트에 제출** 액션을 사용하여 제출된 데이터를 REST URL에 게시합니다. URL은 내부 서버(양식이 렌더링되는 서버) 또는 외부 서버일 수 있습니다.

데이터를 내부 서버에 게시하려면 리소스 경로를 제공합니다. 데이터는 리소스 경로에 게시됩니다. 예: /content/restEndPoint. 해당 게시 요청이 있는 경우 제출 요청에 대한 인증 정보가 사용됩니다.

데이터를 외부 서버에 게시하려면 URL을 제공합니다. URL의 형식은 https://host:port/path_to_rest_end_point입니다. POST 요청을 익명으로 처리하는 경로를 구성해야 합니다.

![감사 페이지 매개변수로 전달된 필드 값 매핑](assets/post-enabled-actionconfig.png)

위 예에서 사용자는 매개변수 `param1`을 사용하여 캡처한 정보를 `textbox`에 입력했습니다. `param1`을 사용하여 캡처한 데이터를 게시하는 구문은 다음과 같습니다.

`String data=request.getParameter("param1");`

마찬가지로 XML 데이터와 첨부 파일 게시에 사용되는 매개변수는 `dataXml` 및 `attachments`입니다.

예를 들어 스크립트의 이 두 매개변수를 사용하여 데이터를 REST 엔드포인트로 구문 분석합니다. 다음 구문을 사용하여 데이터를 저장하고 구문 분석합니다.

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

이 예에서 `data`는 XML 데이터를 저장하고 `att`는 첨부 파일 데이터를 저장합니다.

## 이메일 보내기 {#send-email}

다음 **이메일 보내기** 제출 액션은 양식 제출 시 한 명 이상의 수신자에게 이메일을 전송합니다. 생성된 이메일에는 사전 정의된 형식의 양식 데이터가 포함될 수 있습니다.

>[!NOTE]
>
이메일에 양식 데이터를 포함하기 위해서는 모든 양식 필드에 서로 다른 패널에 배치된 경우에도 서로 다른 요소 이름이 있어야 합니다.

## 이메일을 통해 PDF 보내기 {#send-pdf-via-email}

다음 **이메일을 통해 PDF 보내기** 제출 액션은 양식 데이터가 포함된 PDF이 포함된 이메일을 양식을 성공적으로 제출하면 한 명 이상의 수신자에게 보냅니다.

>[!NOTE]
>
이 제출 액션은 기록 문서 템플릿이 있는 XFA 기반 적응형 양식 및 XSD 기반 적응형 양식에 사용할 수 있습니다.

## Forms Workflow 호출 {#invoke-a-forms-workflow}

다음 **Forms Workflow에 제출** 제출 옵션은 기존 Adobe LiveCycle 또는 JEE의 AEM Forms 프로세스에 데이터 xml 및 첨부 파일(있는 경우)을 전송합니다.

Forms Workflow 제출 액션을 구성하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [양식 워크플로우를 사용하여 양식 데이터 제출 및 처리](../../forms/using/submit-form-data-livecycle-process.md).

## 양식 데이터 모델을 사용하여 제출 {#submit-using-form-data-model}

다음 **양식 데이터 모델을 사용하여 제출** 제출 액션은 양식 데이터 모델의 지정된 데이터 모델 개체에 대해 제출된 적응형 양식 데이터를 해당 데이터 소스에 기록합니다. 제출 액션을 구성할 때 제출된 데이터를 해당 데이터 소스에 다시 쓸 데이터 모델 개체를 선택할 수 있습니다.

또한 양식 데이터 모델 및 기록 문서(DoR)를 사용하여 데이터 소스에 양식 첨부 파일을 제출할 수 있습니다.

양식 데이터 모델에 대한 자세한 내용은 [AEM Forms 데이터 통합](../../forms/using/data-integration.md).

## Forms 포털 제출 액션 {#forms-portal-submit-action}

다음 **Forms 포털 제출 액션** 옵션을 사용하면 AEM Forms 포털에서 양식 데이터를 사용할 수 있습니다.

Forms 포털 및 제출 작업에 대한 자세한 내용은 을 참조하십시오. [초안 및 제출 구성 요소](../../forms/using/draft-submission-component.md).

## AEM Workflow 호출 {#invoke-an-aem-workflow}

**[!UICONTROL AEM Workflow 호출]** 제출 액션은 적응형 양식을 [AEM Workflow](/help/sites-developing/workflows-models.md)와 연결합니다. 양식이 제출되면 연결된 워크플로가 작성자 인스턴스에서 자동으로 시작됩니다. 데이터 파일, 첨부 파일 및 기록 문서를 상대 폴더 또는 워크플로의 페이로드 아래 또는 변수에 저장할 수 있습니다. 워크플로가 외부 데이터 스토리지에 대해 표시된 경우 페이로드 옵션이 아닌 변수 옵션을 사용할 수 있습니다. 워크플로 모델에 제공되는 변수 목록에서 선택할 수 있습니다. 워크플로 생성 시점이 아닌 이후 단계에서 워크플로가 외부 데이터 스토리지로 표시되면 필수 변수 구성이 마련되었는지 확인합니다.

를 사용하기 전에 **AEM 워크플로우 호출** 제출 액션, [Experience Manager DS 설정 구성](../../forms/using/configuring-the-processing-server-url-.md). AEM 워크플로우 만들기에 대한 내용은 [OSGi의 양식 중심 워크플로](../../forms/using/aem-forms-workflow.md).

제출 액션은 워크플로우의 페이로드 위치에 다음을 배치합니다. 그러나 워크플로 모델이 외부 데이터 저장용으로 표시된 경우에는 변수 옵션만 표시되고 페이로드 옵션은 표시되지 않습니다.

* **데이터 파일**: 적응형 양식에 제출된 데이터가 포함됩니다. **[!UICONTROL 데이터 파일 경로]** 옵션을 사용하여 페이로드를 기준으로 파일 이름과 파일 경로를 지정할 수 있습니다. 예를 들어 `/addresschange/data.xml` 경로는 `addresschange`라는 폴더를 만들고 페이로드를 기준으로 배치합니다. 또한 `data.xml`만 지정하여 폴더 계층 구조를 만들지 않고도 제출된 데이터만 전송할 수 있습니다. 변수 옵션을 사용하고 워크플로우 모델에 사용할 수 있는 변수 목록에서 변수를 선택합니다.

>[!NOTE]
>
워크플로 모델이 외부 데이터 스토리지에 대해 표시되는지 여부에 관계없이 변수를 사용할 수 있습니다.

* **첨부 파일**: **[!UICONTROL 첨부 파일 경로]** 옵션을 사용하여 폴더 이름을 지정하면 적응형 양식에 업로드된 첨부 파일을 저장할 수 있습니다. 페이로드를 기준으로 폴더를 생성합니다. 워크플로가 외부 데이터 스토리지로 표시되면 변수 옵션을 사용하고 워크플로 모델에 제공되는 변수 목록에서 변수를 선택합니다.

* **기록 문서**: 적응형 양식에 생성된 기록 문서가 포함됩니다. **[!UICONTROL 기록 문서 경로]** 옵션을 사용하여 페이로드를 기준으로 기록 문서 파일 이름과 파일 경로를 지정할 수 있습니다. 예를 들어 `/addresschange/DoR.pdf` 경로는 `addresschange`라는 폴더를 만들고 페이로드를 기준으로 `DoR.pdf`를 배치합니다. 또한 `DoR.pdf`만 지정하여 폴더 계층 구조를 만들지 않고도 기록 문서만 저장할 수 있습니다. 워크플로가 외부 데이터 스토리지로 표시되면 변수 옵션을 사용하고 워크플로 모델에 제공되는 변수 목록에서 변수를 선택합니다.

## Power Automate에 제출 {#microsoft-power-automate}

제출 시 Microsoft® Power Automate Cloud Flow를 실행하도록 적응형 양식을 구성할 수 있습니다. 구성된 적응형 양식은 캡처된 데이터, 첨부 파일 및 기록 문서를 처리를 위해 Power Automate Cloud Flow로 전송합니다. 이렇게 하면 Microsoft® Power Automate의 강력한 기능을 활용하면서 사용자 정의 데이터 캡처 환경을 빌드하여 캡처된 데이터를 중심으로 비즈니스 논리를 빌드하고 고객 워크플로를 자동화할 수 있습니다. 다음은 적응형 양식을 Microsoft® Power Automate와 통합한 후 수행할 수 있는 작업에 대한 몇 가지 예입니다.

* Power Automate 비즈니스 프로세스에서 적응형 양식 데이터 사용
* Power Automate를 사용하여 캡처된 데이터를 500개 이상의 데이터 소스 또는 공개적으로 사용 가능한 API로 전송
* 캡처된 데이터에 대해 복잡한 계산 수행
* 미리 정의된 일정에 따라 적응형 양식 데이터를 스토리지 시스템에 저장

적응형 양식 편집기는 **Microsoft® Power Automate 흐름 호출** 제출 작업을 제공하여 적응형 양식 데이터, 첨부 파일 및 기록 문서를 Power Automate Cloud Flow로 전송합니다. 제출 액션을 사용하여 캡처된 데이터를 Microsoft® Power Automate로 보내려면 [AEM Forms 인스턴스와 Microsoft® Power Automate 연결](/help/forms/using/forms-microsoft-power-automate-integration.md)

성공적으로 구성한 후 [Microsoft® Power Automate 흐름 호출](/help/forms/using/forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) 제출 액션을 사용하여 데이터를 Power Automate 흐름으로 전송합니다.

## 적응형 양식에서 서버측 유효성 재검사 {#server-side-revalidation-in-adaptive-form}

일반적으로 온라인 데이터 캡처 시스템에서 개발자는 몇 가지 비즈니스 규칙을 적용하기 위해 클라이언트측에 대해 JavaScript 유효성 검사를 일부 실시합니다. 단, 최신 브라우저에서 최종 사용자는 이러한 유효성 검사를 무시하고 웹 브라우저 DevTools 콘솔과 같은 다양한 기술을 사용하여 수동으로 제출 액션을 수행할 수 있습니다. 이러한 기법은 적응형 양식에도 유효합니다. 양식 개발자는 다양한 유효성 검사 논리를 만들 수 있지만 기술적 측면에서 최종 사용자는 이러한 유효성 검사 논리를 무시하고 잘못된 데이터를 서버에 제출할 수 있습니다. 잘못된 데이터로 인해 양식 작성자가 적용한 비즈니스 규칙이 깨질 수 있습니다.

서버측 유효성 재검사 기능은 서버에서 적응형 양식을 디자인하는 동안 적응형 양식 작성자가 제공한 유효성 검사를 실행할 수도 있습니다. 양식 유효성 검사에 표시되는 데이터 제출 및 비즈니스 규칙 위반 사항에 발생할 수 있는 잠재적 손상을 방지할 수 있습니다.

### 서버에서의 유효성 검사 대상은 무엇입니까? {#what-to-validate-on-server-br}

서버에서 다시 실행되는 적응형 양식의 모든 즉시 사용 가능한(OOTB) 필드 유효성 검사는 다음과 같습니다.

* 필수
* 유효성 검사 픽처 구절
* 유효성 검사 표현식

### 서버측 유효성 검사 활성화 {#enabling-server-side-validation-br}

사이드바의 적응형 양식 컨테이너 아래에 있는 **서버측 유효성 재검사**&#x200B;를 사용하여 현재 양식에 대해 서버측 유효성 검사를 활성화하거나 비활성화합니다.

![서버측 유효성 검사 활성화](assets/revalidate-on-server.png)

서버측 유효성 검사 활성화

최종 사용자가 이러한 유효성 검사를 무시하고 양식을 제출하면 서버에서 다시 유효성 검사를 수행합니다. 유효성 검사가 서버 끝에서 실패하면 제출 트랜잭션이 중지됩니다. 원래 양식이 최종 사용자에게 다시 표시됩니다. 캡처된 데이터와 제출된 데이터는 사용자에게 오류로 표시됩니다.

>[!NOTE]
>
서버측 유효성 검사는 양식 모델의 유효성을 검사합니다. 유효성 검사를 위해 별도의 클라이언트 라이브러리를 만들고 동일한 클라이언트 라이브러리에서 HTML 스타일링 및 DOM 조작과 같은 다른 항목과 혼합하지 않는 것이 좋습니다.

### 유효성 검사 표현식에서 사용자 정의 함수 지원 {#supporting-custom-functions-in-validation-expressions-br}

복잡한 유효성 검사 규칙이 있는 경우 정확한 유효성 검사 스크립트는 사용자 지정 함수에 상주하며 작성자는 필드 유효성 검사 표현식에서 이러한 사용자 지정 함수를 호출합니다. 서버측 유효성 검사를 수행하면서 이 사용자 정의 함수 라이브러리를 이해하고 사용할 수 있도록 양식 작성자는 아래와 같이 적응형 양식 컨테이너 속성의 **기본** 탭 아래에서 AEM 클라이언트 라이브러리 이름을 구성할 수 있습니다.

![유효성 검사 표현식에서 사용자 정의 함수 지원](assets/clientlib-cat.png)

유효성 검사 표현식에서 사용자 정의 함수 지원

작성자는 적응형 양식에 따라 customJavaScript 라이브러리를 구성할 수 있습니다. jquery 및 underscore.js 서드파티 라이브러리에 종속된 재사용 가능한 함수만 라이브러리에 유지됩니다.

## 제출 액션 시 오류 처리 {#error-handling-on-submit-action}

Experience Manager 보안 및 강화 지침의 일부로 404.jsp 및 500.jsp와 같은 사용자 지정 오류 페이지를 구성합니다. 이러한 처리기는 양식 404 또는 500 오류를 제출할 때 호출됩니다. 이러한 오류 코드가 Publish 노드에서 트리거되면 핸들러도 호출됩니다.

자세한 내용은 [오류 핸들러로 표시된 페이지 사용자 지정](/help/sites-developing/customizing-errorhandler-pages.md).
