---
title: 임베드할 글꼴 지정
description: 적응형 양식에 임베드할 글꼴을 지정하는 방법을 알아봅니다. Forms 서비스에서 생성하는 양식에 임베드하거나 임베드하지 않을 글꼴을 지정할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '282'
ht-degree: 100%

---

# 임베드할 글꼴 지정 {#specifying-fonts-to-embed}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

Forms 서비스에서 생성하는 양식에 항상 임베드하거나 임베드하지 않을 글꼴을 지정할 수 있습니다. 글꼴을 임베드하면 양식의 파일 크기가 커집니다. 사용자의 시스템에 거의 없는 특이한 글꼴을 임베드하는 것이 좋습니다. 대부분의 시스템에 설치되어 있는 일반적인 글꼴은 임베드하지 마십시오.

>[!NOTE]
>
>Forms에 사용자 정의 XCI 파일을 지정한 경우 XCI 파일의 글꼴 임베드 옵션이 해당 설정을 재정의합니다. ([Forms 위치 구성](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)을 참조하십시오.)

1. 관리 콘솔에서 **[!UICONTROL 서비스 > Forms]**&#x200B;를 클릭합니다.
1. **[!UICONTROL 글꼴 임베드 설정]**&#x200B;의 **[!UICONTROL 항상 글꼴 임베드]** 상자에 양식에 임베드할 글꼴 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 양식에서 사용되는 경우에만 생성된 양식에 임베드됩니다. 서비스에 전달된 XCI 파일에서 글꼴 임베드 옵션이 켜져 있는 경우 이 설정은 무시됩니다. 이 경우 PDF에 사용된 모든 글꼴이 항상 임베드되기 때문입니다.
1. **[!UICONTROL 글꼴 임베드 안 함]** 상자에 양식에 임베드하지 않을 글꼴 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴이 생성된 PDF에서 사용되는 경우에도 해당 글꼴은 PDF에 임베드되지 않습니다. 서비스에 전달된 XCI 파일에서 글꼴 임베드 옵션이 꺼져 있는 경우 이 설정은 무시됩니다. 이 경우 PDF에 사용된 글꼴 중 어느 것도 임베드되지 않기 때문입니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
