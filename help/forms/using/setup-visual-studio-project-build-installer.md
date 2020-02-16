---
title: Visual Studio 프로젝트 설정 및 Windows 앱 빌드
seo-title: Visual Studio 프로젝트 설정 및 Windows 앱 빌드
description: Visual Studio 프로젝트를 설정하여 AEM Forms Windows 모바일 장치 앱을 빌드하는 방법을 알아봅니다.
seo-description: Visual Studio 프로젝트를 설정하여 AEM Forms Windows 모바일 장치 앱을 빌드하는 방법을 알아봅니다.
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Visual Studio 프로젝트 설정 및 Windows 앱 빌드{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms는 AEM Forms 앱의 전체 소스 코드를 제공합니다. 소스에는 사용자 정의 작업 영역 응용 프로그램을 빌드하는 모든 구성 요소가 포함되어 있습니다. 소스 코드 아카이브는 `adobe-lc-mobileworkspace-src-<version>.zip`패키지 공유에서 패키지의 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 일부입니다.

AEM Forms 앱 소스를 가져오려면 다음 단계를 수행하십시오.

1. 패키지 공유 탐색\
   URL: `https://<server>:<port>/crx/packageshare`.

1. 소스 패키지를 다운로드합니다. 패키지를 다운로드하면 AEM Forms 패키지 관리자에 추가됩니다.
1. 다운로드가 완료되면 다음 위치로 이동합니다.를 `https://<server>:<port>/crx/packmgr/index.jsp`설치하고 설치합니다 `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. 소스 코드 아카이브를 다운로드하려면 브라우저에서 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 엽니다.\
   소스 패키지가 장치에 다운로드됩니다.

다음 이미지는 추출된 파일의 내용을 표시합니다 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

다음 이미지는 폴더에 있는 `windows` 폴더의 디렉토리 구조를 `src` 표시합니다.

![win-dir](assets/win-dir.png)

## 환경 설정 {#setting-up-the-environment}

Windows 장치의 경우 다음을 필요로 합니다.

* Microsoft Windows 8.1 또는 Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools for Apache Cordova

## AEM Forms용 Visual Studio 프로젝트 설정 앱 {#setting-up-visual-studio-project-for-aem-forms-app}

Visual Studio에서 AEM Forms 앱 프로젝트를 설정하려면 다음 단계를 수행하십시오.

1. Visual Studio 2015가 설치 및 구성된 Windows 8.1 또는 Windows 10 장치의 `adobe-lc-mobileworkspace-src-<version>.zip` `%HOMEPATH%\Projects` 폴더에 아카이브를 복사합니다.
1. 디렉토리에서 아카이브를 `%HOMEPATH%\Projects\MobileWorkspace` 추출합니다.
1. 디렉토리로 `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` 이동합니다.
1. Visual Studio 2015를 사용하여 `CordovaApp.sln` 파일을 열고 AEM Forms 앱을 빌드합니다.

## AEM Forms 앱 빌드 {#build-aem-forms-app}

AEM Forms 앱을 빌드하고 배포하려면 다음 단계를 수행하십시오.

>[!NOTE]
>
>AEM Forms 앱용 Windows 파일 시스템에 저장된 데이터가 암호화되지 않습니다. Windows BitLocker 드라이브 암호화와 같은 타사 도구를 사용하여 디스크 데이터를 암호화하는 것이 좋습니다.

1. Visual Studio Standard 도구 모음의 **빌드** 모드에 대해 드롭다운에서 릴리스를 선택합니다.

1. 플랫폼에 따라 Windows-AnyCPU, Windows-x64 또는 Windows-x86을 선택합니다. Windows-AnyCPU가 권장됩니다.
1. Visual Studio 솔루션 탐색기에서 CordovaApp.Windows 프로젝트를 마우스 오른쪽 단추로 클릭하고 **스토어** > **AppPackages 만들기를 선택합니다**.

   ![createapppackages](assets/createapppackages.png)

   앱 패키지 만들기 마법사가 나타납니다.

   CordovaApp.Windows_3.0.2.0_anycpu.appx 설치 프로그램 파일은 platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test 디렉토리에 만들어집니다.

   오류가 발생하면 오류를 마우스 오른쪽 단추로 `Retarget to windows 8.1 required`클릭하고 팝업 메뉴에서 [Windows 8.1로 **다시 타깃팅]을 선택합니다**.

   ![retarget 솔루션](assets/retarget-solution.png)

1. 앱 패키지 만들기 마법사에서 앱을 Windows Store에 업로드할지 여부를 선택한 다음 다음을 **클릭합니다**.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 필요에 따라 앱 빌드의 버전 및 출력 위치와 같은 매개 변수를 변경합니다.

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 프로젝트가 빌드되면 다음을 사용하여 앱을 설치할 수 있습니다.

   * Windows PowerShell
   * Visual Studio
   패키지를 설치하려면 다음 항목이 `.appx` 필요합니다.

   1. WinJS 라이브러리
   1. 패키지에 자체 서명된 인증서 또는 VeriSign과 같은 신뢰할 수 있는 인증 기관이 서명한 공개 인증서가 포함되어 있는지 확인합니다.
   1. 개발자 라이선스
   Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test 디렉토리에는 다음 네 가지 기본 구성 요소가 포함되어 있습니다.

   1. `.appx` 파일
   1. 인증서(현재 Apache Cordova의 자체 서명 인증서임)
   1. 종속성 폴더
   1. PowerShell 파일(.ps1 확장)



## Windows PowerShell을 사용하여 앱 배포 {#deploying-an-app-using-windows-powershell}

Windows 장치에 응용 프로그램을 설치하는 방법은 두 가지가 있습니다.

### 개발자 라이선스 취득 {#by-acquiring-the-developer-license}

1. PowerShell 파일()을 마우스 오른쪽 버튼으로 클릭하고 PowerShell을 사용하여 `Add-AppDevPackage.ps1)`실행을 선택합니다 ****.

1. 개발자 라이선스를 가져오라는 메시지가 표시됩니다. Microsoft 계정 자격 증명을 사용하여 개발자 라이선스를 획득합니다.\
   이 라이선스는 30일간 유효하며 무료로 갱신할 수 있습니다.
1. 개발자 라이센스를 취득하면 설치 프로그램은 자체 서명된 인증서를 시스템에 설치하고 응용 프로그램을 설치합니다.

### 기업 소유 디바이스 사용 {#by-using-enterprise-owned-devices}

기업의 도메인에 가입되어 있는 기업 소유의 장치의 경우 개발자 라이선스를 취득할 필요가 없습니다.

기업 소유 디바이스는 Professional 및 Enterprise 에디션의 Windows를 사용합니다.

Microsoft에서는 VeriSign과 같은 신뢰할 수 있는 기관에서 발급한 공용 인증서를 설치할 것을 권장합니다.

앱을 배포하려면:

* 장치가 기업 도메인에 가입되어 있는지 확인합니다.
* 그룹 정책 설정을 활성화합니다.

**그룹 정책 설정을 활성화하려면:**

1. 디바이스에서 실행합니다. `gpedit.msc`
1. 컴퓨터 구성 **> 관리 템플릿 > Windows 구성 요소 > 앱 패키지 배포로 이동합니다**.
1. Allow all trusted apps **to install**.
1. 편집을 **클릭하고** 활성화를 **선택합니다**.

1. **확인**&#x200B;을 클릭합니다.

Visual Studio에서 생성한 PowerShell 스크립트를 편집하여 개발자 라이센스를 획득하지 못하도록 합니다.

PowerShell 스크립트에서 변수를 설정합니다. `$NeedDeveloperLicense = $false`Adobe

도메인에 가입되지 않은 장치의 경우 보조 로딩 제품 활성화 키가 필요합니다. Windows 리셀러를 통해 구매할 수 있습니다.

Windows 8.1 Home Edition의 경우 그룹 정책이 없으며, 기업 내부 로딩이 허용되지 않으며, 엔터프라이즈 도메인과 연결할 수 없습니다. 개발자 라이선스를 사용하여 Windows 8.1 Home Edition 장치에 앱을 배포합니다.

자세한 내용을 보려면 [여기를](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)클릭하십시오.

## Visual Studio를 사용하여 앱 배포 {#deploying-an-app-using-visual-studio}

Visual Studio를 사용하여 Windows에 앱을 설치하려면:

1. 원격 디버거를 사용하여 장치를 연결합니다.\
   자세한 내용은 [원격 컴퓨터에서](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)Windows Store 앱 실행을 참조하십시오.

1. Visual Studio에서 응용 프로그램을 열고 [솔루션 플랫폼] 목록에서 Windows-x64, Windows-x86 또는 Windows-AnyCPU를 선택하고 [원격 컴퓨터] **를 선택합니다**.
1. 앱이 원격 컴퓨터에 배포됩니다.

