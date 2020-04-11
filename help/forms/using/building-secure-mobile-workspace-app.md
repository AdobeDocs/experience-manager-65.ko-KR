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
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# iOS용 보안 AEM Forms 앱 빌드 {#building-a-secure-aem-forms-app-for-ios}

설치 프로그램(.ipa 파일)과 속성 목록(.plist 파일) 파일을 빌드하려면 AEM Forms 앱용 Xcode 프로젝트를 보관해야 합니다. 속성 목록 파일에는 앱의 이름 및 호스팅 위치와 같은 호스팅된 사내 앱의 구성 정보가 포함되어 있습니다. 속성 목록 파일에 대한 자세한 내용은 정보 [속성 목록 파일 정보를 참조하십시오](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 다음 웹 사이트에 로그인합니다.

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 앱 ID 만들기를 참조하십시오. 앱 ID를 만드는 자세한 단계는 앱 ID [만들기 및 구성을 참조하십시오](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. 앱에 대한 iOS 응용 프로그램의 번들 식별자를 구성하려면 앱 ID **[!UICONTROL 구성을 클릭합니다]**.
1. 웹 페이지 하단에서 데이터 보호 **[!UICONTROL 활성화를 선택합니다]**. 데이터 보호 옵션을 지정합니다.

   완료를 **[!UICONTROL 클릭합니다]**.

1. Provisioning->Distribution으로 이동하고 3단계에서 구성된 앱 ID를 사용하여 새 프로필을 만듭니다.
1. Xcode 및 iPad에 프로비저닝 프로필을 다운로드하고 추가합니다.
1. Xcode 및 iOS SDK가 설치 및 구성된 Mac 시스템에 로그인합니다.
1. Xcode에서 `AEM Forms.xcodeproj` 프로젝트를 엽니다.
1. AEM **[!UICONTROL Forms를]**&#x200B;클릭하고 **[!UICONTROL TARGETS]**&#x200B;아래에서 **[!UICONTROL AEM Forms를]**&#x200B;선택합니다. 빌드 **[!UICONTROL 설정]** 탭을 선택하고 코드 서명 **[!UICONTROL 권한 부여]** 섹션을 찾은 후 권한 드롭다운에서 LC 엔터프라이즈 **[!UICONTROL 옵션을]** 선택합니다.
1. 편집할 Xcode에서 파일을 찾아 엽니다. `LC Enterprise.entitlements` XCode **권한**&#x200B;아래에서 프로비저닝 프로필에 있는 것과 동일한 키-값 쌍을 추가합니다.
1. [ **[!UICONTROL 빌드 설정]** ] 탭에서 [모두] **[!UICONTROL 를]** 클릭한 **[!UICONTROL 다음 [통합]을]**&#x200B;클릭합니다.
1. 설정 **[!UICONTROL 목록에서 코드]** 서명을 **[!UICONTROL 확장합니다]**.
1. 코드 **[!UICONTROL 서명 ID의]**&#x200B;경우 해당 서명을 선택합니다. 디버그, 릴리스 및 모든 iOS SDK에 대해 동일한 **[!UICONTROL 서명이]******&#x200B;선택되어 **[!UICONTROL 있는지 확인합니다]**.
1. 프로젝트 **[!UICONTROL 아래에서]** AEM Forms **[!UICONTROL 를]** 선택하고 **[!UICONTROL 적절한 서명이 코드 코드 Identity]** Debug **[!UICONTROL , SigningRelease 및 Signing Signing]** For Identity **[!UICONTROL , SigningRelease 및 Any iOS SDK]** ****&#x200B;중 하나를 선택했는지 확인합니다.
1. AEM Forms 앱 빌드 및 배포. AEM Forms 앱을 빌드하고 배포하는 방법에 대한 자세한 지침은 AEM Forms 앱용 [설치 프로그램](/help/forms/using/setup-xcode-project-build-installer.md#main-pars-text-12)빌드를 참조하십시오.
