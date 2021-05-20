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
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# {#specifying-fonts-to-embed} 포함 글꼴 지정

Forms 서비스에서 생성하는 양식과 함께 항상 포함되거나 포함되지 않는 글꼴을 지정할 수 있습니다. 글꼴을 포함하면 양식의 파일 크기가 늘어납니다. 사용자가 시스템에 거의 사용하지 않는 비정상적인 글꼴을 포함합니다. 일반적으로 설치한 일반 글꼴은 포함하지 마십시오.

>[!NOTE]
>
>Forms에 대해 사용자 지정 XCI 파일을 지정한 경우 XCI 파일의 포함 글꼴 옵션이 이러한 설정을 무시합니다. ([Forms에 대한 위치 구성](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)을 참조하십시오.)

1. 관리 콘솔에서 **[!UICONTROL 서비스 > Forms]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 글꼴 포함 설정]** 아래의 **[!UICONTROL 항상 글꼴 포함]** 상자에서 양식에 포함할 글꼴의 이름을 쉼표로 구분하여 입력합니다. 지정하는 글꼴은 양식에서 사용하는 경우에만 생성된 양식에 포함됩니다. 서비스에 전달된 XCI 파일에서 포함 글꼴 옵션을 설정한 경우 PDF에 사용된 모든 글꼴이 항상 포함되므로 이 설정은 무시됩니다.
1. **[!UICONTROL 글꼴 포함 안 함]** 상자에 양식에 포함할 글꼴의 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 생성된 PDF에서 사용되더라도 PDF에 포함되지 않습니다. 서비스에 전달된 XCI 파일에서 포함 글꼴 옵션이 꺼져 있는 경우 PDF에 사용된 글꼴이 포함되지 않으므로 이 설정은 무시됩니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
