---
title: 메타데이터, 이미지 및 비디오 처리 프로필
description: 프로필은 폴더에 업로드된 자산에 적용할 옵션에 대한 규칙 세트입니다. 업로드한 비디오 자산에 적용할 메타데이터 프로필 및 비디오 인코딩 프로필을 지정합니다. 이미지 자산의 경우 이미지 자산에 적용할 이미징 프로필을 지정하여 이미지 자산을 제대로 잘릴 수도 있습니다.
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
role: Business Practitioner, Administrator
feature: 워크플로우,자산 관리,표현물
exl-id: 3d9367ed-5a02-43aa-abd9-24fae457d4c5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 0%

---

# 메타데이터, 이미지 및 비디오 처리를 위한 프로필{#profiles-for-processing-metadata-images-and-videos}

프로필은 폴더에 업로드되는 자산에 적용할 옵션에 대한 레서피입니다. 예를 들어 업로드하는 비디오 자산에 적용할 메타데이터 프로필 및 비디오 인코딩 프로필을 지정할 수 있습니다. 또는 이미지 자산에 적용할 이미징 프로필로 제대로 잘립니다.

이러한 규칙에는 메타데이터 추가, 이미지 스마트 자르기 또는 비디오 인코딩 프로필 설정이 포함될 수 있습니다. AEM에서 다음 링크에서 자세히 다룹니다. 세 가지 유형의 프로필을 만들 수 있습니다.

* [메타데이터 프로필](/help/assets/metadata-config.md#metadata-profiles)
* [이미지 프로필](/help/assets/image-profiles.md)
* [비디오 프로필](/help/assets/video-profiles.md)

메타데이터, 이미지 또는 비디오 프로필을 만들고, 편집하고, 삭제하려면 관리자 권한이 있어야 합니다.

메타데이터, 이미지 또는 비디오 프로필을 만든 후 새로 업로드한 자산의 대상으로 사용하는 하나 이상의 폴더에 할당합니다.

AEM Assets에서 프로필 사용과 관련된 중요한 개념은 프로필에 폴더가 할당된다는 것입니다. 프로필 내에는 비디오 프로필 또는 이미지 프로필과 함께 메타데이터 프로필 형식의 설정이 있습니다. 이러한 설정은 폴더의 컨텐츠를 하위 폴더와 함께 처리합니다. 따라서 파일 및 폴더의 이름 지정 방법, 하위 폴더 정렬 방법 및 이러한 폴더 내의 파일을 처리하는 방법은 프로필에서 해당 자산을 처리하는 방법에 큰 영향을 줍니다.
일관된 적절한 파일 및 폴더 이름 지정 전략을 좋은 메타데이터 방식과 함께 사용하면 디지털 자산 수집을 최대한 활용하고 올바른 프로필에 의해 올바른 파일이 처리되도록 할 수 있습니다.

>[!NOTE]
>
>한 폴더에서 다른 폴더로 이동하는 자산은 다시 처리되지 않습니다. 예를 들어, 프로파일 A가 지정된 폴더 1과 프로파일 B가 지정된 폴더 2가 있다고 가정합니다. 자산을 폴더 1에서 폴더 2로 이동하는 경우, 이동된 자산은 폴더 1의 원래 처리를 유지합니다.
>
>동일한 프로필이 할당된 두 폴더 간에 자산을 이동하는 경우에도 마찬가지입니다.

## {#reprocessing-assets} 폴더에서 자산 재처리

>[!NOTE]
>
>AEM 6.4.6.0 이상에서만 *Dynamic Media - Scene7 모드*&#x200B;에 적용됩니다.

나중에 변경한 기존 처리 프로필이 이미 있는 폴더에서 자산을 재처리할 수 있습니다.

예를 들어 이미지 프로필을 만들어 폴더에 할당했다고 가정합니다. 폴더에 업로드한 모든 이미지 자산에는 자동으로 이미지 프로필이 자산에 적용되었습니다. 하지만 나중에 프로필에 새로운 스마트 자르기 비율을 추가하기로 합니다. 이제 자산을 선택하고 다시 폴더에 업로드하는 대신 *Scene7을 실행하기만 하면 됩니다.자산* 워크플로우를 다시 처리합니다.

처음으로 처리가 실패한 자산에서 재처리 워크플로우를 실행할 수 있습니다. 따라서 처리 프로필을 편집하지 않았거나 처리 프로필을 적용하지 않았더라도 언제든지 자산 폴더에서 재처리 워크플로우를 실행할 수 있습니다.

선택적으로 재처리 워크플로우의 배치 크기를 최대 1000개의 자산인 기본값 50개에서 조정할 수 있습니다. _Scene7을 실행하는 경우:폴더에서 자산_ 워크플로우를 재처리하는 경우 자산은 일괄로 그룹화된 다음 처리를 위해 Dynamic Media 서버로 전송됩니다. 처리 후, 전체 배치 세트에 있는 각 자산의 메타데이터가 AEM에서 업데이트됩니다. 일괄 처리 크기가 매우 큰 경우 처리가 지연될 수 있습니다. 또는 일괄 처리 크기가 너무 작으면 Dynamic Media 서버로 라운드 트립이 너무 많이 발생할 수 있습니다.

[재처리 워크플로우의 일괄 처리 크기 조정](#adjusting-load)을 참조하십시오.

>[!NOTE]
>
>Dynamic Media Classic에서 AEM으로 자산의 벌크 마이그레이션을 수행하는 경우 Dynamic Media 서버에서 마이그레이션 복제 에이전트를 활성화해야 합니다. 마이그레이션이 완료되면 에이전트를 비활성화해야 합니다.
>
>Dynamic Media 서버에서 마이그레이션 게시 에이전트를 비활성화해야 재처리 워크플로우가 예상대로 작동합니다.

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**폴더에서 자산을 재처리하려면 다음을 수행하십시오**.
1. AEM의 자산 페이지에서 처리 프로필이 할당된 자산의 폴더로 이동하고 **Scene7을 적용할 자산의 폴더로 이동합니다.자산 재처리** 워크플로우,

   처리 프로필이 이미 할당된 폴더는 카드 보기에서 폴더 이름 바로 아래에 프로필 이름이 표시되어 표시됩니다.

1. 폴더를 선택합니다.

   * 워크플로우는 선택한 폴더의 모든 파일을 재귀적으로 고려합니다.
   * 기본 선택한 폴더에 자산이 있는 하위 폴더가 하나 이상 있는 경우 워크플로우는 폴더 계층 구조의 모든 자산을 다시 처리합니다.
   * 자산이 1000개 이상인 폴더 계층 구조에서 이 워크플로우를 실행하지 않는 것이 좋습니다.

1. 페이지의 왼쪽 위 모서리 근처에 있는 드롭다운 목록에서 **[!UICONTROL 타임라인 을 클릭합니다.]**
1. 페이지의 왼쪽 아래 모서리 근처에 있는 댓글 필드 오른쪽에 있는 캐럿 아이콘( **^** )을 클릭합니다.

   ![자산 워크플로우 재처리 1](/help/assets/assets/reprocess-assets1.png)

1. **[!UICONTROL 워크플로우 시작 을 클릭합니다.]**
1. **[!UICONTROL 워크플로우 시작]** 드롭다운 목록에서 **[!UICONTROL Scene7을 선택합니다.자산을 재처리합니다.]**
1. (선택 사항) **워크플로우 제목 입력** 텍스트 필드에 워크플로우의 이름을 입력합니다. 필요한 경우 이름을 사용하여 워크플로우 인스턴스를 참조할 수 있습니다.

   ![자산 재처리 2](/help/assets/assets/reprocess-assets2.png)

1. **[!UICONTROL 시작]**&#x200B;을 클릭한 다음 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   워크플로우를 모니터링하거나 진행 상황을 확인하려면 AEM 주 콘솔 페이지에서 **[!UICONTROL 도구 > 워크플로우를 클릭합니다.]** 워크플로우 인스턴스 페이지에서 워크플로우를 선택합니다. 메뉴 모음에서 **[!UICONTROL 기록 열기를 클릭합니다.]** 동일한 [워크플로우 인스턴스] 페이지에서 선택한 워크플로우를 종료, 일시 중단 또는 이름을 변경할 수도 있습니다.

### 재처리 워크플로우의 일괄 처리 크기 조정 {#adjusting-load}

(선택 사항) 재처리 워크플로우의 기본 배치 크기는 작업당 50개의 자산입니다. 이 최적 배치 크기는 재처리가 실행되는 평균 자산 크기 및 MIME 유형의 자산에 의해 제어됩니다. 값이 높을수록 하나의 재처리 작업에 많은 파일이 있게 됩니다. 이에 따라, 처리 배너는 AEM 자산에 더 오랫동안 머무른다. 그러나 평균 파일 크기가 1MB 이하인 경우 값을 수백 개로 늘릴 것을 권장하지만 1000을 넘지 않습니다. 평균 파일 크기가 수백 MB인 경우 배치 크기를 최대 10개까지 줄이는 것이 좋습니다.

**재처리 워크플로우의 배치 크기를 선택적으로 조정하려면**

1. Experience Manager에서 **[!UICONTROL Adobe Experience Manager]**&#x200B;을 클릭하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]**(망치) 아이콘 > **[!UICONTROL 워크플로우 > 모델.]**
1. 워크플로우 모델 페이지의 카드 보기 또는 목록 보기에서 **[!UICONTROL Scene7을 선택합니다.자산]**&#x200B;을 재처리합니다.

   ![Scene7이 있는 워크플로우 모델 페이지:카드 보기에서 선택한 자산 워크플로우 재처리](/help/assets/assets-dm/reprocess-assets7.png)

1. 도구 모음에서 **[!UICONTROL 편집 을 클릭합니다.]** 새 브라우저 탭에서 Scene7을 엽니다.자산 워크플로우 모델 페이지를 재처리합니다.
1. Scene7에서:오른쪽 위 모서리 근처에 있는 자산 워크플로우 페이지를 다시 처리하려면 **[!UICONTROL 편집]** 을 클릭하여 워크플로우를 &quot;잠금 해제&quot;합니다.
1. 워크플로우에서 Scene7 일괄 업로드 구성 요소를 선택하여 도구 모음을 열고 도구 모음에서 **[!UICONTROL 구성]**&#x200B;을 클릭합니다.

   ![Scene7 배치 업로드 구성 요소](/help/assets/assets-dm/reprocess-assets8.png)

1. **[!UICONTROL Scene7에 일괄 업로드—단계 속성]** 대화 상자에서 다음을 설정합니다.
   * **[!UICONTROL 제목]** 및 **[!UICONTROL 설명]** 텍스트 필드에 원하는 경우 작업에 대한 새 제목과 설명을 입력합니다.
   * 핸들러가 다음 단계로 이동할 경우 **[!UICONTROL 핸들러 Advance]**&#x200B;를 선택합니다.
   * **[!UICONTROL 시간 초과]** 필드에 외부 프로세스 시간 초과(초)를 입력합니다.
   * **[!UICONTROL 기간]** 필드에 외부 프로세스 완료를 테스트할 폴링 간격(초)을 입력합니다.
   * **[!UICONTROL 일괄 처리 필드]**&#x200B;에 Dynamic Media 서버 일괄 처리 업로드 작업에서 처리할 최대 자산 수(50-1000)를 입력합니다.
   * 시간 초과에 도달했을 때 진행하려면 **[!UICONTROL 시간 초과 시작]**&#x200B;을 선택합니다. 시간이 초과되면 받은 편지함으로 진행하려면 선택 취소 를 클릭하십시오.

   ![속성 대화 상자](/help/assets/assets-dm/reprocess-assets3.png)

1. **[!UICONTROL Scene7에 일괄 업로드 - 단계 속성]** 대화 상자의 오른쪽 맨 위에 있는 **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

1. Scene7의 오른쪽 위 모서리:자산 워크플로우 모델 페이지를 다시 처리하고 **[!UICONTROL 동기화]**&#x200B;를 클릭합니다. **[!UICONTROL 동기화된]**&#x200B;가 표시되면 워크플로우 런타임 모델이 성공적으로 동기화되어 폴더의 자산을 재처리할 수 있습니다.

   ![워크플로우 모델 동기화](/help/assets/assets-dm/reprocess-assets1.png)

1. Scene7을 표시하는 브라우저 탭을 닫습니다.자산 워크플로우 모델을 재처리합니다.

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, click **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then click the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite.]**
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, click **[!UICONTROL Add.]** The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, click **[!UICONTROL Save All.]**
1. In the upper-left corner of the page, click **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
