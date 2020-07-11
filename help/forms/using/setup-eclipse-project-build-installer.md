---
title: AEM Forms Android 앱 빌드
seo-title: AEM Forms Android 앱 빌드
description: Android용 Android Studio 프로젝트를 설정하고 Android용 AEM Forms 응용 프로그램용 .apk 파일을 빌드하는 절차
seo-description: Android용 Android Studio 프로젝트를 설정하고 Android용 AEM Forms 응용 프로그램용 .apk 파일을 빌드하는 절차
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 3%

---


# AEM Forms Android 앱 빌드 {#build-the-aem-forms-android-app}

AEM Forms용 Android 앱을 빌드하려면 권장 시퀀스에서 다음 단계를 수행하십시오.

1. [AEM Forms 앱 소스 코드 패키지 다운로드](#download-android-zip)
1. [환경 변수 설정](#set-environment-variable-android)
1. [표준 AEM Forms 앱 빌드](#set-up-the-xcode-project)

## AEM Forms 앱 소스 코드 패키지 다운로드 {#download-android-zip}

AEM Forms 앱 소스 코드 패키지가 아카이브를 `adobe-lc-mobileworkspace-src-<version>.zip` 참조합니다. 이 아카이브는 사용자 정의 AEM Forms 앱을 빌드하는 데 필요한 소스 코드를 포함합니다. 아카이브는 소프트웨어 배포에서 사용할 수 있는 `adobe-aemfd-forms-app-src-pkg-<version>.zip`패키지에 포함되어 있습니다.

다음 단계를 수행하여 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 파일을 다운로드합니다.

1. 오픈 [소프트웨어 배포](https://experience.adobe.com/downloads). 소프트웨어 배포에 로그인하려면 Adobe ID이 필요합니다.
1. 헤더 메뉴에서 **[!UICONTROL 사용 가능한 Adobe Experience Manager]** 를 누릅니다.
1. 필터 **[!UICONTROL 섹션]** :
   1. **[!UICONTROL 솔루션]** **** 드롭다운 목록에서 양식을선택합니다.
   2. 패키지의 버전과 유형을 선택합니다. 다운로드 **[!UICONTROL 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
1. 운영 체제에 해당하는 패키지 이름을 누르고 EULA 약관 **[!UICONTROL 승인을 선택한]**&#x200B;다음 **[!UICONTROL 다운로드를 누릅니다]**.
1. [패키지 관리자](https://docs.adobe.com/content/help/ko-KR/experience-manager-65/administering/contentmanagement/package-manager.html)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.
1. 소스 코드 아카이브를 다운로드하려면 브라우저에서 **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip을** 엽니다. Android 앱 .zip 파일이 장치에 다운로드됩니다.
1. 로컬 파일 시스템의 폴더에 .zip 파일의 내용을 추출합니다. 예: *C:\&lt;폴더 구조>\adobe-lc-mobileworkspace-src-2.4.20*

다음 이미지는 `adobe-lc-mobileworkspace-src-<version>.zip\android`폴더 구조를 표시합니다.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 환경 변수 설정 {#set-environment-variable-android}

AEM Forms 앱에 대한 빌드 프로세스를 시작하기 전에 다음 환경 변수를 설정합니다.

* JAVA_HOME 환경 변수를 로컬 파일 시스템의 JDK 소프트웨어 위치로 설정합니다. 예: C:\Program Files\Java\jdk1.8.0_181
* Android용 SDK 위치에 `ANDROID_SDK_ROOT` 시스템 환경 변수를 설정합니다. 예: C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Android용 플랫폼 도구 및 도구 폴더 위치를 포함하도록 `Path` 시스템 환경 변수를 설정합니다. 예: C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## 표준 AEM Forms 앱 빌드 {#set-up-the-xcode-project}

로컬 파일 시스템에 adobe-lc-mobileworkspace-src-&lt;버전>.zip 파일을 저장하고 환경 변수를 설정한 후에는 다음 옵션을 사용하여 표준 AEM Forms Android 앱을 빌드합니다.

* [Android Studio를 사용하여 AEM Forms 앱 빌드](#using-android-studio)
* [Android Studio를 사용하여 .apk 파일 생성](#generate-apk-android-studio)

### Android Studio를 사용하여 AEM Forms 앱 빌드 {#using-android-studio}

Android Studio를 사용하여 AEM Forms 앱을 빌드하려면 다음 단계를 수행하십시오.

1. 컴퓨터에서 Android Studio 응용 프로그램을 실행합니다.
1. 기존 **Android Studio 프로젝트 열기를 클릭합니다**. 기존 프로젝트를 여는 대화 상자가 자동으로 표시되지 않으면 **파일** > **열기를 선택합니다**.
1. 로컬 파일 시스템에서 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* 로 이동하고 확인을 **클릭합니다**.

   왼쪽 창에 **android** 옵션이 표시됩니다.

   ![android_folder_studio](assets/android_folder_studio.png)

1. 왼쪽 창에서 **android** 를 선택하고 **실행** > **&#39;android**&#x200B;실행&#39;을 클릭합니다.
1. [배포 Target 선택] 대화 상자의 [연결된 장치] 섹션에서 Android 장치를 선택하고 [확인]을 클릭합니다.

   개발 환경을 성공적으로 구축한 후에는 이제 앱에서 사용자 지정을 적용할 수 있습니다. 다음 아티클을 사용하여 앱을 사용자 정의합니다.

   * [브랜딩 사용자 지정](/help/forms/using/branding-customization.md)
   * [테마 맞춤화](/help/forms/using/theme-customization.md)
   * [제스처 사용자 지정](/help/forms/using/gesture-customization.md)

   앱에 적절한 사용자 지정을 적용한 후 배포할 .apk 파일을 생성할 수 있습니다.

### Android Studio를 사용하여 .apk 파일 생성 {#generate-apk-android-studio}

Android Studio를 사용하여 .apk 파일을 생성하려면 다음 단계를 수행하십시오.

1. 컴퓨터에서 Android Studio 응용 프로그램을 실행합니다.
1. 기존 **Android Studio 프로젝트 열기를 선택합니다**. 기존 프로젝트를 여는 대화 상자가 자동으로 표시되지 않으면 **파일** > **열기를 선택합니다**.
1. 로컬 파일 시스템에서 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* 로 이동하고 확인을 **클릭합니다**.

   android 옵션은 왼쪽 창에 표시됩니다.

1. [ **빌드** ] > **APK** 빌드를 선택하여 .apk 파일을 생성합니다.

   필요에 따라 **빌드****>** 서명된 APK [생성을 선택하여](https://developer.android.com/studio/publish/app-signing) 서명된 버전의.apk 파일을 생성합니다.

## Android Debug Bridge 사용 {#build-android-debug-bridge}

.apk 파일이 생성되면 다음 명령을 실행하여 [Android Debug Bridge를 사용하여 Android 장치에 응용 프로그램을 설치합니다](https://developer.android.com/tools/help/adb.html).

**Windows 사용자:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**MAC 사용자:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
