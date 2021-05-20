---
title: Visual Studio 프로젝트를 설정하고 Windows 앱을 빌드합니다.
seo-title: Visual Studio 프로젝트를 설정하고 Windows 앱을 빌드합니다.
description: AEM Forms Windows 모바일 장치 앱을 빌드하기 위해 Visual Studio 프로젝트를 설정하는 방법을 알아봅니다.
seo-description: AEM Forms Windows 모바일 장치 앱을 빌드하기 위해 Visual Studio 프로젝트를 설정하는 방법을 알아봅니다.
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 6%

---

# Visual Studio 프로젝트를 설정하고 Windows 앱을 빌드합니다.{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms은 AEM Forms 앱의 전체 소스 코드를 제공합니다. 소스에는 사용자 정의 작업 공간 응용 프로그램을 만들기 위한 모든 구성 요소가 포함되어 있습니다. 소스 코드 아카이브 `adobe-lc-mobileworkspace-src-<version>.zip`는 소프트웨어 배포의 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 패키지의 일부입니다.

AEM Forms 앱 소스를 가져오려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에 제공된 **[!UICONTROL Adobe Experience Manager]**&#x200B;를 누릅니다.
1. **[!UICONTROL 필터]** 섹션에서 다음을 수행합니다.
   1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을 선택합니다.
   2. 패키지의 버전 및 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
1. 운영 체제에 해당하는 패키지 이름을 탭하고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 탭합니다.
1. [패키지 관리자](https://docs.adobe.com/content/help/ko-KR/experience-manager-65/administering/contentmanagement/package-manager.html)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. 소스 코드 아카이브를 다운로드하려면 브라우저에서 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 을 엽니다.\
   소스 패키지가 장치에서 다운로드됩니다.

다음 이미지는 추출된 `adobe-lc-mobileworkspace-src-<version>.zip` 내용을 표시합니다.

![mws-content-1](assets/mws-content-1.png)

다음 이미지는 `src` 폴더에 있는 `windows` 폴더의 디렉토리 구조를 표시합니다.

![win-dir](assets/win-dir.png)

## 환경 설정 {#setting-up-the-environment}

Windows 장치의 경우 다음을 수행해야 합니다.

* Microsoft Windows 8.1 또는 Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova용 Microsoft Visual Studio Tools

## AEM Forms용 Visual Studio 프로젝트 앱 설정 {#setting-up-visual-studio-project-for-aem-forms-app}

다음 단계를 수행하여 Visual Studio에서 AEM Forms 앱 프로젝트를 설정합니다.

1. Visual Studio 2015가 설치되어 구성된 Windows 8.1 또는 Windows 10 장치의 `%HOMEPATH%\Projects` 폴더에 `adobe-lc-mobileworkspace-src-<version>.zip` 아카이브를 복사합니다.
1. `%HOMEPATH%\Projects\MobileWorkspace` 디렉토리에서 아카이브를 추출합니다.
1. `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` 디렉토리로 이동합니다.
1. Visual Studio 2015를 사용하여 `CordovaApp.sln` 파일을 열고 AEM Forms 앱 빌드를 계속 진행합니다.

## AEM Forms 앱 빌드 {#build-aem-forms-app}

다음 단계를 수행하여 AEM Forms 앱을 빌드하고 배포합니다.

>[!NOTE]
>
>AEM Forms 앱용 Windows 파일 시스템에 저장된 데이터가 암호화되지 않습니다. Windows BitLocker 드라이브 암호화와 같은 타사 도구를 사용하여 디스크 데이터를 암호화하는 것이 좋습니다.

1. Visual Studio Standard 도구 모음의 빌드 모드에 대한 드롭다운에서 **릴리스**&#x200B;를 선택합니다.

1. 플랫폼에 따라 Windows-AnyCPU, Windows-x64 또는 Windows-x86을 선택합니다. Windows-AnyCPU가 권장됩니다.
1. Visual Studio 솔루션 탐색기에서 프로젝트 **CordovaApp.Windows**&#x200B;를 마우스 오른쪽 단추로 클릭하고 **스토어 > AppPackages 만들기**&#x200B;를 선택합니다.

   ![createapppackages](assets/createapppackages.png)

   앱 패키지 만들기 마법사가 나타납니다.

   CordovaApp.Windows_3.0.2.0_anycpu.appx 설치 프로그램 파일은 platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test 디렉터리에 만들어집니다.

   `Retarget to windows 8.1 required` 오류가 발생하면 오류를 마우스 오른쪽 단추로 클릭하고 팝업 메뉴에서 **Windows 8.1로 재타깃팅**&#x200B;을 선택합니다.

   ![재타겟팅 솔루션](assets/retarget-solution.png)

1. 앱 패키지 만들기 마법사에서 앱을 Windows 스토어에 업로드하지 않으려는 날씨를 선택한 다음 **다음**&#x200B;을 클릭합니다.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 필요에 따라 앱 빌드의 버전 및 출력 위치와 같은 매개 변수를 변경합니다.

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 프로젝트가 빌드되면 다음을 사용하여 앱을 설치할 수 있습니다.

   * Windows PowerShell
   * Visual Studio

   `.appx` 패키지를 설치하려면 다음 항목이 필요합니다.

   1. WinJS 라이브러리
   1. 패키지에 자체 서명된 인증서나 VeriSign과 같은 신뢰할 수 있는 인증 기관이 서명한 공개 인증서가 포함되어 있는지 확인합니다.
   1. 개발자 라이선스

   Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test 디렉토리에는 네 가지 기본 구성 요소가 있습니다.

   1. `.appx` 파일
   1. 인증서(현재 Apache Cordova에서 자체 서명된 인증서임)
   1. 종속성 폴더
   1. PowerShell 파일(.ps1 확장)



## Windows PowerShell {#deploying-an-app-using-windows-powershell}을 사용하여 앱 배포

Windows 장치에 응용 프로그램을 설치하는 방법에는 두 가지가 있습니다.

### 개발자 라이선스 {#by-acquiring-the-developer-license} 가져오기

1. PowerShell 파일( `Add-AppDevPackage.ps1)`)을 마우스 오른쪽 버튼으로 클릭하고 **Run with PowerShell**&#x200B;을 선택합니다.

1. 개발자 라이센스를 가져오라는 메시지가 표시됩니다. Microsoft 계정 자격 증명을 사용하여 개발자 라이선스를 얻습니다.\
   이 라이선스는 30일 동안 유효하며 무료로 갱신할 수 있습니다.
1. 개발자 라이센스를 취득하면 설치 프로그램이 시스템에 자체 서명된 인증서를 설치하고 응용 프로그램이 성공적으로 설치됩니다.

### 엔터프라이즈 소유 장치 {#by-using-enterprise-owned-devices} 사용

엔터프라이즈 도메인에 가입된 엔터프라이즈 소유 장치의 경우 개발자 라이선스를 가져올 필요가 없습니다.

엔터프라이즈 소유 장치는 Windows Professional 및 Enterprise Edition을 사용합니다.

VeriSign과 같은 신뢰할 수 있는 권한이 발급된 공개 인증서를 설치하는 것이 좋습니다.

앱을 배포하려면 다음을 수행하십시오.

* 장치가 엔터프라이즈 도메인에 가입되어 있는지 확인합니다.
* 그룹 정책 설정을 사용하도록 설정합니다.

**그룹 정책 설정을 사용하려면**

1. 장치에서 `gpedit.msc` 을 실행합니다.
1. **컴퓨터 구성 > 관리 템플릿 > Windows 구성 요소 > 앱 패키지 배포**&#x200B;로 이동합니다.
1. **신뢰할 수 있는 모든 앱이 설치되도록 마우스 오른쪽 단추를 클릭하십시오**.
1. **편집**&#x200B;을 클릭하고 **활성화됨**&#x200B;을 선택합니다.

1. **확인**&#x200B;을 클릭합니다.

Visual Studio에서 생성한 PowerShell 스크립트를 편집하여 개발자 라이선스를 가져오지 못하도록 합니다.

PowerShell 스크립트에서 변수를 설정합니다.`$NeedDeveloperLicense = $false`

도메인에 가입되지 않은 장치의 경우, 사이드 로딩 제품 활성화 키가 필요합니다. Windows 리셀러를 통해 구입할 수 있습니다.

Windows 8.1 Home Edition에는 그룹 정책이 없고 엔터프라이즈 측 로드가 허용되지 않으며 엔터프라이즈 도메인에 가입할 수 없습니다. 개발자 라이선스를 사용하여 Windows 8.1 Home Edition 장치에 앱을 배포합니다.

자세한 내용을 보려면 [여기](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)를 클릭하십시오.

## Visual Studio {#deploying-an-app-using-visual-studio}를 사용하여 앱 배포

Visual Studio를 사용하여 Windows에 앱을 설치하려면 다음을 수행하십시오.

1. 원격 디버거를 사용하여 장치를 연결합니다.\
   자세한 내용은 원격 컴퓨터에서 [Windows 스토어 앱 실행](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)을 참조하십시오.

1. Visual Studio에서 앱을 연 상태에서 솔루션 플랫폼 목록에서 Windows-x64, Windows-x86 또는 Windows-AnyCPU를 선택하고 **원격 컴퓨터**&#x200B;를 선택합니다.
1. 앱이 원격 컴퓨터에 배포됩니다.
