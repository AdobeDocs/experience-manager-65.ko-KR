---
title: MSM 우수 사례
seo-title: MSM 우수 사례
description: Adobe 엔지니어링 및 컨설팅 팀이 컴파일한 최상의 작업 방법을 찾아 AEM Multi Site Manager를 시작하고 실행하는 데 도움이 됩니다.
seo-description: Adobe 엔지니어링 및 컨설팅 팀이 컴파일한 최상의 작업 방법을 찾아 AEM Multi Site Manager를 시작하고 실행하는 데 도움이 됩니다.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
feature: Multi Site Manager
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 1%

---


# MSM 우수 사례{#msm-best-practices}

## 일반 {#general}

MSM은 콘텐츠 배포를 자동화하기 위한 구성 가능한 프레임워크입니다. 종종 구현에는 웹 사이트의 주요 부분과 조직 및 지리적 범위에 포함됩니다. 따라서 웹 사이트를 계획하는 대로 MSM 구현을 계획하는 것이 좋습니다.

* 구현을 시작하기 전에 **계획 구조와 콘텐츠 흐름**&#x200B;을 주의하십시오.
* **Live Copy의 양을 최소한으로 유지하십시오.** Live Copy 처리는 리소스를 많이 사용하는 작업입니다. 시스템에 Live Copy가 더 많을수록 성능이 더 영향을 받을 수 있습니다.내부 Live Copy 인덱스 처리, 롤아웃과 같은 Live Copy 작업 간, 사이트 관리자 참조 레일에 Live Copy 관계 표시와 같은 UI 작업에 이르기까지 다양한 작업이 가능합니다. Live Copy 관계가 사이트나 분기의 페이지에 상속되는 사이트의 사이트나 분기의 Live Copy를 만드는 것이 좋습니다. 전체 구조를 Live Copy로 만들 수 있는 경우 사이트나 분기의 페이지에 대한 개별 Live Copy를 만들지 마십시오.
* **필요에 따라 원하는 만큼 사용자 정의할 수 있습니다.** MSM은 높은 수준의 사용자 지정(예: 롤아웃 구성)을 지원하지만 일반적으로 웹 사이트의 성능, 안정성 및 업그레이드 가능성에 대한 우수 사례는 사용자 지정을 최소화하는 것입니다.
* **거버넌스** 모델을 일찍 설정하고 이에 따라 사용자를 교육하여 성공을 보장합니다. 거버넌스 관점에서 가장 좋은 방법은 로컬 컨텐츠 제작자가 다른 로컬 사용자와 해당 Live Copy에 컨텐츠를 할당/연결하기 위해 **의 권한을 최소화하는 것입니다.** 이는 비관리, 연쇄 상속이 MSM 구조의 복잡성을 상당히 증가시키고 성능과 안정성을 손상시킬 수 있기 때문입니다.

* 구조, 콘텐츠 흐름, 자동화 및 거버넌스 - **프로토타입을 작성하고 실시간 구현을 시작하기 전에 시스템을 철저히 테스트합니다.**
* **Adobe 컨설팅 및 선도적인 시스템 통합업체**&#x200B;는 MSM을 사용하여 컨텐츠 자동화를 계획하고 구현하는 경험이 있기 때문에 MSM 프로젝트를 시작하는 방법과 전체 구현 전반에서 모두 시작할 수 있습니다.

>[!NOTE]
>
>MSM 작업에 대한 자세한 내용은 기술 자료 문서에서 확인할 수 있습니다.
>
>* [MSM FAQ](https://helpx.adobe.com/experience-manager/kb/index/msm_faq.html)
>* [MSM 문제 해결](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>[참조 구성 요소](/help/sites-authoring/default-components-foundation.md#reference)를 사용하여 단일 페이지 또는 단락을 다시 사용할 수도 있습니다. 그러나 다음 사항에 유의하십시오.
>
>* MSM은 보다 유연하므로 동기화된 컨텐츠와 시기를 세부적으로 제어할 수 있습니다.
>* [이제 ](https://docs.adobe.com/content/help/ko-KR/experience-manager-core-components/using/introduction.html) 기본 구성 요소를 기본 구성 요소에 비해 권장합니다.

>



## Live Copy 소스 및 블루프린트 구성 {#live-copy-sources-and-blueprint-configurations}

Live Copy는 [일반 페이지](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 또는 [블루프린트 구성](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)을 사용하여 만들 수 있습니다. 두 가지 모두 유효한 사용 사례입니다.

블루프린트 구성을 사용하면 다음과 같은 이점이 있습니다.

* 작성자가 이 블루프린트에서 상속되는 Live Copy에 대한 수정 사항을 푸시할 때 블루프린트에 대해 **롤아웃** 옵션을 사용할 수 있도록 합니다.
* 작성자가 **사이트 만들기**;를 사용하도록 허용따라서 사용자는 손쉽게 언어를 선택하고 live copy 구조를 구성할 수 있습니다.
* 블루프린트와 관계가 있는 Live Copy에 대한 기본 롤아웃 구성을 정의합니다.

블루프린트 구성이 참조되지 않는 경우 롤아웃은 Live Copy 자체에서만 시작할 수 있으므로 기본적으로 소스에서 컨텐츠를 가져올 수 있습니다.

Live Copy를 사용하여 새 사이트를 만들 때 전체 MSM 기능 세트를 사용할 수 있도록 블루프린트 구성을 만드는 것이 좋습니다.

## 구성 요소 및 컨테이너 동기화 {#components-and-container-synchronization}

일반적으로 구성 요소 동기화에 대한 MSM의 롤아웃 규칙은 다음과 같습니다.

* 구성 요소는 블루프린트에 포함된 모든 리소스를 동기화하도록 롤아웃됩니다.
* 컨테이너는 현재 리소스만 동기화합니다.

즉, 구성 요소는 집계로 처리되고, 롤아웃에서 구성 요소 자체가 표시되고 모든 하위 요소는 블루프린트 안에 있는 구성 요소로 대체됩니다. 즉, 리소스가 해당 구성 요소에 로컬로 추가되는 경우 롤아웃 시 블루프린트의 콘텐츠로 손실됩니다.

로컬에 추가된 구성 요소가 롤아웃에서 유지 관리되도록 구성 요소 중첩을 지원하려면 구성 요소를 컨테이너로 선언해야 합니다. 예를 들어, 기본 parsys는 로컬로 추가된 컨텐츠를 지원할 수 있도록 컨테이너로 선언됩니다.

>[!NOTE]
>
>구성 요소에 속성 `cq:isContainer`을 추가하여 컨테이너로 지정합니다.

## 사이트 만들기 {#create-site}

AEM에는 Live Copy를 만드는 두 가지 주요 방법이 있습니다.

* [Live Copy 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   이 방법은 보다 일반적인 방법으로 간주하여 모든 페이지에서 Live Copy를 만들 수 있습니다. Live Copy의 컨텐츠 구조는 소스와 정확하게 일치합니다.

* [사이트](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)를 만드는 경우

   다국어 구조가 있는 웹 사이트를 제작하는 데 주로 사용됩니다.

사이트를 만들 때 고려해야 할 몇 가지 사항은 다음과 같습니다.

* 새 사이트를 만들려면 [블루프린트 구성](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)이 필요합니다.
* 새 사이트에서 만들 언어 경로를 선택하려면 해당 언어 루트가 블루프린트(소스)에 있어야 합니다.
* [새 사이트가 Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)(**Create** Then **사이트** 사용)으로 만들어지면 이 Live Copy의 처음 2개 수준은 *얕은*&#x200B;입니다. 페이지의 자식은 라이브 관계에 속하지 않지만, 트리거와 일치하는 라이브 관계가 발견되면 롤아웃이 여전히 내려갑니다.

   다음을 방지할 수 있습니다.

   * 블루프린트에서 수동으로 언어 추가(첫 번째 수준 아래)
   * 언어 루트 바로 아래에 컨텐츠를 수동으로 추가,
   * 롤아웃 시 이 새 내용을 live copy에 자동으로 전달하지 않습니다.

## MSM 및 다국어 웹 사이트 {#msm-and-multilingual-websites}

MSM은 다음과 같은 두 가지 방법으로 다국어 웹 사이트 제작을 지원할 수 있습니다.

* 언어 마스터를 만들 때.

   * MSM 자체에는 **이(가) 내용 번역**&#x200B;을 제공하지 않지만 제3자 번역 커넥터와 통합할 수 있습니다. 다음 사항에 주의하십시오.

      * MSM을 사용하면 페이지 및/또는 구성 요소 수준에서 상속을 취소할 수 있습니다. 이렇게 하면 다음 롤아웃 시 번역된 컨텐츠(live copy의 블루프린트에서 아직 번역되지 않은 컨텐츠로)를 덮어쓰는 것을 방지할 수 있습니다.
      * 일부 제3자 번역 커넥터는 MSM 상속 관리를 자동화합니다.

         자세한 내용은 번역 서비스 공급업체에 문의하십시오.

      * 언어 마스터를 만들고 번역하기 위한 또 다른 방법은 기본 AEM 변환 통합 프레임워크와 함께 언어 사본을 사용하는 것입니다.

* 언어 마스터에서 컨텐츠를 롤아웃할 때.

   * 예를 들어, 프랑스어(프랑스어) 마스터에서 프랑스/프랑스어, 캐나다/프랑스어, 스위스/프랑스어(캐나다) 등 국가별 사이트에 이르기까지 모든 언어 마스터에서

자세한 내용은 [다국어 사이트의 콘텐츠 번역](/help/sites-administering/translation.md) 및 [번역 우수 사례](/help/sites-administering/tc-bp.md)를 참조하십시오.

## 구조 변경 및 롤아웃 {#structure-changes-and-rollouts}

블루프린트/소스 트리에서 컨텐츠 구조를 수정하면 Live Copy에 다르게 반영됩니다. 이것은 수정 유형에 따라 달라집니다.

* **블루프린트** 에서 새 페이지를 만들면 표준 롤아웃 구성으로 롤아웃 후 Live Copy에서 해당 페이지가 생성됩니다.

* **블루프린트** 에서 페이지를 삭제하면 표준 롤아웃 구성으로 롤아웃 후 해당 페이지가 Live Copy에서 삭제됩니다.

* **표준** 롤아웃 구성을 사용하여 롤아웃 후 블루프린트의 페이지  **** 이동은 해당 페이지가 Live Copy로 이동되는 결과를 초래하지 않습니다.

   * 이러한 비헤이비어의 원인은 페이지 이동이 암시적으로 페이지 삭제를 포함하기 때문입니다. 작성자의 페이지를 삭제하면 게시 시 해당 컨텐츠가 자동으로 비활성화되므로 게시에서는 예기치 않은 동작이 발생할 수 있습니다. 링크, 책갈피 및 기타 같은 관련 항목에도 노크 효과를 적용할 수 있습니다.
   * 각 Live Copy 페이지의 컨텐츠 상속은 블루프린트에서 소스의 새 위치를 반영하도록 업데이트됩니다.
   * 블루프린트에서 Live Copy로 페이지가 이동하는 것을 완전히 실현하려면 다음 우수 사례를 고려하십시오.

>[!NOTE]
>
>이 작업은 [롤아웃 시 트리거](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers)에서만 작동합니다.

* 사용자 지정 롤아웃 구성을 만듭니다.

   * 이 새 구성에는 작업이 포함되어야 합니다.

      `PageMoveAction`

      이 구성에 다른 작업을 추가하지 마십시오.

* 새 구성을 배치합니다.

   * Live Copy의 이전 위치에서 각 페이지를 삭제하는 동안 페이지 이동을 완전히 롤아웃하려면:

      * 표준 롤아웃 구성 전에 새로 만든 구성을 배치합니다.

         표준 롤아웃 구성은 이전 위치에서 페이지를 삭제하는 것을 처리합니다.
   * 각 페이지를 Live Copy의 이전 위치에 보관하는 동안 페이지 이동을 롤아웃하려면(기본적으로 컨텐츠를 복제):

      * 표준 롤아웃 구성 뒤에 새로 만든 구성을 배치합니다.

         그러면 Live Copy에서 컨텐츠가 삭제되거나 게시에서 비활성화되지 않습니다.


## 역할 사용자 지정 {#customizing-rollouts}

MSM 롤아웃 구성은 사용자 지정이 매우 쉽습니다. 자동 롤아웃을 수행하면 결과가 상당히 높아집니다. 가장 좋은 방법은 *매우*&#x200B;를 신중하게 계획하는 것입니다. 예를 들면 다음과 같습니다.

* 자동 롤아웃;예를 들어 [onModify 트리거](#onmodify),
* [노드 유형/속성](#node-types-properties) 사용자 정의
* 후속 워크플로우 시작,
* 및/또는 롤아웃의 일부로 컨텐트 활성화.

### onModify {#onmodify}

[롤아웃 트리거](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`를 사용할 때는 다음 사항을 고려해야 합니다.

* `onModify` 트리거를 사용하여 롤아웃을 자동화하면 *모든* 페이지 수정 후 롤아웃을 트리거하므로 제작 성능에 부정적인 영향을 줄 수 있습니다.

* 롤아웃 결과는 다음과 같이 예상된 결과와 다를 수 있습니다.

   * 결과 수정 이벤트의 순서를 지정할 수 없습니다.
   * 이벤트 기반 아키텍처는 롤아웃 관리자에 전달된 이벤트의 시퀀스를 보장할 수 없습니다.

* 이러한 롤아웃 구성을 사용하면 동일한 리소스에 대한 동시 업데이트가 발생하는 경우 충돌 문제가 발생할 수 있습니다.

따라서 자동 롤아웃 시작 시 얻을 수 있는 성능 문제가 잠재적인 성능 문제보다 더 큰 경우 *만* 트리거를 사용하는 것이 좋습니다.`onModify`

### 노드 유형/속성 {#node-types-properties}

다음 사항을 기억하십시오.

* 롤아웃 작업을 사용자 지정하는 것 외에도 MSM을 사용하여 롤아웃되는 노드 속성을 사용자 지정할 수 있습니다. [MSM OSGi 구성을 사용하면 노드 유형](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization)이(가) 소스에서 Live Copy로 복사되지 않도록 제외할 수 있습니다.

## 추가 정보 {#further-information}

이 페이지와 다음 페이지에서는 관련 문제를 다룹니다.

* [Live Copy 만들기 및 동기화](/help/sites-administering/msm-livecopy.md)
* [Live Copy 개요 콘솔](/help/sites-administering/msm-livecopy-overview.md)
* [Live Copy 동기화 구성](/help/sites-administering/msm-sync.md)
* [MSM 롤아웃 충돌](/help/sites-administering/msm-rollout-conflicts.md)

