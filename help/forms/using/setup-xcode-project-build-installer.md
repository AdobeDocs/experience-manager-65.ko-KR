---
title: Xcode 프로젝트 설정 및 iOS 앱 빌드
seo-title: Xcode 프로젝트 설정 및 iOS 앱 빌드
description: iOS용 표준 AEM Forms 앱을 빌드하는 방법에 대해 설명합니다.
seo-description: iOS용 표준 AEM Forms 앱을 빌드하는 방법에 대해 설명합니다.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
translation-type: tm+mt
source-git-commit: 72a582b7ac19322b81fd1a92de8fce34e55b9db1

---


# Xcode 프로젝트 설정 및 iOS 앱 빌드{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms는 AEM Forms 앱의 전체 소스 코드를 제공합니다. 소스에는 사용자 정의 AEM Forms 앱을 빌드하는 모든 구성 요소가 포함되어 있습니다. 소스 코드 아카이브는 `adobe-lc-mobileworkspace-src-<version>.zip` 패키지 공유의 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 패키지의 일부입니다.

AEM Forms 앱 소스를 가져오려면 다음 단계를 수행하십시오.

1. shareURL 패키지로 이동: `https://<server>:<port>/crx/packageshare`Adobe

1. 소스 패키지를 다운로드합니다. 패키지를 다운로드하면 AEM Forms 패키지 관리자에 추가됩니다.
1. 다운로드가 완료되면 다음 위치로 이동합니다.를 `https://<server>:<port>/crx/packmgr/index.jsp`설치하고 설치합니다 `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. 소스 코드 아카이브를 다운로드하려면 브라우저에서 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 엽니다.
소스 패키지가 장치에 다운로드됩니다.

다음 이미지는 추출된 파일의 내용을 표시합니다 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

다음 표에서는 `adobe-lc-mobileworkspace-src-[version]/ios` 폴더의 컨텐츠를 자세히 설명합니다.

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

코드 서명 및 iOS 프로비저닝 포털에 장치 추가에 대한 자세한 내용은 iOS 코드 [서명 설정, 프로세스 및 문제 해결을 참조하십시오](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## 표준 AEM Forms 앱 빌드 {#set-up-the-xcode-project}

1. Xcode에서 프로젝트를 설정하고 서명 ID를 제공하려면 다음 단계를 수행하십시오.

   Xcode 및 iOS SDK가 설치 및 구성된 Mac 시스템에 로그인합니다.

1. 다운로드 `adobe-lc-mobileworkspace-src-<version>.zip` 폴더의 아카이브를 다음 위치에 복사합니다 `[User_Home]/Projects/`.
1. 디렉토리에서 아카이브를 `[User_Home]/Projects/[your-project]`추출합니다.
1. 프로젝트 ` [User_Home]/Projects/ `[디렉터리로 이동합니다]`/adobe-lc-mobileworkspace-src-[version]/ios` .
1. Xcode에서 `AEM Forms.xcodeproj` 프로젝트를 엽니다.
1. AEM **Forms를**&#x200B;클릭하고 **TARGETS**&#x200B;아래에서 **AEM Forms를**&#x200B;선택합니다. 빌드 **설정** 탭을 선택하고 코드 서명 **권한** 섹션을 찾은 다음 디버그 및 릴리스 필드에서 다음 중 하나를 수행합니다.

   * 표준 모바일 작업 공간 앱을 빌드하려면 필드를 지정하지 않은 상태로 두십시오
   * 보안 AEM Forms 앱을 [빌드하기 위해 iOS용 보안 AEM Forms 앱 빌드에 설명된 대로](/help/forms/using/building-secure-mobile-workspace-app.md) 필드를 지정합니다.

1. [ **빌드 설정** ] 탭에서 [모두] **를** 클릭한 **다음 [통합]을**&#x200B;클릭합니다.
1. 설정 **목록에서 코드** 서명을 **확장합니다**.
1. 코드 **서명 ID의**&#x200B;경우 해당 서명을 선택합니다. 새 서명 만들기에 대한 자세한 내용은 개발 [프로비저닝 프로필 만들기 및 다운로드를 참조하십시오](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. 디버그, 릴리스 및 모든 iOS SDK에 대해 동일한 **서명이******&#x200B;선택되어 **있는지 확인합니다**.
1. 파일에서 다음 코드를 `AEM Forms-info.plist` 바꿉니다.

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   를 사용하여 서버에 적합한 호스트 `yourserver.com` 이름으로 바꾸는 동안 다음을 수행합니다.

   ```java
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
   >이 단계는 AEM Forms 앱이 앱 전송 보안 요구 사항을 따르지 않는 서버에 연결해야 하는 경우에만 필요합니다.

1. 프로젝트 **아래에서** AEM Forms **를** 선택하고 **적절한 서명이 코드 코드 Identity** Debug **, SigningRelease 및 Signing Signing** For Identity **, SigningRelease 및 Any iOS SDK** ****&#x200B;중 하나를 선택했는지 확인합니다.
1. 제공된 iPad를 Mac 컴퓨터에 연결합니다.
1. AEM Forms 프로젝트에 대해 제공된 **장치를** 선택합니다.

   ![ipad](assets/ipad.png)

   제공된 장치 iPad Air 2가 선택됩니다.

1. 제품 **>** 정리를 **선택합니다**.
1. 제품 **** > 빌드를 **선택합니다**.

## AEM Forms 앱용 설치 프로그램 만들기 {#build-the-installer-for-the-mobile-workspace-app}

설치 프로그램(.ipa 파일)과 속성 목록(.plist 파일)을 빌드하려면 Xcode 프로젝트를 보관해야 합니다. 속성 목록 파일에는 앱의 이름 및 호스팅 위치와 같은 호스팅된 사내 앱의 구성 정보가 포함되어 있습니다. 속성 목록 파일에 대한 자세한 내용은 정보 [속성 목록 파일 정보를 참조하십시오](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 제공된 iPad를 Mac 컴퓨터에 연결합니다. iPad 프로비전에 대한 자세한 내용은 개발 프로비저닝 [프로필 만들기 및 다운로드를 참조하십시오](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. AEM Forms 프로젝트에 대해 제공된 **장치를** 선택합니다.

   ![ipad-1](assets/ipad-1.png)

   제공된 장치 iPad Air 2가 선택됩니다.

1. 제품 **>** 정리를 **선택합니다**.
1. 제품 **** > 빌드를 **선택합니다**.
1. 제품 **> 보관을** **선택합니다**.
1. 문서 분류함 - 보관에서 프로젝트의 최신 아카이브를 선택하고 배포를 **클릭합니다**.
1. 배포 **방법으로 기업 또는 애드혹** 배포용으로 저장을 선택하고 다음을 **클릭합니다**.
1. 적절한 코드 **서명 ID를** 선택하고 다음을 **클릭합니다**. 승인을 **클릭하여** 서명을 적용합니다.
1. 앱의 이름을 입력하고 Enterprise Distribution **용으로 저장을 선택합니다**.
1. 앱용 **애플리케이션** URL을 제공합니다. 예를 들어 CRX 서버에서 앱을 호스팅하려면 URL을 제공합니다 `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. 제목 **필드에서** AEM Forms를 지정합니다.
1. 저장을 **클릭하고** Xcode를 닫습니다.

   설치 관리자 파일 `AEM Forms.ipa`및 속성 목록 파일이 `AEM Forms-info.plist`지정된 위치에 생성됩니다.

1. 편집기에서 파일을 엽니다 `AEM Forms-info.plist` .
1. .ipa 파일의 URL에 있는 모든 공백을 %20으로 바꿉니다.
1. 파일을 저장하고 `AEM Forms-info.plist` 닫습니다.