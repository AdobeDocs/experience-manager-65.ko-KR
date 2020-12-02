---
title: 디자인 모드에서 구성 요소 구성
seo-title: 디자인 모드에서 구성 요소 구성
description: AEM 인스턴스가 바로 설치되면 사이드 킥에서 즉시 구성 요소를 선택할 수 있습니다. 이러한 구성 요소 외에 다양한 다른 구성 요소도 사용할 수 있습니다. 디자인 모드를 사용하여 이러한 구성 요소를 활성화/비활성화할 수 있습니다.
seo-description: AEM 인스턴스가 바로 설치되면 사이드 킥에서 즉시 구성 요소를 선택할 수 있습니다. 이러한 구성 요소 외에 다양한 다른 구성 요소도 사용할 수 있습니다. 디자인 모드를 사용하여 이러한 구성 요소를 활성화/비활성화할 수 있습니다.
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 93%

---


# 디자인 모드에서 구성 요소 구성{#configuring-components-in-design-mode}

AEM 인스턴스가 바로 설치되면 사이드 킥에서 즉시 구성 요소를 선택할 수 있습니다.

이러한 구성 요소 외에 다양한 다른 구성 요소도 사용할 수 있습니다. 디자인 모드를 사용하여 [이러한 구성 요소를 활성화/비활성화](#enabledisablecomponentsusingdesignmode)할 수 있습니다. 구성 요소가 활성화되어 사용자 페이지에 있으면 디자인 모드에서 속성 매개 변수를 편집하여 [구성 요소 디자인의 여러 측면을 구성](#configuringcomponentsusingdesignmode)할 수 있습니다.

>[!NOTE]
>
>이러한 구성 요소를 편집할 때는 세심한 주의를 기울여야 합니다. 디자인 설정은 전체 웹 사이트의 디자인에서 핵심적인 부분인 경우가 많으므로 적절한 권한 및 경험을 갖춘 작성자(예: 관리자 또는 개발자)만 이러한 설정을 변경해야 합니다. 자세한 내용은 [구성 요소 개발](/help/sites-developing/components.md)을 참조하십시오.

실제로는 페이지의 단락 시스템에서 허용되는 구성 요소를 추가 또는 제거하게 됩니다. 단락 시스템(`parsys`)은 다른 모든 단락 구성 요소를 포함하는 복합 구성 요소입니다. 단락 시스템에는 다른 단락 구성 요소도 모두 포함되어 있으므로 작성자가 여러 유형의 구성 요소를 페이지에 추가할 수 있습니다. 각 단락 유형은 구성 요소로 표현됩니다. 

예를 들어 제품 페이지의 컨텐츠에는 다음을 포함하는 단락 시스템이 있을 수 있습니다.

* 제품 이미지(이미지 또는 텍스트 이미지 단락 형태)
* 제품 설명(텍스트 단락)
* 기술 데이터가 기재된 표(표 단락 형태)
* 사용자가 입력하는 양식(양식 시작, 양식 요소 및 양식 끝 단락)

>[!NOTE]
>
>[에 대한 자세한 내용은 ](/help/sites-developing/components.md#paragraphsystem)구성 요소 개발[ 및 ](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components)템플릿 및 구성 요소 사용 지침`parsys`을 참조하십시오.

## 구성 요소 활성화/비활성화 {#enable-disable-components}

디자인 모드에서는 사이드 킥이 최소화되고 작성을 위해 액세스할 수 있는 구성 요소를 구성할 수 있습니다.

1. 디자인 모드를 시작하려면 편집할 페이지를 열고 사이드 킥 아이콘을 사용합니다.

   ![](do-not-localize/chlimage_1.png)

1. 단락 시스템에서 **편집**(**단락 디자인**)을 클릭합니다.

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. 대화 상자가 열리면서 사이드 킥에 표시된 구성 요소 그룹이 해당 그룹에 포함된 개별 구성 요소와 함께 나열됩니다.

   사이드 킥에서 사용할 수 있도록 구성 요소를 추가하거나 제거하려면 필요에 따라 선택하십시오.

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. 디자인 모드에서는 사이드 킥이 최소화됩니다. 화살표를 클릭하면 사이드 킥을 최대화하고 편집 모드로 돌아갈 수 있습니다.

   ![](do-not-localize/sidekick-collapsed.png)

## 구성 요소 디자인 구성 {#configuring-the-design-of-a-component}

디자인 모드에서 개별 구성 요소에 대한 속성을 구성할 수도 있습니다. 각 구성 요소에는 자체 매개 변수가 있습니다. 다음 예는 **이미지** 구성 요소를 보여 줍니다.

1. 디자인 모드를 시작하려면 편집할 페이지를 열고 사이드 킥 아이콘을 사용합니다.

   ![](do-not-localize/chlimage_1-1.png)

1. 구성 요소의 디자인을 구성할 수 있습니다.

   예를 들어 이미지 구성 요소(**이미지 디자인**)에서 **편집**&#x200B;을 클릭하면 구성 요소별 매개 변수를 구성할 수 있습니다.

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. **확인**&#x200B;을 클릭하여 변경 사항을 저장합니다.

1. 디자인 모드에서는 사이드 킥이 최소화됩니다. 화살표를 클릭하면 사이드 킥을 최대화하고 편집 모드로 돌아갈 수 있습니다.

   ![](do-not-localize/sidekick-collapsed-1.png)
