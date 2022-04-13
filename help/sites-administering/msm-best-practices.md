---
title: MSM 모범 사례
description: AEM 다중 사이트 관리자를 시작하고 실행하는 데 도움이 되도록 Adobe 엔지니어링 및 컨설팅 팀이 컴파일한 우수 사례를 찾습니다.
topic-tags: site-features, best-practices
feature: Multi Site Manager
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: c6ccd204dbd514d6195424aff495bc38f1f31bce
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 1%

---

# MSM 모범 사례{#msm-best-practices}

## 일반 {#general}

MSM은 콘텐츠 배포를 자동화하기 위한 구성 가능한 프레임워크입니다. 구현에는 종종 웹 사이트의 주요 부분과 조직 및 지역 범위가 포함됩니다. 따라서 웹 사이트를 계획하는 대로 MSM 구현을 신중하게 계획하는 것이 좋습니다.

* 주의 깊게 **계획 구조 및 컨텐츠 흐름** 구현을 시작하기 전에
* **Live Copy 양을 최소한으로 유지합니다.** Live Copy 처리는 리소스를 많이 사용하는 작업입니다. 시스템에 Live Copy가 많을수록 성능에 더 많은 영향을 줄 수 있습니다. 내부 live copy 인덱스 처리에서 롤아웃과 같은 live copy 작업을 통해 사이트 관리자 참조 레일에 live copy 관계 표시와 같은 UI 작업에 이르기까지 가장 좋은 방법은 Live Copy 관계가 사이트 또는 분기의 페이지에 상속되는 사이트의 사이트 또는 분기의 Live Copy를 만드는 것입니다. 전체 구조를 Live Copy로 만들 수 있는 경우 사이트 또는 분기에서 페이지에 대한 개별 Live Copy를 생성하지 마십시오.
* **필요한 만큼 사용자 지정하되 가능한 한 적게 사용자 지정합니다.** MSM은 높은 수준의 사용자 지정(예: 롤아웃 구성)을 지원하는 반면 웹 사이트의 성능, 안정성 및 업그레이드 가능성에 대한 우수 사례는 사용자 지정을 최소화하는 것입니다.
* 설정 **거버넌스** 빨리 모델링하고 그에 따라 사용자를 교육시켜 성공을 보장하세요. 거버넌스 관점에서 모범 사례는 다음과 같습니다 **지역 컨텐츠 제작자들이 가지는 권한을 최소화하십시오** 컨텐츠를 다른 로컬 사용자와 해당 라이브 카피에 할당/접속하기 위해. 이것은 제어되지 않고 체인화된 상속이 MSM 구조의 복잡성을 크게 증가시키고 성능과 안정성을 손상시킬 수 있기 때문입니다.

* 구조, 컨텐츠 흐름, 자동화 및 거버넌스에 대한 계획이 수립되면 - **시스템 프로토타입 및 철저한 테스트**, 라이브 구현을 시작하기 전에
* 주의 사항 **Adobe 컨설팅 및 주요 시스템 통합업체** MSM을 사용하여 콘텐츠 자동화를 계획하고 구현하는 경험이 풍부하므로 MSM 프로젝트 및 전체 구현 시 둘 다 시작할 수 있습니다.

>[!NOTE]
>
>MSM 작업에 대한 자세한 내용은 기술 자료 문서를 참조하십시오.
>
>* [MSM 문제 해결 및 FAQ](troubleshoot-msm.md)
>


>[!NOTE]
>
>를 사용할 수도 있습니다 [참조 구성 요소](/help/sites-authoring/default-components-foundation.md#reference) 단일 페이지 또는 단락을 다시 사용하려면 다음을 수행하십시오. 그러나 다음 사항에 주의하십시오.
>
>* MSM은 보다 유연하며, 동기화 내용과 시기를 미세 제어할 수 있습니다.
>* [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko) 이제 기초 구성 요소보다 권장 됩니다.
>


## Live Copy 소스 및 블루프린트 구성 {#live-copy-sources-and-blueprint-configurations}

Live Copy는 다음 중 하나를 사용하여 만들 수 있습니다 [일반 페이지](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 또는 [블루프린트 구성](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 둘 다 유효한 사용 사례입니다.

블루프린트 구성을 사용하면 다음과 같은 이점이 있습니다.

* 작성자가 **롤아웃** 블루프린트의 옵션 - 이 블루프린트에서 상속되는 라이브 카피에 대한 수정 사항을 푸시할 대상.
* 작성자가 사용할 수 있도록 허용 **사이트 만들기**; 언어를 쉽게 선택하고 live copy 구조를 구성할 수 있습니다.
* 블루프린트와 관계가 있는 Live Copy에 대한 기본 롤아웃 구성을 정의합니다.

블루프린트 구성을 참조하지 않는 경우 Live Copy 자체에서만 롤아웃을 시작할 수 있으므로 기본적으로 소스에서 컨텐츠를 가져옵니다.

Live Copy를 사용하여 새 사이트를 만들 때 전체 MSM 기능 세트의 가용성을 보장하기 위해 블루프린트 구성을 만드는 것이 좋습니다.

>[메모!]
>
> 권한 탭의 CUG는 Blueprint의 Live Copy로 롤아웃할 수 없습니다. Live Copy를 구성할 때 이를 계획하십시오.

## 구성 요소 및 컨테이너 동기화 {#components-and-container-synchronization}

일반적으로 구성 요소 동기화에 대한 MSM의 롤아웃 규칙은 다음과 같습니다.

* 구성 요소는 블루프린트에 포함된 모든 리소스 동기화를 롤아웃합니다.
* 컨테이너는 현재 리소스만 동기화합니다.

즉, 구성 요소가 합계로 처리되고 롤아웃 시 구성 요소 자체가 사용되고 모든 해당 하위 구성 요소가 블루프린트의 합계로 대체됩니다. 즉, 리소스가 이러한 구성 요소에 로컬로 추가되는 경우 롤아웃 시 블루프린트의 콘텐츠로 손실됩니다.

로컬에 추가된 구성 요소가 롤아웃에서 유지 관리되도록 구성 요소 중첩을 지원하려면 구성 요소를 컨테이너로 선언해야 합니다. 예를 들어, 기본 parsys는 컨테이너로 선언되므로 로컬에서 추가한 컨텐츠를 지원할 수 있습니다.

>[!NOTE]
>
>속성 추가 `cq:isContainer` 를 구성 요소로 지정합니다.

## 사이트 만들기 {#create-site}

AEM에는 Live Copy를 만드는 두 가지 주요 접근 방식이 있습니다.

* When [live Copy 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   이 방법은 모든 페이지에서 Live Copy를 생성할 수 있도록 보다 일반적인 방법으로 간주할 수 있습니다. Live Copy의 컨텐츠 구조가 소스와 정확히 일치합니다.

* When [사이트 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   이는 주로 다국어 구조로 웹 사이트를 제작하는 데 사용되는 보다 전문적인 접근 방법입니다.

다음은 사이트를 만들 때 고려해야 할 몇 가지 고려 사항입니다.

* 새 사이트를 만들려면 [블루프린트 구성](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* 새 사이트에서 만들 언어 경로를 선택하려면 해당 언어 루트가 블루프린트(소스)에 있어야 합니다.
* 한 번 [새 사이트가 live copy로 만들어졌습니다.](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (사용 **만들기**, 그런 다음 **사이트**)를 채울 수 있습니다. *얕은*. 페이지의 하위 페이지는 라이브 관계에 속하지 않지만 트리거와 일치하는 라이브 관계가 발견되면 롤아웃이 계속 내려옵니다.

   이 방법은 다음을 방지할 수 있습니다.

   * 블루프린트에서 수동으로 언어 추가(첫 번째 수준 아래)
   * 언어 루트 바로 아래에 컨텐츠를 수동으로 추가,
   * 롤아웃 시 이 새 컨텐츠를 Live Copy로 자동으로 전달하지 않습니다.

## MSM 및 다국어 웹 사이트 {#msm-and-multilingual-websites}

MSM은 다음과 같은 두 가지 방법으로 다국어 웹 사이트를 만들 수 있습니다.

* 언어 마스터를 만들 때

   * MSM 자체 **콘텐츠 번역을 제공하지 않음**&#x200B;를 지원하는 타사 번역 커넥터와 통합할 수 있습니다. 참고 사항:

      * MSM을 사용하면 페이지 및/또는 구성 요소 수준에서 상속을 취소할 수 있습니다. 이렇게 하면 다음 롤아웃 시 번역된 컨텐츠(Live Copy에서 블루프린트에서 아직 번역되지 않은 컨텐츠로)를 덮어쓰는 것을 방지할 수 있습니다.
      * 일부 타사 번역 커넥터는 MSM 상속을 자동화합니다.

         자세한 내용은 번역 서비스 공급자에게 문의하십시오.

      * 언어 마스터를 만들고 번역할 수 있는 또 다른 방법은 AEM 기본 제공 번역 통합 프레임워크와 함께 언어 사본을 사용하는 것입니다.

* 언어 마스터에서 컨텐츠를 롤아웃할 때.

   * 예를 들어, 프랑스어 마스터 부터 프랑스/프랑스어, 캐나다/프랑스어, 스위스/프랑스어 등 국가별 사이트에 이르기까지 다양한 국가에서 사용할 수 있습니다.

자세한 내용은 [다국어 사이트의 컨텐츠 번역](/help/sites-administering/translation.md) 그리고 [번역 우수 사례](/help/sites-administering/tc-bp.md).

## 구조 변경 및 롤아웃 {#structure-changes-and-rollouts}

블루프린트/소스 트리의 컨텐츠 구조에 대한 수정 사항은 Live Copy에 다르게 반영됩니다. 이것은 수정 유형에 따라 달라집니다.

* **만들기** 블루프린트의 새 페이지는 표준 롤아웃 구성을 사용하여 롤아웃 후 Live Copy에서 해당 페이지가 생성됩니다.

* **삭제** 블루프린트의 페이지는 표준 롤아웃 구성을 사용하여 롤아웃 후 Live Copy에서 해당 페이지가 삭제됩니다.

* **이동** 블루프린트의 페이지는 **not** 표준 롤아웃 구성을 사용하여 롤아웃 후 Live Copy에서 해당 페이지가 이동됩니다.

   * 이 동작의 이유는 페이지 이동이 암시적으로 페이지 삭제를 포함하기 때문입니다. 이로 인해 작성자에서 페이지를 삭제하면 게시 시 해당 컨텐츠가 자동으로 비활성화되므로 게시 시 예기치 않은 동작이 발생할 수 있습니다. 링크, 책갈피 및 기타 항목과 같은 관련 항목에 노크 효과가 있을 수도 있습니다.
   * 각 Live Copy 페이지의 컨텐츠 상속은 블루프린트에서 해당 소스의 새 위치를 반영하도록 업데이트됩니다.
   * 블루프린트에서 Live Copy로 페이지 이동을 완전히 실현하려면 다음 우수 사례를 고려하십시오.

>[!NOTE]
>
>이 작업은 [롤아웃 트리거 시](/help/sites-administering/msm-sync.md#rollout-triggers).

* 사용자 지정 롤아웃 구성을 만듭니다.

   * 이 새 구성에는 작업이 포함되어야 합니다.

      `PageMoveAction`

      이 구성에 다른 작업을 추가하지 마십시오.

* 새 구성을 배치합니다.

   * Live Copy에서 이전 위치에서 각 페이지를 삭제하는 동안 페이지 이동을 완전히 롤아웃하려면:

      * 표준 롤아웃 구성 전에 새로 만든 구성을 배치합니다.

         표준 롤아웃 구성에서는 이전 위치에서 페이지를 삭제하는 작업이 수행됩니다.
   * 각 페이지를 Live Copy에서 이전 위치에 유지한 채 페이지 이동을 롤아웃하려면(기본적으로 컨텐츠가 복제됨):

      * 표준 롤아웃 구성 뒤에 새로 만든 구성을 배치합니다.

         이렇게 하면 Live Copy에서 컨텐츠가 삭제되거나 게시에서 비활성화되지 않습니다.


## 롤아웃 사용자 지정 {#customizing-rollouts}

MSM 롤아웃 구성은 사용자 지정이 매우 가능합니다. 롤아웃 자동화는 매우 큰 결과를 초래할 수 있습니다. 모범 사례로는 계획을 세워야 합니다 *매우* 주의 사항:

* 롤아웃 자동화 예를 들어 [onModify 트리거](#onmodify),
* 사용자 지정 [노드 유형/속성](#node-types-properties),
* 후속 워크플로우 시작
* 롤아웃의 일부로 컨텐츠 및/또는 활성화.

### onModify {#onmodify}

를 사용할 때 [롤아웃 트리거](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` 다음 사항을 고려해야 합니다.

* 롤아웃 자동화 `onModify` 트리거는 이후에 롤아웃을 트리거하므로 작성 성능에 부정적인 영향을 줄 수 있습니다 *매* 페이지 수정.

* 롤아웃 결과는 다음과 같이 예상되는 결과와 다를 수 있습니다.

   * 결과 수정 이벤트의 순서를 지정할 수 없습니다.
   * 이벤트 기반 아키텍처는 롤아웃 관리자에 전달된 이벤트의 시퀀스를 보장할 수 없습니다.

* 이러한 롤아웃 구성을 사용하면 동일한 리소스의 동시 업데이트가 발생하는 경우 커밋 충돌이 발생할 수 있습니다.

따라서 다음을 수행하는 것이 좋습니다 *전용* 사용 `onModify` 자동 롤아웃 시작의 이점이 잠재적 성능 문제를 능가하면 트리거됩니다.

### 노드 유형/속성 {#node-types-properties}

다음 사항을 기억하십시오.

* MSM을 사용하면 롤아웃 작업을 사용자 정의할 수 있을 뿐만 아니라 롤아웃되는 노드 속성을 사용자 지정할 수도 있습니다. 다음 [MSM OSGi 구성을 사용하여 노드 유형을 제외할 수 있습니다](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) 소스에서 Live Copy로 복사되는 중입니다.

## 추가 정보 {#further-information}

이 페이지와 다음 페이지에서는 관련 문제를 다룹니다.

* [라이브 카피 생성 및 동기화](/help/sites-administering/msm-livecopy.md)
* [라이브 카피 개요 콘솔](/help/sites-administering/msm-livecopy-overview.md)
* [라이브 카피 동기화 구성](/help/sites-administering/msm-sync.md)
* [MSM 롤아웃 충돌](/help/sites-administering/msm-rollout-conflicts.md)
