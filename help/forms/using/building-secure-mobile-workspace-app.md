---
title: iOS용 보안 AEM Forms 앱 구축
seo-title: Building a secure AEM Forms app for iOS
description: 보안 AEM Forms 앱을 빌드하는 단계입니다.
seo-description: Steps to build a secure AEM Forms app.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# iOS용 보안 AEM Forms 앱 구축 {#building-a-secure-aem-forms-app-for-ios}

설치 관리자(.ipa 파일) 및 속성 목록(.plist 파일) 파일을 빌드하려면 AEM Forms 앱용 Xcode 프로젝트를 보관해야 합니다. 속성 목록 파일에는 호스팅된 사내 앱의 구성 정보(예: 앱 이름 및 호스팅 위치)가 포함되어 있습니다. 속성 목록 파일에 대한 자세한 내용은 [정보 등록 정보 목록 파일 정보](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 다음 웹 사이트에 로그인합니다.

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 앱 ID를 만듭니다. 앱 ID를 만드는 자세한 단계는 를 참조하십시오. [앱 ID 만들기 및 구성](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. 앱용 iOS 애플리케이션의 번들 식별자를 구성하려면 **[!UICONTROL 앱 ID 구성]**.
1. 웹 페이지 하단에서 **[!UICONTROL 데이터 보호 활성화]**. 데이터 보호 옵션을 지정합니다.

   클릭 **[!UICONTROL 완료]**.

1. 프로비저닝->배포 로 이동한 다음 3단계에서 구성한 앱 ID를 사용하여 새 프로필을 만듭니다.
1. 프로비저닝 프로필을 다운로드하여 Xcode 및 iPad에 추가합니다.
1. Xcode가 있고 iOS SDK가 설치 및 구성된 Mac 컴퓨터에 로그인합니다.
1. 를 엽니다. `AEM Forms.xcodeproj` xcode의 프로젝트입니다.
1. 클릭 **[!UICONTROL AEM Forms]**, 아래 **[!UICONTROL TARGET]**, 선택 **[!UICONTROL AEM Forms]**. 다음 항목 선택 **[!UICONTROL 빌드 설정]** 탭에서 다음을 찾습니다. **[!UICONTROL 코드 서명 권한]** 섹션을 참조하고 권한 드롭다운에서 **[!UICONTROL LC 엔터프라이즈]** 옵션을 선택합니다.
1. 을(를) 찾아 엽니다. `LC Enterprise.entitlements` 편집할 Xcode의 파일입니다. 아래 **XCode 권한**&#x200B;를 클릭하고 프로비저닝 프로필에 있는 것과 동일한 키-값 쌍을 추가합니다.
1. 다음에서 **[!UICONTROL 빌드 설정]** 탭을 클릭하고 **[!UICONTROL 모두]** 그런 다음 을 클릭합니다. **[!UICONTROL 결합]**.
1. 다음에서 **[!UICONTROL 설정]** 목록, 확장 **[!UICONTROL 코드 서명]**.
1. 대상 **[!UICONTROL 코드 서명 ID]**&#x200B;적절한 서명을 선택합니다. 에 대해 동일한 서명을 선택해야 합니다. **[!UICONTROL 디버그]**, **[!UICONTROL 릴리스]**, 및 **[!UICONTROL 모든 iOS SDK]**.
1. 아래 **[!UICONTROL 프로젝트]**, 선택 **[!UICONTROL AEM Forms]** 및에 대한 적절한 서명이 선택되어 있는지 확인합니다. **[!UICONTROL 코드 서명 ID]**, **[!UICONTROL 디버그]**, **[!UICONTROL 릴리스]** 및 **[!UICONTROL 모든 iOS SDK]**.
1. AEM Forms 앱 빌드 및 배포 AEM Forms 앱을 빌드하고 배포하는 방법에 대한 자세한 지침은 [AEM Forms 앱용 설치 관리자 빌드](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
