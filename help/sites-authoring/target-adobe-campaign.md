---
title: Adobe Campaign 타기팅
description: 세그먼테이션을 설정한 후 Adobe Campaign에 대한 타겟팅된 경험을 만들 수 있습니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 1%

---

# Adobe Campaign 타기팅{#targeting-your-adobe-campaign}

Adobe Campaign 뉴스레터를 타겟팅하려면 먼저 Classic UI에서만 사용할 수 있는 세그먼테이션을 설정해야 합니다(클라이언트 컨텍스트용). 그런 다음 Adobe Campaign에 대한 타겟팅된 경험을 만들 수 있습니다. 두 가지 모두 이 섹션에 설명되어 있습니다.

## AEM에서 세그먼테이션 설정 {#setting-up-segmentation-in-aem}

세그먼테이션을 설정하려면 클래식 UI를 사용하여 세그먼트를 설정해야 합니다. 나머지 단계는 표준 UI에서 수행할 수 있습니다.

세그먼테이션 설정에는 세그먼트, 브랜드, 캠페인 및 경험 만들기가 포함됩니다.

>[!NOTE]
>
>세그먼트 ID는 Adobe Campaign 측의 세그먼트 ID에 매핑해야 합니다.

### 세그먼트 만들기 {#creating-segments}

세그먼트를 만들려면 다음 작업을 수행하십시오.

1. [&lt;host>:&lt;port>/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation)에서 **세그먼테이션 콘솔**&#x200B;을 엽니다.
1. 페이지를 만들고 제목(예: **AC 세그먼트**)을 입력한 다음 **세그먼트(Adobe Campaign)** 템플릿을 선택합니다.
1. 왼쪽의 트리 보기에서 만든 페이지를 선택합니다.
1. 만든 세그먼트 아래에 Male이라는 페이지를 만들어 남성 사용자를 타깃팅하는 등의 방법으로 세그먼트를 만들고 **세그먼트(Adobe Campaign)** 템플릿을 선택합니다.
1. 만든 세그먼트 페이지를 열고 **세그먼트 ID**&#x200B;를 사이드 킥에서 페이지로 끌어다 놓습니다.
1. 트레이트를 두 번 클릭하고, 이 경우 Adobe Campaign에 정의된 남성 세그먼트를 나타내는 ID를 입력한 다음(예: **MALE**) **확인**&#x200B;을 클릭합니다. 다음 메시지가 표시됩니다. *`targetData.segmentCode == "MALE"`*
1. 다른 세그먼트(예: 여성 사용자를 타겟팅하는 세그먼트)에 대해 단계를 반복합니다.

### 브랜드 만들기 {#creating-a-brand}

브랜드를 만들려면:

1. **사이트**&#x200B;에서 **캠페인** 폴더(예: We.Retail)로 이동합니다.
1. **페이지 만들기**&#x200B;를 클릭하고 페이지 제목(예: We.Retail 브랜드)을 입력한 다음 **브랜드** 템플릿을 선택합니다.

### 캠페인 생성 {#creating-a-campaign}

캠페인을 만들려면 다음 작업을 수행하십시오.

1. 만든 **브랜드** 페이지를 엽니다.
1. **페이지 만들기**&#x200B;를 클릭하고 페이지 제목(예: We.Retail 캠페인)을 입력한 다음 **캠페인** 템플릿을 선택하고 **만들기**&#x200B;를 클릭합니다.

### 경험 만들기 {#creating-experiences}

세그먼트를 위한 경험을 만들려면 다음 작업을 수행하십시오.

1. 만든 **Campaign** 페이지를 엽니다.
1. **페이지 만들기**&#x200B;를 클릭하고 페이지의 제목(예: 남성 세그먼트에 대한 경험을 만들 때 남성)을 입력하여 세그먼트에 대한 경험을 만들고 **경험** 템플릿을 선택합니다.
1. 생성된 경험 페이지를 엽니다.
1. **편집**&#x200B;을 클릭한 다음 세그먼트 아래에서 **항목 추가**&#x200B;를 클릭합니다.
1. 남성 세그먼트의 경로(예: **/etc/segmentation/ac-segments/male**)를 입력하고 **확인**&#x200B;을 클릭합니다. 다음 메시지가 표시되어야 합니다. *경험이 타깃팅됨: 남성*
1. 모든 세그먼트(예: 여성 타겟)에 대한 경험을 만들려면 이전 단계를 반복하십시오.
