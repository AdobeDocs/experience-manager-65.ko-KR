---
title: 모바일 앱 테스트
description: 다양한 도구를 사용하여 모바일 앱을 자동화하거나 수동으로 테스트하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
exl-id: e10e1904-7016-4eb0-9408-36297285f378
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# 모바일 앱 테스트{#testing-mobile-apps}

{{ue-over-mobile}}

시장에 출시된 다양한 디바이스와 출시되는 디바이스를 고려할 때 앱 테스트가 반드시 필요합니다. 이 영역은 기능 및 사용성이 앱스토어에서 낮은 평가를 받을 수 있지만, 한 번의 오류로 인해 앱이 제거될 수 있는 영역입니다. 테스트 계획 및 품질 보증에 세심한 주의를 기울여야 합니다. 다음 링크에서는 환경 식별, 테스트 사례 정의, 테스트 유형, 가정 및 고객 참여와 같이 일반적으로 해결해야 하는 많은 주제를 다룹니다. 또한 테스트 작업에 도움이 되는 도구에 대해서도 설명합니다. [Hobbes](/help/sites-developing/hobbes.md)와 같은 내부 도구는 웹 기반 UI 테스트에 도움이 될 수 있습니다. [힘든 날](/help/sites-developing/tough-day.md)은(는) 시뮬레이션된 부하로 인스턴스에 스트레스를 줄 수 있습니다. 테스트 환경에서 Selenium과 같은 타사 도구를 이미 사용한 경우 이러한 도구도 사용할 수 있습니다.

모바일 앱을 개발할 때, 기존 테스트의 문제와 함께 해결해야 하는 디바이스 고유의 새로운 문제가 많습니다.

* 기능 - 앱에서 모든 요구 사항을 충족합니까?
* 유용성 - 고객이 앱을 쉽게 사용하고 이해할 수 있습니까?
* 성능 - 사용량이 급증하는 동안 발생하는 작업 스와이프와 캐러셀 같은 앱 요소가 빠르고 경험을 손상시키지 않습니까?
* 실패 또는 중단 - 앱이 실행되는 동안 들어오는 호출 또는 알림이 있을 때 어떻게 됩니까? 네트워크가 중단되거나 전원이 꺼지면 어떻게 됩니까?
* 설치 및 업데이트 - 설치 경험은 어떻습니까? 업데이트는 어떻게 푸시됩니까?
* 기술 - 앱이 장치에서 너무 많은 전력을 소비합니까?
* 로컬라이제이션 - 앱의 모든 영역이 번역됩니까?
* 인증 - 앱이 인증되었습니까? 모든 데이터 개인 정보 보호 법적 요구 사항을 준수한다고 고객이 신뢰할 수 있습니까?

이러한 질문은 자동화된 테스트 및 수동 테스트 중에 답변되어야 합니다.

## 자동화된 테스트 {#automated-testing}

다양한 화면 크기, 메모리 제한, 입력 방법 및 운영 체제를 다루기 위해 어느 정도의 자동화된 테스트를 수행해야 합니다. 많은 테스트 사례를 다룰 뿐만 아니라 새로운 기능이나 장치가 도입되면 회귀 테스트 속도를 높일 수 있다. 가장 좋은 방법은 자동화 툴이 노력의 중복을 줄이거나 제한하는 것입니다. 모든 플랫폼에서 테스트 작업을 적용할 수 있도록 도구 또는 프레임워크를 사용합니다. 다음 차트는 웹 기반 UI 테스트와 모바일 앱 테스트 모두를 위한 테스트 환경의 간소화된 구조를 보여 줍니다. 차트의 왼쪽에는 브라우저가 있는 일련의 Selenium 노드가 표시됩니다. SeleniumGrid는 이러한 모든 노드에 대해 공통적인 웹 기반 UI 테스트를 팜아웃할 수 있습니다. Selenium 허브는 플랫폼 간 앱 테스트를 위해 Appium에 연결할 수도 있습니다. 표시된 것은 시뮬레이터이지만 Android™용 adb 및 iOS 장치용 Xcode 유틸리티를 통합할 수 있습니다. 링크는 이 문서의 후반부에 제공되며, 여기에서 언급된 도구에 대한 특정 세부 정보를 찾을 수 있습니다.

![chlimage_1](assets/chlimage_1.jpeg)

## 수동 테스트 {#manual-testing}

자동화된 테스트 외에도 앱은 수동 테스트 주기를 거쳐야 합니다. 실제 디바이스에서 앱을 실행하는 고객은 스크립트로 복제할 수 없습니다. 여기도 여러 가지 옵션이 있습니다 HokeyApp과 같은 플랫폼을 사용하여 액세스 권한이 있는 사용자를 정의하고 피드백을 수집할 수 있습니다. 또는 UTest, ElusiveStars 또는 Testn과 같은 서비스에 전체 프로세스를 아웃소싱할 수 있습니다. 내부 테스터 그룹이 있지만 디바이스의 변형이 부족한 경우 디바이스 풀에서 수동 테스트를 수행할 수 있는 클라우드 서비스가 있습니다. 이를 제공하는 서비스 중 하나가 SauceLabs입니다. 또한 PhoneGap Enterprise에 원격으로 앱을 빌드하고 승인 테스트 또는 데모 수준으로 로컬 장치에 설치할 수 있습니다. 최신 기능 및 설명서는 PhoneGap(`https://phonegap.com/`) 웹 사이트를 참조하십시오. 어떤 방법을 사용하든 수동 테스트는 다음 작업을 수행해야 합니다.

* 대규모 테스터를 공격하고
* 대규모 장치 풀(이상적으로는 실제 장치이지만 실제 장치를 사용할 수 없는 경우 시뮬레이터/에뮬레이터)에 대해 테스트합니다.
* 유용한 피드백 제공:

   * 충돌 보고,
   * 분석/추적,
   * 유용성,
   * 주의 영역,
   * 성능,
   * 데이터/전력 소비 등.

## 도구 {#tools}

모바일 앱을 테스트하는 데 사용할 수 있는 다양한 도구가 있습니다. 사용할 기능 선택은 특정 상황(기능, 가격, 지원, 적용 범위 등)을 기반으로 해야 합니다. 다음은 사용 가능한 도구 및 서비스 중 일부에 대한 간략한 설명입니다.

**Selenium**

* WebDriver를 제공하고 다양한 브라우저를 제어하는 테스트 스크립트용 API를 포함하는 프레임워크입니다.
* Appium과 함께 사용하여 실제 장치에서 테스트할 수 있습니다.
* SeleniumGrid는 병렬 테스트를 위해 노드 간에 테스트를 지시합니다.
* Selenium IDE는 테스트 사례 작성을 줄이는 데 도움이 됩니다.

자세한 내용은 [https://www.selenium.dev/](https://www.selenium.dev/)을(를) 참조하십시오.

**Testdroid**

* 지속적인 통합 후크와 실제 디바이스 테스트를 갖춘 클라우드 기반 테스트 서비스.
* 장치 호환성을 확인하고, 로그를 분석하고, 보기를 트래버스하고, 스크린샷을 촬영하고, 성능을 모니터링하는 앱 크롤러가 포함됩니다.

자세한 내용은 [https://testdroid.com/](https://testdroid.com/)을(를) 참조하십시오.

**앱**

* Appium은 모바일 테스트 자동화를 위한 인기 있는 크로스 플랫폼 프레임워크입니다.
* 또한 검사자는 코드 테스트 사례를 돕는 기록 기능을 갖추고 있습니다.

자세한 내용은 [https://appium.io/](https://appium.io/)을(를) 참조하십시오.

**SauceLabs**

* SauceLabs는 클라우드 기반 테스트를 제공하며 지속적인 통합과 통합됩니다.
* 테스트는 클라우드 환경에서 자동으로 실행되거나 특정 장치 또는 플랫폼을 시작하고 수동 테스트를 수행하여 문제를 디버깅할 수 있습니다.

자세한 내용은 [https://saucelabs.com/](https://saucelabs.com/)을(를) 참조하십시오.

<!-- **AppTestNow**

* An outsourcing service that tests your mobile apps.
* Included is a large pool of devices and offers a wide range of types of testing: performance, quality, functional, certification, localization, data consumption, and so on.

For more information, see [https://apptestnow.com/](https://apptestnow.com/). -->

**HokeyApp**

* 하키앱은 테스터가 다운로드하여 사용해 볼 수 있는 개인 앱스토어에 모바일 앱을 푸시하는 수동 테스트에 해당됩니다.

자세한 내용은 [https://hockeyapp.net/features/](https://hockeyapp.net/features/)을(를) 참조하십시오.

**Jenkins**

* 테스트 도구는 아니지만 Jenkins는 자동화된 테스트를 위한 중추를 제공하는 지속적인 통합 프레임워크입니다. 다양한 서드파티 플러그인을 사용하여 기능을 확장할 수 있습니다. 예를 들어 SeleniumGrid 플러그인은 Selenium 허브 및 노드를 관리하는 데 도움이 되는 UI를 제공합니다.

자세한 내용은 [https://www.jenkins.io/](https://www.jenkins.io/) 및 [https://plugins.jenkins.io/](https://plugins.jenkins.io/)을(를) 참조하십시오.
