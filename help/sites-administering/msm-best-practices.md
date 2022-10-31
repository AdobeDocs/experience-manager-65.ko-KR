---
title: MSM 모범 사례
description: AEM 다중 사이트 관리자를 시작하고 실행하는 데 도움이 되도록 Adobe 엔지니어링 및 컨설팅 팀이 컴파일한 우수 사례를 찾습니다.
topic-tags: site-features, best-practices
feature: Multi Site Manager
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 41%

---

# MSM 모범 사례{#msm-best-practices}

## 일반 {#general}

MSM은 콘텐츠 배포 자동화를 위한 구성 가능 프레임워크입니다. 구현은 종종 웹 사이트의 주요 부분을 포함하며 조직과 지역에 걸쳐 있습니다. 따라서 웹 사이트를 계획할 때와 마찬가지로 MSM 구현을 신중하게 계획하는 것이 좋습니다.

* 구현을 시작하기 전에 **구조 및 콘텐츠 흐름을 계획**&#x200B;하십시오.
* **Live Copy 양을 최소한으로 유지합니다.** Live Copy 처리는 리소스를 많이 사용하는 작업입니다. 시스템에 Live Copy가 많을수록 성능에 더 많은 영향을 줄 수 있습니다. 내부 live copy 인덱스 처리에서 롤아웃과 같은 live copy 작업을 통해 사이트 관리자 참조 레일에 live copy 관계 표시와 같은 UI 작업에 이르기까지 가장 좋은 방법은 Live Copy 관계가 사이트 또는 분기의 페이지에 상속되는 사이트의 사이트 또는 분기의 Live Copy를 만드는 것입니다. 전체 구조를 Live Copy로 만들 수 있는 경우 사이트 또는 분기에서 페이지에 대한 개별 Live Copy를 생성하지 마십시오.
* **필요한 만큼, 하지만 가능한 적게 맞춤화하십시오.** MSM은 높은 수준의 사용자 지정(예: 롤아웃 구성)을 지원하는 반면 웹 사이트의 성능, 안정성 및 업그레이드 가능성에 대한 우수 사례는 사용자 지정을 최소화하는 것입니다.
* 성공을 보장하려면 초기에 **거버넌스** 모델을 수립하고 그에 따라 사용자를 교육하십시오. 거버넌스 관점에서 모범 사례는 다음과 같습니다 **지역 컨텐츠 제작자들이 가지는 권한을 최소화하십시오** 컨텐츠를 다른 로컬 사용자와 해당 라이브 카피에 할당/접속하기 위해. 통제되지 않는 연결된 상속은 MSM 구조의 복잡성을 크게 증가시키고 성능과 안정성을 손상시킬 수 있기 때문입니다.

* 구조, 컨텐츠 흐름, 자동화 및 거버넌스에 대한 계획이 수립되면 - **시스템 프로토타입 및 철저한 테스트**, 라이브 구현을 시작하기 전에
* **Adobe 컨설팅 및 주요 시스템 통합업체**&#x200B;는 MSM을 통한 콘텐츠 자동화 계획 및 구현에 대한 풍부한 경험을 바탕으로 MSM 프로젝트 시작 및 전체적인 구현에 도움이 될 수 있습니다.

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
>* [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 이제 기초 구성 요소보다 권장 됩니다.
>


## 라이브 카피 소스 및 블루프린트 구성 {#live-copy-sources-and-blueprint-configurations}

Live Copy는 다음 중 하나를 사용하여 만들 수 있습니다 [일반 페이지](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 또는 [블루프린트 구성](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 두 가지 모두 유용한 사용 사례입니다.

블루프린트 구성을 사용할 때의 추가적인 이점은 다음과 같습니다.

* 작성자가 **롤아웃** 블루프린트의 옵션 - 이 블루프린트에서 상속되는 라이브 카피에 대한 수정 사항을 푸시할 대상.
* 작성자가 사용할 수 있도록 허용 **사이트 만들기**; 언어를 쉽게 선택하고 live copy 구조를 구성할 수 있습니다.
* 블루프린트와 관계가 있는 Live Copy에 대한 기본 롤아웃 구성을 정의합니다.

블루프린트 구성을 참조하지 않는 경우 Live Copy 자체에서만 롤아웃을 시작할 수 있으므로 기본적으로 소스에서 컨텐츠를 가져옵니다.

Live Copy를 사용하여 새 사이트를 만들 때 전체 MSM 기능 세트의 가용성을 보장하기 위해 블루프린트 구성을 만드는 것이 좋습니다.

>[!NOTE]
>
>권한 탭의 CUG는 블루프린트에서 라이브 카피로 롤아웃할 수 없습니다. 라이브 카피를 구성할 때 이를 염두에 두고 계획을 세우십시오.

## 구성 요소 및 컨테이너 동기화 {#components-and-container-synchronization}

일반적으로 구성 요소 동기화와 관련된 MSM의 롤아웃 규칙은 다음과 같습니다.

* 구성 요소는 블루프린트에 포함된 리소스를 동기화하여 롤아웃합니다.
* 컨테이너는 현재 리소스만 동기화합니다.

이는 구성 요소는 총계로 취급되며 롤아웃 시 구성 요소 자체 및 모든 하위 항목은 블루프린트의 구성 요소 및 하위 항목으로 대체됨을 의미합니다. 즉, 이러한 구성 요소에 리소스를 로컬로 추가하면 이는 롤아웃 시 블루프린트 콘텐츠로 손실됩니다.

로컬로 추가된 구성 요소가 롤아웃 시 유지되도록 구성 요소의 중첩을 지원하려면 해당 구성 요소를 컨테이너로 선언해야 합니다. 예를 들어, 기본 parsys는 컨테이너로 선언되므로 로컬에서 추가한 컨텐츠를 지원할 수 있습니다.

>[!NOTE]
>
>구성 요소에 `cq:isContainer` 속성을 추가하여 이를 컨테이너로 지정하십시오.

## 사이트 생성 {#create-site}

AEM에는 Live Copy를 만드는 두 가지 주요 접근 방식이 있습니다.

* When [live Copy 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   이 방법은 모든 페이지에서 Live Copy를 생성할 수 있도록 보다 일반적인 방법으로 간주할 수 있습니다. Live Copy의 컨텐츠 구조가 소스와 정확히 일치합니다.

* When [사이트 만들기](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   이는 주로 다국어 구조로 웹 사이트를 제작하는 데 사용되는 보다 전문적인 접근 방법입니다.

다음은 사이트를 만들 때 고려해야 할 몇 가지 고려 사항입니다.

* 새 사이트를 만들 때는 [블루프린트 구성](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations)이 필요합니다.
* 새 사이트에 생성할 언어 경로를 선택하려면 해당하는 언어 루트가 블루프린트(소스)에 존재해야 합니다.
* 한 번 [새 사이트가 live copy로 만들어졌습니다.](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (사용 **만들기**, 그런 다음 **사이트**)를 채울 수 있습니다. *얕은*. 페이지의 하위 항목은 라이브 관계에 속하지 않지만, 트리거와 일치하는 라이브 관계가 있는 경우 롤아웃은 계속 적용됩니다.

   이 방법은 다음을 방지할 수 있습니다.

   * 블루프린트에서 수동으로 언어 추가(첫 번째 수준 아래)
   * 언어 루트 바로 아래에 컨텐츠를 수동으로 추가,
   * 롤아웃 시 이 새 컨텐츠를 Live Copy로 자동으로 전달하지 않습니다.

## MSM 및 다국어 웹 사이트 {#msm-and-multilingual-websites}

MSM은 두 가지 방법으로 다국어 웹 사이트 생성을 지원할 수 있습니다.

* 언어 마스터를 만들 때

   * MSM 자체는 **콘텐츠 번역을 지원하지 않지만**, 이를 지원하는 서드파티 번역 커넥터와 통합할 수 있습니다. 다음을 참고하십시오.

      * MSM을 사용하면 페이지 및/또는 구성 요소 수준에서 상속을 취소할 수 있습니다. 이렇게 하면 다음 롤아웃 시 번역된 컨텐츠(Live Copy에서 블루프린트에서 아직 번역되지 않은 컨텐츠로)를 덮어쓰는 것을 방지할 수 있습니다.
      * 일부 서드파티 번역 커넥터는 이러한 MSM 상속 관리를 자동화합니다.

         자세한 내용은 귀사의 번역 서비스 공급업체에 문의하십시오.

      * 언어 마스터를 만들고 번역하기 위한 또 다른 접근 방식은 AEM의 기본 번역 통합 프레임워크와 함께 언어 사본을 사용하는 것입니다.

* 언어 마스터에서 컨텐츠를 롤아웃할 때.

   * 예를 들어, 프랑스어 마스터 부터 프랑스/프랑스어, 캐나다/프랑스어, 스위스/프랑스어 등 국가별 사이트에 이르기까지 다양한 국가에서 사용할 수 있습니다.

자세한 내용은 [다국어 사이트의 컨텐츠 번역](/help/sites-administering/translation.md) 그리고 [번역 우수 사례](/help/sites-administering/tc-bp.md).

## 구조 변경 및 롤아웃 {#structure-changes-and-rollouts}

블루프린트/소스 트리의 컨텐츠 구조에 대한 수정 사항은 Live Copy에 다르게 반영됩니다. 이는 수정 유형에 따라 달라집니다.

* **만들기** 블루프린트의 새 페이지는 표준 롤아웃 구성을 사용하여 롤아웃 후 Live Copy에서 해당 페이지가 생성됩니다.

* **삭제** 블루프린트의 페이지는 표준 롤아웃 구성을 사용하여 롤아웃 후 Live Copy에서 해당 페이지가 삭제됩니다.

* **이동** 블루프린트의 페이지는 **not** 표준 롤아웃 구성을 사용하여 롤아웃 후 Live Copy에서 해당 페이지가 이동됩니다.

   * 이 비헤이비어의 이유는 페이지 이동이 페이지 삭제를 묵시적으로 포함하기 때문입니다. 작성자의 페이지를 삭제하면 게시 시 해당 콘텐츠가 자동으로 비활성화되므로 예기치 않은 비헤이비어가 발생할 수 있습니다. 링크, 책갈피 및 기타 항목과 같은 관련 항목에 노크 효과가 있을 수도 있습니다.
   * 각 Live Copy 페이지의 컨텐츠 상속은 블루프린트에서 해당 소스의 새 위치를 반영하도록 업데이트됩니다.
   * 블루프린트에서 Live Copy로 페이지 이동을 완전히 실현하려면 다음 우수 사례를 고려하십시오.

>[!NOTE]
>
>이 작업은 [롤아웃 트리거 시](/help/sites-administering/msm-sync.md#rollout-triggers).

* 사용자 정의 롤아웃 구성을 만듭니다:

   * 이 새 구성에는 작업이 포함되어야 합니다.

      `PageMoveAction`

      이 구성에 다른 작업을 추가하지 마십시오.

* 새 구성을 배치합니다:

   * Live Copy에서 이전 위치에서 각 페이지를 삭제하는 동안 페이지 이동을 완전히 롤아웃하려면:

      * 새로 생성된 구성을 표준 롤아웃 구성 앞에 배치합니다.

         표준 롤아웃 구성에서는 이전 위치에서 페이지를 삭제하는 작업이 수행됩니다.
   * 각 페이지를 Live Copy에서 이전 위치에 유지한 채 페이지 이동을 롤아웃하려면(기본적으로 컨텐츠가 복제됨):

      * 새로 생성된 구성을 표준 롤아웃 구성 뒤에 배치합니다.

         이렇게 하면 Live Copy에서 컨텐츠가 삭제되거나 게시에서 비활성화되지 않습니다.


## 롤아웃 맞춤화 {#customizing-rollouts}

MSM 롤아웃 구성은 맞춤화가 매우 용이합니다. 롤아웃을 자동화하면 광범위한 결과를 초래할 수 있습니다. 모범 사례로는 계획을 세워야 합니다 *매우* 주의 사항:

* 롤아웃 자동화 예를 들어 [onModify 트리거](#onmodify),
* 사용자 지정 [노드 유형/속성](#node-types-properties),
* 후속 워크플로우 시작
* 롤아웃의 일부로 컨텐츠 및/또는 활성화.

### onModify {#onmodify}

[롤아웃 트리거](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`를 사용할 때에는 다음을 참고하십시오.

* `onModify` 트리거를 사용하여 롤아웃을 자동화하면 모든 페이지 수정 시 롤아웃이 트리거되므로 작성 성능에 부정적인 영향을 미칠 수 있습니다.**

* 롤아웃 결과는 예상과 다를 수 있습니다. 그 이유는 다음과 같습니다.

   * 최종 수정 이벤트의 순서를 지정할 수 없기 때문입니다.
   * 이벤트 기반 아키텍처가 롤아웃 관리자에게 전달된 이벤트의 순서를 보장할 수 없기 때문입니다.

* 이러한 롤아웃 구성을 사용하면 동일한 리소스의 동시 업데이트가 발생할 경우 커밋 충돌이 발생할 수 있기 때문입니다.

따라서 다음을 수행하는 것이 좋습니다 *전용* 사용 `onModify` 자동 롤아웃 시작의 이점이 잠재적 성능 문제를 능가하면 트리거됩니다.

### 노드 유형/속성 {#node-types-properties}

다음 사항을 기억하십시오.

* MSM을 사용하면 롤아웃 작업 외에도 롤아웃되는 노드 속성을 맞춤화할 수 있습니다. 다음 [MSM OSGi 구성을 사용하여 노드 유형을 제외할 수 있습니다](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) 소스에서 Live Copy로 복사되는 중입니다.

## 추가 정보 {#further-information}

이 페이지와 다음 페이지에서는 관련 문제를 다룹니다.

* [라이브 카피 생성 및 동기화](/help/sites-administering/msm-livecopy.md)
* [라이브 카피 개요 콘솔](/help/sites-administering/msm-livecopy-overview.md)
* [라이브 카피 동기화 구성](/help/sites-administering/msm-sync.md)
* [MSM 롤아웃 충돌](/help/sites-administering/msm-rollout-conflicts.md)
