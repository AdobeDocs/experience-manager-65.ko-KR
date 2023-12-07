---
title: AEM Forms 앱을 위한 환경 설정
description: AEM Forms 앱을 빌드하고 배포하기 위한 하드웨어, 소프트웨어 및 라이센스입니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1d1f9db2-83cf-4612-ac8c-d2638c3bbaea
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# AEM Forms 앱을 위한 환경 설정{#set-up-environment-for-aem-forms-app}

AEM Forms 앱을 빌드하고 배포하려면 다음 하드웨어, 소프트웨어 및 라이선스가 필요합니다.

## Windows 디바이스용 {#for-windows-devices}

* Microsoft® 윈도우
* Microsoft® Visual Studio 2015
* Microsoft® Visual Studio Tools for Apache Cordova

## iOS 디바이스용 {#for-ios-devices}

* macOS X 10.9.5 이상을 실행하는 인텔 기반 Apple Mac
* iOS SDK 8.4 이상
* Xcode 버전: OS X용 Xcode 6.4 이상
* iOS Developer Enterprise 프로그램 멤버십
* 사내 iOS 앱 배포를 위한 엔터프라이즈 인증서
* Apple iPad 및 iOS 8.4 이상

## Android™ 디바이스용 {#for-android-devices}

* 에서 다운로드할 수 있는 Android™ Development Toolkit(ADT 번들) [https://developer.android.com/studio](https://developer.android.com/studio)
* 환경이 Mac 시스템에 설정된 경우 Applications 폴더에 ADT를 설치해야 합니다.
* ADT가 Mac의 다른 위치에 설치되었거나 환경이 Windows 시스템에 설정된 경우 ADT SDK 경로를에서 업데이트해야 합니다 `local.properties` 파일. 이 파일은 다음에서 사용할 수 있습니다. `src\android` 추출된 소스 아카이브의 폴더 `mobileworkspace-src.zip`. 이 파일에서 `sdk.dir` 변수를 데스크탑의 ADT SDK 위치에 매핑합니다.

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip에는 PhoneGap SDK 5.0이 포함되어 있습니다. PhoneGap SDK가 사전 설치되어 있지 않은지 확인하십시오.
