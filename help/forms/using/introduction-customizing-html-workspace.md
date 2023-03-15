---
title: AEM 양식 작업 공간 사용자 지정 소개
seo-title: Introduction to Customizing AEM form workspace
description: 프로세스 관리를 위해 AEM Forms 작업 공간을 사용자 지정하는 개념 및 기술 정보를 포함한 빠른 소개.
seo-description: A quick introduction, with conceptual and technical information, to customize LiveCycle AEM Forms workspace for process management.
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# AEM 양식 작업 공간 사용자 지정 소개{#introduction-to-customizing-aem-form-workspace}

AEM 양식 작업 공간에서는 인터페이스의 프레젠테이션 의미 체계와 기능을 수정하는 기능을 제공합니다. 스타일, 레이아웃, 서식, 브랜딩 및 핵심 기능을 변경하는 사용자 지정 유형은 아래에 설명되어 있습니다.

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

사용자 지정된 작업 공간의 예

## 사용자 지정 유형 {#types-of-customizations}

AEM Forms 작업 공간에서는 사용자 인터페이스의 레이아웃, 모양, 기능 등을 업데이트할 수 있는 다양한 사용자 지정을 지원합니다. 사용자 지정에는 다음 중 하나 이상을 업데이트하는 작업이 포함됩니다.

* 사용자 인터페이스의 표시
* 의미 체계 사용자 지정을 사용하는 기능
* 다른 애플리케이션에서 HTML 구성 요소 재사용

### 사용자 인터페이스 변경 사항 {#user-interface-changes}

AEM Forms 작업 공간의 모양, 레이아웃 및 기타 프레젠테이션 의미 체계를 변경할 수 있습니다. CSS, HTML 템플릿 및 JavaScript™ 파일을 사용자 지정하여 작업 영역을 변경합니다. 기본 설치에는 모든 기본 파일이 제공됩니다.

가장 일반적으로 적용 가능한 단계는 [AEM Forms 작업 공간 사용자 지정을 위한 일반 단계](../../forms/using/generic-steps-html-workspace-customization.md). 자세한 단계를 비롯한 이러한 사용자 지정 예에 대한 자세한 내용은 이 문서의 끝에 있는 관련 문서를 참조하십시오.

#### 스타일 시트 이해 {#understanding-the-style-sheet}

작업 공간을 사용자 지정하기 전에 /libs/ws/css/style.css에서 AEM Forms에 제공된 기본 스타일 시트 를 숙지하십시오.

작업 영역을 사용자 지정하려면 /libs/ws/css 폴더에 있는 기존 스타일 시트 style.css를 잘 알고 있는 것이 좋습니다. 몇 가지 주목할 만한 구성 요소가 아래에 설명되어 있습니다.

<table>
 <tbody>
  <tr>
   <th><p>CSS 요소</p> </th>
   <th><p>사용자 인터페이스 구성 요소가 수정됨</p> </th>
  </tr>
  <tr>
   <td><p>#머리글</p> </td>
   <td><p>AEM Forms 작업 공간 헤더</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>범주 목록</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>카테고리 목록 머리글</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>범주 목록 아래의 스페이스</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>범주</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>선택한 범주 및 마우스를 범주 스타일 위로 가져갑니다.</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar.tool, categoryListBar.content</p> </td>
   <td><p>프로세스 시작 페이지(닫힌 범주 목록)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar.tool, filterListBar.content</p> </td>
   <td><p>할 일 페이지(닫힌 필터 목록)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar.tool, processNameListBar.content</p> </td>
   <td><p>추적 페이지(닫힌 프로세스 이름 목록)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>시작 지점 목록 또는 작업 목록</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>시작 지점 목록 또는 작업 목록의 헤더</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>선택한 시작점 또는 작업</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected.description, .task.selected.description</p> </td>
   <td><p>선택한 시작점 또는 작업에 대한 설명</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>작업 영역</p> </td>
  </tr>
  <tr>
   <td><p>#header .드롭다운</p> </td>
   <td><p>헤더의 사용자 드롭다운</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop ul</p> </td>
   <td><p>작업 정렬 드롭다운</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

AEM Forms 작업 영역의 모양은 CSS에서 모양을 차용합니다. CSS를 사용자 지정하여 글꼴, 색상, 브랜딩 및 레이아웃과 같은 작업 영역의 표시 의미 체계를 변경할 수 있습니다.

CSS 사용자 지정을 위한 최상위 단계는 다음과 같습니다.

* CSS 파일을 만듭니다.
* 이 CSS에 스타일 항목을 추가합니다. 자세한 내용은 CSS 스타일 이해 를 참조하십시오.
* 에서 해당 참조를 업데이트합니다 `html.jsp`.

이러한 사용자 지정을 수행하는 정확한 단계는 다음을 참조하십시오 [AEM Forms 작업 공간 사용자 지정을 위한 일반 단계](../../forms/using/generic-steps-html-workspace-customization.md). AEM Forms 작업 공간과 함께 제공되는 CSS 파일은 /libs/ws/css/에 있습니다. CSS 관련 사용자 지정의 경우 [배송 패키지](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). CSS 관련 사용자 정의에 대한 특정 예는 이 문서의 끝에 있는 관련 도움말 항목을 참조하십시오.

#### 이미지 {#image}

AEM Forms 작업 공간을 사용자 지정하여 사용자 아바타를 추가하거나 조직의 로고를 추가할 수 있습니다. 이러한 사용자 지정의 경우 [배송 패키지](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

이미지 사용자 지정에 대한 최상위 단계는 다음과 같습니다.

* WebDAV를 설치 및 구성합니다.
* 새 이미지를 추가합니다.
* 추가된 이미지에 해당하는 새 스타일을 추가합니다.
* 의 새 CSS 파일에 연결 `html.jsp` 파일.

AEM Forms 작업 영역에서 이미지 사용자 지정을 시작하려면 다음을 수행하십시오. [AEM Forms 작업 공간 사용자 지정을 위한 일반 단계](../../forms/using/generic-steps-html-workspace-customization.md). 이미지 관련 사용자 정의에 대한 특정 예는 이 문서의 끝에 있는 관련 도움말 항목을 참조하십시오.

#### HTML 템플릿 {#html-template}

HTML 템플릿은 작업 공간 사용자 인터페이스의 모양 및 레이아웃을 정의하는 데 도움이 됩니다. 기본 HTML 템플릿을 업데이트하여 레이아웃 기본 사용자 인터페이스를 사용자 지정할 수 있습니다.

HTML 템플릿 사용자 지정에 대한 최상위 단계는 다음과 같습니다.

* 사용자가 만든 폴더에서 필요한 기본 파일의 복사본을 만듭니다.
* 사용자 정의 폴더에 새 템플릿을 추가합니다.
* 복사된 파일 경로(예: 새 템플릿의 경로)에 대한 관련 업데이트를 수행합니다.

이러한 사용자 정의에 대한 특정 예는 이 문서의 끝에 제공된 도움말 항목을 참조하십시오. 다음 중 하나를 선택합니다 [배송 패키지](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) 또는 [개발 패키지](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)사용자 지정할 템플릿에 따라 다릅니다.

### 시맨틱 변경 {#semantic-changes}

AEM Forms 작업 공간 기능을 수정하려면 JavaScript 소스 코드를 변경합니다. 핵심 기능의 수정 사항은 의미 체계 변경이라고 레이블이 지정됩니다. AEM Forms 작업 공간의 소스 코드의 일부로 제공된 모델, 보기 및 템플릿을 수정합니다.

AEM Forms 작업 영역의 기능을 수정하기 위해 시맨틱 변경을 수행하는 최상위 단계는 다음과 같습니다.

* 사용자가 만든 폴더에서 적절한 기본 파일의 복사본을 만듭니다.
* 사용자 정의 폴더에 새 모델과 보기를 추가합니다.
* 기본 JavaScript 파일에서 새로 추가된 모델 및 보기의 경로를 업데이트하는 것과 같은 관련 업데이트를 만듭니다.
* 패키지를 축소하여 성능을 최적화합니다.

소스 코드에 포함된 구성 요소에 대한 자세한 내용은 [재사용 가능한 구성 요소에 대한 설명](/help/forms/using/description-reusable-components.md). 이러한 사용자 지정의 경우 개발 패키지를 사용하십시오.

### 재사용 가능한 구성 요소 {#reusable-components}

AEM Forms 작업 공간은 구성 요소 기반 소프트웨어이므로 쉽게 사용자 지정하고 다시 사용할 수 있습니다. 작업 공간 구성 요소를 웹 애플리케이션과 쉽게 통합할 수 있습니다.

개념적 정보에 대해서는 [재사용 가능한 구성 요소에 대한 설명](/help/forms/using/description-reusable-components.md) 구성 요소 사용에 대한 자세한 내용은 [웹 애플리케이션에서 AEM Forms 작업 공간 구성 요소 통합](/help/forms/using/description-reusable-components.md).

## AEM Forms 작업 공간 코드 작성 {#building-html-workspace-code}

### SDK 패키지 {#sdk-package}

패키지에는 AEM Forms 작업 공간의 소스 코드가 들어 있습니다. 패키지는 `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

다음을 생성하는 기능을 제공하므로 주로 사용자 지정을 위한 것입니다.

* 배송, 디버그 및 개발 프로필에 대한 CRX 패키지(아래에 언급됨)에서 [CRX 패키지](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* 사용자 지정 코드의 축소된 버전(의미 체계 변경).

#### WS 콘텐츠 {#ws-content}

* client-pkg:

   * src - CRX 노드를 만드는 데 필요한 아티팩트가 포함되어 있습니다.
   * pom.xml - 다양한 프로필용 패키지를 배포하기 위한 스크립트 WS-Deploy 패키지

* client-html:

   * 어셈블리 - AEM Forms 작업 공간 SDK를 만드는 스크립트에서 사용하는 zip.xml을 포함합니다.
   * src/main/webapp -

      * css - AEM Forms 작업 영역의 스타일 시트를 포함합니다.
      * 이미지 - AEM Forms 작업 공간에서 사용되는 이미지를 포함합니다.
      * js:

         * libs - AEM Forms 작업 공간에 사용되는 모든 타사 라이브러리를 포함합니다.
         * 라이센스 - HTML 및 JS 파일에 대한 라이센스와 이러한 라이센스를 각 소스 파일에 접두사로 추가할 코드를 포함합니다.
         * minifier - 사용자 지정된 JavaScript 코드의 조합, 축소 및 통합에 사용됩니다.
         * resourcejs_optimizer - JavaScript 소스의 조합, 축소 및 통합에 사용됩니다.
         * resource_generator - register.js 및 modelcontrollerpath.js를 생성하는 데 사용됩니다.
         * 런타임:

            * 이니셜라이저 - AEM Forms 작업 공간에 사용되는 백본 및 모델을 초기화하는 데 사용되는 initializer.js가 포함되어 있습니다.
            * 모델 - AEM Forms 작업 공간에 있는 모든 구성 요소의 백본 모델을 포함합니다.
            * 경로 - AEM Forms 작업 영역의 시작 프로세스, todo, tracking 및 환경 설정을 로드하는 JavaScript 파일 및 HTML 파일을 포함합니다.
            * 서비스 - AEM Forms 작업 공간에 사용되는 service.js를 포함합니다. 모든 서버 호출은 service.js를 통해 수행됩니다.
            * 템플릿 - AEM Forms 작업 공간에 있는 모든 보기의 HTML 파일, 즉 모든 템플릿을 포함합니다.
            * util - AEM Forms 작업 영역에서 사용되는 모든 유틸리티 파일(javascript)을 포함합니다.
            * 보기 - AEM Forms 작업 공간에 있는 모든 구성 요소의 백본 보기를 포함합니다.
         * main.js
         * router.js
      * libs/ws: pdf.html 및 pluginPing.pdf 는 AEM Forms 작업 공간에서 PDF forms을 로드하는 데 사용되며 WSNextAdapter.swf는 AEM Forms 작업 영역에서 SWF 양식 및 안내서를 로드하는 데 사용됩니다.
      * 로케일:

         * de-DE - 독일어용 translation.json을 포함합니다.
         * en-US - 영어로 translation.json을 포함합니다.
         * fr-FR - 프랑스어용 translation.json을 포함합니다.
         * ja-JP - 일본어 translation.json을 포함합니다.
         * html.jsp - 현재 브라우저 로케일을 찾는 코드를 포함합니다.
      * html.jsp
      * GET.jsp




### CRX 패키지 {#crx-package}

CRX 패키지는 CRX™ 저장소에 배포할 수 있습니다. 다음 위치에서 사용 가능합니다 `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

이 패키지는 아래에 설명된 세 가지 프로필을 사용하여 작성할 수 있습니다.

| **프로필** | **설명** | **사용량** |
|---|---|---|
| 출하 프로파일 | 이 프로필은 축소를 사용하여 가능한 가장 작은 크기의 CRX 패키지를 만듭니다. 이 패키지가 가장 효율적입니다. 모든 JavaScript™ 파일이 결합되고 단일 JS 파일로 축소됩니다. | JS 파일에 더 이상 의미 있는 변경이 필요하지 않으면 이 프로필을 사용하십시오. |
| 프로필 디버그 | 이 프로필은 비교적 효율적인 CRX 패키지를 만듭니다. 패키지 크기가 배송 프로필을 사용하여 만든 패키지보다 약간 큽니다. 이 패키지에는 대부분의 JavaScript 파일이 단일 JS 파일에 결합되어 있습니다. | 디버깅을 위해 이 프로필을 사용합니다. |
| 개발 프로필 | 이 프로필은 가능한 가장 큰 크기의 CRX 패키지를 만듭니다. 모든 JavaScript 파일은 SDK 패키지에 있으므로 별도로 사용할 수 있습니다. | 의미 변경 사항을 통합할 때 이 프로필을 사용하십시오. |

#### 출하 프로파일 {#ship-profile}

#### Command {#command}

* mvn clean -P 클라이언트로 제공된 소스 패키지의 클라이언트-pkg 폴더에 배송 설치
* 출하 프로필 명령 실행은 64비트 JVM에서만 작동합니다.

#### WS 콘텐츠 {#ws-content-1}

* css - style.css, ie.css 및 jquery-ui.css를 포함합니다.
* 이미지 - 모든 이미지를 포함합니다.
* js:

   * libs:

      * 필요 - require.js를 포함합니다.
      * jqueryui - jquery.ui.datepicker.ja.js을 포함합니다.
   * 런타임:

      * 템플릿 - AEM Forms 작업 공간에 있는 모든 구성 요소의 HTML 파일, 즉 모든 템플릿을 포함합니다.
   * main.js(결합, 축소 및 확장).
   * registry.js



* libs:

   * ws - pluginPing.pdf, pdf.html 및 WSNextAdapter.swf를 포함합니다.

* Locale - .content.xml을 포함합니다.
* 로케일:

   * de-DE - 독일어용 translation.json을 포함합니다.
   * en-US - 영어로 translation.json을 포함합니다.
   * fr-FR - 프랑스어용 translation.json을 포함합니다.
   * ja-JP - 일본어 translation.json을 포함합니다.
   * html.jsp - 현재 브라우저 로케일을 찾는 코드를 포함합니다.

* 인덱스 - .content.xml 포함
* profile - offline.jsp를 포함합니다.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 디버그 프로필 {#debug-profile}

#### Command {#command-1}

* mvn clean -P Debug가 클라이언트-pkg에 설치됨
* 디버그 프로필 명령 실행은 64비트 JVM에서만 작동합니다.

#### WS 콘텐츠 {#ws-content-2}

* css - style.css, ie.css 및 jqueri-ui.css를 포함합니다.
* 이미지 - 모든 이미지를 포함합니다.
* js:

   * libs:

      * 필요 - require.js를 포함합니다.
      * jqueryui - jquery.ui.datepicker.ja.js을 포함합니다.
   * 런타임:

      * 템플릿 - AEM Forms 작업 공간에 있는 모든 구성 요소의 HTML 파일, 즉 모든 템플릿을 포함합니다.
   * main.js(결합).
   * registry.js



* libs:

   * ws - pluginPing.pdf, pdf.html 및 WSNextAdapter.swf를 포함합니다.

* Locale - .content.xml을 포함합니다.
* 로케일:

   * de-DE - 독일어용 translation.json을 포함합니다.
   * en-US - 영어로 translation.json을 포함합니다.
   * fr-FR - 프랑스어용 translation.json을 포함합니다.
   * ja-JP - 일본어 translation.json을 포함합니다.
   * html.jsp - 현재 브라우저 로케일을 찾는 코드를 포함합니다.

* 인덱스 - .content.xml 포함
* profile - offline.jsp를 포함합니다.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 개발 프로필 {#dev-profile}

#### Command {#command-2}

mvn clean -P 개발 설치를 클라이언트-pkg에 설치

#### WS 콘텐츠 {#ws-content-3}

* css - style.css, ie.css 및 jqueri-ui.css를 포함합니다.
* 이미지 - 모든 이미지를 포함합니다.
* js:

   * libs - AEM Forms 작업 공간에 사용되는 모든 라이브러리를 포함합니다.
   * 필요 - require.js 포함
   * jqueryui - jquery.ui.datepicker.ja.js 포함
   * 런타임:

      * initializer - initializer.js 및 modelcontrollerpath.js를 포함합니다.
      * 모델 - AEM Forms 작업 공간에 있는 모든 구성 요소의 모델을 포함합니다.
      * 경로 - AEM Forms 작업 영역의 시작 프로세스, todo, tracking 및 환경 설정을 로드하는 JavaScript 파일 및 HTML 파일을 포함합니다.
      * 서비스 - AEM Forms 작업 공간에 사용되는 service.js를 포함합니다.
      * 템플릿 - AEM Forms 작업 공간에 있는 모든 구성 요소의 HTML 파일, 즉 모든 템플릿을 포함합니다.
      * util - AEM Forms 작업 영역에서 사용되는 모든 유틸리티 파일(JavaScript)을 포함합니다.
      * 보기 - AEM Forms 작업 공간의 모든 구성 요소 보기를 포함합니다.
   * main.js
   * registry.js
   * router.js


* libs:

   * ws - pluginPing.pdf, pdf.html 및 WSNextAdapter.swf를 포함합니다.

* Locale - .content.xml을 포함합니다.
* 로케일:

   * de-DE - 독일어용 translation.json을 포함합니다.
   * en-US - 영어로 translation.json을 포함합니다.
   * fr-FR - 프랑스어용 translation.json을 포함합니다.
   * ja-JP - 일본어 translation.json을 포함합니다.
   * html.jsp - 현재 브라우저 로케일을 찾는 코드를 포함합니다.

* 인덱스 - .content.xml 포함
* profile - offline.jsp를 포함합니다.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
