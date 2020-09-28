---
title: 자산을 공유할 비공개 폴더
description: 비공개 폴더를 만들고 다른 사용자와 [!DNL Adobe Experience Manager Assets] 공유하고 다양한 권한을 할당하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---


# 비공개 폴더( [!DNL Adobe Experience Manager Assets] {#private-folder}

개인 폴더는 [!DNL Adobe Experience Manager Assets] 사용자 인터페이스에서만 사용할 수 있습니다. 이 비공개 폴더를 다른 사용자에게 공유하고 다양한 권한을 할당할 수 있습니다. 사용자가 지정하는 권한 수준에 따라, 사용자는 폴더에서 다양한 작업을 수행할 수 있습니다. 예를 들어 폴더 내의 자산을 보거나 자산을 편집할 수 있습니다.

>[!NOTE]
>
>비공개 폴더에는 소유자 역할을 가진 구성원이 하나 이상 있습니다.

## 비공개 폴더 생성 및 공유 {#create-share-private-folder}

비공개 폴더를 만들고 공유하려면:

1. 콘솔의 도구 모음 [!DNL Assets] 에서 **[!UICONTROL 만들기를]** 클릭한 다음 메뉴에서 **[!UICONTROL 폴더]** 를 선택합니다.

   ![에셋 폴더 만들기](assets/Create-folder.png)

1. [폴더 **[!UICONTROL 만들기]** ] 대화 상자에서 폴더의 제목과 이름(선택 사항)을 입력하고 [ **[!UICONTROL 비공개]** ] 옵션을 선택합니다.

1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 비공개 폴더가 생성됩니다.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. 다른 사용자와 폴더를 공유하고 사용자에게 할당 권한을 공유하려면 폴더를 선택하고 도구 모음에서 **[!UICONTROL 속성]** 을 클릭합니다.

   ![정보 옵션](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >폴더를 공유하기 전에는 다른 사용자가 해당 폴더를 볼 수 없습니다.

1. [ **[!UICONTROL 폴더 속성]** ] 페이지의 [사용자 **[!UICONTROL 추가]** ] 목록에서 사용자를 선택하고 비공개 폴더의 사용자에게 역할을 할당한 다음 **[!UICONTROL 추가를 클릭합니다]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >폴더를 공유하는 사용자에게 편집기, 소유자 또는 뷰어와 같은 다양한 역할을 할당할 수 있습니다. 사용자에게 소유자 역할을 할당하는 경우 해당 사용자는 폴더에 대한 편집기 권한을 갖습니다. 또한 사용자는 다른 사람과 폴더를 공유할 수 있습니다. 편집기 역할을 할당하는 경우 사용자는 비공개 폴더의 자산을 편집할 수 있습니다. 뷰어 역할을 할당하면 사용자는 비공개 폴더의 에셋만 볼 수 있습니다.

   >[!NOTE]
   >
   >비공개 폴더에는 소유자 역할을 가진 구성원이 하나 이상 있습니다. 따라서 관리자는 비공개 폴더에서 모든 소유자 구성원을 제거할 수 없습니다. 그러나 개인 폴더에서 기존 소유자(및 관리자 자체)를 제거하려면 관리자가 다른 사용자를 소유자로 추가해야 합니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다. 지정한 역할에 따라 사용자가 로그인할 때 개인 폴더에 대한 권한 세트가 할당됩니다 [!DNL Assets].
1. 확인을 **[!UICONTROL 클릭하여]** 확인 메시지를 닫습니다.
1. 폴더를 공유하는 사용자는 공유 알림을 받습니다. 알림을 보려면 사용자 [!DNL Assets] 의 자격 증명으로 로그인합니다.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 알림을 클릭하여 알림 목록을 엽니다.

   ![알림 목록](assets/Assets-Notification.png)

1. 관리자가 공유하는 비공개 폴더의 항목을 클릭하여 폴더를 엽니다.

>[!NOTE]
>
>비공개 폴더를 만들려면 비공개 폴더를 만들 상위 폴더에 대한 읽기 및 수정 [액세스 권한](/help/sites-administering/security.md#permissions-in-aem) 권한이 필요합니다. 관리자가 아닌 경우 기본적으로 이러한 권한이 활성화되어 있지 않습니다 `/content/dam`. 이 경우 비공개 폴더를 만들기 전에 먼저 사용자 ID/그룹에 대해 이러한 권한을 얻습니다.

## 비공개 폴더 삭제 {#delete-private-folder}

폴더를 선택하고 상단 메뉴에서 [!UICONTROL 삭제] 옵션을 선택하거나 키보드에서 백스페이스 키를 사용하여 폴더를 삭제할 수 있습니다.

![상단 메뉴에서 옵션 삭제](assets/delete-option.png)

>[!CAUTION]
>
>CRXDE Lite에서 비공개 폴더를 삭제하면 중복된 사용자 그룹이 저장소에 남아 있게 됩니다.

>[!NOTE]
>
>사용자 인터페이스에서 위의 방법을 사용하여 폴더를 삭제하면 연결된 사용자 그룹도 삭제됩니다.
그러나 기존 중복, 사용하지 않음 및 자동 생성된 사용자 그룹은 [JMX를 사용하여 저장소에서 정리될 수 있습니다](#group-clean-up-jmx).

### JMX를 사용하여 사용되지 않은 사용자 그룹 정리 {#group-clean-up-jmx}

사용하지 않은 사용자 그룹의 저장소를 정리하려면

1. JMX를 열어 작성자 인스턴스의 자산에 대한 중복 그룹을 [!DNL Experience Manager] 정리합니다 `http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`.
예, `http://no1010042068039.corp.adobe.com:4502/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`.

1. 이 JMX에서 `clean` 메서드를 호출합니다.

이전에 삭제한 그룹과 동일한 이름으로 폴더를 만들 때 생성되는 모든 중복 사용자 그룹 또는 자동 생성 그룹이 경로에서 제거됨을 확인할 수 있습니다 `/home/groups/mac/default/<user_name>/<folder_name>`.
