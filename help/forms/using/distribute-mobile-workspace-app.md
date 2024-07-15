---
title: AEM Forms 앱 배포
description: 모바일 장치에서 앱의 대규모 배포에 MDM(모바일 장치 관리)을 사용합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# AEM Forms 앱 배포 {#distribute-aem-forms-app}

모바일 장치 관리(MDM)를 사용하면 모바일 장치에서 앱을 대규모 배포할 수 있습니다.

>[!NOTE]
>
>이 배포는 iOS 및 Android™ 장치에만 적용할 수 있습니다.

## MDM 솔루션에서 제공하는 주요 기능: {#main-features-generally-provided-by-mdm-solutions}

* 엔터프라이즈 환경에서 장치 등록 활성화
* 장치 설정 구성 및 업데이트 허용
* 보안 규정 준수 적용
* 기업 리소스에 대한 모바일 액세스 보안

모바일 애플리케이션 관리와 함께 MDM 솔루션을 사용하면 기업 내 모바일 디바이스에서 내부, 공용 및 구매한 앱을 관리할 수 있습니다.

MDM 관리자는 ipa 및 apk 파일을 모두 MDM 서버에 업로드하고 ipa 또는 apk 파일에 액세스할 수 있는 사용자를 제어할 수 있습니다. 또한 관리자는 각 애플리케이션에 해당하는 프로필 설정을 제어할 수 있습니다.

## AEM Forms 앱에 영향을 주는 프로필 설정 {#profile-settings-affecting-the-aem-forms-app-br}

장치의 다음 프로필 설정은 장치에서 AEM Forms 앱의 기능에 영향을 줍니다.

* **장치 기능** 섹션에서 **카메라 사용 허용**

**카메라 사용 허용**&#x200B;을 사용하지 않도록 설정하면 [사진 주석](/help/forms/using/add-attachments.md)의 카메라 기능이 작동하지 않습니다. 앱에서 카메라를 사용하려면 이 옵션을 활성화하십시오.

* 암호 정책 섹션의 **장치에 암호 필요**

응용 프로그램 데이터의 **암호화**&#x200B;를 사용하려면 장치에서 **암호**&#x200B;를 사용하도록 설정하는 것이 좋습니다. 암호가 장치에 설정되어 있지 않으면 장치에 저장된 응용 프로그램 데이터가 암호화되지 않습니다.
