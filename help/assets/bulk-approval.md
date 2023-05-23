---
title: 폴더 자산 및 컬렉션 검토
description: 폴더 또는 컬렉션 내의 자산에 대한 검토 워크플로우를 설정하고 검토자 또는 크리에이티브 파트너와 공유하여 피드백을 얻습니다.
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 5%

---

# 폴더 자산 및 컬렉션 검토 {#review-folder-assets-and-collections}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | 이 문서 |

폴더 또는 컬렉션 내의 자산에 대한 검토 워크플로우를 설정하고 검토자 또는 크리에이티브 파트너와 공유하여 피드백을 얻습니다.

[!DNL Adobe Experience Manager Assets] 폴더 또는 컬렉션 내의 자산에 대한 임시 검토 워크플로우를 설정하고 검토자 또는 크리에이티브 파트너와 공유하여 피드백을 구할 수 있습니다.

검토 워크플로를 프로젝트와 연결하거나 독립 검토 작업을 만들 수 있습니다.

에셋을 공유하면 검토자가 승인하거나 거부할 수 있습니다. 워크플로의 다양한 단계에서 알림을 전송하여 의도한 수신자에게 다양한 작업의 완료를 알립니다. 예를 들어 폴더 또는 컬렉션을 공유할 때 검토자는 검토를 위해 폴더/컬렉션이 공유되었다는 알림을 수신합니다.

검토자가 검토를 완료한 후(에셋을 승인하거나 거부함) 검토 완료 알림을 받습니다.

## 폴더에 대한 검토 작업 만들기 {#creating-a-review-task-for-folders}

1. 다음에서 [!DNL Assets] 사용자 인터페이스에서 검토 작업을 생성할 폴더를 선택합니다.
1. 도구 모음에서 를 클릭합니다 **[!UICONTROL 리뷰 작업 만들기]** ![리뷰 작업 만들기](assets/do-not-localize/create-review-task.png) 을(를) 열려면 **[!UICONTROL 작업 검토]** 페이지를 가리키도록 업데이트하는 중입니다. 도구 모음에 옵션이 표시되지 않으면 **[!UICONTROL 자세히]** 그런 다음 옵션을 선택합니다.

1. (선택 사항) **[!UICONTROL 프로젝트]** 목록에서 검토 작업과 연결할 프로젝트를 선택합니다. 기본적으로 **[!UICONTROL 없음]** 옵션이 선택되어 있습니다. 프로젝트를 검토 작업과 연결하지 않으려면 이 선택 사항을 유지하십시오.

   >[!NOTE]
   >
   >편집기 수준 권한(또는 이상)이 있는 프로젝트만 **[!UICONTROL 프로젝트]** 목록을 표시합니다.

1. 검토 작업의 이름을 입력하고 승인자에서 승인자를 선택합니다. **[!UICONTROL 할당 대상]** 목록을 표시합니다.

   >[!NOTE]
   >
   >선택한 프로젝트의 멤버/그룹은 다음에서 승인자로 사용할 수 있습니다. **[!UICONTROL 할당 대상]** 목록을 표시합니다.

1. 검토 작업에 대한 설명, 작업 우선 순위 및 기한을 입력합니다.

   ![task_details](assets/task_details.png)

1. 고급 탭에서 URI를 만드는 데 사용할 레이블을 입력합니다.

   ![review_name](assets/review_name.png)

1. 클릭 **[!UICONTROL 제출]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 완료]** 확인 메시지를 닫습니다. A notification for the new task is sent to the approver.
1. 에 로그인 [!DNL Assets] 승인자로서 다음 위치로 이동합니다. [!DNL Assets] UI. 자산을 승인하려면 **[!UICONTROL 알림]** 그런 다음 목록에서 검토 작업을 선택합니다.

   ![에셋 알림](assets/aemAssetsNotification.png)

1. 다음에서 **[!UICONTROL 작업 검토]** 페이지에서 검토 작업의 세부 사항을 검사한 다음 **[!UICONTROL 리뷰]**.
1. 다음에서 **[!UICONTROL 작업 검토]** 페이지를 열고 에셋을 선택한 다음 **[!UICONTROL 승인/거부]** 승인 또는 거부

   ![review_task](assets/review_task.png)

1. 클릭 **[!UICONTROL 완료]** 을 클릭합니다. 대화 상자에서 댓글을 입력하고 을(를) 클릭합니다.  **[!UICONTROL 완료]** 확인할 수 있습니다.
1. 다음 위치로 이동 [!DNL Assets] 사용자 인터페이스를 사용하고 폴더를 엽니다. 에셋에 대한 승인 상태 아이콘이 카드 보기 및 목록 보기에 나타납니다.

   **카드 보기**

   ![카드 보기에 표시된 상태 검토](assets/chlimage_1-404.png)

   **목록 보기**

   ![목록 보기에 표시된 상태 검토](assets/review_status_listview.png)

## 컬렉션에 대한 검토 작업 만들기 {#creating-a-review-task-for-collections}

1. 컬렉션 페이지에서 검토 작업을 생성할 컬렉션을 선택합니다.
1. 도구 모음에서 를 클릭합니다 **[!UICONTROL 리뷰 작업 만들기]** ![리뷰 작업 만들기](assets/do-not-localize/create-review-task.png) 을(를) 열려면 **[!UICONTROL 작업 검토]** 페이지를 가리키도록 업데이트하는 중입니다. 도구 모음에 옵션이 표시되지 않으면 **[!UICONTROL 자세히]** 그런 다음 옵션을 선택합니다.

1. (선택 사항) **[!UICONTROL 프로젝트]** 목록에서 검토 작업과 연결할 프로젝트를 선택합니다. 기본적으로 **[!UICONTROL 없음]** 옵션이 선택되어 있습니다. 프로젝트를 검토 작업과 연결하지 않으려면 이 선택 사항을 유지하십시오.

   >[!NOTE]
   >
   >편집기 수준 권한(또는 이상)이 있는 프로젝트만 **[!UICONTROL 프로젝트]** 목록을 표시합니다.

1. 검토 작업의 이름을 입력하고 승인자에서 승인자를 선택합니다. **[!UICONTROL 할당 대상]** 목록을 표시합니다.

   >[!NOTE]
   >
   >선택한 프로젝트의 멤버/그룹은 다음에서 승인자로 사용할 수 있습니다. **[!UICONTROL 할당 대상]** 목록을 표시합니다.

1. 검토 작업에 대한 설명, 작업 우선 순위 및 기한을 입력합니다.

   ![task_details-collection](assets/task_details-collection.png)

1. 클릭 **[!UICONTROL 제출]**&#x200B;을 클릭한 다음 을 클릭합니다 **[!UICONTROL 완료]** 확인 메시지를 닫습니다. A notification for the new task is sent to the approver.
1. 에 로그인 [!DNL Assets] 승인자로서 다음 위치로 이동합니다. [!DNL Assets] 콘솔. 자산을 승인하려면 **[!UICONTROL 알림]** 그런 다음 목록에서 검토 작업을 선택합니다.
1. 다음에서 **[!UICONTROL 작업 검토]** 페이지에서 검토 작업의 세부 사항을 검사한 다음 **[!UICONTROL 리뷰]**.
1. 컬렉션의 모든 자산이 검토 페이지에 표시됩니다. 에셋을 선택하고 **[!UICONTROL 승인/거부]** 에셋을 승인하거나 거부합니다.

   ![review_task_collection](assets/review_task_collection.png)

1. 클릭 **[!UICONTROL 완료]** 을 클릭합니다. 대화 상자에서 댓글을 입력하고 을(를) 클릭합니다. **[!UICONTROL 완료]** 확인할 수 있습니다.
1. 컬렉션 콘솔로 이동하고 컬렉션을 엽니다. 에셋에 대한 승인 상태 아이콘이 카드 보기와 목록 보기에 모두 나타납니다.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *그림: 카드 보기*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *그림: 목록 보기*
