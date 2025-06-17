---
title: SPA 편집기 서비스 중단
description: SPA Editor는 Adobe에서 계속 지원되지만, 그 가치가 프로젝트에 어떤 의미가 있는지, 그리고 향후 프로젝트를 위해 어떤 옵션이 있는지 알아보십시오.
feature: Developing
role: Admin, Architect, Developer
exl-id: ea6e46ee-4a90-4236-8d93-292a4dda4dc0
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---

# SPA 편집기 서비스 중단 {#spa-editor-deprecation}

SPA Editor는 Adobe에서 계속 지원되지만, 그 가치가 프로젝트에 어떤 의미가 있는지, 그리고 향후 프로젝트를 위해 어떤 옵션이 있는지 알아보십시오.

## 요약 {#summary}

Adobe은 SPA 편집기를 더 이상 사용하지 않으며, AEM 6.5의 [릴리스 6.5.23,](/help/release-notes/release-notes.md#spa-editor)을(를) 통해 SDK에 대한 추가 개선 사항 또는 업데이트가 수행되지 않습니다. Adobe에서는 AEM의 혁신적인 최신 기능을 활용하기 위해 새로운 헤드리스 프로젝트에 [유니버설 편집기](/help/sites-developing/universal-editor/introduction.md)를 사용할 것을 권장합니다.

## 사용 중단 세부 정보 {#details}

SPA 편집기 **의 사용 중단은 즉시 제거**&#x200B;를 의미하지 않으며, 기존 구현이 있는 경우 **필요에 맞는 경우 계속 사용할 수 있습니다.** 그러나 사용 중단에 대한 다음과 같은 의미에 유의하십시오.

* 앞으로 Adobe은 P1 및 P2 문제와 보안 취약점만 해결합니다.
* SDK에 대한 추가 개발, 개선 사항 또는 업데이트는 제공되지 않습니다.

사용 중단이란 다음 SDK가 이제 기능이 정지되었음을 의미합니다.

* [AEM Project Archetype](https://github.com/adobe/aem-project-archetype/)
* [AEM SPA 프로젝트 코어](https://github.com/adobe/aem-spa-project-core)
* [AEM SPA 페이지 모델 관리자](https://github.com/adobe/aem-spa-page-model-manager)
* [AEM SPA 구성 요소 매핑](https://github.com/adobe/aem-spa-component-mapping)
* [AEM SPA React 편집 가능한 구성 요소](https://github.com/adobe/aem-react-editable-components)
   * [AEM React 핵심 구성 요소](https://github.com/adobe/aem-react-core-wcm-components)
   * [AEM React 핵심 구성 요소 베이스](https://github.com/adobe/aem-react-core-wcm-components-base)
   * [AEM React 핵심 구성 요소 SPA](https://github.com/adobe/aem-react-core-wcm-components-spa)
   * [AEM React 핵심 구성 요소 예제](https://github.com/adobe/aem-react-core-wcm-components-examples)
* [AEM SPA Angular 편집 가능한 구성 요소](https://github.com/adobe/aem-angular-editable-components)
   * [AEM Angular 핵심 구성 요소](https://github.com/adobe/aem-angular-core-wcm-components)
   * [AEM Angular 핵심 구성 요소 베이스](https://github.com/adobe/aem-angular-core-wcm-components-base)
   * [AEM Angular 핵심 구성 요소 SPA](https://github.com/adobe/aem-angular-core-wcm-components-spa)
   * [AEM Angular 핵심 구성 요소 예제](https://github.com/adobe/aem-angular-core-wcm-components-examples)
* [AEM SPA 값 편집 가능한 구성 요소](https://github.com/mavicellc/aem-vue-editable-components)

## SPA 편집기의 대안 {#alternatives}

SPA 편집기에 가장 적합한 대체 요소는 프로젝트 요구 사항에 따라 다릅니다.

* **[범용 편집기](/help/sites-developing/universal-editor/introduction.md)**&#x200B;는 SPA 편집기를 직접 대체하는 것이 가장 좋습니다.
   * 또한 범용 편집기는 시각적 편집기이며 SPA 편집기의 모든 Adobe 경험을 통합하여 분리된 구현을 위해 특별히 디자인되었습니다.
   * 또한 범용 편집기는 [AEM as a Cloud Service용으로 릴리스](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)되었으므로 클라우드 서비스 외에도 AMS 및 온프레미스 사용 사례를 지원합니다.
* **[콘텐츠 조각 편집기](/help/sites-developing/universal-editor/introduction.md)**&#x200B;는 양식 기반 편집기를 선호하는 사용자를 위한 대체 요소입니다.
   * 콘텐츠 조각 편집기는 콘텐츠가 페이지가 아닌 콘텐츠 조각으로 구조화될 때 가장 적합합니다.

콘텐츠 조각을 사용하여 콘텐츠를 구조화해도 시각적 편집기로서의 범용 편집기의 사용이 제외되지 않으며 두 편집기를 함께 사용할 수 있습니다.

## 범용 편집기로 마이그레이션 {#migrate-ue}

유니버설 편집기는 많은 이점을 제공하므로 이 편집기로 마이그레이션하는 것이 새로운 프로젝트에 적합한 솔루션입니다.

* **시각적 편집:** SPA 편집기와 마찬가지로 작성자가 미리 보기 내에서 직접 콘텐츠를 편집하여 변경 내용이 방문자 경험에 미치는 영향을 즉시 확인할 수 있습니다.
* **향후 교정:** AEM의 로드맵은 비주얼 편집기로 유니버설 편집기의 우선 순위를 지정합니다. 이를 채택하면 최신 혁신 및 향상된 기능에 액세스할 수 있습니다.
* **간단한 통합:** 범용 편집기를 사용하는 데 AEM 관련 SDK이 필요하지 않으므로 기술 스택 잠금이 줄어듭니다.
* **나만의 앱 만들기:** 유니버설 편집기는 모든 웹 프레임워크나 아키텍처를 지원하므로 복잡한 리팩터링을 수행하지 않아도 됩니다.
* **확장성:** 유니버설 편집기는 GenAI, Workfront 등과의 통합을 포함하여 강력한 [확장 프레임워크,](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/extending)의 이점을 제공합니다.

SPA 편집기에서 범용 편집기로의 직접 마이그레이션 경로는 없습니다. 이는 두 기술의 근본적인 차이에서 기인한다.

* 범용 편집기는 템플릿 편집기, 스타일 시스템 또는 반응형 그리드 같은 기능을 다시 도입하지 않습니다.
   * 이제 Edge Delivery Services 또는 Headless 프로젝트의 린 프론트엔드 CSS 및 JS를 사용하여 이러한 사용 사례를 보다 효율적으로 처리할 수 있습니다.
* 범용 편집기는 Editor-as-a-Service이므로 구현자가 CSS 또는 JS를 구성 요소 대화 상자에 삽입하는 것을 허용하지 않습니다.
   * 이렇게 하면 페이지 편집기에서 구성 요소 대화 상자가 자동으로 변환되지 않습니다.
   * 이 기능은 사용자 정의 위젯, 필드 유효성 검사, 규칙 표시/숨기기 및 템플릿 기반 사용자 지정과 같은 대화 상자의 많은 영역에 영향을 줍니다.

이러한 기술적 차이점을 염두에 두고 Adobe의 권장 사항은 다음과 같습니다.

* 지원이 계속되므로 기존 SPA Editor 사이트를 그대로 유지합니다.
* 새 사이트, 섹션 또는 페이지를 포함한 모든 새로운 개발에 범용 편집기를 채택합니다.

유니버설 편집기에 특정 SPA 편집기 기능이 직접 구현되지 않았더라도, 유니버설 편집기의 새로운 유연성을 사용하여 동일한 문제를 해결할 수 있는 새로운 방법이 있다는 점을 명심하십시오.

## SPA 편집기와 유니버설 편집기 비교 {#spa-vs-ue}

유니버설 편집기는 이 다이어그램에 표시된 대로 웹 앱의 구현자에게 훨씬 더 많은 자유를 제공합니다.

![유니버설 편집기 및 SPA 편집기 아키텍처 비교](assets/spa-editor-vs-ue.png)

|  | SPA 편집기 | 범용 편집기 |
|---|---|---|
| **테마 설정** | 앱은 AEM의 그리드 CSS를 사용하여 레이아웃을 구현해야 합니다. | 앱은 모든 최신 CSS 기술을 레이아웃에 사용할 수 있습니다. |
| **렌더링** | 앱은 SPA 편집기의 라우팅 구조를 따라야 합니다. | 앱은 지켜야 할 규칙이나 패턴이 부과되지 않고 자유롭게 구현할 수 있다. |
| **SDK** | 구현은 SDK과 긴밀하게 통합되어야 합니다. | 작성자 계층에서 앱은 `corlib.js`만 로드하고 HTML 주석을 통해 유니버설 편집기에 지시합니다. |
| **프레임워크** | 앱은 지원되는 버전의 React 또는 Angular을 사용해야 합니다. | 앱은 모든 프레임워크나 아키텍처를 사용할 수 있습니다. |
| **호스팅** | 앱은 AEM 도메인에서 호스팅되어야 합니다. | 앱은 어디에서나 완전히 분리되고 호스팅될 수 있습니다. |
| **API** | 앱은 `model.json` API에서 콘텐츠를 검색해야 합니다. | 앱은 사용자 지정 API를 포함한 모든 API를 사용할 수 있습니다. |
| **지속성** | SPA 편집기는 시각적 편집을 위한 페이지 콘텐츠만 지원합니다. | 유니버설 편집기는 기본적으로 페이지 및 콘텐츠 조각의 시각적 편집을 지원합니다. |
|  |  | 범용 편집기를 확장하여 동일한 시각적 기능으로 외부 콘텐츠를 편집할 수 있습니다. |
|  | 개발자는 AEM에 Sling 모델 및 `cq:Dialog`을(를) 배포해야 합니다. | 개발자는 AEM 경험이 거의 필요하지 않으며 Java를 쓸 필요가 없습니다. |
