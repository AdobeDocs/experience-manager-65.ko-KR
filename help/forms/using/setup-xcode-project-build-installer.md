---
title: Xcode 프로젝트 설정 및 iOS 앱 빌드
description: iOS용 표준 AEM Forms 앱을 빌드하는 방법을 설명합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 3%

---

# Xcode 프로젝트 설정 및 iOS 앱 빌드{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms은 AEM Forms 앱의 전체 소스 코드를 제공합니다. 소스에는 사용자 지정 AEM Forms 앱을 빌드하기 위한 모든 구성 요소가 포함되어 있습니다. 소스 코드 아카이브, `adobe-lc-mobileworkspace-src-<version>.zip` 의 일부임 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 소프트웨어 배포 패키지

AEM Forms 앱 소스를 가져오려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 선택 **[!UICONTROL Adobe Experience Manager]** 헤더 메뉴에서 사용할 수 있습니다.
1. 다음에서 **[!UICONTROL 필터]** 섹션:
   1. 선택 **[!UICONTROL Forms]** 다음에서 **[!UICONTROL 솔루션]** 드롭다운 목록입니다.
   2. 패키지의 버전 및 유형을 선택합니다. 다음을 사용할 수도 있습니다 **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**, 및 선택 **[!UICONTROL 다운로드]**.
1. 열기 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  및 클릭 **[!UICONTROL 패키지 업로드]** 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. 소스 코드 아카이브를 다운로드하려면 를 엽니다. `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 을 클릭합니다.
소스 패키지가 디바이스에 다운로드됩니다.

다음 이미지는 추출된 내용을 표시합니다. `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

다음 표는 의 내용을 자세히 설명합니다. `adobe-lc-mobileworkspace-src-[version]/ios` 폴더를 삭제합니다.

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

코드 서명 및 iOS 프로비저닝 포털에 장치 추가에 대한 자세한 내용은 [iOS 코드 서명 설정, 프로세스 및 문제 해결](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## 표준 AEM Forms 앱 빌드 {#set-up-the-xcode-project}

1. Xcode에서 프로젝트를 설정하고 서명 ID를 제공하려면 다음 단계를 수행하십시오.

   Xcode 및 iOS SDK가 설치 및 구성된 Mac 컴퓨터에 로그인합니다.

1. 다음을 복사합니다. `adobe-lc-mobileworkspace-src-<version>.zip` 다운로드 폴더에서 다음으로 보관 `[User_Home]/Projects/`.
1. 에서 아카이브 추출 `[User_Home]/Projects/[your-project]`디렉토리.
1. 다음 위치로 이동 ` [User_Home]/Projects/ `[your-project]`/adobe-lc-mobileworkspace-src-[version]/ios` 디렉토리.
1. 를 엽니다. `AEM Forms.xcodeproj` xcode의 프로젝트입니다.
1. 클릭 **AEM Forms**, 아래 **타겟**, 선택 **AEM Forms**. 다음 항목 선택 **빌드 설정** 탭에서 다음을 찾습니다. **코드 서명 권한** 섹션으로 이동하여 디버그 및 릴리스 필드에서 다음 중 하나를 수행합니다.

   * 표준 모바일 작업 영역 앱을 빌드하려면 필드를 지정하지 마십시오
   * 에 설명된 대로 필드를에 지정합니다. [iOS용 보안 AEM Forms 앱 구축](/help/forms/using/building-secure-mobile-workspace-app.md) 보안 AEM Forms 앱을 빌드합니다.

1. 다음에서 **빌드 설정** 탭을 클릭하고 **모두** 그런 다음 을 클릭합니다. **결합**.
1. 다음에서 **설정** 목록, 확장 **코드 서명**.
1. 대상 **코드 서명 ID**&#x200B;적절한 서명을 선택합니다. 새 서명 만들기에 대한 자세한 내용은 [개발 프로비저닝 프로필 만들기 및 다운로드](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. 에 대해 동일한 서명을 선택해야 합니다. **디버그**, **릴리스**, 및 **모든 iOS SDK**.
1. 에서 다음 코드를 바꿉니다. `AEM Forms-info.plist` 파일:

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   을 교체하는 동안 다음과 같이 `yourserver.com` 서버에 적합한 호스트 이름을 사용합니다.

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
   >이 단계는 AEM Forms 앱이 앱 전송 보안 요구 사항을 따르지 않는 서버에 연결해야 하는 경우에만 필요합니다.

1. 아래 **프로젝트**, 선택 **AEM Forms** 및에 대한 적절한 서명이 선택되어 있는지 확인합니다. **코드 서명 ID**, **디버그**, **릴리스** 및 **모든 iOS SDK**.
1. 프로비저닝된 iPad을 Mac 시스템에 연결합니다.
1. 다음에 대해 프로비저닝된 장치 선택 **AEM Forms** 프로젝트.

   ![ipad](assets/ipad.png)

   프로비저닝된 디바이스, iPad Air 2가 선택됩니다.

1. 선택 **제품** > **정리**.
1. 선택 **제품** > **빌드**.

## AEM Forms 앱용 설치 관리자 빌드 {#build-the-installer-for-the-mobile-workspace-app}

설치 관리자(.ipa 파일) 및 속성 목록(.plist 파일) 파일을 빌드하려면 Xcode 프로젝트를 보관해야 합니다. 속성 목록 파일에는 호스팅된 사내 앱의 구성 정보(예: 앱 이름 및 호스팅 위치)가 포함되어 있습니다. 속성 목록 파일에 대한 자세한 내용은 [정보 등록 정보 목록 파일 정보](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 프로비저닝된 iPad을 Mac 시스템에 연결합니다. iPad 프로비저닝에 대한 자세한 내용은 다음을 참조하십시오. [개발 프로비저닝 프로필 만들기 및 다운로드](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 다음에 대해 프로비저닝된 장치 선택 **AEM Forms** 프로젝트.

   ![ipad-1](assets/ipad-1.png)

   프로비저닝된 디바이스, iPad Air 2가 선택됩니다.

1. 선택 **제품** > **정리**.
1. 선택 **제품** > **빌드**.
1. 선택 **제품** > **보관**.
1. 주최자 - 아카이브에서 프로젝트의 최신 아카이브를 선택하고 **배포**.
1. 선택 **엔터프라이즈 또는 임시 배포를 위해 저장** 배포 및 클릭 방법으로 **다음**.
1. 적절한 항목 선택 **코드 서명 ID** 및 클릭 **다음**. 클릭 **허용** 서명을 적용합니다.
1. 앱 이름을 입력하고 다음을 선택합니다. **엔터프라이즈 배포를 위해 저장**.
1. 다음을 제공합니다 **애플리케이션 URL** 앱용 예를 들어 CRX 서버에서 앱을 호스팅하려면 URL을 제공합니다 `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. 다음에서 **제목** 필드, AEM Forms 지정
1. 클릭 **저장** Xcode를 닫습니다.

   설치 관리자 파일, `AEM Forms.ipa`및 속성 목록 파일, `AEM Forms-info.plist`: 지정된 위치에 만들어집니다.

1. 를 엽니다. `AEM Forms-info.plist` 파일을 편집기에 넣습니다.
1. .ipa 파일의 URL에 있는 모든 공백을 %20(으)로 바꿉니다.
1. 저장 후 닫기 `AEM Forms-info.plist` 파일.
