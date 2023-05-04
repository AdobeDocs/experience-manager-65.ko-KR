---
title: 폴더 에셋 및 컬렉션 검토
description: 폴더 또는 컬렉션 내의 자산에 대한 검토 워크플로우를 설정하고 검토자 또는 크리에이티브 파트너와 공유하여 피드백을 받습니다.
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 5%

---

# 폴더 에셋 및 컬렉션 검토 {#review-folder-assets-and-collections}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | 이 문서 |

폴더 또는 컬렉션 내의 자산에 대한 검토 워크플로우를 설정하고 검토자 또는 크리에이티브 파트너와 공유하여 피드백을 받습니다.

[!DNL Adobe Experience Manager Assets] 폴더 또는 컬렉션 내의 자산에 대해 임시 검토 워크플로우를 설정하고 검토자 또는 크리에이티브 파트너와 공유하여 피드백을 받을 수 있습니다.

검토 워크플로우를 프로젝트에 연결하거나 독립적인 검토 작업을 만들 수 있습니다.

자산을 공유하면 검토자가 이를 승인하거나 거부할 수 있습니다. 알림은 워크플로우의 다양한 단계에서 수신자에게 다양한 작업 완료에 대한 알림을 보냅니다. 예를 들어, 폴더나 컬렉션을 공유할 때 검토자는 검토용으로 폴더/컬렉션이 공유되었다는 알림을 받습니다.

검토자가 검토를 완료한 후(자산을 승인하거나 거부함) 검토 완료 알림을 받게 됩니다.

## 폴더에 대한 검토 작업 만들기 {#creating-a-review-task-for-folders}

1. 에서 [!DNL Assets] 사용자 인터페이스에서 검토 작업을 만들 폴더를 선택합니다.
1. 도구 모음에서 **[!UICONTROL 검토 작업 만들기]** ![검토 작업 만들기](assets/do-not-localize/create-review-task.png) 열다 **[!UICONTROL 작업 검토]** 페이지. 도구 모음에 옵션이 표시되지 않으면 **[!UICONTROL 자세히]** 그런 다음 옵션을 선택합니다.

1. (선택 사항) **[!UICONTROL 프로젝트]** 목록에서 검토 작업을 연결할 프로젝트를 선택합니다. 기본적으로 **[!UICONTROL 없음]** 옵션이 선택되어 있습니다. 프로젝트를 검토 작업에 연결하지 않으려면 이 선택 항목을 유지합니다.

   >[!NOTE]
   >
   >편집자 수준 권한(또는 이상)이 있는 프로젝트만 **[!UICONTROL 프로젝트]** 목록.

1. 검토 작업의 이름을 입력하고, **[!UICONTROL 할당 대상]** 목록.

   >[!NOTE]
   >
   >선택한 프로젝트의 멤버/그룹은 **[!UICONTROL 할당 대상]** 목록.

1. 검토 작업의 설명, 작업 우선순위 및 기한을 입력합니다.

   ![task_details](assets/task_details.png)

1. 고급 탭에서 URI를 만드는 데 사용할 레이블을 입력합니다.

   ![review_name](assets/review_name.png)

1. 클릭 **[!UICONTROL 제출]**&#x200B;를 클릭한 다음 **[!UICONTROL 완료]** 확인 메시지를 닫습니다. A notification for the new task is sent to the approver.
1. 에 로그인합니다. [!DNL Assets] 승인자로 이동하여 [!DNL Assets] UI. 자산을 승인하려면 **[!UICONTROL 알림 을 참조하십시오]** 그런 다음 목록에서 검토 작업을 선택합니다.

   ![자산 알림](assets/aemAssetsNotification.png)

1. 에서 **[!UICONTROL 작업 검토]** 페이지에서 검토 작업의 세부 사항을 검토한 다음 **[!UICONTROL 검토]**.
1. 에서 **[!UICONTROL 작업 검토]** 페이지에서 자산을 선택하고 를 클릭합니다 **[!UICONTROL 승인/거부]** 승인하거나 거부하도록 하는 것입니다.

   ![review_task](assets/review_task.png)

1. 클릭 **[!UICONTROL 완료]** 를 클릭합니다. 대화 상자에서 설명을 입력하고 을(를) 클릭합니다.  **[!UICONTROL 완료]** 확인합니다.
1. 로 이동합니다 [!DNL Assets] 사용자 인터페이스를 사용하여 폴더를 엽니다. 자산에 대한 승인 상태 아이콘이 카드 보기 및 목록 보기에 표시됩니다.

   **카드 보기**

   ![카드 보기에 표시된 상태 검토](assets/chlimage_1-404.png)

   **목록 보기**

   ![목록 보기에 표시된 상태 검토](assets/review_status_listview.png)

## 컬렉션에 대한 검토 작업 만들기 {#creating-a-review-task-for-collections}

1. 컬렉션 페이지에서 검토 작업을 생성할 컬렉션을 선택합니다.
1. 도구 모음에서 **[!UICONTROL 검토 작업 만들기]** ![검토 작업 만들기](assets/do-not-localize/create-review-task.png) 열다 **[!UICONTROL 작업 검토]** 페이지. 도구 모음에 옵션이 표시되지 않으면 **[!UICONTROL 자세히]** 그런 다음 옵션을 선택합니다.

1. (선택 사항) **[!UICONTROL 프로젝트]** 목록에서 검토 작업을 연결할 프로젝트를 선택합니다. 기본적으로 **[!UICONTROL 없음]** 옵션이 선택되어 있습니다. 프로젝트를 검토 작업에 연결하지 않으려면 이 선택 항목을 유지합니다.

   >[!NOTE]
   >
   >편집자 수준 권한(또는 이상)이 있는 프로젝트만 **[!UICONTROL 프로젝트]** 목록.

1. 검토 작업의 이름을 입력하고, **[!UICONTROL 할당 대상]** 목록.

   >[!NOTE]
   >
   >선택한 프로젝트의 멤버/그룹은 **[!UICONTROL 할당 대상]** 목록.

1. 검토 작업의 설명, 작업 우선순위 및 기한을 입력합니다.

   ![task_details-collection](assets/task_details-collection.png)

1. 클릭 **[!UICONTROL 제출]**&#x200B;를 클릭한 다음 **[!UICONTROL 완료]** 확인 메시지를 닫습니다. A notification for the new task is sent to the approver.
1. 에 로그인합니다. [!DNL Assets] 승인자로 이동하여 [!DNL Assets] 콘솔. 자산을 승인하려면 **[!UICONTROL 알림 을 참조하십시오]** 그런 다음 목록에서 검토 작업을 선택합니다.
1. 에서 **[!UICONTROL 작업 검토]** 페이지에서 검토 작업의 세부 사항을 검토한 다음 **[!UICONTROL 검토]**.
1. 컬렉션의 모든 자산이 검토 페이지에 표시됩니다. 자산을 선택하고 을(를) 클릭합니다 **[!UICONTROL 승인/거부]** 자산을 승인하거나 거부하려면 적절하게 사용하십시오.

   ![review_task_collection](assets/review_task_collection.png)

1. 클릭 **[!UICONTROL 완료]** 를 클릭합니다. 대화 상자에서 설명을 입력하고 을(를) 클릭합니다. **[!UICONTROL 완료]** 확인합니다.
1. 컬렉션 콘솔로 이동하고 컬렉션을 엽니다. 자산에 대한 승인 상태 아이콘은 카드 및 목록 보기 모두에 표시됩니다.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *그림: 카드 보기.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *그림: 목록 보기.*
