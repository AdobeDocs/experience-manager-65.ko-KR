---
title: Android&trade; studio 프로젝트를 설정하고 Android&trade; 앱을 빌드합니다.
description: Android&trade; Studio 프로젝트를 설정하고 Adobe Experience Manager(AEM) Forms 앱용 설치 관리자를 빌드하는 절차
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 3%

---

# Android™ studio 프로젝트 설정 및 Android™ 앱 빌드 {#set-up-the-android-studio-project-and-build-the-android-app}

이 문서는 AEM Forms 앱 6.3.1.1 이상 버전을 빌드하기 위한 것입니다. AEM Forms 앱 6.3의 소스 코드에서 앱을 빌드하려면 다음을 참조하십시오. [Eclipse 프로젝트 설정 및 Android™ 앱 빌드](/help/forms/using/setup-eclipse-project-build-installer.md).

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

다음 이미지는 추출된 내용을 표시합니다. `adobe-lc-mobileworkspace-src-<version>.zip`.

![압축 된 Android™ 소스의 추출된 콘텐츠](assets/mws-content-1.png)

다음 이미지는 의 디렉토리 구조를 표시합니다. `android`폴더의 폴더 `src`폴더를 삭제합니다.

![src에 있는 android 폴더의 디렉터리 구조](assets/android-folder.png)

## 표준 AEM Forms 앱 빌드 {#set-up-the-xcode-project}

1. Android™ Studio에서 프로젝트를 설정하고 서명 ID를 제공하려면 다음 단계를 수행하십시오.

   Android™ Studio가 설치 및 구성된 컴퓨터에 로그인합니다.

1. 다운로드한 항목 복사 `adobe-lc-mobileworkspace-src-<version>.zip` 보관 위치:

   **Mac 사용자용**: `[User_Home]/Projects`

   **Windows® 사용자용**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Windows®의 경우 Android™ 프로젝트를 시스템 드라이브에 보관하는 것이 좋습니다.

1. 다음 디렉토리에서 아카이브를 추출합니다.

   **Mac 사용자용**: `[User_Home]/Projects/[your-project]`

   **Windows® 사용자용**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   프로젝트를 Android™ Studio로 가져오기 전에 추출한 Android 프로젝트를 시스템 드라이브에 보관하는 것이 좋습니다.

1. Android™ Studio를 시작합니다.

   **Mac 사용자용**: 를 업데이트합니다 `local.properties` 에 있는 파일 `[User_Home]/Projects/[your-project]/android` 폴더 및 다음을 가리키기 `sdk.dir` 변수 대상 `SDK` 위치입니다.

   **Windows® 사용자용**: 를 업데이트합니다 `local.properties` 에 있는 파일 `%HOMEPATH%\Projects\[your-project]\android` 폴더 및 다음을 가리키기 `sdk.dir` 변수 대상 `SDK` 위치입니다.

1. 클릭 **[!UICONTROL 완료]** 프로젝트를 빌드합니다.

   프로젝트는 ADT 프로젝트 탐색기에서 사용할 수 있습니다.

   ![앱을 빌드한 후 eclipse 프로젝트](assets/eclipsebuildmws.png)

1. Android™ Studio에서 **[!UICONTROL 프로젝트 가져오기(Eclipse ADT, Gradle 등)]**.
1. 프로젝트 탐색기에서 빌드할 프로젝트의 루트 디렉터리를 선택합니다 **루트 디렉터리** 텍스트 상자:

   **Mac 사용자의 경우:** [User_Home]/프로젝트/모바일 작업 영역/src/android

   **Windows® 사용자의 경우:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 프로젝트를 가져오면 Android™ 플러그인 Gradle을 업데이트하는 옵션과 함께 팝업이 나타납니다. 요구 사항에 따라 적절한 버튼을 클릭합니다.

   ![이 프로젝트에 대한 dontremindmeagainforthis project](assets/dontremindmeagainforthisproject.png)

1. Gradle 빌드가 완료되면 다음 화면이 나타납니다. 적절한 장치 또는 에뮬레이터를 시스템에 연결하고 **[!UICONTROL Android™ 실행]**.

   ![그라들콩솔](assets/gradleconsole.png)

1. Android™ Studio는 연결된 장치 및 사용 가능한 에뮬레이터를 표시합니다. 응용 프로그램을 실행할 장치를 선택한 다음 **확인**.

   ![연결된 장치](assets/connecteddevice.png)

프로젝트를 빌드한 후에는 Android™ Debug Bridge 또는 Android™ Studio를 사용하여 앱을 설치하도록 선택할 수 있습니다.

### Android™ Debug Bridge 사용 {#andriod-debug-bridge}

다음을 통해 Android™ 장치에 애플리케이션을 설치할 수 있습니다. [Android™ 디버그 브리지](https://developer.android.com/tools/adb) 다음 명령을 사용하여 생성합니다.

**Mac 사용자용**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Windows® 사용자용**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
