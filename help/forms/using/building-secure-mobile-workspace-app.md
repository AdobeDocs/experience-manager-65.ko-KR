---
title: iOS용 보안 AEM Forms 앱 빌드
seo-title: iOS용 보안 AEM Forms 앱 빌드
description: 보안 AEM Forms 앱을 빌드하는 절차.
seo-description: 보안 AEM Forms 앱을 빌드하는 절차.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# iOS용 보안 AEM Forms 앱 빌드 {#building-a-secure-aem-forms-app-for-ios}

설치 프로그램(.ipa 파일) 및 속성 목록(.plist 파일) 파일을 빌드하려면 AEM Forms 앱용 Xcode 프로젝트를 보관해야 합니다. 속성 목록 파일에는 앱의 이름 및 호스팅 위치와 같은 호스팅된 사내 앱의 구성 정보가 포함되어 있습니다. 속성 목록 파일에 대한 자세한 내용은 [정보 속성 목록 파일 정보](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)를 참조하십시오.

1. 다음 웹 사이트에 로그인합니다.

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 앱 ID 만들기를 참조하십시오. 앱 ID를 만드는 자세한 방법은 [앱 ID 만들기 및 구성](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)을 참조하십시오.
1. 앱에 대한 iOS 응용 프로그램의 번들 식별자를 구성하려면 **[!UICONTROL 앱 ID 구성]**&#x200B;을 클릭합니다.
1. 웹 페이지 하단에서 **[!UICONTROL 데이터 보호 활성화]**&#x200B;를 선택합니다. 데이터 보호 옵션을 지정합니다.

   **[!UICONTROL 완료]**&#x200B;를 클릭합니다.

1. 3단계에서 구성한 앱 ID를 사용하여 프로비저닝->배포로 이동하고 새 프로필을 만듭니다.
1. 프로비저닝 프로필을 다운로드하여 Xcode 및 iPad에 추가합니다.
1. Xcode 및 iOS SDK가 설치 및 구성된 Mac 컴퓨터에 로그인합니다.
1. Xcode에서 `AEM Forms.xcodeproj` 프로젝트를 엽니다.
1. **[!UICONTROL AEM Forms]** TARGET ]**에서**[!UICONTROL  AEM Forms ]**를 클릭합니다.**[!UICONTROL  **[!UICONTROL 빌드 설정]** 탭을 선택하고 **[!UICONTROL 코드 서명 자격 부여]** 섹션을 찾은 다음 권한 드롭다운에서 **[!UICONTROL LC Enterprise]** 옵션을 선택합니다.
1. 편집할 Xcode에서 `LC Enterprise.entitlements` 파일을 찾아 엽니다. **XCode 권한**&#x200B;에서 프로비저닝 프로필에 있는 것과 동일한 키-값 쌍을 추가합니다.
1. **[!UICONTROL 빌드 설정]** 탭에서 **[!UICONTROL 모두]**&#x200B;를 클릭한 다음 **[!UICONTROL 결합]**&#x200B;을 클릭합니다.
1. **[!UICONTROL 설정]** 목록에서 **[!UICONTROL 코드 서명]**&#x200B;을 확장합니다.
1. **[!UICONTROL 코드 서명 ID]**&#x200B;의 경우 적절한 서명을 선택합니다. **[!UICONTROL 디버그]**, **[!UICONTROL 릴리스]** 및 **[!UICONTROL 모든 iOS SDK]**&#x200B;에 대해 동일한 서명이 선택되어 있는지 확인합니다.
1. **[!UICONTROL PROJECT]**&#x200B;에서 **[!UICONTROL AEM Forms]**&#x200B;을 선택하고 **[!UICONTROL 코드 서명 ID]**, **[!UICONTROL 디버그]**, **[!UICONTROL 릴리스]** 및 **[!UICONTROL 모든 iOS SDK&lt;a 11/>.]**
1. AEM Forms 앱 빌드 및 배포. AEM Forms 앱을 빌드하고 배포하는 방법에 대한 자세한 내용은 [AEM Forms 앱용 설치 프로그램 만들기](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)를 참조하십시오.
