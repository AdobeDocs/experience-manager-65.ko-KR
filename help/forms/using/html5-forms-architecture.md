---
title: HTML5 양식의 건축
description: HTML5 forms는 임베드된 AEM 인스턴스 내에 패키지로 배포되고 RESTful Apache Sling 아키텍처를 사용하여 HTTP/S에 대한 REST 끝점으로 기능을 노출합니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1976'
ht-degree: 0%

---

# HTML5 양식의 건축{#architecture-of-html-forms}

## 아키텍처 {#architecture}

HTML5 forms 기능은 포함된 AEM 인스턴스 내에 패키지로 배포되고 RESTful을 사용하여 HTTP/S에 대한 REST 끝점으로 표시됩니다 [Apache Sling 아키텍처](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Sling 프레임워크 사용 {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) 는 리소스 중심적입니다. 요청 URL을 사용하여 먼저 리소스를 확인합니다. 각 리소스에는 **sling:resourceType** (또는 **sling:resourceSuperType**) 속성을 사용합니다. 이 속성, 요청 메서드 및 요청 URL의 속성에 따라 요청을 처리할 sling 스크립트가 선택됩니다. 이 슬링 스크립트는 JSP 또는 서블릿일 수 있습니다. HTML5 양식의 경우 **프로필** 노드는 sling 리소스로 작동하며 **프로필 렌더러** 는 특정 프로필로 모바일 양식을 렌더링하도록 요청을 처리하는 sling 스크립트 역할을 합니다. A **프로필 렌더러** 는 요청에서 매개 변수를 읽고 Forms OSGi 서비스를 호출하는 JSP입니다.

REST 끝점 및 지원되는 요청 매개 변수에 대한 자세한 내용은 [렌더링 양식 템플릿](/help/forms/using/rendering-form-template.md).

사용자가 iOS 또는 Android™ 브라우저와 같은 클라이언트 디바이스에서 요청을 수행하면 Sling은 먼저 요청 URL을 기반으로 프로필 노드를 확인합니다. 이 프로필 노드에서 다음을 읽습니다. **sling:resourceSuperType** 및 **sling:resourceType** 이 양식 렌더링 요청을 처리할 수 있는 모든 사용 가능한 스크립트를 결정합니다. 그런 다음 요청 메서드와 함께 Sling 요청 선택기를 사용하여 이 요청을 처리하는 데 가장 적합한 스크립트를 식별합니다. 요청이 프로필 렌더러 JSP에 도달하면 JSP는 Forms OSGi 서비스를 호출합니다.

Sling 스크립트 해상도에 대한 자세한 내용은 [AEM Sling 치트 시트](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko-KR) 또는 [Apache Sling Url 분해](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html).

#### 일반적인 양식 처리 호출 흐름 {#typical-form-processing-call-flow}

HTML5 양식은 첫 번째 요청에서 양식을 처리(렌디션 또는 제출)하는 데 필요한 모든 중간 개체를 캐시합니다. 이러한 개체는 변경될 가능성이 있으므로 데이터에 종속된 개체를 캐시하지 않습니다.

모바일 양식은 PreRender 캐시와 Render Cache, 이렇게 두 가지 수준의 캐시를 유지합니다. PreRender 캐시에는 해결된 템플릿의 모든 조각과 이미지가 포함되어 있으며 Render 캐시에는 HTML 등의 렌더링된 콘텐츠가 포함되어 있습니다.

![HTML 5 양식 워크플로](assets/cacheworkflow.png)

HTML 5 양식 워크플로

HTML 5 양식은 단편 및 이미지에 대한 참조가 누락된 템플릿을 캐시하지 않습니다. HTML5 양식이 일반적인 시간보다 오래 걸리는 경우 서버 로그에서 누락된 참조 및 경고가 있는지 확인하십시오. 또한 개체의 최대 크기에 도달하지 않았는지 확인합니다.

Forms OSGi 서비스는 다음 두 단계로 요청을 처리합니다.

* **레이아웃 및 초기 양식 상태 생성**: Forms OSGi 렌더링 서비스는 Forms 캐시 구성 요소를 호출하여 양식이 이미 캐시되었으며 무효화되지 않았는지 확인합니다. 양식이 캐시되고 유효한 경우 캐시에서 생성된 HTML을 제공합니다. 양식이 무효화된 경우 Forms OSGi 렌더링 서비스는 XML 형식으로 초기 양식 레이아웃 및 양식 상태를 생성합니다. 이 XML은 Forms OSGi 서비스에 의해 HTML 레이아웃 및 초기 JSON 양식 상태로 변환된 다음 후속 요청에 대해 캐시됩니다.
* **미리 채워진 Forms**: 렌더링 중에 사용자가 미리 채워진 데이터가 있는 양식을 요청하면 Forms OSGi 렌더링 서비스가 Forms 서비스 컨테이너를 호출하고 병합된 데이터로 새 양식 상태를 생성합니다. 그러나 레이아웃은 이미 위의 단계에서 생성되었으므로 이 호출은 첫 번째 호출보다 빠릅니다. 이 호출은 데이터 병합만 수행하고 데이터에 대한 스크립트를 실행합니다.

양식에 업데이트가 있거나 양식 내에서 사용된 자산이 있는 경우 양식 캐시 구성 요소가 이를 감지하고 해당 특정 양식에 대한 캐시가 무효화됩니다. Forms OSGi 서비스가 처리를 완료하면 프로필 렌더러 jsp는 JavaScript 라이브러리 참조 및 스타일을 이 양식에 추가하고 응답을 클라이언트에 반환합니다. 다음과 같은 일반적인 웹 서버 [Apache](https://httpd.apache.org/) HTML 압축을 켠 상태로 여기에서 사용할 수 있습니다. 웹 서버는 응답 크기, 네트워크 트래픽 및 서버와 클라이언트 컴퓨터 간에 데이터를 스트리밍하는 데 필요한 시간을 크게 줄일 수 있습니다.

사용자가 양식을 제출하면 브라우저가 JSON 형식의 양식 상태를 로 보냅니다. [서비스 프록시 제출](../../forms/using/service-proxy.md)그런 다음 제출 서비스 프록시는 JSON 데이터를 사용하여 데이터 XML을 생성하고 해당 데이터 XML을 제출하여 끝점을 제출합니다.

## 구성 요소 {#components}

HTML5 양식을 활성화하려면 AEM Forms 추가 기능 패키지가 필요합니다. AEM Forms 추가 기능 패키지 설치에 대한 자세한 내용은 [AEM Forms 설치 및 구성](../../forms/using/installing-configuring-aem-forms-osgi.md).

### OSGi 구성 요소(adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA Forms 렌더러(com.adobe.livecycle.adobe-lc-forms-core)** 는 Felix 관리 콘솔의 번들 보기(https://)에서 볼 때 HTML5 forms OSGi 번들의 표시 이름입니다[호스트]:[포트]/system/console/bundles).

이 구성 요소에는 렌더링, 캐시 관리 및 구성 설정을 위한 OSGi 구성 요소가 포함되어 있습니다.

#### Forms OSGi 서비스 {#forms-osgi-service}

이 OSGi 서비스에는 XDP를 HTML으로 렌더링하는 논리가 포함되어 있으며 데이터 XML을 생성하는 양식 제출을 처리합니다. 이 서비스는 Forms 서비스 컨테이너를 사용합니다. Forms 서비스 컨테이너는 내부적으로 기본 구성 요소를 호출합니다. `XMLFormService.exe` 이 프로세스를 수행합니다.

렌더링 요청이 수신되면 이 구성 요소는 Forms 서비스 컨테이너를 호출하여 HTML 및 JSON 양식 DOM 상태를 생성하기 위해 추가로 처리되는 레이아웃 및 상태 정보를 생성합니다.

이 구성 요소는 제출된 양식 상태 JSON에서 데이터 XML을 생성하는 역할도 합니다.

#### 캐시 구성 요소 {#cache-component}

HTML5 양식은 캐싱을 사용하여 처리량과 응답 시간을 최적화합니다. 캐시 서비스 수준을 구성하여 성능과 공간 사용률 사이의 균형을 세밀하게 조정할 수 있습니다.

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
   <td>보수적</td>
   <td>인라인 조각 및 이미지가 포함된 템플릿과 같이 양식 렌더링 전에 생성된 중간 아티팩트만 캐시합니다.</td>
  </tr>
  <tr>
   <td>공격적</td>
   <td>렌더링된 HTML 컨텐츠 캐시<br /> Conservative 수준에서 캐시된 모든 아티팩트를 캐시합니다.<br /> <strong>참고</strong>: 이 전략은 최상의 성능을 제공하지만 캐시된 아티팩트를 저장하기 위해 더 많은 메모리를 사용합니다.</td>
  </tr>
 </tbody>
</table>

HTML5 형식은 LRU 전략을 사용하여 인메모리 캐싱을 수행합니다. 캐시 전략을 없음으로 설정하면 캐시가 생성되지 않으며 기존 캐시 데이터(있는 경우)가 지워집니다. 캐싱 전략 외에 총 메모리 내 캐시 크기를 구성할 수도 있습니다. 이 경우 캐시 크기에 대한 최대 바인드를 확보하고 이를 초과하면 LRU 모드를 사용하여 캐시 리소스를 확보할 수 있습니다.

>[!NOTE]
>
>클러스터 노드 간에 메모리 내 캐시가 공유되지 않습니다.

#### 구성 서비스 {#configuration-service}

구성 서비스를 통해 HTML 5 양식에 대한 구성 매개 변수 및 캐시 설정을 조정할 수 있습니다.

이러한 설정을 업데이트하려면 CQ Felix Admin Console(https://&lt;&#39;)로 이동하십시오.[server]:[포트]&#39;/system/console/configMgr), 모바일 Forms 구성을 검색하여 선택하십시오.

구성 서비스를 사용하여 캐시 크기를 구성하거나 캐시를 비활성화할 수 있습니다. 디버그 옵션 매개 변수를 사용하여 디버깅을 활성화할 수도 있습니다. 양식 디버깅에 대한 자세한 내용은 [HTML 5 양식 디버깅](/help/forms/using/debug.md).

### 런타임 구성 요소(adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

런타임 패키지에는 HTML 양식을 렌더링하는 데 사용되는 클라이언트측 라이브러리가 포함되어 있습니다.

**런타임 패키지의 일부로 사용할 수 있는 중요한 구성 요소:**

#### 스크립팅 엔진 {#scripting-engine}

Adobe XFA 구현은 JavaScript 및 FormCalc와 같은 양식에서 사용자 정의 논리 실행을 가능하게 하는 두 종류의 스크립팅 언어를 지원합니다.

HTML Forms의 스크립팅 엔진은 두 언어로 XFA 스크립팅 API를 지원하기 위해 JavaScript로 작성되었습니다.

렌더링 시 FormCalc 스크립트는 사용자 또는 디자이너에 영향을 주지 않고 서버의 JavaScript로 번역(및 캐싱)됩니다.

이 스크립팅 엔진은 Object.defineProperty와 같은 ECMAScript5의 기능 중 일부를 사용합니다. 엔진 / 라이브러리는 범주 이름을 사용하는 CQ 클라이언트 라이브러리로 제공됩니다 **xfaforms.profile**. 또한 다음을 제공합니다 **FormBridge API** 외부 포털 또는 앱이 양식과 상호 작용할 수 있도록 합니다. 외부 앱은 FormBridge를 사용하여 프로그래밍 방식으로 특정 요소를 숨기거나, 해당 값을 가져오거나 설정하거나, 특성을 변경할 수 있습니다.

자세한 내용은 [양식 브리지](/help/forms/using/form-bridge-apis.md) 기사.

#### 레이아웃 엔진 {#layout-engine}

HTML5 양식의 레이아웃 및 시각적 측면은 SVG 1.1, jQuery, BackBone 및 CSS3 기능을 기반으로 합니다. 양식의 초기 모습은 서버에서 생성 및 캐시됩니다. 해당 초기 레이아웃의 변경 및 양식 레이아웃에 대한 추가 증분 변경 사항은 클라이언트에서 관리됩니다. 이를 위해 런타임 패키지에는 JavaScript로 작성되고 jQuery/Backbone을 기반으로 하는 레이아웃 엔진이 포함되어 있습니다. 이 엔진은 반복 가능한 인스턴스 추가/제거, 확장 가능한 개체 레이아웃과 같은 모든 동적 동작을 처리합니다. 이 레이아웃 엔진은 한 번에 한 페이지씩 양식을 렌더링합니다. 처음에는 사용자가 한 페이지만 보고 가로 스크롤 막대는 첫 페이지만 처리합니다. 그러나 사용자가 아래로 스크롤하면 다음 페이지가 렌더링을 시작합니다. 이 페이지별 렌디션은 브라우저에서 첫 번째 페이지를 렌더링하는 데 필요한 시간을 줄이고 양식의 인지된 성능을 향상시킵니다. 이 엔진/라이브러리는 범주 이름을 사용하는 CQ 클라이언트 라이브러리의 일부입니다. **xfaforms.profile**.

레이아웃 엔진에는 사용자로부터 양식 필드의 값을 캡처하는 데 사용되는 위젯 세트가 포함되어 있습니다. 이러한 위젯은 [jQuery UI 위젯](https://api.jqueryui.com/jQuery.widget/) 레이아웃 엔진과 원활하게 작동하도록 특정 추가 계약을 구현합니다.

위젯 및 해당 계약에 대한 자세한 내용은 을 참조하십시오. [HTML5 양식에 대한 사용자 정의 위젯](/help/forms/using/introduction-widgets.md).

#### 스타일링 {#styling}

HTML 요소와 연결된 스타일은 인라인이나 포함된 CSS 블록을 기반으로 추가됩니다. 양식에 종속되지 않는 일반적인 스타일 중 일부는 CQ 클라이언트 라이브러리에 포함되어 있으며 카테고리 이름은 xfaforms.profile입니다.

기본 스타일 속성 외에도 각 양식 요소에는 요소 유형, 이름 및 기타 속성을 기반으로 하는 특정 CSS 클래스도 포함됩니다. 이러한 클래스를 사용하면 자체 CSS를 지정하여 요소의 스타일을 변경할 수 있습니다.

기본 스타일 및 클래스에 대한 자세한 내용은 [스타일 소개](/help/forms/using/css-styles.md).

#### 서버측 스크립트 및 웹 서비스 {#server-side-script-and-web-services}

서버에서 실행되도록 표시되거나 웹 서비스를 호출하도록 표시된 스크립트(실행 표시 위치에 상관없이)는 항상 서버에서 실행됩니다.

클라이언트 스크립트 엔진:

1. JSON 형식으로 현재 양식 상태를 전달하는 서버에 대한 동기 호출을 만듭니다.
1. 서버에서 스크립트 또는 웹 서비스를 실행합니다.
1. 새 JSON 상태 생성
1. 응답이 반환되면 클라이언트에서 새 JSON 상태를 병합합니다.

#### 로컬라이제이션 리소스 번들 {#localization-resource-bundles}

HTML5 forms는 이탈리아어(it), 스페인어(es), 포르투갈어(pt_BR), 중국어 간체(zh_CN), 중국어 번체(제한적 지원만)(zh_TW), 한국어(ko_KR), 영어(en_US), 프랑스어(fr_FR), 독일어(de_DE) 및 일본어(ja) 언어를 지원합니다. 요청 헤더에 수신된 로케일을 기반으로 해당 리소스 번들이 클라이언트로 전송됩니다. 이 리소스 번들은 범주 이름을 가진 CQ 클라이언트 라이브러리로 프로필 JSP에 추가됩니다 **xfaforms.I18N**. 프로필에서 로케일 패키지를 선택하는 논리를 재정의할 수 있습니다.

### Sling 구성 요소(adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Sling 패키지에는 프로필 및 프로필 렌더러와 관련된 콘텐츠가 포함되어 있습니다.

#### 프로필 {#profiles}

프로필은 양식 또는 Forms 제품군을 나타내는 sling의 리소스 노드입니다. CQ 수준에서 이러한 프로필은 JCR 노드입니다. 노드는 **/content** JCR 저장소의 폴더이며, **/content** 폴더를 삭제합니다.

#### 프로필 렌더러 {#profile-renderers}

프로필 노드에는 속성이 있습니다. **sling:resourceSuperType** 값 포함 **xfaforms/profile**. 이 속성은 내부적으로 의 프로필 노드에 대한 sling 스크립트로 전달 요청을 보냅니다. **/libs/xfaforms/profile** 폴더를 삭제합니다. 이러한 스크립트는 HTML 양식 및 필수 JS/CSS 아티팩트를 결합하기 위한 컨테이너인 JSP 페이지입니다. 이 페이지에는 다음에 대한 참조가 포함되어 있습니다.

* **xfaforms.I18N.&lt;locale>**: 이 라이브러리에는 지역화된 데이터가 포함되어 있습니다.
* **xfaforms.profile**: 이 라이브러리에는 XFA 스크립팅 및 레이아웃 엔진에 대한 구현이 포함되어 있습니다.

이러한 라이브러리는 CQ 프레임워크 JavaScript 라이브러리의 자동 연결, 축소 및 압축 기능을 활용하는 CQ 클라이언트 라이브러리로 모델링됩니다.
CQ 클라이언트 라이브러리에 대한 자세한 내용은 [CQ Clientlib 설명서](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko-KR).

위에서 설명한 바와 같이, 프로필 렌더러 JSP는 슬링 인포드를 통해 Forms 서비스를 호출한다. 또한 이 JSP는 관리자 구성 또는 요청 매개 변수에 따라 다양한 디버그 옵션을 설정합니다.

HTML5 양식을 사용하면 개발자가 프로필 및 프로필 렌더러를 만들어 양식의 모양을 사용자 지정할 수 있습니다. 예를 들어 HTML 양식을 사용하여 개발자는 패널에 양식을 통합하거나 &lt;div> 기존 HTML 포털의 섹션입니다.
사용자 지정 프로필 만들기에 대한 자세한 내용은 [사용자 지정 프로필 만들기](/help/forms/using/custom-profile.md).
