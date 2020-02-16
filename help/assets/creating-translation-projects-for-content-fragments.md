---
title: 컨텐츠 조각에 대한 번역 프로젝트 만들기
seo-title: 컨텐츠 조각에 대한 번역 프로젝트 만들기
description: 컨텐츠 조각을 변환하는 방법을 알아봅니다.
seo-description: 컨텐츠 조각을 변환하는 방법을 알아봅니다.
uuid: 23176e70-4003-453c-af25-6499a5ed3f6d
contentOwner: heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: d2decc31-a04b-4a8e-bb19-65f21cf7107e
translation-type: tm+mt
source-git-commit: 48fd5ddb386d69795291e560fa7b21da6edf5979

---


# 컨텐츠 조각에 대한 번역 프로젝트 만들기 {#creating-translation-projects-for-content-fragments}

자산 외에도 Adobe Experience Manager(AEM) 자산은 [컨텐츠 조각](content-fragments.md) (변형 포함)에 대한 언어 복사 워크플로우를 지원합니다. 컨텐츠 조각에서 언어 복사 워크플로우를 실행하는 데 추가로 최적화할 필요가 없습니다. 각 워크플로우에서 번역용으로 전체 컨텐츠 조각이 전송됩니다.

컨텐츠 조각에서 실행할 수 있는 워크플로우 유형은 자산에 대해 실행하는 워크플로우 유형과 정확하게 유사합니다. 또한 각 워크플로우 유형 내에서 사용할 수 있는 옵션은 자산에 대해 해당 워크플로우 유형 아래에서 사용할 수 있는 옵션과 일치합니다.

컨텐츠 조각에서 다음 유형의 언어 복사 워크플로우를 실행할 수 있습니다.

**작성 및 번역**

이 워크플로우에서 번역될 컨텐츠 조각은 번역할 언어의 언어 루트로 복사됩니다. 또한 선택한 옵션에 따라 프로젝트 콘솔에서 컨텐츠 조각에 대한 번역 프로젝트가 생성됩니다. 설정에 따라 번역 프로젝트를 수동으로 시작하거나 번역 프로젝트를 만드는 즉시 자동으로 실행할 수 있습니다.

**언어 복사 업데이트**

소스 컨텐츠 조각을 업데이트하거나 수정할 때 해당 로케일/언어별 컨텐츠 조각은 다시 번역해야 합니다. 언어 사본 업데이트 워크플로우는 컨텐츠 조각 그룹을 추가로 번역하여 특정 로케일의 언어 복사본에 포함합니다. 이 경우 번역된 컨텐츠 조각은 이전에 번역된 컨텐츠 조각을 이미 포함하는 대상 폴더에 추가됩니다.

## 워크플로우 작성 및 번역 {#create-and-translate-workflow}

만들기 및 번역 워크플로우에는 다음 옵션이 포함되어 있습니다. 각 옵션과 관련된 절차적 단계는 자산의 해당 옵션과 관련된 단계와 유사합니다.

* 구조만 만들기:절차 단계는 자산에만 [대한 구조 만들기를 참조하십시오](translation-projects.md#create-structure-only).
* 새 번역 프로젝트 만들기:절차 단계는 [자산에](translation-projects.md#create-a-new-translation-project)대한 새 번역 프로젝트 만들기를 참조하십시오.
* 기존 번역 프로젝트에 추가:절차 단계는 자산의 [기존 번역 프로젝트에 추가를 참조하십시오](translation-projects.md#add-to-existing-translation-project).

## 언어 사본 업데이트 워크플로우 {#update-language-copies-workflow}

언어 사본 업데이트 워크플로우에는 다음 옵션이 포함되어 있습니다. 각 옵션과 관련된 절차적 단계는 자산의 해당 옵션과 관련된 단계와 유사합니다.

* 새 번역 프로젝트 만들기:절차 단계는 자산에 [대한 새 번역 프로젝트 만들기](translation-projects.md#create-a-new-translation-project) (업데이트 워크플로우)를 참조하십시오.
* 기존 번역 프로젝트에 추가:절차 단계는 기존 번역 [프로젝트에 자산](translation-projects.md#add-to-existing-translation-project) 추가(업데이트 워크플로우)를 참조하십시오.

에셋에 대한 임시 복사본을 만드는 방법과 유사한 방식으로 조각에 대한 임시 언어 사본을 만들 수도 있습니다. 자세한 내용은 자산에 [대한 임시 언어 사본](translation-projects.md#creating-temporary-language-copies)만들기를 참조하십시오.

## 혼합 미디어 조각 변환 {#translating-mixed-media-fragments}

AEM에서는 다양한 유형의 미디어 자산 및 컬렉션을 포함하는 컨텐츠 조각을 변환할 수 있습니다. 인라인 자산을 포함하는 컨텐츠 조각을 번역할 경우 이러한 자산의 번역된 사본은 대상 언어 루트 아래에 저장됩니다.

콘텐츠 조각에 컬렉션이 포함된 경우 컬렉션 내의 자산은 컨텐츠 조각과 함께 변환됩니다. 번역된 에셋 사본은 소스 언어 루트 아래의 소스 에셋의 실제 위치와 일치하는 위치의 적절한 대상 언어 루트 내에 저장됩니다.

혼합 미디어가 포함된 컨텐츠 조각을 번역할 수 있도록 하려면 먼저 기본 번역 프레임워크를 편집하여 콘텐츠 조각과 연결된 인라인 에셋 및 컬렉션을 번역할 수 있도록 합니다.

1. AEM 로고를 클릭/탭하고 도구 > 배포 **[!UICONTROL > 클라우드 서비스로 이동합니다]**.
1. Adobe **[!UICONTROL Marketing Cloud에서]** 번역 **[!UICONTROL 통합을]**&#x200B;찾아 구성 표시를 클릭/ **[!UICONTROL 탭합니다]**.

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. 사용 가능한 구성 목록에서 기본 구성( **[!UICONTROL 번역 통합 구성)]** 을 클릭/탭하여 기본 구성 **** 페이지를 엽니다.

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. 도구 **[!UICONTROL 모음에서 편집을]** 클릭하여 번역 구성 **[!UICONTROL 대화 상자를]** 표시합니다.

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. 자산 탭으로 **[!UICONTROL 이동하고]** 콘텐츠 조각 자산 번역 **[!UICONTROL 목록에서]** 인라인 미디어 자산 및 관련 **[!UICONTROL 컬렉션을]** 선택합니다. Click/tap **[!UICONTROL OK]** to save the changes.

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. 영어 루트 폴더 내에서 컨텐츠 조각을 엽니다.

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. 자산 삽입 **[!UICONTROL 아이콘을 클릭/]** 탭합니다.

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. 자산을 컨텐츠 조각에 삽입합니다.

   ![컨텐츠 조각에 에셋 삽입](assets/column-view.png)

1. 콘텐츠 연결 **[!UICONTROL 아이콘을 클릭/탭합니다]** .

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. 콘텐츠 연결을 클릭/ **[!UICONTROL 탭합니다]**.

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. 컬렉션을 선택하고 콘텐츠 조각에 포함합니다. Click/tap **[!UICONTROL Save]**.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. 컨텐츠 조각을 선택하고 GlobalNav **[!UICONTROL 아이콘을 클릭/탭합니다]** .
1. 메뉴에서 **[!UICONTROL 참조를]** 선택하여 참조 **[!UICONTROL 창을 표시합니다]** .

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. 사본 **[!UICONTROL 아래의 언어]** 사본을 클릭/탭하여 **** 언어 사본을 표시합니다.

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. 패널 아래쪽에서 **[!UICONTROL 만들기 및]** 번역을 클릭/탭하여 만들기 및 번역 **[!UICONTROL 대화 상자를 표시합니다]** .

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. 타겟 언어 목록에서 타겟 **[!UICONTROL 언어를]** 선택합니다.

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. 프로젝트 목록에서 번역 프로젝트 유형을 **[!UICONTROL 선택합니다]** .

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. 프로젝트 제목 상자에서 프로젝트 제목을 **[!UICONTROL 지정한]** 다음 만들기를 클릭/ **탭합니다**.

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. 프로젝트 **[!UICONTROL 콘솔로]** 이동하고 만든 번역 프로젝트의 프로젝트 폴더를 엽니다.

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. 프로젝트 타일을 클릭/탭하여 프로젝트 세부 사항 페이지를 엽니다.

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. 번역 작업 타일에서 변환할 자산의 수를 확인합니다.
1. 번역 **[!UICONTROL 작업]** 타일에서 번역 작업을 시작합니다.

   ![chlimage_1-461](assets/chlimage_1-462.png)

1. 번역 작업 타일 하단의 줄임표를 클릭하여 번역 작업의 상태를 표시합니다.

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. 컨텐츠 조각을 클릭/탭하여 번역된 관련 자산의 경로를 확인합니다.

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. 컬렉션 콘솔에서 컬렉션의 언어 사본을 검토합니다.

   ![chlimage_1-465](assets/chlimage_1-465.png)

   컬렉션의 콘텐츠만 변환됩니다. 컬렉션 자체는 번역되지 않습니다.

1. 번역된 관련 자산의 경로로 이동합니다. 번역된 에셋이 대상 언어 루트 아래에 저장되었는지 확인합니다.

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. 콘텐츠 조각과 함께 번역되는 컬렉션 내의 자산으로 이동합니다. 번역된 에셋 사본은 적절한 대상 언어 루트에 저장됩니다.

   ![chlimage_1-468](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >기존 프로젝트에 컨텐츠 조각을 추가하거나 업데이트 워크플로우를 수행하기 위한 절차는 자산의 해당 절차와 유사합니다. 이러한 절차에 대한 지침은 자산에 대해 설명된 절차를 참조하십시오.

