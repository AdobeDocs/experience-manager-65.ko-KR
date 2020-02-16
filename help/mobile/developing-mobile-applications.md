---
title: AEM에서 모바일 애플리케이션 개발
seo-title: AEM에서 모바일 애플리케이션 개발
description: Adobe PhoneGap Enterprise를 사용하여 AEM에서 모바일 애플리케이션 개발을 시작하려면 이 페이지를 따르십시오.
seo-description: Adobe PhoneGap Enterprise를 사용하여 AEM에서 모바일 애플리케이션 개발을 시작하려면 이 페이지를 따르십시오.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM에서 모바일 애플리케이션 개발 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM은 Adobe PhoneGap 및 Adobe Publishing Solutions를 활용하므로, 컨텐츠가 풍부한 및 유틸리티 기반 크로스 플랫폼 모바일 애플리케이션을 모두 만들고 관리할 수 있습니다.

* 모든 모바일 앱을 중앙에서 관리
* 프로비저닝 프로필의 복잡한 준비 과정 없이 개발 및 스테이징 환경에서 앱을 검토하고 공유를 위해 앱을 빌드하고 업로드합니다.
* AEM 작성 환경을 사용하여 앱에 사용할 리치 컨텐츠를 만들고 관리할 수 있습니다.
* Adobe PhoneGap과 함께 HTML5를 사용하면 디바이스 기반의 기능을 통해 풍부한 경험을 제작할 수 있습니다.
* Cordova WebViews를 통해 신규 또는 기존 **기본** 애플리케이션에 HTML5 웹뷰를 소개합니다.
* 웹, 모바일 웹, 모바일 앱, 인쇄 등 모든 전달 채널에서 리치 멀티미디어 컨텐츠를 제작, 조정 및 공유할 수 있습니다.

AEM은 Adobe PhoneGap **[Build 서비스와](https://build.phonegap.com/)**통합되므로 애플리케이션 빌드 및 배포 프로세스를 간소화할 수 있습니다.

**Adobe ContentSync를** 통해 사용자는 애플리케이션을 다시 설치하거나 appStore, Google Play 또는 기타 앱 소스에서 다운로드할 필요 없이 OTA(Over-the-Air)를 통해 디바이스로 손쉽게 페이지 및 컨텐츠 업데이트를 다운로드할 수 있습니다.

**Adobe Analytics** 는 AEM 앱과 완벽하게 통합되어 배포, 지리적 위치, 운영 체제, 디바이스, 클릭 스트림, iBeacon 추적 등에 대한 자세한 추적을 지원합니다.

## 앱 만들기 {#creating-apps}

개발자는 AEM PhoneGap [시작 키트와](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) https://github.com/adobe-marketing-cloud-apps에 [있는 추가 리소스를 사용하여 Cordova 웹 보기를 실행하는 참조 기본 앱을](https://github.com/adobe-marketing-cloud-apps) 포함하여 PhoneGap을 사용하여 AEM앱을 부트스트래핑할 수 있습니다.

Starter Kit Git 보관소의 읽어보기 파일에는 시작 키트 사용에 대한 자습서가 포함되어 있습니다.

* 브랜딩 사용자 정의
* Maven 샘플 빌드 및 배포 타겟
* 소스 제어 저장소 구성
* 로컬 또는 원격 AEM 인스턴스에 설치 및 배포
* AEM에서 제거

>[!NOTE]
>
>랩을 비롯한 추가 참조 구현 소스는 [여기에서](https://github.com/adobe-marketing-cloud-apps) GitHub 및 &quot;키친 싱크&quot; 소스를 [확인할 수 있습니다](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## IOS 9 및 HTTP 호스트에 대한 개발 {#developing-for-ios-and-http-hosts}

IOS 개발자는 iOS 9에서 실행되는 Cordova 앱의 미해결 문제를 알고 있어야 합니다. 이 문제는 안전하지 않은 호스트(예: http://localhost:4502)에 요청이 *수행되지 않도록 합니다*. 이 문제는 예정된 cordova-ios 릴리스(Cordova CLI에 의해 사용됨)로 해결되지만 그 동안 두 가지 해결 방법이 있습니다.

1. 즉각적인 해결 방법으로 문제 없이 iOS 8 시뮬레이터를 사용할 수 있습니다.
1. iOS 9를 사용해야 하는 경우 앱 -Info.plist(&quot;&lt;앱 루트>/platforms/ios/&lt;앱 이름>/&lt;앱 이름>-Info.plist&quot; 실행 후 `cordova platform add ios` 찾음) 파일을 수동으로 편집하여 다음 속성을 포함할 수 있습니다.

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>&quot;App Transport Security&quot;에 대한 자세한 내용은 Apple의 iOS9 [베타 버전 문서](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) 및 이 스택 오버플로우 [토론의](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)다음 섹션을 참조하십시오.

## AEM에서 모바일 애플리케이션 개발 {#developing-mobile-applications-in-aem-1}

* [AEM PhoneGap 시작](/help/mobile/starting-aem-phonegap-app.md)
* [모바일 애플리케이션 구축](/help/mobile/building-app-mobile-phonegap.md)
* [앱 구조](/help/mobile/phonegap-structure-an-app.md)
* [앱 콘솔을 사용하여 앱 만들기 및 편집](/help/mobile/phonegap-apps-console.md)
* [단일 페이지 애플리케이션](/help/mobile/phonegap-single-page-applications.md)
* [PhoneGap CLI를 사용하여 앱 개발](/help/mobile/phonegap-apps-pg-cli.md)
* [장치 기능 액세스](/help/mobile/phonegap-access-device-features.md)
* [Adobe Mobile Analytics를 사용하여 앱 성능 추적](/help/mobile/phonegap-intro-to-app-analytics.md)
* [모바일 애플리케이션에 Adobe Analytics 추가](/help/mobile/phonegap-add-analytics-to-apps.md)
* [알림 푸시](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile 콘텐츠 개인화](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [앱의 구조](/help/mobile/phonegap-apps-arch.md)
* [하이브리드 앱이 AEM Mobile용으로 준비되어 있습니까?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 추가 리소스 {#additional-resources}

관리자 및 개발자의 역할과 책임에 대한 자세한 내용은 아래 리소스를 참조하십시오.

* [AEM 파섹](/help/mobile/phonegap.md)
* [AEM을 사용하여 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)
