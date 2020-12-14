---
title: AEM Forms 앱용 환경 설정
seo-title: AEM Forms 앱용 환경 설정
description: AEM Forms 앱을 빌드하고 배포할 하드웨어, 소프트웨어 및 라이센스.
seo-description: AEM Forms 앱을 빌드하고 배포할 하드웨어, 소프트웨어 및 라이센스.
uuid: 4123a6b7-5766-476c-9afb-f57029b148ad
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e6b01ade-7ea3-42a7-872d-cc35a3d2782a
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# AEM Forms 앱 환경 설정{#set-up-environment-for-aem-forms-app}

AEM Forms 앱을 빌드하고 배포하려면 다음 하드웨어, 소프트웨어 및 라이선스가 필요합니다.

## Windows 장치의 경우 {#for-windows-devices}

* Microsoft Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova용 Microsoft Visual Studio 도구

## iOS 장치의 경우 {#for-ios-devices}

* Mac OS X 10.9.5 이상을 실행하는 Intel 기반 Apple Mac
* iOS SDK 8.4 이상
* Xcode 버전:OS X 이상용 Xcode 6.4
* iOS Developer Enterprise 프로그램의 멤버십
* 사내 iOS 앱 배포를 위한 기업 인증서
* iOS 8.4 이상이 설치된 Apple iPad

## Android 장치의 경우 {#for-android-devices}

* [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)에서 다운로드할 수 있는 Android Development Toolkit(ADT 번들)
* MAC 시스템에 환경이 설정되어 있는 경우 ADT는 응용 프로그램 폴더에 설치해야 합니다.
* ADT가 MAC의 다른 위치에 설치되어 있거나 Windows 시스템에 환경이 설정되어 있는 경우 소스 아카이브 `mobileworkspace-src.zip`의 `src\android` 폴더에 있는 `local.properties` 파일에서 ADT SDK 경로를 업데이트해야 합니다. 이 파일에서 `sdk.dir` 변수를 바탕 화면에서 ADT SDK 위치를 가리킵니다.

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip에 PhoneGap SDK 5.0이 포함되어 있습니다. PhoneGap SDK가 사전 설치되어 있지 않은지 확인하십시오.
