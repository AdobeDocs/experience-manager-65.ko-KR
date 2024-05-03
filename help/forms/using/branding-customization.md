---
title: 브랜딩 사용자 지정
description: 애플리케이션 아이콘, 애플리케이션 이름, 실행 이미지 및 로그인 페이지를 사용자 정의하여 AEM Forms 앱에 고유한 조직별 모양과 느낌을 제공합니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 1%

---

# 브랜딩 사용자 지정 {#branding-customization}

애플리케이션 아이콘, 애플리케이션 이름, 론치 이미지 및 로그인 페이지를 사용자 정의하여 AEM Forms 앱에 고유한 조직별 모양을 제공할 수 있습니다. 예를 들어 조직의 로고를 사용하도록 이미지를 변경할 수 있습니다. AEM Forms 앱은 다음과 같은 사용자 지정을 지원합니다.

* 애플리케이션 아이콘 및 론치 이미지 맞춤화
* 앱 이름 사용자 지정
* 로그인 페이지에서 이미지 사용자 정의
* 앱 메뉴에서 로고 사용자 지정

## 아이콘 및 론치 이미지 맞춤화 {#customizing-icon-and-launch-images}

기본 앱 아이콘과 AEM Forms 앱의 시작 이미지를 사용자 정의하려면 다음 단계를 수행하십시오.

>[!NOTE]
>
>모든 아이콘과 이미지에 비인터레이스 PNG 형식을 사용합니다.

### 아이콘 및 론치 이미지를 사용자 정의하려면 {#to-customize-icon-and-launch-images}

#### iOS용 {#for-ios}

1. 를 엽니다. `Capture.xcodeproj` xcode의 프로젝트입니다.
1. (***사용자 지정 아이콘***) 캡처의 네비게이터 보기에서 다음 위치로 이동합니다. **[!UICONTROL 캡처 > 캡처 > 지원 파일 > Capture-info.plist]**. 아이콘 파일 옆에 있는 드롭다운을 클릭합니다. 아이콘 파일(.png)의 이름을 지정하고 다음 위치에 파일을 업로드합니다. **[!UICONTROL 캡처 > 캡처 > 리소스 > 아이콘]**. 현재 지원되는 차원은 29x29, 50x50, 58x58, 72x72, 100x100 및 144x144입니다.
1. (***Launch 이미지 사용자 정의용***) 이미지의 파일 이름이 다음과 같은지 확인합니다.

   * 세로: `Default-Portrait~ipad.png` 및 `Default-Portrait@2x~ipad.png`
   * 가로: `Default-Landscape~ipad.png` 및 `Default-Landscape@2x~ipad.png`

   Capture 프로젝트에 업로드하여 프로젝트의 기존 파일을 바꿉니다.

   >[!NOTE]
   >
   >이미지의 이름 및 해상도가 프로젝트에서 교체하는 이미지와 일치하는지 확인합니다.

1. iOS 장치 또는 iOS 시뮬레이터에서 AEM Forms 앱을 빌드하고 실행합니다.

#### Android용 {#for-android}

1. 애플리케이션 아이콘 파일의 이름을 다음과 같이 지정합니다.

   `ic_launcher.png`

1. 해당 아이콘 파일을 다음 디렉토리에 넣습니다.

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >이미지의 이름 및 해상도가 프로젝트에서 교체하는 이미지와 일치하는지 확인합니다.

1. AEM Forms 앱을 다시 빌드합니다.

### Windows용 {#for-windows}

1. 경로의 아이콘을 바꿉니다.

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. 경로의 런처 이미지를 바꿉니다.

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >이미지의 이름 및 해상도가 프로젝트에서 교체하는 이미지와 일치하는지 확인합니다.

1. AEM Forms 앱을 다시 빌드합니다.

## 앱 이름 사용자 지정 {#customize-the-app-name}

### iOS용 {#for-ios-1}

1. 를 엽니다. `Capture.xcodeproj` xcode의 프로젝트입니다.
1. 캡처의 네비게이터 보기에서 다음 위치로 이동합니다. **[!UICONTROL 캡처 > 캡처 > 지원 파일 > InfoPlist.strings]**.

   에 대한 값 업데이트 `CFBundleDisplayName` 앱에 표시할 이름의 속성입니다.

1. iOS 장치 또는 iOS 시뮬레이터에서 AEM Forms 앱을 빌드하고 실행합니다.

   iOS용 앱 빌드에 대한 자세한 내용은 [Xcode 프로젝트 설정 및 iOS 앱 빌드](/help/forms/using/setup-xcode-project-build-installer.md).

### Android용 {#for-android-1}

1. 텍스트 또는 Xml 편집기에서 다음 Xml을 엽니다.

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. 키 값 업데이트 `app_name`.
1. AEM Forms 앱을 다시 빌드합니다.

   Android용 앱 빌드에 대한 자세한 내용은 [Eclipse 프로젝트 설정 및 Android 앱 빌드](/help/forms/using/setup-eclipse-project-build-installer.md).

### Windows용 {#for-windows-1}

1. 텍스트 편집기에서 다음 Xml을 엽니다.

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. 에서 값 업데이트 `<name>...</name>` 태그에 가깝게 배치하십시오.
1. AEM Forms 앱을 다시 빌드합니다.

   Windows용 앱 빌드에 대한 자세한 내용은 [Visual Studio 프로젝트 설정 및 Windows 앱 빌드](/help/forms/using/setup-visual-studio-project-build-installer.md).

## 로그인 페이지에서 이미지 사용자 정의 {#customizing-images-on-the-login-page}

AEM Forms 앱의 로그인 페이지에는 로고와 배경 이미지가 있습니다. 로고는 로그인 대화 상자 위에 있고 배경 이미지는 로그인 대화 상자 아래에 있습니다. 로그인 페이지에서 기본 이미지를 사용자 정의하려면 다음 단계를 수행하십시오.

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

**Xcode를 사용하여 로그인 페이지에서 이미지를 사용자 지정하려면**

1. 를 엽니다. `Capture.xcodeproj` xcode의 프로젝트입니다.

1. 다음 위치로 이동 `www/wsmobile/images`폴더를 삭제합니다.
1. 로고를 변경하려면 기본값을 바꿉니다. `LC-logo.png` 사용자 지정 파일이 있는 파일 `LC-logo.png` 파일.
1. 배경을 변경하려면 기본값을 바꿉니다. `Landing_bg.jpeg` 사용자 지정 파일이 있는 파일 `Landing_bg.jpeg`파일.
1. iOS 장치 또는 iOS 시뮬레이터에서 AEM Forms 앱을 빌드하고 실행합니다.

### Eclipse를 사용하여 로그인 페이지에서 이미지 사용자 정의하기 {#to-customize-images-on-the-login-pages-using-eclipse}

1. Eclipse에서 Android 프로젝트를 엽니다.

1. 다음 위치로 이동 `assets/www/wsmobile/images`폴더를 삭제합니다.
1. 로고를 변경하려면 기본값을 바꿉니다. `LC-logo.png` 사용자 지정 파일이 있는 파일 `LC-logo.png` 파일.
1. 배경을 변경하려면 기본값을 바꿉니다. `Landing_bg.jpeg` 사용자 지정 파일이 있는 파일 `Landing_bg.jpeg`파일.
1. Android 장치에서 AEM Forms 앱을 빌드하고 실행합니다.

### Visual Studio를 사용하여 로그인 페이지의 이미지를 사용자 지정하려면 {#to-customize-images-on-the-login-pages-using-visual-studio}

1. 를 엽니다. `MWSWindows.sln` visual Studio의 프로젝트입니다.

1. 다음 위치로 이동 `MWSWindows\www\wsmobile\images`폴더를 삭제합니다.
1. 로고를 변경하려면 기본값을 바꿉니다. `LC-logo.png` 사용자 지정 파일이 있는 파일 `LC-logo.png` 파일.
1. 배경을 변경하려면 기본값을 바꿉니다. `Landing_bg.jpeg` 사용자 지정 파일이 있는 파일 `Landing_bg.jpeg`파일.
1. Windows 장치에서 AEM Forms 앱을 빌드하고 실행합니다.

## 앱 메뉴에서 로고 사용자 지정 {#customizing_images_on_the_login_page-1}

AEM Forms 앱에 로그인하고 메뉴 버튼을 선택하면 메뉴 위에 로고가 표시됩니다. 기본 로고를 사용자 지정하려면 다음 단계를 수행하십시오.

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

**Xcode를 사용하여 로그인 페이지에서 이미지를 사용자 지정하려면**

1. 를 엽니다. `Capture.xcodeproj` xcode의 프로젝트입니다.

1. 다음 위치로 이동 `www/wsmobile/images`폴더를 삭제합니다.
1. 로고를 변경하려면 기본값을 바꿉니다. `aem_icon.png` 사용자 지정 파일이 있는 파일 `aem_icon.png` 파일.
1. iOS 장치 또는 iOS 시뮬레이터에서 AEM Forms 앱을 빌드하고 실행합니다.

### Eclipse를 사용하여 로그인 페이지에서 이미지 사용자 정의하기 {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Eclipse에서 Android 프로젝트를 엽니다.

1. 다음 위치로 이동 `assets/www/wsmobile/images`폴더를 삭제합니다.
1. 로고를 변경하려면 기본값을 바꿉니다. `aem_icon.png` 사용자 지정 파일이 있는 파일 `aem_icon.png` 파일.
1. Android 장치에서 AEM Forms 앱을 빌드하고 실행합니다.

### Visual Studio를 사용하여 로그인 페이지의 이미지를 사용자 지정하려면 {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. 를 엽니다. `MWSWindows.sln` visual Studio의 프로젝트입니다.

1. 다음 위치로 이동 `MWSWindows\www\wsmobile\images`폴더를 삭제합니다.
1. 로고를 변경하려면 기본값을 바꿉니다. `aem_icon.png` 사용자 지정 파일이 있는 파일 `aem_icon.png` 파일.
1. Windows 장치에서 AEM Forms 앱을 빌드하고 실행합니다.
