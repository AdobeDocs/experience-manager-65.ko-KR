---
title: 양식을 HTML로 렌더링
seo-title: 양식을 HTML로 렌더링
description: 'null'
seo-description: 'null'
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '4108'
ht-degree: 0%

---


# 양식을 HTML로 렌더링 {#rendering-forms-as-html}

양식 서비스는 웹 브라우저의 HTTP 요청에 응답하여 양식을 HTML로 렌더링합니다. 양식을 HTML로 렌더링하면 클라이언트 웹 브라우저가 있는 컴퓨터에 Adobe Reader, Acrobat 또는 Flash Player가 필요하지 않습니다(양식 안내서(더 이상 사용되지 않음).

양식을 HTML로 렌더링하려면 양식 디자인을 XDP 파일로 저장해야 합니다. PDF 파일로 저장된 양식 디자인은 HTML로 렌더링할 수 없습니다. Designer에서 HTML로 렌더링되는 양식 디자인을 개발할 때는 다음 조건을 고려하십시오.

* 개체의 테두리 속성을 사용하여 양식에 선, 상자 또는 그리드를 그리지 마십시오. 일부 브라우저는 미리 보기에 나타나는 것과 동일한 테두리로 정렬되지 않을 수 있습니다. 개체는 레이어로 표시되거나 다른 개체를 원하는 위치에서 밀어낼 수 있습니다.
* 선, 사각형 및 원을 사용하여 배경을 정의할 수 있습니다.
* 텍스트를 수용하는 데 필요한 것보다 약간 큰 텍스트를 그릴 수 있습니다. 일부 웹 브라우저에서는 텍스트를 가독하게 표시하지 않습니다.

>[!NOTE]
>
>개체 및 방법을 사용하여 TIFF 이미지가 포함된 양식을 렌더링할 때 `FormServiceClient` TIFF `(Deprecated) renderHTMLForm` `renderHTMLForm2` 이미지는 Internet Explorer 또는 Mozilla Firefox 브라우저에 표시되는 렌더링된 HTML 양식에서는 볼 수 없습니다. 이러한 브라우저는 TIFF 이미지에 대한 기본 지원을 제공하지 않습니다.

## HTML 페이지 {#html-pages}

양식 디자인이 HTML 양식으로 렌더링되면 각 두 번째 하위 폼이 HTML 페이지(패널)로 렌더링됩니다. Designer에서 하위 폼의 계층을 볼 수 있습니다. 루트 하위 폼에 속하는 하위 폼(루트 하위 폼의 기본 이름은 form1)은 패널 하위 폼입니다. 다음 예는 양식 디자인의 하위 양식을 보여줍니다.

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

양식 디자인이 HTML 양식으로 렌더링될 때 패널은 특정 페이지 크기로 제한되지 않습니다. 동적 하위 폼이 있는 경우 패널 하위 폼 내에 중첩되어야 합니다. 동적 하위 양식은 HTML 페이지로 무제한으로 확장할 수 있습니다.

양식을 HTML 양식으로 렌더링할 때 페이지 크기(PDF로 렌더링된 양식을 페이지 매김하는 데 필요)는 아무런 의미가 없습니다. 순서별 레이아웃이 있는 양식은 HTML 페이지로 확장될 수 있으므로 마스터 페이지의 바닥글을 사용하지 않는 것이 중요합니다. 마스터 페이지의 컨텐츠 영역 아래에 있는 바닥글은 페이지 경계를 넘는 HTML 컨텐츠를 덮어쓸 수 있습니다.

및 메서드를 사용하여 패널에서 패널로 명시적으로 이동해야 합니다 `xfa.host.pageUp` `xfa.host.pageDown` . 양식을 양식 서비스로 보내고 양식 서비스가 양식을 클라이언트 장치(일반적으로 웹 브라우저)로 다시 렌더링하도록 하여 페이지를 변경합니다.

>[!NOTE]
>
>양식을 양식 서비스로 전송한 다음 양식 서비스를 통해 양식을 다시 클라이언트 장치로 렌더링하는 과정을 서버로의 양방향 데이터 전송이라고 합니다.

>[!NOTE]
>
>HTML 양식의 HTML 디지털 서명 단추 모양을 사용자 지정하려면 fscdigsig.css 파일(adobe-forms-ds.ear > adobe-forms-ds.war 파일 내)에서 다음 속성을 변경해야 합니다.

**.fsc-ds-sb**: 이 스타일 시트는 빈 기호 필드의 경우에 적용됩니다.

**.fsc-ds-ssv**: 이 스타일 시트는 유효한 기호 필드의 경우에 적용됩니다.

**.fsc-ds-ssc**: 이 스타일 시트는 유효한 서명 필드의 경우 적용되지만 데이터가 변경되었습니다.

**.fsc-ds-ssi**: 이 스타일 시트는 잘못된 기호 필드의 경우에 적용됩니다.

**.fsc-ds-popup-bg**: 이 스타일 시트 속성은 사용되지 않습니다.

**.fsc-ds-popup-btn**: 이 스타일 시트 속성은 사용되지 않습니다.

## 스크립트 실행 {#running-scripts}

양식 작성자는 스크립트가 서버에서 실행되는지 또는 클라이언트에서 실행되는지를 지정합니다. Forms 서비스는 `runAt` 속성을 사용하여 클라이언트와 서버 간에 배포할 수 있는 양식 인텔리전스를 실행하기 위한 분산 이벤트 처리 환경을 만듭니다. 이 특성 또는 양식 디자인 내에서 스크립트 만들기에 대한 자세한 내용은 [Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63)

양식 서비스는 양식을 렌더링하는 동안 스크립트를 실행할 수 있습니다. 따라서 클라이언트에서 사용할 수 없는 데이터베이스 또는 웹 서비스에 연결하여 데이터를 미리 채울 수 있습니다. 서버에서 실행되도록 단추의 `Click` 이벤트를 설정하여 클라이언트가 서버에 대한 이동 데이터를 라운드할 수도 있습니다. 이를 통해 클라이언트는 사용자가 양식과 상호 작용하는 동안 엔터프라이즈 데이터베이스와 같은 서버 리소스를 필요로 할 수 있는 스크립트를 실행할 수 있습니다. HTML 양식의 경우 양식 계산 스크립트는 서버에서만 실행할 수 있습니다. 따라서 `server` 또는 에서 실행되도록 이러한 스크립트를 표시해야 합니다 `both`.

호출과 메서드를 통해 페이지(패널) 간에 이동하는 양식 `xfa.host.pageUp` 을 디자인할 수 `xfa.host.pageDown` 있습니다. 이 스크립트는 단추의 `Click` 이벤트에 삽입되며 `runAt` 속성은 로 설정됩니다 `Both`. 선택한 이유 `Both` 는 PDF로 렌더링되는 양식의 경우 Adobe Reader 또는 Acrobat에서 서버로 이동하지 않고 페이지를 변경할 수 있고 HTML 양식에서 데이터를 서버에 전달하여 페이지를 변경할 수 있기 때문입니다. 즉, 양식이 양식 서비스로 전송되고 양식이 새 페이지가 표시된 상태에서 HTML로 다시 렌더링됩니다.

스크립트 변수 및 양식 필드에 항목과 같은 이름을 지정하지 않는 것이 좋습니다. Internet Explorer와 같은 일부 웹 브라우저는 스크립트 오류가 발생하는 양식 필드와 동일한 이름으로 변수를 초기화할 수 없습니다. 양식 필드 및 스크립트 변수를 다른 이름으로 지정하는 것이 좋습니다.

페이지 탐색 기능과 양식 스크립트가 모두 포함된 HTML 양식을 렌더링할 때(예를 들어, 스크립트가 양식이 렌더링될 때마다 데이터베이스에서 필드 데이터를 검색한다고 가정할 경우) 양식 스크립트가 form:readyevent 대신 form:calculate 이벤트에 있는지 확인합니다.

form:ready 이벤트에 있는 양식 스크립트는 양식의 초기 렌더링 중에 한 번만 실행되며 이후 페이지 검색에 대해서는 실행되지 않습니다. 반면에 form:calculate 이벤트는 양식이 렌더링되는 각 페이지 탐색에 대해 실행됩니다.

>[!NOTE]
여러 페이지로 된 양식에서 JavaScript에서 페이지로 변경한 내용은 다른 페이지로 이동하는 경우 유지되지 않습니다.

양식을 제출하기 전에 사용자 지정 스크립트를 호출할 수 있습니다. 이 기능은 사용 가능한 모든 브라우저에서 작동합니다. 하지만 사용자가 속성이 설정된 HTML 양식을 렌더링할 때만 사용할 `Output Type` 수 있습니다 `Form Body`. 그것이 있을 때는 작동하지 `Output Type` 않을 것이다 `Full HTML`. 이 기능을 구성하는 단계는 관리 도움말의 양식 구성을 참조하십시오.

먼저 함수 이름이 있는 양식을 제출하기 전에 호출되는 콜백 함수를 정의해야 합니다 `_user_onsubmit`. 함수에서 예외를 throw하지 않거나 예외를 throw할 경우 예외가 무시됩니다. html의 헤드 섹션에 JavaScript 함수를 배치하는 것이 좋습니다. 그러나 포함하는 스크립트 태그의 끝 전 어디에서든 선언할 수 있습니다 `xfasubset.js`.

양식 서버가 드롭다운 목록이 포함된 XDP를 렌더링할 때 드롭다운 목록을 만드는 것 외에도 두 개의 숨겨진 텍스트 필드도 만듭니다. 이러한 텍스트 필드는 드롭다운 목록의 데이터를 저장합니다. 하나는 옵션의 표시 이름을 저장하고 다른 하나는 옵션에 대한 값을 저장합니다. 따라서 사용자가 양식을 제출할 때마다 드롭다운 목록의 전체 데이터가 제출됩니다. 항상 그렇게 많은 데이터를 제출하지 않으려는 경우 사용자 지정 스크립트를 작성하여 이를 비활성화할 수 있습니다. 예: 드롭다운 목록의 이름은 하위 폼 머리글 `drpOrderedByStateProv` 에 둘러싸여 있습니다. HTML 입력 요소의 이름이 됩니다 `header[0].drpOrderedByStateProv[0]`. 드롭다운의 데이터를 저장 및 제출하는 숨김 필드의 이름에는 다음 이름이 있습니다. `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

데이터를 게시하지 않으려는 경우 다음과 같이 입력 요소를 비활성화할 수 있습니다. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFA 하위 세트 {#xfa-subsets}

HTML로 렌더링할 양식 디자인을 만들 때 JavaScript 언어의 스크립트에 대한 XFA 하위 세트로 스크립팅을 제한해야 합니다.

클라이언트에서 실행하거나 클라이언트와 서버에서 실행되는 스크립트는 XFA 하위 세트 내에 작성해야 합니다. 서버에서 실행되는 스크립트는 전체 XFA 스크립팅 모델을 사용하고 FormCalc를 사용할 수 있습니다. JavaScript 사용에 대한 자세한 내용은 [양식 디자이너를 참조하십시오](https://www.adobe.com/go/learn_aemforms_designer_63).

클라이언트에서 스크립트를 실행할 때 표시되는 현재 패널만 스크립트를 사용할 수 있습니다. 예를 들어 패널 B가 표시되면 패널 A에 있는 필드에 대해 스크립팅할 수 없습니다. 서버에서 스크립트를 실행할 때 모든 패널에 액세스할 수 있습니다.

클라이언트에서 실행되는 스크립트 내에서 SOM(스크립팅 개체 모델) 표현식을 사용할 때도 주의해야 합니다. 클라이언트에서 실행되는 스크립트에서 SOM 표현식의 간소화된 하위 집합만 지원됩니다.

## 이벤트 타이밍 {#event-timing}

XFA 하위 세트는 HTML 이벤트에 매핑되는 XFA 이벤트를 정의합니다. 이벤트를 계산하고 확인하는 타이밍에 대한 동작에는 약간의 차이가 있습니다. 웹 브라우저에서 필드를 종료하면 전체 계산 이벤트가 실행됩니다. 필드 값을 변경하면 계산 이벤트가 자동으로 실행되지 않습니다. 메서드를 호출하여 계산 이벤트를 강제 적용할 수 `xfa.form.execCalculate` 있습니다.

웹 브라우저에서 유효성 검사 이벤트는 필드를 종료하거나 양식을 제출할 때만 실행됩니다. 메서드를 사용하여 유효성 검사 이벤트를 강제 적용할 수 `xfa.form.execValidate` 있습니다.

웹 브라우저에 표시되는 양식(Adobe Reader 또는 Acrobat과 반대)은 필수 필드에 대한 XFA null 테스트(오류 또는 경고)를 따릅니다.

* null 테스트에 오류가 발생하고 값을 지정하지 않고 필드를 종료하면 메시지 상자가 표시되고 확인을 클릭한 후 필드에 다시 배치됩니다.
* null 테스트에 경고가 발생하고 값을 지정하지 않고 필드를 종료하는 경우 [확인] 또는 [취소]를 클릭하라는 메시지가 표시됩니다. 값을 지정하지 않고 계속 진행할 수 있는 옵션이나 값을 입력하여 필드로 돌아갈 수 있습니다.

null 테스트에 대한 자세한 내용은 [Forms 디자이너를 참조하십시오](https://www.adobe.com/go/learn_aemforms_designer_63).

## 양식 단추 {#form-buttons}

제출 단추를 클릭하면 양식 데이터가 양식 서비스로 전송되고 양식 처리의 끝을 나타냅니다. 이 `preSubmit` 이벤트는 클라이언트 또는 서버에서 실행되도록 설정할 수 있습니다. 클라이언트에서 실행되도록 구성된 경우 이 `preSubmit` 이벤트는 양식 제출 전에 실행됩니다. 그렇지 않으면 `preSubmit` 이벤트는 양식을 제출하는 동안 서버에서 실행됩니다. 이벤트에 대한 자세한 내용은 `preSubmit` 양식 디자이너 [](https://www.adobe.com/go/learn_aemforms_designer_63)를 참조하십시오.

단추에 연결된 클라이언트측 스크립트가 없으면 데이터가 서버로 전송되고 서버에서 계산이 수행되며 HTML 양식이 다시 생성됩니다. 단추에 클라이언트측 스크립트가 있으면 데이터는 서버로 전송되지 않고 클라이언트측 스크립트는 웹 브라우저에서 실행됩니다.

## HTML 4.0 웹 브라우저 {#html-4-0-web-browser}

HTML 4.0만 지원하는 웹 브라우저는 XFA 하위 집합 클라이언트측 스크립팅 모델을 지원할 수 없습니다. HTML 4.0과 MSDHTML 또는 CSS2HTML 모두에서 작동하는 양식 디자인을 만들 때 클라이언트에서 실행되도록 표시된 스크립트가 실제로 서버에서 실행됩니다. 예를 들어 사용자가 HTML 4.0 웹 브라우저에 표시되는 양식에 있는 단추를 클릭했다고 가정할 수 있습니다. 이 경우 양식 데이터는 클라이언트측 스크립트가 실행되는 서버로 전송됩니다.

HTML 4.0의 서버 및 MSDHTML 또는 CSS2HTML의 클라이언트에서 실행되는 계산 이벤트에 양식 논리를 배치하는 것이 좋습니다.

## 프레젠테이션 변경 내용 유지 {#maintaining-presentation-changes}

HTML 페이지(패널) 간을 이동할 때 데이터의 상태만 유지됩니다. 배경색 또는 필수 필드 설정과 같은 설정은 유지되지 않습니다(초기 설정과 다른 경우). 프레젠테이션 상태를 유지하려면 필드의 프레젠테이션 상태를 나타내는 필드(일반적으로 숨김)를 만들어야 합니다. 숨김 필드 값에 따라 프레젠테이션을 변경하는 필드 `Calculate` 이벤트에 스크립트를 추가하는 경우 HTML 페이지(패널) 간을 이동할 때 프레젠테이션 상태를 유지할 수 있습니다.

다음 스크립트는 값 `fillColor` 을 기반으로 필드의 상태를 유지합니다 `hiddenField`. 이 스크립트가 필드의 `Calculate` 이벤트에 있다고 가정합니다.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
정적 개체는 표 셀 내에 중첩될 때 렌더링된 HTML 양식에 표시되지 않습니다. 예를 들어 표 셀 내에 중첩된 원 및 직사각형은 렌더링 HTML 양식 내에 표시되지 않습니다. 하지만 이러한 동일한 정적 개체는 표 외부에 있을 때 제대로 표시됩니다.

## HTML 양식에 디지털 서명 {#digitally-signing-html-forms}

양식이 다음 HTML 변형 중 하나로 렌더링되는 경우 디지털 서명 필드가 포함된 HTML 양식에 서명할 수 없습니다.

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

문서에 디지털 서명을 하는 방법에 대한 자세한 내용은 문서 [디지털 서명 및 인증을 참조하십시오.](/help/forms/developing/digitally-signing-certifying-documents.md)

## 액세서빌러티 가이드라인을 준수하는 XHTML 양식 렌더링 {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

액세서빌러티 지침을 준수하는 전체 HTML 양식을 렌더링할 수 있습니다. 즉, 전체 HTML 태그가 아닌 본문 태그 내에 렌더링되는 HTML 양식과 비교하여 양식이 전체 HTML 태그 내에서 렌더링됩니다.

## 양식 데이터 유효성 확인 {#validating-form-data}

양식을 HTML 양식으로 렌더링할 때는 양식 필드에 대한 유효성 검사 규칙 사용을 제한하는 것이 좋습니다. 일부 유효성 검사 규칙은 HTML 양식에 지원되지 않을 수 있습니다. 예를 들어 MM-DD-YYYY의 유효성 검사 패턴이 HTML 양식으로 렌더링되는 양식 디자인에 있는 `Date/Time` 필드에 적용되면 날짜를 올바르게 입력해도 제대로 작동하지 않습니다. 그러나 이 유효성 검사 패턴은 PDF로 렌더링된 양식에 대해 제대로 작동합니다.

>[!NOTE]
양식 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

## 단계 요약 {#summary-of-steps}

HTML 양식을 렌더링하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. Forms 클라이언트 API 개체를 만듭니다.
1. HTML 런타임 옵션을 설정합니다.
1. HTML 양식을 렌더링합니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 씁니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

프로그래밍 방식으로 데이터를 PDF formClient API로 가져오기 전에 양식 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다.

**HTML 런타임 옵션 설정**

HTML 양식을 렌더링할 때 HTML 런타임 옵션을 설정합니다. 예를 들어 HTML 양식에 도구 모음을 추가하여 사용자가 클라이언트 컴퓨터에 있는 첨부 파일을 선택하거나 HTML 양식으로 렌더링된 첨부 파일을 검색할 수 있도록 할 수 있습니다. 기본적으로 HTML 도구 모음은 비활성화됩니다. HTML 양식에 도구 모음을 추가하려면 프로그래밍 방식으로 런타임 옵션을 설정해야 합니다. 기본적으로 HTML 도구 모음은 다음 단추로 구성됩니다.

* `Home`: 응용 프로그램의 웹 루트에 대한 링크를 제공합니다.
* `Upload`: 현재 양식에 첨부할 파일을 선택할 수 있는 사용자 인터페이스를 제공합니다.
* `Download`: 첨부된 파일을 표시하는 사용자 인터페이스를 제공합니다.

HTML 도구 모음이 HTML 양식에 표시되면 사용자는 양식 데이터와 함께 제출할 최대 10개의 파일을 선택할 수 있습니다. 파일이 제출되면 양식 서비스는 파일을 검색할 수 있습니다.

양식을 HTML로 렌더링할 때 사용자-에이전트 값을 지정할 수 있습니다. 사용자-에이전트 값은 브라우저 및 시스템 정보를 제공합니다. 선택적 값이며 빈 문자열 값을 전달할 수 있습니다. Java API 빠른 시작을 사용하여 HTML 양식 렌더링은 사용자 에이전트 값을 가져와서 이를 사용하여 양식을 HTML로 렌더링하는 방법을 보여줍니다.

양식 데이터가 게시된 HTTP URL은 Forms Service Client API를 사용하여 대상 URL을 설정하여 지정하거나 XDP 양식 디자인에 포함된 제출 단추에 지정할 수 있습니다. 대상 URL이 양식 디자인에 지정된 경우 Forms Service 클라이언트 API를 사용하여 값을 설정하지 마십시오.

>[!NOTE]
도구 모음에서 HTML 양식 렌더링은 선택 사항입니다.

>[!NOTE]
AHTML 양식을 렌더링하는 경우 양식에 도구 모음을 추가하지 않는 것이 좋습니다.

**HTML 양식 렌더링**

HTML 양식을 렌더링하려면 Designer에서 만들고 XDP 파일로 저장한 양식 디자인을 지정해야 합니다. HTML 변형 유형도 선택해야 합니다. 예를 들어 Internet Explorer 5.0 이상의 동적 HTML을 렌더링하는 HTML 변형 유형을 지정할 수 있습니다.

HTML 양식을 렌더링하려면 다른 양식 유형을 렌더링하는 데 필요한 URI 값과 같은 값도 필요합니다.

**양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기**

Forms 서비스가 HTML 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성할 때 HTML 양식이 사용자에게 표시됩니다.

**참고 항목**

[Java API를 사용하여 양식을 HTML로 렌더링](#render-a-form-as-html-using-the-java-api)

[웹 서비스 API를 사용하여 양식을 HTML로 렌더링](#render-a-form-as-html-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[사용자 지정 도구 모음을 사용하여 HTML 양식 렌더링](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[양식을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API를 사용하여 양식을 HTML로 렌더링 {#render-a-form-as-html-using-the-java-api}

양식 API(Java)를 사용하여 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `FormsServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. HTML 런타임 옵션 설정

   * 생성자를 사용하여 `HTMLRenderSpec` 개체를 만듭니다.
   * 도구 모음을 사용하여 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체의 `setHTMLToolbar` 메서드를 호출하고 열거형 값을 `HTMLToolbar` 전달합니다. 예를 들어 세로 HTML 도구 모음을 표시하려면 전달하십시오 `HTMLToolbar.Vertical`.
   * HTML 양식의 로케일 값을 설정하려면 `HTMLRenderSpec` 개체의 `setLocale` 메서드를 호출하고 로케일 값을 지정하는 문자열 값을 전달합니다. (선택적 설정입니다.)
   * 전체 HTML 태그 내에서 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체의 `setOutputType` 메서드를 호출하고 전달합니다 `OutputType.FullHTMLTags`. (선택적 설정입니다.)

   >[!NOTE]
   이 `StandAlone` 옵션이 선택되어 있고 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버 이외의 서버를 참조하는 경우 양식 `true` 이 HTML로 `ApplicationWebRoot` 렌더링되지 않습니다. 이 `ApplicationWebRoot` 값은 `URLSpec` 개체의 `FormsServiceClient` `(Deprecated) renderHTMLForm` 메서드에 전달된 개체를 사용하여 지정됩니다. 이 서버 `ApplicationWebRoot` 가 하나의 호스팅 AEM Forms에서 다른 서버일 경우 관리 콘솔에서 웹 루트 URI의 값을 양식의 웹 응용 프로그램 URI 값으로 설정해야 합니다. 관리 콘솔에 로그인하고 서비스 > 양식을 클릭한 다음 웹 루트 URI를 https://server-name:port/FormServer으로 설정하여 수행할 수 있습니다. 그런 다음 설정을 저장합니다.

1. HTML 양식 렌더링

   개체의 `FormsServiceClient` 메서드를 `(Deprecated) renderHTMLForm` 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값. Forms 응용 프로그램의 일부인 양식 디자인을 참조하는 경우 전체 경로를 지정해야 합니다(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`).
   * HTML `TransformTo` 기본 설정 형식을 지정하는 열거형 값. 예를 들어 Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 을 지정합니다 `TransformTo.MSDHTML`.
   * 양식과 병합할 데이터가 포함된 `com.adobe.idp.Document` 개체 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * HTML 런타임 옵션을 저장하는 `HTMLRenderSpec` 개체입니다.
   * 헤더 값을 지정하는 `HTTP_USER_AGENT` 문자열 값; 예를 들면 다음과 같습니다 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다.

   이 `(Deprecated) renderHTMLForm` 메서드는 클라이언트 웹 브라우저에 쓸 수 있는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * 개체 &#39;s 메서드 `com.adobe.idp.Document` 를 호출하여 개체를 `FormsResult` 만듭니다 `getOutputContent` .
   * 해당 메서드를 호출하여 개체의 `com.adobe.idp.Document` 콘텐츠 유형을 `getContentType` 가져옵니다.
   * 해당 메서드를 호출하고 개체의 컨텐트 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 컨텐트 유형을 `setContentType` `com.adobe.idp.Document` 설정합니다.
   * 개체의 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 `javax.servlet.http.HttpServletResponse` `getOutputStream` 만듭니다.
   * 개체 `java.io.InputStream` 의 메서드를 호출하여 `com.adobe.idp.Document` 개체를 `getInputStream` 만듭니다.
   * 바이트 배열을 만들고 `InputStream` `read` 개체의 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * 개체의 `javax.servlet.ServletOutputStream` 메서드를 `write` 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 보냅니다. 바이트 배열을 `write` 메서드로 전달합니다.

**참고 항목**

[양식을 HTML로 렌더링](#rendering-forms-as-html)

[빠른 시작(SOAP 모드): Java API를 사용하여 HTML 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 양식을 HTML로 렌더링 {#render-a-form-as-html-using-the-web-service-api}

Forms API(웹 서비스)를 사용하여 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   객체를 만들고 인증 값을 `FormsService` 설정합니다.

1. HTML 런타임 옵션 설정

   * 생성자를 사용하여 `HTMLRenderSpec` 개체를 만듭니다.
   * 도구 모음을 사용하여 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체의 `setHTMLToolbar` 메서드를 호출하고 열거형 값을 `HTMLToolbar` 전달합니다. 예를 들어 세로 HTML 도구 모음을 표시하려면 전달하십시오 `HTMLToolbar.Vertical`.
   * HTML 양식의 로케일 값을 설정하려면 `HTMLRenderSpec` 개체의 `setLocale` 메서드를 호출하고 로케일 값을 지정하는 문자열 값을 전달합니다. 자세한 내용은 [AEM Forms API 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 전체 HTML 태그 내에서 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체의 `setOutputType` 메서드를 호출하고 전달합니다 `OutputType.FullHTMLTags`.

   >[!NOTE]
   이 `StandAlone` 옵션이 선택되어 있고 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버 이외의 서버를 참조하는 경우 양식 `true` 이 HTML로 `ApplicationWebRoot` 렌더링되지 않습니다. 이 `ApplicationWebRoot` 값은 `URLSpec` 개체의 `FormsServiceClient` `(Deprecated) renderHTMLForm` 메서드에 전달된 개체를 사용하여 지정됩니다. 이 서버 `ApplicationWebRoot` 가 하나의 호스팅 AEM Forms에서 다른 서버일 경우 관리 콘솔에서 웹 루트 URI의 값을 양식의 웹 응용 프로그램 URI 값으로 설정해야 합니다. 관리 콘솔에 로그인하고 서비스 > 양식을 클릭한 다음 웹 루트 URI를 https://server-name:port/FormServer으로 설정하여 수행할 수 있습니다. 그런 다음 설정을 저장합니다.

1. HTML 양식 렌더링

   개체의 `FormsService` 메서드를 `(Deprecated) renderHTMLForm` 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장자를 포함하여 양식 디자인 이름을 지정하는 문자열 값. Forms 응용 프로그램의 일부인 양식 디자인을 참조하는 경우 전체 경로를 지정해야 합니다(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`).
   * HTML `TransformTo` 기본 설정 형식을 지정하는 열거형 값. 예를 들어 Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 을 지정합니다 `TransformTo.MSDHTML`.
   * 양식과 병합할 데이터가 포함된 `BLOB` 개체 데이터를 병합하지 않으려면 전달하십시오 `null`. ( [순서별 레이아웃으로 양식 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)참조)
   * HTML 런타임 옵션을 저장하는 `HTMLRenderSpec` 개체입니다.
   * 헤더 값을 지정하는 `HTTP_USER_AGENT` 문자열 값; 예를 들면 다음과 같습니다 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 이 값을 설정하지 않으려는 경우 빈 문자열을 전달할 수 있습니다.
   * HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 `URLSpec` 개체입니다. 자세한 내용은 [URI 값 지정을 참조하십시오](/help/forms/developing/rendering-interactive-pdf-forms.md).
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택 매개 변수이며 양식에 파일을 첨부하지 않으려는 `null` 경우 지정할 수 있습니다. 양식에 [파일 첨부를 참조하십시오](/help/forms/developing/rendering-interactive-pdf-forms.md).
   * 메서드로 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 이 매개 변수 값은 렌더링된 양식을 저장합니다.
   * 메서드로 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 이 매개 변수는 출력 XML 데이터를 저장합니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 개체입니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 로케일 값을 저장합니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 사용되는 HTML 렌더링 값을 저장합니다.
   * 이 작업 결과를 포함할 빈 `com.adobe.idp.services.holders.FormsResultHolder` 개체입니다.

   이 `(Deprecated) renderHTMLForm` 메서드는 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 채웁니다.

1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰기

   * 개체 `FormResult` 의 데이터 멤버 값을 가져와서 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 `value` 만듭니다.
   * 개체의 메서드를 호출하여 양식 데이터 `BLOB` 가 포함된 `FormsResult` `getOutputContent` 개체를 만듭니다.
   * 해당 메서드를 호출하여 개체의 `BLOB` 콘텐츠 유형을 `getContentType` 가져옵니다.
   * 해당 메서드를 호출하고 개체의 컨텐트 유형을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 컨텐트 유형을 `setContentType` `BLOB` 설정합니다.
   * 개체의 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 `javax.servlet.http.HttpServletResponse` `getOutputStream` 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 개체의 메서드를 호출하여 `getBinaryData` 채웁니다. 이 작업은 개체의 내용을 바이트 배열에 `FormsResult` 할당합니다.
   * 개체의 `javax.servlet.http.HttpServletResponse` 메서드를 `write` 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 보냅니다. 바이트 배열을 `write` 메서드로 전달합니다.

**참고 항목**

[양식을 HTML로 렌더링](#rendering-forms-as-html)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

