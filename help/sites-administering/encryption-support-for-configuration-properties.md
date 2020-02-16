---
title: 구성 속성에 대한 암호화 지원
seo-title: 구성 속성에 대한 암호화 지원
description: 'null'
seo-description: 'null'
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 구성 속성에 대한 암호화 지원{#encryption-support-for-configuration-properties}

## 개요 {#overview}

이 기능을 사용하면 모든 OSGi 구성 속성을 명확한 텍스트 대신 보호된 암호화된 양식으로 저장할 수 있습니다. 웹 콘솔 UI의 양식은 시스템 전체 암호화 마스터 키를 사용하여 일반 텍스트에서 암호화된 텍스트를 만드는 데 사용됩니다.

서비스에서 사용하기 전에 속성의 암호를 해독하기 위해 OSGi 구성 플러그인 지원이 추가되었습니다.

>[!NOTE]
>
>암호화된 값이 필요한 서비스는 IsProtected 검사를 사용하여 암호를 해독하기 전에 값이 암호화되었는지 확인해야 합니다. 이미 암호를 해독했을 수 있습니다.

## 암호화 지원 활성화 {#enabling-encryption-support}

이 단계는 메일 서비스에 대한 SMTP 암호를 암호화하는 방법을 보여줍니다. 암호화할 OSGI 속성에 대해 이러한 단계를 완료할 수 있습니다.

1. https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr의 *AEM 웹 콘솔로 이동합니다.*
1. 왼쪽 상단 모서리에서 Main - **Crypto 지원으로 이동합니다.**

   ![chlimage_1-321](assets/chlimage_1-325.png)

1. Adobe **Experience Manager 웹 콘솔 암호화 지원** 페이지가 표시됩니다.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. 일반 **텍스트** 필드에 보호할 중요한 데이터의 텍스트를 입력합니다.
1. 보호를 **선택합니다**. 보호된 텍스트는 암호화된 텍스트로 표시됩니다.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. 5단계에서 보호된 텍스트를 복사하여 OSGI 양식 값에 붙여넣습니다. 이 예에서는 암호화된 SMTP **암호가** Day CQ Mail *Service에 추가됩니다*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. 요일 CQ 메일 서비스 속성을 저장합니다. 이제 SMTP 암호가 암호화된 값으로 전송됩니다.

## 암호 해독 지원 {#decryption-support}

이제 AEM에서 구성 속성을 해독하는 구성 플러그인을 제공합니다. 이 AEM 플러그인은 명확한 텍스트 속성을 자동으로 해독하고 검색합니다.
