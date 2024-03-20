---
title: 포함할 글꼴 지정
description: 적응형 양식에 포함할 글꼴을 지정하는 방법을 알아봅니다. Forms 서비스에서 생성하는 양식에 포함할 글꼴과 포함하지 않을 글꼴을 지정할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 포함할 글꼴 지정 {#specifying-fonts-to-embed}

Forms 서비스에서 생성하는 양식에 항상 포함할 글꼴과 포함하지 않을 글꼴을 지정할 수 있습니다. 글꼴을 포함하면 양식의 파일 크기가 증가합니다. 사용자가 시스템에 거의 가지고 있지 않은 특이한 글꼴을 임베드합니다. 일반적으로 설치된 일반 글꼴은 포함하지 마십시오.

>[!NOTE]
>
>Forms에 대한 사용자 지정 XCI 파일을 지정한 경우 XCI 파일의 포함 글꼴 옵션이 이러한 설정을 무시합니다. (참조: [Forms에 대한 위치 구성](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. 관리 콘솔에서 다음을 클릭합니다. **[!UICONTROL 서비스 > Forms]**.
1. 아래 **[!UICONTROL 글꼴 포함 설정]**, **[!UICONTROL 항상 글꼴 포함]** 상자에 양식에 포함할 글꼴 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 폼에서 사용되는 경우에만 생성된 폼에 포함됩니다. 서비스로 전달된 XCI 파일에서 글꼴 포함 옵션이 켜진 경우 PDF에 사용된 모든 글꼴이 항상 포함되므로 이 설정은 무시됩니다.
1. 다음에서 **[!UICONTROL 글꼴 임베드 안 함]** 상자에 양식에 포함되지 않을 글꼴 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 생성된 PDF에서 사용되더라도 PDF에 포함되지 않습니다. 서비스로 전달된 XCI 파일에서 글꼴 포함 옵션이 꺼진 경우 PDF에 사용된 글꼴이 하나도 포함되어 있지 않으므로 이 설정은 무시됩니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
