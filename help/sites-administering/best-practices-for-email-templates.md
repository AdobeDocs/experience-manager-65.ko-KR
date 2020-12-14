---
title: 이메일 템플릿 우수 사례
seo-title: 이메일 템플릿 우수 사례
description: AEM에서 이메일 템플릿을 만드는 방법에 대한 우수 사례를 살펴보십시오.
seo-description: AEM에서 이메일 템플릿을 만드는 방법에 대한 우수 사례를 살펴보십시오.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---


# 이메일 템플릿 {#best-practices-for-email-templates} 우수 사례

>[!CAUTION]
>
>AEM 이메일 구성 요소는 더 이상 사용되지 않습니다. 컨텐츠 및 스타일을 병합하는 이메일의 특성으로 인해 AEM에서 제공하는 이메일 구성 요소는 프로젝트에 필요한 구성 요소에 사용자 정의 스타일을 구현해야 하므로 고객에게 즉시 재사용할 수 없습니다.
>
>이메일 구성 요소는 프로젝트 수준에서 구현될 수 있으며, 가치가 떨어진 AEM 이메일 구성 요소는 이를 어떻게 달성할 수 있는지 보여줍니다. 그러나 이러한 가치 하락 구성 요소는 프로젝트에서 사용해서는 안 됩니다.

이 문서에서는 잘 개발된 이메일 캠페인 템플릿으로 이어지는 이메일 디자인에 대한 우수 사례 중 일부를 설명합니다.

AEM에서 사용할 수 있는 데모 캠페인은 다음과 같은 모든 모범 사례를 따릅니다. 각 우수 사례에 대해 데모 캠페인에서 우수 사례를 구현하는 방법에 대해 설명합니다.

자신만의 뉴스레터를 만들 때 이러한 우수 사례를 사용합니다.

>[!NOTE]
>
>모든 캠페인 컨텐츠는 `cq/personalization/components/ambitpage` 유형의 `master` 페이지 아래에 만들어야 합니다.
>
>예를 들어 계획된 캠페인 구조가
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>`master` 페이지 아래에 있는지 확인해야 합니다.
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Adobe Campaign에 대한 메일 템플릿을 만들 때 템플릿의 **jcr:content** 노드에 값 **mapRecipient**&#x200B;과 함께 속성 **acMapping** 속성을 포함해야 합니다. 그렇지 않으면 AEM의 **페이지 속성**&#x200B;에서 Adobe Campaign 템플릿을 선택할 수 없습니다(필드가 비활성화됨).

## 템플릿/페이지 구성 요소 {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>모범 사례</strong></td>
   <td><strong>구현</strong></td>
  </tr>
  <tr>
   <td><p>일관된 렌더링을 위해 문서 유형을 지정합니다.</p> <p>시작 부분에 DOCTYPE 추가(HTML 또는 XHTML)</p> </td>
   <td><p><i>cq:doctype</i> 속성을 <i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>기본값은 "XHTML"입니다.</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>"HTML_5"로 변경할 수 있습니다.</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>특수 문자를 정확하게 렌더링할 수 있도록 문자 정의를 지정합니다.</p> <p>CHARSET 선언(예: iso-8859-15, UTF-8)을 &lt;head&gt;에 추가</p> </td>
   <td><p>이 UTF-8로 설정되어 있습니다.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>&lt;table&gt;요소를 사용하여 모든 구조를 코딩합니다. 보다 복잡한 레이아웃의 경우 표를 중첩하여 복잡한 구조를 만들어야 합니다.</p> <p>이메일은 css가 없더라도 좋아 보입니다.</p> </td>
   <td><p>전체 템플릿 전체에서 표를 사용하여 컨텐츠를 구조화합니다. 현재 중첩된 최대 4개의 표(기본 표 1개 + 최대)를 사용하고 있습니다. 3 중첩 수준)</p> <p>&lt;div&gt; 태그는 적절한 구성 요소 편집을 위해 작성 모드에서만 사용됩니다.</p> </td>
  </tr>
  <tr>
   <td>요소 특성(예: 셀 패딩, 값 및 폭)을 사용하여 표 크기를 설정합니다. 이것은 박스 모델 구조를 만든다.</td>
   <td><p>모든 표에는 <i>border</i>, <i>cellpadding</i>, <i>cellspacing</i> 및 <i>width</i>와 같은 필요한 속성이 포함되어 있습니다.</p> <p>표 내부에 요소 배치를 조화롭게 하기 위해 모든 테이블 셀에는 <i>valign="top"</i> 속성이 설정되어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>가능하면 모바일친화성을 고려하십시오. 미디어 쿼리를 사용하여 작은 화면에서 텍스트 크기를 늘리고 링크에 대해 축소판 크기의 히트 영역을 제공합니다.</p> <p>디자인이 허용하는 경우 반응형 이메일을 만듭니다.</p> </td>
   <td>CSS 스타일을 사용하여 데모 디자인 일러스트레이션에 이르는 한 모바일 친화적인 버전을 제공하는 데 미디어 쿼리를 사용합니다.</td>
  </tr>
  <tr>
   <td>인라인 CSS는 모든 CSS를 시작 부분에 놓는 것보다 더 좋습니다.</td>
   <td><p>기본 HTML 구조를 보다 잘 보여주고 뉴스레터 구조를 일부 CSS 정의만 삽입하여 사용자 정의할 수 있도록 하기 위해.</p> <p>페이지의 &lt;head&gt;에 있는 스타일 블록에 기본 스타일과 템플릿 변화가 추출되었습니다. 뉴스레터의 최종 제출 시 이러한 CSS 정의는 HTML에 삽입해야 합니다. 자동 인라인닝 메커니즘은 계획되었지만 현재 사용할 수 없습니다.</p> </td>
  </tr>
  <tr>
   <td>CSS를 간소화할 수 있습니다. 복합 스타일 선언, 대표 코드, CSS 레이아웃 속성, 복잡한 선택기 및 의사 요소를 사용하지 마십시오.</td>
   <td>CSS 스타일을 사용하여 데모 디자인 일러스트레이션에 이르는 한 CSS 권장 사항을 따릅니다.</td>
  </tr>
  <tr>
   <td>이메일은 최대 폭 600-800픽셀이어야 합니다. 이렇게 하면 많은 클라이언트가 제공하는 미리 보기 창 크기 내에서 더 잘 동작합니다.</td>
   <td>내용 테이블의 <i>너비</i>는 데모 디자인에서 600px로 제한됩니다.</td>
  </tr>
 </tbody>
</table>

### 이미지 {#images}

/libs/mcm/campaign/components/image

| **모범 사례** | **구현** |
|---|---|
| 이미지에 *alt* 특성 추가 | *alt* 특성이 이미지 구성 요소에 대해 필수로 정의되었습니다. |
| 이미지에 *png* 형식 대신 *jpg*&#x200B;을 사용합니다. | 이미지는 이미지 구성 요소에서 항상 JPG로 제공됩니다. |
| 표의 배경 이미지 대신 `<img>` 요소를 사용합니다. | 템플릿에 배경 이미지 데이터가 사용되지 않습니다. |
| 사진에 속성 스타일=&quot;표시 블록&quot;을 추가합니다. Gmail에 잘 표시할 수 있습니다. | 모든 이미지는 기본적으로 *style=&quot;display block&quot;* 속성을 포함합니다. |

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
   <td>이제 RichTextEditor(예: 텍스트 이미지 구성 요소의 경우)에서 선택한 텍스트에 글꼴군과 글꼴 크기를 선택하여 적용할 수 있습니다. &lt;font&gt; 태그로 렌더링됩니다.</td>
  </tr>
  <tr>
   <td><i>Arial, Verdana, Georgia</i> 및 <i>Times New Roman</i>과 같은 기본 크로스 플랫폼 글꼴을 사용합니다.</td>
   <td><p>뉴스레터 디자인에 따라 다릅니다.</p> <p>데모 디자인의 경우 "Helvetica" 글꼴이 사용되지만 없는 경우 일반 sans-serif 글꼴로 돌아갑니다.</p> </td>
  </tr>
 </tbody>
</table>

### 일반 {#generic}

| **모범 사례** | **구현** |
|---|---|
| W3C 유효성 검사기를 사용하여 HTML 코드를 수정합니다. 열려 있는 태그가 모두 올바르게 닫혀 있는지 확인합니다. | 코드가 확인되었습니다. XHTML 전환 Doctype의 경우 `<html>` 요소에 대한 누락된 xmlns 특성만 누락되었습니다. |
| JavaScript 또는 Flash으로 고민하지 마십시오. 이러한 기술은 이메일 클라이언트에서 대부분 지원되지 않습니다. | 뉴스레터 템플릿에는 JavaScript와 Flash이 사용되지 않습니다. |
| 다중 부분 전송을 위해 일반 텍스트 버전을 추가합니다. | 새 위젯은 페이지 컨텐츠에서 일반 텍스트 버전을 쉽게 추출하기 위해 페이지 속성으로 빌드되었습니다. 최종 일반 텍스트 버전의 시작점으로 사용할 수 있습니다. |

## 캠페인 뉴스레터 템플릿 및 예 {#campaign-newsletter-templates-and-examples}

AEM에는 캠페인 뉴스레터를 만들 수 있는 다양한 템플릿과 구성 요소가 포함되어 있습니다. 이러한 템플릿 및 구성 요소를 사용하여 사용자 정의 뉴스레터를 만들 수 있습니다.

### 템플릿 {#templates}

기본 템플릿을 제공하고 다양한 컨텐츠 흐름을 확장하려면 기본적으로 3가지 서로 다른 템플릿 유형을 사용할 수 있습니다. 이러한 뉴스레터를 사용하여 사용자 지정 뉴스레터를 만들 수 있습니다.

모두 **머리글**, **바닥글** 및 **body** 섹션이 있습니다. 본문 섹션 아래에 있는 각 템플릿은 **열 디자인**(1, 2 또는 3열)과 다릅니다.

![](assets/chlimage_1-69.png)

### 구성 요소 {#components}

현재 캠페인 템플릿](/help/sites-authoring/adobe-campaign-components.md)에서 사용할 수 있는 구성 요소가 [7개 있습니다. 이러한 구성 요소는 모두 Adobe 마크업 언어 **HTL**&#x200B;을 기반으로 합니다.

| **구성 요소 이름** | **구성 요소 경로** |
|---|---|
| 제목 | /libs/mcm/campaign/components/heading |
| 이미지 | /libs/mcm/campaign/components/image |
| 텍스트 및 개인화 | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 링크 | /libs/mcm/campaign/components/reference |
| Scene7 이미지 템플릿 | /libs/mcm/campaign/s7image |
| 대상 참조 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>이러한 구성 요소는 메일 컨텐츠에 최적화되어 있습니다.즉, 이 문서의 모범 사례를 준수합니다. 다른 기본 구성 요소를 사용하면 일반적으로 이러한 규칙을 위반하게 됩니다.

이러한 구성 요소는 [Adobe Campaign 구성 요소](/help/sites-authoring/adobe-campaign-components.md)에서 자세히 설명합니다.