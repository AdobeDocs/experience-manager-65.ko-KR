---
title: AEM Sites 단일 페이지 애플리케이션에 적응형 양식 또는 대화형 통신 포함
seo-title: AEM Sites 페이지에 적응형 양식 또는 인터랙티브 커뮤니케이션 포함
description: AEM Sites 페이지에 적응형 양식 또는 대화형 통신을 포함합니다. 사용자는 사이트 페이지를 종료하지 않고도 양식을 작성하고 제출할 수 있습니다.
seo-description: AEM Sites 페이지에 적응형 양식 또는 대화형 통신을 포함할 수 있습니다. 사용자는 사이트 페이지를 종료하지 않고도 양식을 작성하고 제출할 수 있습니다.
uuid: 4c75494e-e9d2-43b9-bbae-562e0eda8abb
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a74ed6c1-3006-4baf-bd77-ad4045e23c22
docset: aem65
translation-type: tm+mt
source-git-commit: d12d35bf8355d3069071523427a7794b88c09b13

---


# AEM Sites 단일 페이지 애플리케이션에 적응형 양식 또는 대화형 통신 포함{#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-single-page-application}

## 개요 {#overview}

양식 개발자는 AEM Forms를 사용하여 적응형 양식 및 인터랙티브한 커뮤니케이션을 AEM Sites SPA(Single Page Application)에 매끄럽게 포함할 수 있습니다. 포함된 적응형 양식 및 인터랙티브 커뮤니케이션이 완벽하게 작동하므로 사용자는 페이지를 종료하지 않고도 양식을 작성하고 제출할 수 있습니다. 사용자는 웹 페이지에서 다른 요소의 컨텍스트에 그대로 있고 적응형 양식 또는 인터랙티브한 커뮤니케이션과 동시에 상호 작용할 수 있습니다.

AEM Sites 단일 페이지 애플리케이션에서 AEM Forms SPA 컨테이너 구성 요소를 사용하여 적응형 양식 또는 [대화형 통신을](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component)[추가할 수 있습니다.](../../forms/using/embed-adaptive-form-aem-sites-spa.md#af-component) 사이트 페이지에 추가할 수 있는 AEM Sites SPA용 AEM Forms 구성 요소입니다.

비-SPA AEM Sites에 적응형 양식을 임베드하는 방법에 대한 자세한 내용은 AEM [Sites 페이지에](/help/forms/using/embed-adaptive-form-aem-sites.md)적응형 양식 또는 인터랙티브한 커뮤니케이션 임베드 페이지를 참조하십시오.

## 전제 조건 {#prerequisites}

AEM Forms SPA 컨테이너 구성 요소를 사용하여 AEM Sites SPA에 적응형 양식 또는 대화형 통신을 포함하려면 다음을 설치했는지 확인하십시오.

* Java SE Development Kit 8 이상
* Apache Maven 3.3.1 이상
* AEM 작성자 인스턴스
* [작성 인스턴스의 AEM Forms 6.4.2 Add-on 패키지](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)

## AEM Forms SPA 컨테이너 구성 요소 설치 {#install-aem-forms-spa-container-component}

다음 단계를 수행하여 AEM Forms SPA 컨테이너 구성 요소를 설치합니다.

1. [SPA용 AEM Forms 구성 요소를 복제하거나 다운로드합니다](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa).
1. SPA용 AEM Forms 구성 요소를 설치합니다. 구성 요소 설치 지침은 README.md [파일에](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa#aem-form-component) 있습니다.

   이 구성 요소에는 SPA 컨테이너 구성 요소를 React 기반 SPA 프로젝트와 통합하는 데 사용할 수 있는 [샘플 React 구성 요소가](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component) 포함되어 있습니다.

1. [반응형 SPA 프로젝트를](https://github.com/adobe/aem-sample-we-retail-journal)복제하거나 다운로드할 수 있습니다.
1. README.md [](https://github.com/Adobe-Marketing-Cloud/aem-forms/tree/master/forms-spa/react-component#aem-form-react-component-for-spa---editor) 파일의 지침에 따라 SPA 컨테이너 구성 요소를 React 기반 SPA 프로젝트와 통합합니다.

   AEM Forms SPA 컨테이너 구성 요소를 설치하고, 구성 요소를 반응 기반 SPA 프로젝트와 통합한 후, AEM Sites 페이지에 적응형 양식 및 대화형 통신을 포함할 수 있습니다.

## 적응형 양식 또는 인터랙티브 커뮤니케이션 임베드 {#af-component}

AEM Forms for SPA Container 구성 요소를 사용하여 적응형 양식 또는 대화형 통신을 포함하려면 다음을 수행하십시오.

1. 적응형 양식 또는 대화형 통신을 포함할 AEM 사이트 페이지를 편집 모드로 엽니다.
1. 다음 **옵션을 사용하여 페이지에 AEM** Form for SPA 구성 요소를 삽입합니다.

   * 사이트 페이지에서 레이아웃 컨테이너를 누르고 **+** 을 탭하고 AEM Form **for SPA 구성 요소를** 선택합니다.

   * 구성 요소 브라우저 패널에서 페이지에 **AEM Form for SPA** 구성 요소를 드래그하여 놓습니다.
   * 자산 브라우저에서 적응형 양식 또는 대화형 통신을 검색하고 사이트 페이지에 끌어 놓습니다. AEM Forms for SPA 구성 요소 컨테이너에 양식을 포함합니다.
   >[!NOTE]
   >
   >페이지에서 여러 AEM Forms SPA Container 구성 요소를 렌더링할 수 없습니다. 한 페이지에 여러 개의 AEM Forms SPA 컨테이너를 보유할 수 있지만 한 번에 하나의 구성 요소만 렌더링됩니다. 한 페이지에 하나의 구성 요소만 표시되므로 불일치를 방지할 수 있습니다.

1. 사이트 페이지에서 포함된 AEM Forms SPA Container 구성 요소를 탭한 다음 작업 표시줄에서 ![settings_icon](assets/settings_icon.png) 을 탭합니다. AEM **Forms SPA 컨테이너 편집** 대화 상자가 열립니다.
1. AEM **양식 컨테이너 편집** 대화 상자에서 다음을 지정합니다.

   * **** 자산 유형:포함할 자산 유형을 선택합니다. 적응형 양식 **및** 인터랙티브 **커뮤니케이션을 위한 옵션**

   * **자산 경로**:포함할 적응형 양식 또는 대화형 통신을 찾아 선택합니다. 적응형 양식이나 대화형 통신이 자산 브라우저를 사용하여 삽입되면 필드가 자동으로 채워집니다.
   * **채널** (대화형 통신만):포함할 대화형 채널 유형을 선택합니다. 옵션은 웹 **채널과** 인쇄 **채널입니다**.

   * **테마**:적응형 양식 또는 대화형 커뮤니케이션의 구성 요소에 대한 스타일을 정의하는 테마를 선택합니다. 스타일링에는 글꼴 스타일, 배경색, 크기 및 정렬과 같은 모양 속성이 포함되어 있습니다.

1. 을 ![](assets/done_icon.png) 눌러 설정을 저장합니다. 적응형 양식 또는 대화형 통신이 이제 페이지에 포함됩니다.

## 포함된 적응형 양식 및 인터랙티브한 커뮤니케이션 게시 {#publish-embedded-adaptive-form-and-interactive-communication}

AEM Sites 페이지에 포함된 자산(적응형 양식 또는 대화형 통신)을 게시하기 위한 다음 시나리오를 고려하십시오.

* AEM Sites 페이지를 처음으로 게시하고 포함된 적응형 양식 또는 대화형 통신이 포함된 경우 사이트 페이지와 포함된 자산을 게시합니다.
* 게시된 사이트 페이지에서 포함된 적응형 양식이나 대화형 통신만 수정한 경우 원본 자산을 게시하면 변경 사항이 게시된 사이트 페이지에 반영됩니다. 게시된 사이트 페이지에는 자산에 대한 참조가 포함되어 있으며 페이지를 다시 게시할 필요가 없습니다.
* 사이트 페이지와 포함된 적응형 양식 또는 대화형 통신을 수정한 경우 사이트 페이지와 포함된 자산을 다시 게시합니다.

## 포함된 적응형 양식 및 인터랙티브 커뮤니케이션 수정 {#modify-embedded-adaptive-form-and-interactive-communication}

AEM 사이트 페이지는 AEM Forms 컨테이너의 적응형 양식 및 대화형 통신에 대한 참조를 유지 관리합니다. 따라서 테마, 스타일 및 제출 동작과 같은 모든 구성 및 속성은 원래의 적응형 양식과 대화형 통신에 구성되어 있는 적응형 양식과 대화형 커뮤니케이션에 유지됩니다.

포함된 응용 양식과 대화형 커뮤니케이션의 구성이나 속성을 수정하려면 다음 중 하나를 수행합니다.

* 각 편집기에서 적응형 양식 또는 인터랙티브 커뮤니케이션으로 원본 양식을 열고 수정합니다.
* 편집 모드에서 사이트 페이지 내에서 적응형 양식 또는 대화형 통신을 누른 다음 **새 창에서**&#x200B;편집을 누릅니다. 원본 양식이 편집 모드로 열립니다.

## 고려 사항 및 우수 사례 {#considerations-and-best-practices}

AEM 사이트 페이지에 적응형 양식을 포함할 때는 다음 사항에 유의하십시오.

* 원본 양식의 머리글과 바닥글은 포함된 양식에 포함되지 않습니다.
* 사용자 초안 및 포함된 양식 제출은 양식 포털의 초안 및 제출 양식 탭에서 지원되고 볼 수 있습니다.
* 원본 양식에 구성된 제출 작업은 포함된 양식으로 유지됩니다.
* 원래 양식에 구성된 경험 타깃팅 및 A/B 테스트는 포함된 양식에서 작동하지 않습니다. 하지만 사이트 페이지에서 경험 타깃팅을 사용하여 사용자 프로필에 따라 다른 양식을 표시할 수 있습니다.
* Adobe Analytics가 원본 양식에 대해 구성된 경우 포함된 양식의 분석 데이터가 Adobe Analytics에서 캡처됩니다. 하지만 양식 분석 보고서에서는 사용할 수 없습니다.

