---
title: 이메일 템플릿 우수 사례
seo-title: 이메일 템플릿 우수 사례
description: AEM에서 이메일 템플릿 만들기에 대한 우수 사례를 찾습니다.
seo-description: AEM에서 이메일 템플릿 만들기에 대한 우수 사례를 찾습니다.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
translation-type: tm+mt
source-git-commit: 87a8c36130c70d1fe8839c092fffda2821333466

---


# 이메일 템플릿 우수 사례 {#best-practices-for-email-templates}

>[!CAUTION]
>
>AEM 이메일 구성 요소는 더 이상 사용되지 않습니다. 콘텐츠와 스타일을 결합하는 이메일의 특성으로 인해 AEM에서 제공하는 이메일 구성 요소는 프로젝트에 필요한 구성 요소에 사용자 정의 스타일을 구현해야 하기 때문에 고객에게 제한된 재사용이 되었습니다.
>
>이메일 구성 요소는 프로젝트 수준에서 구현될 수 있으며, 더 이상 사용되지 않는 AEM 이메일 구성 요소는 이러한 기능을 구현하는 방법을 설명합니다. 그러나 이러한 사용되지 않는 구성 요소는 프로젝트에서 사용할 수 없습니다.

이 문서에서는 잘 개발된 이메일 캠페인 템플릿으로 이어지는 이메일 디자인에 대한 우수 사례 중 일부를 설명합니다.

AEM에서 사용할 수 있는 데모 캠페인은 이러한 모든 우수 사례를 따릅니다. 데모 캠페인에서 모범 사례를 구현하는 방법은 각 우수 사례에 대해 설명합니다.

자신만의 뉴스레터를 만들 때 이러한 우수 사례를 사용합니다.

>[!NOTE]
>
>모든 캠페인 컨텐츠는 유형 `master` 페이지 아래에 만들어야 합니다 `cq/personalization/components/ambitpage`.
>
>예를 들어 계획된 캠페인 구조가
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>페이지 아래에 있는지 확인해야 `master` 합니다
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Adobe Campaign에 대한 메일 템플릿을 만들 때는 값 **map** 받는 사람이 **있는 속성 acMapping을 템플릿의** jcr:content **노드에 포함시켜야** 합니다 **. 그렇지 않으면 AEM의 페이지 속성에서 Adobe Campaign** 템플릿을 선택할 수 없습니다(필드가 비활성화됨).

## 템플릿/페이지 구성 요소 {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletter 페이지***

<table>
 <tbody>
  <tr>
   <td><strong>모범 사례</strong></td>
   <td><strong>구현</strong></td>
  </tr>
  <tr>
   <td><p>일관된 렌더링을 위해 문서 유형을 지정합니다.</p> <p>시작 부분에 DOCTYPE 추가(HTML 또는 XHTML)</p> </td>
   <td><p>"/etc/designs/default/jcr:content/campaign_newsletter page"에서 <i>cq:doctype</i> 속성을 변경하여 디자인할 수 있습니다<i>.</i></p> <p>기본값은 "XHTML"입니다.</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>"HTML_5"로 변경할 수 있습니다.</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>문자 정의를 지정하여 특수 문자를 올바르게 렌더링할 수 있습니다.</p> <p>CHARSET 선언(예: iso-8859-15, UTF-8)을 &lt;head&gt;에 추가</p> </td>
   <td><p>UTF-8로 설정됩니다.</p> <p>&lt;meta http-equiv="content-type" content="text/html;charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>&lt;table&gt;요소를 사용하여 모든 구조를 코딩합니다. 보다 복잡한 레이아웃의 경우 표를 중첩하여 복잡한 구조를 만들어야 합니다.</p> <p>이메일은 css가 없어도 좋아 보입니다.</p> </td>
   <td><p>표는 전체 템플릿 전체에서 컨텐츠 작성에 사용됩니다. 현재 중첩된 최대 4개의 표(기본 표 1개 + 최대)를 사용하고 있습니다. 3개의 중첩 수준)</p> <p>&lt;div&gt; 태그는 적절한 구성 요소 편집을 위해 작성 모드에서만 사용됩니다.</p> </td>
  </tr>
  <tr>
   <td>요소 특성(예: 셀 패딩, 값 및 폭)을 사용하여 표 크기를 설정합니다. 이것은 박스 모델 구조를 만들어냅니다.</td>
   <td><p>모든 표에는 <i>테두리</i>, <i>셀 패딩</i>, <i>셀 간격</i> 및 <i>너비와 같은 필요한 속성이</i>포함되어 있습니다.</p> <p>표 안에 요소 위치를 일치시키기 위해 모든 표 셀에는 속성 <i>값="top"</i> 설정이 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>가능한 모바일용 고객 미디어 쿼리를 사용하여 작은 화면에서 텍스트 크기를 늘리고 링크에 대해 축소판 크기의 히트 영역을 제공할 수 있습니다.</p> <p>디자인이 허용하는 경우 반응형 이메일을 만들 수 있습니다.</p> </td>
   <td>CSS 스타일이 데모 디자인을 표현하는 데 사용되는 한, 미디어 쿼리를 사용하여 모바일 친화적인 버전을 제공하고 있습니다.</td>
  </tr>
  <tr>
   <td>인라인 CSS는 모든 CSS를 시작 부분에 넣는 것보다 낫습니다.</td>
   <td><p>기본 HTML 구조를 보다 잘 보여주고 뉴스레터 구조를 일부 CSS 정의만 삽입하여 사용자 정의할 수 있도록 하기 위해.</p> <p>페이지의 &lt;head&gt;에 있는 스타일 블록에 기본 스타일과 템플릿 변화가 추출되었습니다. 뉴스레터의 최종 제출 시 이러한 CSS 정의는 HTML에 삽입되어야 합니다. 자동 인라인닝 메커니즘은 계획되었지만 현재 사용할 수 없습니다.</p> </td>
  </tr>
  <tr>
   <td>CSS를 간소화할 수 있습니다. 복합 스타일 선언, 축약형 코드, CSS 레이아웃 속성, 복잡한 선택기 및 의사 요소를 피하십시오.</td>
   <td>CSS 스타일이 데모 디자인을 표현하는 데 사용되는 한 CSS 권장 사항이 적용됩니다.</td>
  </tr>
  <tr>
   <td>이메일의 최대 너비는 600-800픽셀이어야 합니다. 이렇게 하면 많은 클라이언트가 제공하는 미리 보기 창 크기 내에서 더 잘 동작합니다.</td>
   <td>데모 디자인에서 컨텐츠 테이블의 <i>너비는</i> 600px로 제한됩니다.</td>
  </tr>
 </tbody>
</table>

### 이미지 {#images}

/libs/mcm/campaign/components/image

| **모범 사례** | **구현** |
|---|---|
| 이미지에 *대체* 속성 추가 | alt *속성은* 이미지 구성 요소에 대해 필수로 정의되었습니다. |
| 이미지에 *png* ** 형식 대신 jpg를 사용합니다. | 이미지는 이미지 구성 요소에서 항상 JPG로 제공됩니다. |
| 표의 배경 이미지 대신 요소를 `<img>` 사용합니다. | 템플릿에 배경 이미지 데이터가 사용되지 않습니다. |
| 그림에 속성 style=&quot;display block&quot;을 추가합니다. Gmail에 잘 표시됩니다. | 모든 이미지는 기본적으로 *style=&quot;display block&quot;* 속성을 포함합니다. |

### 텍스트 및 링크 {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>모범 사례</strong></td>
   <td><strong>구현</strong></td>
  </tr>
  <tr>
   <td>CSS에서 스타일 대신 html &lt;font&gt;를 사용합니다(글꼴 모음).</td>
   <td>RichTextEditor(예: 텍스트 이미지 구성 요소)는 이제 선택한 텍스트에 글꼴군과 글꼴 크기를 선택하고 적용할 수 있습니다. &lt;font&gt; 태그로 렌더링됩니다.</td>
  </tr>
  <tr>
   <td>Arial, Verdana, Georgia 및 Times New <i>Roman과 같은 기본 크로스 플랫폼</i> 글꼴을 <i>사용할 수 있습니다</i>.</td>
   <td><p>뉴스레터 디자인에 따라 다릅니다.</p> <p>데모 디자인의 경우 "Helvetica" 글꼴이 사용되지만 없는 경우 일반 sans-serif 글꼴로 돌아갑니다.</p> </td>
  </tr>
 </tbody>
</table>

### 일반 {#generic}

| **모범 사례** | **구현** |
|---|---|
| W3C 유효성 검사기를 사용하여 HTML 코드를 수정합니다. 열려 있는 모든 태그가 올바르게 닫혀 있는지 확인합니다. | 코드가 확인되었습니다. XHTML 전환 Doctype의 경우 <html> 요소가 없습니다. |
| JavaScript나 Flash로 작업하지 마십시오. 이러한 기술은 이메일 클라이언트에서 대부분 지원되지 않습니다. | JavaScript와 Flash는 뉴스레터 템플릿에서 모두 사용되지 않습니다. |
| 다중 부분 전송을 위한 일반 텍스트 버전을 추가합니다. | 페이지 컨텐츠에서 일반 텍스트 버전을 쉽게 추출하기 위해 새 위젯이 페이지 속성으로 빌드되었습니다. 최종 일반 텍스트 버전의 시작점으로 사용할 수 있습니다. |

## 캠페인 뉴스레터 템플릿 및 예제 {#campaign-newsletter-templates-and-examples}

AEM에는 캠페인 뉴스레터를 만들 수 있는 몇 가지 템플릿과 구성 요소가 포함되어 있습니다. 이러한 템플릿과 구성 요소를 사용하여 사용자 정의 뉴스레터를 만들 수 있습니다.

### 템플릿 {#templates}

실선을 제공하고 다양한 컨텐츠 흐름 가능성을 확장하기 위해 즉시 사용할 수 있는 세 가지 서로 다른 템플릿 유형이 있습니다. 이러한 기능을 사용하여 사용자 지정 뉴스레터를 만들 수 있습니다.

모두 **머리글**, **바닥글** 및 **본문** 섹션이 있습니다. 본문 섹션 아래에서는 각 템플릿이 **열 디자인** (1, 2 또는 3열)과 다릅니다.

![](assets/chlimage_1-69.png)

### 구성 요소 {#components}

현재 캠페인 템플릿에서 [사용할 수 있는 구성 요소는](/help/sites-authoring/adobe-campaign-components.md)7개 있습니다. 이러한 구성 요소는 모두 Adobe 마크업 언어 HTL을 기반으로 **합니다**.

| **구성 요소 이름** | **구성 요소 경로** |
|---|---|
| 제목 | /libs/mcm/campaign/components/heading |
| 이미지 | /libs/mcm/campaign/components/image |
| 텍스트 및 개인화 | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 링크 | /libs/mcm/campaign/components/reference |
| Scene7 이미지 템플릿 | /libs/mcm/campaign/s7image |
| 타깃팅된 참조 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>이러한 구성 요소는 메일 컨텐츠에 최적화되어 있습니다.즉, 이 문서의 모범 사례를 준수합니다. 다른 기본 구성 요소를 사용하면 일반적으로 이러한 규칙을 위반하게 됩니다.

이러한 구성 요소는 Adobe Campaign 구성 [요소에](/help/sites-authoring/adobe-campaign-components.md)자세히 설명되어 있습니다.