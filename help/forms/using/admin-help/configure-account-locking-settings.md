---
title: 계정 잠금 설정 구성
seo-title: 계정 잠금 설정 구성
description: 지정된 수의 연속적인 인증 실패 후 사용자 계정을 잠그려면 계정 잠금 활성화 옵션을 사용합니다.
seo-description: 지정된 수의 연속적인 인증 실패 후 사용자 계정을 잠그려면 계정 잠금 활성화 옵션을 사용합니다.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 4%

---


# 계정 잠금 설정 구성 {#configure-account-locking-settings}

도메인을 추가할 때 계정 잠금을 활성화할지 여부를 지정합니다. [계정 잠금 활성화] 옵션을 선택하면 지정된 수의 연속적인 인증 실패 후 사용자 계정이 잠깁니다. 지정된 시간 후에 사용자가 다시 인증을 시도할 수 있습니다. 이 기능은 사용자가 시스템에 액세스하기 위해 다양한 자격 증명 조합을 시도하지 못하도록 합니다.

[도메인 관리] 페이지의 설정을 사용하여 최대 인증 실패 횟수와 계정이 잠긴 시간을 지정합니다. 이러한 설정은 계정 잠금이 활성화된 모든 도메인에 적용됩니다.

1. 관리 콘솔에서 **[!UICONTROL 설정 > 사용자 관리 > 도메인 관리]**&#x200B;를 클릭합니다.
1. 최대 연속 인증 실패 상자에 사용자가 계정이 잠기기 전에 로그인을 시도할 수 없었던 연속적인 횟수를 입력합니다. 기본값은 20입니다.
1. [다음 이후 계정 잠금 해제(분)] 상자에 사용자 계정이 잠긴 시간(분)을 입력합니다. 지정된 시간(분) 후 사용자가 다시 로그인을 시도할 수 있습니다. 기본값은 30입니다.
1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

