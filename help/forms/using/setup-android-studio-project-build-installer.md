---
title: Android 스튜디오 프로젝트 설정 및 Android 앱 빌드
seo-title: Android 스튜디오 프로젝트 설정 및 Android 앱 빌드
description: Android Studio 프로젝트를 설정하고 AEM Forms 앱용 설치 프로그램을 빌드하는 절차
seo-description: Android Studio 프로젝트를 설정하고 AEM Forms 앱용 설치 프로그램을 빌드하는 절차
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Android 스튜디오 프로젝트 설정 및 Android 앱 빌드 {#set-up-the-android-studio-project-and-build-the-android-app}

이 문서는 AEM Forms 앱 6.3.1.1 이상 버전을 빌드하기 위한 것입니다. AEM Forms App 6.3의 소스 코드의 소스 코드에서 앱을 빌드하려면 Eclipse [프로젝트 설정 및 Android™ 앱](/help/forms/using/setup-eclipse-project-build-installer.md)빌드를 참조하십시오.

AEM Forms는 AEM Forms 앱의 전체 소스 코드를 제공합니다. 소스에는 사용자 정의 AEM Forms 앱을 빌드하는 모든 구성 요소가 포함되어 있습니다. 소스 코드 아카이브는 `adobe-lc-mobileworkspace-src-<version>.zip` 패키지 공유의 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 패키지의 일부입니다.

AEM Forms 앱 소스를 가져오려면 다음 단계를 수행하십시오.

1. 패키지 공유 탐색

   URL: `https://<server>:<port>/crx/packageshare`.

1. 소스 패키지를 다운로드합니다. 패키지를 다운로드하면 AEM Forms 패키지 관리자에 추가됩니다.
1. 다운로드가 완료되면 다음 위치로 이동합니다.를 `https://<server>:<port>/crx/packmgr/index.jsp`설치하고 설치합니다 `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. 소스 코드 아카이브를 다운로드하려면 브라우저에서 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 엽니다.

   소스 패키지가 장치에 다운로드됩니다.

다음 이미지는 추출된 파일의 내용을 표시합니다 `adobe-lc-mobileworkspace-src-<version>.zip`.

![압축을 푼 Android™ 소스의 컨텐츠](assets/mws-content-1.png)

다음 이미지는 `android`폴더에 있는 `src`폴더의 디렉토리 구조를 표시합니다.

![src의 android 폴더의 디렉토리 구조](assets/android-folder.png)

## 표준 AEM Forms 앱 빌드 {#set-up-the-xcode-project}

1. Android™ Studio에서 프로젝트를 설정하고 서명 ID를 제공하려면 다음 단계를 수행하십시오.

   Android™ Studio가 설치 및 구성된 컴퓨터에 로그인합니다.

1. 다운로드한 `adobe-lc-mobileworkspace-src-<version>.zip` 아카이브를 다음 위치에 복사합니다.

   **MAC 사용자의**&#x200B;경우: `[User_Home]/Projects`

   **Windows® 사용자의**&#x200B;경우: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Windows®의 경우 시스템 드라이브에 Android 프로젝트를 보관하는 것이 좋습니다.

1. 다음 디렉토리에서 아카이브를 추출합니다.

   **MAC 사용자의**&#x200B;경우: `[User_Home]/Projects/[your-project]`

   **Windows® 사용자의**&#x200B;경우: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >프로젝트를 Android Studio로 가져오기 전에 압축을 푼 Android 프로젝트를 시스템 드라이브에 보관하는 것이 좋습니다.

1. Android™ Studio를 실행합니다.

   **MAC 사용자의**&#x200B;경우:폴더에 있는 `local.properties` 파일을 `[User_Home]/Projects/[your-project]/android` 업데이트하고 `sdk.dir` 변수를 바탕 화면의 `SDK` 위치로 지정합니다.

   **Windows® 사용자의**&#x200B;경우:폴더에 있는 `local.properties` 파일을 `%HOMEPATH%\Projects\[your-project]\android` 업데이트하고 `sdk.dir` 변수를 바탕 화면의 `SDK` 위치로 지정합니다.

1. 마침을 **[!UICONTROL 클릭하여]** 프로젝트를 빌드합니다.

   이 프로젝트는 ADT 프로젝트 탐색기에서 사용할 수 있습니다.

   ![앱 빌드 후 eclipse 프로젝트](assets/eclipsebuildmws.png)

1. Android™ Studio에서 프로젝트 **[!UICONTROL 가져오기(Eclipse ADT, Gradle 등)]**&#x200B;를 선택합니다.
1. 프로젝트 탐색기에서 루트 디렉토리 텍스트 상자에서 빌드할 프로젝트의 루트 **디렉토리를** 선택합니다.

   **Mac 사용자의 경우:** User_ [Home]/Projects/MobileWorkspace/src/android

   **Windows® 사용자의 경우:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 프로젝트를 가져오면 Android™ 플러그인 그레이드를 업데이트하는 옵션이 있는 팝업이 표시됩니다. 요구 사항에 따라 적절한 단추를 클릭합니다.

   ![dontremindemaginvotherforge project](assets/dontremindmeagainforthisproject.png)

1. 성공적인 점진적 빌드가 완료되면 다음 화면이 나타납니다. 해당 장치 또는 에뮬레이터를 시스템과 연결하고 Android **[!UICONTROL ™]**&#x200B;실행을 클릭합니다.

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio는 연결된 장치와 사용 가능한 에뮬레이터를 표시합니다. 애플리케이션을 실행할 장치를 선택한 다음 확인을 **클릭합니다**.

   ![connecteddevice](assets/connecteddevice.png)

프로젝트를 빌드한 후 Android™ Debug Bridge 또는 Android™ Studio를 사용하여 앱을 설치하도록 선택할 수 있습니다.

### Android™ Debug Bridge 사용 {#andriod-debug-bridge}

다음 명령을 사용하여 Android™ Debug Bridge를 통해 Android™ [장치에](https://developer.android.com/tools/help/adb.html) 응용 프로그램을 설치할 수 있습니다.

**MAC 사용자의**&#x200B;경우: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Windows® 사용자의**&#x200B;경우: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
