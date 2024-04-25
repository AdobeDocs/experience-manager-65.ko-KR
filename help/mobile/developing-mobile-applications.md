---
title: AEM에서 모바일 애플리케이션 개발
description: Adobe PhoneGap Enterprise를 사용하여 AEM에서 모바일 애플리케이션 개발을 시작하려면 이 페이지를 따르십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# AEM에서 모바일 애플리케이션 개발 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

AEM은 Adobe PhoneGap 및 Adobe 게시 솔루션을 사용하여 다양한 컨텐츠와 유틸리티 기반의 크로스 플랫폼 모바일 애플리케이션을 모두 만들고 관리할 수 있습니다.

* 모든 회사 모바일 앱을 한 곳에서 관리할 수 있습니다.
* 프로비저닝 프로필의 복잡성과 공유를 위해 앱을 빌드 및 업로드하기 위한 추가 노력 없이 개발 및 스테이징 환경에서 앱을 검토합니다.
* 이 AEM 저작 환경 사용하여 앱에 대한 다양한 컨텐츠 만들고 관리.
* HTML5와 Adobe PhoneGap을 함께 사용하면 디바이스 기본 기능으로 풍부한 경험을 만들 수 있습니다.
* 신규 또는 기존 Webviews에 HTML5 소개 **기본** Cordova WebViews를 통한 애플리케이션.
* 웹, 모바일 웹, 모바일 앱 및 인쇄를 포함한 모든 게재 채널에서 풍부한 멀티미디어 콘텐츠를 만들고, 선별하고 공유할 수 있습니다.

AEM은 Adobe PhoneGap Build 서비스와 통합됩니다(`https://build.phonegap.com/`)을 클릭하여 애플리케이션 빌드 및 배포 프로세스를 단순화합니다.

**Adobe ContentSync** 를 사용하면 앱을 다시 설치하거나 appStore, Google Play 또는 기타 앱 소스에서 다운로드할 필요 없이 OTA(Over-the-Air)로 페이지 및 콘텐츠 업데이트를 장치에 쉽게 다운로드할 수 있습니다.

**Adobe Analytics** 는 AEM 앱에 완전히 통합되어 배포, 지리적 위치, 운영 체제, 장치, 클릭 스트림, iBeacon 추적 등을 자세히 추적할 수 있습니다.

## 앱 만들기 {#creating-apps}

개발자는 [AEM PhoneGap 시작 키트](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) 에 있는 추가 리소스와 함께 [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) Cordova 웹 보기를 실행하는 참조 기본 앱을 포함하여 PhoneGap으로 AEM 앱을 부트스트랩합니다.

시작 키트 Git 저장소 추가 정보에는 시작 키트 사용에 대한 튜토리얼 내용이 포함되어 있습니다.

* 브랜딩 사용자 지정
* Maven 샘플 빌드 및 배포 대상
* 소스 제어 저장소 구성
* 로컬 또는 원격 AEM 인스턴스에 설치 및 배포
* AEM에서 제거

>[!NOTE]
>
>labs를 비롯한 추가 참조 구현 소스는 GitHub에서 확인할 수 있습니다 [여기](https://github.com/adobe-marketing-cloud-apps) and, the &quot;kitchen-sink&quot; source [여기](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## iOS 9 및 HTTP 호스트를 위한 개발 {#developing-for-ios-and-http-hosts}

IOS 개발자는 iOS 9에서 실행되는 Cordova 앱의 진행 중 문제에 대해 알고 있어야 합니다. 이 문제는 비보안 호스트(예: *http://localhost:4502*). 이 문제는 예정된 Cordova-ios(Cordova CLI에서 사용) 릴리스를 통해 해결되지만, 그 동안에는 다음 두 가지 해결 방법을 사용할 수 있습니다.

1. 즉각적인 해결 방법으로 iOS 8 시뮬레이터를 문제없이 계속 사용할 수 있습니다.
1. iOS 9를 사용해야 하는 경우 앱 -Info.plist(&quot;&lt;app root=&quot;&quot;>/platforms/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>-Info.plist&quot;에서 실행된 후 발견됨) 파일을 수동으로 편집하여 다음 속성 포함시킬 수 있습니다.&lt;/app>&lt;/app>&lt;/app> `cordova platform add ios`

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>&quot;앱 전송 보안&quot;에 대한 자세한 내용은 Apple의 iOS9 시험판 문서](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) 및 이 [Stack Overflow 토론](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)의 [다음 섹션을 참조하세요.

## AEM 에서 모바일 애플리케이션 개발 {#developing-mobile-applications-in-aem-1}

* [AEM PhoneGap 시작](/help/mobile/starting-aem-phonegap-app.md)
* [모바일 애플리케이션 구축](/help/mobile/building-app-mobile-phonegap.md)
* [앱 구조](/help/mobile/phonegap-structure-an-app.md)
* [앱 콘솔을 사용하여 앱 만들기 및 편집](/help/mobile/phonegap-apps-console.md)
* [SPA (Single Page Applications)](/help/mobile/phonegap-single-page-applications.md)
* [PhoneGap CLI를 사용한 앱 개발](/help/mobile/phonegap-apps-pg-cli.md)
* [장치 기능 액세스](/help/mobile/phonegap-access-device-features.md)
* [Adobe Systems Mobile Analytics를 사용하여 앱 성능 추적](/help/mobile/phonegap-intro-to-app-analytics.md)
* [모바일 애플리케이션에 Adobe Analytics 추가](/help/mobile/phonegap-add-analytics-to-apps.md)
* [알림 푸시](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile 컨텐츠 개인화](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [앱 분석](/help/mobile/phonegap-apps-arch.md)
* [하이브리드 앱이 AEM Mobile에 대해 준비되었습니까?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 추가 리소스 {#additional-resources}

관리자와 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM을 사용한 Adobe PhoneGap Enterprise 작성](/help/mobile/phonegap.md)
* [AEM을 사용하여 Adobe PhoneGap Enterprise에 대한 컨텐츠 관리](/help/mobile/administer-phonegap.md)
