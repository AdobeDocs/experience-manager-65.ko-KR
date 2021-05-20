---
title: 적응형 양식 작업을 위한 우수 사례
seo-title: 적응형 양식 작업을 위한 우수 사례
description: AEM Forms 프로젝트 설정, 적응형 양식 개발 및 AEM Forms 시스템용 성능 최적화에 대한 우수 사례를 설명합니다.
seo-description: AEM Forms 프로젝트 설정, 적응형 양식 개발 및 AEM Forms 시스템용 성능 최적화에 대한 우수 사례를 설명합니다.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: 적응형 양식
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4298'
ht-degree: 0%

---

# 적응형 양식 작업을 위한 우수 사례 {#best-practices-for-working-with-adaptive-forms}

## 개요 {#overview}

Adobe Experience Manager (AEM) 양식을 사용하면 복잡한 트랜잭션을 간편하고 쾌적한 디지털 경험으로 변환할 수 있습니다. 그러나 효율적이고 생산적인 AEM Forms 에코시스템을 구현, 빌드, 실행 및 유지 관리하기 위해 공동 노력이 필요합니다.

이 문서에서는 Forms 관리자, 작성자 및 개발자가 AEM Forms, 특히 적응형 양식 구성 요소를 사용하여 작업할 때 활용할 수 있는 지침과 권장 사항을 제공합니다. Forms 개발 프로젝트 설정에서부터 AEM Forms 구성, 사용자 지정, 작성 및 최적화에 이르기까지 Forms에 대한 우수 사례에 대해 설명합니다. 이러한 모범 사례는 AEM Forms 에코시스템의 전반적인 성능에 전체적으로 기여합니다.

또한 일반적인 AEM 우수 사례에 대해 몇 가지 권장 읽기도 있습니다.

* [우수 사례:AEM 배포 및 유지 관리](/help/sites-deploying/best-practices.md)
* [우수 사례:컨텐츠 작성](/help/sites-authoring/best-practices.md)
* [우수 사례:AEM 관리](/help/sites-administering/administer-best-practices.md)
* [우수 사례:솔루션 개발](/help/sites-developing/best-practices.md)

## AEM Forms 설정 및 구성 {#set-up-and-configure-aem-forms}

### 양식 개발 프로젝트 설정 {#setting-up-forms-development-project}

단순화되고 표준화된 프로젝트 구조를 통해 개발 및 유지 관리 노력을 크게 줄일 수 있습니다. Apache Maven은 AEM 프로젝트를 작성하는 데 권장되는 오픈 소스 도구입니다.

* Apache Maven `aem-project-archetype` 을 사용하여 AEM 프로젝트의 구조를 만들고 관리합니다. AEM 프로젝트에 대한 권장 구조 및 템플릿을 만듭니다. 또한 프로젝트를 관리하는 데 도움이 되도록 빌드 자동화 및 변경 제어 시스템을 제공합니다.

   * maven `archetype:generate` 명령을 사용하여 초기 구조를 생성합니다.
   * maven `eclipse:eclipse` 명령을 사용하여 eclipse 프로젝트 파일을 생성하고 프로젝트를 eclipse로 가져옵니다.

자세한 내용은 [Apache Maven](/help/sites-developing/ht-projects-maven.md)을 사용하여 AEM 프로젝트를 작성하는 방법 을 참조하십시오.

* FileVault 도구 또는 VLT는 CRX 또는 AEM 인스턴스의 컨텐츠를 파일 시스템에 매핑하는 데 도움이 됩니다. AEM 프로젝트 콘텐츠 체크인 및 체크아웃 등의 변경 제어 관리 작업을 제공합니다. [VLT 도구 사용 방법](/help/sites-developing/ht-vlttool.md)을 참조하십시오.

* Eclipse 통합 개발 환경을 사용하는 경우 AEM 개발자 도구를 사용하여 AEM 인스턴스와 Eclipse IDE를 원활하게 통합하여 AEM 애플리케이션을 만들 수 있습니다. 자세한 내용은 [Eclipse용 AEM 개발자 도구](/help/sites-developing/aem-eclipse.md)를 참조하십시오.

* /libs 폴더에 내용을 저장하거나 수정하지 마십시오. /app 폴더에 오버레이를 만들어 기본 기능을 확장하거나 덮어씁니다.

* 컨텐츠를 이동할 패키지를 만들 때 패키지 필터 경로가 올바르고 필요한 경로만 언급되어 있는지 확인하십시오.

* /libs 폴더에 내용을 저장하거나 수정하지 마십시오. /app 폴더에 오버레이를 만들어 기본 기능을 확장하거나 덮어씁니다.

* 미리 결정된 설치 순서/순서를 강제 적용할 패키지에 대한 올바른 종속성을 정의합니다.

* /libs 또는 /apps에서 참조할 수 있는 노드를 만들지 마십시오.

### 작성 환경 계획 {#planning-for-authoring-environment}

AEM 프로젝트를 설정하고 나면 적응형 양식 템플릿 및 구성 요소를 작성하고 사용자 지정하는 전략을 정의합니다.

* 적응형 양식 템플릿은 적응형 양식의 구조와 머리글 바닥글 정보를 정의하는 전문 AEM 페이지입니다. 템플릿에는 적응형 양식의 사전 구성된 레이아웃, 스타일 및 기본 구조가 있습니다. AEM Forms은 적응형 양식을 작성하는 데 사용할 수 있는 기본 템플릿 및 구성 요소를 제공합니다. 그러나 요구 사항에 따라 사용자 지정 템플릿 및 구성 요소를 만들 수 있습니다. 적응형 양식에 필요한 추가 템플릿 및 구성 요소에 대한 요구 사항을 수집하는 것이 좋습니다. 자세한 내용은 [적응형 양식 및 구성 요소 사용자 정의](/help/forms/using/adaptive-forms-best-practices.md#customize-components)를 참조하십시오.
* AEM Forms에서는 다음 양식 모델을 기반으로 적응형 양식을 만들 수 있습니다. 양식 모델은 양식과 AEM 시스템 간의 데이터 교환을 위한 인터페이스 역할을 하며 적응형 양식 내/외부에서 데이터 흐름을 위한 XML 기반 구조를 제공합니다. 또한 양식 모델은 스키마 및 XFA 제한 형태로 적응형 양식에 규칙과 제한을 적용합니다.

   * **없음**:이 옵션을 사용하여 만든 적응형 양식에서는 양식 모델을 사용하지 않습니다. 이러한 양식에서 생성된 데이터 XML은 필드 및 해당 값이 있는 플랫 구조를 갖습니다.
   * **XML 또는 JSON 스키마**:XML 및 JSON 스키마는 조직의 백엔드 시스템에서 데이터를 생성하거나 사용하는 구조를 나타냅니다. 스키마를 적응형 양식에 연결하고 해당 요소를 사용하여 적응형 양식에 동적 컨텐츠를 추가할 수 있습니다. 스키마의 요소는 적응형 양식을 작성할 컨텐츠 브라우저의 데이터 모델 개체 탭에서 사용할 수 있습니다. 스키마 요소를 드래그하여 놓아 양식을 작성할 수 있습니다.
   * **XFA 양식 템플릿**:XFA 기반 HTML5 양식에 투자를 하는 경우 이상적인 양식 모델입니다. XFA 기반 양식을 적응형 양식으로 전환하는 직접적인 방법을 제공합니다. 기존 XFA 규칙은 연결된 적응형 양식에 유지됩니다. 결과 적응형 양식은 유효성 검사, 이벤트, 속성 및 패턴과 같은 XFA 구문을 지원합니다.
   * **양식 데이터 모델**:데이터베이스, 웹 서비스 및 AEM 사용자 프로필과 같은 백엔드 시스템을 통합하여 적응형 양식을 미리 작성하고 제출된 양식 데이터를 다시 백엔드 시스템에 기록하려는 경우 기본 양식 모델입니다. 양식 데이터 모델 편집기를 사용하면 적응형 양식을 만드는 데 사용할 수 있는 양식 데이터 모델에서 엔티티와 서비스를 정의하고 구성할 수 있습니다. 자세한 내용은 [AEM Forms 데이터 통합](/help/forms/using/data-integration.md)을 참조하십시오.

요구 사항에 부합할 뿐만 아니라 XFA 및 XSD 자산에 대한 기존 투자를 확장하는 데이터 모델이 있는 경우 신중하게 선택해야 합니다. 생성된 XML에 스키마에 의해 정의된 XPATH에 따라 데이터가 포함되므로 XSD 모델을 사용하여 양식 템플릿을 만드는 것이 좋습니다. 양식 데이터 모델의 기본 선택 항목으로 XSD 모델을 사용하는 것도 데이터를 처리하고 사용하는 백엔드 시스템에서 양식 디자인을 분리하고 양식 필드의 일대일 매핑으로 인해 양식 성능을 개선하기 때문에 도움이 됩니다. 또한 필드의 BindRef를 XML에 있는 해당 데이터 값의 XPATH로 만들 수 있습니다.

자세한 내용은 [적응형 양식 만들기](/help/forms/using/creating-adaptive-form.md)를 참조하십시오.

* 적응형 양식에는 몇 가지 공통 섹션이 있습니다. 이를 식별하고 컨텐츠 재사용 촉진을 위한 전략을 정의할 수 있습니다. 적응형 양식을 사용하면 독립형 조각을 만들고 양식 전체에서 재사용할 수 있습니다. 패널을 적응형 양식에 조각으로 저장할 수도 있습니다. 조각의 모든 변경 사항은 관련 모든 양식에 반영됩니다. 이렇게 하면 작성 시간을 줄이고 양식 간에 일관성을 유지할 수 있습니다. 또한 조각을 사용하면 적응형 양식을 경량화할 수 있으므로 작성 경험이 향상됩니다(특히 큰 양식의 경우). 자세한 내용은 [적응형 양식 조각](/help/forms/using/adaptive-form-fragments.md)을 참조하십시오.

### 적응형 양식 및 구성 요소 사용자 지정 {#customize-components}

* AEM Forms은 적응형 양식을 만드는 데 사용할 수 있는 기본 적응형 양식 템플릿을 제공합니다. 자신만의 템플릿을 만들 수도 있습니다. AEM은 정적 및 편집 가능한 템플릿을 제공합니다.

   * 정적 템플릿은 개발자가 정의하고 구성합니다.
   * 편집 가능한 템플릿은 템플릿 편집기를 사용하여 작성자가 만듭니다. 템플릿 편집기를 사용하면 기본 구조와 초기 컨텐츠를 템플릿에 정의할 수 있습니다. 구조 레이어의 수정 사항은 해당 템플릿을 사용하는 모든 양식에 반영됩니다. 초기 컨텐츠에는 사전 구성된 테마, 미리 채우기 서비스, 제출 작업 등이 포함될 수 있습니다. 그러나 양식 편집기를 사용하여 양식에 대해 이러한 설정을 수정할 수 있습니다. 자세한 내용은 [적응형 양식 템플릿](/help/forms/using/template-editor.md)을 참조하십시오.

* 특정 필드 또는 패널 인스턴스에 스타일을 지정하려면 [인라인 스타일](/help/forms/using/inline-style-adaptive-forms.md)을 사용하십시오. 또는 CSS 파일에서 클래스를 정의하고 구성 요소의 CSS 클래스 속성에 클래스 이름을 지정할 수 있습니다.
* 구성 요소에 클라이언트 라이브러리를 포함하여 해당 구성 요소를 사용하는 적응형 양식 또는 조각에 스타일을 일관되게 적용합니다. 자세한 내용은 [적응형 양식 페이지 구성 요소 만들기](/help/forms/using/custom-adaptive-forms-templates.md)를 참조하십시오.
* 클라이언트 라이브러리에 정의된 스타일을 적용하여 적응형 양식 컨테이너 속성의 CSS 파일 경로 필드에서 클라이언트 라이브러리에 대한 경로를 지정하여 적응형 양식을 선택합니다.
* 스타일의 클라이언트 라이브러리를 만들려면 테마 편집기 기본 clientlib 또는 양식 컨테이너 속성에서 사용자 지정 CSS 파일을 구성할 수 있습니다.
* 적응형 양식은 응답형, 탭, 아코디언 및 마법사와 같은 패널 레이아웃을 제공하여 패널에서 양식 구성 요소를 레이아웃하는 방법을 제어합니다. 사용자 정의 패널 레이아웃을 만들고 양식 작성자가 사용할 수 있도록 만들 수 있습니다. 자세한 내용은 [적응형 양식에 대한 사용자 지정 레이아웃 구성 요소 만들기](/help/forms/using/custom-layout-components-forms.md)를 참조하십시오.
* 필드 및 패널 레이아웃과 같은 특정 적응형 양식 구성 요소를 사용자 지정할 수도 있습니다.

   * 구성 요소의 사본을 수정하려면 AEM의 [오버레이](/help/sites-developing/overlays.md) 기능을 사용하십시오. 기본 구성 요소를 수정하지 않는 것이 좋습니다.
   * /libs에서 바로 사용 가능한 적응형 양식 구성 요소의 레이아웃을 사용자 지정하려면 [사용자 지정 레이아웃 구성 요소](/help/forms/using/custom-layout-components-forms.md) 외에 [기본 레이아웃](/help/forms/using/layout-capabilities-adaptive-forms.md)을 만드십시오.
   * 사용자 지정 위젯 또는 모양을 만들어 사용자 지정 상호 작용을 도입합니다. 기본 구성 요소를 수정하지 않는 것이 좋습니다. 자세한 내용은 [모양 프레임워크](/help/forms/using/introduction-widgets.md)를 참조하십시오.

* PII 데이터 처리에 대한 권장 사항은 [개인 식별 정보 처리](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) 를 참조하십시오.

## 적응형 양식 {#author-adaptive-forms} 작성

### 작성을 위해 터치에 적합한 UI 사용 {#using-touch-optimized-ui-for-authoring}

* 사이드바의 객체 브라우저를 사용하여 양식 계층 구조의 필드에 빠르게 액세스합니다. 검색 상자를 사용하여 폼이나 객체 트리에서 개체를 검색하여 한 객체에서 다른 객체로 이동할 수 있습니다.
* 사이드바의 구성 요소 브라우저에서 구성 요소의 속성을 보고 편집하려면 구성 요소를 선택하고 ![cmppr-1](assets/cmppr-1.png)을 클릭합니다. 구성 요소를 두 번 클릭하여 속성 브라우저에서 해당 속성을 볼 수도 있습니다.
* 키보드 단축키를 사용하여 양식에 빠른 작업을 수행할 수 있습니다. [AEM Forms 키보드 단축키](/help/forms/using/keyboard-shortcuts.md)를 참조하십시오.

* 적응형 양식 구성 요소는 적응형 양식 페이지에서만 사용하는 것이 좋습니다. 구성 요소는 상위 계층에 종속되어 있습니다. 따라서 AEM 페이지에서 이러한 매개 변수를 사용하지 마십시오.

또한 [적응형 양식 작성 소개](/help/forms/using/introduction-forms-authoring.md)에서 구성 요소 설명 및 우수 사례를 참조하십시오.

### 적응형 양식에서 규칙 사용 {#using-rules-in-adaptive-forms}

AEM Forms에서는 적응형 양식 구성 요소에 동적 동작을 추가하는 규칙을 만들 수 있는 [규칙 편집기](/help/forms/using/rule-editor.md)를 제공합니다. 이러한 규칙을 사용하여 조건을 평가하고 필드 표시 또는 숨기기, 값 계산, 드롭다운 목록 동적으로 변경 등과 같은 구성 요소에 대한 작업을 트리거할 수 있습니다.

규칙 편집기는 규칙 작성을 위한 시각적 편집기와 코드 편집기를 제공합니다. 코드 편집기 모드를 사용하여 규칙을 작성할 때에는 다음 사항을 고려하십시오.

* 규칙을 작성하는 동안 발생할 수 있는 충돌을 방지하려면 양식 필드 및 구성 요소에 의미 있고 고유한 이름을 사용하십시오.
* 규칙 표현식에서 해당 구성 요소를 참조하려면 `this` 연산자를 사용하십시오. 이렇게 하면 구성 요소 이름이 변경되더라도 규칙이 유효하게 유지됩니다. 예, `field1.valueCommit script: this.value > 10`.

* 다른 양식 구성 요소를 참조할 때 구성 요소 이름을 사용합니다. `value` 속성을 사용하여 필드나 구성 요소의 값을 가져옵니다. 예, `field1.value`.

* 충돌을 방지하려면 상대적 고유 계층별로 구성 요소를 참조합니다. 예, `parentName.fieldName`.

* 복잡하거나 일반적으로 사용되는 규칙을 처리할 때 적응형 양식 간에 지정하고 재사용할 수 있는 별도의 클라이언트 라이브러리에서 비즈니스 논리를 함수로 쓰는 것이 좋습니다. 클라이언트 라이브러리는 자체 포함된 라이브러리여야 하며 jQuery 및 Underscore.js를 제외하고 외부 종속성이 없어야 합니다. 클라이언트 라이브러리를 사용하여 제출된 양식 데이터의 [서버측 재유효성 검사](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form)를 적용할 수도 있습니다.
* 적응형 양식은 적응형 양식과 통신하고 작업을 수행하는 데 사용할 수 있는 API 세트를 제공합니다. 일부 주요 API는 다음과 같습니다. 자세한 내용은 응용 Forms](https://adobe.com/go/learn_aemforms_documentation_63)에 대한 [JavaScript 라이브러리 API 참조를 참조하십시오.

   * `guideBridge.reset()`:양식을 재설정합니다.
   * `guideBridge.submit()`:양식을 제출합니다.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`:포커스를 필드에 설정합니다.
   * `guideBridge.validate(errorList, somExpression, focus)`:양식의 유효성을 검사합니다.
   * `guideBridge.getDataXML(options)`:양식 데이터를 XML로 가져옵니다.
   * `guideBridge.resolveNode(somExpression)`:양식 개체를 가져옵니다.
   * `guideBridge.setProperty(somList, propertyName, valueList)`:양식 개체의 속성을 설정합니다.
   * 또한 다음 필드 속성을 사용할 수 있습니다.

      * `field.value` 필드의 값을 변경하려면 다음을 수행하십시오.
      * f `ield.enabled` 을 클릭하여 필드를 활성화/비활성화합니다.
      * `field.visible` 필드의 표시 여부를 변경하려면 다음을 수행하십시오.

* 적응형 양식 작성자는 비즈니스 논리를 양식에 작성하기 위해 JavaScript 코드를 작성해야 할 수 있습니다. JavaScript는 강력하고 효과적이지만, 보안 기대치를 손상시킬 수 있습니다. 따라서 양식을 프로덕션에 넣기 전에 양식 작성자가 신뢰할 수 있는 인물이고 JavaScript 코드를 검토하고 승인하는 프로세스가 있는지 확인해야 합니다. 관리자는 역할 또는 기능을 기반으로 사용자 그룹에 대한 규칙 편집기 액세스 권한을 제한할 수 있습니다. 사용자 그룹을 선택하려면 [규칙 편집기 액세스 권한 부여](/help/forms/using/rule-editor-access-user-groups.md)를 참조하십시오.
* 규칙의 표현식을 사용하여 적응형 양식을 동적으로 만들 수 있습니다. 모든 표현식은 유효한 JavaScript 표현식이며, 적응형 양식 스크립팅 모델 API를 사용합니다. 이러한 표현식은 특정 유형의 값을 반환합니다. 표현식 및 그에 대한 우수 사례에 대한 자세한 내용은 [적응형 양식 표현식](/help/forms/using/adaptive-form-expressions.md)을 참조하십시오.

### 테마 작업 {#working-with-themes}

테마에 적응형 을 사용하면 일관된 모양과 스타일을 위해 여러 양식에 적용할 수 있는 재사용 가능한 스타일을 만들 수 있습니다. 양식 구성 요소 및 패널에 대한 스타일을 정의하려면 테마 를 사용하는 것이 좋습니다. 테마에 대한 일부 우수 사례는 다음과 같습니다.

* 텍스트 스타일, 배경 및 이미지를 빠르게 적용할 수 있도록 자산 라이브러리를 사용합니다. 자산 라이브러리에 스타일을 추가하면 다른 테마 및 양식 편집기의 스타일 모드에서 사용할 수 있습니다.
* 페이지 수준 선택기를 사용하여 글꼴 및 페이지 배경과 같은 전역 설정을 적용합니다.
* 클라이언트 라이브러리를 사용하여 기존 또는 고급 스타일을 테마로 가져옵니다.
* 양식 스타일 레이어에서 특정 필드, 패널 또는 단추의 스타일을 재정의할 수 있습니다.
* 테마가 스타일링 요구 사항을 충족하지 않는 경우 guideFieldNode, guideFieldLabel, guideFieldWidget 및 guidePanelNode와 같은 사전 정의된 클래스를 사용하여 양식에 공통 스타일을 적용할 수 있습니다.

자세한 내용은 [테마](/help/forms/using/themes.md)를 참조하십시오.

### 크고 복잡한 양식의 성능 최적화 {#optimizing-performance-of-large-and-complex-forms}

양식 작성자 및 최종 사용자는 일반적으로 작성 모드나 런타임 시 큰 양식을 로드할 때 성능 문제가 발생합니다. 양식의 개체 수(필드 및 패널)가 늘어나면 작성 및 런타임 경험이 저하되기 시작합니다. 또한 여러 작성자가 동시에 양식을 공동 작업하고 작성할 수 없습니다.

큰 양식의 성능 문제를 해결하려면 다음 모범 사례를 고려하십시오.

* XFA를 적응형 양식으로 전환할 때에도 XSD 양식 데이터 모델을 사용하여 적응형 양식을 만드는 것이 좋습니다.
* 사용자의 정보를 캡처하는 적응형 양식에 이러한 필드와 패널만 포함하십시오. 정적 콘텐츠를 최소한으로 유지하거나 URL을 사용하여 별도의 창에서 여는 것이 좋습니다.
* 모든 양식은 특정 용도로 디자인되지만, 대부분의 양식에는 몇 가지 공통 세그먼트가 있습니다. 예를 들어, 개인 세부 사항, 주소, 고용 세부 사항 등이 있습니다. 공통 양식 요소 및 섹션에 대해 [적응형 양식 조각](/help/forms/using/adaptive-form-fragments.md)을 만들고 양식에서 사용합니다. 기존 양식의 패널을 조각으로 저장할 수도 있습니다. 조각의 모든 변경 사항은 연관된 모든 적응형 양식에 반영됩니다. 여러 작성자가 양식을 구성하는 서로 다른 조각에서 동시에 작업할 수 있으므로 공동 작성을 촉진합니다.

   * 적응형 양식과 유사하게 모든 조각 관련 스타일 및 사용자 지정 스크립트가 조각 컨테이너 대화 상자를 사용하여 클라이언트 라이브러리에 정의된 것이 좋습니다. 또한 외부 객체에 의존하지 않는 자족적 조각을 만들어 보십시오.
   * 교차 조각 스크립팅을 사용하지 마십시오. 참조하는 조각 외부에 개체가 있는 경우 해당 개체를 상위 양식의 일부로 만들려고 합니다. 개체가 여전히 다른 조각에 있어야 하는 경우 스크립트에서 해당 이름으로 참조합니다.

* 자동 저장으로 저장 및 다시 시작 을 사용하여 적응형 양식을 주기적으로 저장하고 사용자가 나중에 다시 방문하여 양식을 완료할 수 있도록 하십시오.
* 지연을 로드하도록 조각을 구성합니다. 런타임 시 느리게 로드되도록 표시된 조각이 필요한 경우에만 렌더링됩니다. 큰 양식의 로드 시간을 크게 줄입니다. 반복 가능한 패널이 있는 조각에서도 지원됩니다. 자세한 내용은 [지연 로드 구성](/help/forms/using/lazy-loading-adaptive-forms.md)을 참조하십시오.

   * 응답형 격자 레이아웃 또는 첫 번째 패널에서 조각에 대한 레이지 로드를 구성하지 마십시오.
   * 파일 첨부 파일 및 약관 구성 요소는 느리게 로드된 조각에서 지원되지 않습니다.
   * 지연 로드 패널의 값을 포함 패널을 언로드할 때 해당 값을 사용할 수 있도록 양식의 다른 부분에서 이 값을 사용할 경우 값 전역적으로 사용 으로 표시합니다.
   * 조건을 기반으로 표시하거나 숨겨야 하는 조각에 대한 가시성 규칙 작성을 고려하십시오.

### 적응형 양식 미리 채우기 {#prefilling-adaptive-forms}

백엔드에서 가져온 데이터로 적응형 양식 필드를 미리 채우면 사용자가 양식을 빠르게 채우고 입력 오류가 발생하지 않도록 할 수 있습니다.

* AEM Forms은 사전 정의된 데이터 XML 파일에서 데이터를 읽고 적응형 양식의 필드를 미리 채우기 XML 파일의 컨텐츠로 미리 채우기 위한 미리 채우기 서비스를 제공합니다.
* 미리 채우기 데이터 XML은 적응형 양식과 연결된 양식 모델의 스키마와 호환되어야 합니다.
* 미리 채우기 XML에 `afBoundedData` 및 `afUnBoundedData` 섹션을 포함시켜 적응형 양식의 바인딩되지 않은 필드와 필드를 모두 미리 채웁니다.

* 양식 데이터 모델을 기반으로 하는 적응형 양식의 경우 AEM Forms에서는 기본 양식 데이터 모델 미리 채우기 서비스를 제공합니다. 미리 채우기 서비스는 적응형 양식의 데이터 모델 개체에 대한 데이터 소스를 쿼리하고 양식을 렌더링할 때 필드 값을 미리 채웁니다.
* 파일, crx, 서비스 또는 http 프로토콜을 사용하여 적응형 양식을 미리 채울 수도 있습니다.
* AEM Forms은 적응형 양식을 미리 채우기 위해 OSGi 서비스로 로그인할 수 있는 사용자 지정 미리 채우기 서비스를 지원합니다.

자세한 내용은 [적응형 양식 필드 미리 채우기](/help/forms/using/prepopulate-adaptive-form-fields.md)를 참조하십시오.

### 적응형 양식 서명 및 제출 {#signing-and-submitting-adaptive-forms}

적응형 양식에서는 사용자가 지정한 데이터를 처리하려면 제출 작업이 필요합니다. 제출 작업은 적응형 양식을 사용하여 제출하는 데이터에 대해 수행되는 작업을 결정합니다.

* 적응형 양식에는 즉시 사용할 수 있는 몇 가지 제출 작업이 있습니다. 자세한 내용은 [제출 작업 구성](/help/forms/using/configuring-submit-actions.md)을 참조하십시오.
* 기본 제출 작업이 사용 사례를 충족하지 않는 경우 사용자 지정 제출 작업을 작성할 수 있습니다. 자세한 내용은 적응형 양식에 대한 사용자 지정 제출 작업 쓰기](/help/forms/using/custom-submit-action-form.md)를 참조하십시오.[
* 잘못된 데이터 제출을 방지하기 위해 서버측 유효성 검사를 포함합니다.

적응형 양식에서 Adobe Sign의 다중 서명 경험을 활용할 수 있습니다. 적응형 양식에서 Adobe Sign을 구성할 때 다음 사항을 고려하십시오. 자세한 내용은 적응형 양식](/help/forms/using/working-with-adobe-sign.md)에서 Adobe Sign 사용 을 참조하십시오.[

* Adobe Sign이 활성화된 적응형 양식은 모든 서명자가 양식에 서명한 후에만 제출됩니다. 모든 서명자가 양식을 서명할 때까지 Forms이 보류 중인 서명 상태로 나타납니다.
* 제출 시 양식 서명 경험을 구성하거나 서명자를 서명 페이지로 리디렉션할 수 있습니다.
* 필요에 따라 순차적 또는 병렬 서명 경험을 구성합니다.

### 레코드 {#generating-document-of-record} 문서를 생성하는 중

레코드 문서(DoR)는 인쇄, 서명 또는 보관할 수 있는 적응형 양식의 병합된 PDF 버전입니다.

* 적응형 양식의 기반이 되는 양식 데이터 모델에 따라 다음과 같이 DoR에 대한 템플릿을 구성할 수 있습니다.

   * **XFA 양식 템플릿**:연결된 XDP 파일을 DoR 템플릿으로 사용합니다.
   * **XSD 스키마**:적응형 양식에서 사용하는 것과 동일한 XML 스키마를 사용하는 관련 XFA 템플릿을 사용합니다.
   * **없음**:자동 생성된 DoR을 사용합니다.

* 적응형 양식 편집기의 레코드 문서 탭에서 머리글, 바닥글, 이미지, 색상, 글꼴 등을 바로 구성합니다.
* 프로그래밍 방식으로 DoR을 생성하려면 `DoRService` 를 사용하십시오.
* DoR에서 숨김 필드를 제외합니다.
* 다른 로케일에서 `afAcceptLang` 요청 매개 변수를 사용하여 DoR을 봅니다.

### 적응형 양식 디버깅 및 테스트 {#debugging-and-testing-adaptive-forms}

[AEM Chrome 플러그인](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) 은 적응형 양식을 디버깅하는 도구를 제공하는 Google Chrome용 브라우저 확장입니다. 양식 작성자 및 개발자는 다음 도구를 사용하여 다음을 수행할 수 있습니다.

* 병목 현상 파악 및 양식 렌더링 성능 최적화
* 폼의 키워드 및 bindRef 오류 디버깅
* 로그 활성화 및 구성
* 양식에서 디버그 규칙 및 스크립트
* 안내서 Bridge API에 대한 탐색 및 학습

자세한 내용은 [AEM Chrome 플러그인 - 적응형 양식](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)을 참조하십시오.

Calvin SDK는 응용 Forms 개발자가 응용 Forms을 테스트할 수 있는 유틸리티 API입니다. Calvin SDK는 [Hobbes.js 테스트 프레임워크](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html) 맨 위에 빌드되어 있습니다. 프레임워크를 사용하여 다음을 테스트할 수 있습니다.

* 적응형 양식의 표현물 경험
* 적응형 양식의 미리 채우기 경험
* 적응형 양식의 경험 제출
* 표현식 규칙
* 유효성 검사
* 지연 로드

자세한 내용은 [적응형 양식 테스트 자동화](/help/forms/using/calvin.md)를 참조하십시오.

### AEM 서버에서 적응형 양식 유효성 검사 {#validating-adaptive-forms-on-aem-server}

클라이언트에서의 유효성 검사를 무시하려는 시도와 데이터 제출 및 비즈니스 규칙 위반의 가능한 손상을 방지하기 위해 서버측 유효성 검사가 필요합니다. 서버측 유효성 검사는 필요한 클라이언트 라이브러리를 로드하여 서버에서 실행됩니다.

* 적응형 양식의 표현식의 유효성을 검사하는 클라이언트 라이브러리에 함수를 포함하고 적응형 양식 컨테이너 대화 상자에서 클라이언트 라이브러리를 지정합니다. 자세한 내용은 [서버측 재유효성 검사](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p)를 참조하십시오.
* 서버측 유효성 검사는 양식 모델의 유효성을 검사합니다. 유효성 검사를 위해 별도의 클라이언트 라이브러리를 만들고 동일한 클라이언트 라이브러리에서 HTML 스타일 및 DOM 조작과 같은 다른 항목과 혼합하지 않는 것이 좋습니다.

### 적응형 양식 현지화 {#localizing-adaptive-forms}

AEM에서는 적응형 양식을 현지화하는 데 사용할 수 있는 번역 워크플로우를 제공합니다. 자세한 내용은 [AEM 번역 워크플로우를 사용하여 적응형 양식 현지화](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)를 참조하십시오.

적응형 양식을 현지화할 때의 몇 가지 우수 사례는 다음과 같습니다.

* 양식에서 일반적인 요소에 적용형 양식 조각을 사용하고 조각을 현지화합니다. 조각을 한 번 현지화하면 현지화된 조각이 사용되는 모든 양식에 반영됩니다.
* 새 구성 요소 추가 또는 현지화된 양식의 스크립트 적용과 같은 수정 사항은 자동으로 현지화되지 않습니다. 따라서 현지화 주기를 여러 번 사용하지 않으려면 양식을 현지화하기 전에 완료해야 합니다.
* `afAcceptLang` 요청 매개 변수를 사용하여 브라우저 로케일을 재정의하고 지정된 로케일에서 양식을 렌더링합니다. 예를 들어 다음 URL은 브라우저 설정에 지정된 로케일에 관계없이 일본어 로케일로 양식을 렌더링합니다.

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms은 현재 영어(en), 스페인어(es), 프랑스어(fr), 이탈리아어(it), 독일어(de), 일본어(ja), 포르투갈어(pt-BR), 중국어(zh-CN), 중국어(zh-TW) 및 한국어(ko-KR) 로케일로 적응형 양식 컨텐츠의 지역화를 지원합니다. 그러나 런타임 시 적응형 양식에 대한 새 로케일 지원을 추가할 수 있습니다. 자세한 내용은 [적응형 양식 현지화를 위한 새 로케일 지원](/help/forms/using/supporting-new-language-localization.md)을 참조하십시오.

## 프로덕션 {#prepare-forms-project-for-production} 양식 프로젝트 준비

### 양식 처리 서버 {#adding-forms-processing-server} 추가

보안 영역의 방화벽 뒤에 있는 AEM Forms 서버의 추가 인스턴스를 구성할 수 있습니다. 이 인스턴스는에 사용할 수 있습니다.

* **일괄 처리**:로드가 많은 배치에서 반복되거나 예약된 작업입니다. 예를 들어, 인쇄 문을 생성하고, PDF 생성기, 출력 및 어셈블러와 같은 문서 서비스를 생성합니다.
* **PII 데이터 저장**:처리 서버에 PII 데이터를 저장합니다. PII 데이터를 저장하기 위해 이미 사용자 지정 저장소 공급자를 사용하는 경우에는 필요하지 않습니다.

### 프로젝트를 다른 환경 {#moving-project-to-another-environment}으로 이동

AEM 프로젝트를 한 환경에서 다른 환경으로 이동해야 하는 경우가 많습니다. 이동할 때 기억해야 할 주요 사항 중 일부는 다음과 같습니다.

* 기존 클라이언트 라이브러리, 사용자 지정 코드 및 구성을 백업합니다.
* 새 환경에서 지정된 순서로 제품 패키지 및 패치를 수동으로 배포합니다.
* 프로젝트별 코드 패키지 및 번들을 수동으로 그리고 새 AEM 서버에 별도의 패키지 또는 번들로 배포합니다.
* (*JEE의 AEM Forms만*) Forms Workflow 서버에 LCA 및 DSC를 수동으로 배포합니다.
* [Export-Import](/help/forms/using/import-export-forms-templates.md) 기능을 사용하여 자산을 새 환경으로 이동합니다. 복제 에이전트를 구성하고 자산을 게시할 수도 있습니다.
* 업그레이드할 때 더 이상 사용되지 않는 모든 API 및 기능을 새 API 및 기능으로 바꾸십시오.

### AEM {#configuring-aem} 구성

전체 성능을 개선하기 위해 AEM을 구성하는 몇 가지 우수 사례는 다음과 같습니다.

* Felix 콘솔에서 JavaScript 및 CSS용 HTML 클라이언트 라이브러리 압축을 활성화합니다. [예제](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)로 설명되는 Clientlibs 를 참조하십시오.
* 모든 클라이언트 라이브러리를 `/etc.clientlibs/fd` 및 AEM Dispatcher의 추가 사용자 지정 클라이언트 라이브러리를 캐시하여 게시된 양식의 응답성과 보안을 높입니다. 자세한 내용은 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 를 참조하십시오.

* `/content/forms/af/` 및 `/content/dam/formsanddocuments/*` 경로를 캐시하지 마십시오. 적응형 양식 캐싱 구성에 대한 자세한 내용은 [적응형 양식 캐싱](/help/forms/using/configure-adaptive-forms-cache.md)을 참조하십시오.

* 웹 서버 압축 모듈을 통해 HTML을 활성화합니다. 자세한 내용은 [AEM Forms 서버의 성능 조정](/help/forms/using/performance-tuning-aem-forms.md)을 참조하십시오.
* 큰 양식에 대한 요청당 호출 수를 늘립니다. [크고 복잡한 양식의 성능 최적화](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms)를 참조하십시오.
* 오류 처리기에 표시된 [사용자 지정 오류 페이지를 만듭니다](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html).
* 보안 AEM Forms 서버.

   * 프로덕션 서버에 배포된 샘플 컨텐츠 및 샘플 사용자가 없는지 확인하려면 `nosamplecontent` 실행 모드를 사용하십시오. [프로덕션 준비 모드에서 AEM 실행](/help/sites-administering/production-ready.md)을 참조하십시오.

* 힙의 크기를 최소 8GB로 유지합니다. 다른 설정에 대해서는 [AEM Forms 서버의 성능 조정](/help/forms/using/performance-tuning-aem-forms.md)을 참조하십시오.
* 서비스 수준 작업을 실행하려면 관리자 세션 대신 서비스 사용자 세션을 사용합니다. 자세한 내용은 [서비스 인증](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html)을 참조하십시오.

>[!VIDEO](https://vimeo.com/)

### 초안 및 제출된 양식 데이터에 대한 외부 저장소 구성 {#external-storage}

프로덕션 환경에서는 제출된 양식 데이터를 AEM 저장소에 저장하지 않는 것이 좋습니다. Forms Portal 저장, 컨텐츠 저장 및 PDF 저장 제출 작업의 기본 구현은 양식 데이터를 AEM 저장소에 저장합니다. 이러한 제출 작업은 데모 용도로만 사용됩니다. 또한 저장 및 재개 및 자동 저장 기능은 기본적으로 포털 저장소를 사용합니다. 따라서 다음 권장 사항을 고려하십시오.

* **초안 데이터 저장**:적응형 양식의 초안 기능을 사용하는 경우 SPI(사용자 지정 서비스 제공 인터페이스)를 구현하여 초안 데이터를 데이터베이스와 같은 보다 안전한 저장소에 저장해야 합니다. 자세한 내용은 [초안 및 제출 구성 요소를 데이터베이스](/help/forms/using/integrate-draft-submission-database.md)와 통합하기 위한 샘플을 참조하십시오.

* **제출 데이터 저장**:Form Portal 제출 저장소를 사용하는 경우 사용자 지정 SPI를 구현하여 제출 데이터를 데이터베이스에 저장해야 합니다. 샘플 통합에 대해서는 [초안 및 제출 구성 요소와 데이터베이스](/help/forms/using/integrate-draft-submission-database.md)를 통합하려면 샘플을 참조하십시오.

   또한 양식 데이터와 첨부 파일을 보안 저장소에 저장하는 사용자 지정 제출 작업을 작성할 수 있습니다. 자세한 내용은 [적응형 양식에 대한 사용자 지정 제출 작업 쓰기](/help/forms/using/custom-submit-action-form.md)를 참조하십시오.

* **초안 ID 길이**:적응형 양식을 초안으로 저장하면 초안 ID가 생성되어 초안을 고유하게 식별합니다. 초안 ID 필드 길이의 최소값은 26자입니다. Adobe은 초안 ID 길이를 26자 이상으로 설정하는 것이 좋습니다.

### 개인 식별 정보 처리 {#handling-personally-identifiable-information}

조직의 주요 문제 중 하나는 개인 식별(PII) 데이터를 처리하는 방법입니다. 이러한 데이터를 처리하는 데 도움이 되는 몇 가지 모범 사례는 다음과 같습니다.

* 데이터베이스와 같은 안전한 외부 저장소를 사용하여 초안 및 제출된 양식의 데이터를 저장합니다. [초안 및 제출된 양식 데이터에 대한 외부 저장소 구성](/help/forms/using/adaptive-forms-best-practices.md#external-storage)을 참조하십시오.
* 자동 저장을 활성화하기 전에 사용자의 명시적 동의를 받으려면 약관 양식 구성 요소를 사용하십시오. 이 경우 사용자가 약관 구성 요소의 조건에 동의하는 경우에만 자동 저장을 활성화합니다.
