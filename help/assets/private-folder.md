---
title: 자산을 공유할 개인 폴더
description: ' [!DNL Adobe Experience Manager Assets] 에서 개인 폴더를 만들어 다른 사용자와 공유하고 사용자에게 다양한 권한을 할당하는 방법에 대해 알아보십시오.'
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager Assets]의 개인 폴더 {#private-folder}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | 이 문서 |

[!DNL Adobe Experience Manager Assets] 사용자 인터페이스에서 자신만 사용할 수 있는 개인 폴더를 만들 수 있습니다. 이 개인 폴더를 다른 사용자에게 공유하고 다양한 권한을 할당할 수 있습니다. 사용자가 지정한 권한 수준에 따라 폴더에서 다양한 작업(예: 폴더 내 에셋 보기 또는 에셋 편집)을 수행할 수 있습니다.

>[!NOTE]
>
>개인 폴더에 소유자 역할을 가진 구성원이 하나 이상 있습니다.

## 개인 폴더 만들기 및 공유 {#create-share-private-folder}

개인 폴더를 만들고 공유하려면:

1. [!DNL Assets] 콘솔의 도구 모음에서 **[!UICONTROL 만들기]**&#x200B;를 클릭한 다음 메뉴에서 **[!UICONTROL 폴더]**&#x200B;를 선택합니다.

   ![에셋 폴더 만들기](assets/Create-folder.png)

1. **[!UICONTROL 폴더 만들기]** 대화 상자에서 폴더의 제목과 이름(선택 사항)을 입력하고 **[!UICONTROL 개인]** 옵션을 선택합니다.

1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 비공개 폴더가 생성됩니다.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. 다른 사용자와 폴더를 공유하고 사용자에게 권한을 할당하려면 폴더를 선택한 다음 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭하십시오.

   ![정보 옵션](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >폴더는 공유할 때까지 다른 사용자가 볼 수 없습니다.

1. **[!UICONTROL 폴더 속성]** 페이지의 **[!UICONTROL 사용자 추가]** 목록에서 사용자를 선택하고 개인 폴더에서 사용자에게 역할을 할당한 다음 **[!UICONTROL 추가]**&#x200B;를 클릭합니다.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >폴더를 공유하는 사용자에게 `Editor`, `Owner` 또는 `Viewer` 등 다양한 역할을 할당할 수 있습니다. 사용자에게 `Owner` 역할을 할당하면 사용자는 폴더에 대한 `Editor` 권한을 갖게 됩니다. 또한 사용자는 폴더를 다른 사용자와 공유할 수 있습니다. `Editor` 역할을 할당하면 사용자는 개인 폴더의 자산을 편집할 수 있습니다. 뷰어 역할을 할당하면 사용자는 개인 폴더에 있는 에셋만 볼 수 있습니다.

   >[!NOTE]
   >
   >개인 폴더에 `Owner` 역할을 가진 구성원이 하나 이상 있습니다. 따라서 관리자가 개인 폴더에서 일부 소유자 구성원을 제거할 수 없습니다. 그러나 개인 폴더에서 기존 소유자(및 관리자 자체)를 제거하려면 관리자가 다른 사용자를 소유자로 추가해야 합니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 할당된 역할에 따라 사용자가 [!DNL Assets]에 로그인할 때 개인 폴더에 대한 권한 집합이 할당됩니다.
1. 확인 메시지를 닫으려면 **[!UICONTROL 확인]**&#x200B;을 클릭하세요.
1. 폴더를 공유하는 사용자는 공유 알림을 받습니다. 알림을 보려면 사용자의 자격 증명으로 [!DNL Assets]에 로그인하십시오.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 알림 목록을 열려면 [!UICONTROL 알림]을 클릭하세요.

   ![알림 목록](assets/Assets-Notification.png)

1. 관리자가 공유한 개인 폴더에 대한 항목을 클릭하여 폴더를 엽니다.

>[!NOTE]
>
>개인 폴더를 만들려면 개인 폴더를 만들려는 부모 폴더에 대한 읽기 및 수정 [액세스 제어 권한](/help/sites-administering/security.md#permissions-in-aem)이 필요합니다. 관리자가 아닌 경우 `/content/dam`에서 이러한 사용 권한을 기본적으로 사용할 수 없습니다. 이 경우 개인 폴더를 만들기 전에 먼저 사용자 ID/그룹에 대한 이러한 권한을 얻습니다.

## 개인 폴더 삭제 {#delete-private-folder}

폴더를 선택하고 상단 메뉴에서 [!UICONTROL 삭제] 옵션을 선택하거나 키보드의 백스페이스 키를 사용하여 폴더를 삭제할 수 있습니다.

상단 메뉴의 ![삭제 옵션](assets/delete-option.png)

>[!CAUTION]
>
>CRXDE Lite에서 개인 폴더를 삭제하면 저장소에 중복된 사용자 그룹이 남게 됩니다.

>[!NOTE]
>
>사용자 인터페이스에서 위의 방법을 사용하여 폴더를 삭제하면 연결된 사용자 그룹도 삭제됩니다.
>
>그러나 작성자 인스턴스(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)의 JMX에서 `clean` 메서드를 사용하여 기존의 중복, 미사용 및 자동 생성된 사용자 그룹을 리포지토리에서 제거할 수 있습니다.
