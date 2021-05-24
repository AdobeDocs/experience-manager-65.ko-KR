---
title: 이메일 템플릿 우수 사례
seo-title: 이메일 템플릿 우수 사례
description: AEM에서 이메일 템플릿을 만드는 방법에 대한 모범 사례를 찾습니다.
seo-description: AEM에서 이메일 템플릿을 만드는 방법에 대한 모범 사례를 찾습니다.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 1%

---

# 전자 메일 템플릿에 대한 우수 사례 {#best-practices-for-email-templates}

>[!CAUTION]
>
>AEM 이메일 구성 요소는 더 이상 사용되지 않습니다. 컨텐츠 및 스타일을 병합하는 이메일의 특성으로 인해, AEM에서 기본적으로 제공하는 이메일 구성 요소는 프로젝트에 필요한 구성 요소에 사용자 지정 스타일을 구현해야 하므로 고객을 위해 제한된 재사용이 됩니다.
>
>이메일 구성 요소는 프로젝트 수준에서 구현할 수 있으며 사용되지 않는 AEM 이메일 구성 요소는 이를 어떻게 달성할 수 있는지 보여줍니다. 하지만 이렇게 사용되지 않는 구성 요소는 프로젝트에서 사용해서는 안 됩니다.

이 문서에서는 잘 개발된 이메일 캠페인 템플릿에 기여하는 이메일 디자인에 대한 모범 사례 중 일부를 설명합니다.

AEM에서 사용할 수 있는 데모 캠페인은 이러한 모든 우수 사례를 따릅니다. 데모 캠페인에서 모범 사례를 구현하는 방법은 각 우수 사례에 대해 설명되어 있습니다.

자신만의 뉴스레터를 만들 때 이러한 우수 사례를 사용하십시오.

>[!NOTE]
>
>모든 캠페인 콘텐츠는 `cq/personalization/components/ambitpage` 유형의 `master` 페이지 아래에 만들어야 합니다.
>
>예를 들어 계획된 캠페인 구조가 다음과 같은 경우
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>`master` 페이지 아래에 있는지 확인해야 합니다
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Adobe Campaign용 메일 템플릿을 만들 때 템플릿의 **jcr:content** 노드에 값 **mapRecipient**&#x200B;이 있는 **acMapping** 속성을 포함해야 합니다. 그렇지 않으면 AEM의 **페이지 속성**&#x200B;에서 Adobe Campaign 템플릿을 선택할 수 없습니다(필드가 비활성화됨).

## 템플릿/페이지 구성 요소 {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>우수 사례</strong></td>
   <td><strong>구현</strong></td>
  </tr>
  <tr>
   <td><p>일관된 렌더링을 위해 문서 유형을 지정합니다.</p> <p>시작 부분에 DOCTYPE(HTML 또는 XHTML)을 추가합니다</p> </td>
   <td><p><i>cq:doctype</i> 속성을 <i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i>에서 변경하여 디자인에서 구성할 수 있습니다.</p> <p>기본값은 "XHTML"입니다.</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>다음 "HTML_5"로 변경할 수 있습니다.</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>특수 문자를 올바르게 렌더링하려면 문자 정의를 지정합니다.</p> <p>&lt;head&gt;에 CHARSET 선언(예: iso-8859-15, UTF-8)을 추가합니다.</p> </td>
   <td><p>이 UTF-8로 설정되어 있습니다.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>&lt;table&gt;요소를 사용하여 모든 구조를 코딩합니다. 복잡한 레이아웃을 만들려면 표를 중첩하여 복잡한 구조를 만들어야 합니다.</p> <p>이메일은 css 없이도 잘 보입니다.</p> </td>
   <td><p>표는 전체 템플릿 전체에서 컨텐츠 구조화에 사용됩니다. 현재 최대 4개의 중첩 테이블(기본 테이블 1개 + 최대)을 사용하고 있습니다. 3개 중첩 수준)</p> <p>&lt;div&gt; 태그는 적절한 구성 요소 편집을 위해 작성 모드에서만 사용됩니다.</p> </td>
  </tr>
  <tr>
   <td>요소 속성(예: cellpadding, valign 및 width)을 사용하여 표 차원을 설정합니다. 이렇게 하면 박스 모델 구조가 강제 적용됩니다.</td>
   <td><p>모든 표에는 <i>border</i>, <i>cellpadding</i>, <i>cellspacing</i> 및 <i>width</i>과 같은 필요한 특성이 포함되어 있습니다.</p> <p>테이블 내에 요소 위치를 일치시키기 위해 모든 테이블 셀에는 <i>valign="top"</i> 특성이 설정되어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>가능하면 모바일 친화성을 고려하십시오. 미디어 쿼리를 사용하여 작은 화면에서 텍스트 크기를 늘리고, 링크에 대한 축소판 크기 히트 영역을 제공합니다.</p> <p>디자인에서 허용하는 경우 이메일 응답형으로 만듭니다.</p> </td>
   <td>데모 디자인을 표시하는 데 CSS 스타일이 사용되는 한 미디어 쿼리를 사용하여 모바일 친화적인 버전을 제공하고 있습니다.</td>
  </tr>
  <tr>
   <td>인라인 CSS는 모든 CSS를 시작 부분에 넣는 것보다 낫습니다.</td>
   <td><p>기본 HTML 구조를 더 잘 보여주고 일부 CSS 정의만 삽입된 뉴스레터 구조를 사용자 지정할 수 있는 가능성을 개선하기 위해</p> <p>기본 스타일 및 템플릿 변형이 페이지의 &lt;head&gt;에 있는 스타일 블록으로 추출되었습니다. 뉴스레터를 최종적으로 제출할 때 이러한 CSS 정의는 HTML에 삽입해야 합니다. 자동 인선 메커니즘이 계획되었지만 현재 사용할 수 없습니다.</p> </td>
  </tr>
  <tr>
   <td>CSS를 단순하게 유지합니다. 복합 스타일 선언, 축약형 코드, CSS 레이아웃 속성, 복잡한 선택기 및 의사 요소를 사용하지 마십시오.</td>
   <td>데모 디자인을 표시하는 데 CSS 스타일이 사용되는 한 CSS 권장 사항이 따릅니다.</td>
  </tr>
  <tr>
   <td>전자 메일의 최대 너비는 600-800픽셀이어야 합니다. 이렇게 하면 많은 클라이언트가 제공하는 미리 보기 창 크기 내에서 더 잘 작동합니다.</td>
   <td>콘텐츠 테이블의 <i>width</i>은 데모 디자인에서 600px로 제한됩니다.</td>
  </tr>
 </tbody>
</table>

### 이미지 {#images}

/libs/mcm/campaign/components/image

| **우수 사례** | **구현** |
|---|---|
| 이미지에 *alt* 속성 추가 | *alt* 속성이 이미지 구성 요소에 대해 필수로 정의되었습니다. |
| 이미지에 *png* 형식 대신 *jpg* 형식을 사용합니다 | 이미지는 항상 이미지 구성 요소에서 JPG로 제공됩니다. |
| 테이블에서 배경 이미지 대신 `<img>` 요소를 사용합니다. | 템플릿에 배경 이미지 데이터가 사용되지 않습니다. |
| 그림에 속성 style=&quot;display block&quot;을 추가합니다. Gmail에서 잘 표시할 수 있습니다. | 모든 이미지는 기본적으로 *style=&quot;display block&quot;* 속성을 포함합니다. |

### 텍스트 및 링크 {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>우수 사례</strong></td>
   <td><strong>구현</strong></td>
  </tr>
  <tr>
   <td>CSS에서 스타일 대신 html &lt;font&gt;를 사용(font-family)</td>
   <td>리치 텍스트 편집기(예: 텍스트 이미지 구성 요소)는 이제 선택한 텍스트에 글꼴 패밀리와 글꼴 크기를 선택하고 적용할 수 있습니다. &lt;font&gt; 태그로 렌더링됩니다.</td>
  </tr>
  <tr>
   <td><i>Arial, Verdana, Georgia</i> 및 <i>Times New Roman</i>과 같은 기본적인 교차 플랫폼 글꼴을 사용합니다.</td>
   <td><p>뉴스레터 디자인에 따라 다릅니다.</p> <p>데모 디자인에서 "Helvetica" 글꼴은 사용되지만 없는 경우 일반 sans-serif 글꼴로 돌아갑니다.</p> </td>
  </tr>
 </tbody>
</table>

### 일반 {#generic}

| **우수 사례** | **구현** |
|---|---|
| W3C 유효성 검사기를 사용하여 HTML 코드를 수정합니다. 열려 있는 모든 태그가 올바르게 닫혀 있는지 확인합니다. | 코드가 검증되었습니다. XHTML 변환 Doctype의 경우 `<html>` 요소에 대해 누락된 xmlns 속성만 누락됩니다. |
| JavaScript나 Flash을 사용하지 마십시오. 이러한 기술은 이메일 클라이언트가 주로 지원하지 않습니다. | JavaScript나 Flash은 뉴스레터 템플릿에 사용되지 않습니다. |
| 다중 부분 전송을 위한 일반 텍스트 버전을 추가합니다. | 페이지 컨텐츠에서 일반 텍스트 버전을 쉽게 추출하기 위해 새 위젯이 페이지 속성에 빌드되었습니다. 최종 일반 텍스트 버전의 시작점으로 사용할 수 있습니다. |

## Campaign 뉴스레터 템플릿 및 예 {#campaign-newsletter-templates-and-examples}

AEM에는 캠페인 뉴스레터를 만들기 위해 즉시 사용 가능한 몇 가지 템플릿과 구성 요소가 포함되어 있습니다. 이러한 템플릿 및 구성 요소를 사용하여 사용자 지정 뉴스레터를 만들 수 있습니다.

### 템플릿 {#templates}

솔리드 베이스를 제공하고 다양한 컨텐츠 플로우 가능성을 확장하기 위해 기본적으로 사용할 수 있는 템플릿 유형은 세 가지가 약간 다릅니다. 이러한 속성을 사용하여 사용자 지정 뉴스레터를 작성할 수 있습니다.

모두 **header**, **바닥글** 및 **body** 섹션이 있습니다. 본문 섹션 아래에 각 템플릿은 **열 디자인**(1, 2 또는 3열)에 서로 다릅니다.

![](assets/chlimage_1-69.png)

### 구성 요소 {#components}

현재 캠페인 템플릿](/help/sites-authoring/adobe-campaign-components.md) 내에서 사용할 수 있는 구성 요소가 [7개 있습니다. 이러한 구성 요소는 모두 Adobe 마크업 언어 **HTL**&#x200B;을 기반으로 합니다.

| **구성 요소 이름** | **구성 요소 경로** |
|---|---|
| 제목 | /libs/mcm/campaign/components/heading |
| 이미지 | /libs/mcm/campaign/components/image |
| 텍스트 및 개인화 | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 링크 | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic(이전 Scene7) 이미지 템플릿 | /libs/mcm/campaign/s7image |
| 타깃팅된 참조 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>이러한 구성 요소는 메일 콘텐츠에 최적화되어 있습니다.즉, 이 문서에서는 이 문서에 설명된 우수 사례를 따릅니다. 다른 기본 구성 요소를 사용하면 일반적으로 이러한 규칙을 위반합니다.

이러한 구성 요소는 [Adobe Campaign 구성 요소](/help/sites-authoring/adobe-campaign-components.md)에 자세히 설명되어 있습니다.
