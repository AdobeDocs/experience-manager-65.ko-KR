---
title: 브랜딩 사용자 지정
seo-title: 브랜딩 사용자 지정
description: 애플리케이션 아이콘, 애플리케이션 이름, 실행 이미지 및 로그인 페이지를 사용자 정의하여 별도의 조직별 모양과 느낌을 AEM Forms 앱에 제공할 수 있습니다.
seo-description: 애플리케이션 아이콘, 애플리케이션 이름, 실행 이미지 및 로그인 페이지를 사용자 정의하여 별도의 조직별 모양과 느낌을 AEM Forms 앱에 제공할 수 있습니다.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 1%

---


# 브랜딩 사용자 지정 {#branding-customization}

애플리케이션 아이콘, 응용 프로그램 이름, 실행 이미지 및 로그인 페이지를 사용자 지정하여 AEM Forms 앱에 고유한 조직별 모양을 제공할 수 있습니다. 예를 들어 조직에서 로고를 사용하도록 이미지를 변경할 수 있습니다. AEM Forms 앱은 다음과 같은 사용자 지정을 지원합니다.

* 애플리케이션 아이콘 및 실행 이미지 사용자 정의
* 앱 이름 맞춤화
* 로그인 페이지에서 이미지 사용자 정의
* 앱 메뉴에서 로고 사용자 정의

## 아이콘 사용자 정의 및 시작 이미지 {#customizing-icon-and-launch-images}

기본 앱 아이콘과 AEM Forms 앱의 실행 이미지를 사용자 지정하려면 다음 단계를 수행하십시오.

>[!NOTE]
>
>모든 아이콘 및 이미지의 경우 비인터레이스된 PNG 형식을 사용하십시오.

### 아이콘을 사용자 정의하고 {#to-customize-icon-and-launch-images} 이미지를 시작하려면

#### iOS {#for-ios}의 경우

1. Xcode에서 `Capture.xcodeproj` 프로젝트를 엽니다.
1. (***사용자 정의 아이콘***) 캡처의 네비게이터 보기에서 **[!UICONTROL 캡처 > 지원 파일 > Capture-info.plist]**&#x200B;로 이동합니다. 아이콘 파일 옆의 드롭다운을 클릭합니다. 아이콘 파일(.png)의 이름을 지정하고 **[!UICONTROL 캡처 > 캡처 > 리소스 > 아이콘]**&#x200B;에서 파일을 업로드합니다. 현재 지원되는 대화 상자:29x29, 50x50, 58x58, 72x72, 100x100 및 144x144.
1. (***시작 이미지를 사용자 정의하는 경우***) 이미지의 파일 이름이 다음과 같은지 확인합니다.

   * 세로:`Default-Portrait~ipad.png` 및 `Default-Portrait@2x~ipad.png`
   * 가로:`Default-Landscape~ipad.png` 및 `Default-Landscape@2x~ipad.png`

   캡처 프로젝트에 업로드하여 프로젝트의 기존 파일을 대체합니다.

   >[!NOTE]
   >
   >이미지의 이름과 해상도가 프로젝트에서 바꾼 이미지와 일치하는지 확인합니다.

1. iOS 디바이스 또는 iOS 시뮬레이터에서 AEM Forms 앱을 빌드하고 실행합니다.

#### Android {#for-android}의 경우

1. 애플리케이션 아이콘 파일의 이름을 다음과 같이 지정합니다.

   `ic_launcher.png`

1. 다음 디렉토리에 해당 아이콘 파일을 배치합니다.

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >이미지의 이름과 해상도가 프로젝트에서 바꾼 이미지와 일치하는지 확인합니다.

1. AEM Forms 앱을 다시 빌드합니다.

### Windows {#for-windows}

1. 경로의 아이콘을 바꿉니다.

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. 경로에서 시작 관리자 이미지를 교체합니다.

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >이미지의 이름과 해상도가 프로젝트에서 바꾼 이미지와 일치하는지 확인합니다.

1. AEM Forms 앱을 다시 빌드합니다.

## 앱 이름 {#customize-the-app-name} 사용자 지정

### iOS {#for-ios-1}의 경우

1. Xcode에서 `Capture.xcodeproj` 프로젝트를 엽니다.
1. Capture의 탐색기 보기에서 **[!UICONTROL 캡처 > 캡처 > 지원 파일 > InfoPlist.strings]**&#x200B;로 이동합니다.

   `CFBundleDisplayName` 속성의 값을 앱에 표시할 이름으로 업데이트합니다.

1. iOS 디바이스 또는 iOS 시뮬레이터에서 AEM Forms 앱을 빌드하고 실행합니다.

   iOS용 앱 빌드에 대한 자세한 내용은 [Xcode 프로젝트 설정 및 iOS 앱](/help/forms/using/setup-xcode-project-build-installer.md)을 참조하십시오.

### Android {#for-android-1}의 경우

1. 텍스트 또는 Xml 편집기에서 다음 Xml을 엽니다.

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. `app_name` 키에 대한 값을 업데이트합니다.
1. AEM Forms 앱을 다시 빌드합니다.

   Android용 앱 빌드에 대한 자세한 내용은 [Eclipse 프로젝트 설정 및 Android 앱](/help/forms/using/setup-eclipse-project-build-installer.md) 빌드를 참조하십시오.

### Windows {#for-windows-1}

1. 텍스트 편집기에서 다음 Xml을 엽니다.

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. `<name>...</name>` 태그의 값을 업데이트합니다.
1. AEM Forms 앱을 다시 빌드합니다.

   Windows용 앱 빌드에 대한 자세한 내용은 [Visual Studio 프로젝트 설정 및 Windows 앱](/help/forms/using/setup-visual-studio-project-build-installer.md) 빌드를 참조하십시오.

## 로그인 페이지 {#customizing-images-on-the-login-page}의 이미지 사용자 정의

AEM Forms 앱의 로그인 페이지에는 로고와 배경 이미지가 있습니다. 로고는 로그인 대화 상자 위에 있으며 배경 이미지는 로그인 대화 상자 아래에 있습니다. 로그인 페이지에서 기본 이미지를 사용자 정의하려면 다음 단계를 수행합니다.

**시작하기 전에**

다음 이미지가 있는지 확인합니다.

<table>
 <tbody>
  <tr>
   <th><p>설명</p> </th>
   <th><p>크기</p> </th>
   <th><p>파일 이름</p> </th>
  </tr>
  <tr>
   <td><p>로고</p> </td>
   <td><p>72 x 72픽셀</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>배경 이미지(세로)</p> </td>
   <td><p>1280 x 989픽셀</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**Xcode를 사용하여 로그인 페이지의 이미지를 사용자 정의하려면**

1. Xcode에서 `Capture.xcodeproj` 프로젝트를 엽니다.

1. `www/wsmobile/images`폴더로 이동합니다.
1. 로고를 변경하려면 기본 `LC-logo.png` 파일을 사용자 지정 `LC-logo.png` 파일로 바꾸십시오.
1. 배경을 변경하려면 기본 `Landing_bg.jpeg` 파일을 사용자 지정 `Landing_bg.jpeg` 파일로 바꾸십시오.
1. iOS 디바이스 또는 iOS 시뮬레이터에서 AEM Forms 앱을 빌드하고 실행합니다.

### Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}을(를) 사용하여 로그인 페이지의 이미지를 사용자 정의하려면

1. Eclipse에서 Android 프로젝트를 엽니다.

1. `assets/www/wsmobile/images`폴더로 이동합니다.
1. 로고를 변경하려면 기본 `LC-logo.png` 파일을 사용자 지정 `LC-logo.png` 파일로 바꾸십시오.
1. 배경을 변경하려면 기본 `Landing_bg.jpeg` 파일을 사용자 지정 `Landing_bg.jpeg` 파일로 바꾸십시오.
1. Android 디바이스에서 AEM Forms 앱을 빌드하고 실행합니다.

### Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}을 사용하여 로그인 페이지의 이미지를 사용자 지정하려면

1. Visual Studio에서 `MWSWindows.sln` 프로젝트를 엽니다.

1. `MWSWindows\www\wsmobile\images`폴더로 이동합니다.
1. 로고를 변경하려면 기본 `LC-logo.png` 파일을 사용자 지정 `LC-logo.png` 파일로 바꾸십시오.
1. 배경을 변경하려면 기본 `Landing_bg.jpeg` 파일을 사용자 지정 `Landing_bg.jpeg` 파일로 바꾸십시오.
1. Windows 디바이스에서 AEM Forms 앱을 빌드하고 실행합니다.

## 앱 메뉴 {#customizing_images_on_the_login_page-1}에서 로고 사용자 지정

AEM Forms 앱에 로그인하고 메뉴 단추를 누르면 메뉴 위에 로고가 표시됩니다. 기본 로고를 사용자 정의하려면 다음 단계를 수행하십시오.

**시작하기 전에**

다음 이미지가 있는지 확인합니다.

<table>
 <tbody>
  <tr>
   <th><p>설명</p> </th>
   <th><p>크기</p> </th>
   <th><p>파일 이름</p> </th>
  </tr>
  <tr>
   <td><p>로고</p> </td>
   <td><p>72 x 72픽셀</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**Xcode를 사용하여 로그인 페이지의 이미지를 사용자 정의하려면**

1. Xcode에서 `Capture.xcodeproj` 프로젝트를 엽니다.

1. `www/wsmobile/images`폴더로 이동합니다.
1. 로고를 변경하려면 기본 `aem_icon.png` 파일을 사용자 지정 `aem_icon.png` 파일로 바꾸십시오.
1. iOS 디바이스 또는 iOS 시뮬레이터에서 AEM Forms 앱을 빌드하고 실행합니다.

### Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}을(를) 사용하여 로그인 페이지의 이미지를 사용자 정의하려면

1. Eclipse에서 Android 프로젝트를 엽니다.

1. `assets/www/wsmobile/images`폴더로 이동합니다.
1. 로고를 변경하려면 기본 `aem_icon.png` 파일을 사용자 지정 `aem_icon.png` 파일로 바꾸십시오.
1. Android 디바이스에서 AEM Forms 앱을 빌드하고 실행합니다.

### Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}을 사용하여 로그인 페이지의 이미지를 사용자 지정하려면

1. Visual Studio에서 `MWSWindows.sln` 프로젝트를 엽니다.

1. `MWSWindows\www\wsmobile\images`폴더로 이동합니다.
1. 로고를 변경하려면 기본 `aem_icon.png` 파일을 사용자 지정 `aem_icon.png` 파일로 바꾸십시오.
1. Windows 디바이스에서 AEM Forms 앱을 빌드하고 실행합니다.
