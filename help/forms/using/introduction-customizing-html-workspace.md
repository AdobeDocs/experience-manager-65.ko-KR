---
title: AEM 양식 작업 영역 사용자 지정 소개
seo-title: AEM 양식 작업 영역 사용자 지정 소개
description: 프로세스 관리를 위해 LiveCycle AEM Forms 작업 영역을 사용자 정의하는 개념 및 기술 정보가 포함된 빠른 소개
seo-description: 프로세스 관리를 위해 LiveCycle AEM Forms 작업 영역을 사용자 정의하는 개념 및 기술 정보가 포함된 빠른 소개
uuid: 38759071-e6b8-4976-8b06-909ad7a786cd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 021c6606-8cd3-472c-a80b-b1bcace7e87f
docset: aem65
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 0%

---


# AEM 양식 작업 영역 사용자 지정 소개{#introduction-to-customizing-aem-form-workspace}

AEM 양식 작업 공간에서는 인터페이스의 프레젠테이션 의미론 및 기능을 수정하는 기능을 제공합니다. 스타일, 레이아웃, 서식, 브랜딩 및 핵심 기능을 변경하기 위한 사용자 정의 유형은 아래에 설명되어 있습니다.

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

사용자 정의된 작업 영역의 예

## 사용자 정의 유형 {#types-of-customizations}

AEM Forms 작업 영역은 유저 인터페이스의 레이아웃, 모양, 기능 등을 업데이트하기 위해 다양한 사용자 정의 설정을 지원합니다. 사용자 지정에는 다음 중 하나 이상을 업데이트하는 작업이 포함됩니다.

* 사용자 인터페이스의 모양
* 의미 체계 사용자 지정을 사용하는 기능
* 다른 애플리케이션에서 HTML 구성 요소 재사용

### 유저 인터페이스 변경 {#user-interface-changes}

AEM Forms 작업 영역의 모양, 레이아웃 및 기타 프레젠테이션 의미론을 변경할 수 있습니다. CSS, HTML 템플릿 및 JavaScript™ 파일을 사용자 정의하여 작업 영역을 변경할 수 있습니다. 모든 기본 파일은 기본 설치에서 제공됩니다.

가장 일반적으로 적용할 수 있는 단계는 AEM Forms 작업 공간 사용자 지정을 위한 [일반 단계입니다](../../forms/using/generic-steps-html-workspace-customization.md). 세부 단계를 비롯한 이러한 사용자 지정 예제에 대한 자세한 내용은 이 문서의 후반부에 있는 관련 문서를 참조하십시오.

#### 스타일 시트 이해 {#understanding-the-style-sheet}

작업 영역을 사용자 정의하기 전에 /libs/ws/css/style.css에서 AEM Forms과 함께 제공되는 기본 스타일 시트를 잘 알고 있어야 합니다.

작업 영역을 사용자 정의하려면 /libs/ws/css 폴더에 있는 기존 스타일 시트 style.css에 익숙해지는 것이 좋습니다. 몇 가지 중요한 구성 요소가 아래에 설명되어 있습니다.

<table>
 <tbody>
  <tr>
   <th><p>CSS 요소</p> </th>
   <th><p>사용자 인터페이스 구성 요소 수정됨</p> </th>
  </tr>
  <tr>
   <td><p>#머리글</p> </td>
   <td><p>AEM Forms 작업 공간의 헤더</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>범주 목록</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>범주 목록 머리글</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>범주 목록 아래의 공간</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>카테고리</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>선택한 카테고리 및 마우스가 카테고리 스타일 위에 있음</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar.content</p> </td>
   <td><p>프로세스 시작 페이지(닫힌 카테고리 목록)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar.content</p> </td>
   <td><p>할 일 페이지(닫힌 필터 목록)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
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
   <td><p>선택한 시작 지점 또는 작업</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected .description, .task.selected.description</p> </td>
   <td><p>선택한 시작 지점 또는 작업에 대한 설명</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>작업 영역</p> </td>
  </tr>
  <tr>
   <td><p>#header .dropdown</p> </td>
   <td><p>헤더의 사용자 드롭다운</p> </td>
  </tr>
  <tr>
   <td><p>.sort삭제 ul</p> </td>
   <td><p>정렬 작업 드롭다운</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

AEM Forms 작업 영역의 모양은 CSS에서 차용됩니다. CSS를 사용자 정의함으로써 글꼴, 색상, 브랜딩 및 레이아웃과 같은 작업 영역의 프레젠테이션 의미론을 변경할 수 있습니다.

CSS 사용자 지정을 위한 최상위 단계는 다음과 같습니다.

* CSS 파일을 만듭니다.
* 이 CSS에 스타일 항목을 추가합니다. 자세한 내용은 CSS 스타일 이해를 참조하십시오.
* 에서 해당 참조를 업데이트합니다 `html.jsp`.

이러한 사용자 지정을 수행하는 정확한 단계는 AEM Forms 작업 공간 사용자 지정을 위한 [일반 단계를 참조하십시오](../../forms/using/generic-steps-html-workspace-customization.md). AEM Forms 작업 영역과 함께 제공되는 CSS 파일은 /libs/ws/css/입니다. CSS 관련 사용자 지정의 경우 [배송 패키지를 사용하십시오](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). CSS 관련 사용자 정의에 대한 특정 예제는 이 문서의 끝 부분에 있는 관련 도움말 항목을 참조하십시오.

#### 이미지 {#image}

AEM Forms 작업 영역을 사용자 지정하여 사용자 아바타를 추가하거나 조직의 로고를 추가할 수 있습니다. 이러한 사용자 설정의 경우 [배송 패키지를 사용하십시오](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

이미지에 대한 사용자 지정을 위한 최상위 단계는 다음과 같습니다.

* WebDAV 설치 및 구성
* 새 이미지 추가
* 추가된 이미지에 해당하는 새 스타일을 추가합니다.
* 파일의 새로운 CSS 파일에 `html.jsp` 연결합니다.

AEM Forms 작업 영역에서 이미지 사용자 지정을 시작하려면 AEM Forms 작업 공간 사용자 지정을 위한 [일반 단계를 따르십시오](../../forms/using/generic-steps-html-workspace-customization.md). 이미지 관련 사용자 지정 예제에 대한 자세한 내용은 이 문서의 후반부에 있는 관련 도움말 항목을 참조하십시오.

#### HTML 템플릿 {#html-template}

HTML 템플릿을 사용하면 작업 공간 사용자 인터페이스의 모양과 레이아웃을 정의할 수 있습니다. 기본 HTML 템플릿을 업데이트하여 레이아웃 기본 사용자 인터페이스를 사용자 정의할 수 있습니다.

HTML 템플릿 사용자 지정에 대한 최상위 단계는 다음과 같습니다.

* 사용자가 만든 폴더에서 필요한 기본 파일의 복사본을 만듭니다.
* 사용자 정의 폴더에 새 템플릿을 추가합니다.
* 새 템플릿의 경로와 같이 복사한 파일에 대한 관련 업데이트를 만듭니다.

이러한 사용자 지정 예제에 대한 자세한 내용은 이 문서의 마지막에 제공되는 도움말 항목을 참조하십시오. 사용자 정의할 템플릿에 따라 [배송 패키지](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) 또는 [개발 패키지](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)중에서 선택합니다.

### 의미 변경 {#semantic-changes}

AEM Forms 작업 공간 기능을 수정하려면 JavaScript 소스 코드를 변경합니다. 핵심 기능의 수정 사항은 의미 체계 변경 사항으로 레이블이 지정됩니다. AEM Forms 작업 공간의 소스 코드의 일부로 제공되는 모델, 뷰 및 템플릿을 수정할 수 있습니다.

AEM Forms 작업 공간의 기능을 수정하기 위해 의미 변경을 수행하는 최상위 단계는 다음과 같습니다.

* 사용자가 만든 폴더에서 해당 기본 파일의 복사본을 만듭니다.
* 사용자 정의 폴더에 새 모델과 뷰를 추가합니다.
* 기본 JavaScript 파일에서 새롭게 추가된 모델 및 보기의 경로 업데이트와 같은 관련 업데이트를 수행합니다.
* 성능을 최적화할 패키지를 축소합니다.

소스 코드에 포함된 구성 요소에 대한 자세한 내용은 재사용 가능한 구성 요소 [설명을 참조하십시오](/help/forms/using/description-reusable-components.md). 이러한 사용자 정의에 대해서는 개발 패키지를 사용하십시오.

### 재사용 가능한 구성 요소 {#reusable-components}

AEM Forms 작업 공간은 구성 요소 기반 소프트웨어이므로 손쉽게 사용자 정의 및 재사용할 수 있습니다. 작업 영역 구성 요소를 웹 애플리케이션과 손쉽게 통합할 수 있습니다.

개념적인 정보는 재사용 가능한 구성 요소 [에 대한 설명](/help/forms/using/description-reusable-components.md) 및 구성 요소 사용에 대한 지침은 웹 응용 프로그램에서 AEM Forms 작업 영역 [구성 요소 통합을 참조하십시오](/help/forms/using/description-reusable-components.md).

## AEM Forms 작업 공간 코드 작성 {#building-html-workspace-code}

### SDK 패키지 {#sdk-package}

패키지에는 AEM Forms 작업 영역의 소스 코드가 들어 있습니다. 소포는 에서 사용할 수 있습니다 `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

기본적으로 다음을 생성하는 기능을 제공하므로 사용자 지정을 위한 것입니다.

* 배송, 디버그 및 개발 프로파일에 대한 CRX 패키지( [CRX 패키지에](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)아래 참조).
* 사용자 지정된 코드의 축소 버전(의미 체계 변경).

#### WS 컨텐츠 {#ws-content}

* client-pkg:

   * src - CRX 노드를 만드는 데 필요한 결함을 포함합니다.
   * pom.xml - 다양한 프로필 WS-Deploy 패키지의 배포 패키지를 빌드하는 스크립트

* client-html:

   * 어셈블리 - AEM Forms 작업 공간 SDK를 만드는 스크립트에서 사용하는 zip.xml을 포함합니다.
   * src/main/webapp -

      * css - AEM Forms 작업 영역에 대한 스타일 시트를 포함합니다.
      * 이미지 - AEM Forms 작업 영역에 사용되는 이미지를 포함합니다.
      * js:

         * libs - AEM Forms 작업 공간에 사용된 모든 타사 라이브러리를 포함합니다.
         * 라이선스 - HTML 및 JS 파일에 대한 라이선스와 각 소스 파일에 이러한 라이선스에 대한 접두사를 추가할 수 있는 코드를 포함합니다.
         * minifier - customizedJavaScript 코드의 조합, 축소 및 인증에 사용됩니다.
         * resourcejs_optimizer - JavaScript 소스의 조합, 축소 및 통합에 사용됩니다.
         * resource_generator - register.js 및 modelcontrolerpath.js를 생성하는 데 사용됩니다.
         * 런타임:

            * 이니셜라이저 - AEM Forms 작업 공간에 사용된 백본 및 모델을 초기화하는 데 사용되는 이니셜라이저.js를 포함합니다.
            * 모델 - AEM Forms 작업 공간에 있는 모든 구성 요소의 백본 모델을 포함합니다.
            * 경로 - AEM Forms 작업 영역의 시작 프로세스, 수행할 작업, 추적 및 환경 설정을 로드하는 HTML 파일과 JavaScript 파일이 들어 있습니다.
            * 서비스 - AEM Forms 작업 공간에 사용되는 service.js를 포함합니다. 모든 서버 호출은 service.js를 통해 수행됩니다.
            * 템플릿 - 모든 템플릿, 즉 AEM Forms 작업 영역에서 모든 보기의 HTML 파일을 포함합니다.
            * util - AEM Forms 작업 공간에 사용되는 모든 유틸리티 파일(javascript)을 포함합니다.
            * 보기 - AEM Forms 작업 영역의 모든 구성 요소에 대한 백본 보기를 포함합니다.
         * main.js
         * router.js
      * libs/ws: pdf.html 및 pluginPing.pdf는 AEM Forms 작업 영역에서 PDF forms을 로드하는 데 사용되고 WSNextAdapter.swf는 AEM Forms 작업 공간에서 SWF 양식 및 안내선을 로드하는 데 사용됩니다.
      * locales:

         * de-DE - 독일어용 translation.json을 포함합니다.
         * en-US - 영어에 대한 translation.json을 포함합니다.
         * fr-FR - 프랑스어용 translation.json 포함
         * ja-JP - 일본어용 translation.json을 포함합니다.
         * html.jsp - 현재 브라우저 로케일을 찾는 코드를 포함합니다.
      * html.jsp
      * GET.jsp




### CRX 패키지 {#crx-package}

CRX 패키지는 CRX™ 저장소에 배포할 수 있습니다. 은 에서 사용할 수 있습니다 `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

이 패키지는 아래 설명된 세 가지 프로필을 사용하여 빌드할 수 있습니다.

| **프로필** | **설명** | **사용량** |
|---|---|---|
| 출하 프로파일 | 이 프로파일은 미니화를 사용하여 가능한 가장 작은 크기의 CRX 패키지를 만듭니다. 이 소포가 가장 효율적입니다 모든 JavaScript™ 파일이 결합되어 단일 JS 파일로 축소됩니다. | JS 파일에 더 이상 의미 체계 변경이 필요하지 않은 경우 이 프로필을 사용하십시오. |
| 디버그 프로필 | 이 프로파일은 적당히 효율적인 CRX 패키지를 생성합니다. 패키지의 크기가 배송 프로필을 사용하여 만든 패키지보다 약간 큽니다. 이 패키지에는 단일 JS 파일로 결합된 대부분의 JavaScript 파일이 있습니다. | 디버깅에 이 프로필을 사용합니다. |
| 개발 프로필 | 이 프로파일은 가능한 가장 큰 크기의 CRX 패키지를 만듭니다. 모든 JavaScript 파일은 SDK 패키지에서처럼 별도로 사용할 수 있습니다. | 의미 변경 사항을 적용할 때 이 프로필을 사용합니다. |

#### 출하 프로필 {#ship-profile}

#### 명령 {#command}

* mvn clean -P 클라이언트에 배송된 소스 패키지의 클라이언트-패키지 폴더에 출하 설치
* 출하 프로파일 명령 실행은 64비트 JVM에서만 작동합니다.

#### WS 컨텐츠 {#ws-content-1}

* css - style.css, ie.css 및 jquery-ui.css를 포함합니다.
* 이미지 - 모든 이미지를 포함합니다.
* js:

   * libs:

      * require - require.js를 포함합니다.
      * jqueryi - jquery.ui.datepicker.ja.js 포함
   * 런타임:

      * 템플릿 - AEM Forms 작업 공간에 있는 모든 구성 요소의 HTML 파일 등 모든 템플릿을 포함합니다.
   * main.js(결합, 축소 및 단순화됨).
   * registry.js



* libs:

   * ws - Contains pluginPing.pdf, pdf.html, and WSNextAdapter.swf.

* 로케일 - .content.xml을 포함합니다.
* locales:

   * de-DE - 독일어용 translation.json을 포함합니다.
   * en-US - 영어에 대한 translation.json을 포함합니다.
   * fr-FR - 프랑스어용 translation.json 포함
   * ja-JP - 일본어용 translation.json을 포함합니다.
   * html.jsp - 현재 브라우저 로케일을 찾는 코드를 포함합니다.

* 색인 - .content.xml 포함
* profile - offline.jsp를 포함합니다.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 디버그 프로필 {#debug-profile}

#### 명령 {#command-1}

* mvn clean -P Debug 설치 - client-pkg
* 디버그 프로필 명령 실행은 64비트 JVM에서만 작동합니다.

#### WS 컨텐츠 {#ws-content-2}

* css - style.css, ie.css 및 jquery-ui.css를 포함합니다.
* 이미지 - 모든 이미지를 포함합니다.
* js:

   * libs:

      * require - require.js를 포함합니다.
      * jqueryi - jquery.ui.datepicker.ja.js 포함
   * 런타임:

      * 템플릿 - AEM Forms 작업 공간에 있는 모든 구성 요소의 HTML 파일 등 모든 템플릿을 포함합니다.
   * main.js(결합).
   * registry.js



* libs:

   * ws - Contains pluginPing.pdf, pdf.html, and WSNextAdapter.swf.

* 로케일 - .content.xml을 포함합니다.
* locales:

   * de-DE - 독일어용 translation.json을 포함합니다.
   * en-US - 영어에 대한 translation.json을 포함합니다.
   * fr-FR - 프랑스어용 translation.json 포함
   * ja-JP - 일본어용 translation.json을 포함합니다.
   * html.jsp - 현재 브라우저 로케일을 찾는 코드를 포함합니다.

* 색인 - .content.xml 포함
* profile - offline.jsp를 포함합니다.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### 개발 프로필 {#dev-profile}

#### 명령 {#command-2}

mvn clean -P 개발 설치 클라이언트-pkg

#### WS 컨텐츠 {#ws-content-3}

* css - style.css, ie.css 및 jquery-ui.css를 포함합니다.
* 이미지 - 모든 이미지를 포함합니다.
* js:

   * libs - AEM Forms 작업 공간에 사용된 모든 라이브러리를 포함합니다.
   * require - require.js 포함
   * jqueryi - jquery.ui.datepicker.ja.js 포함
   * 런타임:

      * 이니셜라이저 - initializer.js 및 modelcontrolerpath.js를 포함합니다.
      * 모델 - AEM Forms 작업 공간에 있는 모든 구성 요소의 모델을 포함합니다.
      * 경로 - AEM Forms 작업 영역의 시작 프로세스, 수행할 작업, 추적 및 환경 설정을 로드하는 HTML 파일과 JavaScript 파일이 들어 있습니다.
      * 서비스 - AEM Forms 작업 공간에 사용되는 service.js를 포함합니다.
      * 템플릿 - AEM Forms 작업 공간에 있는 모든 구성 요소의 HTML 파일 등 모든 템플릿을 포함합니다.
      * util - AEM Forms 작업 공간에 사용되는 모든 유틸리티 파일(JavaScript)을 포함합니다.
      * 보기 - AEM Forms 작업 공간의 모든 구성 요소 보기를 포함합니다.
   * main.js
   * registry.js
   * router.js


* libs:

   * ws - Contains pluginPing.pdf, pdf.html, and WSNextAdapter.swf.

* 로케일 - .content.xml을 포함합니다.
* locales:

   * de-DE - 독일어용 translation.json을 포함합니다.
   * en-US - 영어에 대한 translation.json을 포함합니다.
   * fr-FR - 프랑스어용 translation.json 포함
   * ja-JP - 일본어용 translation.json을 포함합니다.
   * html.jsp - 현재 브라우저 로케일을 찾는 코드를 포함합니다.

* 색인 - .content.xml 포함
* profile - offline.jsp를 포함합니다.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
