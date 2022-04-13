---
title: MSM 문제 해결 및 FAQ
description: 가장 일반적인 MSM 관련 문제를 해결하고 가장 일반적인 MSM 관련 질문에 대한 답변을 얻는 방법을 알아봅니다.
feature: Multi Site Manager
role: Admin
source-git-commit: d4fa331ad048e1d8bd57e0944c8bc5b67be1d203
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# MSM 문제 해결 및 FAQ {#troubleshooting-msm}

## 첫 단계 문제 해결 {#first-steps}

MSM에서 잘못된 동작이나 오류가 발생한 경우 시작 및 세부 문제 해결을 시작하기 전에 다음을 확인하십시오.

* 을(를) 확인합니다. [MSM FAQ](#faq) 문제는 이미 해결되었습니다.
* 을(를) 확인합니다. [MSM 우수 사례 문서](msm-best-practices.md) 여러 가지 잘못된 인식을 명확히 하는 동시에 많은 팁이 제공됩니다.

## 블루프린트 및 Live Copy 상태에 대한 고급 정보 찾기 {#advanced-info}

MSM은 리소스 URL의 선택기로 요청할 수 있는 여러 서블릿을 등록합니다. UI에서 사용되지만, 직접 요청하여 페이지에 대한 고급 계산된 MSM 상태를 직접 볼 수도 있습니다.

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 블루프린트 페이지에서 이 옵션을 사용하여 연결된 모든 Live Copy 목록과 추가 Live Copy 상태 정보를 검색합니다.
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Live Copy 페이지에서 이 정보를 사용하여 블루프린트 페이지와의 연결에 대한 고급 정보를 검색합니다. 페이지가 Live Copy가 아닌 경우 아무 것도 반환되지 않습니다.

이러한 서블릿은 다음을 통해 DEBUG 로그 메시지를 생성합니다 `com.day.cq.wcm.msm` 유용할 수 있는 로거.

## 저장소에서 MSM 관련 정보 확인 {#checking-repo}

이전 서블릿은 MSM 관련 노드 및 mixin을 기반으로 계산된 정보를 반환했습니다. 정보는 다음과 같은 방법으로 저장소에 저장됩니다.

* `cq:LiveSync` mixin 유형
   * 이 설정은 `jcr:content` 노드 및 루트 Live Copy 페이지 정의
   * 해당 페이지에는 `cq:LiveSyncConfig` 하위 노드 유형 `cq:LiveCopy` 여기에는 다음 속성을 통해 Live Copy에 대한 기본 및 필수 정보가 포함됩니다.
      * `cq:master` 는 Live Copy의 블루프린트 페이지를 가리킵니다.
      * `cq:rolloutConfigs` Live Copy에 적용된 활성 롤아웃 구성을 나타냅니다.
      * `cq:isDeep` 이 루트 Live Copy 페이지의 하위 페이지가 Live Copy에 포함된 경우 true입니다.
* `cq:LiveRelationship` mixin 유형
   * 모든 Live Copy 페이지에는 와 같은 mixin 유형이 있습니다 `jcr:content` 노드 아래에 있어야 합니다.
   * 코드가 포함되어 있지 않으면 Live Copy 작업 외부의 작성 인터페이스를 통해 특정 지점의 페이지가 분리되거나 수동으로 생성되었습니다(만들기 또는 롤아웃).
* `cq:LiveSyncCancelled` mixin 유형
   * 에 추가됨 `jcr:content` 일시 중지된 Live Copy 페이지의 노드입니다.
   * 하위 페이지에도 일시 중단이 적용되는 경우, `cq:isCancelledForChildren` 속성이 동일한 노드에서 true로 설정됩니다.

이러한 속성에 있는 정보는 UI에 반영되어야 하지만 문제 해결 시 MSM 작업이 발생할 때 저장소에서 직접 MSM 동작을 관찰하는 것이 도움이 될 수 있습니다.

이러한 속성을 아는 것은 리포지토리를 쿼리하고 특정 상태의 페이지 세트를 찾는 데 유용합니다. 예:

* `select * from cq:LiveSync` 모든 Live Copy 루트 페이지를 반환합니다.

## FAQ {#faq}

다음은 MSM 및 Live Copy와 관련된 몇 가지 FAQ입니다.

### MSM 롤아웃 중에 일부 속성(예: 제목, 주석)이 업데이트되지 않는 이유는 무엇입니까? {#missing-properties}

MSM 동기화 작업은 구성 가능성이 높습니다. 롤아웃 중에 수정되는 속성 또는 구성 요소는 해당 구성의 속성에 따라 직접 수정됩니다.

자세한 내용은 [이 문서](msm-best-practices.md) 자세한 내용은 이 항목을 참조하십시오.

### 작성자 그룹에 대한 롤아웃 권한을 제거하려면 어떻게 해야 합니까? {#remove-rollout-permissions}

없습니다 **롤아웃** AEM 주체(사용자 또는 그룹)에 대해 설정하거나 제거할 수 있는 권한.

또는 다음 중 하나를 수행할 수 있습니다.

* 지정된 주도자에 대한 롤아웃 작업을 숨기도록 제품 UI를 사용자 지정합니다.
* 롤아웃이 허용되지 않는 작성자의 Live Copy 트리에서 쓰기 권한을 제거합니다.

### 접미사가 &quot;_msm_moved&quot;인 Live Copy 페이지가 표시되는 이유는 무엇입니까? {#moved-pages}

블루프린트 페이지가 롤아웃되면 해당 Live Copy 페이지를 업데이트하거나, 페이지가 아직 존재하지 않는 경우(예: 처음 롤아웃되거나 Live Copy 페이지가 수동으로 삭제되었을 때) 새 Live Copy 페이지를 만듭니다.

하지만 이 경우 페이지가 `cq:LiveRelationship` 속성이 동일한 이름으로 존재하며 Live Copy 페이지가 만들어지기 전에 이 페이지의 이름이 적절하게 변경됩니다.

기본적으로 롤아웃에는 Live Copy 페이지가 작성될 때 블루프린트의 업데이트가 롤아웃되는 연결된 Live Copy 페이지가 필요하거나 페이지가 작성되지 않은 페이지가 필요합니다.

독립형 페이지가 있는 경우 MSM에서 이 페이지의 이름을 변경하고 연결된 별도의 Live Copy 페이지를 만듭니다.

Live Copy 하위 트리의 이러한 독립형 페이지는 일반적으로 **분리** 작업 또는 이전에 Live Copy 페이지를 작성자가 수동으로 삭제한 다음 동일한 이름으로 다시 만들었습니다.

이를 방지하려면 Live Copy 를 사용합니다 **일시 중단** 기능 대신 **분리**. 에 대한 자세한 내용 **분리** 작업 [이 문서를 참조하십시오.](msm-livecopy.md)
