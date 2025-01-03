---
title: 포함할 글꼴 지정
description: 적응형 양식에 포함할 글꼴을 지정하는 방법을 알아봅니다. Forms 서비스에서 생성하는 양식에 포함할 글꼴과 포함하지 않을 글꼴을 지정할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 포함할 글꼴 지정{#specify-fonts-to-embed}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

출력에서 사용하는 양식에 항상 포함될 글꼴과 포함되지 않을 글꼴을 지정할 수 있습니다. 글꼴을 포함하면 양식의 파일 크기가 증가합니다. 사용자가 시스템에 가지고 있을 수 없는 특이한 글꼴을 포함하고 설치할 일반 글꼴은 포함하지 마십시오.

>[!NOTE]
>
>출력에 대해 사용자 지정 XCI 파일을 지정한 경우 XCI 파일의 포함 글꼴 옵션이 이러한 설정을 무시합니다. [출력의 파일 위치 지정](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)을 참조하십시오.

1. 관리 콘솔에서 서비스 > 출력을 클릭합니다.
1. 글꼴 포함 설정 아래의 항상 글꼴 포함 상자에서 양식에 포함할 글꼴 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 폼에서 사용되는 경우에만 생성된 폼에 포함됩니다. 서비스로 전달된 XCI 파일에서 글꼴 포함 옵션이 켜진 경우 이 설정은 무시됩니다. 이 경우 PDF에 사용된 모든 글꼴이 항상 포함됩니다.
1. 글꼴을 포함하지 않음 상자에 양식에 포함되지 않을 글꼴의 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 생성된 PDF에서 사용되더라도 PDF에 포함되지 않습니다. 서비스로 전달된 XCI 파일에서 글꼴 포함 옵션이 꺼진 경우 이 설정은 무시됩니다. 이 경우 PDF에 사용된 글꼴이 포함되지 않습니다.
1. 저장을 클릭합니다.
