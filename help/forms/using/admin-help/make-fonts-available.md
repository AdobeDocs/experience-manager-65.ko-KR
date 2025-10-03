---
title: 글꼴을 사용 가능하도록 제공
description: 양식 내에서 사용되는 글꼴을 AEM Forms를 호스팅하는 J2EE Application Server에서 사용할 수 있도록 합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '228'
ht-degree: 100%

---

# 글꼴을 사용 가능하도록 제공 {#make-fonts-available}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

양식 내에서 사용되는 글꼴을 AEM Forms를 호스팅하는 J2EE Application Server에서 사용할 수 있도록 합니다. 예를 들어 다음 시나리오를 생각해 보십시오. 양식 디자이너가 Designer에서 사용하는 글꼴 디렉터리에 글꼴을 추가하고 별도의 컴퓨터에서 해당 글꼴을 사용하는 양식을 만듭니다. Output 서비스에서 해당 글꼴을 사용하려면 이 글꼴을 고객 글꼴 디렉터리에 넣습니다. 고객 글꼴 디렉터리가 없으면 AEM Forms를 호스팅하는 J2EE Application Server에 디렉터리를 만듭니다.

추가 글꼴 설정에 대한 자세한 내용은 [일반 AEM Forms 설정 구성](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)을 참조하십시오.

**고객 글꼴 디렉터리 위치 지정**

1. 관리 콘솔에서 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
1. 시스템 글꼴 디렉터리 위치 상자에 고객 글꼴 디렉터리의 경로를 입력합니다. 여러 디렉터리를 세미콜론(**;**)으로 구분하여 추가할 수 있습니다.
1. 확인을 클릭합니다.
1. AEM Forms가 설치된 시스템을 다시 시작합니다.

>[!NOTE]
>
>글꼴은 Windows 시스템 글꼴 캐시에서 선택되며 캐시를 업데이트하려면 시스템을 다시 시작해야 합니다. 고객 글꼴 디렉터리를 지정한 후 AEM Forms가 설치된 시스템을 다시 시작하십시오.
