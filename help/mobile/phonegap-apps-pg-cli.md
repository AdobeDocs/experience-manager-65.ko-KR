---
title: PhoneGap CLI를 사용한 앱 개발
seo-title: PhoneGap CLI를 사용한 앱 개발
description: PhoneGap CLI를 사용한 앱 개발에 대해 알려면 이 페이지를 따르십시오.
seo-description: PhoneGap CLI를 사용한 앱 개발에 대해 알려면 이 페이지를 따르십시오.
uuid: 9a66171d-19af-40db-9c07-f5dd9561e1b5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 4a034e15-3394-4be3-9e8e-bc894668946a
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---

# PhoneGap CLI{#developing-apps-with-phonegap-cli}를 사용하여 앱 개발

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

개발 환경을 구성했다면 개발자로서 언제든지 장치 또는 에뮬레이터 내에서 앱을 실행할 수 있습니다.

다음 예제를 실행하려면 Xcode와 함께 OSx(Mac)를 실행하는 시스템 또는 Android SDK가 설치된 Mac/Win/Linux 시스템이 필요합니다.

## 개발 환경 Bootstrap {#bootstrap-your-development-environment}

[PhoneGap CLI 설정](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

iOS의 경우:iPhone과 iPad용으로 개발하려면 Apple의 Xcode IDE가 필요합니다.

* [여기](https://developer.apple.com/xcode/downloads/)에 무료로 다운로드하십시오.
* [PhoneGap iOS 플랫폼 안내서](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

Android의 경우:아이폰과 아이패드용으로 개발하려면 구글의 안드로이드 IDE가 필요하다.

* [여기](https://developer.android.com/sdk/index.html)에 무료로 다운로드하십시오.
* [PhoneGap Android 플랫폼 안내서](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## 소스 {#download-the-source} 다운로드

개발 환경을 성공적으로 부트하면 AEM 앱 빌드 타일에서 소스를 다운로드합니다.

* PhoneGap Build 타일 V자형 화살표를 클릭합니다.

![chlimage_1-45](assets/chlimage_1-45.png)

* 소스 다운로드를 클릭합니다.
* 다운로드 소스 모달에서 원하는 소스를 선택합니다.

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>개발 소스에는 스테이징되지 않은 변경 사항을 포함하는 동안 앱의 최신 상태가 포함되어 있습니다. 앱스토어 공급업체에 제출할 릴리스 후보 작성을 위해 스테이징 소스를 사용하십시오.
>
>앱을 스테이징하지 않은 경우 스테이징을 선택하면 스테이징 워크플로우가 트리거됩니다(힌트:이 경우 AppStore 및 Google PlayStore에서 사용할 수 있는 PhoneGap Enterprise Viewer 앱에서 준비된 앱으로 표시됩니다.

* 다운로드 를 클릭하고 ZIP을 컴퓨터에 저장합니다.
* 다운로드한 zip 파일을 작업 공간에 추출합니다.

## 앱을 빌드하고 로드합니다(소스에서) {#build-and-load-the-app-from-source}

PhoneGap CLI는 플랫폼 프로젝트를 만들고 소스를 컴파일하고 단일 명령으로 앱을 배포할 수 있습니다.

>[!NOTE]
>
>이 모든 단계를 별도로 수행할 수 있습니다. [PhoneGap CLI 문서](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/)를 참조하십시오.

1. PhoneGap CLI를 설치했는지 확인합니다. 위의 내용을 참조하십시오.
1. 콘솔(또는 터미널) 창에서 추출된 소스의 루트 디렉토리로 이동합니다.
1. 다음 명령을 입력합니다.

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>현재 문제가 있는 경우 기본 사항으로 돌아가 문제 해결 -
>
>1. 새 폴더 만들기(mkdir 테스트)
>1. 이 새 폴더(cd 테스트)로 이동합니다.
>1. &#39;phonegap create helloWorld&#39; 실행
>1. helloWorld(cd helloWorld)로 이동합니다.
>1. &#39;phonegap run android(또는 android를 위와 같이 ios로 바꾸기)를 실행합니다.
>1. 에뮬레이터는 JavaScript 브리지가 네이티브 방식으로 작동하는 경우 &#39;Device Ready&#39;라고 말하면서 새로 만든 PhoneGap 앱을 실행 중입니다.

>
>
이렇게 하면 PhoneGap CLI 개발 환경이 제대로 작동하고 있는지 확인할 수 있습니다.

## Safari 및 IOS 디버그를 사용하여 Javascript 디버그 {#debug-javascripts-with-safari-and-ios-debug}

웹 애플리케이션을 사용하는 것과 동일한 방식으로 Safari의 개발자 도구를 사용하여 앱의 JavaScript를 디버깅할 수 있습니다.

## Safari 개발자 도구 활성화 {#enable-safari-developer-tools}

개발자 도구를 활성화하려면

* Safari 기본 설정 열기

   * 메뉴 막대에서 Safari 클릭
   * 기본 설정을 클릭합니다

* 기본 설정 창에서 고급 을 클릭합니다

![chlimage_1-47](assets/chlimage_1-47.png)

* &quot;메뉴 모음에 개발 메뉴 표시&quot;를 선택합니다.
* 기본 설정 창을 닫습니다.

## Safari를 iOS에 연결 {#connect-safari-to-ios}

Safari를 iOS 장치 또는 에뮬레이터에 연결할 수 있습니다.

* 콘솔 창에서 추출된 소스의 루트 디렉토리로 이동합니다.
* 다음 명령을 입력하여 장치 또는 에뮬레이터에서 앱을 실행합니다.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Safari 열기
* 메뉴 모음에서 개발 을 클릭합니다
* iOS Simulator 하위 메뉴 선택
* home.html 을 클릭합니다.

![chlimage_1-48](assets/chlimage_1-48.png)

## Safari의 웹 관리자 {#debug-javascript-with-safari-s-web-inspector}를 사용하여 JavaScript 디버그

소스의 모든 위치에서 중단점을 설정할 수 있습니다. 에뮬레이터 또는 장치와 상호 작용할 때 앱 실행이 해당 중단됩니다. 실행을 단계별로 수행하고 변수의 값을 검사할 수 있습니다.

* 웹 검사기 창에서 리소스 를 클릭합니다
* 소스 트리를 탐색하고 원하는 소스 파일을 클릭합니다
* 중단점을 추가하려면 인접한 줄 번호를 클릭합니다
* 장치 또는 에뮬레이터와 상호 작용

![chlimage_1-49](assets/chlimage_1-49.png)

* 제어 단추를 사용하여 실행, 단계 오버, 단계 및 단계 내림 방법을 계속합니다.

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>변수 값을 보려면 현재 메서드에서 마우스를 가져갑니다.

## 다음 단계 {#the-next-steps}

PhoneGap CLI를 사용한 앱 개발에 대해 학습하면 [장치 기능 액세스](/help/mobile/phonegap-access-device-features.md)를 참조하십시오.
