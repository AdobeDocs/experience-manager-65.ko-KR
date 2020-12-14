---
title: 글꼴을 사용할 수 있도록 설정
seo-title: 글꼴을 사용할 수 있도록 설정
description: 양식 내에 사용된 글꼴을 AEM 양식을 호스팅하는 J2EE 응용 프로그램 서버에서 사용할 수 있는지 확인합니다.
seo-description: 양식 내에 사용된 글꼴을 AEM 양식을 호스팅하는 J2EE 응용 프로그램 서버에서 사용할 수 있는지 확인합니다.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 글꼴을 {#make-fonts-available} 사용 가능하게 만들기

양식 내에 사용된 글꼴을 AEM 양식을 호스팅하는 J2EE 응용 프로그램 서버에서 사용할 수 있는지 확인합니다. 예를 들어 다음 시나리오를 생각해 보십시오. 양식 디자이너는 Designer에서 사용하는 글꼴 디렉토리에 글꼴을 추가하고 별도의 컴퓨터에서 해당 글꼴을 사용하는 양식을 만듭니다. 출력 서비스에서 해당 글꼴을 사용하려면 고객 글꼴 디렉토리에 글꼴을 배치합니다. 고객 글꼴 디렉토리가 없는 경우 AEM 양식을 호스팅하는 J2EE 응용 프로그램 서버에 디렉토리를 만듭니다.

추가 글꼴 설정에 대한 자세한 내용은 [일반 AEM 양식 설정 구성](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)을 참조하십시오.

**고객 글꼴 디렉토리의 위치 지정**

1. 관리 콘솔에서 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
1. [시스템 글꼴 디렉토리 위치] 상자에 고객 글꼴 디렉토리 경로를 입력합니다. 여러 디렉터리를 세미콜론 **;**&#x200B;으로 구분하여 추가할 수 있습니다.
1. 확인을 클릭합니다.
1. AEM 양식이 설치된 시스템을 다시 시작합니다.

>[!NOTE]
>
>글꼴은 Windows 시스템 글꼴 캐시에서 선택되며 캐시를 업데이트하려면 시스템을 다시 시작해야 합니다. 고객 글꼴 디렉토리를 지정한 후 AEM 양식이 설치된 시스템을 다시 시작해야 합니다.

