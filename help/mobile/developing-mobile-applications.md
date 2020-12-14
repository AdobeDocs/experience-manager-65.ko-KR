---
title: AEM에서 모바일 애플리케이션 개발
seo-title: AEM에서 모바일 애플리케이션 개발
description: Adobe PhoneGap Enterprise를 사용하여 AEM에서 모바일 애플리케이션을 개발하기 시작하려면 이 페이지를 따르십시오.
seo-description: Adobe PhoneGap Enterprise를 사용하여 AEM에서 모바일 애플리케이션을 개발하기 시작하려면 이 페이지를 따르십시오.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---


# AEM {#developing-mobile-applications-in-aem}에서 모바일 응용 프로그램 개발

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM은 Adobe PhoneGap 및 Adobe 게시 솔루션을 활용하므로, 컨텐츠가 풍부한 컨텐츠와 유틸리티 기반의 크로스 플랫폼 모바일 애플리케이션을 모두 제작하고 관리할 수 있습니다.

* 모든 회사 모바일 앱을 한 곳에서 관리할 수 있습니다.
* 프로비저닝 프로필의 번거로움 없이 개발 및 스테이징 환경에서 앱을 검토하고 공유를 위해 앱을 빌드하고 업로드해야 합니다.
* AEM 제작 환경을 사용하여 앱에 사용할 리치 컨텐츠를 만들고 관리할 수 있습니다.
* Adobe PhoneGap과 함께 HTML5를 사용하면 디바이스 기반의 기능을 통해 풍부한 경험을 제작할 수 있습니다.
* Cordova WebViews를 통해 신규 또는 기존 **기본** 응용 프로그램에 HTML5 웹 보기를 도입합니다.
* 웹, 모바일 웹, 모바일 앱, 인쇄 등 모든 전달 채널에서 리치 멀티미디어 컨텐츠를 제작, 조정 및 공유할 수 있습니다.

AEM은 Adobe **[PhoneGap Build 서비스](https://build.phonegap.com/)**&#x200B;와 통합되어 응용 프로그램 빌드 및 배포 프로세스를 단순화합니다.

**Adobe** ContentSync를 사용하면 애플리케이션을 다시 설치하거나 appStore, Google Play 또는 기타 앱 소스에서 다운로드할 필요 없이 페이지 및 컨텐츠 업데이트를 OTA(Over-the-Air)를 디바이스로 손쉽게 다운로드할 수 있습니다.

**Adobe** Analytics는 AEM 앱과 완벽하게 통합되어 있으므로 배포, 지리적 위치, 운영 체제, 디바이스, 클릭 스트림, iBeacon 추적 등에 대한 세부 추적 기능을 사용할 수 있습니다.

## 앱 만들기 {#creating-apps}

개발자는 [AEM PhoneGap 시작 키트](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit)와 [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps)에 있는 추가 리소스를 함께 사용하여 Cordova 웹 보기를 실행하는 참조 기본 앱을 포함하여 PhoneGap을 사용하여 AEM 앱을 부트스트래핑할 수 있습니다.

Starter Kit Git 리포지토리에 대한 읽어보기: 시작 키트 사용 자습서를 포함합니다.

* 브랜딩 사용자 정의
* 샘플 빌드 및 배포 타겟
* 소스 제어 저장소 구성
* 로컬 또는 원격 AEM 인스턴스 설치 및 배포
* AEM에서 제거

>[!NOTE]
>
>labs를 비롯한 추가 참조 구현 출처는 GitHub [여기](https://github.com/adobe-marketing-cloud-apps) 및 &quot;kitchen-sink&quot; 소스 [여기](https://github.com/blefebvre/aem-phonegap-kitchen-sink)에서 찾을 수 있습니다.

## IOS 9 및 HTTP 호스트 {#developing-for-ios-and-http-hosts}용 개발

IOS 개발자는 iOS 9에서 실행되는 Cordova 앱의 개방 문제를 알고 있어야 합니다. 이 문제는 안전하지 않은 호스트에 대한 요청이 수행되지 않도록 합니다(예: *http://localhost:4502*). 이 문제는 Cordova CLI에서 사용되던 Cordova-ios의 예정된 릴리스로 해결되지만 그 동안 다음과 같은 2가지 해결 방법이 있습니다.

1. 즉각적인 해결 방법은 아무 문제 없이 iOS 8 시뮬레이터를 사용할 수 있습니다.
1. iOS 9를 사용해야 하는 경우 앱 -Info.plist(&quot;&lt;app root>/platforms/ios/&lt;app name>/&lt;app name>-Info.plist&quot;에서 `cordova platform add ios`을 실행한 후 찾음) 파일을 수동으로 편집하여 다음 속성을 포함할 수 있습니다.

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>&quot;앱 전송 보안&quot;에 대한 자세한 내용은 [Apple의 iOS9 베타 버전 문서](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) 및 이 [스택 오버플로 토론](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)의 다음 섹션을 참조하십시오.

## AEM {#developing-mobile-applications-in-aem-1}에서 모바일 응용 프로그램 개발

* [AEM PhoneGap 시작](/help/mobile/starting-aem-phonegap-app.md)
* [모바일 애플리케이션 구축](/help/mobile/building-app-mobile-phonegap.md)
* [앱 구조](/help/mobile/phonegap-structure-an-app.md)
* [앱 콘솔을 사용하여 앱 만들기 및 편집](/help/mobile/phonegap-apps-console.md)
* [SPA(Single Page Applications)](/help/mobile/phonegap-single-page-applications.md)
* [PhoneGap CLI를 사용하여 앱 개발](/help/mobile/phonegap-apps-pg-cli.md)
* [장치 기능 액세스](/help/mobile/phonegap-access-device-features.md)
* [Adobe 모바일 분석을 사용하여 앱 성능 추적](/help/mobile/phonegap-intro-to-app-analytics.md)
* [모바일 애플리케이션에 Adobe Analytics 추가](/help/mobile/phonegap-add-analytics-to-apps.md)
* [알림 푸시](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile 콘텐츠 개인화](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [앱의 구조](/help/mobile/phonegap-apps-arch.md)
* [하이브리드 앱이 AEM Mobile용으로 준비되었습니까?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 추가 리소스 {#additional-resources}

관리자 및 개발자의 역할 및 책임을 살펴보려면 아래 리소스를 참조하십시오.

* [AEM을 사용한 Adobe PhoneGap Enterprise 저작](/help/mobile/phonegap.md)
* [AEM에서 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)
