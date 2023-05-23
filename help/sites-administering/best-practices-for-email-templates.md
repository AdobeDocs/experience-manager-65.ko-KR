---
title: 이메일 템플릿에 대한 우수 사례
seo-title: Best Practices for Email Templates
description: AEM에서 이메일 템플릿을 만드는 모범 사례를 확인하십시오.
seo-description: Find best practices on creating email templates in AEM.
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
source-wordcount: '1116'
ht-degree: 1%

---

# 이메일 템플릿에 대한 우수 사례 {#best-practices-for-email-templates}

>[!CAUTION]
>
>AEM 이메일 구성 요소는 더 이상 사용되지 않습니다. 콘텐츠와 스타일을 병합하는 이메일의 특성상 AEM에서 즉시 제공하는 이메일 구성 요소는 프로젝트에 필요한 모든 구성 요소로 사용자 정의 스타일을 구현해야 하므로 고객이 제한적으로 재사용할 수 있습니다.
>
>이메일 구성 요소는 프로젝트 수준에서 구현할 수 있으며, 더 이상 사용되지 않는 AEM 이메일 구성 요소는 이를 구현하는 방법을 보여 줍니다. 단, 이렇게 사용되지 않는 구성 요소는 프로젝트에서 사용할 수 없습니다.

이 문서에서는 이메일 디자인 관련 모범 사례 중 일부를 설명합니다. 이렇게 하면 이메일 캠페인 템플릿이 제대로 개발됩니다.

AEM에서 사용할 수 있는 데모 캠페인은 이러한 모든 모범 사례를 따릅니다. 각 모범 사례에 대해 데모 캠페인에서 모범 사례를 구현하는 방법을 설명합니다.

뉴스레터를 생성할 때 다음 모범 사례를 사용하십시오.

>[!NOTE]
>
>모든 캠페인 콘텐츠는 `master` 유형의 페이지 `cq/personalization/components/ambitpage`.
>
>예를 들어 계획된 캠페인 구조가 다음과 같은 경우
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>이 항목이 아래에 있는지 확인해야 합니다. `master` 페이지
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Adobe Campaign용 메일 템플릿을 만들 때 속성을 포함해야 합니다 **acMapping** 값 포함 **mapRecipient** 다음에서 **jcr:content** 템플릿의 노드이거나 다음 위치에서 Adobe Campaign 템플릿을 선택할 수 없습니다. **페이지 속성** / AEM (필드가 비활성화됨)

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
   <td><p>를 변경하는 디자인으로 구성할 수 있습니다. <i>cq:doctype</i> 의 속성<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>기본값은 "XHTML"입니다.</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>"HTML_5"로 변경할 수 있습니다.</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>특수 문자를 올바르게 렌더링하도록 문자 정의를 지정합니다.</p> <p>CHARSET 선언(예: iso-8859-15, UTF-8)을 &lt;head&gt;</p> </td>
   <td><p>UTF-8로 설정됩니다.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>를 사용하여 모든 구조 코드 작성 &lt;table&gt;요소를 생성하지 않습니다. 복잡한 레이아웃의 경우 표를 중첩하여 복잡한 구조를 만들어야 합니다.</p> <p>CSS가 없어도 이메일이 좋아야 합니다.</p> </td>
   <td><p>표는 전체 템플릿 전체에서 콘텐츠 구조화에 사용됩니다. 현재 최대 4개의 중첩 테이블 사용(기본 테이블 1개 + 최대 4개). 3 중첩 수준)</p> <p>&lt;div&gt; 태그는 적절한 구성 요소 편집을 위해 작성자 모드에서만 사용됩니다.</p> </td>
  </tr>
  <tr>
   <td>요소 속성(예: cellpadding, valign 및 width)을 사용하여 테이블 차원을 설정합니다. 이렇게 하면 상자-모델 구조가 강제 적용됩니다.</td>
   <td><p>모든 표에는 다음과 같은 필수 속성이 포함됩니다. <i>테두리</i>, <i>셀 패딩</i>, <i>cellspacing</i> 및 <i>폭</i>.</p> <p>표 내에서 요소 위치를 조화시키기 위해 모든 표 셀에는 속성이 있습니다 <i>valign="top"</i> 설정 중입니다.</p> </td>
  </tr>
  <tr>
   <td><p>가능하면 모바일 친화성을 고려하십시오. 미디어 쿼리를 사용하여 작은 화면의 텍스트 크기를 늘리고, 엄지 손가락 크기의 히트 영역을 링크에 제공합니다.</p> <p>디자인이 허용하는 경우 응답형 이메일을 만듭니다.</p> </td>
   <td>CSS 스타일을 사용하여 데모 디자인을 표현하는 한, 미디어 쿼리는 모바일 친화적 인 버전을 제공하는 데 사용됩니다.</td>
  </tr>
  <tr>
   <td>인라인 CSS는 모든 CSS를 시작 부분에 배치하는 것보다 좋습니다.</td>
   <td><p>기본 HTML 구조를 더 잘 보여 주고 뉴스레터 구조를 사용자 정의할 수 있는 가능성을 완화하기 위해 일부 CSS 정의만 인라인되었습니다.</p> <p>기본 스타일과 템플릿 변형이 의 스타일 블록으로 추출되었습니다. &lt;head&gt; 페이지의 입니다. 뉴스레터를 최종 제출할 때 이러한 CSS 정의는 HTML에 인라인되어야 합니다. 자동 인라인 메커니즘이 계획되어 있지만 현재 사용할 수 없습니다.</p> </td>
  </tr>
  <tr>
   <td>CSS를 간단하게 유지하십시오. 복합 스타일 선언, 속기 코드, CSS 레이아웃 속성, 복합 선택기 및 의사 요소를 사용하지 마십시오.</td>
   <td>CSS 스타일을 사용하여 데모 디자인을 표현하는 한, CSS 권장 사항이 준수됩니다.</td>
  </tr>
  <tr>
   <td>이메일은 최대 너비 600~800픽셀이어야 합니다. 이렇게 하면 많은 클라이언트가 제공하는 미리 보기 창 크기 내에서 더 잘 동작합니다.</td>
   <td>다음 <i>폭</i> 데모 디자인에서 콘텐츠 표의 크기는 600px로 제한됩니다.</td>
  </tr>
 </tbody>
</table>

### 이미지 {#images}

/libs/mcm/campaign/components/image

| **우수 사례** | **구현** |
|---|---|
| 추가 *alt* 이미지에 대한 속성 | 다음 *alt* 속성이 이미지 구성 요소에 필수로 정의되었습니다. |
| 사용 *jpg* 대신 *png* 이미지 형식 | 이미지는 항상 이미지 구성 요소에 의해 JPG으로 제공됩니다. |
| 사용 `<img>` 요소를 사용하여 테이블에 있는 배경 이미지 대신 붙여넣습니다. | 템플릿에 배경 이미지 데이터가 사용되지 않습니다. |
| 그림에 style=&quot;display block&quot; 특성을 추가합니다. Gmail에 잘 표시되도록 허용합니다. | 모든 이미지에는 기본적으로 *style=&quot;display block&quot;* 특성. |

### 텍스트 및 링크 {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>우수 사례</strong></td>
   <td><strong>구현</strong></td>
  </tr>
  <tr>
   <td>CSS에서 스타일 대신 html 사용(font-family)</td>
   <td>이제 RichTextEditor(예: textimage 구성 요소)에서 글꼴 패밀리와 글꼴 크기를 선택하여 선택한 텍스트에 적용할 수 있습니다. 태그로 렌더링됩니다.</td>
  </tr>
  <tr>
   <td>다음과 같은 기본적인 교차 플랫폼 글꼴 사용 <i>Arial, Verdana, 조지아</i> 및 <i>타임즈 뉴 로마자</i>.</td>
   <td><p>뉴스레터 디자인에 따라 다릅니다.</p> <p>데모 디자인의 경우 "Helvetica" 글꼴이 사용되지만, 존재하지 않는 경우 일반 sans-serif 글꼴로 대체됩니다.</p> </td>
  </tr>
 </tbody>
</table>

### 범용 {#generic}

| **우수 사례** | **구현** |
|---|---|
| W3C 유효성 검사기를 사용하여 HTML 코드를 수정합니다. 열려 있는 모든 태그가 제대로 닫혀 있는지 확인하십시오. | 코드가 확인되었습니다. XHTML 전환 Doctype의 경우 `<html>` 요소가 누락되었습니다. |
| JavaScript 또는 Flash에 구애받지 마십시오. 이러한 기술은 주로 이메일 클라이언트에서 지원되지 않습니다. | 뉴스레터 템플릿에서 JavaScript와 Flash을 사용하지 않습니다. |
| 다중 부분 전송을 위한 일반 텍스트 버전을 추가합니다. | 페이지 콘텐츠에서 일반 텍스트 버전을 쉽게 추출할 수 있도록 페이지 속성에 새 위젯을 빌드했습니다. 이를 최종 평문 버전의 시작점으로 사용할 수 있다. |

## Campaign 뉴스레터 템플릿 및 예제 {#campaign-newsletter-templates-and-examples}

AEM에는 캠페인 뉴스레터를 생성할 수 있는 몇 가지 템플릿과 구성 요소가 기본 제공됩니다. 이러한 템플릿과 구성 요소를 사용하여 사용자 정의 뉴스레터를 생성할 수 있습니다.

### 템플릿 {#templates}

견고한 기반을 제공하고 다양한 콘텐츠 흐름 가능성을 넓히기 위해 즉시 사용할 수 있는 세 가지 약간 다른 템플릿 유형이 있습니다. 이를 사용하여 사용자 지정 뉴스레터를 쉽게 작성할 수 있습니다.

모두 이(가) 있음 **머리글**, a **꼬리말** 및 a **본문** 섹션. 본문 섹션 아래에서 각 템플릿은 **열 디자인** (1, 2 또는 3열).

![](assets/chlimage_1-69.png)

### 구성 요소 {#components}

현재 다음 항목이 있습니다. [캠페인 템플릿 내에서 사용할 수 있는 7개 구성 요소](/help/sites-authoring/adobe-campaign-components.md). 이러한 구성 요소는 모두 Adobe 마크업 언어를 기반으로 합니다 **HTL**.

| **구성 요소 이름** | **구성 요소 경로** |
|---|---|
| 제목 | /libs/mcm/campaign/components/header |
| 이미지 | /libs/mcm/campaign/components/image |
| 텍스트 및 개인화 | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 링크 | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic(이전 Scene7) 이미지 템플릿 | /libs/mcm/campaign/s7image |
| 타깃팅된 참조 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>이러한 구성 요소는 메일 콘텐츠에 맞게 최적화됩니다. 즉, 이 문서에 설명된 모범 사례를 준수합니다. 다른 기본 구성 요소를 사용하는 것은 일반적으로 이러한 규칙을 위반합니다.

이러한 구성 요소에 대해서는 다음에서 자세히 설명합니다. [Adobe Campaign 구성 요소](/help/sites-authoring/adobe-campaign-components.md).
