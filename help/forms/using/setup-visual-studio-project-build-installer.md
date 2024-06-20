---
title: Visual Studio 프로젝트 설정 및 Windows 앱 빌드
description: AEM Forms Windows 모바일 장치 앱을 빌드하도록 Visual Studio 프로젝트를 설정하는 방법에 대해 알아봅니다.
topic-tags: forms-app
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 2%

---

# Visual Studio 프로젝트 설정 및 Windows 앱 빌드{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms은 AEM Forms 앱의 전체 소스 코드를 제공합니다. 소스에는 사용자 지정 작업 영역 응용 프로그램을 빌드하기 위한 모든 구성 요소가 포함되어 있습니다. 소스 코드 아카이브, `adobe-lc-mobileworkspace-src-<version>.zip`의 일부임 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 소프트웨어 배포 패키지

AEM Forms 앱 소스를 가져오려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 선택 **[!UICONTROL Adobe Experience Manager]** 헤더 메뉴에서 사용할 수 있습니다.
1. 다음에서 **[!UICONTROL 필터]** 섹션:
   1. 선택 **[!UICONTROL Forms]** 다음에서 **[!UICONTROL 솔루션]** 드롭다운 목록입니다.
   2. 패키지의 버전 및 유형을 선택합니다. 다음을 사용할 수도 있습니다 **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**, 및 선택 **[!UICONTROL 다운로드]**.
1. 열기 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  및 클릭 **[!UICONTROL 패키지 업로드]** 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

1. 소스 코드 아카이브를 다운로드하려면 를 엽니다. `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 을 클릭합니다.\
   소스 패키지가 디바이스에 다운로드됩니다.

다음 이미지는 추출된 내용을 표시합니다. `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

다음 이미지는 의 디렉토리 구조를 표시합니다. `windows` 폴더의 폴더 `src` 폴더를 삭제합니다.

![win-dir](assets/win-dir.png)

## 환경 설정 {#setting-up-the-environment}

Windows 장치의 경우 다음이 필요합니다.

* Microsoft Windows 8.1 또는 Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools for Apache Cordova

## AEM Forms 앱용 Visual Studio 프로젝트 설정 {#setting-up-visual-studio-project-for-aem-forms-app}

Visual Studio에서 AEM Forms 앱 프로젝트를 설정하려면 다음 단계를 수행하십시오.

1. 다음을 복사합니다. `adobe-lc-mobileworkspace-src-<version>.zip` 보관 위치: `%HOMEPATH%\Projects` Visual Studio 2015가 설치 및 구성된 Windows 8.1 또는 Windows 10 장치의 폴더입니다.
1. 에서 아카이브 추출 `%HOMEPATH%\Projects\MobileWorkspace` 디렉토리.
1. 다음 위치로 이동 `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` 디렉토리.
1. 를 엽니다. `CordovaApp.sln` 파일을 Visual Studio 2015를 사용하여 만들고 AEM Forms 앱 빌드로 이동합니다.

## AEM Forms 앱 빌드 {#build-aem-forms-app}

AEM Forms 앱을 빌드하고 배포하려면 다음 단계를 수행하십시오.

>[!NOTE]
>
>AEM Forms 앱용 Windows 파일 시스템에 저장된 데이터는 암호화되지 않습니다. Windows BitLocker 드라이브 암호화와 같은 타사 도구를 사용하여 디스크 데이터를 암호화하는 것이 좋습니다.

1. Visual Studio Standard 도구 모음에서 **릴리스** 빌드 모드의 드롭다운에서

1. 플랫폼을 기반으로 Windows-AnyCPU, Windows-x64 또는 Windows-x86을 선택합니다. Windows-AnyCPU를 사용하는 것이 좋습니다.
1. Visual Studio 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다 **CordovaApp.Windows** 및 선택 **스토어 > 앱 패키지 만들기**.

   ![createapppackages](assets/createapppackages.png)

   앱 패키지 만들기 마법사가 나타납니다.

   CordovaApp.Windows_3.0.2.0_anycpu.appx 설치 관리자 파일은 platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test 디렉터리에 만들어집니다.

   오류가 발생하는 경우 `Retarget to windows 8.1 required`을 클릭하고 오류를 마우스 오른쪽 단추로 클릭한 다음 팝업 메뉴에서 **Windows 8.1로 리타겟팅**.

   ![리타겟 솔루션](assets/retarget-solution.png)

1. 앱 패키지 만들기 마법사에서 Windows 스토어에 앱을 업로드할 날씨 를 선택한 다음 을(를) 클릭합니다 **다음**.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 필요에 따라 앱 빌드의 버전 및 출력 위치와 같은 매개 변수를 변경합니다.

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 프로젝트가 빌드되면 다음을 사용하여 앱을 설치할 수 있습니다.

   * 윈도우 파워쉘
   * Visual Studio

   다음 `.appx` 패키지를 설치하려면 다음 항목이 필요합니다.

   1. WinJS 라이브러리
   1. 패키지에 자체 서명된 인증서 또는 VeriSign과 같은 신뢰할 수 있는 기관의 서명된 공개 인증서가 포함되어 있는지 확인합니다.
   1. 개발자 라이선스

   Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test 디렉토리에는 네 가지 기본 구성 요소가 있습니다.

   1. `.appx` 파일
   1. 인증서(현재 Apache Cordova가 자체 서명한 인증서)
   1. 종속성 폴더
   1. PowerShell 파일(.ps1 확장명)

## Windows PowerShell을 사용하여 앱 배포 {#deploying-an-app-using-windows-powershell}

Windows 장치에 응용 프로그램을 설치하는 두 가지 방법이 있습니다.

### 개발자 라이선스를 취득함으로써 {#by-acquiring-the-developer-license}

1. PowerShell 파일을 마우스 오른쪽 단추로 클릭합니다( `Add-AppDevPackage.ps1)`, 및 선택 **PowerShell로 실행**.

1. 개발자 라이선스를 입력하라는 메시지가 표시됩니다. Microsoft 계정 자격 증명을 사용하여 개발자 라이선스를 취득합니다.\
   이 라이센스는 30일 동안 유효하며 무료로 갱신할 수 있습니다.
1. 개발자 라이선스를 취득하면 설치 프로그램이 자체 서명된 인증서를 시스템에 설치하고 응용 프로그램을 성공적으로 설치합니다.

### 엔터프라이즈 소유 디바이스 사용 {#by-using-enterprise-owned-devices}

기업 도메인에 가입된 기업 소유 장치의 경우 개발자 라이선스를 취득할 필요가 없습니다.

엔터프라이즈 소유 장치는 Professional 및 Enterprise Edition의 Windows를 사용합니다.

Microsoft은 VeriSign과 같은 신뢰할 수 있는 기관에서 발급한 공개 인증서를 설치할 것을 권장합니다.

앱을 배포하려면:

* 장치가 엔터프라이즈의 도메인에 가입되어 있는지 확인합니다.
* 그룹 정책 설정을 사용하도록 설정합니다.

**그룹 정책 설정을 사용하려면:**

1. 장치에서 를 실행합니다. `gpedit.msc`.
1. 다음으로 이동 **컴퓨터 구성 > 관리 템플릿 > Windows 구성 요소 > 앱 패키지 배포**.
1. 마우스 오른쪽 버튼 클릭 **모든 신뢰할 수 있는 앱 설치 허용**.
1. 클릭 **편집** 및 선택 **활성화됨**.

1. **확인**&#x200B;을 클릭합니다.

Visual Studio에서 생성된 PowerShell 스크립트를 편집하여 개발자 라이선스를 획득하지 못하도록 합니다.

PowerShell 스크립트에서 변수를 설정합니다. `$NeedDeveloperLicense = $false`.

도메인에 가입되지 않은 장치의 경우 사이드 로딩 제품 활성화 키가 필요합니다. Windows 대리점에서 구입할 수 있습니다.

Windows 8.1 Home Edition의 경우 그룹 정책이 없으며 엔터프라이즈 측 로드가 허용되지 않으며 엔터프라이즈 도메인으로 가입할 수 없습니다. 개발자 라이선스를 사용하여 Windows 8.1 Home Edition 장치에 앱을 배포합니다.

자세한 내용을 보려면 [여기](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx).

## Visual Studio를 사용하여 앱 배포 {#deploying-an-app-using-visual-studio}

Visual Studio를 사용하여 Windows에 앱을 설치하려면

1. 원격 디버거를 사용하여 장치를 연결합니다.\
   자세한 내용은 [원격 컴퓨터에서 Windows 스토어 앱 실행](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine).

1. Visual Studio에서 앱을 연 상태에서 솔루션 플랫폼 목록에서 Windows-x64, Windows-x86 또는 Windows-AnyCPU를 선택하고 **원격 컴퓨터**.
1. 앱이 원격 컴퓨터에 배포됩니다.
