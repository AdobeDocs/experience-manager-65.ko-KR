---
title: AEM sites 페이지에 적응형 양식 또는 대화형 통신 포함
description: AEM sites 페이지에 적응형 양식을 포함할 수 있습니다. 사용자는 사이트 페이지를 벗어나지 않고도 양식을 작성하고 제출할 수 있습니다.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author, interactive-communications
feature: Adaptive Forms, Foundation Components
exl-id: 00ee7929-649f-4cbb-be79-ba13ac73a16d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 6%

---

# AEM sites 페이지에 적응형 양식 또는 대화형 통신 포함 {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-aem-sites.html) |
| AEM 6.5 | 이 문서 |


## 개요 {#overview}

AEM Forms을 사용하면 양식 개발자가 적응형 양식 및 대화형 커뮤니케이션을 AEM Sites 페이지 또는 AEM 외부에 호스트된 웹 페이지에 원활하게 포함할 수 있습니다. 임베드된 적응형 양식 및 대화형 커뮤니케이션은 완전히 기능하며 사용자는 페이지를 종료하지 않고 양식을 작성하고 제출할 수 있습니다. 사용자가 웹 페이지의 다른 요소 컨텍스트에 남아 있으면서 양식 또는 대화형 통신과 동시에 상호 작용하는 데 도움이 됩니다.

외부 웹 페이지에 적응형 양식을 포함하는 방법에 대한 내용은 [외부 웹 페이지에 적응형 양식 포함](/help/forms/using/embed-adaptive-form-external-web-page.md).

AEM Sites 페이지에서 다음을 사용하여 적응형 양식 또는 대화형 통신을 추가할 수 있습니다.

* **[AEM Forms 컨테이너 구성 요소](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms은 사이트 페이지에 추가할 수 있는 구성 요소를 제공합니다. AEM Forms 컨테이너 구성 요소를 사용하여 적응형 양식 및 대화형 통신을 포함할 수 있습니다.

* **[에셋 브라우저](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
사용자가 만드는 모든 양식 및 대화형 커뮤니케이션은 Assets에서 사용할 수 있습니다. 양식을 페이지에 에셋으로 드래그 앤 드롭할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

편집 가능한 템플릿을 사용하는 AEM sites 페이지에 적응형 양식 또는 대화형 통신을 포함하려면 AEM 양식 구성 요소가 관련 템플릿에 허용된 구성 요소로 구성되어 있는지 확인하십시오. 자세한 내용은 **정책 및 속성(레이아웃 컨테이너)** 의 섹션 [페이지 템플릿 만들기](/help/sites-authoring/templates.md).

정적 템플릿을 사용하는 사이트 페이지가 있는 경우 사이트 페이지의 단락 시스템에서 구성해야 합니다. 자세한 내용은 [디자인 모드에서 구성 요소 구성](/help/sites-authoring/default-components-designmode.md)을 참조하십시오.

## 적응형 양식 또는 대화형 통신 포함 {#af-component}

AEM Forms 컨테이너 구성 요소를 사용하여 적응형 양식 또는 대화형 통신을 포함하려면 다음을 수행하십시오.

1. 적응형 양식 또는 대화형 커뮤니케이션을 포함할 AEM 사이트 페이지를 편집 모드로 엽니다.
1. 구성 요소 브라우저 패널에서 AEM Forms 컨테이너 구성 요소를 페이지에 드래그 앤 드롭합니다.

   또는 Assets 브라우저에서 적응형 양식 또는 대화형 커뮤니케이션을 검색하고 사이트 페이지로 드래그 앤 드롭할 수 있습니다. AEM Forms 컨테이너에 양식을 임베드합니다.

   >[!NOTE]
   >
   >페이지의 여러 AEM Forms 컨테이너 구성 요소는 지원되지 않습니다.

1. 사이트 페이지에서 임베드된 AEM Forms 컨테이너 구성 요소를 선택한 다음 를 선택합니다. ![settings_icon](assets/settings_icon.png) 작업 표시줄에 표시됩니다. 다음 **[!UICONTROL AEM Forms 컨테이너 편집]** 대화 상자가 열립니다.
1. AEM Forms 컨테이너 편집 대화 상자에서 다음을 지정합니다.

   * **에셋 유형:** 포함할 에셋 유형을 선택합니다. 옵션은 적응형 양식 및 대화형 통신입니다
   * **자산 경로**: 포함할 적응형 양식 또는 대화형 커뮤니케이션을 찾아보고 선택합니다. 에셋 브라우저에서 삭제한 경우 자동으로 채워집니다.
   * (적응형 양식만) **사후 제출**: 양식 제출 시 트리거할 작업을 선택합니다. 감사 메시지 또는 감사 페이지를 표시하도록 선택할 수 있습니다.

      * **감사 인사 메시지**: 서식 있는 텍스트 편집기를 사용하여 메시지를 작성하여 양식 제출 시 표시하십시오. 이 옵션은 감사 메시지를 표시하도록 선택한 경우에만 사용할 수 있습니다.
      * **감사 인사 페이지**: 양식 제출에 표시할 페이지를 검색하여 선택합니다. 이 옵션은 감사 페이지를 표시하도록 선택한 경우에만 사용할 수 있습니다.
      * **제출 시 페이지 새로 고침**: 임베드된 적응형 양식이 포함된 페이지를 새로 고쳐 감사 페이지를 표시할 수 있도록 활성화합니다. 그렇지 않으면 감사 페이지가 페이지를 새로 고치지 않고 AEM Forms 컨테이너의 적응형 양식을 대체합니다. 이 옵션은 감사 페이지를 표시하도록 선택한 경우에만 사용할 수 있습니다.

   * **테마**: 적응형 양식 또는 대화형 통신의 구성 요소에 대한 스타일을 정의하는 테마를 선택합니다. 스타일링에는 글꼴 스타일, 배경색, 치수 및 정렬과 같은 모양 속성이 포함됩니다.
   * **높이**: 컨테이너의 높이를 지정합니다. 컨테이너의 크기를 자동으로 조정하려면 비워 둡니다.
   * **CSS 클라이언트 라이브러리**: CSS 클라이언트 라이브러리의 경로를 지정합니다.

1. 설정을 저장합니다. 이제 적응형 양식 또는 대화형 통신이 페이지에 임베드됩니다.

## 포함된 적응형 양식 및 대화형 통신 게시 {#publishing-embedded-adaptive-form-and-interactive-communication}

AEM sites 페이지에 임베드된 에셋(적응형 양식 또는 대화형 통신)을 게시하기 위한 다음 시나리오를 살펴보겠습니다.

* AEM Sites 페이지를 처음 게시하고 여기에 임베드된 적응형 양식 또는 대화형 통신이 포함된 경우 사이트 페이지와 임베드된 에셋을 게시하십시오.
* 게시된 사이트 페이지에서 임베드된 적응형 양식 또는 대화형 통신만 수정한 경우 원래 에셋을 게시하고 변경 사항은 게시된 사이트 페이지에 반영됩니다. 게시된 사이트 페이지에는 자산에 대한 참조가 포함되어 있으며 페이지를 다시 게시할 필요가 없습니다.
* 사이트 페이지와 포함된 적응형 양식 또는 대화형 통신을 수정한 경우 사이트 페이지와 포함된 자산을 다시 게시하십시오.

## 포함된 적응형 양식 및 대화형 통신 수정 {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM sites 페이지는 AEM Forms 컨테이너에서 적응형 양식 및 대화형 통신에 대한 참조를 유지 관리합니다. 따라서 원래 적응형 양식 및 대화형 통신에 구성된 테마, 스타일 및 제출 동작과 같은 모든 구성 및 속성은 임베드된 적응형 양식 및 대화형 통신에 유지됩니다.

임베드된 적응형 양식 및 대화형 통신의 구성 또는 속성을 수정하려면 다음 중 하나를 수행합니다.

* 각 편집기에서 적응형 양식 또는 대화형 커뮤니케이션에서 원본 양식을 열고 수정합니다.
* 편집 모드로 사이트 페이지 내에서 적응형 양식 또는 대화형 통신을 선택한 다음 을 선택합니다 **[!UICONTROL 새 창에서 편집]**. 원본 양식은 편집 모드에서 열리고 수정할 수 있습니다.

>[!NOTE]
>
>원래 적응형 양식 또는 대화형 커뮤니케이션에서 변경된 사항은 임베드된 양식에 자동으로 반영됩니다. 그러나 적응형 양식, 대화형 통신 또는 사이트 페이지를 다시 게시하여 게시된 페이지의 변경 사항을 반영합니다.

## 고려 사항 및 우수 사례 {#considerations-and-best-practices}

AEM sites 페이지에 적응형 양식을 포함할 때는 다음 사항을 염두에 두십시오.

* 원래 양식의 머리글 및 바닥글은 포함된 양식에 포함되지 않습니다.
* 포함된 양식의 사용자 초안 및 제출은 양식 포털의 초안 및 제출된 Forms 탭에서 지원되고 볼 수 있습니다.
* 원래 양식에 구성된 제출 액션은 포함된 양식에 유지됩니다.
* 원본 양식에 구성된 경험 타깃팅 및 A/B 테스트가 포함된 양식에서 작동하지 않습니다. 하지만 사이트 페이지에서 경험 타깃팅을 사용하여 사용자 프로필에 따라 다른 양식을 표시할 수 있습니다.
* 원래 양식에 대해 Adobe Analytics이 구성된 경우, 임베드된 양식의 분석 데이터가 Adobe Analytics에 캡처됩니다. 하지만 양식 분석 보고서에서는 사용할 수 없습니다.
