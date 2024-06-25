---
title: 적응형 양식 작업 모범 사례
description: AEM Forms 프로젝트 설정, 적응형 양식 개발 및 AEM Forms 시스템 성능 최적화를 위한 모범 사례에 대해 설명합니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components,Core Components
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '5538'
ht-degree: 1%

---

# 적응형 양식 작업 모범 사례 {#best-practices-for-working-with-adaptive-forms}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

## 개요 {#overview}

Adobe Experience Manager(AEM) forms를 사용하면 복잡한 트랜잭션을 간단하고 즐거운 디지털 경험으로 변환할 수 있습니다. 그러나 효율적이고 생산적인 AEM Forms 에코시스템을 구현, 빌드, 실행 및 유지 관리하는 데 있어 일치된 노력이 필요합니다.

이 문서에서는 양식 관리자, 작성자 및 개발자가 AEM Forms, 특히 적응형 양식 구성 요소로 작업할 때 유용하게 사용할 수 있는 지침과 권장 사항을 제공합니다. 이 비디오에서는 양식 개발 프로젝트 설정에서 AEM Forms 구성, 사용자 정의, 작성 및 최적화에 대한 모범 사례에 대해 설명합니다. 이러한 모범 사례는 전체적으로 AEM Forms 생태계의 전체 성능에 기여합니다.

또한 일반 AEM 우수 사례에 대한 몇 가지 권장 읽기는 다음과 같습니다.

* [우수 사례: AEM 배포 및 유지 관리](/help/sites-deploying/best-practices.md)
* [모범 사례: 콘텐츠 작성](/help/sites-authoring/best-practices.md)
* [우수 사례: AEM 관리](/help/sites-administering/administer-best-practices.md)
* [모범 사례: 솔루션 개발](/help/sites-developing/best-practices.md)

## AEM Forms 설정 및 구성 {#set-up-and-configure-aem-forms}

### 양식 개발 프로젝트 설정 {#setting-up-forms-development-project}

단순화되고 표준화된 프로젝트 구조는 개발 및 유지 관리 노력을 크게 줄일 수 있다. Apache Maven은 AEM 프로젝트 구축에 권장되는 오픈 소스 도구입니다.

* Apache Maven 사용 `aem-project-archetype` AEM 프로젝트에 대한 구조를 만들고 관리합니다. AEM 프로젝트에 대한 권장 구조 및 템플릿을 만듭니다. 또한 빌드 자동화 및 변경 제어 시스템을 제공하여 프로젝트 관리를 돕습니다.

   * Maven 사용 `archetype:generate` 초기 구조를 생성하는 명령입니다.
   * Maven 사용 `eclipse:eclipse` eclipse 프로젝트 파일을 생성하고 프로젝트를 eclipse로 가져오는 명령.

자세한 내용은 [Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법](/help/sites-developing/ht-projects-maven.md).

* FileVault 도구 또는 VLT를 사용하면 CRX 또는 AEM 인스턴스의 콘텐츠를 파일 시스템에 매핑할 수 있습니다. AEM 프로젝트 콘텐츠 체크인 및 체크아웃 등 변경 제어 관리 작업을 제공합니다. 다음을 참조하십시오 [VLT 도구 사용 방법](/help/sites-developing/ht-vlttool.md).

* Eclipse 통합 개발 환경을 사용하는 경우 AEM 개발자 도구를 사용하여 Eclipse IDE와 AEM 인스턴스를 원활하게 통합하여 AEM 애플리케이션을 만들 수 있습니다. 자세한 내용은 [Eclipse용 AEM 개발자 도구](/help/sites-developing/aem-eclipse.md).

* /libs 폴더에 컨텐츠를 저장하거나 수정하지 마십시오. /app 폴더에 오버레이를 만들어 기본 기능을 확장하거나 덮어씁니다.

* 콘텐츠를 이동하는 패키지를 만들 때 패키지 필터 경로가 올바르고 필수 경로만 언급되었는지 확인하십시오.

* /libs 폴더에 컨텐츠를 저장하거나 수정하지 마십시오. /app 폴더에 오버레이를 만들어 기본 기능을 확장하거나 덮어씁니다.

* 패키지에 대한 올바른 종속성을 정의하여 사전 결정된 설치 순서/시퀀스를 적용합니다.

* /libs 또는 /apps에 참조 가능한 노드를 만들지 마십시오.

### 작성 환경 계획 {#planning-for-authoring-environment}

AEM 프로젝트를 설정하고 나면 적응형 양식 템플릿 및 구성 요소를 작성하고 사용자 지정하는 전략을 정의합니다.

* 적응형 양식 템플릿은 적응형 양식의 구조 및 머리글-바닥글 정보를 정의하는 전문 AEM 페이지입니다. 템플릿에는 적응형 양식에 대해 미리 구성된 레이아웃, 스타일 및 기본 구조가 있습니다. AEM Forms은 적응형 양식을 작성하는 데 사용할 수 있는 기본 템플릿 및 구성 요소를 제공합니다. 하지만 요구 사항에 따라 사용자 정의 템플릿과 구성 요소를 만들 수 있습니다. 적응형 양식에 필요한 추가 템플릿 및 구성 요소에 대한 요구 사항을 수집하는 것이 좋습니다. 자세한 내용은 [적응형 양식 및 구성 요소 사용자 지정](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* CRX 패키지 관리자를 통해 패키지를 업로드하면 경우에 따라 이상이 발생할 수 있으므로 CRX 패키지 관리자 사용자 인터페이스 대신 양식 관리자 사용자 인터페이스를 사용하여 양식 패키지를 업로드하는 것이 좋습니다.
* AEM Forms을 사용하면 다음 양식 모델을 기반으로 적응형 양식을 만들 수 있습니다. 양식 모델은 양식과 AEM 시스템 간의 데이터 교환을 위한 인터페이스 역할을 하며 적응형 양식 내/외부의 데이터 흐름을 위한 XML 기반 구조를 제공합니다. 또한 양식 모델은 스키마 및 XFA 제한 사항의 형태로 적응형 양식에 규칙과 제한을 부과합니다.

   * **없음**: 이 옵션을 사용하여 만든 적응형 양식은 양식 모델을 사용하지 않습니다. 해당 양식에서 생성된 데이터 XML에는 필드와 해당 값이 포함된 기본 구조가 있습니다.
   * **XML 또는 JSON 스키마**: XML 및 JSON 스키마는 조직의 백엔드 시스템이 데이터를 생성하거나 사용하는 구조를 나타냅니다. 스키마를 적응형 양식에 연결하고 해당 요소를 사용하여 적응형 양식에 다이내믹 콘텐츠를 추가할 수 있습니다. 스키마의 요소는 적응형 양식을 작성하는 콘텐츠 브라우저의 데이터 모델 개체 탭에서 사용할 수 있습니다. 스키마 요소를 끌어 놓아 양식을 작성할 수 있습니다.
   * **XFA 양식 템플릿**: XFA 기반 HTML5 양식에 투자한 경우 이상적인 양식 모델입니다. XFA 기반 양식을 적응형 양식으로 전환하는 직접적인 방법을 제공합니다. 기존 XFA 규칙은 연결된 적응형 양식에 유지됩니다. 결과 적응형 양식은 유효성 검사, 이벤트, 속성 및 패턴과 같은 XFA 구문을 지원합니다.
   * **양식 데이터 모델**: 데이터베이스, 웹 서비스 및 AEM 사용자 프로필과 같은 백엔드 시스템을 통합하여 적응형 양식을 미리 채우고 제출된 양식 데이터를 백엔드 시스템에 다시 작성하려는 경우 선호되는 양식 모델입니다. 양식 데이터 모델 편집기를 사용하면 적응형 양식을 만드는 데 사용할 수 있는 양식 데이터 모델에서 엔티티 및 서비스를 정의하고 구성할 수 있습니다. 자세한 내용은 [AEM Forms 데이터 통합](/help/forms/using/data-integration.md).

요구 사항에 적합할 뿐만 아니라 XFA 및 XSD 자산(있는 경우)에 대한 기존 투자를 확장하는 데이터 모델을 신중하게 선택하는 것이 중요합니다. 생성된 XML에 스키마에 의해 정의된 XPATH에 따른 데이터가 포함되어 있으므로 XSD 모델을 사용하여 양식 템플릿을 만듭니다. 또한 XSD 모델을 양식 데이터 모델의 기본 옵션으로 사용하면 데이터를 처리하고 사용하는 백엔드 시스템과 양식 디자인을 분리하고 양식 필드의 일대일 매핑으로 인해 양식의 성능을 향상시킬 수 있습니다. 또한 필드의 BindRef를 XML로 해당 데이터 값의 XPATH로 만들 수 있습니다.

자세한 내용은 [적응형 양식 만들기](/help/forms/using/creating-adaptive-form.md).

* 적응형 양식에는 몇 가지 공통 섹션이 있습니다. 이를 식별하고 콘텐츠 재사용을 촉진하는 전략을 정의할 수 있습니다. 적응형 양식을 사용하면 독립 실행형 조각을 만들어 양식 간에 재사용할 수 있습니다. 패널을 적응형 양식에 조각으로 저장할 수도 있습니다. 조각의 모든 변경 사항은 연결된 모든 양식에 반영됩니다. 작성 시간을 줄이고 양식 간에 일관성을 유지하는 데 도움이 됩니다. 또한 조각을 사용하면 적응형 양식이 간소화되어 특히 대형 양식의 작성 경험이 향상됩니다. 자세한 내용은 [적응형 양식 단편](/help/forms/using/adaptive-form-fragments.md).

### 적응형 양식 및 구성 요소 사용자 지정 {#customize-components}

* AEM Forms은 적응형 양식을 만드는 데 사용할 수 있는 기본 적응형 양식 템플릿을 제공합니다. 자신만의 템플릿을 만들 수도 있습니다. AEM은 정적 및 편집 가능한 템플릿을 제공합니다.

   * 정적 템플릿은 개발자가 정의하고 구성합니다.
   * 편집 가능한 템플릿은 작성자가 템플릿 편집기를 사용하여 만듭니다. 템플릿 편집기 를 사용하여 템플릿의 기본 구조와 초기 콘텐츠를 정의할 수 있습니다. 구조 레이어의 수정 사항은 해당 템플릿을 사용하는 모든 양식에 반영됩니다. 초기 콘텐츠는 사전 구성된 테마, 미리 채우기 서비스, 제출 액션 등을 포함할 수 있다. 그러나 양식 편집기를 사용하여 양식에 대해 이러한 설정을 수정할 수 있습니다. 자세한 내용은 [적응형 양식 템플릿](/help/forms/using/template-editor.md).

* 특정 필드 또는 패널 인스턴스의 스타일을 지정하려면 [인라인 스타일 지정](/help/forms/using/inline-style-adaptive-forms.md). 또는 CSS 파일에서 클래스를 정의하고 구성 요소의 CSS Class 속성에서 클래스 이름을 지정할 수 있습니다.
* 구성 요소에 클라이언트 라이브러리를 포함하여 해당 구성 요소를 사용하는 적응형 양식 또는 조각에 스타일을 일관되게 적용할 수 있습니다. 자세한 내용은 [적응형 양식 페이지 구성 요소 만들기](/help/forms/using/custom-adaptive-forms-templates.md).
* 클라이언트 라이브러리에 정의된 스타일을 적용하여 적응형 양식 컨테이너 속성의 CSS 파일 경로 필드에 있는 클라이언트 라이브러리의 경로를 지정하여 적응형 양식을 선택합니다.
* 스타일의 클라이언트 라이브러리를 만들려면 테마 편집기 기본 clientlib 또는 양식 컨테이너 속성에서 사용자 지정 CSS 파일을 구성할 수 있습니다.
* 적응형 양식은 반응형, 탭, 아코디언 및 마법사와 같은 패널 레이아웃을 제공하여 패널에서 양식 구성 요소가 배치되는 방식을 제어합니다. 사용자 정의 패널 레이아웃을 만들어 양식 작성자가 사용할 수 있도록 할 수 있습니다. 자세한 내용은 [적응형 양식을 위한 사용자 정의 레이아웃 구성 요소 만들기](/help/forms/using/custom-layout-components-forms.md).
* 필드 및 패널 레이아웃과 같은 특정 적응형 양식 구성 요소를 사용자 지정할 수도 있습니다.

   * 사용 [오버레이](/help/sites-developing/overlays.md) 구성 요소 사본을 수정하는 AEM 기능입니다. 기본 구성 요소는 수정하지 않는 것이 좋습니다.
   * /libs에서 즉시 사용 가능한 적응형 양식 구성 요소의 레이아웃을 사용자 지정하려면 [사용자 지정 레이아웃 구성 요소 만들기](/help/forms/using/custom-layout-components-forms.md) 및 [기본 레이아웃](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * 사용자 정의 위젯 또는 모양을 만들어 사용자 정의 상호 작용을 소개합니다. 기본 구성 요소는 수정하지 않는 것이 좋습니다. 자세한 내용은 [모양 프레임워크](/help/forms/using/introduction-widgets.md).

* 다음을 참조하십시오 [개인 식별 정보 처리](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) pii 데이터 처리에 대한 권장 사항입니다.

### 양식 템플릿 만들기

에서 활성화된 양식 템플릿을 사용하여 적응형 양식을 만들 수 있습니다 **구성 브라우저**. 양식 템플릿을 활성화하려면 다음을 참조하십시오. [적응형 양식 템플릿 만들기](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=en).

다른 작성자 컴퓨터에서 만든 적응형 양식 패키지에서 양식 템플릿을 업로드할 수도 있습니다. 양식 템플릿은 다음을 설치하여 사용할 수 있습니다. [aemforms-references-* 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en). 권장되는 몇 가지 모범 사례는 다음과 같습니다.

* 다음 **nosamplecontent** 실행 모드는 작성자에게만 권장되며 게시 노드에는 권장되지 않습니다.
* 적응형 양식, 테마, 템플릿 또는 클라우드 구성과 같은 에셋 작성은 구성된 게시 노드에 게시할 수 있는 작성자 노드에서만 수행됩니다.
자세한 내용은 [양식 및 문서 게시 및 게시 취소](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)
* 문서 서비스 작업을 지원하기 위한 작성 및 게시에 Forms addon 패키지가 필요하므로 종속성으로 간주할 수 있습니다.
Forms 관련 샘플 템플릿, 테마 및 DOR 패키지만 원하는 경우에서 다운로드할 수 있습니다. [aemforms-references-* 패키지](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en).

자세한 내용은 의 모범 사례를 참조하십시오. [적응형 양식 작성 소개](/help/forms/using/introduction-forms-authoring.md).

## 적응형 양식 작성 {#author-adaptive-forms}

### 작성에 터치에 적합한 UI 사용 {#using-touch-optimized-ui-for-authoring}

* 사이드바의 오브젝트 브라우저를 사용하여 양식 계층 구조의 깊은 곳에 있는 필드에 빠르게 액세스할 수 있습니다. 검색 상자를 사용하여 양식 또는 객체 트리에서 객체를 검색하여 한 객체에서 다른 객체로 이동할 수 있습니다.
* 사이드바의 구성 요소 브라우저에서 구성 요소의 속성을 보고 편집하려면 구성 요소를 선택하고 ![cmppr-1](assets/cmppr-1.png). 구성 요소를 두 번 클릭하여 속성 브라우저에서 해당 속성을 볼 수도 있습니다.
* 키보드 단축키를 사용하여 양식에 대한 빠른 작업을 수행할 수 있습니다. 다음을 참조하십시오 [AEM Forms 키보드 단축키](/help/forms/using/keyboard-shortcuts.md).

* 적응형 양식 구성 요소는 적응형 양식 페이지에서만 사용하는 것이 좋습니다. 구성 요소는 상위 계층에 종속됩니다. 따라서 AEM 페이지에서 사용하지 마십시오.

또한 의 구성 요소 설명 및 모범 사례를 참조하십시오. [적응형 양식 작성 소개](/help/forms/using/introduction-forms-authoring.md).

### 적응형 양식에서 규칙 사용 {#using-rules-in-adaptive-forms}

AEM Forms은 [규칙 편집기](/help/forms/using/rule-editor.md) 을 사용하면 적응형 양식 구성 요소에 동적 동작을 추가하는 규칙을 만들 수 있습니다. 이러한 규칙을 사용하여 조건을 평가하고 필드 표시 또는 숨기기, 값 계산, 드롭다운 목록을 동적으로 변경 등과 같은 구성 요소에 대한 작업을 트리거할 수 있습니다.

규칙 편집기는 규칙을 작성할 수 있는 시각적 편집기와 코드 편집기를 제공합니다. 코드 편집기 모드를 사용하여 규칙을 작성할 때에는 다음 사항을 고려하십시오.

* 양식 필드 및 구성 요소에 의미 있고 고유한 이름을 사용하여 규칙을 작성하는 동안 발생할 수 있는 충돌을 방지하십시오.
* 사용 `this` 연산자로, 구성 요소가 규칙 표현식에서 자신을 참조합니다. 구성 요소 이름이 변경되더라도 규칙이 계속 유효한지 확인합니다. 예: `field1.valueCommit script: this.value > 10`

* 다른 양식 구성 요소를 참조할 때 구성 요소 이름을 사용합니다. 사용 `value` 필드 또는 구성 요소의 값을 가져오는 속성입니다. 예: `field1.value`

* 충돌을 방지하려면 상대적 고유 계층 구조를 기준으로 구성 요소를 참조하십시오. 예: `parentName.fieldName`

* 복잡하거나 일반적으로 사용되는 규칙을 처리할 때 비즈니스 논리를 적응형 양식에 걸쳐 지정하고 재사용할 수 있는 별도의 클라이언트 라이브러리에 함수로 작성하는 것이 좋습니다. 클라이언트 라이브러리는 자체 포함된 라이브러리여야 하며, jQuery 및 Underscore.js를 제외하고는 어떠한 외부 종속성도 없어야 합니다. 클라이언트 라이브러리를 사용하여 다음을 적용할 수도 있습니다 [서버측 유효성 재검사](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) / 제출된 양식 데이터.
* 적응형 양식은 적응형 양식과 통신하고 적응형 양식에 대한 작업을 수행하는 데 사용할 수 있는 API 세트를 제공합니다. 일부 주요 API는 다음과 같습니다. 자세한 내용은 [적응형 Forms에 대한 JavaScript 라이브러리 API 참조](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`: 양식을 재설정합니다.
   * `guideBridge.submit()`: 양식을 제출합니다.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: 포커스를 필드로 설정합니다.
   * `guideBridge.validate(errorList, somExpression, focus)`: 양식의 유효성을 검사합니다.
   * `guideBridge.getDataXML(options)`: 양식 데이터를 XML로 가져옵니다.
   * `guideBridge.resolveNode(somExpression)`: 양식 개체를 가져옵니다.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: 양식 개체의 속성을 설정합니다.
   * 또한 다음 필드 속성을 사용할 수 있습니다.

      * `field.value` 필드의 값을 변경합니다.
      * `field.enabled` 필드를 활성화/비활성화합니다.
      * `field.visible` 필드의 가시성을 변경합니다.

* 적응형 양식 작성자는 양식에서 비즈니스 논리를 작성하기 위해 JavaScript 코드를 작성해야 할 수 있습니다. JavaScript는 강력하고 효과적이지만 보안 기대치에 영향을 줄 수 있습니다. 따라서 양식 작성자가 신뢰할 수 있는 사용자인지, 양식을 프로덕션에 추가하기 전에 JavaScript 코드를 검토하고 승인할 수 있는 프로세스가 있는지 확인해야 합니다. 관리자는 역할 또는 기능에 따라 사용자 그룹에 대한 규칙 편집기 액세스를 제한할 수 있습니다. 다음을 참조하십시오 [사용자 그룹을 선택할 수 있는 규칙 편집기 액세스 권한 부여](/help/forms/using/rule-editor-access-user-groups.md).
* 규칙에서 표현식을 사용하여 적응형 양식을 동적으로 만들 수 있습니다. 모든 표현식은 유효한 JavaScript 표현식이며 적응형 양식 스크립팅 모델 API를 사용합니다. 이 표현식은 특정 유형의 값을 반환합니다. 표현식과 관련 모범 사례에 대한 자세한 내용은 [적응형 양식 표현식](/help/forms/using/adaptive-form-expressions.md).

* Adobe은 규칙 편집기로 규칙을 만들 때 비동기 작업보다 JavaScript 동기 작업을 사용하는 것이 좋습니다. 비동기 작업은 사용하지 않는 것이 좋습니다. 그러나 비동기 작업이 불가피한 상황에 처한 경우 JavaScript Closure 함수를 구현해야 합니다. 이렇게 하면 잠재적인 경합 조건으로부터 효과적으로 보호할 수 있으므로 규칙 구현이 최적의 성능을 제공하고 전체에서 안정성을 유지할 수 있습니다.

  예를 들어 외부 API에서 데이터를 가져온 다음 해당 데이터를 기반으로 몇 가지 규칙을 적용해야 한다고 가정해 보겠습니다. 비동기 API 호출을 처리하고 데이터를 가져온 후 규칙이 적용되도록 클로저를 사용합니다. 다음은 샘플 코드입니다.

  ```JavaScript
       function fetchDataFromAPI(apiEndpoint, callback) {
        // Simulate asynchronous API call with setTimeout
        setTimeout(() => {
          // Assuming the API call is successful, we receive some data
          const data = {
            someValue: 42,
          };
          // Invoke the callback with the fetched data
          callback(data);
        }, 2000); // Simulate a 2-second delay for the API call
      }
      // Rule implementation using Closure
      function ruleImplementation(apiEndpoint) {
        // Using a closure to handle the asynchronous API call and rule application
        // say you have set this value in street field inside address panel
        var streetField = address.street;
        fetchDataFromAPI(apiEndpoint, (data) => {
          streetField.value = data.someValue;
        });
      }
      // Example usage of the rule implementation
      const apiEndpoint = "https://example-api.com/data";
      ruleImplementation(apiEndpoint);
  ```

  이 예에서는 `fetchDataFromAPI` 를 사용하여 비동기 API 호출 시뮬레이션 `setTimeout`. 데이터를 가져오면 제공된 콜백 함수를 호출하며, 이 함수는 후속 규칙 응용 프로그램을 처리하는 닫힘입니다. 다음 `ruleImplementation` 함수에는 규칙 논리가 포함되어 있습니다.


### 테마 작업 {#working-with-themes}

테마를 위한 적응형 기능을 사용하면 일관된 모양과 스타일을 위해 양식 간에 적용할 수 있는 재사용 가능한 스타일을 만들 수 있습니다. 테마를 사용하여 양식 구성 요소 및 패널의 스타일을 정의합니다. 테마에 대한 몇 가지 우수 사례는 다음과 같습니다.

* 에셋 라이브러리를 사용하여 텍스트 스타일, 배경 및 이미지를 신속하게 적용할 수 있습니다. 에셋 라이브러리에 스타일이 추가되면 다른 테마와 양식 편집기의 스타일 모드에서 사용할 수 있습니다.
* 페이지 수준 선택기를 사용하여 글꼴 및 페이지 배경과 같은 전역 설정을 적용합니다.
* 클라이언트 라이브러리를 사용하여 기존 스타일 또는 고급 스타일을 테마로 가져옵니다.
* 양식 스타일 레이어에서 특정 필드, 패널 또는 단추의 스타일을 재정의할 수 있습니다.
* 테마가 스타일 요구 사항을 충족하지 않는 경우 guideFieldNode, guideFieldLabel, guideFieldWidget 및 guidePanelNode와 같이 미리 정의된 클래스를 사용하여 양식에 일반적인 스타일을 적용할 수 있습니다.

자세한 내용은 [테마](/help/forms/using/themes.md).

### 크고 복잡한 양식의 성능 최적화 {#optimizing-performance-of-large-and-complex-forms}

양식 작성자 및 최종 사용자는 일반적으로 작성 모드 또는 런타임 시 대형 양식을 로드할 때 성능 문제에 직면합니다. 양식의 오브젝트(필드 및 패널) 수가 증가하면 작성 및 런타임 환경이 저하되기 시작합니다. 또한 여러 작성자가 동시에 협업하고 양식을 작성하는 것을 방지합니다.

대규모 양식에서 성능 문제를 극복하기 위해 다음 모범 사례를 고려하십시오.

* 가능하면 XFA를 적응형 양식으로 전환할 때도 XSD 양식 데이터 모델을 사용하여 적응형 양식을 만드는 것이 좋습니다.
* 사용자의 정보를 캡처하는 적응형 양식에 해당 필드와 패널만 포함하십시오. 정적 콘텐츠를 최소로 유지하거나 URL을 사용하여 별도의 창에서 여는 것이 좋습니다.
* 모든 양식이 특정 목적을 위해 디자인되었지만 대부분의 양식에는 몇 가지 일반적인 세그먼트가 있습니다. 예를 들어 개인 세부 정보, 주소, 고용 세부 정보 등이 있습니다. 만들기 [적응형 양식 단편](/help/forms/using/adaptive-form-fragments.md) 일반적인 양식 요소 및 섹션의 경우 여러 양식에서 사용하십시오. 기존 양식의 패널을 조각으로 저장할 수도 있습니다. 조각의 모든 변경 사항은 연결된 모든 적응형 양식에 반영됩니다. 여러 작성자가 양식을 구성하는 여러 조각에서 동시에 작업할 수 있으므로 공동 작성을 촉진합니다.

   * 적응형 양식과 유사하게 모든 조각별 스타일 및 사용자 지정 스크립트는 조각 컨테이너 대화 상자를 사용하여 클라이언트 라이브러리에 정의하는 것이 좋습니다. 또한 외부 오브젝트에 의존하지 않는 자급자족 조각을 만들어 보십시오.
   * 교차 조각 스크립팅을 사용하지 마십시오. 참조해야 하는 조각 외부에 개체가 있는 경우 해당 개체를 상위 양식의 일부로 만드십시오. 객체가 다른 조각에 계속 있어야 하는 경우 스크립트에서 해당 이름으로 객체를 참조합니다.

* 자동 저장과 함께 저장 및 다시 시작 을 사용하여 적응형 양식을 정기적으로 저장하고 사용자가 나중에 다시 방문하여 양식을 완료할 수 있도록 합니다.
* 느리게 로드할 조각을 구성합니다. 런타임 시 느리게 로드되도록 표시된 조각은 필요한 경우에만 렌더링됩니다. 대형 양식의 로드 시간을 크게 줄입니다. 반복 가능한 패널이 있는 조각에서도 지원됩니다. 자세한 내용은 [레이지 로드 구성](/help/forms/using/lazy-loading-adaptive-forms.md).

   * 응답형 격자 레이아웃 또는 첫 번째 패널에서 조각에 대한 소극적 로드를 구성하지 마십시오.
   * 느리게 로드된 조각에서 파일 첨부 및 약관 구성 요소가 지원되지 않습니다.
   * 포함된 패널이 언로드될 때 값을 사용할 수 있도록 해당 값이 다른 부분에서 사용되는 경우 지연 로드된 패널의 값을 전체적으로 값 사용(Use Value Globally)으로 표시합니다.
   * 조건을 기반으로 표시하거나 숨겨야 하는 조각에 대한 가시성 규칙을 작성하는 것이 좋습니다.
* 값 설정 **요청당 호출 수** 다음에서 **Apache Sling 기본 서블릿** 꽤 많은 숫자로. 이를 통해 Forms 서버는 추가 호출을 허용할 수 있습니다. 이 구성은 기본값 1500을 표시합니다. 값 1500 호출은 Sites 및 Assets와 같은 기타 Experience Manager 구성 요소를 위한 것입니다. 적응형 양식의 기본값 세트는 20000. 다음 상황이 발생하는 경우 `too many calls` 로그에 오류가 있거나 양식이 렌더링되지 않습니다. 값을 큰 수로 늘려 문제를 해결하십시오. 호출 수가 20000개를 초과하는 경우 양식이 복잡하므로 브라우저에서 양식을 렌더링하는 데 시간이 걸릴 수 있습니다. 이 작업은 양식이 처음 로드될 때만 발생하며, 그 이후에는 양식이 캐시되고 양식이 캐시되면 성능에 큰 영향을 주지 않습니다.

### 적응형 양식 미리 채우기 {#prefilling-adaptive-forms}

적응형 양식 필드에 백엔드에서 가져온 데이터를 미리 채워 사용자가 양식을 빠르게 채우고 입력 실수를 피할 수 있습니다.

* AEM Forms은 사전 정의된 데이터 XML 파일에서 데이터를 읽고 적응형 양식의 필드를 사전 채우기 XML 파일의 콘텐츠로 미리 채우는 사전 채우기 서비스를 제공합니다.
* 미리 채우기 데이터 XML은 적응형 양식과 연결된 양식 모델의 스키마와 호환되어야 합니다.
* 포함 `afBoundedData` 및 `afUnBoundedData` 적응형 양식의 바인딩된 필드와 바인딩되지 않은 필드를 모두 미리 채우려면 미리 채우기 XML의 섹션을 참조하십시오.

* 양식 데이터 모델 기반 적응형 양식의 경우 AEM Forms에서 즉시 사용 가능한 양식 데이터 모델 미리 채우기 서비스를 제공합니다. 미리 채우기 서비스는 적응형 양식의 데이터 모델 개체에 대한 데이터 소스를 쿼리하고 양식을 렌더링할 때 필드 값을 미리 채웁니다.
* 파일, crx, 서비스 또는 http 프로토콜을 사용하여 적응형 양식을 미리 채울 수도 있습니다.
* AEM Forms은 적응형 양식을 미리 채우기 위해 OSGi 서비스로 연결할 수 있는 사용자 지정 미리 채우기 서비스를 지원합니다.

자세한 내용은 [적응형 양식 필드 미리 채우기](/help/forms/using/prepopulate-adaptive-form-fields.md).

### 적응형 양식 서명 및 제출 {#signing-and-submitting-adaptive-forms}

적응형 양식을 처리하려면 제출 액션이 필요합니다. 제출 액션은 적응형 양식을 사용하여 제출하는 데이터에 대해 수행되는 작업을 결정합니다.

* 적응형 양식에서는 몇 가지 제출 액션을 즉시 사용할 수 있습니다. 자세한 내용은 [제출 액션 구성](/help/forms/using/configuring-submit-actions.md).
* 기본 제출 액션이 사용 사례를 충족하지 않는 경우 사용자 지정 제출 액션을 작성할 수 있습니다. 자세한 내용은 [적응형 양식에 대한 사용자 정의 제출 액션 작성](/help/forms/using/custom-submit-action-form.md).
* 잘못된 데이터 제출을 방지하기 위해 서버측 유효성 검사를 포함합니다.

적응형 양식에서 Adobe Sign의 다중 서명 경험을 사용할 수 있습니다. 적응형 양식에서 Adobe Sign을 구성할 때는 다음 사항을 고려하십시오. 자세한 내용은 [적응형 양식에서 Adobe Sign 사용](/help/forms/using/working-with-adobe-sign.md).

* Adobe Sign이 활성화된 적응형 양식은 모든 서명자가 양식에 서명한 후에만 제출됩니다. 모든 서명자가 양식에 서명할 때까지 Forms이 서명 보류 중 상태로 표시됩니다.
* 제출 시 양식 내 서명 경험을 구성하거나 서명자를 서명 페이지로 리디렉션할 수 있습니다.
* 필요에 따라 순차적 또는 병렬 서명 환경을 구성합니다.

### 기록 문서 생성 중 {#generating-document-of-record}

기록 문서(DoR)는 인쇄, 서명 또는 보관할 수 있는 적응형 양식의 병합된 PDF 버전입니다.

* 적응형 양식의 기반이 되는 양식 데이터 모델에 따라 다음과 같이 DoR용 템플릿을 구성할 수 있습니다.

   * **XFA 양식 템플릿**: 연결된 XDP 파일을 DoR 템플릿으로 사용합니다.
   * **XSD 스키마**: 적응형 양식에서 사용되는 것과 동일한 XML 스키마를 사용하는 관련 XFA 템플릿을 사용합니다.
   * **없음**: 자동 생성된 DoR을 사용합니다.

* 적응형 양식 편집기의 기록 문서 탭에서 머리글, 바닥글, 이미지, 색상, 글꼴 등을 바로 구성합니다.
* 사용 `DoRService` 를 입력하여 프로그래밍 방식으로 DoR을 생성합니다.
* DoR에서 숨겨진 필드를 제외합니다.
* 사용 `afAcceptLang` 다른 로케일에서 DoR을 보려면 매개 변수를 요청하십시오.

### 적응형 양식 디버깅 및 테스트 {#debugging-and-testing-adaptive-forms}

[AEM Chrome 플러그인](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) 는 적응형 양식 디버깅을 위한 도구를 제공하는 Google Chrome용 브라우저 확장 기능입니다. 양식 작성자 및 개발자는 다음 도구를 사용하여 다음을 수행할 수 있습니다.

* 병목 현상 파악 및 양식 렌더링 성능 최적화
* 양식의 디버그 키워드 및 bindRef 오류
* 로그 활성화 및 구성
* 양식에서 규칙 및 스크립트 디버그
* guideBridge API에 대해 알아보고 알아봅니다.

자세한 내용은 [AEM Chrome 플러그인 - 적응형 양식](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### AEM 서버에서 적응형 양식 유효성 검사 {#validating-adaptive-forms-on-aem-server}

클라이언트에서의 유효성 검사를 우회하려는 시도와 데이터 제출 및 비즈니스 규칙 위반의 가능한 중단을 방지하기 위해 서버측 유효성 검사가 필요합니다. 서버측 유효성 검사는 필요한 클라이언트 라이브러리를 로드하여 서버에서 실행됩니다.

* 적응형 양식의 표현식을 확인하기 위한 함수를 클라이언트 라이브러리에 포함하고 적응형 양식 컨테이너 대화 상자에서 클라이언트 라이브러리를 지정합니다. 자세한 내용은 [서버 측 유효성 재검사](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* 서버측 유효성 검사는 양식 모델의 유효성을 검사합니다. 유효성 검사를 위해 별도의 클라이언트 라이브러리를 만들고 동일한 클라이언트 라이브러리에서 HTML 스타일링 및 DOM 조작과 같은 다른 항목과 혼합하지 않는 것이 좋습니다.

### 적응형 양식 현지화 {#localizing-adaptive-forms}

AEM은 적응형 양식을 현지화하는 데 사용할 수 있는 번역 워크플로우를 제공합니다. 자세한 내용은 [AEM 번역 워크플로를 사용하여 적응형 양식 현지화](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

적응형 양식을 현지화할 때의 몇 가지 모범 사례는 다음과 같습니다.

* 여러 양식의 공통 요소에 대해 적응형 양식 조각을 사용하고 조각을 현지화합니다. 이렇게 하면 조각을 한 번 현지화하고 현지화된 조각이 사용되는 모든 양식에 반영할 수 있습니다.
* 새 구성 요소를 추가하거나 현지화된 양식으로 스크립트를 적용하는 등의 수정 사항은 자동으로 현지화되지 않습니다. 따라서 양식을 현지화하기 전에 먼저 양식을 완료해야 여러 현지화 주기를 방지할 수 있습니다.
* 사용 `afAcceptLang` 브라우저 로케일을 재정의하고 지정된 로케일에서 양식을 렌더링하도록 매개 변수를 요청합니다. 예를 들어 다음 URL은 브라우저 설정에 지정된 로케일에 관계없이 일본어 로케일로 양식을 렌더링해야 합니다.

  `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms은 현재 영어(en), 스페인어(es), 프랑스어(fr), 이탈리아어(it), 독일어(de), 일본어(ja), 포르투갈어(브라질), 중국어(zh-CN), 중국어(zh-TW) 및 한국어(ko-KR) 로케일로 된 적응형 양식 콘텐츠의 현지화를 지원합니다. 그러나 런타임 시 적응형 양식에 대한 새 로케일에 대한 지원을 추가할 수 있습니다. 자세한 내용은 [적응형 양식 지역화를 위한 새 로케일 지원](/help/forms/using/supporting-new-language-localization.md).

## 제작을 위한 양식 프로젝트 준비 {#prepare-forms-project-for-production}

### Forms 처리 서버 추가 중 {#adding-forms-processing-server}

보안 영역에서 방화벽 뒤에 있는 AEM Forms 서버의 추가 인스턴스를 구성할 수 있습니다. 다음 경우에 이 인스턴스를 사용할 수 있습니다.

* **일괄 처리**: 로드가 많은 배치로 반복 또는 예약된 작업. 예를 들어 명령문 인쇄, 서신 생성, PDF Generator, 출력 및 어셈블러와 같은 문서 서비스 사용 등이 있습니다.
* **PII 데이터 저장**: 처리 서버에 PII 데이터를 저장합니다. 이미 PII 데이터를 저장하기 위해 사용자 지정 스토리지 공급자를 사용 중인 경우에는 필요하지 않습니다.

### 프로젝트를 다른 환경으로 이동 {#moving-project-to-another-environment}

한 환경에서 다른 환경으로 AEM 프로젝트를 이동해야 하는 경우가 많습니다. 이동할 때 기억해야 할 몇 가지 주요 사항은 다음과 같습니다.

* 기존 클라이언트 라이브러리, 사용자 정의 코드 및 구성을 백업합니다.
* 새 환경에서 지정된 순서로 제품 패키지 및 패치를 수동으로 배포합니다.
* 프로젝트별 코드 패키지 및 번들을 수동으로 새 AEM 서버에 별도의 패키지 또는 번들로 배포합니다.
* (*JEE의 AEM Forms 전용*) Forms Workflow 서버에 LCA 및 DSC를 수동으로 배포합니다.
* 사용 [Export-Import](/help/forms/using/import-export-forms-templates.md) 새 환경으로 에셋을 이동하는 기능입니다. 복제 에이전트를 구성하고 자산을 게시할 수도 있습니다.
* 업그레이드 시 더 이상 사용되지 않는 모든 API 및 기능을 새 API 및 기능으로 바꾸십시오.

### AEM 구성 {#configuring-aem}

전반적인 성능을 개선하도록 AEM을 구성하는 몇 가지 모범 사례는 다음과 같습니다.

* Felix 콘솔에서 JavaScript 및 CSS에 대한 HTML 클라이언트 라이브러리 압축을 활성화합니다.
* 다음 위치에 모든 클라이언트 라이브러리 캐시하기 `/etc.clientlibs/fd` 게시된 양식의 응답성과 보안을 개선하기 위해 AEM dispatcher의 모든 추가 사용자 지정 클라이언트 라이브러리를 제공합니다. 자세한 내용은 [디스패처](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* 캐시하지 않음 `/content/forms/af/` 및 `/content/dam/formsanddocuments/*` 경로. 적응형 양식 캐싱 구성에 대한 자세한 내용은 다음을 참조하십시오. [적응형 양식 캐싱](/help/forms/using/configure-adaptive-forms-cache.md).

* 웹 서버 압축 모듈을 통해 HTML을 활성화합니다. 자세한 내용은 [AEM Forms 서버의 성능 조정](/help/forms/using/performance-tuning-aem-forms.md).
* 대형 양식에 대한 요청 구성당 호출 수를 늘립니다. 다음을 참조하십시오 [크고 복잡한 양식의 성능 최적화](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* 만들기 [오류 핸들러에 의해 표시되는 사용자 지정 오류 페이지](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html).
* 보안 AEM Forms 서버.

   * 사용 `nosamplecontent` 실행 모드를 사용하여 프로덕션 서버에 배포된 샘플 콘텐츠 및 샘플 사용자가 없도록 합니다. 다음을 참조하십시오 [프로덕션 준비 모드에서 AEM 실행](/help/sites-administering/production-ready.md).

* 힙 크기를 최소 8GB로 유지합니다. 다른 설정에 대해서는 [AEM Forms 서버의 성능 조정](/help/forms/using/performance-tuning-aem-forms.md).
* 서비스 수준 작업을 실행하기 위해 관리자 세션 대신 서비스 사용자 세션을 사용하십시오. 자세한 내용은 [서비스 인증](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### 초안 및 제출된 양식 데이터에 대한 외부 저장소 구성 {#external-storage}

프로덕션 환경에서는 제출된 양식 데이터를 AEM 저장소에 저장하지 않는 것이 좋습니다. Forms 포털 스토어, 컨텐츠 저장 및 스토어 PDF 제출 작업의 기본 구현은 AEM 저장소에 양식 데이터를 저장합니다. 이러한 제출 액션은 데모용으로만 사용됩니다. 또한 저장 및 재개 및 자동 저장 기능은 기본적으로 포털 저장소를 사용합니다. 따라서 다음 권장 사항을 고려하십시오.

* **초안 데이터 저장**: 적응형 양식의 초안 기능을 사용하는 경우 사용자 정의 SPI(서비스 제공 인터페이스)를 구현하여 초안 데이터를 데이터베이스와 같은 보다 안전한 저장소에 저장해야 합니다. 자세한 내용은 [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md).

* **제출 데이터 저장**: Form Portal 제출 저장소를 사용하는 경우 데이터베이스에 제출 데이터를 저장하려면 사용자 지정 SPI를 구현해야 합니다. 다음을 참조하십시오 [초안 및 제출 구성 요소와 데이터베이스를 통합하기 위한 샘플](/help/forms/using/integrate-draft-submission-database.md) 샘플 통합용.

  보안 저장소에 양식 데이터 및 첨부 파일을 저장하는 사용자 지정 제출 액션을 작성할 수도 있습니다. 다음을 참조하십시오 [적응형 양식에 대한 사용자 정의 제출 액션 작성](/help/forms/using/custom-submit-action-form.md) 추가 정보.

* **초안 ID 길이**: 적응형 양식을 초안으로 저장하면 초안을 고유하게 식별하기 위한 초안 ID가 생성됩니다. 초안 ID 필드의 최소 값은 26자입니다. Adobe은 초안 ID 길이를 26자 이상으로 설정할 것을 권장합니다.

### 개인 식별 정보 처리 {#handling-personally-identifiable-information}

조직의 주요 당면 과제 중 하나는 PII(개인 식별 가능) 데이터를 처리하는 방법입니다. 이러한 데이터를 처리하는 데 도움이 되는 몇 가지 모범 사례는 다음과 같습니다.

* 데이터베이스와 같은 안전한 외부 저장소를 사용하여 초안 및 제출된 양식의 데이터를 저장합니다. 다음을 참조하십시오 [초안 및 제출된 양식 데이터에 대한 외부 저장소 구성](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* 자동 저장을 활성화하기 전에 약관 양식 구성 요소를 사용하여 사용자의 명시적 동의를 얻으십시오. 이 경우 사용자가 약관 구성 요소의 약관에 동의하는 경우에만 자동 저장을 활성화하십시오.

## 적응형 양식에 대한 규칙 편집기, 코드 편집기 또는 사용자 지정 클라이언트 라이브러리를 선택합니다 {#RuleEditor-CodeEditor-ClientLibs}

### 규칙 편집기 {#rule-editor}

<!--The AEM Forms Rule Editor offers predefined functions for defining rules in adaptive forms without extensive programming. It facilitates the implementation of conditional logic, data validation, and integration with external sources. This visual interface is especially valuable for business users and form designers, enabling them to create dynamic and complex rules with ease, here we discusss few use cases where rule editor allows you to:-->

AEM Forms 규칙 편집기는 규칙을 만들고 관리하기 위한 시각적 인터페이스를 제공하여 광범위한 코딩의 필요성을 줄입니다. 고급 프로그래밍 기술은 없지만 양식 내에서 비즈니스 규칙을 정의하고 유지 관리해야 하는 비즈니스 사용자 또는 양식 디자이너에게 특히 유용할 수 있습니다. 여기서는 규칙 편집기를 통해 다음과 같은 작업을 수행할 수 있는 몇 가지 사용 사례에 대해 설명합니다.

* <!-- Allows you --> 포괄적인 프로그래밍을 하지 않고도 양식에 대한 비즈니스 규칙을 정의할 수 있습니다.
* <!-- Use the Rule Editor when you need --> 양식 내에 조건부 논리를 구현합니다. 여기에는 양식 요소 표시 또는 숨기기, 특정 조건에 따라 필드 값 변경 또는 양식의 동작 동적 변경이 포함됩니다.
* <!--When you want --> 양식 제출에 데이터 검증 규칙을 적용하려면 규칙 편집기 를 사용하여 검증 조건을 정의할 수 있습니다.
* <!-- When you need --> 양식을 외부 데이터 소스(FDM) 또는 서비스와 통합하기 위해 규칙 편집기는 양식 상호 작용 중에 데이터를 가져오고, 표시하거나, 조작하기 위한 규칙을 정의하는 데 도움이 될 수 있습니다.
* <!-- If you want -->사용자 작업에 응답하는 동적 및 대화형 양식을 만들기 위해 규칙 편집기를 사용하여 양식 요소의 동작을 실시간으로 제어하는 규칙을 정의할 수 있습니다.

규칙 편집기는 AEM Forms Foundation 구성 요소와 핵심 구성 요소 모두에서 사용할 수 있습니다.

### 코드 편집기 {#code-editor}

코드 편집기는 Adobe Experience Manager(AEM) Forms 내의 도구로서, 여기에서는 몇 가지 사용 사례에 대해 논의하여 양식에 보다 복잡하고 고급 기능을 위한 사용자 지정 스크립트 및 코드를 작성할 수 있습니다.

* AEM Forms 규칙 편집기의 기능을 벗어나는 사용자 지정 클라이언트측 논리 또는 비헤이비어를 구현해야 하는 경우. 코드 편집기를 사용하면 복잡한 상호 작용, 계산 또는 유효성 검사를 처리하는 JavaScript 코드를 작성할 수 있습니다.
* 양식에 서버측 처리 또는 외부 시스템과의 통합이 필요한 경우 코드 편집기를 사용하여 사용자 지정 서버측 스크립트를 작성할 수 있습니다. 코드 편집기에서 guideBridge API에 액세스하여 양식 이벤트 및 개체에 대한 복잡한 논리를 구현할 수 있습니다.
* AEM Forms 구성 요소의 표준 기능을 뛰어넘는 고도로 맞춤화된 사용자 인터페이스가 필요한 경우 코드 편집기를 사용하여 사용자 정의 스타일, 비헤이비어를 구현하거나 사용자 정의 양식 구성 요소를 만들 수 있습니다.
* 양식에 비동기 데이터 로드와 같은 비동기 작업이 포함된 경우, 코드 편집기를 사용하여 사용자 지정 비동기 JavaScript 코드를 통해 이러한 작업을 관리할 수 있습니다.

코드 편집기를 사용하려면 JavaScript 및 AEM Forms 아키텍처에 대한 올바른 이해가 필요합니다. 또한 사용자 지정 코드를 구현할 때에는 모범 사례를 따르고, 보안 지침을 준수하고, 프로덕션 환경에서 발생할 수 있는 문제를 방지하기 위해 코드를 철저히 테스트해야 합니다. 코드 편집기를 사용하여 FDM에 대한 콜백을 구현할 수 있습니다.

코드 편집기는 AEM Forms Foundation 구성 요소에만 사용할 수 있습니다. 적응형 양식 핵심 구성 요소의 경우 다음 섹션에 설명된 대로 사용자 정의 함수를 사용하여 고유한 양식 규칙을 만들 수 있습니다.

### 사용자 정의 함수 {#custom-client-libs}

AEM Forms(Adobe Experience Manager Forms)에서 사용자 지정 클라이언트 라이브러리를 사용하면 다양한 시나리오에서 양식의 기능, 스타일 또는 동작을 개선하는 데 유용할 수 있습니다. 다음은 사용자 지정 클라이언트 라이브러리를 사용하는 것이 적절할 수 있는 몇 가지 상황입니다.

* AEM Forms에서 제공하는 기본 스타일 옵션의 기능을 벗어나는 양식에 고유한 디자인이나 브랜딩을 구현해야 하는 경우 사용자 지정 클라이언트 라이브러리를 만들어 모양과 느낌을 제어할 수 있습니다.
* 사용자 지정 클라이언트측 논리가 필요한 경우, 표준 AEM Forms 기능을 통해 달성할 수 없는 여러 양식 또는 동작에서 메서드를 재사용할 수 있습니다. 여기에는 동적 양식 상호 작용, 사용자 지정 유효성 검사 또는 서드파티 라이브러리와의 통합이 포함될 수 있습니다.
* 클라이언트측 리소스를 최적화 및 축소하여 양식의 성능을 개선하십시오. 사용자 지정 클라이언트 라이브러리를 사용하여 JavaScript 및 CSS 파일을 번들로 제공하고 압축할 수 있으므로 전체 페이지 로드 시간이 줄어듭니다.
* 기본 AEM Forms 설정에 포함되지 않은 추가 JavaScript 라이브러리 또는 프레임워크를 통합해야 하는 경우. 이 작업은 고급 날짜 선택기, 차트 또는 기타 대화형 구성 요소와 같은 기능에 필요할 수 있습니다.

사용자 정의 클라이언트 라이브러리를 사용하기 전에 유지 관리 오버헤드, 향후 업데이트와의 잠재적 충돌 및 모범 사례를 준수하는 것을 고려해야 합니다. 업그레이드 중이나 다른 개발자와 공동 작업할 때 발생하는 문제를 방지하기 위해 맞춤화 사항이 잘 문서화되고 테스트되었는지 확인하십시오.

>[!NOTE]
> 사용자 지정 기능은 AEM Forms Foundation 구성 요소와 핵심 구성 요소 모두에서 사용할 수 있습니다.

**사용자 정의 함수의 장점:**

**사용자 정의 함수** 보다 주목할 만한 이점 제공 **코드 편집기** 이는 콘텐츠와 코드 간의 명확한 분리를 통해 공동 작업을 향상시키고 워크플로를 간소화하기 때문입니다. 다음과 같은 이점을 얻으려면 사용자 지정 함수를 사용하는 것이 좋습니다.

* **Git과 같은 버전 관리 제어를 원활하게 사용할 수 있습니다.**
   * 콘텐츠에서 코드를 분리하면 콘텐츠 관리 중에 Git 충돌이 크게 줄어들고 잘 정리된 저장소가 촉진됩니다.
   * 사용자 지정 함수는 여러 기여자가 동시에 작업하는 프로젝트에 유용합니다.

* **기술적 이점:**
   * 맞춤형 기능은 모듈화 및 캡슐화를 제공합니다.
   * 모듈은 독립적으로 개발, 테스트 및 유지 관리할 수 있습니다.
   * 코드 재사용 및 유지 관리 기능이 향상됩니다.

* **효율적인 개발 프로세스:**
   * 모듈화를 통해 개발자는 특정 기능에 집중할 수 있습니다.
   * 전체 코드 베이스의 복잡성을 줄여 개발자의 부담을 줄여 개발 프로세스를 보다 효율적으로 진행할 수 있습니다.



