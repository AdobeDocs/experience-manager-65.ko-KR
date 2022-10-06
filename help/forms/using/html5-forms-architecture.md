---
title: HTML 5 양식의 아키텍처
seo-title: Architecture of HTML5 forms
description: HTML5 양식은 포함된 AEM 인스턴스 내에 패키지로 배포되고 RESTful Apache Sling 아키텍처를 사용하여 HTTP/S를 통해 REST 종료 지점으로 기능을 표시합니다.
seo-description: HTML5 forms is deployed as a package within the embedded AEM instance and exposes the functionality as REST end point over HTTP/S using RESTful Apache Sling architecture.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
feature: Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 0%

---

# HTML 5 양식의 아키텍처{#architecture-of-html-forms}

## 아키텍처 {#architecture}

HTML5 양식 기능은 포함된 AEM 인스턴스 내에 패키지로 배포되며 RESTful을 사용하여 HTTP/S를 통해 REST 끝점으로 표시됩니다 [Apache Sling 아키텍처](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Sling 프레임워크 사용 {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) 은 리소스 중심입니다. 먼저 요청 URL을 사용하여 리소스를 확인합니다. 각 리소스에는 **sling:resourceType** 또는 **sling:resourceSuperType**) 속성을 사용합니다. 이 속성, 요청 메서드 및 요청 URL의 속성을 기반으로 요청을 처리하기 위해 sling 스크립트가 선택됩니다. 이 sling 스크립트는 JSP 또는 서블릿일 수 있습니다. HTML5 양식의 경우 **프로필** 노드는 sling 리소스 및 **프로필 렌더러** 특정 프로필로 모바일 양식을 렌더링하기 위한 요청을 처리하는 sling 스크립트 역할을 합니다. A **프로필 렌더러** 는 요청에서 매개 변수를 읽고 Forms OSGi 서비스를 호출하는 JSP입니다.

REST 엔드포인트 및 지원되는 요청 매개 변수에 대한 자세한 내용은 [양식 템플릿 렌더링](/help/forms/using/rendering-form-template.md).

사용자가 iOS 또는 Android 브라우저와 같은 클라이언트 장치에서 요청을 수행하면 Sling이 먼저 요청 URL을 기반으로 프로필 노드를 확인합니다. 이 프로필 노드에서 **sling:resourceSuperType** 및 **sling:resourceType** 이 양식 렌더링 요청을 처리할 수 있는 사용 가능한 스크립트를 모두 확인하려면 그런 다음 요청 메서드와 함께 Sling 요청 선택기를 사용하여 이 요청을 처리하는 데 가장 적합한 스크립트를 식별합니다. 요청이 프로필 렌더러 JSP에 도달하면 JSP가 Forms OSGi 서비스를 호출합니다.

Sling 스크립트 해상도에 대한 자세한 내용은 [AEM Sling 치트 시트](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html) 또는 [Apache Sling Url 제거](https://sling.apache.org/site/url-decomposition.html).

#### 일반적인 양식 처리 호출 흐름 {#typical-form-processing-call-flow}

HTML5 forms는 첫 번째 요청에서 양식을 처리(변환 또는 제출)하는 데 필요한 모든 중간 개체를 캐시합니다. 이러한 개체가 변경될 가능성이 있으므로 데이터에 종속된 개체를 캐시하지 않습니다.

모바일 양식은 두 가지 서로 다른 수준의 캐시, PreRender 캐시 및 Render 캐시를 유지합니다. preRender 캐시에는 해결된 템플릿의 모든 조각과 이미지가 포함되며 Render 캐시에 HTML과 같은 렌더링된 컨텐츠가 포함됩니다.

![HTML5 양식 워크플로우](assets/cacheworkflow.png)

HTML5 양식 워크플로우

HTML5 양식은 조각 및 이미지에 대한 참조가 누락된 템플릿을 캐시하지 않습니다. HTML5 양식이 일반적인 시간 이상 걸리는 경우 서버 로그에서 누락된 참조 및 경고를 확인합니다. 또한 개체의 최대 크기에 도달하지 않는지 확인합니다.

Forms OSGi 서비스는 요청을 두 단계로 처리합니다.

* **레이아웃 및 초기 양식 상태 생성**: Forms OSGi 렌더링 서비스는 Forms 캐시 구성 요소를 호출하여 양식이 이미 캐시되었으며 무효화되지 않았는지 확인합니다. 양식이 캐시되고 유효한 경우 캐시에서 생성된 HTML을 제공합니다. 양식이 무효화된 경우 Forms OSGi 렌더링 서비스는 XML 형식으로 초기 양식 레이아웃 및 양식 상태를 생성합니다. 이 XML은 Forms OSGi 서비스에 의해 HTML 레이아웃 및 초기 JSON 양식 상태로 변환된 다음 후속 요청에 대해 캐시됩니다.
* **미리 채워진 Forms**: 렌더링 중에 사용자가 미리 채워진 데이터로 양식을 요청하는 경우 Forms OSGi 렌더링 서비스는 Forms 서비스 컨테이너를 호출하고 병합된 데이터가 있는 새 양식 상태를 생성합니다. 그러나 레이아웃은 위의 단계에서 이미 생성되었으므로 이 호출은 첫 번째 호출보다 빠릅니다. 이 호출은 데이터 병합만 수행하고 데이터에 대해 스크립트를 실행합니다.

양식 또는 양식 내에서 사용되는 자산이 업데이트되면 양식 캐시 구성 요소는 이를 감지하고 특정 양식의 캐시가 무효화됩니다. Forms OSGi 서비스 처리가 완료되면 프로필 렌더러 jsp 가 이 양식에 JavaScript 라이브러리 참조 및 스타일을 추가하고 응답을 클라이언트에 반환합니다. 과 같은 일반적인 웹 서버 [Apache](https://httpd.apache.org/) HTML 압축과 함께 여기에서 사용할 수 있습니다. 웹 서버는 서버 및 클라이언트 시스템 간의 데이터를 스트리밍하는 데 필요한 응답 크기, 네트워크 트래픽 및 시간을 크게 줄입니다.

사용자가 양식을 제출하면 브라우저가 양식 상태를 JSON 형식으로 을 [서비스 프록시 제출](../../forms/using/service-proxy.md); 그런 다음 제출 서비스 프록시는 JSON 데이터를 사용하여 데이터 XML을 생성하고 해당 데이터 XML을 제출하여 엔드포인트를 제출합니다.

## 구성 요소 {#components}

HTML5 양식을 활성화하려면 AEM Forms 추가 기능 패키지가 필요합니다. AEM Forms 추가 기능 패키지 설치에 대한 자세한 내용은 [AEM Forms 설치 및 구성](../../forms/using/installing-configuring-aem-forms-osgi.md).

### OSGi 구성 요소(adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA Forms 렌더러(com.adobe.livecycle.adobe-lc-forms-core)** 는 Felix 관리 콘솔의 번들 보기에서 볼 때 HTML5 forms OSGi 번들의 표시 이름입니다(https://).[호스트]:[포트]/system/console/bundles).

이 구성 요소에는 렌더링, 캐시 관리 및 구성 설정을 위한 OSGi 구성 요소가 포함되어 있습니다.

#### Forms OSGi 서비스 {#forms-osgi-service}

이 OSGi 서비스에는 XDP를 HTML으로 렌더링하고 데이터 XML을 생성하기 위해 양식 제출을 처리하는 논리가 포함되어 있습니다. 이 서비스는 Forms 서비스 컨테이너를 사용합니다. Forms 서비스 컨테이너가 내부적으로 기본 구성 요소를 호출합니다 `XMLFormService.exe` 에서 처리를 수행합니다.

렌더링 요청이 수신되면, 이 구성 요소는 Forms 서비스 컨테이너를 호출하여 HTML 및 JSON 양식 DOM 상태를 생성하기 위해 추가로 처리되는 레이아웃 및 상태 정보를 생성합니다.

이 구성 요소는 제출된 양식 상태 JSON에서 데이터 XML을 생성하는 작업도 수행합니다.

#### 캐시 구성 요소 {#cache-component}

HTML5 forms는 캐싱을 사용하여 처리량 및 응답 시간을 최적화합니다. 성능 및 공간 활용률 간의 트레이드오프를 미세 조정하도록 캐시 서비스 수준을 구성할 수 있습니다.

<table>
 <tbody>
  <tr>
   <th>캐시 전략</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>없음</td>
   <td>아티팩트를 캐시하지 않음<br /> </td>
  </tr>
  <tr>
   <td>보수</td>
   <td>인라인 조각 및 이미지가 포함된 템플릿과 같은 양식을 렌더링하기 전에 생성된 중간 가공물만 캐시합니다</td>
  </tr>
  <tr>
   <td>공격적</td>
   <td>렌더링된 HTML 콘텐츠 캐시<br /> 보관 수준에서 캐시된 모든 객체를 캐시합니다.<br /> <strong>참고</strong>: 이 전략은 최상의 성능을 제공하지만 캐시된 객체를 저장하는 데 더 많은 메모리를 사용합니다.</td>
  </tr>
 </tbody>
</table>

HTML5 forms는 LRU 전략을 사용하여 인메모리 캐싱을 수행합니다. 캐시 전략이 없음 캐시로 설정되어 있으면 캐시 데이터가 생성되지 않고 기존 캐시 데이터가 있는 경우 지워집니다. 캐싱 전략 외에, 캐시 크기에 대한 최대 바운드를 가질 수 있고 캐시 리소스를 확보하기 위해 LRU 모드를 사용할 경우 최대 캐시 크기를 가질 수 있는 총 메모리 내 캐시 크기를 구성할 수도 있습니다.

>[!NOTE]
>
>메모리 내 캐시가 클러스터 노드 간에 공유되지 않습니다.

#### 구성 서비스 {#configuration-service}

Configuration Service를 통해 HTML5 양식에 대한 구성 매개 변수와 캐시 설정을 조정할 수 있습니다.

이러한 설정을 업데이트하려면 CQ Felix Admin Console(https://&lt;&#39;에서 사용 가능)로 이동하십시오[server]:[포트]&#39;/system/console/configMgr)에서 모바일 Forms 구성을 검색하고 선택합니다.

구성 서비스를 사용하여 캐시 크기를 구성하거나 캐시를 비활성화할 수 있습니다. 디버그 옵션 매개 변수를 사용하여 디버깅을 활성화할 수도 있습니다. 양식 디버깅에 대한 자세한 내용은 [HTML 5 양식 디버깅](/help/forms/using/debug.md).

### 런타임 구성 요소(adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

런타임 패키지에는 HTML 양식을 렌더링하는 데 사용되는 클라이언트측 라이브러리가 포함되어 있습니다.

**런타임 패키지의 일부로 사용할 수 있는 중요한 구성 요소:**

#### 스크립팅 엔진 {#scripting-engine}

Adobe XFA 구현에서는 양식에서 사용자 정의 로직을 실행할 수 있도록 두 가지 유형의 스크립팅 언어를 지원합니다. JavaScript 및 FormCalc를 참조하십시오.

HTML Forms의 스크립팅 엔진은 두 언어로 XFA 스크립팅 API를 지원하기 위해 JavaScript로 작성됩니다.

렌더링 시 FormCalc 스크립트가 사용자 또는 디자이너에 투명하게 서버의 JavaScript로 번역(및 캐시됨)됩니다.

이 스크립팅 엔진은 Object.defineProperty와 같은 ECMAScript5의 일부 기능을 사용합니다. 엔진/라이브러리는 카테고리 이름을 사용하여 CQ Client Lib으로 전달됩니다 **xfaforms.profile**. 또한 다음을 제공합니다 **FormBridge API** 외부 포털 또는 앱이 양식과 상호 작용할 수 있도록 설정 FormBridge를 사용하는 외부 앱은 프로그래밍 방식으로 특정 요소를 숨기거나, 해당 값을 가져오거나 설정하거나, 속성을 변경할 수 있습니다.

자세한 내용은 [양식 브리지](/help/forms/using/form-bridge-apis.md) 문서.

#### 레이아웃 엔진 {#layout-engine}

HTML5 양식의 레이아웃 및 시각적 측면은 SVG 1.1, jQuery, BackBone 및 CSS3 기능을 기반으로 합니다. 양식의 초기 모양이 생성되어 서버에서 캐시됩니다. 초기 레이아웃의 수정과 양식 레이아웃에 대한 추가 증분 변경 사항은 클라이언트에서 관리됩니다. 이를 위해 런타임 패키지에는 JavaScript로 작성되고 jQuery/Background를 기반으로 하는 레이아웃 엔진이 포함되어 있습니다. 이 엔진은 반복 가능한 인스턴스 추가/제거, 증가 가능한 개체 레이아웃과 같은 모든 동적 동작을 처리합니다. 이 레이아웃 엔진은 양식을 한 번에 한 페이지로 렌더링합니다. 처음에는 사용자가 한 페이지만 보고 가로 스크롤 막대는 첫 번째 페이지에만 적용됩니다. 그러나 사용자가 아래로 스크롤하면 다음 페이지에서 렌더링을 시작합니다. 이 페이지별 렌디션은 브라우저에서 첫 번째 페이지를 렌더링하는 데 필요한 시간을 줄이고, 양식의 인식된 성능을 향상시킵니다. 이 엔진/라이브러리는 범주 이름이 있는 CQ Client Lib의 일부입니다 **xfaforms.profile**.

레이아웃 엔진에는 사용자로부터 양식 필드의 값을 캡처하는 데 사용되는 위젯 세트도 포함되어 있습니다. 이러한 위젯은 다음과 같이 모델링됩니다 [jQuery UI 위젯](https://api.jqueryui.com/jQuery.widget/) 레이아웃 엔진과 원활하게 작동하도록 특정 추가 계약을 구현합니다.

위젯 및 해당 계약에 대한 자세한 내용은 [HTML 5 양식에 대한 사용자 지정 위젯](/help/forms/using/introduction-widgets.md).

#### 스타일링 {#styling}

HTML 요소와 연결된 스타일이 인라인 또는 포함된 CSS 블록을 기반으로 추가됩니다. 양식에 의존하지 않는 일부 일반 스타일은 category name xfaforms.profile이 있는 CQ Client Lib의 일부입니다.

기본 스타일 속성 외에도 각 양식 요소에는 요소 유형, 이름 및 기타 속성을 기반으로 하는 특정 CSS 클래스도 포함되어 있습니다. 이러한 클래스를 사용하면 고유한 CSS를 지정하여 요소를 다시 정렬할 수 있습니다.

기본 스타일 및 클래스에 대한 자세한 내용은 [스타일 소개](/help/forms/using/css-styles.md).

#### 서버측 스크립트 및 웹 서비스 {#server-side-script-and-web-services}

서버에서 실행 상태로 표시되거나 웹 서비스를 호출하도록 표시된 모든 스크립트(실행 대상으로 표시된 위치에 상관없이)는 항상 서버에서 실행됩니다.

클라이언트 스크립트 엔진:

1. 현재 양식 상태를 JSON 형식으로 전달하는 서버에 동기식으로 호출합니다
1. 서버에서 스크립트 또는 웹 서비스를 실행합니다
1. 새 JSON 상태를 생성합니다
1. 응답이 반환되면 클라이언트에서 새 JSON 상태를 병합합니다.

#### 로컬라이제이션 리소스 번들 {#localization-resource-bundles}

HTML5 양식은 이탈리아어(it), 스페인어(es), 포르투갈어(pt_BR), 중국어 간체(zh_CN), 중국어 번체(zh_TW), 한국어(ko_KR), 영어(en_US), 프랑스어(fr_FR), 독일어(de_DE) 및 일본어(ja) 언어를 지원합니다. 요청 헤더에서 받은 로케일에 따라 해당 리소스 번들이 클라이언트로 전송됩니다. 이 리소스 번들은 카테고리 이름을 사용하는 CQ 클라이언트 라이브러리로 프로필 JSP에 추가됩니다 **xfaforms.I18N**. 프로필에서 로케일 패키지를 선택하는 논리를 재정의할 수 있습니다.

### Sling 구성 요소(adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Sling 패키지에는 프로필 및 프로필 렌더러와 관련된 컨텐츠가 들어 있습니다.

#### 프로필 {#profiles}

프로필은 Forms의 양식 또는 제품군을 나타내는 sling의 리소스 노드입니다. CQ 수준에서 이러한 프로필은 JCR 노드입니다. 노드는 **/content** JCR 저장소의 폴더 및 **/content** 폴더를 입력합니다.

#### 프로필 렌더러 {#profile-renderers}

프로필 노드에는 속성이 있습니다 **sling:resourceSuperType** 값 포함 **xfaforms/profile**. 이 속성은 내부적으로 다음 위치에 있는 프로필 노드에 대한 sling 스크립트에 요청을 전송합니다 **/libs/xfaforms/profile** 폴더를 입력합니다. 이러한 스크립트는 HTML 양식과 필요한 JS/CSS 객체를 함께 입력하는 컨테이너인 JSP 페이지입니다. 페이지에 다음에 대한 참조가 포함되어 있습니다.

* **xfaforms.I18N.&lt;locale>**: 이 라이브러리에는 현지화된 데이터가 포함되어 있습니다.
* **xfaforms.profile**: 이 라이브러리에는 XFA 스크립팅 및 레이아웃 엔진에 대한 구현이 포함되어 있습니다.

이러한 라이브러리는 CQ 프레임워크 JavaScript 라이브러리의 자동 연결, 축소 및 압축 기능을 사용하는 CQ 클라이언트 라이브러리로 모델링됩니다.
CQ Client Libs에 대한 자세한 내용은 [CQ Clientlib 설명서](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html).

위에서 설명한 대로 프로필 렌더러 JSP는 sling을 통해 Forms 서비스를 호출합니다. 또한 이 JSP는 관리 구성 또는 요청 매개 변수에 따라 다양한 디버그 옵션을 설정합니다.

HTML5 양식을 사용하면 개발자가 프로필 및 프로필 렌더러를 만들어 양식의 모양을 사용자 지정할 수 있습니다. 예를 들어 HTML 양식을 사용하여 개발자가 패널이나 &lt;div> 기존 HTML 포털의 섹션.
사용자 지정 프로필 만들기에 대한 자세한 내용은 [사용자 지정 프로필 만들기](/help/forms/using/custom-profile.md).
