---
title: AEM Forms 앱 문제 해결
seo-title: AEM Forms 앱 문제 해결
description: AEM Forms 앱의 일반적인 문제 및 문제 해결 방법에 대해 알아보십시오.
seo-description: AEM Forms 앱의 일반적인 문제 및 문제 해결 방법에 대해 알아보십시오.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: 3690d2d76ce13064bd3946f4f6fea1a2759cdf37
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---


# AEM Forms 앱 문제 해결 {#troubleshoot-aem-forms-app}

이 문서에서는 AEM Forms 앱을 빌드하는 동안 표시할 오류 메시지와 이를 해결하는 단계에 대해 설명합니다.

이 아티클의 섹션은 다음과 같습니다.

* [iOS 사용자를 위한 첨부 파일 손실](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [작업 공간 사용자가 제출한 HTML5 양식 초안이 포털에 표시되지 않습니다.](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [AEM Forms 앱에서 HTML5 양식(캐시되지 않음)을 로드하지 못함](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [Windows에서 AEM Forms 동기화 안 함](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [지원되지 않는 Gradle 버전](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle 및 Android Gradle 플러그인 호환성 문제](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS 사용자에 대한 첨부 파일 손실 {#attachment-loss-for-ios-users}

OSGi에서 AEM Forms과 동기화하도록 구성된 iOS용 AEM Forms 앱은 필드 수준 첨부 파일만 지원합니다. 모든 첨부 파일의 이름은 고유해야 합니다. 여러 첨부 파일의 이름이 동일한 경우 하나의 첨부 파일만 유지되고 동일한 이름의 다른 첨부 파일은 모두 손실됩니다. iOS 장치의 사용자가 데이터 손실을 보지 않도록 하려면 다음 단계를 수행하십시오.

1. 연결된 서버에서 **Adobe Experience Manager > 도구 > 작업 > 웹 콘솔**&#x200B;으로 이동합니다.
1. **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성]**&#x200B;을 찾아 클릭합니다.
1. [!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성] 대화 상자에서 **파일 이름을 고유하게 만들기**&#x200B;를 활성화합니다.

   **파일 이름을 고유하게 만들기** 설정이 비활성화되어 있으면 사용자가 여러 첨부 파일이 있는 적응형 양식을 제출하려고 하면 데이터 손실이 발생합니다.

1. **저장**&#x200B;을 클릭합니다.

## 작업 공간 사용자가 제출한 HTML5 양식 초안이 포털 {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}에 표시되지 않습니다.

**초안** HTML 렌더링 프로필로 저장을 사용하여 AEM Forms 앱에서 활성화된 HTML5 양식의 경우 저장된 초안이 작업 영역 사용자에게 표시되지 않습니다. 포털에서 작업 공간 사용자가 제출한 HTML5 양식의 저장된 초안을 보려면 다음 단계를 수행하십시오.

1. CRXDE를 열고 관리자 자격 증명으로 로그인합니다.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. CRXDE의 루트 경로에서 액세스 제어의 액세스 제어 목록에서 **+**&#x200B;을 클릭합니다.
1. **새 항목 추가** 대화 상자에서 주체 필드에서 그룹 검색 단추를 클릭합니다.
1. [주체 선택] 대화 상자의 [이름] 필드에 `PERM_WORKSPACE_USER`을 입력하고 **검색**&#x200B;을 클릭합니다.
1. [주체 선택] 대화 상자에서 `PERM_WORKSPACE_USER` 그룹을 선택하고 **확인**&#x200B;을 클릭합니다.
1. [새 항목 추가] 대화 상자의 [주체] 필드에 `PERM_WORKSPACE_USER` 그룹이 선택됩니다.

   사용자 그룹에 대해 `jcr:read` 권한을 활성화합니다.

1. **확인**&#x200B;을 클릭합니다.

## HTML5 양식(캐시되지 않음)을 AEM Forms 앱 {#html-forms-not-cached-fail-to-load-in-aem-forms-app}에서 로드하지 못했습니다.

AEM Forms 앱이 이전 버전의 AEM Forms 서버에 연결되어 있으면 캐시되지 않은 HTML5 양식을 AEM Forms 앱에서 로드하지 못합니다.

문제를 해결하려면 다음 단계를 수행하십시오.

1. 작성자 인스턴스에서 **Adobe Experience Manager > 도구 > Workspace 앱 오프라인 서비스 구성 > 지금 구성**&#x200B;으로 이동합니다.
1. **작업 공간 앱 오프라인 서비스** 페이지에서 **수동 리소스 캐시**&#x200B;를 클릭합니다.

   URL:https://&lt;서버>:&lt;포트>/libs/fd/workspace-offline/content/config.html

1. **수동 리소스 캐시** 탭에서 **+** 단추를 클릭하여 CRX 경로를 추가합니다.
1. **새 리소스 추가** 필드에 다음을 입력합니다./etc.clientlibs/fd/xfaforms/I18N/en_US.js을 클릭하고 **추가**&#x200B;를 클릭합니다.
1. **저장**&#x200B;을 클릭합니다.

## AEM Forms은 Windows {#aem-forms-do-not-sync-on-windows}에서 동기화되지 않습니다.

Windows의 AEM Forms 앱에서 양식 경로 또는 해당 리소스의 경로가 256자 이상 또는 같은 문자를 포함하는 경우 양식이 연결된 서버와 동기화되지 않습니다.

양식의 경로와 해당 리소스를 수정하여 문자 수를 256자 미만으로 줄입니다.

## 지원되지 않는 Gradle {#unsupported-version-of-gradle} 버전

**오류 메시지:** 프로젝트가 지원되지 않는 버전의 Gradle을 사용하고 있습니다.

Android Studio에서 AEM Forms 앱을 빌드할 때 오류 메시지가 표시됩니다. 시스템에서 지원되는 Grade 버전이 지원되지 않아 문제가 발생합니다.

**해결 방법:** Fix  **Gradle 래퍼를 클릭하고 프로젝트를 다시** 가져와 문제를 해결합니다.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle 및 Android Gradle 플러그인 호환성 문제 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**오류 메시지:** Android Gradle 플러그인 및 Gradle 버전이 호환되지 않습니다.

Android Studio 사용자 인터페이스의 **빌드** 메뉴에서 **APK** 옵션을 선택하면 오류 메시지가 표시됩니다.

![gradile_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**해상도:** Gradle  **Scripts** >  **gradle-wrapper.** properties 파일을 열고 distributionUrlproperty를  **** 편집합니다.

예를 들어 Android Studio 콘솔에서는 Gradle 버전을 3.5로 다운로드할 것을 권장합니다. **gradle-wrapper.properties** 파일의 **distributionUrl**&#x200B;에서 버전을 편집합니다.

**빌드** > **빌드 APK**&#x200B;를 다시 선택하여 오류를 해결하고 .apk 파일을 생성합니다.

![grade_wrapper_properties](assets/gradle_wrapper_properties.png)

