---
title: AEM에서 모바일 애플리케이션 개발
seo-title: Developing Mobile Applications in AEM
description: Adobe PhoneGap Enterprise를 사용하여 AEM에서 모바일 애플리케이션 개발을 시작하려면 이 페이지에 따르십시오.
seo-description: Follow this page to start developing mobile application in AEM using Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# AEM에서 모바일 애플리케이션 개발 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM은 Adobe PhoneGap과 Adobe Publishing Solution을 활용하여 컨텐츠 풍부하고 유틸리티 기반의 교차 플랫폼 모바일 애플리케이션을 모두 만들고 관리할 수 있습니다.

* 모든 회사 모바일 앱을 한 곳에서 관리합니다.
* 프로비저닝 프로필의 복잡성과 공유를 위해 앱을 빌드하고 업로드하는 추가 작업 없이 개발 및 스테이징 환경에서 앱을 검토하십시오.
* AEM 작성 환경을 사용하여 앱에 사용할 풍부한 컨텐츠를 만들고 관리합니다.
* 장치 기본 기능을 사용하여 풍부한 경험을 만들려면 Adobe PhoneGap과 함께 HTML5를 사용하십시오.
* 신규 또는 기존 웹 사이트에 HTML5 웹 뷰 소개 **기본** Cordova WebViews를 통한 응용 프로그램.
* 웹, 모바일 웹, 모바일 앱 및 인쇄를 포함한 모든 게재 채널에서 다양한 멀티미디어 컨텐츠를 제작, 조정 및 공유할 수 있습니다.

AEM은 Adobe과 통합됩니다 **[PhoneGap Build 서비스](https://build.phonegap.com/)** 응용 프로그램 빌드 및 배포 프로세스를 단순화합니다.

**Adobe ContentSync** 앱을 다시 설치하거나 appStore, Google Play 또는 기타 앱 소스에서 다운로드할 필요 없이 사용자가 페이지 및 콘텐츠 업데이트 OTA(Over-the-Air)를 해당 장치에 쉽게 다운로드할 수 있습니다.

**Adobe Analytics** 는 AEM 앱에 완전히 통합되어 있어 배포, 지리적 위치, 운영 체제, 장치, 클릭 스트림, iBeacon 추적 등에 대한 세부 추적을 수행할 수 있습니다.

## 앱 만들기 {#creating-apps}

개발자는 [AEM PhoneGap 시작 키트](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) 에 있는 추가 리소스와 [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) Cordova 웹 보기를 실행하는 참조 기본 앱을 포함하여 PhoneGap를 사용하여 AEM 앱을 부트스트랩합니다.

Starter Kit Git 저장소의 추가 정보에는 시작 키트를 사용하기 위한 자습서가 포함되어 있습니다.

* 브랜딩 사용자 지정
* Maven 샘플 빌드 및 배포 대상
* 소스 제어 저장소 구성
* 로컬 또는 원격 AEM 인스턴스에 설치 및 배포
* AEM에서 제거

>[!NOTE]
>
>labs를 비롯한 추가 참조 구현 소스는 GitHub에서 찾을 수 있습니다 [여기](https://github.com/adobe-marketing-cloud-apps) 그리고, &quot;부엌 싱크대&quot; [여기](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## IOS 9 및 HTTP 호스트를 위한 개발 {#developing-for-ios-and-http-hosts}

iOS 개발자는 iOS 9에서 실행되는 Cordova 앱의 공개 문제를 알고 있어야 합니다. 이 문제는 안전하지 않은 호스트(예: *http://localhost:4502*). 이 문제는 향후 cordova-ios 릴리스(Cordova CLI에서 사용)로 해결되지만, 그 동안에는 다음 두 가지 해결 방법이 있습니다.

1. 즉각적인 해결 방법으로, 문제 없이 iOS 8 시뮬레이터를 사용할 수 있습니다.
1. iOS 9을 사용해야 하는 경우 앱 - Info.plist(실행 후 발견됨)가 `cordova platform add ios` in &quot;&lt;app root=&quot;&quot;>/platforms/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>-Info.plist&quot;) 파일을 수동으로 편집하여 다음 속성을 포함할 수 있습니다.

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>&quot;앱 전송 보안&quot;에 대한 자세한 내용은 [Apple의 iOS9 사전 릴리스 문서](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) 그리고 [스택 오버플로 토론](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## AEM에서 모바일 애플리케이션 개발 {#developing-mobile-applications-in-aem-1}

* [AEM PhoneGap 시작](/help/mobile/starting-aem-phonegap-app.md)
* [모바일 애플리케이션 제작](/help/mobile/building-app-mobile-phonegap.md)
* [앱 구조](/help/mobile/phonegap-structure-an-app.md)
* [앱 콘솔을 사용한 앱 만들기 및 편집](/help/mobile/phonegap-apps-console.md)
* [SPA (Single Page Applications)](/help/mobile/phonegap-single-page-applications.md)
* [PhoneGap CLI를 사용한 앱 개발](/help/mobile/phonegap-apps-pg-cli.md)
* [액세스 장치 기능](/help/mobile/phonegap-access-device-features.md)
* [Adobe Mobile Analytics를 사용하여 앱 성능 추적](/help/mobile/phonegap-intro-to-app-analytics.md)
* [모바일 애플리케이션에 Adobe Analytics 추가](/help/mobile/phonegap-add-analytics-to-apps.md)
* [알림 푸시](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile 콘텐츠 개인화](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [앱의 해부학](/help/mobile/phonegap-apps-arch.md)
* [하이브리드 앱을 AEM Mobile에 사용할 준비가 되었습니까?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 추가 리소스 {#additional-resources}

관리자 및 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM으로 Adobe PhoneGap Enterprise용 작성](/help/mobile/phonegap.md)
* [AEM을 통해 Adobe PhoneGap Enterprise에 대한 컨텐츠 관리](/help/mobile/administer-phonegap.md)
