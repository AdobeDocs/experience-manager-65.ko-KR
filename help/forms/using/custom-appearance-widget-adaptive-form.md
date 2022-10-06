---
title: 적응형 양식 필드에 대한 사용자 지정 모양 만들기
seo-title: Create custom appearances for adaptive form fields
description: 응용 Forms에서 기본 구성 요소의 모양을 사용자 지정합니다.
seo-description: Customize appearance of out-of-the-box components in Adaptive Forms.
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
source-git-commit: 8a24ca02762e7902b7d0033b36560629ee711de1
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 0%

---

# 적응형 양식 필드에 대한 사용자 지정 모양 만들기{#create-custom-appearances-for-adaptive-form-fields}

## 소개 {#introduction}

적응형 양식은 [모양 프레임워크](/help/forms/using/introduction-widgets.md) 적응형 양식 필드에 대한 사용자 지정 모양을 만들고 다른 사용자 경험을 제공하는 데 도움이 됩니다. 예를 들어, 라디오 단추와 확인란을 전환 단추로 바꾸거나 사용자 지정 jQuery 플러그인을 사용하여 전화 번호나 이메일 ID와 같은 필드에 사용자 입력을 제한합니다.

이 문서에서는 jQuery 플러그인을 사용하여 적응형 양식 필드에 대해 이러한 대체 경험을 만드는 방법을 설명합니다. 또한 숫자 필드 구성 요소가 숫자 스테퍼 또는 슬라이더로 표시되는 사용자 지정 모양을 만드는 예제를 보여줍니다.

이 문서에서 사용되는 주요 용어와 개념을 먼저 살펴보겠습니다.

**모양** 적응형 양식 필드의 다양한 요소의 스타일, 모양 및 느낌 및 구성을 나타냅니다. 이 목록에는 보통 입력, 도움말 아이콘, 필드에 대한 짧고 긴 설명을 제공하는 레이블, 대화형 영역이 포함되어 있습니다. 이 문서에서 설명한 모양새 사용자 지정은 필드의 입력 영역 모양에 적용됩니다.

**jQuery 플러그인** jQuery 위젯 프레임워크를 기반으로 대체 모양을 구현하는 표준 메커니즘을 제공합니다.

**ClientLib** 복잡한 JavaScript 및 CSS 코드에 의해 구동되는 AEM 클라이언트 측 처리에서의 클라이언트 측 라이브러리 시스템. 자세한 내용은 클라이언트측 라이브러리 사용 을 참조하십시오.

**원형** Maven 프로젝트용 원본 패턴 또는 모델로 정의된 Maven 프로젝트 템플릿 도구 키트입니다. 자세한 내용은 Archetypes 소개 를 참조하십시오.

**사용자 제어** 는 필드의 값을 포함하는 위젯의 기본 요소를 나타내며, 사용자 지정 위젯 UI를 적응형 양식 모델과 결합하기 위해 모양 프레임워크에서 사용됩니다.

## 사용자 정의 모양을 만드는 절차 {#steps-to-create-a-custom-appearance}

높은 수준에서 사용자 정의 모양을 만드는 단계는 다음과 같습니다.

1. **프로젝트 만들기**: AEM에 배포할 컨텐츠 패키지를 생성하는 Maven 프로젝트를 만듭니다.
1. **기존 위젯 클래스 확장**: 기존 위젯 클래스를 확장하고 필요한 클래스를 재정의합니다.
1. **클라이언트 라이브러리 만들기**: 만들기 `clientLib: af.customwidget` 라이브러리를 추가하고 필요한 JavaScript 및 CSS 파일을 추가합니다.

1. **프로젝트를 빌드하고 설치합니다**: Maven 프로젝트를 빌드하고 생성된 컨텐츠 패키지를 AEM에 설치합니다.
1. **적응형 양식 업데이트**: 적응형 양식 필드 속성을 업데이트하여 사용자 지정 모양을 사용합니다.

### 프로젝트 만들기 {#create-a-project}

maven 원형은 사용자 지정 모양을 만드는 시작점입니다. 사용할 원형 세부 사항은 다음과 같습니다.

* **저장소**: https://repo1.maven.org/maven2/com/adobe/
* **아티팩트 Id**: custom-appearance-archetype
* **그룹 Id**: com.adobe.aemforms
* **버전**: 1.0.4

다음 명령을 실행하여 원형 기반 로컬 프로젝트를 생성합니다.

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

이 명령은 저장소에서 Maven 플러그인 및 원형 정보를 다운로드하고 다음 정보를 기반으로 프로젝트를 생성합니다.

* **groupId**: 생성된 Maven 프로젝트에서 사용하는 그룹 ID
* **artifactId**: 생성된 Maven 프로젝트에서 사용하는 아티팩트 ID입니다.
* **버전**: 생성된 Maven 프로젝트의 버전입니다.
* **패키지**: 파일 구조에 사용되는 패키지입니다.
* **artifactName**: 생성된 AEM 패키지의 아티팩트 이름입니다.
* **packageGroup**: 생성된 AEM 패키지의 패키지 그룹입니다.
* **widgetName**: 참조에 사용되는 모양새 이름입니다.

생성된 프로젝트는 다음 구조를 갖습니다.

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### 기존 위젯 클래스 확장 {#extend-an-existing-widget-class}

프로젝트 템플릿이 생성되면 필요에 따라 다음 변경 사항을 수행합니다.

1. 프로젝트에 대한 타사 플러그인 종속성을 포함합니다.

   1. 타사 또는 사용자 지정 jQuery 플러그인을 `jqueryplugin/javascript` 의 폴더 및 관련 CSS 파일 `jqueryplugin/css` 폴더를 입력합니다. 자세한 내용은 `jqueryplugin/javascript and jqueryplugin/css` 폴더를 입력합니다.

   1. 수정 `js.txt` 및 `css.txt` 추가 JavaScript 및 jQuery 플러그인의 CSS 파일을 포함할 파일입니다.

1. 타사 플러그인을 프레임워크와 통합하여 사용자 지정 모양 프레임워크와 jQuery 플러그인 간의 상호 작용을 활성화합니다. 새 위젯은 다음 함수를 확장하거나 재정의한 후에만 작동합니다.

<table>
 <tbody>
  <tr>
   <td><strong>함수</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>render 함수는 위젯의 기본 HTML 요소에 대한 jQuery 개체를 반환합니다. 기본 HTML 요소는 포커스가 있는 유형이어야 합니다. 예, <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code>, 및 <code>&lt;li&gt;</code>. 반환된 요소는 <code>$userControl</code>. 만약 <code>$userControl</code> 위의 제약 조건, <code>AbstractWidget</code> 클래스가 예상대로 작동하므로, 그렇지 않으면 일부 일반적인 API(포커스, 클릭)에 변경이 필요합니다. </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>HTML 이벤트를 XFA 이벤트로 변환하는 맵을 반환합니다. <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> 이 예는 다음과 같습니다 <code>blur</code> 는 HTML 이벤트 및 <code>XFA_EXIT_EVENT</code> 는 해당 XFA 이벤트입니다. </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>옵션 변경에 대해 수행할 작업에 대한 세부 사항을 제공하는 맵을 반환합니다. 키는 위젯에 제공되는 옵션이며 값은 옵션이 변경될 때마다 호출되는 함수입니다. 위젯은 모든 공통 옵션(제외)에 대한 핸들러를 제공합니다 <code>value</code> 및 <code>displayValue</code>).</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>jQuery 위젯 프레임워크는 jQuery 위젯의 값이 XFA 모델(예: 텍스트 필드의 종료 이벤트)에 저장될 때마다 함수를 로드합니다. 구현은 위젯에 저장된 값을 반환해야 합니다. 처리기에 옵션에 대한 새 값이 제공됩니다.</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>기본적으로 Enter 이벤트 시 XFA에서 <code>rawValue</code> 필드가 표시됩니다. 이 함수는 <code>rawValue</code> 아래와 같이 변경하는 것을 의미합니다. </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>기본적으로 종료 이벤트 시 XFA에서 <code>formattedValue</code> 필드가 표시됩니다. 이 함수는 <code>formattedValue</code> 아래와 같이 변경하는 것을 의미합니다. </td>
  </tr>
 </tbody>
</table>

1. 에서 JavaScript 파일을 업데이트합니다. `integration/javascript` 폴더를 입력합니다(필요에 따라).

   * 텍스트 바꾸기 `__widgetName__` 실제 위젯 이름 사용.
   * 적절한 기본 제공 위젯 클래스에서 위젯을 확장합니다. 대부분의 경우, 대체되는 기존 위젯에 해당하는 위젯 클래스입니다. 상위 클래스 이름은 여러 위치에 사용되므로 문자열의 모든 인스턴스를 검색하는 것이 좋습니다 `xfaWidget.textField` 파일에서 해당 파일을 사용하고 실제 부모 클래스로 바꿉니다.
   * 확장 `render` 대체 UI 제공 방법. UI 또는 상호 작용 동작을 업데이트하기 위해 jQuery 플러그인을 호출할 위치입니다. 다음 `render` 메서드는 사용자 제어 요소를 반환해야 합니다.

   * 확장 `getOptionsMap` 위젯의 변경으로 인해 영향을 받는 모든 옵션 설정을 재정의하는 방법입니다. 함수는 옵션 변경 시 수행할 작업에 대한 세부 사항을 제공하는 매핑을 반환합니다. 키는 위젯에 제공된 옵션이며 값은 옵션이 변경될 때마다 호출되는 함수입니다.
   * 다음 `getEventMap` 메서드는 위젯에 의해 트리거된 이벤트를 적응형 양식 모델에 필요한 이벤트와 함께 매핑합니다. 기본값은 기본 위젯에 대한 표준 HTML 이벤트를 매핑하며, 대체 이벤트가 트리거되는 경우 업데이트해야 합니다.
   * 다음 `showDisplayValue` 및 `showValue` 표시 및 편집 그림 절을 적용하고 대체 동작을 갖도록 대체할 수 있습니다.

   * 다음 `getCommitValue` 메서드는 `commit`이벤트가 발생합니다. 일반적으로 드롭다운, 라디오 단추 및 변경 시 발생하는 확인란 요소를 제외한 종료 이벤트입니다. 자세한 내용은 [적응형 Forms 표현식](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * 템플릿 파일은 다양한 방법에 대한 샘플 구현을 제공합니다. 확장되지 않을 메서드를 제거합니다.

### 클라이언트 라이브러리 만들기 {#create-a-client-library}

Maven Archetype에서 생성한 샘플 프로젝트는 필수 클라이언트 라이브러리를 자동으로 만들고 카테고리가 있는 클라이언트 라이브러리에 래핑합니다 `af.customwidgets`. 에서 사용할 수 있는 JavaScript 및 CSS 파일 `af.customwidgets` 는 런타임에 자동으로 포함됩니다.

### 빌드 및 설치 {#build-and-install}

프로젝트를 빌드하려면 셸에서 다음 명령을 실행하여 AEM 서버에 설치해야 하는 CRX 패키지를 생성합니다.

`mvn clean install`

>[!NOTE]
>
>maven 프로젝트가 POM 파일 내의 원격 저장소를 참조합니다. 이것은 참조용으로만 사용되며 Maven 표준에 따라 저장소 정보가 `settings.xml` 파일.

### 적응형 양식 업데이트 {#update-the-adaptive-form}

사용자 지정 모양을 적응형 양식 필드에 적용하려면:

1. 편집 모드에서 적응형 양식을 엽니다.
1. 를 엽니다. **속성** 사용자 지정 모양을 적용할 필드에 대한 대화 상자입니다.
1. 에서 **스타일링** 탭에서 업데이트를 수행합니다 `CSS class` 속성에 모양새 이름을 추가합니다. `widget_<widgetName>` 형식 지정 예: **widget_numericstepper**

## 샘플: 사용자 정의 모양 만들기   {#sample-create-a-custom-appearance-nbsp}

이제 숫자 필드가 숫자 스테퍼 또는 슬라이더로 표시되는 사용자 지정 모양을 만드는 예를 살펴보겠습니다. 다음 단계를 수행합니다.

1. 다음 명령을 실행하여 Maven 원형 기반의 로컬 프로젝트를 생성합니다.

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   다음 매개 변수에 대한 값을 지정하라는 메시지가 표시됩니다.
   *이 샘플에 사용된 값은 굵게 강조 표시됩니다*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 로 이동합니다 `customWidgets` (지정된 값 `artifactID` property) 디렉토리 및 다음 명령을 실행하여 Eclipse 프로젝트를 생성합니다.

   `mvn eclipse:eclipse`

1. Eclipse 도구를 열고 다음을 수행하여 Eclipse 프로젝트를 가져옵니다.

   1. 선택 **[!UICONTROL 파일 > 가져오기 > 기존 프로젝트를 Workspace로]**.

   1. 을(를) 실행한 폴더를 찾아 선택합니다 `archetype:generate` 명령.

   1. 클릭 **[!UICONTROL 완료]**.

      ![eclipse 스크린샷](assets/eclipse-screenshot.png)

1. 사용자 지정 모양에 사용할 위젯을 선택합니다. 이 샘플은 다음 숫자 스테퍼 위젯을 사용합니다.

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   Eclipse 프로젝트에서 의 플러그인 코드를 검토하십시오 `plugin.js` 파일 을 사용하여 모양새 요구 사항과 일치하도록 합니다. 이 샘플에서 모양은 다음 요구 사항을 충족합니다.

   * 숫자 스테퍼는 다음에서 확장되어야 합니다. `- $.xfaWidget.numericInput`.
   * 다음 `set value` 위젯의 메서드는 포커스가 필드에 있는 후에 값을 설정합니다. 적응형 양식 위젯에 대한 필수 요구 사항입니다.
   * 다음 `render` 메서드를 호출하여 `bootstrapNumber` 메서드를 사용합니다.

   * 플러그인의 기본 소스 코드 외에 플러그인에 대한 추가 종속성이 없습니다.
   * 샘플은 스테퍼에서 스타일을 수행하지 않으므로 추가 CSS가 필요하지 않습니다.
   * 다음 `$userControl` 객체를 사용할 수 있어야 합니다. `render` 메서드를 사용합니다. 필드의 필드입니다 `text` 플러그인 코드로 복제된 유형입니다.

   * 다음 **+** 및 **-** 필드가 비활성화되어 있으면 단추를 비활성화해야 합니다.

1. 의 내용을 바꿉니다 `bootstrap-number-input.js` (jQuery 플러그인) 및 `numericStepper-plugin.js` 파일.
1. 에서 `numericStepper-widget.js` 파일에서 다음 코드를 추가하여 render 메서드를 재정의하여 플러그인을 호출하고 를 반환합니다 `$userControl` 개체:

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. 에서 `numericStepper-widget.js` 파일에서 재정의하십시오. `getOptionsMap` 속성을 사용하여 액세스 옵션을 재정의하고, 비활성화된 모드에서 + 및 - 단추를 숨깁니다.

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. 변경 사항을 저장하고, `pom.xml` 파일을 실행하고 다음 Maven 명령을 실행하여 프로젝트를 빌드합니다.

   `mvn clean install`

1. AEM 패키지 관리자를 사용하여 패키지를 설치합니다.

1. 사용자 지정 모양을 적용할 편집 모드에서 적응형 양식을 열고 다음을 수행합니다.

   1. 모양을 적용할 필드를 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 편집]** 구성 요소 편집 대화 상자를 엽니다.

   1. 스타일 탭에서 **[!UICONTROL CSS 클래스]** 추가할 속성 `widget_numericStepper`.

이제 방금 만든 새 모양을 사용할 수 있습니다.
