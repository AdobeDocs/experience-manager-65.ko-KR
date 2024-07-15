---
title: 워크플로 프로세스 참조
description: Adobe Experience Manager의 워크플로에 대한 이 프로세스 참조 를 참조하십시오.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# 워크플로 프로세스 참조{#workflow-process-reference}

AEM에서는 워크플로우 모델을 만드는 데 사용할 수 있는 몇 가지 프로세스 단계를 제공합니다. 기본 제공 단계에서 다루지 않는 작업에 대해 사용자 지정 프로세스 단계를 추가할 수도 있습니다([워크플로 모델 만들기](/help/sites-developing/workflows-models.md) 참조).

## 프로세스 특성 {#process-characteristics}

각 공정 단계별로 다음과 같은 특징을 기재한다.

### Java™ 클래스 또는 ECMA 경로 {#java-class-or-ecma-path}

프로세스 단계는 Java™ 클래스 또는 ECMAScript로 정의됩니다.

* Java™ 클래스 프로세스의 경우 정규화된 클래스 이름이 제공됩니다.
* ECMAScript 프로세스의 경우 스크립트에 대한 경로가 제공됩니다.

### 페이로드 {#payload}

페이로드는 워크플로 인스턴스가 작동하는 엔티티입니다. 페이로드는 워크플로 인스턴스가 시작되는 컨텍스트에 의해 암시적으로 선택됩니다.

예를 들어 워크플로가 AEM 페이지 *P*&#x200B;에 적용되면 워크플로가 진행될 때 *P*&#x200B;이(가) 단계에서 단계로 전달되며, 각 단계는 선택적으로 *P*&#x200B;에 어떤 식으로든 작동합니다.

가장 일반적인 경우 페이로드는 저장소의 JCR 노드(예: AEM 페이지 또는 에셋)입니다. JCR 노드 페이로드는 JCR 경로 또는 JCR 식별자(UUID)인 문자열로 전달됩니다. 경우에 따라 페이로드는 JCR 속성(JCR 경로로 전달됨), URL, 이진 객체 또는 일반 Java™ 객체일 수 있습니다. 페이로드에 작동하는 개별 프로세스 단계는 일반적으로 특정 유형의 페이로드를 예상하거나 페이로드 유형에 따라 다르게 작동합니다. 아래에 기술된 각 프로세스에 대해, 만약 있다면, 예상되는 페이로드 유형이 기술된다.

### 인수 {#arguments}

일부 워크플로 프로세스에서는 관리자가 워크플로 단계를 설정할 때 지정하는 인수를 수락합니다.

인수는 워크플로우 편집기의 **속성** 창에서 **프로세스 인수** 속성에 단일 문자열로 입력됩니다. 아래에 설명된 각 프로세스에 대해, 인수 문자열의 형식은 간단한 EBNF 문법으로 기술된다. 예를 들어, 다음은 인수 문자열이 하나 이상의 쉼표로 구분된 쌍으로 구성되어 있고 각 쌍은 이름(문자열)과 값으로 구성되며 이중 콜론으로 구분됨을 나타냅니다.

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 시간 초과 {#timeout}

이 시간 제한 기간이 지나면 워크플로우 단계가 더 이상 작동하지 않습니다. 일부 워크플로우 프로세스는 시간 제한을 준수하지만, 다른 워크플로우 프로세스는 적용되지 않으며 무시됩니다.

### 권한 {#permissions}

`WorkflowProcess`에 전달된 세션은 저장소의 루트에 다음 권한이 있는 워크플로 프로세스 서비스의 서비스 사용자가 지원합니다.

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

해당 권한 집합이 `WorkflowProcess` 구현에 충분하지 않으면 필요한 권한이 있는 세션을 사용해야 합니다.

권장되는 방법은 필요한 권한이지만 필요한 권한의 하위 집합을 최소화하면서 만든 서비스 사용자를 사용하는 것입니다.

>[!CAUTION]
>
>AEM 6.2 이전 버전에서 업그레이드하는 경우 구현을 업데이트해야 할 수 있습니다.
>
>이전 버전에서는 관리 세션이 `WorkflowProcess` 구현에 전달되었으므로 특정 ACL을 정의하지 않고도 저장소에 대한 전체 액세스 권한을 가질 수 있었습니다.
>
>이제 권한이 위와 같이 정의되었습니다([권한](#permissions)). 는 구현을 업데이트하는 데 권장되는 방법입니다.
>
>단기 솔루션은 코드를 변경할 수 없는 경우 이전 버전과의 호환성을 위해서도 사용할 수 있습니다.
>
>* 웹 콘솔(`/system/console/configMgr`)을 사용하여 **Adobe Granite 워크플로 구성 서비스를 찾습니다**
>
>* **워크플로 프로세스 레거시 모드** 사용
>
>이 작업은 `WorkflowProcess` 구현에 관리자 세션을 제공하는 이전 동작으로 되돌아가서 저장소 전체에 다시 무제한 액세스를 제공합니다.

## 워크플로우 제어 프로세스 {#workflow-control-processes}

다음 프로세스에서는 콘텐츠에 대해 작업을 수행하지 않습니다. 워크플로우 자체의 동작을 제어하는 역할을 합니다.

### AbsoluteTimeAutoAdvancer(절대 시간 자동 진행) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

`AbsoluteTimeAutoAdvancer`(절대 시간 자동 진행) 프로세스는 지정된 시간이 지난 후 대신 지정된 시간 및 날짜에 시간 초과된다는 점을 제외하면 **AutoAdvancer**&#x200B;와 동일하게 동작합니다.

* **Java™ 클래스**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **페이로드**: 없음.
* **인수**: 없음.
* **시간 초과**: 설정된 시간 및 날짜에 도달하면 프로세스 시간이 초과됩니다.

### AutoAdvancer(자동 진행) {#autoadvancer-auto-advancer}

`AutoAdvancer` 프로세스는 자동으로 워크플로우를 다음 단계로 진행합니다. 가능한 다음 단계가 두 개 이상 있는 경우(예: OR 분할이 있는 경우) 이 프로세스는 *기본 경로*&#x200B;을(를) 따라 워크플로우를 진행합니다(지정된 경우). 그렇지 않으면 워크플로우가 진행되지 않습니다.

* **Java™ 클래스**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **페이로드**: 없음.
* **인수**: 없음.
* **시간 초과**: 설정된 시간 이후에 프로세스 시간이 초과되었습니다.

### ProcessAssembler(프로세스 어셈블러) {#processassembler-process-assembler}

`ProcessAssembler` 프로세스는 단일 워크플로우 단계에서 여러 하위 프로세스를 순차적으로 실행합니다. `ProcessAssembler`을(를) 사용하려면 워크플로우에서 이 형식의 단일 단계를 만들고 해당 인수를 설정하여 실행하려는 하위 프로세스의 이름과 인수를 나타냅니다.

* **Java™ 클래스**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **페이로드**: DAM 자산, AEM 페이지 또는 페이로드 없음(하위 프로세스의 요구 사항에 따라 다름)
* **인수**:

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **시간 초과**: 적용됩니다.

예:

* 에셋에서 메타데이터를 추출합니다.
* 지정된 세 가지 크기의 축소판을 세 개 만듭니다.
* 에셋이 원래 GIF 또는 PNG가 아니라고 가정하여 에셋에서 JPEG 이미지를 만듭니다(이 경우 JPEG이 만들어지지 않음).
* 에셋에서 마지막으로 수정한 날짜를 설정합니다.

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 기본 프로세스 {#basic-processes}

다음 프로세스는 간단한 작업을 수행하거나 예제로 사용됩니다.

>[!CAUTION]
>
>`/libs` 경로에서 아무 것도 변경하지 마십시오.
>
>이는 다음에 인스턴스를 업그레이드할 때 `/libs`의 콘텐츠가 덮어쓰기되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓰기될 수 있음).

### 삭제 {#delete}

지정된 경로의 항목이 삭제됩니다.

* **ECMAScript 경로**: `/libs/workflow/scripts/delete.ecma`

* **페이로드**: JCR 경로
* **인수**: 없음
* **시간 초과**: 무시됨

### noop {#noop}

null 프로세스입니다. 작업을 수행하지 않지만 디버그 메시지를 기록합니다.

* **ECMAScript 경로**: `/libs/workflow/scripts/noop.ecma`

* **페이로드**: 없음
* **인수**: 없음
* **시간 초과**: 무시됨

### rule-false {#rule-false}

`check()` 메서드에서 `false`을(를) 반환하는 Null 프로세스입니다.

* **ECMAScript 경로**: `/libs/workflow/scripts/rule-false.ecma`

* **페이로드**: 없음
* **인수**: 없음
* **시간 초과**: 무시됨

### 샘플 {#sample}

샘플 ECMAScript 프로세스입니다.

* **ECMAScript 경로**: `/libs/workflow/scripts/sample.ecma`

* **페이로드**: 없음
* **인수**: 없음
* **시간 초과**: 무시됨

### LockProcess {#lockprocess}

워크플로우의 페이로드를 잠급니다.

* **Java™ 클래스:** `com.day.cq.workflow.impl.process.LockProcess`

* **페이로드:** JCR_PATH 및 JCR_UUID
* **인수:** 없음
* **시간 제한:** 무시됨

다음 상황에서는 단계가 적용되지 않습니다.

* 페이로드가 이미 잠겨 있습니다.
* 페이로드 노드에 jcr:content 하위 노드가 없습니다.

### UnlockProcess {#unlockprocess}

워크플로우의 페이로드를 잠금 해제합니다.

* **Java™ 클래스:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **페이로드:** JCR_PATH 및 JCR_UUID
* **인수:** 없음
* **시간 제한:** 무시됨

다음 상황에서는 단계가 적용되지 않습니다.

* 페이로드가 이미 잠금 해제되었습니다.
* 페이로드 노드에 jcr:content 하위 노드가 없습니다.

## 버전 관리 프로세스 {#versioning-processes}

다음 프로세스는 버전 관련 작업을 수행합니다.

### CreateVersionProcess {#createversionprocess}

워크플로 페이로드(AEM 페이지 또는 DAM 에셋)의 버전을 만듭니다.

* **Java™ 클래스**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **페이로드**: 페이지 또는 DAM 자산을 참조하는 JCR 경로 또는 UUID
* **인수**: 없음
* **시간 초과**: 준수됨
