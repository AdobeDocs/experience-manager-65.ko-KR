---
title: Forms을 HTML로 렌더링
seo-title: Forms을 HTML로 렌더링
description: 웹 브라우저의 HTTP 요청에 응답하여 양식을 HTML로 렌더링하려면 Forms 서비스를 사용합니다. Java API 및 웹 서비스 API를 사용하여 양식을 HTML로 렌더링할 수 있습니다.
seo-description: 웹 브라우저의 HTTP 요청에 응답하여 양식을 HTML로 렌더링하려면 Forms 서비스를 사용합니다. Java API 및 웹 서비스 API를 사용하여 양식을 HTML로 렌더링할 수 있습니다.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4188'
ht-degree: 0%

---

# Forms을 HTML {#rendering-forms-as-html}으로 렌더링

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

Forms 서비스는 웹 브라우저에서 HTTP 요청에 응답하여 양식을 HTML로 렌더링합니다. 양식을 HTML로 렌더링하면 클라이언트 웹 브라우저가 있는 컴퓨터에서 Adobe Reader, Acrobat 또는 Flash Player(양식 안내서(더 이상 사용되지 않음)가 필요하지 않습니다.

양식을 HTML로 렌더링하려면 양식 디자인을 XDP 파일로 저장해야 합니다. PDF 파일로 저장된 양식 디자인은 HTML로 렌더링할 수 없습니다. HTML로 렌더링될 디자이너에서 양식 디자인을 개발할 때 다음 기준을 고려하십시오.

* 개체의 테두리 속성을 사용하여 양식에 선, 상자 또는 그리드를 그리거나 그리드를 그리면 안 됩니다. 일부 브라우저는 미리 보기에 표시된 대로 테두리를 정렬하지 않을 수 있습니다. 객체가 레이어로 나타나거나 다른 객체를 원하는 위치에서 푸시할 수 있습니다.
* 선, 사각형 및 원을 사용하여 배경을 정의할 수 있습니다.
* 텍스트를 수용하는 데 필요한 것보다 약간 큰 텍스트를 그립니다. 일부 웹 브라우저에서는 텍스트를 읽기 쉽게 표시하지 않습니다.

>[!NOTE]
>
>`FormServiceClient` 개체의 `(Deprecated) renderHTMLForm` 및 `renderHTMLForm2` 메서드를 사용하여 TIFF 이미지가 포함된 양식을 렌더링할 때 Internet Explorer 또는 Mozilla Firefox 브라우저에 표시되는 렌더링된 HTML 양식에는 TIFF 이미지가 표시되지 않습니다. 이러한 브라우저는 TIFF 이미지에 대한 기본 지원을 제공하지 않습니다.

## HTML 페이지 {#html-pages}

양식 디자인이 HTML 양식으로 렌더링되면 각 두 번째 수준의 하위 양식이 HTML 페이지(패널)로 렌더링됩니다. 디자이너에서 하위 양식의 계층을 볼 수 있습니다. 루트 하위 폼에 속하는 하위 폼(루트 하위 양식의 기본 이름은 form1임)은 패널 하위 폼입니다. 다음 예제에서는 양식 디자인의 하위 양식을 보여줍니다.

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

양식 디자인을 HTML 양식으로 렌더링할 때 패널은 특정 페이지 크기로 제한되지 않습니다. 동적 하위 양식이 있는 경우 패널 하위 양식 내에 중첩되어야 합니다. 동적 하위 양식은 HTML 페이지를 무제한으로 확장할 수 있습니다.

양식을 HTML 양식으로 렌더링할 때 페이지 크기(PDF로 렌더링된 양식의 페이지 매김에 필요)는 아무런 의미가 없습니다. 유동성 레이아웃이 있는 양식은 무한 수의 HTML 페이지로 확장될 수 있으므로 마스터 페이지에서 바닥글을 사용하지 않는 것이 중요합니다. 마스터 페이지의 콘텐츠 영역 아래에 있는 바닥글은 페이지 경계를 넘어 이동하는 HTML 콘텐츠를 덮어쓸 수 있습니다.

`xfa.host.pageUp` 및 `xfa.host.pageDown` 메서드를 사용하여 패널에서 패널로 명시적으로 이동해야 합니다. 양식을 Forms 서비스에 보내고 Forms 서비스가 양식을 클라이언트 장치(일반적으로 웹 브라우저)로 다시 렌더링하도록 하여 페이지를 변경합니다.

>[!NOTE]
>
>양식을 Forms 서비스에 보낸 다음 Forms 서비스가 양식을 다시 클라이언트 장치로 렌더링하도록 하는 프로세스를 서버로의 반올림 트리핑 데이터라고 합니다.

>[!NOTE]
>
>HTML 양식에서 HTML 디지털 서명 단추의 모양을 사용자 지정하려면 fscsig.css 파일(adobe-forms-ds.ear > adobe-forms-ds.war 파일 내)에서 다음 속성을 변경해야 합니다.

**.fsc-ds-ssb**:이 스타일 시트는 빈 기호 필드의 경우 적용할 수 있습니다.

**.fsc-ds-ssv**:이 스타일 시트는 유효한 기호 필드의 경우에 적용할 수 있습니다.

**.fsc-ds-ssc**:이 스타일 시트는 유효한 기호 필드의 경우 적용되지만 데이터가 변경되었습니다.

**.fsc-ds-ssi**:이 스타일 시트는 잘못된 기호 필드의 경우 적용할 수 있습니다.

**.fsc-ds-popup-bg**:이 스타일 시트 속성을 사용하지 않습니다.

**.fsc-ds-popup-btn**:이 스타일 시트 속성을 사용하지 않습니다.

## 스크립트 실행 중 {#running-scripts}

양식 작성자는 서버에서 스크립트가 실행되는지 클라이언트에서 실행되는지를 지정합니다. Forms 서비스는 `runAt` 속성을 사용하여 클라이언트와 서버 간에 배포할 수 있는 양식 인텔리전스 실행을 위한 분산 이벤트 처리 환경을 만듭니다. 이 특성 또는 양식 디자인 내에서 스크립트를 만드는 방법에 대한 자세한 내용은 [Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63)를 참조하십시오

양식을 렌더링하는 동안 Forms 서비스에서 스크립트를 실행할 수 있습니다. 따라서 클라이언트에서 사용할 수 없는 데이터베이스 또는 웹 서비스에 연결하여 양식을 미리 데이터로 채울 수 있습니다. 클라이언트에서 서버로 이동 데이터를 반올림하도록 단추의 `Click` 이벤트를 서버에서 실행하도록 설정할 수도 있습니다. 이를 통해 사용자는 양식과 상호 작용할 때 엔터프라이즈 데이터베이스와 같은 서버 리소스를 필요로 할 수 있는 스크립트를 실행할 수 있습니다. HTML Forms의 경우 양식 계산 스크립트는 서버에서만 실행할 수 있습니다. 따라서 이러한 스크립트를 `server` 또는 `both`에서 실행하도록 표시해야 합니다.

`xfa.host.pageUp` 및 `xfa.host.pageDown` 메서드를 호출하여 페이지(패널) 간에 이동하는 양식을 디자인할 수 있습니다. 이 스크립트는 단추의 `Click` 이벤트에 배치되며 `runAt` 속성이 `Both`로 설정됩니다. `Both`을 선택하는 이유는 Adobe Reader 또는 Acrobat(PDF로 렌더링되는 양식의 경우)가 서버로 이동하지 않고 페이지를 변경할 수 있고 HTML Forms가 데이터를 서버에 반올림하여 페이지를 변경할 수 있기 때문입니다. 즉, 양식이 Forms 서비스로 전송되고 양식이 새 페이지가 표시된 상태로 HTML로 다시 렌더링됩니다.

스크립트 변수 및 양식 필드에 항목과 같은 이름을 지정하지 않는 것이 좋습니다. Internet Explorer와 같은 일부 웹 브라우저는 스크립트 오류가 발생하는 양식 필드와 동일한 이름의 변수를 초기화할 수 없습니다. 양식 필드와 스크립트 변수에 다른 이름을 지정하는 것이 좋습니다.

페이지 탐색 기능과 양식 스크립트가 모두 포함된 HTML 양식을 렌더링할 때(예를 들어, 스크립트가 양식을 렌더링할 때마다 데이터베이스에서 필드 데이터를 검색한다고 가정) 양식 스크립트가 form:readyevent 대신 form:calculate event에 있는지 확인합니다.

form:ready 이벤트에 있는 양식 스크립트는 양식의 초기 렌더링 중에 한 번만 실행되며 후속 페이지 검색에 대해 실행되지 않습니다. 반면에 form:calculate 이벤트는 양식이 렌더링되는 각 페이지 탐색에 대해 실행됩니다.

>[!NOTE]
다중 페이지 양식에서는 다른 페이지로 이동하는 경우 JavaScript에서 페이지에 변경한 내용이 유지되지 않습니다.

양식을 제출하기 전에 사용자 지정 스크립트를 호출할 수 있습니다. 이 기능은 사용 가능한 모든 브라우저에서 작동합니다. 그러나 사용자가 `Output Type` 속성이 `Form Body`로 설정된 HTML 양식을 렌더링할 때만 사용할 수 있습니다. `Output Type`이 `Full HTML`이면 작동하지 않습니다. 이 기능을 구성하는 단계는 관리 도움말의 양식 구성 을 참조하십시오.

먼저 양식을 제출하기 전에 호출되는 콜백 함수를 정의해야 합니다. 여기서 함수의 이름은 `_user_onsubmit`입니다. 이 경우 함수는 예외를 throw하지 않거나 예외를 throw하는 경우 예외가 무시됩니다. JavaScript 함수를 html의 헤드 섹션에 배치하는 것이 좋습니다.그러나 `xfasubset.js` 을 포함하는 스크립트 태그가 종료되기 전 어디에서든 선언할 수 있습니다.

양식 서버에서 드롭다운 목록이 포함된 XDP를 렌더링할 때 드롭다운 목록을 만들 뿐만 아니라 두 개의 숨겨진 텍스트 필드도 만듭니다. 이러한 텍스트 필드는 드롭다운 목록의 데이터를 저장합니다(하나는 옵션의 표시 이름을 저장하고 다른 하나는 옵션 값을 저장합니다). 따라서 사용자가 양식을 제출할 때마다 드롭다운 목록의 전체 데이터가 제출됩니다. 매번 그렇게 많은 데이터를 제출하지 않으려는 경우 사용자 지정 스크립트를 작성하여 이를 비활성화할 수 있습니다. 예:드롭다운 목록의 이름은 `drpOrderedByStateProv`이며 하위 양식 헤더 아래에 래핑됩니다. HTML 입력 요소의 이름은 `header[0].drpOrderedByStateProv[0]`입니다. 드롭다운의 데이터를 저장하고 제출하는 숨김 필드의 이름은 다음과 같습니다.`header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

데이터를 게시하지 않으려면 다음과 같이 이러한 입력 요소를 비활성화할 수 있습니다.`var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

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

## XFA 하위 집합 {#xfa-subsets}

HTML로 렌더링할 양식 디자인을 만들 때 JavaScript 언어의 스크립트에 대한 XFA 하위 집합으로 스크립팅을 제한해야 합니다.

클라이언트에서 실행되거나 클라이언트와 서버 모두에서 실행되는 스크립트는 XFA 하위 집합 내에 작성해야 합니다. 서버에서 실행되는 스크립트는 전체 XFA 스크립팅 모델을 사용하고 FormCalc도 사용할 수 있습니다. JavaScript 사용에 대한 자세한 내용은 [Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63)를 참조하십시오.

클라이언트에서 스크립트를 실행할 때 표시되는 현재 패널만 스크립트를 사용할 수 있습니다.예를 들어 패널 B가 표시될 때 패널 A에 있는 필드에 대해 스크립팅할 수 없습니다. 서버에서 스크립트를 실행할 때 모든 패널에 액세스할 수 있습니다.

또한 클라이언트에서 실행되는 스크립트 내에서 SOM(Scripting Object Model) 표현식을 사용할 때도 주의해야 합니다. 클라이언트에서 실행되는 스크립트에서는 SOM 표현식의 단순 하위 집합만 지원됩니다.

## 이벤트 타이밍 {#event-timing}

XFA 하위 세트는 HTML 이벤트에 매핑되는 XFA 이벤트를 정의합니다. 이벤트 계산 및 유효성 검사 타이밍에 대한 동작에 약간의 차이가 있습니다. 웹 브라우저에서 필드를 종료하면 전체 계산 이벤트가 실행됩니다. 필드 값을 변경할 때 이벤트 계산 이 자동으로 실행되지 않습니다. `xfa.form.execCalculate` 메서드를 호출하여 계산 이벤트를 강제 적용할 수 있습니다.

웹 브라우저에서 이벤트 유효성 검사는 필드를 종료하거나 양식을 제출할 때만 실행됩니다. `xfa.form.execValidate` 메서드를 사용하여 유효성 검사 이벤트를 강제 적용할 수 있습니다.

웹 브라우저에 표시되는 Forms(Adobe Reader 또는 Acrobat과 대조적으로)는 필수 필드에 대한 XFA null 테스트(오류 또는 경고)를 따릅니다.

* null 테스트에 오류가 발생하여 값을 지정하지 않고 필드를 종료하면 메시지 상자가 표시되고 확인을 클릭하면 필드에 다시 배치됩니다.
* null 테스트에 경고가 발생하고 값을 지정하지 않고 필드를 종료하면 확인 또는 취소 를 클릭하라는 메시지가 표시됩니다. 값을 지정하지 않고 계속 진행할 수 있는 옵션을 제공하거나 값을 입력할 수 있는 필드로 돌아갑니다.

null 테스트에 대한 자세한 내용은 [Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63)를 참조하십시오.

## 양식 단추 {#form-buttons}

제출 단추를 클릭하면 양식 데이터가 Forms 서비스로 전송되고 양식 처리 종료를 나타냅니다. `preSubmit` 이벤트는 클라이언트 또는 서버에서 실행되도록 설정할 수 있습니다. 클라이언트에서 실행되도록 구성된 경우 `preSubmit` 이벤트는 양식 제출 전에 실행됩니다. 그렇지 않으면 양식을 제출하는 동안 서버에서 `preSubmit` 이벤트가 실행됩니다. `preSubmit` 이벤트에 대한 자세한 내용은 [Forms 디자이너](https://www.adobe.com/go/learn_aemforms_designer_63)를 참조하십시오.

단추에 연결된 클라이언트측 스크립트가 없으면 데이터가 서버에 전송되고 서버에서 계산을 수행하고 HTML 양식이 다시 생성됩니다. 단추에 클라이언트측 스크립트가 포함되어 있으면 데이터가 서버로 전송되지 않고 클라이언트측 스크립트가 웹 브라우저에서 실행됩니다.

## HTML 4.0 웹 브라우저 {#html-4-0-web-browser}

HTML 4.0만 지원하는 웹 브라우저는 XFA 하위 집합 클라이언트측 스크립팅 모델을 지원할 수 없습니다. HTML 4.0과 MSDHTML 또는 CSS2HTML에서 모두 작동하도록 양식 디자인을 만들면 클라이언트에서 실행되도록 표시된 스크립트가 실제로 서버에서 실행됩니다. 예를 들어, 사용자가 HTML 4.0 웹 브라우저에 표시되는 양식에 있는 단추를 클릭한다고 가정해 보겠습니다. 이 경우 양식 데이터는 클라이언트측 스크립트가 실행되는 서버로 전송됩니다.

HTML 4.0의 서버와 MSDHTML 또는 CSS2HTML용 클라이언트에서 실행되는 계산 이벤트에 양식 논리를 배치하는 것이 좋습니다.

## 프레젠테이션 변경 사항 유지 관리 {#maintaining-presentation-changes}

HTML 페이지(패널) 간을 이동할 때 데이터의 상태만 유지됩니다. 배경색 또는 필수 필드 설정과 같은 설정은 유지되지 않습니다(초기 설정과 다른 경우). 프레젠테이션 상태를 유지하려면 필드의 표시 상태를 나타내는 필드(일반적으로 숨김)를 만들어야 합니다. 숨겨진 필드 값을 기반으로 프레젠테이션을 변경하는 필드의 `Calculate` 이벤트에 스크립트를 추가하는 경우 HTML 페이지(패널) 간을 앞뒤로 이동할 때 프레젠테이션 상태를 유지할 수 있습니다.

다음 스크립트는 `hiddenField` 값을 기반으로 필드의 `fillColor`을 유지 관리합니다. 이 스크립트가 필드의 `Calculate` 이벤트에 있다고 가정합니다.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
정적 개체는 표 셀 내에 중첩될 때 렌더링된 HTML 양식에 표시되지 않습니다. 예를 들어, 표 셀 내부에 중첩된 원 및 사각형은 렌더링 HTML 양식 내에 표시되지 않습니다. 그러나 이러한 동일한 정적 개체는 테이블 외부에 있을 때 올바르게 표시됩니다.

## HTML 양식에 디지털 서명 {#digitally-signing-html-forms}

양식이 다음 HTML 변형 중 하나로 렌더링되는 경우 디지털 서명 필드가 포함된 HTML 양식에 서명할 수 없습니다.

* AHTML
* HTML4
* 정적 HTML
* NoScriptXHTML

문서 디지털 서명에 대한 자세한 내용은 [디지털 서명 및 인증 문서](/help/forms/developing/digitally-signing-certifying-documents.md)를 참조하십시오

## 액세스 가능성 지침 호환 XHTML 양식 렌더링 {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

액세스 가능성 지침을 준수하는 전체 HTML 양식을 렌더링할 수 있습니다. 즉, 양식이 본문 태그 내에 렌더링되는 HTML 양식과 비교하여 전체 HTML 태그 내에 렌더링됩니다(완전한 HTML 페이지가 아님).

## 양식 데이터 {#validating-form-data} 확인

양식을 HTML 양식으로 렌더링할 때는 양식 필드에 대한 유효성 검사 규칙 사용을 제한하는 것이 좋습니다. 일부 유효성 검사 규칙은 HTML 양식에 지원되지 않을 수 있습니다. 예를 들어, HTML 양식으로 렌더링되는 양식 디자인에 있는 `Date/Time` 필드에 YYYY-MM-DD의 유효성 검사 패턴이 적용되면, 날짜가 올바르게 입력되더라도 제대로 작동하지 않습니다. 그러나 이 유효성 검사 패턴은 PDF로 렌더링된 양식에 대해 올바르게 작동합니다.

>[!NOTE]
Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 단계 요약 {#summary-of-steps}

HTML 양식을 렌더링하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Forms 클라이언트 API 개체를 만듭니다.
1. HTML 런타임 옵션을 설정합니다.
1. HTML 양식을 렌더링합니다.
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms 클라이언트 API 개체 만들기**

데이터를 프로그래밍 방식으로 PDF formClient API로 가져오려면 먼저 양식 데이터 통합 서비스 클라이언트를 만들어야 합니다. 서비스 클라이언트를 만들 때 서비스를 호출하는 데 필요한 연결 설정을 정의합니다.

**HTML 런타임 옵션 설정**

HTML 양식을 렌더링할 때 HTML 런타임 옵션을 설정합니다. 예를 들어, HTML 양식에 도구 모음을 추가하여 클라이언트 컴퓨터에 있는 첨부 파일을 선택하거나 HTML 양식으로 렌더링되는 첨부 파일을 검색할 수 있습니다. 기본적으로 HTML 도구 모음은 비활성화됩니다. HTML 양식에 도구 모음을 추가하려면 프로그래밍 방식으로 런타임 옵션을 설정해야 합니다. 기본적으로 HTML 도구 모음은 다음 단추로 구성됩니다.

* `Home`:응용 프로그램의 웹 루트에 대한 링크를 제공합니다.
* `Upload`:현재 양식에 첨부할 파일을 선택하는 사용자 인터페이스를 제공합니다.
* `Download`:첨부된 파일을 표시할 사용자 인터페이스를 제공합니다.

HTML 도구 모음이 HTML 양식에 나타나면 사용자는 양식 데이터와 함께 제출할 최대 10개의 파일을 선택할 수 있습니다. 파일이 제출되면 Forms 서비스는 파일을 검색할 수 있습니다.

양식을 HTML로 렌더링할 때 사용자 에이전트 값을 지정할 수 있습니다. 사용자 에이전트 값은 브라우저 및 시스템 정보를 제공합니다. 이 값은 선택 값이며 빈 문자열 값을 전달할 수 있습니다. Java API 빠른 시작을 사용하여 HTML 양식 렌더링은 사용자 에이전트 값을 가져와 양식을 HTML로 렌더링하는 데 사용하는 방법을 보여 줍니다.

양식 데이터가 게시되는 HTTP URL은 Forms Service Client API를 사용하여 대상 URL을 설정하여 지정하거나 XDP 양식 디자인에 포함된 제출 단추에 지정할 수 있습니다. 대상 URL이 양식 디자인에 지정된 경우 Forms 서비스 클라이언트 API를 사용하여 값을 설정하지 마십시오.

>[!NOTE]
도구 모음을 사용하여 HTML 양식을 렌더링하는 것은 선택 사항입니다.

>[!NOTE]
AHTML 양식을 렌더링하는 경우에는 양식에 도구 모음을 추가하지 않는 것이 좋습니다.

**HTML 양식 렌더링**

HTML 양식을 렌더링하려면 디자이너에서 만들고 XDP 파일로 저장한 양식 디자인을 지정해야 합니다. HTML 변형 유형도 선택해야 합니다. 예를 들어 Internet Explorer 5.0 이상에서 동적 HTML을 렌더링하는 HTML 변형 유형을 지정할 수 있습니다.

HTML 양식을 렌더링하려면 다른 양식 유형을 렌더링하는 데 필요한 URI 값과 같은 값도 필요합니다.

**클라이언트 웹 브라우저에 양식 데이터 스트림 쓰기**

Forms 서비스에서 HTML 양식을 렌더링하면 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다. 클라이언트 웹 브라우저에 작성하면 HTML 양식이 사용자에게 표시됩니다.

**참고 항목**

[Java API를 사용하여 양식을 HTML로 렌더링합니다.](#render-a-form-as-html-using-the-java-api)

[웹 서비스 API를 사용하여 양식을 HTML로 렌더링합니다.](#render-a-form-as-html-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[사용자 지정 도구 모음을 사용하여 HTML Forms 렌더링](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API {#render-a-form-as-html-using-the-java-api}를 사용하여 양식을 HTML로 렌더링합니다.

Forms API(Java)를 사용하여 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 `FormsServiceClient` 개체를 만들고 `ServiceClientFactory` 개체를 전달합니다.

1. HTML 런타임 옵션 설정

   * 생성자를 사용하여 `HTMLRenderSpec` 개체를 만듭니다.
   * 도구 모음을 사용하여 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체의 `setHTMLToolbar` 메서드를 호출하고 `HTMLToolbar` 열거형 값을 전달합니다. 예를 들어, 세로 HTML 도구 모음을 표시하려면 `HTMLToolbar.Vertical`을 전달합니다.
   * HTML 양식의 로케일 값을 설정하려면 `HTMLRenderSpec` 개체의 `setLocale` 메서드를 호출하고 로케일 값을 지정하는 문자열 값을 전달합니다. (선택적 설정입니다.)
   * 전체 HTML 태그 내에 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체의 `setOutputType` 메서드를 호출하고 `OutputType.FullHTMLTags`를 전달합니다. (선택적 설정입니다.)

   >[!NOTE]
   `StandAlone` 옵션이 `true`이고 `ApplicationWebRoot`가 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버가 아닌 서버를 참조하는 경우 Forms이 HTML에서 성공적으로 렌더링되지 않습니다(`ApplicationWebRoot` 값은 `FormsServiceClient` 개체의 `(Deprecated) renderHTMLForm` 메서드에 전달된 `URLSpec` 개체를 사용하여 지정됩니다.) `ApplicationWebRoot` 이 하나의 호스팅 AEM Forms의 다른 서버인 경우 관리 콘솔에서 웹 루트 URI 값을 양식의 웹 애플리케이션 URI 값으로 설정해야 합니다. 이 작업은 관리 콘솔에 로그인하고, 서비스 > Forms을 클릭하고, 웹 루트 URI를 https://server-name:port/FormServer으로 설정하여 수행할 수 있습니다. 그런 다음 설정을 저장합니다.

1. HTML 양식 렌더링

   `FormsServiceClient` 개체의 `(Deprecated) renderHTMLForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장명을 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램의 일부인 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`)를 지정해야 합니다.
   * HTML 환경 설정 유형을 지정하는 `TransformTo` 열거형 값. 예를 들어, Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 `TransformTo.MSDHTML` 을 지정합니다.
   * 폼과 병합할 데이터를 포함하는 `com.adobe.idp.Document` 개체입니다. 데이터를 병합하지 않으려면 빈 `com.adobe.idp.Document` 개체를 전달합니다.
   * HTML 런타임 옵션을 저장하는 `HTMLRenderSpec` 개체입니다.
   * `HTTP_USER_AGENT` 헤더 값을 지정하는 문자열 값;예: `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`
   * HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 `URLSpec` 개체입니다.
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택적 매개 변수이며 양식에 파일을 첨부하지 않으려는 경우 `null`을 지정할 수 있습니다.

   `(Deprecated) renderHTMLForm` 메서드는 클라이언트 웹 브라우저에 쓸 수 있는 양식 데이터 스트림을 포함하는 `FormsResult` 개체를 반환합니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 쓰기

   * `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 호출하여 `com.adobe.idp.Document` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `com.adobe.idp.Document` 개체의 콘텐츠 형식을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `com.adobe.idp.Document` 개체의 콘텐츠 형식을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 콘텐츠 형식을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 클라이언트 웹 브라우저에 양식 데이터 스트림을 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * `com.adobe.idp.Document` 개체의 `getInputStream` 메서드를 호출하여 `java.io.InputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `InputStream` 개체의 `read` 메서드를 호출하고 바이트 배열을 인수로 전달하여 양식 데이터 스트림으로 채웁니다.
   * `javax.servlet.ServletOutputStream` 개체의 `write` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저로 보냅니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[Forms을 HTML로 렌더링](#rendering-forms-as-html)

[빠른 시작(SOAP 모드):Java API를 사용하여 HTML 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API {#render-a-form-as-html-using-the-web-service-api}를 사용하여 양식을 HTML로 렌더링합니다.

Forms API(웹 서비스)를 사용하여 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * Java 프록시 클래스를 클래스 경로에 포함합니다.

1. Forms 클라이언트 API 개체 만들기

   `FormsService` 개체를 만들고 인증 값을 설정합니다.

1. HTML 런타임 옵션 설정

   * 생성자를 사용하여 `HTMLRenderSpec` 개체를 만듭니다.
   * 도구 모음을 사용하여 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체의 `setHTMLToolbar` 메서드를 호출하고 `HTMLToolbar` 열거형 값을 전달합니다. 예를 들어, 세로 HTML 도구 모음을 표시하려면 `HTMLToolbar.Vertical`을 전달합니다.
   * HTML 양식의 로케일 값을 설정하려면 `HTMLRenderSpec` 개체의 `setLocale` 메서드를 호출하고 로케일 값을 지정하는 문자열 값을 전달합니다. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.
   * 전체 HTML 태그 내에 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체의 `setOutputType` 메서드를 호출하고 `OutputType.FullHTMLTags`를 전달합니다.

   >[!NOTE]
   `StandAlone` 옵션이 `true`이고 `ApplicationWebRoot`가 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버가 아닌 서버를 참조하는 경우 Forms이 HTML에서 성공적으로 렌더링되지 않습니다(`ApplicationWebRoot` 값은 `FormsServiceClient` 개체의 `(Deprecated) renderHTMLForm` 메서드에 전달된 `URLSpec` 개체를 사용하여 지정됩니다.) `ApplicationWebRoot` 이 하나의 호스팅 AEM Forms의 다른 서버인 경우 관리 콘솔에서 웹 루트 URI 값을 양식의 웹 애플리케이션 URI 값으로 설정해야 합니다. 이 작업은 관리 콘솔에 로그인하고, 서비스 > Forms을 클릭하고, 웹 루트 URI를 https://server-name:port/FormServer으로 설정하여 수행할 수 있습니다. 그런 다음 설정을 저장합니다.

1. HTML 양식 렌더링

   `FormsService` 개체의 `(Deprecated) renderHTMLForm` 메서드를 호출하고 다음 값을 전달합니다.

   * 파일 이름 확장명을 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 응용 프로그램의 일부인 양식 디자인을 참조하는 경우 전체 경로(예: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`)를 지정해야 합니다.
   * HTML 환경 설정 유형을 지정하는 `TransformTo` 열거형 값. 예를 들어, Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 `TransformTo.MSDHTML` 을 지정합니다.
   * 폼과 병합할 데이터를 포함하는 `BLOB` 개체입니다. 데이터를 병합하지 않으려면 `null`을 전달합니다. ([유동형 레이아웃으로 Forms 미리 채우기](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts)를 참조하십시오.)
   * HTML 런타임 옵션을 저장하는 `HTMLRenderSpec` 개체입니다.
   * `HTTP_USER_AGENT` 헤더 값을 지정하는 문자열 값;예: `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)` 이 값을 설정하지 않으려는 경우 빈 문자열을 전달할 수 있습니다.
   * HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 `URLSpec` 개체입니다. ( [URI 값 지정](/help/forms/developing/rendering-interactive-pdf-forms.md)을 참조하십시오.)
   * 첨부 파일을 저장하는 `java.util.HashMap` 개체입니다. 선택적 매개 변수이며 양식에 파일을 첨부하지 않으려는 경우 `null`을 지정할 수 있습니다. ([양식](/help/forms/developing/rendering-interactive-pdf-forms.md)에 파일 첨부 를 참조하십시오.)
   * 메서드로 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 이 매개 변수 값은 렌더링된 양식을 저장합니다.
   * 메서드로 채워지는 빈 `com.adobe.idp.services.holders.BLOBHolder` 개체입니다. 이 매개 변수는 출력 XML 데이터를 저장합니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.LongHolder` 개체입니다. 이 인수는 양식에 페이지 수를 저장합니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 로케일 값을 저장합니다.
   * 메서드로 채워지는 빈 `javax.xml.rpc.holders.StringHolder` 개체입니다. 이 인수는 사용되는 HTML 렌더링 값을 저장합니다.
   * 이 작업의 결과가 포함될 빈 `com.adobe.idp.services.holders.FormsResultHolder` 개체입니다.

   `(Deprecated) renderHTMLForm` 메서드는 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림으로 마지막 인수 값으로 전달되는 `com.adobe.idp.services.holders.FormsResultHolder` 개체를 채웁니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 쓰기

   * `com.adobe.idp.services.holders.FormsResultHolder` 개체의 `value` 데이터 멤버의 값을 가져와서 `FormResult` 개체를 만듭니다.
   * `FormsResult` 개체의 `getOutputContent` 메서드를 호출하여 양식 데이터가 포함된 `BLOB` 개체를 만듭니다.
   * `getContentType` 메서드를 호출하여 `BLOB` 개체의 콘텐츠 형식을 가져옵니다.
   * `setContentType` 메서드를 호출하고 `BLOB` 개체의 콘텐츠 형식을 전달하여 `javax.servlet.http.HttpServletResponse` 개체의 콘텐츠 형식을 설정합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `getOutputStream` 메서드를 호출하여 클라이언트 웹 브라우저에 양식 데이터 스트림을 쓰는 데 사용되는 `javax.servlet.ServletOutputStream` 개체를 만듭니다.
   * 바이트 배열을 만들고 `BLOB` 개체의 `getBinaryData` 메서드를 호출하여 채웁니다. 이 작업은 `FormsResult` 개체의 콘텐츠를 바이트 배열에 할당합니다.
   * `javax.servlet.http.HttpServletResponse` 개체의 `write` 메서드를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저로 보냅니다. 바이트 배열을 `write` 메서드에 전달합니다.

**참고 항목**

[Forms을 HTML로 렌더링](#rendering-forms-as-html)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
