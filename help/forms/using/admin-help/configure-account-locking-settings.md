---
title: 계정 잠금 설정 구성
description: 지정된 수의 연속 인증 실패 후 사용자 계정을 잠그려면 계정 잠금 활성화 옵션을 사용합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 계정 잠금 설정 구성 {#configure-account-locking-settings}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

도메인을 추가할 때 계정 잠금을 활성화할지 여부를 지정합니다. 계정 잠금 활성화 옵션을 선택하면 지정된 수의 연속 인증 실패 후 사용자 계정이 잠깁니다. 지정된 시간이 경과하면 사용자는 다시 인증을 시도할 수 있습니다. 이 기능은 사용자가 시스템에 액세스하기 위해 다양한 자격 증명 조합을 시도하지 못하도록 합니다.

도메인 관리 페이지의 설정을 사용하여 최대 인증 실패 횟수와 계정이 잠긴 기간을 지정합니다. 이러한 설정은 계정 잠금이 활성화된 모든 도메인에 적용됩니다.

1. 관리 콘솔에서 **[!UICONTROL 설정 > 사용자 관리 > 도메인 관리]**&#x200B;를 클릭합니다.
1. 최대 연속 인증 실패 상자에 계정이 잠기기 전에 사용자가 로그인을 시도할 수 있는 연속 횟수를 입력합니다. 기본값은 20입니다.
1. 다음 시간 이후에 계정 잠금 해제(분) 상자에 사용자 계정이 잠긴 시간(분)을 입력합니다. 지정한 시간(분) 후에 사용자는 다시 로그인을 시도할 수 있습니다. 기본값은 30입니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
