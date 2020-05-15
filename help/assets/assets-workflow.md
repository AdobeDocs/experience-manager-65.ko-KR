---
title: 자산을 처리하여 업무 처리 과정 수행, 감사, 규정 준수, 기본적인 안정성 유지
description: 자산 처리를 사용하여 형식을 변환하고, 변환을 만들고, 자산을 관리하고, 자산을 확인하고, 워크플로우를 실행합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 94f7f2cde3c87ed4693b9e2004f80fc5f0cd9855
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---


# 디지털 자산 처리 {#process-assets}

[!DNL Adobe Experience Manager Assets] 강력한 자산 처리를 위해 다양한 방법으로 디지털 자산 작업을 수행할 수 있습니다. 기본 또는 사용자 지정 처리 방법을 사용하여 전체 비즈니스 프로세스 완료, 감사 및 규정 준수, 검색 및 배포, 디지털 자산의 기본적인 안정성 보장 등을 보장할 수 있습니다. 필요한 규모 및 사용자 지정을 수행하면서 에셋 관리 작업을 수행할 수 있습니다.

## 워크플로우 이해 {#understand-workflows}

자산 처리를 위해 워크플로우를 [!DNL Experience Manager] 사용합니다. 워크플로우는 비즈니스 논리 또는 활동을 자동화합니다. 특정 작업을 수행하는 세부 단계는 기본적으로 제공되며 개발자는 고유한 사용자 지정 단계를 만들 수 있습니다. 이러한 단계를 논리적 순서로 결합하여 워크플로우를 만들 수 있습니다. 예를 들어 워크플로우는 업로드된 폴더, 이미지 해상도 등과 같은 특정 기준을 기반으로 업로드된 이미지에 워터마크를 적용할 수 있습니다. 또 다른 예로 워터마크 및 동시에 메타데이터를 추가하고 변환을 만들고, 지능형 태그를 추가하고 데이터 저장소에 게시하도록 구성된 워크플로우가 있습니다.

## 기본 작업 과정은 [!DNL Experience Manager] {#default-workflows}

기본적으로 업로드된 모든 자산은 [!UICONTROL DAM 자산 업데이트 워크플로우를 사용하여] 처리됩니다. 이 워크플로우는 업로드된 각 자산에 대해 실행되고 변환 생성, 메타데이터 쓰기 되돌리기, 페이지 추출, 미디어 추출 및 트랜스코딩과 같은 기본 자산 관리 작업을 수행합니다.

기본적으로 사용할 수 있는 다양한 워크플로우 모델을 보려면 **[!UICONTROL 도구 > 워크플로우 > 모델]** 을 [!DNL Experience Manager]참조하십시오.

![일부 기본 워크플로우](assets/aem-default-workflows.png)

*그림: 일부 기본 워크플로우는 에서 사용할 수 있습니다[!DNL Experience Manager].*

## Apply workflows to process assets {#applying-workflows-to-assets}

디지털 자산에 워크플로우를 적용하는 것은 웹 사이트 페이지의 워크플로우와 동일합니다. 워크플로우 생성 및 사용 방법에 대한 전체 지침은 워크플로우 [시작을 참조하십시오](/help/sites-authoring/workflows-participating.md).

디지털 자산의 워크플로우를 사용하여 자산을 활성화하거나 워터마크를 만들 수 있습니다. 자산에 대한 많은 워크플로우가 자동으로 켜집니다. 예를 들어, 이미지를 편집한 후 자동으로 표현물을 만드는 워크플로우가 자동으로 켜집니다.

>[!NOTE]
>
>클래식 UI에서 사용 가능한 워크플로우를 활성화 요청 및 [!UICONTROL 비활성화 요청] 과 같은 터치 지원 UI에서 사용할 수 없는 경우 [!UICONTROL 워크플로우 모델]만들기를 [참조하십시오](/help/sites-developing/workflows-models.md#classic2touchui).

## 자산에 워크플로우 적용 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
자산에 워크플로우를 적용하려면 다음 단계를 따르십시오.

1. 워크플로우를 시작할 자산의 위치로 이동하고 자산을 클릭하여 자산 페이지를 엽니다. 메뉴에서 **[!UICONTROL 타임라인]** 을 선택하여 타임라인을 표시합니다.

   ![timeline-1](assets/timeline.png)

1. 맨 아래 **[!UICONTROL 에서 작업을]** 클릭하여 자산에 사용할 수 있는 작업 목록을 엽니다.

1. 목록에서 **[!UICONTROL 워크플로우]** 시작을 클릭합니다.

1. 워크플로우 **[!UICONTROL 시작]** 대화 상자의 목록에서 워크플로우 모델을 선택합니다.

   ![chlimage_1-254](assets/chlimage_1-50.png)

1. (선택 사항) 워크플로우의 인스턴스를 참조하는 데 사용할 수 있는 워크플로우의 제목을 지정합니다.

   ![chlimage_1-255](assets/chlimage_1-51.png)

1. 시작 **[!UICONTROL 을]** 클릭한 다음 **[!UICONTROL 진행을 클릭합니다]**. 각 워크플로우 단계가 이벤트로 타임라인에 표시됩니다.

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 여러 자산에 워크플로우 적용 {#applying-a-workflow-to-multiple-assets}

1. 자산 콘솔에서 워크플로우를 시작할 자산의 위치로 이동하고 자산을 선택합니다. 메뉴에서 **[!UICONTROL 타임라인]** 을 선택하여 타임라인을 표시합니다.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 맨 아래 **[!UICONTROL 에서]** 작업을 클릭합니다.

   ![chlimage_1-30](assets/chlimage_1-137.png)

1. 워크플로우 **[!UICONTROL 시작을 클릭합니다]**. 워크플로우 **[!UICONTROL 시작]** 대화 상자의 목록에서 워크플로우 모델을 선택합니다.

   ![chlimage_1-31](assets/chlimage_1-138.png)

1. (선택 사항) 워크플로우 인스턴스를 참조하는 데 사용할 수 있는 워크플로우의 제목을 지정합니다.
1. 시작 **[!UICONTROL 을]** 클릭한 다음 대화 **[!UICONTROL 상자에서]** 확인을 클릭합니다. 워크플로우는 선택한 모든 자산에서 실행됩니다.

## 여러 폴더에 워크플로우 적용 {#applying-a-workflow-to-multiple-folders}

여러 폴더에 워크플로우를 적용하는 절차는 여러 자산에 워크플로우를 적용하는 절차와 유사합니다. 인터페이스에서 폴더를 [!DNL Assets] 선택하고 절차의 2-7단계를 수행하여 여러 자산에 워크플로우를 [적용합니다](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## 컬렉션에 워크플로우 적용 {#applying-a-workflow-to-a-collection}

컬렉션에 워크플로우 [적용을 참조하십시오](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection).

## 조건부로 자산을 처리하는 워크플로우 자동 시작 {#auto-execute-workflow-on-some-assets}

관리자는 미리 정의된 조건을 기반으로 자산을 자동으로 실행하고 처리하도록 워크플로우를 구성할 수 있습니다. 이 기능은 비즈니스 라인 사용자와 마케터에게 유용합니다. 예를 들어 특정 폴더에 사용자 정의 워크플로우를 만들 수 있습니다. 기관의 사진 촬영에서 나온 모든 에셋을 워터마크가 될 수 있고 프리랜서가 업로드한 모든 에셋을 처리하여 특정 표현물을 만들 수 있다고 가정해 보십시오.

워크플로우 모델의 경우 사용자는 워크플로우 런처를 실행하는 워크플로우 런처를 만들 수 있습니다. 워크플로우 론처는 컨텐츠 저장소의 변경 사항을 모니터링하고 사전 정의된 조건이 충족되면 워크플로우를 실행합니다. 관리자는 마케터에게 워크플로우를 만들고 런처를 구성할 수 있는 액세스 권한을 제공할 수 있습니다. 사용자는 기본 [!UICONTROL DAM 자산] 업데이트 워크플로우를 수정하여 특정 자산을 처리하는 데 필요한 추가 단계를 추가할 수 있습니다. 워크플로우는 새로 업로드된 모든 자산에서 실행됩니다. 다음 방법 중 하나를 사용하여 특정 자산에 대한 추가 단계 실행을 제한합니다.

* DAM 자산 [!UICONTROL 업데이트] 작업 과정의 복사본을 만들고 특정 폴더 계층 구조에서 실행되도록 수정합니다. 이 방법은 몇 개의 폴더에 유용합니다.
* 필요한 만큼 많은 폴더에 조건부로 적용할 수 있는 [OR 분할을](/help/sites-developing/workflows-step-ref.md#or-split) 사용하여 추가 처리 단계를 추가할 수 있습니다.

## 모범 사례 및 제한 사항 {#best-practices-limitations-tips}

* 워크플로우를 설계할 때 모든 유형의 변환에 대한 요구 사항을 고려합니다. 나중에 변환의 필요성을 예측할 수 없는 경우 워크플로우에서 변환 생성 단계를 제거합니다. 나중에 변환을 일괄 삭제할 수 없습니다. 장기 사용 후 원치 않는 변환이 많은 저장 공간을 차지할 수 있습니다 [!DNL Experience Manager]. 개별 자산의 경우 사용자 인터페이스에서 변환을 수동으로 제거할 수 있습니다. 여러 자산의 경우 특정 표현물을 삭제하도록 사용자 [!DNL Experience Manager] 지정하거나 자산을 삭제하고 다시 업로드할 수 있습니다.

>[!MORELIKETHIS]
>
>* [워크플로우 적용 및 참여](/help/sites-authoring/workflows.md)
>* [워크플로우 모델 생성 및 워크플로우 기능 확장](/help/sites-developing/workflows.md)
>* [워크플로우 실행 방법](/help/sites-administering/workflows-starting.md)
>* [워크플로우 모범 사례](/help/sites-developing/workflows-best-practices.md)
>* [워크플로우를 사용하여 자산 수정에 대한 커뮤니티 아티클](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)

