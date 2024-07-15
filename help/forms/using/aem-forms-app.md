---
title: AEM Forms 앱
description: AEM Forms 앱을 사용하면 현장 작업자가 모바일 장치에서 적응형 양식을 사용할 수 있습니다.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 1%

---

# AEM Forms 앱 소개 {#aem-forms-app}

## 개요 {#overview}

AEM Forms 앱을 사용하면 서버를 기반으로 모바일 장치에서 적응형 양식, 모바일 양식 및 양식 세트를 동기화할 수 있습니다. OSGi의 [Forms 중심 워크플로](/help/forms/using/aem-forms-workflow.md) 또는 JEE의 Forms 워크플로인 워크플로를 정의할 수 있습니다. 예를 들어, 은행 회사를 운영하고 AEM Forms을 사용하여 고객 애플리케이션과 커뮤니케이션을 관리합니다. 고객이 양식을 작성하여 확인을 위해 제출합니다. 모바일 장치에서 양식을 활성화하면 고객이 AEM Forms 앱에서 양식을 채울 수 있습니다. 모바일 장치에서 확인 양식을 활성화하여 확인 워크플로를 관리할 수도 있습니다. 현장 작업자는 고객에게 모바일 장치를 전달하고, 세부 사항을 확인하고, 양식을 제출할 수 있습니다. AEM Forms 앱은 AEM Forms 서버와 동기화되며 모바일 장치에 대해 활성화된 양식을 가져옵니다. 앱이 오프라인 상태이면 데이터를 로컬에 저장합니다.

AEM Forms 앱의 소스 코드는 소프트웨어 배포를 통해 고객이 사용할 수 있습니다. 소프트웨어 배포의 원본 코드 패키지는 `adobe-aemfd-forms-app-src-pkg-<version>.zip`(으)로 사용할 수 있습니다.

AEM Forms 앱은 iOS, Android, Windows 디바이스에서 지원됩니다. Google Play에서 Android용 AEM Forms 앱, App Store에서 iOS, Windows 스토어에서 Windows를 설치할 수 있습니다.

    [ ![google_play](assets/google_play.png)(https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)(https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)(https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

iOS, Android 또는 Windows 장치에서 앱을 설치, 사용자 지정 및 배포하려면 [AEM Forms 앱 사용자 지정, 빌드 및 배포](#customize-build-distribute)를 참조하십시오.

## 사전 요구 사항 {#prerequisites}

AEM Forms 앱에는 AEM Forms 서버가 필요합니다. 사용자는 AEM Forms에서 만든 양식을 렌더링할 수 있습니다.
서버, 작성, 초안으로 저장 및 제출 앱은 서버에 연결하고 활성화된 양식을 가져옵니다. AEM Forms 앱은 서버와 동기화되며 앱에서 양식이 로드되는 즉시 사용자는 오프라인으로 작업할 수 있습니다. 앱이 오프라인 상태이면 데이터가 장치에 저장되고 앱이 온라인 상태일 때 데이터가 서버와 동기화됩니다.

### AEM Forms 워크플로를 사용하는 서버가 있는 AEM Forms 앱 {#aem-forms-app-with-servers-using-aem-forms-workflow}

AEM Forms Workflow 서버가 있는 경우 양식을 AEM Forms 앱에서 작업으로 렌더링할 수 있습니다. 예를 들어, 당신이 은행회사를 운영하고, 고객이 당신의 서비스를 이용하기 위해 신청서를 작성한다. 이 애플리케이션은 고객의 정보를 받아 검토를 위한 제출로 저장하는 적응형 양식입니다. 관리자가 애플리케이션을 검토하고 확인 요청을 현장 작업자에게 전달합니다. 전달된 응용 프로그램을 사용하면 현장 작업자 앱에서 확인 양식을 작업으로 사용할 수 있습니다. 현장 작업자는 고객에게 모바일 장치를 전달하고 세부 사항을 확인합니다.

### OSGi에서 Forms 중심 워크플로를 사용하는 서버가 있는 AEM Forms 앱 {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

AEM Forms 서버가 있는 경우 적응형 양식을 AEM 받은 편지함 애플리케이션으로 렌더링하고 AEM Forms 앱에서 작업을 수행할 수 있습니다. 예를 들어, 당신이 은행회사를 운영하고, 고객이 당신의 서비스를 이용하기 위해 신청서를 작성한다. 애플리케이션은 고객으로부터 정보를 받아들이는 적응형 양식과 연관되어 검토를 위한 제출로 저장됩니다. 관리자가 작업을 검토하고 현장 작업자에게 확인 요청을 승인한다. 현장 작업자는 고객에게 모바일 장치를 전달하고 세부 사항을 확인합니다.

### AEM Forms Workflow가 없는 서버를 사용하는 독립형 양식 또는 AEM Forms 앱 {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

AEM Forms Workflow를 사용하지 않는 AEM Forms 서버는 OSGi의 AEM Forms 또는 독립 실행형 모바일 양식 또는 적응형 양식입니다. AEM Forms 앱은 [OSGi](/help/sites-deploying/configuring-osgi.md)에서 AEM Forms 구현과 함께 작동합니다. AEM Forms 앱에 대해 활성화하고 게시하는 Forms은 앱에서 사용할 수 있습니다.

양식은 앱에서 다운로드되고 오프라인에서 사용할 수 있습니다. 예를 들어, 은행 회사를 운영하고 있는 경우, 고객이 사이트에서 애플리케이션을 작성합니다. 애플리케이션은 고객의 정보를 수락하고 검토를 위해 저장하는 적응형 양식입니다. 관리자가 양식을 검토하고 AEM 작성자 인스턴스에서 확인 양식을 만듭니다. 관리자는 양식을 AEM Forms 앱과 동기화하고 게시합니다. AEM Forms 앱에서 확인 양식을 사용할 수 있는 경우 필드 에이전트는 모바일 장치를 사용하여 고객의 세부 정보를 확인할 수 있습니다. 모바일 장치가 서버와 동기화되고 확인 양식이 앱에 로드됩니다. 현장 상담원은 고객을 방문하여 세부 정보를 확인하거나 데이터를 초안으로 저장하거나 확인 양식을 제출할 수 있습니다. 앱이 온라인 상태일 때마다 양식이 서버와 동기화됩니다.

AEM Forms 앱에서 양식을 동기화하려면:

1. 작성자 인스턴스에서 양식을 선택하고 **[!UICONTROL 속성 보기]**&#x200B;를 클릭합니다.

1. 속성 페이지에서 **[!UICONTROL 고급]**&#x200B;을 클릭합니다.
1. [고급]에서 옵션 **[!UICONTROL AEM Forms 앱과 동기화]**&#x200B;를 사용하도록 설정하고 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

양식이 게시되면 앱은 서버와 동기화되고 양식을 가져옵니다. 작성자 인스턴스에서 여러 양식을 동기화하려면 Forms Manager에서 여러 양식을 선택하고 **[!UICONTROL AEM Forms 앱과 동기화]**&#x200B;를 선택합니다.

## 모바일 장치 지원 {#mobile-device-support}

[AEM Forms 앱(이전 모바일 Workspace)을 참조하십시오](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms 앱의 주요 기능 {#key-features-of-aem-forms-app}

### AEM Forms 서버가 있는 AEM Forms 앱 {#aem-forms-app-with-aem-forms-servers}

앱을 AEM Forms 서버와 동기화하고 모바일 장치의 양식으로 작업할 수 있습니다.

AEM Forms Workflow Server를 사용하면 Workbench 프로세스 및 AEM 받은 편지함 애플리케이션의 시작점과 양식을 연결할 수 있습니다. AEM 받은 편지함 애플리케이션에는 적응형 양식이 연결되어 있을 수 있습니다. 시작점에는 적응형 양식, HTML5 양식 또는 이와 연결된 양식 집합이 있을 수 있습니다. 시작점을 작업으로 제출하거나 작업을 초안으로 저장할 수 있습니다. AEM 받은 편지함 애플리케이션과 시작 지점 간의 차이점에 대한 자세한 내용은 [OSGi 및 AEM Forms JEE 워크플로우에서 양식 중심의 AEM 워크플로우의 작업 및 기능](capabilities-osgi-jee-workflows.md)을 참조하십시오.

AEM Forms 워크플로가 없는 AEM Forms 서버를 사용하면 앱에서 동기화가 활성화된 양식이 AEM Forms 앱에서 렌더링됩니다. Forms은 앱의 Forms 탭에서 사용할 수 있으며 초안으로 제출하거나 저장할 수 있습니다. 적응형 양식 및 모바일 양식은 앱에서 지원됩니다.

1. **작업 또는 양식을 초안으로 저장**

   초안으로 저장 옵션을 사용하면 작업 또는 양식의 스냅샷과 함께 채워진 데이터 및 관련 양식에 첨부된 파일이 저장됩니다. 초안은 모바일 장치에 저장되고 나중에 검색할 수 있도록 AEM Forms 서버와 동기화됩니다.

   [작업 또는 양식을 초안으로 저장](/help/forms/using/save-as-draft.md)을 참조하십시오.

1. **양식을 템플릿으로 저장**

   사용자가 양식을 채울 때 일부 필드에 대한 입력이 동일하게 유지되는 경우가 있습니다. 이러한 경우 모든 인스턴스에서 동일한 값이 필요한 필드를 채우고 양식 또는 초안을 템플릿으로 저장할 수 있습니다. 이제 템플릿의 인스턴스를 만들 때마다 지정된 필드가 템플릿에 지정된 값으로 이미 채워집니다. 양식을 작성하는 데 필요한 시간과 노력을 절약하는 데 도움이 됩니다.

   [템플릿으로 양식 저장](/help/forms/using/save-forms-and-start-points-as-templates.md)을 참조하십시오.

### 작업 및 양식 작업 {#working-with-tasks-and-forms}

앱을 AEM Forms Workflow 서버와 동기화하고, 모바일 장치에서 작업 및 양식을 작업할 수 있습니다.

모바일 장치의 작업에는 적응형 양식, HTML 5 양식 또는 양식 집합이 포함되어 있으며 첨부 파일 및 [요약 URL](/help/forms/using/getting-task-variables-summary-url.md)도 포함할 수 있습니다. 기본적으로 사용자에게 할당된 작업은 **[!UICONTROL 작업]** 폴더에 배치됩니다. 작업을 수행할 때 작업을 변경하고 AEM Forms 서버에 작업의 초안 사본을 저장할 수 있습니다.

모바일 디바이스상의 양식은 적응형 양식 또는 모바일 양식일 수 있다. 양식 앱에서 동기화가 활성화된 Forms은 Forms 폴더에서 사용할 수 있습니다. AEM Forms 워크플로(OSGi의 AEM Forms) 없이 AEM Forms 서버에서 활성화된 양식을 동기화할 수 있습니다.

다음을 참조하십시오.

* [작업 열기](/help/forms/using/open-task.md)
* [양식 작업](/help/forms/using/working-with-form.md)

### 오프라인 작업 {#working-offline}

오프라인 모드에서 모바일 장치에서 작업할 수 있습니다. 네트워크 연결이 없는 경우에도 응용 프로그램에 로그인할 수 있으며 마지막으로 온라인 상태일 때 장치와 동기화된 모든 양식에서 작업할 수 있습니다. 양식을 동기화하는 방법에 대한 자세한 내용은 [앱 동기화](/help/forms/using/sync-app.md)를 참조하십시오. 양식과 연결된 첨부 파일을 동기화하도록 선택하면 오프라인 모드에서도 첨부 파일을 열 수 있습니다. 오프라인 모드에서 양식을 편집하고, 주석을 추가하고, 양식을 제출하거나 저장할 수 있습니다. 양식은 다음에 온라인 상태일 때 AEM Forms 서버와 동기화됩니다.

자세한 내용은 [오프라인 모드에서 작업](/help/forms/using/work-offline-mode.md)을 참조하세요.

### 주석 추가 {#adding-annotations}

모바일 장치에서 양식에 다음 첨부 파일을 추가할 수 있습니다

* **메모**- 메모 기능을 사용하여 자유 손으로 스크리블 또는 텍스트 메모를 양식에 추가할 수 있습니다. 자세한 내용은 [메모 추가](/help/forms/using/add-attachments.md#adding-a-note)를 참조하세요.

* **사진**- AEM Forms 앱에는 카메라 기능 또는 모바일 장치의 갤러리를 사용하는 기능이 포함되어 있습니다. 사진 첨부 파일을 사용하여 연결된 양식이 있는 사진을 추가할 수 있습니다. 자세한 내용은 [사진 추가](/help/forms/using/add-attachments.md#adding-a-photograph)를 참조하세요.

### 자동 저장 {#autosave}

사용자가 AEM Forms 앱에 데이터를 입력하면 자동 저장 기능이 정기적으로 데이터를 저장합니다. AEM Forms 앱의 자동 저장 기능을 사용하면 배터리 부족 등의 문제로 앱이 닫힐 경우 데이터 손실을 방지할 수 있습니다.

[AEM Forms 앱에서 자동 저장 사용](/help/forms/using/autosave-data-app.md)을 참조하세요.

## AEM 받은 편지함 및 AEM Forms 앱 기능의 차이점 {#differences-between-aem-inbox-and-aem-forms-app-features}

Forms 중심 워크플로를 시작하는 두 가지 두드러진 방법에는 [AEM 받은 편지함](/help/forms/using/manage-applications-inbox.md) 및 AEM Forms 앱이 있습니다. 그러나 AEM Inbox와 AEM Forms 앱의 기능은 다릅니다. AEM 받은 편지함은 [Forms 중심 워크플로](/help/forms/using/aem-forms-workflow.md)에서만 작동하지만, AEM Forms 앱은 Forms 중심 워크플로와 프로세스 관리를 모두 사용합니다. AEM 받은 편지함과 AEM Forms 앱 기능의 차이점에 대한 자세한 내용은 [OSGi 및 AEM Forms JEE 워크플로우에서 양식 중심의 AEM 워크플로우의 작업 및 기능](capabilities-osgi-jee-workflows.md)을 참조하십시오.

## 지원되는 양식 {#supported-forms}

AEM Forms 앱에서 지원되는 양식 유형:

### 적응형 양식 {#adaptive-form}

사용자 입력에 동적으로 적응하는 적응형 양식은 AEM Forms 앱에서 지원됩니다. 지연 로드된 적응형 양식도 지원됩니다.

### 모바일 양식 {#mobile-form}

AEM Forms에서 모바일 장치용 양식을 만들 수 있습니다. 모바일 양식은 디스플레이 장치에 따라 적용되는 모바일 장치에서 HTML 양식으로 렌더링됩니다.

### 양식 세트 {#formset}

양식 세트를 사용하면 서비스 또는 프로세스와 관련된 여러 양식을 그룹화하여 비즈니스 프로세스를 자동화하고 최종 사용자에게 제공할 수 있습니다. 이러한 시나리오에서는 사용자가 전체 세트를 하나로 채울 수 있으며 개별 양식 또는 프로세스를 파일, 제출 및 추적할 필요가 없습니다.

>[!NOTE]
>
>AEM Forms 워크플로(JEE의 AEM Forms)가 필요합니다.

## AEM Forms 앱 작동 방식 {#how-aem-forms-app-works}

AEM Forms 앱은 현장 작업자가 자신에게 할당된 양식을 작업할 수 있는 모바일 솔루션을 제공합니다. 응용 프로그램은 서버에서 전체 데이터를 캐시하고 모든 작업을 로컬로 저장하여 효율적인 사용자 경험을 제공합니다. 디스크의 데이터는 적시에 동기화 업데이트를 통해 서버로 전송됩니다.

AEM Forms 앱은 PhoneGap 5.0 기반 애플리케이션으로, Backbone 모델을 사용하여 모델에 저장된 데이터를 보기를 통해 표시하는 데 효율적으로 사용됩니다. 모든 기본 작업은 PhoneGap 플러그인을 통해 수행됩니다.

## AEM Forms 앱 사용자 지정, 빌드 및 배포 {#customize-build-distribute}

>[!NOTE]
>
>AEM Forms 앱 소스 코드를 사용하여 앱을 빌드하는 경우에만 적용할 수 있습니다.

AEM Forms 앱은 조직별 요구 사항에 맞게 손쉽게 맞춤화할 수 있습니다. 애플리케이션의 소스 코드는 AEM Forms과 함께 제공됩니다. 소스 코드를 변경하고 고유한 모바일 인력 솔루션을 구축할 수 있습니다. 자신의 엔터프라이즈 키로 앱에 서명할 수도 있습니다.

### 맞춤화 {#customize}

다음에 대해 앱을 사용자 지정할 수 있습니다.

**브랜딩**: AEM Forms 앱에서 앱 아이콘, 앱 이름, 시작 이미지 및 페이지를 변경합니다. 텍스트를 변경하여 특정 지역에 대한 앱을 현지화할 수도 있습니다. AEM Forms 앱 브랜딩에 대한 자세한 내용은 [브랜딩 사용자 지정](/help/forms/using/branding-customization.md)을 참조하십시오.

**테마**: AEM Forms 앱 사용자 인터페이스에서 색상, 글꼴 및 간격 등의 스타일을 변경합니다. 자세한 내용은 [테마 맞춤화](/help/forms/using/theme-customization.md)를 참조하세요.

**제스처**: AEM Forms 앱 사용자 인터페이스에서 오른쪽으로 스와이프하고 왼쪽으로 스와이프하는 것과 같은 제스처를 변경합니다. 자세한 내용은 [제스처 사용자 지정](/help/forms/using/gesture-customization.md)을 참조하십시오.

맞춤화를 위한 AEM Forms 앱 프로젝트 설정에 대한 자세한 내용은 다음을 참조하십시오.

* [AEM Forms 앱을 위한 환경 설정](/help/forms/using/setup-environment-mobile-workspace.md)
* [Visual Studio 프로젝트 설정 및 Windows 앱 빌드](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Xcode 프로젝트 설정 및 iOS 앱 빌드](/help/forms/using/setup-xcode-project-build-installer.md)
* [Eclipse 프로젝트 설정 및 Android 앱 빌드](/help/forms/using/setup-eclipse-project-build-installer.md)

### 빌드 및 배포 {#build-and-distribute}

소프트웨어 배포의 AEM Forms 앱 소스 패키지의 일부로 사용할 수 있는 `adobe-lc-mobileworkspace-src.zip`에서 AEM Forms 앱의 소스 코드를 추출할 수 있습니다.

AEM Forms 앱 소스를 가져오려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에서 사용할 수 있는 **[!UICONTROL Adobe Experience Manager]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL 필터]** 섹션에서:
   1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을(를) 선택합니다.
   2. 패키지의 버전 및 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 선택합니다.
1. [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.

iOS의 **1}:**

iOS 앱(.ipa)을 만드는 방법에 대한 자세한 내용은 [Xcode 프로젝트 설정 및 iOS 앱 빌드](/help/forms/using/setup-xcode-project-build-installer.md)를 참조하십시오.

프로비저닝 프로필로 AEM Forms 앱에 서명하는 방법에 대한 자세한 내용은 [iOS 코드 서명 설정, 프로세스 및 문제 해결](https://developer.apple.com/support/code-signing/)을 참조하십시오.

Android의 **1}:**

Android 앱(.apk)을 만드는 방법에 대한 자세한 내용은 [Eclipse 프로젝트 설정 및 Android 앱 빌드](/help/forms/using/setup-eclipse-project-build-installer.md)를 참조하십시오.

AEM Forms 앱에 서명하는 방법에 대한 자세한 내용은 [응용 프로그램 서명](https://developer.android.com/tools/publishing/app-signing.html)을 참조하세요.

**Windows용**:

Windows 앱(.appx)을 만드는 방법에 대한 자세한 내용은 [Visual Studio 프로젝트 설정 및 Windows 앱 빌드](/help/forms/using/setup-visual-studio-project-build-installer.md)를 참조하십시오.

MDM을 통해 앱을 배포하는 방법에 대한 자세한 내용은 [AEM Forms 앱 배포](/help/forms/using/distribute-mobile-workspace-app.md)를 참조하십시오. MDM을 통한 앱 배포는 iOS 및 Android에만 적용됩니다.

## Recommendations - Mobile Workspace을 AEM Forms 앱으로 업그레이드 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

최신 버전의 AEM Forms 앱으로 업그레이드하는 경우 다음 사항을 읽어야 합니다.

* **Android의 Play 스토어에서 이전 버전의 앱을 설치한 경우**
앱을 Play 스토어에서 바로 업그레이드할 수 있습니다.

* **소스 코드(iOS 및 Android에 적용 가능)를 사용하여 이전 버전의 앱을 빌드하고 설치한 경우**:

  새 앱을 설치하기 전에 모든 데이터를 AEM Forms 서버와 동기화합니다. 데이터가 동기화된 후 이전 버전의 앱을 제거하고 새 앱을 설치합니다.
