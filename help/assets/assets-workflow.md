---
title: 워크플로우를 사용하여 에셋 처리
description: 에셋 처리를 통해 형식 변환, 렌디션 만들기, 에셋 관리, 에셋 유효성 검사 및 워크플로 실행
contentOwner: AG
feature: Workflow, Renditions
role: User, Admin
exl-id: e7c84385-efb3-4997-83ff-7a7f31582469
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 디지털 자산 처리 {#process-assets}

[!DNL Adobe Experience Manager Assets]을(를) 사용하면 강력한 자산 처리를 위해 다양한 방식으로 디지털 자산을 처리할 수 있습니다. 기본 또는 사용자 지정된 처리 방법을 사용하여 전체 비즈니스 프로세스 완료, 감사 및 규정 준수, 검색 및 배포, 디지털 에셋의 기본 온전성을 보장할 수 있습니다. 필요한 규모와 사용자 정의를 달성하면서 에셋 관리 작업을 수행할 수 있습니다.

## 워크플로우 이해 {#understand-workflows}

에셋 처리를 위해 [!DNL Experience Manager]은(는) 워크플로를 사용합니다. 워크플로우는 비즈니스 논리 또는 활동을 자동화하는 데 도움이 됩니다. 특정 작업을 수행하기 위한 세부적인 단계는 기본적으로 제공되며, 개발자는 자신만의 사용자 지정 단계를 만들 수 있습니다. 이러한 단계는 논리적 순서로 결합하여 워크플로우를 만들 수 있습니다. 예를 들어 워크플로우는 업로드된 폴더, 이미지 해상도 등의 특정 기준에 따라 업로드된 이미지에 워터마크를 적용할 수 있습니다. 또 다른 예는 워터마크와 동시에 메타데이터를 추가하고, 렌디션을 만들고, 지능형 태그를 추가하고, 데이터 저장소에 게시하도록 구성된 워크플로우입니다.

## [!DNL Experience Manager]에서 사용할 수 있는 기본 워크플로 {#default-workflows}

기본적으로 업로드된 모든 자산은 [!UICONTROL DAM 자산 업데이트] 워크플로우를 사용하여 처리됩니다. 워크플로는 업로드된 각 에셋에 대해 실행되며 렌디션 생성, 메타데이터 원본에 쓰기, 페이지 추출, 미디어 추출 및 코드 변환과 같은 기본 에셋 관리 작업을 수행합니다.

기본적으로 사용할 수 있는 다양한 워크플로 모델을 보려면 [!DNL Experience Manager]의 **[!UICONTROL 도구 > 워크플로 > 모델]**&#x200B;을 참조하세요.

![기본 워크플로 중 일부](assets/aem-default-workflows.png)

*그림: [!DNL Experience Manager]에서 사용할 수 있는 기본 워크플로 중 일부.*

## 자산을 처리하는 데 워크플로우 적용 {#applying-workflows-to-assets}

디지털 에셋에 워크플로를 적용하는 것은 웹 사이트 페이지와 동일합니다. 워크플로우를 만들고 사용하는 방법에 대한 전체 안내서는 [워크플로우 시작](/help/sites-authoring/workflows-participating.md)을 참조하십시오.

디지털 에셋의 워크플로우를 사용하여 에셋을 활성화하거나 워터마크를 만듭니다. 에셋에 대한 많은 워크플로우는 자동으로 켜집니다. 예를 들어 이미지를 편집한 후 자동으로 렌디션을 만드는 워크플로우는 자동으로 켜집니다.

>[!NOTE]
>
>[!UICONTROL 활성화 요청] 및 [!UICONTROL 비활성화 요청]과 같이 터치 사용 UI에서 클래식 UI에서 사용할 수 있는 워크플로를 사용할 수 없는 경우 [워크플로 모델 만들기](/help/sites-developing/workflows-models.md#classic2touchui)를 참조하십시오.

## 자산에 워크플로우 적용 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
자산에 워크플로우를 적용하려면 다음 단계를 수행합니다.

1. 워크플로우를 시작할 자산의 위치로 이동하고 자산을 클릭하여 자산 페이지를 엽니다. 타임라인을 표시하려면 메뉴에서 **[!UICONTROL 타임라인]**&#x200B;을(를) 선택하십시오.

   ![타임라인-1](assets/timeline.png)

1. 자산에 사용할 수 있는 작업 목록을 열려면 맨 아래에 있는 **[!UICONTROL 작업]**&#x200B;을 클릭하세요.

1. 목록에서 **[!UICONTROL 워크플로 시작]**&#x200B;을 클릭합니다.

1. **[!UICONTROL 워크플로 시작]** 대화 상자의 목록에서 워크플로 모델을 선택합니다.

1. (선택 사항) 워크플로우의 인스턴스를 참조하는 데 사용할 수 있는 워크플로우의 제목을 지정합니다.

   ![워크플로를 선택하고 제목을 입력한 다음 시작을 클릭합니다](assets/start-workflow.png)

1. **[!UICONTROL 시작]**&#x200B;을 클릭한 다음 **[!UICONTROL 진행]**&#x200B;을 클릭합니다. Each step of workflow is displayed in the timeline as an event.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 여러 자산에 워크플로우 적용 {#applying-a-workflow-to-multiple-assets}

1. [!DNL Assets] 콘솔에서 워크플로를 시작할 자산의 위치로 이동한 다음 자산을 선택합니다. 타임라인을 표시하려면 메뉴에서 **[!UICONTROL 타임라인]**&#x200B;을(를) 선택하십시오.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 맨 아래에 있는 **[!UICONTROL 작업]** ![펼침](assets/do-not-localize/chevron-up-icon.png)을 클릭합니다.
1. **[!UICONTROL 워크플로 시작]**&#x200B;을 클릭합니다. **[!UICONTROL 워크플로 시작]** 대화 상자의 목록에서 워크플로 모델을 선택합니다.

   ![워크플로우 시작](assets/start-workflow.png)

1. (선택 사항) 워크플로 인스턴스를 참조하는 데 사용할 수 있는 워크플로의 제목을 지정합니다.
1. Click **[!UICONTROL Start]** and then click **[!UICONTROL Confirm]** in the dialog. 워크플로우는 선택한 모든 에셋에서 실행됩니다.

## 여러 폴더에 워크플로 적용 {#applying-a-workflow-to-multiple-folders}

여러 폴더에 워크플로를 적용하는 절차는 여러 에셋에 워크플로를 적용하는 절차와 유사합니다. [!DNL Assets] 인터페이스에서 폴더를 선택하고 [여러 자산에 워크플로 적용](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets) 절차의 2-7단계를 수행합니다.

## 컬렉션에 워크플로우 적용 {#applying-a-workflow-to-a-collection}

[컬렉션에 워크플로 적용](/help/assets/manage-collections.md#running-a-workflow-on-a-collection)을 참조하세요.

## 자산을 조건부로 처리하는 워크플로우 자동 시작 {#auto-execute-workflow-on-some-assets}

관리자는 사전 정의된 조건에 따라 에셋을 자동으로 실행하고 처리하도록 워크플로우를 구성할 수 있습니다. 이 기능은 특정 폴더에 사용자 정의 워크플로를 만드는 등의 작업을 수행하는 사업부 사용자와 마케터에게 유용합니다. 기획사 사진 촬영의 모든 에셋은 워터마크가 될 수도 있고 프리랜서가 업로드한 모든 에셋을 가공하여 특정 렌디션을 만들 수도 있다고 가정해 보겠습니다.

워크플로우 모델의 경우 사용자는 이를 실행하는 워크플로우 런처를 만들 수 있습니다. 워크플로 시작 관리자는 콘텐츠 저장소의 변경 사항을 모니터링하고 미리 정의된 조건이 충족되면 워크플로를 실행합니다. 관리자는 마케터에게 워크플로를 만들고 런처를 구성할 수 있는 액세스 권한을 제공할 수 있습니다. 사용자는 기본 [!UICONTROL DAM 자산 업데이트] 워크플로우를 수정하여 특정 자산을 처리하는 데 필요한 추가 단계를 추가할 수 있습니다. 워크플로우는 새로 업로드한 모든 에셋에 대해 실행됩니다. 다음 방법 중 하나를 사용하여 특정 에셋에 대한 추가 단계 실행을 제한하십시오.

* [!UICONTROL DAM 자산 업데이트] 워크플로우의 복사본을 만들고 특정 폴더 계층에서 실행되도록 수정하십시오. 이 방법은 몇 개의 폴더에 유용합니다.
* 필요한 수만큼 폴더에 조건부로 적용할 수 있는 [OR 분할](/help/sites-developing/workflows-step-ref.md#or-split)을 사용하여 추가 처리 단계를 추가할 수 있습니다.

## 우수 사례 및 제한 사항 {#best-practices-limitations-tips}

* 워크플로우를 디자인할 때 모든 유형의 표현물에 대한 요구 사항을 고려합니다. 나중에 렌디션이 필요할 것으로 예상되지 않으면 워크플로우에서 렌디션 만들기 단계를 제거합니다. 렌디션은 이후에 일괄 삭제할 수 없습니다. [!DNL Experience Manager]을(를) 장기간 사용하면 원하지 않는 렌디션에 저장 공간이 부족해질 수 있습니다. 개별 에셋의 경우 사용자 인터페이스에서 렌디션을 수동으로 제거할 수 있습니다. 여러 에셋의 경우 특정 표현물을 삭제하도록 [!DNL Experience Manager]을(를) 사용자 지정하거나 에셋을 삭제하고 다시 업로드할 수 있습니다.
* 기본적으로 [!UICONTROL DAM 자산 업데이트] 워크플로우에는 썸네일 및 웹 렌디션을 만드는 몇 가지 단계가 포함되어 있습니다. 워크플로우에서 기본 렌디션을 제거하면 [!DNL Assets]의 사용자 인터페이스가 제대로 렌더링되지 않습니다.

>[!MORELIKETHIS]
>
>* [워크플로 적용 및 참여](/help/sites-authoring/workflows.md)
>* [워크플로 모델 만들기 및 워크플로 기능 확장](/help/sites-developing/workflows.md)
>* [워크플로우를 실행하는 방법](/help/sites-administering/workflows-starting.md)
>* [워크플로우 모범 사례](/help/sites-developing/workflows-best-practices.md)
