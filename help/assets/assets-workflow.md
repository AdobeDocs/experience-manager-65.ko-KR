---
title: 워크플로우를 사용하여 자산 처리
description: 자산 처리를 통해 형식을 변환하고, 표현물을 만들고, 자산을 관리하고, 자산을 확인하고, 워크플로우를 실행합니다.
contentOwner: AG
feature: 워크플로우, 표현물
role: Business Practitioner, Administrator
exl-id: e7c84385-efb3-4997-83ff-7a7f31582469
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# 디지털 자산 처리 {#process-assets}

[!DNL Adobe Experience Manager Assets] 강력한 자산 처리를 위해 여러 가지 방법으로 디지털 자산에서 작업할 수 있습니다. 기본 또는 사용자 정의된 처리 방법을 사용하여 전체 비즈니스 프로세스 완료, 감사 및 규정 준수, 검색 및 배포, 디지털 자산의 기본 안정성을 보장할 수 있습니다. 필요한 규모 및 사용자 지정을 충족하면서 자산 관리 작업을 수행할 수 있습니다.

## 워크플로우 이해 {#understand-workflows}

자산 처리에서 [!DNL Experience Manager] 은 워크플로우를 사용합니다. 워크플로우는 비즈니스 로직 또는 활동을 자동화하는 데 도움이 됩니다. 특정 작업을 수행하는 세부 단계는 기본적으로 제공되며 개발자는 고유한 사용자 지정 단계를 만들 수 있습니다. 이러한 단계를 논리적 순서로 결합하여 워크플로우를 만들 수 있습니다. 예를 들어, 워크플로우는 업로드된 폴더, 이미지 해상도 등과 같은 특정 기준에 따라 업로드된 이미지에 워터마크를 적용할 수 있습니다. 다른 예로는 워터마크 지정 및 메타데이터 동시 추가, 변환 만들기, 지능형 태그 추가, 데이터 저장소에 게시하도록 구성된 워크플로우입니다.

## [!DNL Experience Manager] {#default-workflows}에서 사용할 수 있는 기본 워크플로우

기본적으로 업로드된 모든 자산은 [!UICONTROL DAM 자산 업데이트] 워크플로우를 사용하여 처리됩니다. 워크플로우는 업로드된 각 자산에 대해 실행되며, 표현물 생성, 메타데이터 원본에 쓰기, 페이지 추출, 미디어 추출 및 코드 변환과 같은 기본 자산 관리 작업을 수행합니다.

기본적으로 사용 가능한 다양한 워크플로우 모델을 보려면 [!DNL Experience Manager]에서 **[!UICONTROL 도구 > 워크플로우 > 모델]**&#x200B;을 참조하십시오.

![일부 기본 워크플로우](assets/aem-default-workflows.png)

*그림:일부 기본 워크플로우는에서 사용할 수 있습니다 [!DNL Experience Manager].*

## 워크플로우를 적용하여 자산 {#applying-workflows-to-assets} 처리

디지털 자산에 워크플로우를 적용하는 것은 웹 사이트 페이지와 동일합니다. 워크플로우를 만들고 사용하는 방법에 대한 전체 안내서는 [워크플로우 시작](/help/sites-authoring/workflows-participating.md)을 참조하십시오.

디지털 자산의 워크플로우를 사용하여 자산을 활성화하거나 워터마크를 만듭니다. 자산에 대한 많은 워크플로우가 자동으로 켜집니다. 예를 들어, 이미지를 편집한 후 렌디션을 자동으로 만드는 워크플로우가 자동으로 켜집니다.

>[!NOTE]
>
>클래식 UI에서 사용할 수 있는 워크플로우를 [!UICONTROL 활성화 요청] 및 [!UICONTROL 비활성화 요청]과 같은 터치 지원 UI에서 사용할 수 없는 경우 [워크플로우 모델 만들기](/help/sites-developing/workflows-models.md#classic2touchui)를 참조하십시오.

## 자산에 워크플로우 적용 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
자산에 워크플로우를 적용하려면 다음 단계를 수행합니다.

1. 워크플로우를 시작할 자산의 위치로 이동하고 자산을 클릭하여 자산 페이지를 엽니다. 메뉴에서 **[!UICONTROL 타임라인]**&#x200B;을 선택하여 타임라인을 표시합니다.

   ![타임라인-1](assets/timeline.png)

1. 맨 아래에 있는 **[!UICONTROL 작업]**&#x200B;을 클릭하여 자산에 사용할 수 있는 작업 목록을 엽니다.

1. 목록에서 **[!UICONTROL 워크플로우 시작]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 워크플로우 시작]** 대화 상자의 목록에서 워크플로우 모델을 선택합니다.

1. (선택 사항) 워크플로우의 인스턴스를 참조하는 데 사용할 수 있는 워크플로우의 제목을 지정합니다.

   ![워크플로우 선택, 제목 제공 및 시작 클릭](assets/start-workflow.png)

1. **[!UICONTROL 시작]**&#x200B;을 클릭한 다음 **[!UICONTROL 계속]**&#x200B;을 클릭합니다. 워크플로우의 각 단계는 타임라인에 이벤트로 표시됩니다.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 여러 자산 {#applying-a-workflow-to-multiple-assets}에 워크플로우 적용

1. [!DNL Assets] 콘솔에서 워크플로우를 시작할 자산의 위치로 이동하고 자산을 선택합니다. 메뉴에서 **[!UICONTROL 타임라인]**&#x200B;을 선택하여 타임라인을 표시합니다.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 맨 아래에 있는 **[!UICONTROL 작업]** ![V2/>V](assets/do-not-localize/chevron-up-icon.png)을 클릭합니다.
1. **[!UICONTROL 워크플로우 시작]**&#x200B;을 클릭합니다. **[!UICONTROL 워크플로우 시작]** 대화 상자의 목록에서 워크플로우 모델을 선택합니다.

   ![워크플로우 시작](assets/start-workflow.png)

1. (선택 사항) 워크플로우 인스턴스를 참조하는 데 사용할 수 있는 워크플로우의 제목을 지정합니다.
1. **[!UICONTROL 시작]**&#x200B;을 클릭한 다음 대화 상자에서 **[!UICONTROL 확인]**&#x200B;을 클릭합니다. 워크플로우는 선택한 모든 자산에서 실행됩니다.

## 여러 폴더 {#applying-a-workflow-to-multiple-folders}에 워크플로우 적용

여러 폴더에 워크플로우를 적용하는 절차는 여러 자산에 워크플로우를 적용하는 절차와 유사합니다. [!DNL Assets] 인터페이스에서 폴더를 선택하고 [여러 자산에 워크플로우를 적용하는 2-7단계를 수행합니다](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## 컬렉션에 워크플로우 적용 {#applying-a-workflow-to-a-collection}

[컬렉션에 워크플로우 적용](/help/assets/manage-collections.md#running-a-workflow-on-a-collection)을 참조하십시오.

## 조건부로 자산 {#auto-execute-workflow-on-some-assets}을 처리하는 워크플로우를 자동 시작

관리자는 사전 정의된 조건을 기반으로 자산을 자동으로 실행하고 처리하도록 워크플로우를 구성할 수 있습니다. 이 기능은 비즈니스 부문 사용자 및 마케터에게 유용합니다. 예를 들어 특정 폴더에 사용자 지정 워크플로우를 만들 수 있습니다. 기관의 사진 촬영에서 가져온 모든 자산은 워터마크가 될 수 있으며 프리랜서에서 업로드한 모든 자산을 처리하여 특정 표현물을 만들 수 있다고 가정합니다.

워크플로우 모델의 경우 사용자는 워크플로우 런처를 실행하는 워크플로우 런처를 만들 수 있습니다. 워크플로우 런처는 컨텐츠 저장소의 변경 사항을 모니터링하고 사전 정의된 조건이 충족되면 워크플로우를 실행합니다. 관리자는 마케터에게 워크플로우를 만들고 시작 관리자를 구성하기 위한 액세스 권한을 제공할 수 있습니다. 사용자는 기본 [!UICONTROL DAM 자산 업데이트] 워크플로우를 수정하여 특정 자산을 처리하는 데 필요한 추가 단계를 추가할 수 있습니다. 워크플로우는 새로 업로드한 모든 자산에서 실행됩니다. 다음 방법 중 하나를 사용하여 특정 자산에 대한 추가 단계 실행을 제한합니다.

* [!UICONTROL DAM 자산 업데이트] 워크플로우의 사본을 만들고 이를 수정하여 특정 폴더 계층 구조에서 실행합니다. 이 접근 방식은 몇 개의 폴더에 유용합니다.
* [OR split](/help/sites-developing/workflows-step-ref.md#or-split)을 사용하여 필요에 따라 가능한 한 많은 폴더에 추가로 처리 단계를 추가할 수 있습니다.

## 우수 사례 및 제한 사항 {#best-practices-limitations-tips}

* 워크플로우를 디자인할 때 모든 유형의 표현물에 대한 요구 사항을 고려합니다. 나중에 표현물이 필요할 것으로 예상하지 않으면 워크플로우에서 해당 작성 단계를 제거합니다. 변환은 나중에 일괄 삭제할 수 없습니다. 원치 않는 변환은 [!DNL Experience Manager]을 장시간 사용한 후에 많은 저장 공간이 필요할 수 있습니다. 개별 자산의 경우 사용자 인터페이스에서 렌디션을 수동으로 제거할 수 있습니다. 여러 자산의 경우 [!DNL Experience Manager]을 사용자 지정하여 특정 표현물을 삭제하거나 자산을 삭제하고 다시 업로드할 수 있습니다.
* 기본적으로 [!UICONTROL DAM 자산 업데이트] 워크플로우에는 축소판 및 웹 표현물을 만드는 몇 가지 단계가 포함됩니다. 워크플로우에서 기본 표현물이 제거되면 [!DNL Assets]의 사용자 인터페이스가 제대로 렌더링되지 않습니다.

>[!MORELIKETHIS]
>
>* [워크플로우 적용 및 참여](/help/sites-authoring/workflows.md)
* [워크플로우 모델 만들기 및 워크플로우 기능 확장](/help/sites-developing/workflows.md)
* [워크플로우 실행 방법](/help/sites-administering/workflows-starting.md)
* [워크플로우 모범 사례](/help/sites-developing/workflows-best-practices.md)

