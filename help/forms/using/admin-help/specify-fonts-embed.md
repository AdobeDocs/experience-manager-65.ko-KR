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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 포함할 글꼴 지정{#specify-fonts-to-embed}

출력에서 사용하는 양식에 항상 포함되거나 포함되지 않은 글꼴을 지정할 수 있습니다. 글꼴을 포함하면 양식의 파일 크기가 커집니다. 사용자가 시스템에 가지고 있지 않을 독특한 글꼴을 임베드할 수 있으며, 사용자가 설치할 일반 글꼴을 임베드할 수 없습니다.

>[!NOTE]
>
>출력을 위한 사용자 정의 XCI 파일을 지정한 경우 XCI 파일의 포함 글꼴 옵션이 이러한 설정을 무시합니다. 자세한 내용은 [출력에 대한 파일 위치 지정을 참조하십시오](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

1. 관리 콘솔에서 서비스 > 출력을 클릭합니다.
1. [글꼴 임베드 설정]의 [항상 포함 글꼴] 상자에 양식에 포함할 글꼴 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 양식에 사용된 경우에만 생성된 양식에 포함됩니다. 서비스에 전달된 XCI 파일에서 임베드 글꼴 옵션을 설정한 경우 이 설정은 무시됩니다. 이 경우 PDF에 사용된 모든 글꼴은 항상 임베드됩니다.
1. [글꼴 포함 안 함] 상자에 양식에 포함되지 않은 글꼴 이름을 쉼표로 구분하여 입력합니다. 지정한 글꼴은 생성된 PDF 파섹 서비스에 전달된 XCI 파일에서 포함 글꼴 옵션이 해제된 경우 이 설정은 무시됩니다. 이 경우 PDF에 사용된 글꼴은 포함되지 않습니다.
1. [저장]을 클릭합니다.

