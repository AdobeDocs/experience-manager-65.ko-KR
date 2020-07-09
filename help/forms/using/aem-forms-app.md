---
title: AEM Forms 앱
seo-title: AEM Forms 앱
description: AEM Forms 앱을 사용하면 현장 작업자가 모바일 디바이스에서 적응형 양식을 사용할 수 있습니다.
seo-description: AEM Forms 앱을 사용하면 현장 작업자가 모바일 디바이스에서 적응형 양식을 사용할 수 있습니다.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: aaedec7314b0fa8551df560eef2574a53c20d1c5
workflow-type: tm+mt
source-wordcount: '2418'
ht-degree: 0%

---


# Introduction to AEM Forms app {#aem-forms-app}

## 개요 {#overview}

AEM Forms 앱을 사용하면 서버를 기반으로 모바일 디바이스에서 적응형 양식, 모바일 양식 및 양식을 동기화할 수 있습니다. JEE에서 OSGi [또는](/help/forms/using/aem-forms-workflow.md) 양식 워크플로우에서 [양식 중심 워크플로우인 워크플로우를 정의할 수 있습니다](/help/forms/using/finance-reference-site-walkthrough.md#approving-the-application). 예를 들어 은행 회사를 실행하고 AEM Forms을 사용하여 고객 애플리케이션과 커뮤니케이션을 관리합니다. 고객이 양식을 작성하고 확인을 위해 제출합니다. 모바일 장치에서 양식을 활성화하면 고객이 AEM Forms 앱에서 양식을 채울 수 있습니다. 모바일 장치에서 확인 양식을 활성화하여 확인 워크플로우를 관리할 수도 있습니다. 현장 작업자는 모바일 장치를 고객에게 휴대하고 세부 사항을 확인하고 양식을 제출할 수 있습니다. AEM Forms 앱은 AEM Forms 서버와 동기화되고 모바일 장치에서 사용할 수 있는 양식을 가져옵니다. 앱이 오프라인 상태인 경우 로컬에 데이터를 저장합니다.

고객은 패키지 공유를 통해 AEM Forms 앱의 소스 코드를 사용할 수 있습니다. 패키지 공유의 소스 코드 패키지를 다음과 같이 사용할 수 있습니다. `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

AEM Forms 앱은 iOS, Android, Windows 디바이스에서 지원됩니다. Google Play, App Store 및 Windows Store에서 Android용 AEM Forms 앱을 설치할 수 있습니다.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

iOS, Android 또는 Windows 장치에 앱을 설치, 사용자 정의 및 배포하려면 AEM Forms 앱 [사용자 정의, 빌드 및 배포를 참조하십시오](#customize-build-distribute).

## 전제 조건 {#prerequisites}

AEM Forms 앱에 AEM Forms 서버가 필요합니다. 사용자는 AEM Formsserver에서 만든 양식을 렌더링하여 채우고 초안으로 저장한 다음 제출할 수 있습니다. 이 앱은 서버에 연결하여 활성화된 양식을 해당 앱에서 가져옵니다. AEM Forms 앱은 서버와 동기화되며 앱이 앱에 로드되면 사용자가 오프라인으로 작업할 수 있습니다. 앱이 오프라인 상태인 경우 데이터가 장치에 저장되고 앱이 온라인 상태일 때 데이터가 서버와 동기화됩니다.

### AEM Forms을 사용하는 서버의 AEM Forms 앱 {#aem-forms-app-with-servers-using-aem-forms-workflow}

AEM Forms Workflow 서버가 있는 경우 AEM Forms 앱에서 양식을 작업으로 렌더링할 수 있습니다. 예를 들어 은행 회사를 실행하고 고객은 서비스를 사용하는 애플리케이션을 채웁니다. 애플리케이션은 고객으로부터 정보를 받아 검토용으로 저장하는 적응형 양식입니다. 관리자는 애플리케이션을 검토하고 확인 요청을 필드 작업자에게 전달합니다. 전달된 응용 프로그램은 현장 작업자 앱의 확인 양식을 작업으로 활성화합니다. 현장 작업자는 모바일 장치를 고객에게 전달하여 세부 사항을 확인합니다.

### OSGi에서 양식 중심의 워크플로우를 사용하는 서버 기반의 AEM Forms 앱 {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

AEM Forms 서버가 있는 경우 적응형 양식을 AEM 받은 편지함 애플리케이션으로 렌더링하고 AEM Forms 앱에서 작업을 수행할 수 있습니다. 예를 들어 은행 회사를 실행하고 고객은 서비스를 사용하는 애플리케이션을 채웁니다. 애플리케이션은 고객의 정보를 받아 검토한 후 제출용으로 저장하는 적응형 양식과 연결됩니다. 관리자는 작업을 검토하고 필드 작업자에게 확인 요청을 승인합니다. 현장 작업자는 모바일 장치를 고객에게 전달하여 세부 사항을 확인합니다.

### AEM Forms 없이 독립 실행형 양식 또는 AEM Forms 앱 서버 사용 워크플로우 {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

AEM Forms 작업 과정을 사용하지 않는 AEM Forms 서버는 OSGi 또는 독립 실행형 모바일 양식 또는 응용 양식의 AEM Forms입니다. AEM Forms 앱은 OSGi에서 AEM Forms 구현과 [연동됩니다](/help/sites-deploying/configuring-osgi.md). AEM Forms 앱에 대해 활성화하고 게시하는 양식은 앱에서 사용할 수 있습니다.

양식은 앱에서 다운로드되며 오프라인에서 사용할 수 있습니다. 예를 들어 은행 회사를 운영하고 있으며 고객이 사이트의 애플리케이션을 채웁니다. 애플리케이션은 고객의 정보를 받아 검토한 후 저장하는 적응형 양식입니다. 관리자는 양식을 검토하고 AEM 작성자 인스턴스에서 확인 양식을 만듭니다. 관리자는 양식을 AEM Forms 앱과 동기화할 수 있도록 하고 이를 게시합니다. AEM Forms 앱에서 확인 양식을 사용할 수 있는 경우 필드 에이전트는 모바일 장치를 사용하여 고객의 세부 사항을 확인할 수 있습니다. 모바일 장치가 서버와 동기화되고 확인 양식이 앱에 로드됩니다. 필드 에이전트는 고객을 방문하고 세부 사항을 확인하거나 데이터를 초안으로 저장하거나 확인 양식을 제출할 수 있습니다. 앱이 온라인 상태일 때마다 양식이 서버와 동기화됩니다.

AEM Forms 앱에서 양식을 동기화하려면 다음을 수행하십시오.

1. 작성 인스턴스에서 양식을 선택하고 속성 **[!UICONTROL 보기를 클릭합니다]**.

1. 속성 페이지에서 고급을 **[!UICONTROL 클릭합니다]**.
1. 고급 아래에서 옵션을 활성화합니다. **[!UICONTROL AEM Forms 앱과 동기화]** 및 저장을 **[!UICONTROL 탭합니다]**.

양식이 게시되면 앱은 서버와 동기화되고 양식을 페치합니다. 여러 양식을 동기화하려면 작성 인스턴스에서 양식 관리자에서 여러 양식을 선택하고 AEM Forms 앱과 **[!UICONTROL 동기화를 누릅니다]**.

## 모바일 디바이스 지원 {#mobile-device-support}

AEM Forms [앱 보기(이전의 모바일 작업 공간)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms 앱의 주요 기능 {#key-features-of-aem-forms-app}

### AEM Forms 서버가 있는 AEM Forms 앱 {#aem-forms-app-with-aem-forms-servers}

앱을 AEM Forms 서버와 동기화할 수 있으며 모바일 디바이스에서 양식을 사용하여 작업할 수 있습니다.

AEM Forms Workflow 서버에서 양식은 워크벤치 프로세스 및 AEM Inbox 응용 프로그램의 시작점과 연결할 수 있습니다. AEM 받은 편지함 애플리케이션에는 연결된 적응형 양식이 있을 수 있습니다. 시작 지점에는 적응형 양식, HTML5 양식 또는 이와 연결된 양식 세트가 있을 수 있습니다. 시작점을 작업으로 제출하거나 작업을 초안으로 저장할 수 있습니다. AEM 받은 편지함 애플리케이션과 시작 지점 간의 차이점에 대한 자세한 내용은 OSGi 및 AEM Forms JEE 워크플로우에서 [양식 중심의 AEM 워크플로우의 작업 및 기능을 참조하십시오](capabilities-osgi-jee-workflows.md).

AEM Forms 작업 과정이 없는 AEM Forms 서버에서는 앱에서 동기화할 수 있는 양식이 AEM Forms 앱에서 렌더링됩니다. 양식은 앱의 양식 탭에서 사용할 수 있으며, 양식을 제출하거나 초안으로 저장할 수 있습니다. 응용 양식 및 모바일 양식은 앱에서 지원됩니다.

1. **작업 또는 양식을 초안으로 저장**

   초안으로 저장 옵션은 작업 또는 양식의 스냅숏과 연결된 양식에 첨부된 데이터를 저장합니다. 초안이 모바일 장치에 저장되고 나중에 검색할 수 있도록 AEM Forms 서버와 동기화됩니다.

   작업 [또는 양식을 초안으로 저장을 참조하십시오](/help/forms/using/save-as-draft.md).

1. **양식을 템플릿으로 저장**

   때때로 사용자가 양식을 채울 때 일부 필드에 대한 입력은 동일하게 유지됩니다. 이러한 경우 모든 인스턴스에서 동일한 값이 필요한 필드를 채우고 양식이나 초안을 템플릿으로 저장할 수 있습니다. 이제 템플릿의 인스턴스를 만들 때마다 지정된 필드가 이미 템플릿에 지정된 값으로 채워집니다. 양식 작성에 필요한 시간과 노력을 절약할 수 있습니다.

   양식을 템플릿으로 [저장을 참조하십시오](/help/forms/using/save-forms-and-start-points-as-templates.md).

### 작업 및 양식 작업 {#working-with-tasks-and-forms}

앱을 AEM Forms Workflow 서버와 동기화할 수 있으며 모바일 디바이스에서 작업 및 양식을 작업할 수 있습니다.

모바일 장치의 작업에는 응용 양식, HTML5 양식 또는 양식 세트가 포함되어 있으며 첨부 파일과 [요약 URL이 포함될 수도 있습니다](/help/forms/using/getting-task-variables-summary-url.md). 기본적으로 자신에게 할당된 작업은 **[!UICONTROL 작업 폴더에]** 배치됩니다. 작업을 수행할 때 작업을 변경하고 AEM Forms 서버에 작업 초안 사본을 저장할 수 있습니다.

모바일 장치의 양식은 적응형 양식이나 모바일 양식일 수 있습니다. 양식 앱에서 동기화할 수 있는 양식은 양식 폴더에서 사용할 수 있습니다. AEM Forms 작업 과정 없이 AEM Forms 서버에서 활성화된 양식을 동기화할 수 있습니다(OSGi의 AEM Forms).

다음을 참조하십시오.

* [작업 열기](/help/forms/using/open-task.md)
* [양식 작업](/help/forms/using/working-with-form.md)

### 오프라인 작업 {#working-offline}

오프라인 모드에서 모바일 디바이스에서 작업할 수 있습니다. 네트워크에 연결되지 않은 경우에도 응용 프로그램에 로그인할 수 있으며 마지막으로 온라인 상태였을 때 디바이스와 동기화된 모든 양식에서 작업할 수 있습니다. 양식을 동기화하는 방법에 대한 자세한 내용은 앱 [동기화를 참조하십시오](/help/forms/using/sync-app.md). 양식과 연관된 첨부 파일을 동기화하도록 선택하면 오프라인 모드에서도 첨부 파일을 열 수 있습니다. 오프라인 모드에서 양식을 편집하고, 주석을 추가하고, 양식을 제출하거나 저장할 수 있습니다. 다음 번에 온라인 상태일 때 양식이 AEM Forms 서버와 동기화됩니다.

자세한 내용은 [오프라인 모드에서 작업을 참조하십시오](/help/forms/using/work-offline-mode.md).

### Adding annotations {#adding-annotations}

모바일 장치의 양식에 다음 첨부 파일을 추가할 수 있습니다

* **참고**- 메모 기능을 사용하여 양식에 자유 손글씨 또는 텍스트 메모를 추가할 수 있습니다. 자세한 내용은 메모 [추가를 참조하십시오](/help/forms/using/add-attachments.md#adding-a-note).

* **사진**- AEM Forms 앱에는 카메라 기능이나 모바일 장치의 갤러리를 사용하는 기능이 포함되어 있습니다. 사진 첨부 파일을 사용하여 연결된 폼으로 사진을 추가할 수 있습니다. 자세한 내용은 사진 [추가를 참조하십시오](/help/forms/using/add-attachments.md#adding-a-photograph).

### 자동 저장 {#autosave}

사용자가 AEM Forms 앱에 데이터를 입력하면 자동 저장 기능이 정기적으로 데이터를 저장합니다. AEM Forms 앱의 자동 저장 기능을 사용하면 배터리 부족 등의 문제로 앱이 닫히는 경우 데이터 손실을 방지할 수 있습니다.

AEM Forms [앱에서 자동 저장 사용을 참조하십시오](/help/forms/using/autosave-data-app.md).

## AEM 받은 편지함 및 AEM Forms 앱 기능 간의 차이점 {#differences-between-aem-inbox-and-aem-forms-app-features}

양식 중심의 워크플로우를 실행하는 중요한 두 가지 방법 중 하나는 [AEM Inbox](/help/forms/using/manage-applications-inbox.md) 및 AEM Forms 앱을 사용하는 것입니다. 하지만 AEM 받은 편지함 및 AEM Forms 앱의 기능은 다릅니다. AEM Inbox는 [양식 중심 워크플로우에서만](/help/forms/using/aem-forms-workflow.md) 작동하는 반면 AEM Forms 앱은 양식 중심 워크플로우뿐만 아니라 프로세스 관리에서도 작동합니다. AEM 받은 편지함 및 AEM Forms 앱 기능 간의 차이점에 대한 자세한 내용은 OSGi 및 AEM Forms JEE 워크플로우에서 양식 중심 AEM [워크플로우의 작업 및 기능을 참조하십시오](capabilities-osgi-jee-workflows.md).

## 지원되는 양식 {#supported-forms}

AEM Forms 앱에서 지원되는 양식 유형:

### 적응형 양식 {#adaptive-form}

사용자 입력에 동적으로 적용되는 적응형 양식이 AEM Forms 앱에서 지원됩니다. 레이지 로드된 적응형 양식도 지원됩니다.

### 모바일 양식 {#mobile-form}

AEM Forms에서 모바일 장치용 양식을 만들 수 있습니다. 모바일 양식은 디스플레이 장치에 따라 달라지는 모바일 장치에서 HTML 양식으로 렌더링됩니다.

### 양식 세트 {#formset}

양식을 사용하면 서비스 또는 프로세스와 관련된 여러 양식을 그룹화하여 비즈니스 프로세스를 자동화하고 최종 사용자에게 제공할 수 있습니다. 이러한 시나리오에서 사용자는 전체 세트를 하나로 채울 수 있으며 개별 양식 또는 프로세스를 파일, 제출 및 추적할 필요가 없습니다.

>[!NOTE]
>
>AEM Forms 워크플로우(JEE의 AEM Forms)이 필요합니다.

## AEM Forms 앱 작동 방식 {#how-aem-forms-app-works}

AEM Forms 앱은 현장 작업자가 자신에게 지정된 양식을 사용하여 작업할 수 있는 모바일 솔루션을 제공합니다. 애플리케이션은 서버의 전체 데이터를 캐시하고 모든 작업을 로컬에 저장하여 효율적인 사용자 환경을 제공합니다. 디스크의 데이터는 시기 적절한 동기화 업데이트를 통해 서버로 전송됩니다.

AEM Forms 앱은 PhoneGap 5.0 기반 애플리케이션으로, 백본 모델을 통해 모델에 저장된 데이터를 표시하는 데 효율적으로 사용됩니다. 모든 기본 작업은 PhoneGap 플러그인을 통해 수행됩니다.

## AEM Forms 앱 사용자 정의, 빌드 및 배포 {#customize-build-distribute}

>[!NOTE]
>
>AEM Forms 앱 소스 코드를 사용하여 앱을 빌드하는 경우에만 적용됩니다.

AEM Forms 앱은 조직별 요구 사항에 맞게 손쉽게 변경할 수 있습니다. 응용 프로그램의 소스 코드가 AEM Forms과 함께 제공됩니다. 소스 코드를 변경하고 모바일 인력 솔루션을 구축할 수 있습니다. 자신만의 기업 키로 앱에 서명할 수도 있습니다.

### 사용자 지정 {#customize}

다음을 위해 앱을 사용자 정의할 수 있습니다.

**브랜딩**: AEM Forms 앱에서 앱 아이콘, 앱 이름, 실행 이미지 및 페이지를 변경합니다. 텍스트를 변경하여 특정 지역의 앱을 지역화할 수도 있습니다. AEM Forms 앱 브랜딩에 대한 자세한 내용은 [브랜딩 사용자 지정을 참조하십시오](/help/forms/using/branding-customization.md).

**테마**: AEM Forms 앱 유저 인터페이스에서 색상, 글꼴 및 간격과 같은 스타일을 변경할 수 있습니다. 자세한 내용은 [테마 맞춤화를 참조하십시오](/help/forms/using/theme-customization.md).

**제스처**: AEM Forms 앱 사용자 인터페이스에서 오른쪽으로 밀거나 왼쪽으로 밀기와 같은 제스처를 변경합니다. 자세한 내용은 제스처 사용자 [지정을 참조하십시오](/help/forms/using/gesture-customization.md).

사용자 지정을 위한 AEM Forms 앱 프로젝트 설정에 대한 자세한 내용은 다음을 참조하십시오.

* [AEM Forms 앱에 대한 환경 설정](/help/forms/using/setup-environment-mobile-workspace.md)
* [Visual Studio 프로젝트 설정 및 Windows 앱 빌드](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Xcode 프로젝트 설정 및 iOS 앱 빌드](/help/forms/using/setup-xcode-project-build-installer.md)
* [Eclipse 프로젝트 설정 및 Android 앱 빌드](/help/forms/using/setup-eclipse-project-build-installer.md)

### 구축 및 배포 {#build-and-distribute}

패키지 공유에서 AEM Forms 앱 소스 패키지의 일부로 사용할 수 있는 adobe-lc-mobileworkspace-src.zip에서 AEM Forms 앱에 대한 소스 코드를 추출할 수 있습니다.

AEM Forms 앱 소스를 가져오려면 다음 단계를 수행하십시오.

1. 패키지 공유 탐색

   URL: `https://<server>:<port>/crx/packageshare`.

1. 소스 패키지를 다운로드합니다. 패키지를 다운로드할 때 AEM Forms 패키지 관리자에 추가됩니다.
1. 다운로드한 후 다음 위치로 이동합니다. `https://<server>:<port>/crx/packmgr/index.jsp`을 클릭하고 설치합니다 `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. 패키지를 다운로드하려면 브라우저 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 에서 엽니다.

   소스 패키지가 장치에 다운로드됩니다.

**iOS의 경우**:

iOS 앱(.ipa)을 만드는 방법에 대한 자세한 내용은 Xcode 프로젝트 [설정 및 iOS 앱 빌드를 참조하십시오](/help/forms/using/setup-xcode-project-build-installer.md).

프로비저닝 프로필을 사용하여 AEM Forms 앱에 서명하는 방법에 대한 자세한 내용은 [iOS 코드 서명 설정, 프로세스 및 문제 해결을 참조하십시오](https://developer.apple.com/support/code-signing/).

**Android의 경우**:

Android 앱(.apk)을 만드는 방법에 대한 자세한 내용은 Eclipse 프로젝트 [설정 및 Android 앱 빌드를 참조하십시오](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms 앱에 서명하는 방법에 대한 자세한 내용은 응용 프로그램 [서명을 참조하십시오](https://developer.android.com/tools/publishing/app-signing.html).

**Windows**:

Windows 앱(.appx)을 만드는 방법에 대한 자세한 내용은 Visual Studio 프로젝트 [설정 및 Windows 앱 빌드를 참조하십시오](/help/forms/using/setup-visual-studio-project-build-installer.md).

MDM을 통해 앱을 배포하는 방법에 대한 자세한 내용은 AEM Forms 앱 [배포를 참조하십시오](/help/forms/using/distribute-mobile-workspace-app.md). MDM을 통한 앱 배포는 iOS 및 Android에만 적용됩니다.

## 모바일 작업 공간을 AEM Forms 앱으로 업그레이드하기 위한 권장 사항 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

최신 버전의 AEM Forms 앱으로 업그레이드하는 경우 다음 사항을 읽어 보십시오.

* **Android의 Play Store에서 이전 버전의 앱을 설치한 경우**&#x200B;는 Play Store에서 바로 앱을 업그레이드할 수 있습니다.

* **이전 버전의 앱이 소스 코드를 사용하여 빌드되고 설치된 경우(iOS 및 Android에 적용 가능)**:

   새 앱을 설치하기 전에 모든 데이터를 AEM Forms 서버와 동기화하십시오. 데이터가 동기화되면 이전 버전의 앱을 제거하고 새 앱을 설치합니다.

