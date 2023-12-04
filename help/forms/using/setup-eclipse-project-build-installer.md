---
title: AEM Forms Android 앱 빌드
description: Android Studio 프로젝트를 설정하고 Android용 AEM Forms 앱용 .apk 파일을 빌드하는 절차
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 3%

---

# AEM Forms Android 앱 빌드 {#build-the-aem-forms-android-app}

AEM Forms용 Android 앱을 빌드하려면 권장 시퀀스에서 다음 단계를 수행하십시오.

1. [AEM Forms 앱 소스 코드 패키지 다운로드](#download-android-zip)
1. [환경 변수 설정](#set-environment-variable-android)
1. [표준 AEM Forms 앱 빌드](#set-up-the-xcode-project)

## AEM Forms 앱 소스 코드 패키지 다운로드 {#download-android-zip}

AEM Forms 앱 소스 코드 패키지는 `adobe-lc-mobileworkspace-src-<version>.zip` 보관. 이 아카이브에는 사용자 지정 AEM Forms 앱을 빌드하는 데 필요한 소스 코드가 포함되어 있습니다. 아카이브는 `adobe-aemfd-forms-app-src-pkg-<version>.zip`소프트웨어 배포에서 사용할 수 있는 패키지.

다운로드하려면 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 파일에서 다음 단계를 수행합니다.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 선택 **[!UICONTROL Adobe Experience Manager]** 헤더 메뉴에서 사용할 수 있습니다.
1. 다음에서 **[!UICONTROL 필터]** 섹션:
   1. 선택 **[!UICONTROL Forms]** 다음에서 **[!UICONTROL 솔루션]** 드롭다운 목록입니다.
   2. 패키지의 버전 및 유형을 선택합니다. 다음을 사용할 수도 있습니다 **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**, 및 선택 **[!UICONTROL 다운로드]**.
1. 열기 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  및 클릭 **[!UICONTROL 패키지 업로드]** 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.
1. 소스 코드 아카이브를 다운로드하려면 를 엽니다. **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** 을 클릭합니다. Android 앱 .zip 파일이 장치에 다운로드됩니다.
1. 로컬 파일 시스템의 폴더에 .zip 파일의 압축을 풉니다. 예를 들어, *C:\&lt;folder structure=&quot;&quot;>\adobe-lc-mobileworkspace-src-2.4.20*

다음 이미지는 의 구조를 표시합니다. `adobe-lc-mobileworkspace-src-<version>.zip\android`폴더를 삭제합니다.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 환경 변수 설정 {#set-environment-variable-android}

AEM Forms 앱에 대한 빌드 프로세스를 시작하기 전에 다음 환경 변수를 설정하십시오.

* JAVA_HOME 환경 변수를 로컬 파일 시스템에서 JDK 소프트웨어 위치로 설정합니다. 예: C:\Program Files\Java\jdk1.8.0_181
* 설정 `ANDROID_SDK_ROOT` 시스템 환경 변수를 Android의 SDK 위치에 추가합니다. 예: C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* 설정 `Path` android용 platform-tools 및 tools 폴더 위치를 포함하는 시스템 환경 변수입니다. 예: C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools 및 C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## 표준 AEM Forms 앱 빌드 {#set-up-the-xcode-project}

adobe-lc-mobileworkspace-src를 저장한 후&lt;version>로컬 파일 시스템에서 .zip 파일을 사용하고 환경 변수를 설정하면 다음 옵션 중 하나를 사용하여 표준 AEM Forms Android 앱을 빌드합니다.

* [Android Studio를 사용하여 AEM Forms 앱 빌드](#using-android-studio)
* [Android Studio를 사용하여 .apk 파일 생성](#generate-apk-android-studio)

### Android Studio를 사용하여 AEM Forms 앱 빌드 {#using-android-studio}

Android Studio를 사용하여 AEM Forms 앱을 빌드하려면 다음 단계를 수행하십시오.

1. 컴퓨터에서 Android Studio 애플리케이션을 실행합니다.
1. 클릭 **기존 Android Studio 프로젝트 열기**. 기존 프로젝트를 여는 대화 상자가 자동으로 나타나지 않으면 **파일** > **열기**.
1. 다음으로 이동 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* 로컬 파일 시스템에서 을 클릭하고 **확인**.

   다음 **android** 옵션이 왼쪽 창에 표시됩니다.

   ![android_folder_studio](assets/android_folder_studio.png)

1. 선택 **android** 왼쪽 창에서 **실행** > **&#39;android&#39; 실행**.
1. 배포 대상 선택 대화 상자의 연결된 장치 섹션에서 Android 장치를 선택하고 확인을 클릭합니다.

   개발 환경을 성공적으로 빌드하면 이제 앱에 사용자 지정을 적용할 수 있습니다. 다음 문서를 사용하여 앱을 사용자 지정합니다.

   * [브랜딩 사용자 지정](/help/forms/using/branding-customization.md)
   * [테마 맞춤화](/help/forms/using/theme-customization.md)
   * [제스처 사용자 지정](/help/forms/using/gesture-customization.md)

   앱에 적절한 사용자 지정을 적용한 후 배포할 .apk 파일을 생성할 수 있습니다.

### Android Studio를 사용하여 .apk 파일 생성 {#generate-apk-android-studio}

Android Studio를 사용하여 .apk 파일을 생성하려면 다음을 수행합니다.

1. 컴퓨터에서 Android Studio 애플리케이션을 실행합니다.
1. 선택 **기존 Android Studio 프로젝트 열기**. 기존 프로젝트를 여는 대화 상자가 자동으로 나타나지 않으면 **파일** > **열기**.
1. 다음으로 이동 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* 로컬 파일 시스템에서 을 클릭하고 **확인**.

   왼쪽 창에 android 옵션이 표시됩니다.

1. .apk 파일을 생성하려면 다음을 선택합니다. **빌드** > **APK 작성**.

   선택 사항으로 다음을 선택합니다. **빌드** > **서명된 APK 생성** 생성 방법 [서명된 버전](https://developer.android.com/studio/publish/app-signing) .apk 파일

## Android Debug Bridge 사용 {#build-android-debug-bridge}

.apk 파일이 생성되면 다음 명령을 실행하여 를 사용하여 Android 디바이스에 애플리케이션을 설치합니다. [Android 디버그 브리지](https://developer.android.com/tools/adb).

**Windows 사용자:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Mac 사용자:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
