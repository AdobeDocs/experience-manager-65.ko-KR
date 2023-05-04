---
title: 자산을 공유할 비공개 폴더
description: 에서 개인 폴더를 만드는 방법을 알아봅니다. [!DNL Adobe Experience Manager Assets] 다른 사용자와 공유하고 다양한 권한을 사용자에게 할당합니다.
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 2%

---

# 의 비공개 폴더 [!DNL Adobe Experience Manager Assets] {#private-folder}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | 이 문서 |

에서 개인 폴더를 만들 수 있습니다 [!DNL Adobe Experience Manager Assets] 배타적으로 사용 가능한 사용자 인터페이스. 이 비공개 폴더를 다른 사용자에게 공유하고 다양한 권한을 할당할 수 있습니다. 사용자가 지정하는 권한 수준에 따라 폴더에서 다양한 작업을 수행할 수 있습니다. 예를 들어 폴더 내의 자산을 보거나 자산을 편집할 수 있습니다.

>[!NOTE]
>
>개인 폴더에는 소유자 역할을 가진 구성원이 하나 이상 있습니다.

## 비공개 폴더 만들기 및 공유 {#create-share-private-folder}

비공개 폴더를 만들고 공유하려면 다음을 수행하십시오.

1. 에서 [!DNL Assets] 콘솔 **[!UICONTROL 만들기]** 도구 모음에서 를 선택한 다음 **[!UICONTROL 폴더]** 메뉴 아래의 제품에서 사용할 수 있습니다.

   ![자산 폴더 만들기](assets/Create-folder.png)

1. 에서 **[!UICONTROL 폴더 만들기]** 대화 상자에서 폴더의 제목과 이름(선택 사항)을 입력하고 **[!UICONTROL 비공개]** 선택 사항입니다.

1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 비공개 폴더가 만들어집니다.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. 다른 사용자와 폴더를 공유하고 해당 사용자에게 권한을 할당하려면 폴더를 선택하고 **[!UICONTROL 속성]** 를 클릭합니다.

   ![정보 옵션](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >폴더는 공유하기 전까지 다른 사용자에게 표시되지 않습니다.

1. 에서 **[!UICONTROL 폴더 속성]** 페이지의 **[!UICONTROL 사용자 추가]** 목록에 추가하고, 개인 폴더의 사용자에게 역할을 지정한 다음 **[!UICONTROL 추가]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >다음과 같은 다양한 역할을 할당할 수 있습니다 `Editor`, `Owner`, 또는 `Viewer` 폴더를 공유한 사용자에게 표시합니다. 을(를) 지정하는 경우 `Owner` 사용자에게 역할, 사용자에게 역할 `Editor` 폴더에 대한 권한. 또한 사용자는 다른 사용자와 폴더를 공유할 수 있습니다. 을(를) 지정하는 경우 `Editor` 역할, 사용자는 비공개 폴더의 자산을 편집할 수 있습니다. 뷰어 역할을 할당하는 경우 사용자는 비공개 폴더의 자산만 볼 수 있습니다.

   >[!NOTE]
   >
   >개인 폴더에는 `Owner` 역할. 따라서 관리자는 개인 폴더에서 모든 소유자 구성원을 제거할 수 없습니다. 그러나 개인 폴더에서 기존 소유자(및 관리자 자체)를 제거하려면 관리자가 다른 사용자를 소유자로 추가해야 합니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 지정한 역할에 따라 사용자가 로그인하는 경우 사용자에게 개인 폴더에 대한 권한 세트가 할당됩니다 [!DNL Assets].
1. 클릭 **[!UICONTROL 확인]** 확인 메시지를 닫습니다.
1. 폴더를 공유하는 사용자는 공유 알림을 받습니다. 에 로그인합니다. [!DNL Assets] 알림을 볼 사용자의 자격 증명으로 사용.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 클릭 [!UICONTROL 알림 을 참조하십시오] 알림 목록을 엽니다.

   ![알림 목록](assets/Assets-Notification.png)

1. 관리자가 공유하는 비공개 폴더의 항목을 클릭하여 폴더를 엽니다.

>[!NOTE]
>
>비공개 폴더를 만들려면 읽기 및 수정이 필요합니다 [액세스 제어 권한](/help/sites-administering/security.md#permissions-in-aem) 상위 폴더에서 을 클릭합니다. 관리자가 아닌 경우 기본적으로 이 권한은 활성화되지 않습니다 `/content/dam`. 이 경우, 비공개 폴더를 만들기 전에 먼저 사용자 ID/그룹에 대한 이러한 권한을 얻습니다.

## 비공개 폴더 삭제 {#delete-private-folder}

폴더를 선택하고 을 선택하여 폴더를 삭제할 수 있습니다 [!UICONTROL 삭제] 옵션을 선택합니다.

![위쪽 메뉴에서 옵션 삭제](assets/delete-option.png)

>[!CAUTION]
>
>CRXDE Lite에서 개인 폴더를 삭제하면 중복 사용자 그룹이 리포지토리에 남게 됩니다.

>[!NOTE]
>
>사용자 인터페이스에서 위의 방법을 사용하여 폴더를 삭제하면 연결된 사용자 그룹도 삭제됩니다.
>
>그러나 기존 중복, 미사용 및 자동 생성된 사용자 그룹은 `clean` 작성자 인스턴스의 JMX에 있는 메서드(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
