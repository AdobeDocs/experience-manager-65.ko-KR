---
title: 지속 가능한 업그레이드
description: Adobe Experience Manager 6.4의 지속 가능한 업그레이드에 대해 알아보십시오.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 지속 가능한 업그레이드{#sustainable-upgrades}

## 사용자 지정 프레임워크 {#customization-framework}

### 아키텍처 (기능 / 인프라 / 콘텐츠 / 애플리케이션)  {#architecture-functional-infrastructure-content-application}

사용자 지정 프레임워크 기능은 업그레이드할 수 없는 코드(예: API) 또는 콘텐츠(예: 오버레이)의 확장 불가능한 영역에서 위반을 줄이는 데 도움이 되도록 설계되었습니다.

사용자 지정 프레임워크에는 두 가지 구성 요소인 **API 표면** 및 **콘텐츠 분류**.

#### API 표면 {#api-surface}

이전 Adobe Experience Manager(AEM) 릴리스에서는 많은 API가 Uber Jar를 통해 노출되었습니다. 이러한 API 중 일부는 고객이 사용하도록 의도되지 않았지만 번들 전반에서 AEM 기능을 지원하도록 노출되었습니다. 앞으로 Java™ API는 고객에게 업그레이드 컨텍스트에서 안전하게 사용할 수 있는 API를 나타내기 위해 공개 또는 비공개로 표시됩니다. 기타 세부 사항은 다음과 같습니다.

* 로 표시된 Java™ API `Public` 사용자 지정 구현 번들에서 사용하고 참조할 수 있습니다.

* 공개 API는 호환성 패키지 설치와 하위 호환됩니다.
* 호환성 패키지에는 이전 버전과의 호환성을 보장하기 위한 호환성 Uber JAR이 포함되어 있습니다
* 로 표시된 Java™ API `Private` 는 사용자 지정 번들이 아닌 AEM 내부 번들에서만 사용하도록 설계되었습니다.

>[!NOTE]
>
>의 개념 `Private` 및 `Public` 이러한 맥락에서 공적 계급과 사적 계급의 자바™ 개념과 혼동되어서는 안 된다.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### 컨텐츠 분류 {#content-classifications}

AEM은 고객이 AEM 기능을 확장하고 사용자 정의할 수 있도록 하기 위해 오랫동안 오버레이 및 Sling 리소스 병합의 주도권을 사용했습니다. AEM 콘솔 및 UI를 구동하는 사전 정의된 기능은에 저장됩니다. **/libs**. 고객은 아래의 내용을 수정할 수 없습니다. **/libs** 아래에 컨텐츠를 추가할 수 있음 **/apps** 에 정의된 기능을 오버레이하고 확장합니다. **/libs** 자세한 내용은 오버레이를 사용하여 개발 을 참조하십시오. 이로 인해 AEM을 의 콘텐츠로 업그레이드할 때 여전히 많은 문제가 발생합니다 **/libs** 가 변경되어 오버레이 기능이 예기치 않은 방식으로 중단될 수 있습니다. 고객은 상속을 통해 AEM 구성 요소를 확장할 수도 있습니다. `sling:resourceSuperType`또는 의 구성 요소를 간단히 참조 **/libs** sling:resourceType을 통해 직접 참조 및 재정의 사용 사례와 관련하여 유사한 업그레이드 문제가 발생할 수 있습니다.

고객이 의 영역을 보다 안전하고 쉽게 이해할 수 있도록 지원 **/libs** 콘텐츠를 사용하고 오버레이하는 것이 안전합니다. **/libs** 은 다음 mixin으로 분류됩니다.

* **공용(granite:PublicArea)** - 노드를 오버레이하고 상속할 수 있도록 공용으로 정의합니다( `sling:resourceSuperType`) 또는 직접 사용( `sling:resourceType`). 공용으로 표시된 /libs 아래의 노드는 호환성 패키지를 추가하여 안전하게 업그레이드할 수 있습니다. 일반적으로 고객은 공개로 표시된 노드만 사용해야 합니다.

* **요약(granite:AbstractArea)** - 노드를 추상으로 정의합니다. 노드를 오버레이하거나 상속할 수 있음( `sling:resourceSupertype`) 직접 사용되지 않는 것( `sling:resourceType`).

* **Final(granite:FinalArea)** - 노드를 최종으로 정의합니다. 최종으로 분류된 노드는 이상적으로 오버레이 또는 상속되지 않아야 합니다. 최종 노드는 다음을 통해 직접 사용할 수 있습니다. `sling:resourceType`. 최종 노드 아래의 하위 노드는 기본적으로 내부로 간주됩니다.

* ***내부(granite:InternalArea)*** *- *노드를 내부로 정의합니다. 내부로 분류된 노드는 이상적으로 오버레이되거나 상속되거나 직접 사용되어서는 안 됩니다. 이러한 노드는 AEM의 내부 기능만을 위한 것입니다

* **주석 없음** - 노드는 트리 계층 구조를 기반으로 분류를 상속합니다. / 루트는 기본적으로 공용입니다. **상위 노드가 Internal 또는 Final로 분류된 노드도 Internal로 처리됩니다.**

>[!NOTE]
>
>이러한 정책은 Sling 검색 경로 기반 메커니즘에 대해서만 적용됩니다. 의 기타 영역 **/libs** 클라이언트측 라이브러리가 다음과 같이 표시될 수 있습니다. `Internal`, 하지만 여전히 표준 clientlib 포함에 사용할 수 있습니다. 이러한 경우 고객이 내부 분류를 계속 준수하는 것이 중요합니다.

#### CRXDE Lite 컨텐츠 유형 표시기 {#crxde-lite-content-type-indicators}

CRXDE Lite에 적용된 Mixin은 다음으로 표시된 컨텐츠 노드 및 트리를 보여 줍니다. `INTERNAL` 흐리게 표시(회색으로 표시)됩니다. 대상 `FINAL`를 지정하면 아이콘만 흐리게 표시됩니다. 이러한 노드의 자 피쳐도 흐리게 표시됩니다. 이 두 경우 모두에서 오버레이 노드 기능이 비활성화됩니다.

**공용**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Final**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**내부**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**컨텐츠 상태 확인**

>[!NOTE]
>
>AEM Adobe 6.5부터는 패턴 감지기를 사용하여 컨텐츠 액세스 위반을 감지하는 것이 좋습니다. 패턴 탐지기 보고서가 더 상세하고, 더 많은 문제를 탐지하고, 긍정 오류(false positive)의 확률을 줄입니다.
>
>자세한 내용은 [패턴 감지기를 사용한 업그레이드 복잡성 평가](/help/sites-deploying/pattern-detector.md).

AEM 6.5는 오버레이되거나 참조된 콘텐츠가 콘텐츠 분류와 일치하지 않는 방식으로 사용되는 경우 고객에게 경고하기 위해 상태 확인과 함께 제공됩니다.

** Sling/Granite 컨텐츠 액세스 검사**는 고객 코드가 AEM의 보호된 노드에 잘못 액세스하는지 저장소를 모니터링하는 새로운 상태 검사입니다.

이 검사 **/apps** 일반적으로 완료하는 데 몇 초 정도 소요됩니다.

이 새 상태 검사에 액세스하려면 다음을 수행하십시오.

1. AEM 홈 화면에서 다음으로 이동합니다. **도구 > 작업 > 상태 보고서**
1. 클릭 **Sling/Granite 컨텐츠 액세스 검사**.

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

검사가 완료되면, 최종 사용자에게 잘못 참조되고 있는 보호된 노드를 알리는 경고 목록이 나타납니다.

![스크린샷-2018-2-5healthreports](assets/screenshot-2018-2-5healthreports.png)

위반을 해결하면 녹색 상태로 돌아갑니다.

![screenshot-2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

상태 검사에는 모든 Sling 검색 경로에서 오버레이 또는 리소스 유형이 사용될 때마다 비동기적으로 확인하는 백그라운드 서비스에서 수집한 정보가 표시됩니다. 컨텐츠 mixin을 잘못 사용하면 위반을 보고합니다.
