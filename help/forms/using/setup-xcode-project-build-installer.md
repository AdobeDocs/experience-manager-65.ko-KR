---
title: Xcode 프로젝트를 설정하고 iOS 앱을 빌드합니다.
seo-title: Set up the Xcode project and build the iOS app
description: iOS용 표준 AEM Forms 앱을 빌드하는 방법을 설명합니다.
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Xcode 프로젝트를 설정하고 iOS 앱을 빌드합니다.{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms은 AEM Forms 앱의 전체 소스 코드를 제공합니다. 소스에는 사용자 지정 AEM Forms 앱을 빌드할 모든 구성 요소가 포함되어 있습니다. 소스 코드 아카이브, `adobe-lc-mobileworkspace-src-<version>.zip` 는 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 소프트웨어 배포 패키지

AEM Forms 앱 소스를 가져오려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에 제공된 **[!UICONTROL Adobe Experience Manager]**&#x200B;를 누릅니다.
1. 에서 **[!UICONTROL 필터]** 섹션:
   1. 선택 **[!UICONTROL Forms]** 에서 **[!UICONTROL 솔루션]** 드롭다운 목록.
   2. 패키지의 버전 및 유형을 선택합니다. 를 사용할 수도 있습니다 **[!UICONTROL 다운로드 검색]** 결과를 필터링하는 옵션.
1. 운영 체제에 해당하는 패키지 이름을 탭하고 **[!UICONTROL EULA 약관 동의]**, 탭 **[!UICONTROL 다운로드]**.
1. [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. 소스 코드 아카이브를 다운로드하려면 다음을 엽니다 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 브라우저에서
소스 패키지가 장치에서 다운로드됩니다.

다음 이미지는 추출된 컨텐츠의 내용을 표시합니다 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

다음 표에서는 `adobe-lc-mobileworkspace-src-[version]/ios` 폴더를 입력합니다.

<table>
 <tbody>
  <tr>
   <th><p>디렉토리</p> </th>
   <th><p>컨텐트</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>리소스, PhoneGap 플러그인 및 애플리케이션의 기본 모듈</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>AEM Forms 앱용 Xcode 프로젝트</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>AEM Forms 앱 프로젝트용 HTML, CSS, 이미지 및 JavaScript 파일</p> </td>
  </tr>
 </tbody>
</table>

코드 서명 및 iOS Provisioning Portal에 장치 추가에 대한 자세한 내용은 [iOS 코드 서명 설정, 프로세스 및 문제 해결](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## 표준 AEM Forms 앱 구축 {#set-up-the-xcode-project}

1. Xcode에서 프로젝트를 설정하고 서명 ID를 제공하려면 다음 단계를 수행하십시오.

   Xcode 및 iOS SDK가 설치 및 구성된 Mac 시스템에 로그인합니다.

1. 를 복사합니다. `adobe-lc-mobileworkspace-src-<version>.zip` 다운로드 폴더에서 로 보관 `[User_Home]/Projects/`.
1. 에서 아카이브 추출 `[User_Home]/Projects/[your-project]`디렉토리.
1. 로 이동합니다 ` [User_Home]/Projects/ `[프로젝트]`/adobe-lc-mobileworkspace-src-[version]/ios` 디렉토리.
1. 를 엽니다. `AEM Forms.xcodeproj` 프로젝트에 포함되어 있습니다.
1. 클릭 **AEM Forms**, 아래에 **Target**, 선택 **AEM Forms**. 을(를) 선택합니다 **빌드 설정** 탭에서 를 찾습니다 **코드 서명 권한** 섹션을 수정하고 디버그 및 릴리스 필드에서 다음 중 하나를 수행합니다.

   * 표준 Mobile Workspace 앱을 빌드하려면 필드를 지정되지 않은 상태로 둡니다
   * 에 설명된 대로 필드를 지정합니다 [iOS용 보안 AEM Forms 앱 빌드](/help/forms/using/building-secure-mobile-workspace-app.md) 보안 AEM Forms 앱을 빌드하려면 다음을 수행하십시오.

1. 에서 **빌드 설정** 탭, **모두** 을 클릭한 다음 **결합**.
1. 에서 **설정** 목록, 확장 **코드 서명**.
1. 대상 **코드 서명 ID**&#x200B;적절한 서명을 선택합니다. 새 서명 만들기에 대한 자세한 내용은 [개발 프로비저닝 프로필 만들기 및 다운로드](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. 에 대해 동일한 서명이 선택되어 있는지 확인합니다 **디버그**, **릴리스**, 및 **모든 iOS SDK**.
1. 에서 다음 코드를 바꿉니다 `AEM Forms-info.plist` 파일:

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   을 교체하는 동안 `yourserver.com` ( 서버의 적절한 호스트 이름 사용)

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >이 단계는 앱 전송 보안 요구 사항을 따르지 않는 서버에 AEM Forms 앱을 연결해야 하는 경우에만 필요합니다.

1. 아래 **프로젝트**, 선택 **AEM Forms** 및에 대한 적절한 서명이 선택되었는지 확인합니다. **코드 서명 ID**, **디버그**, **릴리스** 및 **모든 iOS SDK**.
1. 프로비저닝된 iPad을 Mac 컴퓨터에 연결합니다.
1. 에 대해 제공된 장치를 선택합니다 **AEM Forms** 프로젝트.

   ![ipad](assets/ipad.png)

   제공된 장치인 iPad Air 2가 선택됩니다.

1. 선택 **제품** > **Clean**.
1. 선택 **제품** > **빌드**.

## AEM Forms 앱용 설치 프로그램 빌드 {#build-the-installer-for-the-mobile-workspace-app}

설치 프로그램(.ipa 파일)과 속성 목록(.plist 파일) 파일을 빌드하려면 Xcode 프로젝트를 보관해야 합니다. 속성 목록 파일에는 앱의 이름 및 호스팅 위치와 같은 호스팅된 인하우스 앱의 구성 정보가 포함되어 있습니다. 속성 목록 파일에 대한 자세한 내용은 [정보 속성 목록 파일 정보](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 프로비저닝된 iPad을 Mac 컴퓨터에 연결합니다. iPad 프로비저닝에 대한 자세한 내용은 [개발 프로비저닝 프로필 만들기 및 다운로드](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 에 대해 제공된 장치를 선택합니다 **AEM Forms** 프로젝트.

   ![ipad-1](assets/ipad-1.png)

   제공된 장치인 iPad Air 2가 선택됩니다.

1. 선택 **제품** > **Clean**.
1. 선택 **제품** > **빌드**.
1. 선택 **제품** > **아카이브**.
1. Organizer - Archives에서 프로젝트의 최신 아카이브를 선택하고 **배포**.
1. 선택 **엔터프라이즈 또는 애드혹 배포를 위한 저장** 을 배포 방법으로 설정하고 을 클릭합니다. **다음**.
1. 적절한 **코드 서명 ID** 을(를) 클릭합니다. **다음**. 클릭 **허용** 서명을 적용하려면
1. 앱 이름을 입력하고 을(를) 선택합니다 **엔터프라이즈 배포를 위한 저장**.
1. 다음을 제공합니다. **애플리케이션 URL** 추가 콘텐츠만 사용할 수 있습니다. 예를 들어 CRX 서버에서 앱을 호스팅하려면 URL을 제공합니다 `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. 에서 **제목** 필드에서 AEM Forms을 지정합니다.
1. 클릭 **저장** 및 를 닫습니다.

   설치 프로그램 파일 `AEM Forms.ipa`, 및 속성 목록 파일, `AEM Forms-info.plist`은 지정된 위치에 만들어집니다.

1. 를 엽니다. `AEM Forms-info.plist` 파일을 편집기에 저장합니다.
1. .ipa 파일의 URL에 있는 모든 공백을 %20으로 바꿉니다.
1. 저장 후 닫기 `AEM Forms-info.plist` 파일.
