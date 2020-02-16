---
title: PhoneGap CLI를 사용하여 앱 개발
seo-title: PhoneGap CLI를 사용하여 앱 개발
description: PhoneGap CLI를 사용한 앱 개발에 대해 알려면 이 페이지를 따르십시오.
seo-description: PhoneGap CLI를 사용한 앱 개발에 대해 알려면 이 페이지를 따르십시오.
uuid: 9a66171d-19af-40db-9c07-f5dd9561e1b5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 4a034e15-3394-4be3-9e8e-bc894668946a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# PhoneGap CLI를 사용하여 앱 개발{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

개발 환경을 구성한 경우 언제든지 개발자는 디바이스 또는 에뮬레이터 내에서 앱을 실행할 수 있습니다.

다음 예제를 실행하려면 Xcode와 함께 OSx(Mac) 또는 Android SDK가 설치된 Mac/Win/Linux 시스템을 실행하는 시스템이 필요합니다.

## 개발 환경의 부트스트랩 {#bootstrap-your-development-environment}

[PhoneGap CLI 설정](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

iOS의 경우:iPhone 및 iPad용으로 개발하려면 Apple의 Xcode IDE가 필요합니다.

* 무료로 [다운로드하십시오](https://developer.apple.com/xcode/downloads/).
* [PhoneGap iOS 플랫폼 가이드](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

Android의 경우:iPhone 및 iPad용으로 개발하려면 Google의 Android Studio IDE가 필요합니다.

* 무료로 [다운로드하십시오](https://developer.android.com/sdk/index.html).
* [PhoneGap Android 플랫폼 가이드](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## 소스 다운로드 {#download-the-source}

개발 환경을 성공적으로 보완하면 AEM App 빌드 타일에서 소스를 다운로드합니다.

* PhoneGap Build tile chevron(PhoneGap 빌드 타일) 드롭다운을 클릭합니다.

![chlimage_1-45](assets/chlimage_1-45.png)

* 소스 다운로드를 클릭합니다.
* 다운로드 소스 모달에서 원하는 소스를 선택합니다.

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>개발 소스에는 스테이징되지 않은 변경 사항을 포함하여 앱의 최신 상태가 포함되어 있습니다. App Store 업체에 제출하기 위한 릴리스 후보용 준비 소스를 사용하십시오.
>
>앱을 스테이징하지 않는 경우 스테이징을 선택하면 스테이징 워크플로가 트리거됩니다(힌트:AppStore 및 Google PlayStore에서 제공되는 PhoneGap Enterprise Viewer 앱에 스테이지된 앱으로 표시됩니다.)

* 다운로드를 클릭하고 컴퓨터에 ZIP을 저장합니다.
* 다운로드한 zip 파일을 작업 영역에 추출합니다.

## 앱 빌드 및 로드(출처) {#build-and-load-the-app-from-source}

PhoneGap CLI는 플랫폼 프로젝트를 만들고 소스를 컴파일하고 단일 명령으로 앱을 배포할 수 있습니다.

>[!NOTE]
>
>이러한 모든 단계를 개별적으로 수행할 수 있습니다. PhoneGap [CLI 문서를](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/)참조하십시오.

1. PhoneGap CLI를 설치했는지 확인하십시오. 위의 참조
1. 콘솔(또는 터미널) 창에서 압축을 푼 소스의 루트 디렉토리로 이동합니다.
1. 다음 명령을 입력합니다.

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>이 시점에서 문제가 있는 경우 기본 사항으로 돌아가 문제 해결 -
>
>1. 새 폴더 만들기(mkdir 테스트)
>1. 이 새 폴더로 이동(cd 테스트)
>1. &#39;phonegap create helloWorld&#39;를 실행합니다.
>1. helloWorld로 이동(cd helloWorld)
>1. &#39;phonegap run android(또는 위와 같이 Android를 ios로 바꾸기)를 실행합니다.
>1. JavaScript Bridge를 기본적으로 실행하는 경우 &#39;Device Ready&#39;라고 말하면서, 새로 만든 PhoneGap 앱을 실행하면 에뮬레이터가 열립니다.
>
>
이렇게 하면 PhoneGap CLI 개발 환경이 제대로 실행되고 있는지 확인합니다.

## Safari 및 IOS 디버깅을 사용하여 JavaScripts 디버그 {#debug-javascripts-with-safari-and-ios-debug}

웹 애플리케이션과 마찬가지로 Safari 개발자 도구를 사용하여 앱의 JavaScript를 디버깅할 수 있습니다.

## Safari 개발자 도구 활성화 {#enable-safari-developer-tools}

개발자 도구를 활성화하려면:

* Safari의 환경 설정 열기

   * 메뉴 모음에서 Safari 클릭
   * 환경 설정을 클릭합니다.

* 기본 설정 창에서 고급을 클릭합니다

![chlimage_1-47](assets/chlimage_1-47.png)

* &quot;메뉴 모음에 현상 메뉴 표시&quot;를 선택합니다.
* 기본 설정 창 닫기

## iOS에 Safari 연결 {#connect-safari-to-ios}

Safari를 iOS 장치 또는 에뮬레이터에 연결할 수 있습니다.

* 콘솔 창에서 압축을 푼 소스의 루트 디렉토리로 이동합니다.
* 다음 명령을 입력하여 장치 또는 에뮬레이터에서 앱을 실행합니다.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Safari 열기
* 메뉴 모음에서 현상 클릭
* iOS 시뮬레이터 하위 메뉴 선택
* home.html을 클릭합니다.

![chlimage_1-48](assets/chlimage_1-48.png)

## Safari의 웹 관리자를 사용하여 JavaScript 디버그 {#debug-javascript-with-safari-s-web-inspector}

소스의 모든 위치에서 중단점을 설정할 수 있습니다. 에뮬레이터 또는 장치와 상호 작용하는 경우 해당 중단점에서 앱 실행이 중지됩니다. 실행을 단계별로 실행하고 변수의 값을 검사할 수 있습니다.

* 웹 검사기 창에서 리소스 클릭
* 소스 트리를 탐색하고 원하는 소스 파일을 클릭합니다.
* 중단점을 추가하려면 인접한 줄 번호를 클릭합니다.
* 디바이스 또는 에뮬레이터와 인터랙션

![chlimage_1-49](assets/chlimage_1-49.png)

* 제어 단추를 사용하여 실행, 단계, 단계 및 메서드 내부와 단계 내부로 계속 이동합니다.

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>변수의 값을 보려면 현재 메서드에서 마우스를 가져갑니다.

## 다음 단계 {#the-next-steps}

PhoneGap CLI를 사용하여 앱 개발에 대해 알려면 디바이스 기능 [액세스를 참조하십시오](/help/mobile/phonegap-access-device-features.md).
