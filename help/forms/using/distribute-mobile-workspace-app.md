---
title: AEM Forms 앱 배포
seo-title: AEM Forms 앱 배포
description: 모바일 장치에 앱을 대량으로 배포하려면 MDM(모바일 장치 관리)을 사용하십시오.
seo-description: 모바일 장치에 앱을 대량으로 배포하려면 MDM(모바일 장치 관리)을 사용하십시오.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms 앱 배포 {#distribute-aem-forms-app}

모바일 장치 관리(MDM)를 통해 모바일 장치에 앱을 대량으로 배포할 수 있습니다.

>[!NOTE]
>
>이 배포는 iOS 및 Android 장치에만 적용됩니다.

## 일반적으로 MDM 솔루션에서 제공하는 주요 기능: {#main-features-generally-provided-by-mdm-solutions}

* 기업 환경에서 디바이스 등록 활성화
* 장치 설정 구성 및 업데이트 허용
* 보안 규정 준수 강화
* 기업 리소스에 대한 안전한 모바일 액세스

모바일 애플리케이션 관리와 함께 MDM 솔루션을 사용하면 기업 내 모바일 장치 전체에서 내부, 공개 및 구입한 앱을 관리할 수 있습니다.

MDM 관리자는 ipa 및 apk 파일을 모두 MDM 서버에 업로드하고 ipa 또는 apk 파일에 액세스할 수 있는 사용자를 제어할 수 있습니다. 관리자는 각 응용 프로그램에 해당하는 프로필 설정을 제어할 수도 있습니다.

## AEM Forms 앱에 영향을 주는 프로필 설정 {#profile-settings-affecting-the-aem-forms-app-br}

장치에서 다음 프로필 설정은 장치에서 AEM Forms 앱의 기능에 영향을 줍니다.

* **장치 기능** 섹션에서 카메라 **사용** 허용

카메라 **사용**&#x200B;허용을 비활성화하면 사진 주석의 [카메라 기능이](/help/forms/using/add-attachments.md) 작동하지 않습니다. 앱에서 카메라를 사용하려면 이 옵션을 활성화해야 합니다.

* **암호 정책 섹션의 장치에** 암호 필요

응용 프로그램 데이터의 ****&#x200B;암호화를 활성화하려면 장치에서 **패스코드를** 활성화하는 것이 좋습니다. 장치에 패스코드가 설정되어 있지 않으면 장치에 저장된 응용 프로그램 데이터가 암호화되지 않습니다.
