---
title: AEM Sites 단일 페이지 애플리케이션에 적응형 양식 또는 대화형 통신 포함
description: AEM Sites 페이지에 적응형 양식 또는 대화형 통신을 임베드합니다. 사용자는 Sites 페이지를 종료하지 않고 양식을 작성하고 제출할 수 있습니다.
topic-tags: author, interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms
exl-id: b549f176-409a-4d81-8c2b-73d0dd0c6649
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 4%

---

# AEM Sites 단일 페이지 애플리케이션에 적응형 양식 또는 대화형 통신 포함{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

## 개요 {#overview}

AEM Forms을 사용하면 양식 개발자가 적응형 양식 및 대화형 커뮤니케이션을 AEM Sites SPA(단일 페이지 애플리케이션)에 원활하게 포함할 수 있습니다. 임베드된 적응형 양식 및 대화형 커뮤니케이션은 완전히 기능하며 사용자는 페이지를 종료하지 않고 양식을 작성하고 제출할 수 있습니다. 사용자가 웹 페이지의 다른 요소 컨텍스트에 남아 있으면서 적응형 양식 또는 대화형 통신과 동시에 상호 작용하는 데 도움이 됩니다.

AEM Sites 단일 페이지 응용 프로그램에서 [AEM Forms SPA 컨테이너 구성 요소](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[를 사용하여 적응형 양식 또는 대화형 통신을 추가할 수 있습니다.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) Sites 페이지에 추가할 수 있는 AEM Sites SPA용 AEM Forms 구성 요소입니다.

비 SPA AEM Sites에 적응형 양식을 포함하는 방법에 대한 자세한 내용은 [AEM Sites 페이지에 적응형 양식 또는 대화형 통신 포함](/help/forms/using/embed-adaptive-form-aem-sites.md)을 참조하십시오.

## 사전 요구 사항 {#prerequisites}

AEM Forms SPA 컨테이너 구성 요소를 사용하여 AEM sites SPA에 적응형 양식 또는 대화형 통신을 포함하려면 다음을 설치했는지 확인합니다.

* Java SE Development Kit 8 이상
* Apache Maven 3.3.1 이상
* AEM 작성자 인스턴스
* 작성자 인스턴스의 [AEM Forms 6.4.2 추가 기능 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html)

## AEM Forms SPA 컨테이너 구성 요소 설치 {#install-aem-forms-spa-container-component}

AEM Forms SPA 컨테이너 구성 요소를 설치하려면 다음 단계를 수행하십시오.

1. [SPA용 AEM Forms 구성 요소를 복제하거나 다운로드합니다](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. SPA용 AEM Forms 구성 요소를 설치합니다. 구성 요소 설치 지침은 [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) 파일에서 확인할 수 있습니다.

   구성 요소에는 SPA 컨테이너 구성 요소를 React 기반 SPA 프로젝트와 통합하는 데 사용할 수 있는 [샘플 React 구성 요소](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component)가 포함되어 있습니다.

1. [React 기반 SPA 프로젝트를 복제하거나 다운로드합니다](https://github.com/adobe/aem-sample-we-retail-journal).
1. [README.md](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) 파일에 있는 지침을 사용하여 SPA 컨테이너 구성 요소를 React 기반 SPA 프로젝트와 통합합니다.

   AEM Forms SPA 컨테이너 구성 요소를 설치하고 구성 요소를 React 기반 SPA 프로젝트와 통합한 후 AEM Sites 페이지에 적응형 양식 및 대화형 커뮤니케이션을 포함할 수 있습니다.

## 적응형 양식 또는 대화형 통신 포함 {#af-component}

SPA용 AEM Forms 컨테이너 구성 요소를 사용하여 적응형 양식 또는 대화형 통신을 포함하려면 다음을 수행하십시오.

1. 적응형 양식 또는 대화형 커뮤니케이션을 포함할 AEM 사이트 페이지를 편집 모드로 엽니다.
1. 다음 옵션 중 하나를 사용하여 **SPA용 AEM 양식** 구성 요소를 페이지에 삽입합니다.

   * 사이트 페이지에서 레이아웃 컨테이너를 선택하고 **+**&#x200B;을(를) 선택한 다음 **SPA용 AEM 양식** 구성 요소를 선택합니다.

   * 구성 요소 브라우저 패널에서 페이지의 **SPA용 AEM 양식** 구성 요소를 드래그 앤 드롭합니다.
   * Assets 브라우저에서 적응형 양식 또는 대화형 커뮤니케이션을 검색하고 사이트 페이지로 드래그 앤 드롭합니다. SPA용 AEM Forms 구성 요소 컨테이너에 양식을 임베드합니다.

   >[!NOTE]
   >
   >한 페이지에서 여러 AEM Forms SPA 컨테이너 구성 요소를 렌더링하는 것은 지원되지 않습니다. 페이지에 여러 AEM Forms SPA 컨테이너가 있을 수 있지만 한 번에 하나의 구성 요소만 렌더링됩니다. 불일치를 방지하기 위해 페이지에 구성 요소가 하나만 표시되는지 확인합니다.

1. 사이트 페이지에서 포함된 AEM Forms SPA 컨테이너 구성 요소를 선택한 다음 작업 표시줄에서 ![settings_icon](assets/settings_icon.png)을(를) 선택합니다. **AEM Forms SPA 컨테이너 편집** 대화 상자가 열립니다.
1. **AEM Forms 컨테이너 편집** 대화 상자에서 다음을 지정하십시오.

   * **자산 유형:** 포함할 자산 유형을 선택합니다. 옵션은 **적응형 양식** 및 **대화형 통신**&#x200B;입니다.

   * **자산 경로**: 포함할 적응형 양식 또는 대화형 커뮤니케이션을 찾아 선택합니다. Assets 브라우저를 사용하여 적응형 양식 또는 대화형 커뮤니케이션이 삽입되는 경우 필드가 자동으로 채워집니다.
   * **채널**(대화형 통신 전용): 포함할 대화형 채널의 유형을 선택하십시오. 옵션은 **웹 채널** 및 **인쇄 채널**&#x200B;입니다.

   * **테마**: 적응형 양식 또는 대화형 통신의 구성 요소에 대한 스타일을 정의하는 테마를 선택하십시오. 스타일링에는 글꼴 스타일, 배경색, 치수 및 정렬과 같은 모양 속성이 포함됩니다.

1. 설정을 저장하려면 ![done_icon](assets/done_icon.png)을(를) 선택하십시오. 이제 적응형 양식 또는 대화형 통신이 페이지에 임베드됩니다.

## Publish 임베드된 적응형 양식 및 대화형 통신 {#publish-embedded-adaptive-form-and-interactive-communication}

AEM Sites 페이지에 임베드된 에셋(적응형 양식 또는 대화형 통신)을 게시하기 위한 다음 시나리오를 고려하십시오.

* AEM Sites 페이지를 처음 게시하고 여기에 임베드된 적응형 양식 또는 대화형 통신이 포함된 경우 Sites 페이지 및 임베드된 에셋을 게시하십시오.
* 게시된 Sites 페이지에서 임베드된 적응형 양식 또는 대화형 통신만 수정한 경우 원래 에셋을 게시하고 변경 사항은 게시된 Sites 페이지에 반영됩니다. 게시된 사이트 페이지에는 에셋에 대한 참조가 포함되어 있으며 페이지를 다시 게시할 필요가 없습니다.
* Sites 페이지와 포함된 적응형 양식 또는 대화형 통신을 수정한 경우 Sites 페이지와 포함된 자산을 다시 게시하십시오.

## 포함된 적응형 양식 및 대화형 통신 수정 {#modify-embedded-adaptive-form-and-interactive-communication}

AEM sites 페이지는 AEM Forms 컨테이너에서 적응형 양식 및 대화형 통신에 대한 참조를 유지 관리합니다. 따라서 원래 적응형 양식 및 대화형 커뮤니케이션에 구성된 테마, 스타일 및 제출 액션과 같은 모든 구성 및 속성은 임베드된 적응형 양식 및 대화형 커뮤니케이션에 유지됩니다.

임베드된 적응형 양식 및 대화형 통신의 구성 또는 속성을 수정하려면 다음 중 하나를 수행합니다.

* 각 편집기에서 적응형 양식 또는 대화형 커뮤니케이션에서 원본 양식을 열고 수정합니다.
* 편집 모드에서 사이트 페이지 내에서 적응형 양식 또는 대화형 통신을 선택한 다음 **새 창에서 편집**&#x200B;을 선택합니다. 원본 양식이 편집 모드로 열립니다.

## 고려 사항 및 우수 사례 {#considerations-and-best-practices}

AEM sites 페이지에 적응형 양식을 포함할 때는 다음 사항을 염두에 두십시오.

* 원래 양식의 머리글 및 바닥글은 포함된 양식에 포함되지 않습니다.
* 포함된 양식의 사용자 초안 및 제출은 양식 포털의 초안 및 제출된 Forms 탭에서 지원되고 볼 수 있습니다.
* 원래 양식에 구성된 제출 액션은 포함된 양식에 유지됩니다.
* 원본 양식에 구성된 경험 타깃팅 및 A/B 테스트가 포함된 양식에서 작동하지 않습니다. 하지만 사이트 페이지에서 경험 타깃팅을 사용하여 사용자 프로필에 따라 다른 양식을 표시할 수 있습니다.
* 원래 양식에 대해 Adobe Analytics이 구성된 경우, 임베드된 양식의 분석 데이터가 Adobe Analytics에 캡처됩니다. 하지만 양식 분석 보고서에서는 사용할 수 없습니다.
