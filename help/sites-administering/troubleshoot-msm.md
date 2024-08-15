---
title: MSM 문제 해결 및 FAQ
description: 가장 일반적인 MSM 관련 문제를 해결하는 방법을 찾아보고 가장 일반적인 MSM 관련 질문에 대한 답변을 받아 보십시오.
feature: Multi Site Manager
role: Admin
exl-id: 23f3391b-5ce3-48e1-ab27-a37737778089
solution: Experience Manager, Experience Manager Sites
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 81%

---

# MSM 문제 해결 및 FAQ {#troubleshooting-msm}

## 문제 해결 첫 단계 {#first-steps}

MSM에서 잘못된 동작이나 오류가 발생하는 경우 문제 해결을 시작하기 전에 다음을 확인하십시오.

* [MSM FAQ](#faq)를 확인합니다. 여기에서 문제 또는 질문이 이미 해결되었을 수 있습니다.
* [MSM 모범 사례 문서](msm-best-practices.md)를 확인합니다. 여기에는 일부 오해에 대한 설명과 함께 몇 가지 팁이 제공됩니다.

## 블루프린트 및 Live Copy 상태에 대한 고급 정보 찾기 {#advanced-info}

MSM은 리소스 URL의 선택기를 통해 요청할 수 있는 여러 서블릿을 등록합니다. 이는 UI에서 사용되지만 페이지에 대한 추가 고급 계산 MSM 상태를 직접 확인하기 위해 요청할 수도 있습니다.

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 블루프린트 페이지에서 이를 사용하여 연결된 모든 Live Copy 목록을 추가 Live Copy 상태 정보와 함께 가져올 수 있습니다.
   * 예:
     `http://localhost:4502/content/wknd/language-masters/en.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`


1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * Live Copy 페이지에서 이를 사용하여 블루프린트 페이지와의 연결에 대한 고급 정보를 가져올 수 있습니다. 페이지가 Live Copy가 아닌 경우 아무것도 반환되지 않습니다.
   * 예:
     `http://localhost:4502/content/wknd/ca/en.msm.json`

이들 서블릿은 `com.day.cq.wcm.msm` 로거를 통해 유용하게 사용할 수 있는 디버그 로그 메시지를 생성합니다.

## 저장소에서 MSM 관련 정보 확인 {#checking-repo}

이전 서블릿에서 MSM 관련 노드 및 믹스인을 기반으로 계산된 정보가 반환되었습니다. 이 정보는 다음과 같은 방법으로 저장소에 저장됩니다.

* `cq:LiveSync` 믹스인 유형
   * `jcr:content` 노드에 대해 설정되며 루트 Live Copy 페이지를 정의합니다.
   * 해당 페이지에는 다음 속성을 통해 Live Copy에 대한 기본 및 필수 정보를 포함하는 `cq:LiveCopy` 유형의 `cq:LiveSyncConfig` 하위 노드가 있습니다.
      * `cq:master`는 Live Copy의 블루프린트 페이지를 나타냅니다.
      * `cq:rolloutConfigs`는 Live Copy에 적용되는 활성 롤아웃 구성을 나타냅니다.
      * `cq:isDeep`은 이 루트 Live Copy 페이지의 하위 페이지가 Live Copy에 포함되어 있는 경우 true입니다.
* `cq:LiveRelationship` 믹스인 유형
   * 모든 Live Copy 페이지는 `jcr:content` 노드에 이러한 믹스인 유형이 있습니다.
   * 그렇지 않은 경우 해당 페이지는 어느 시점에 Live Copy 작업(생성 또는 롤아웃) 외부에 있는 작성 인터페이스를 통해 분리되거나 수동으로 작성된 것입니다.
* `cq:LiveSyncCancelled` 믹스인 유형
   * 일시 중단되었던 Live Copy 페이지의 `jcr:content` 노드에 추가되었습니다.
   * 일시 중단이 하위 페이지에도 적용되는 경우 `cq:isCancelledForChildren` 속성이 동일한 노드에 대해 true로 설정되어 있는 것입니다.

이러한 속성에 있는 정보는 UI에 반영되어야 하지만 문제 해결 시 MSM 작업이 발생할 때 저장소에서 직접 MSM 동작을 관찰하는 것이 도움이 될 수 있습니다.

이러한 속성을 알고 있는 것은 저장소를 쿼리하고 특정 상태에 있는 페이지 세트를 찾는 데에도 유용할 수 있습니다. 예:

* `select * from cq:LiveSync`는 모든 Live Copy 루트 페이지를 반환합니다.

## FAQ {#faq}

다음은 MSM 및 Live Copy와 관련하여 자주 묻는 몇 가지 질문입니다.

### 일부 속성(예: 제목, 주석)이 MSM 롤아웃 도중 업데이트되지 않는 이유는 무엇입니까? {#missing-properties}

MSM 동기화 작업은 구성이 매우 용이합니다. 롤아웃 도중 수정되는 속성 또는 구성 요소는 해당 구성의 속성에 따라 달라집니다.

이 항목에 대한 자세한 내용은 [MSM 모범 사례](msm-best-practices.md)를 참조하세요.

### 작성자 그룹에 대해 롤아웃 권한을 제거하려면 어떻게 해야 합니까? {#remove-rollout-permissions}

AEM 주체(사용자 또는 그룹)에 대해 삭제하거나 제거할 수 있는 **롤아웃** 권한은 없습니다.

대신 다음 중 원하는 작업을 수행할 수 있습니다.

* 지정된 주체에 대해 롤아웃 작업을 숨기도록 제품 UI를 맞춤화합니다.
* 롤아웃이 허용되지 않은 작성자에 대해 Live Copy 트리에서 쓰기 권한을 제거합니다.

### Live Copy 페이지에 접미사 “_msm_moved”가 표시되는 이유는 무엇입니까? {#moved-pages}

블루프린트 페이지가 롤아웃되면 해당 라이브 카피 페이지가 업데이트되거나 아직 존재하지 않는 경우 새 라이브 카피 페이지가 생성됩니다. 예: 처음 롤아웃되었거나 Live Copy 페이지가 수동으로 삭제된 경우.

그러나 후자의 경우 같은 이름의 `cq:LiveRelationship` 속성이 없는 페이지가 있으면 라이브 카피 페이지를 만들기 전에 이 페이지의 이름이 바뀝니다.

기본적으로 롤아웃에는 블루프린트 업데이트가 롤아웃되는 연결된 라이브 카피 페이지가 필요합니다. 또는 라이브 카피 페이지를 만들 때 페이지가 전혀 없을 수도 있습니다.

“독립형” 페이지가 있는 경우 MSM은 이 페이지의 이름을 변경한 다음 별도의 연결된 Live Copy 페이지를 생성합니다.

Live Copy 하위 트리에 있는 이러한 독립형 페이지는 일반적으로 **분리** 작업의 결과이거나, 작성자가 이전 Live Copy 페이지를 수동으로 삭제한 다음 같은 이름으로 다시 만든 결과입니다.

이 문제를 방지하려면 **분리**&#x200B;가 아닌 Live Copy **일시 중단** 기능을 사용합니다. **분리** 작업에 대한 자세한 내용은 [이 문서](msm-livecopy.md)에서 확인할 수 있습니다.
