---
title: 포함할 글꼴 지정
seo-title: 포함할 글꼴 지정
description: 포함할 글꼴을 지정하는 방법을 알아봅니다.
seo-description: 포함할 글꼴을 지정하는 방법을 알아봅니다.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# 포함할 글꼴 지정{#specify-fonts-to-embed}

출력에 사용되는 양식과 함께 항상 포함되거나 포함되지 않는 글꼴을 지정할 수 있습니다. 글꼴을 포함하면 양식의 파일 크기가 늘어납니다. 사용자가 시스템에 가지고 있지 않을 수 있는 비정상적인 글꼴을 포함하고 사용자가 설치할 일반 글꼴을 포함하지 않습니다.

>[!NOTE]
>
>출력에 대한 사용자 지정 XCI 파일을 지정한 경우 XCI 파일의 포함 글꼴 옵션이 이러한 설정을 무시합니다. ([출력](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)에 대한 파일 위치 지정 을 참조하십시오.)

1. 관리 콘솔에서 서비스 > 출력을 클릭합니다.
1. 글꼴 포함 설정 아래의 [항상 포함 글꼴] 상자에서 양식에 포함할 글꼴의 이름을 쉼표로 구분하여 입력합니다. 지정하는 글꼴은 양식에서 사용하는 경우에만 생성된 양식에 포함됩니다. 서비스에 전달된 XCI 파일에서 포함 글꼴 옵션이 켜진 경우 이 설정은 무시됩니다. 이 경우 PDF에 사용된 모든 글꼴은 항상 포함됩니다.
1. 포함 안 함 글꼴 상자에서 양식에 포함할 글꼴의 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 생성된 PDF에서 사용되더라도 PDF에 포함되지 않습니다. 서비스에 전달된 XCI 파일에서 포함 글꼴 옵션이 꺼져 있으면 이 설정이 무시됩니다. 이 경우 PDF에 사용된 글꼴은 포함되지 않습니다.
1. 저장을 클릭합니다.
