---
title: AEM Forms 앱 배포
seo-title: AEM Forms 앱 배포
description: 모바일 장치에서 대규모 앱 배포에 모바일 장치 관리(MDM)를 사용합니다.
seo-description: 모바일 장치에서 대규모 앱 배포에 모바일 장치 관리(MDM)를 사용합니다.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# AEM Forms 앱 배포 {#distribute-aem-forms-app}

모바일 장치 관리(MDM)를 통해 모바일 장치에서 앱을 대규모로 배포할 수 있습니다.

>[!NOTE]
>
>이 배포는 iOS 및 Android 장치에만 적용됩니다.

## 일반적으로 MDM 솔루션에서 제공하는 주요 기능:{#main-features-generally-provided-by-mdm-solutions}

* 엔터프라이즈 환경에서 장치 등록 활성화
* 장치 설정 구성 및 업데이트 허용
* 보안 규정 준수
* 기업 리소스에 대한 안전한 모바일 액세스

Mobile Application Management와 함께 MDM 솔루션을 사용하면 기업의 모바일 장치에서 내부, 공용 및 구입한 앱을 관리할 수 있습니다.

MDM 관리자는 ipa 및 apk 파일을 모두 MDM 서버에 업로드하고 ipa 또는 apk 파일에 액세스할 수 있는 사용자를 제어할 수 있습니다. 관리자는 각 응용 프로그램에 해당하는 프로파일 설정을 제어할 수도 있습니다.

## AEM Forms 앱 {#profile-settings-affecting-the-aem-forms-app-br}에 영향을 주는 프로필 설정

장치에 대한 다음 프로필 설정은 장치에서 AEM Forms 앱의 기능에 영향을 줍니다.

* **장치 기능** 섹션에서  **카메라 사용** 허용

**카메라**&#x200B;을 사용하지 않도록 설정하면 [사진 주석](/help/forms/using/add-attachments.md)의 카메라 기능이 작동하지 않습니다. 앱에서 카메라를 사용하려면 이 옵션을 활성화해야 합니다.

* **암호 정책 섹션의** 장치에서 암호 코드 필요

응용 프로그램 데이터의 **암호화를 활성화하려면**&#x200B;암호&#x200B;**를 장치에서 활성화하는 것이 좋습니다.** 장치에서 암호 코드가 설정되지 않은 경우 장치에 저장된 응용 프로그램 데이터는 암호화되지 않습니다.
