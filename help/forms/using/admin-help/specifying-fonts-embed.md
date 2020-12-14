---
title: 포함할 글꼴 지정
seo-title: 포함할 글꼴 지정
description: 포함할 글꼴을 지정하는 방법을 알아봅니다.
seo-description: 포함할 글꼴을 지정하는 방법을 알아봅니다.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# {#specifying-fonts-to-embed}에 포함할 글꼴 지정

Forms 서비스가 생성하는 양식에 항상 포함되거나 포함되지 않은 글꼴을 지정할 수 있습니다. 글꼴을 포함하면 양식의 파일 크기가 늘어납니다. 사용자의 시스템에 거의 없는 독특한 글꼴을 임베드할 수 있습니다. 일반적으로 설치한 일반 글꼴은 포함하지 마십시오.

>[!NOTE]
>
>Forms에 대한 사용자 정의 XCI 파일을 지정한 경우 XCI 파일의 포함 글꼴 옵션이 이러한 설정을 무시합니다. (Forms[에 대한 위치 구성을 참조하십시오.)](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)

1. 관리 콘솔에서 **[!UICONTROL 서비스 > Forms]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 글꼴 포함 설정]** 아래의 **[!UICONTROL 항상 글꼴 포함]** 상자에 양식에 포함할 글꼴 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 양식에서 사용되는 경우에만 생성된 양식에 포함됩니다. 서비스에 전달된 XCI 파일에서 글꼴 포함 옵션을 설정한 경우 PDF에 사용된 모든 글꼴이 항상 포함되므로 이 설정은 무시됩니다.
1. **[!UICONTROL 글꼴 포함 안 함]** 상자에 양식에 포함되지 않을 글꼴의 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 생성된 PDF에서 사용되더라도 PDF에 포함되지 않습니다. 서비스에 전달된 XCI 파일에서 포함 글꼴 옵션이 꺼져 있는 경우 PDF에 사용된 글꼴이 포함되지 않으므로 이 설정은 무시됩니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

