---
title: 사용자 지정 노드 유형
description: Adobe Experience Manager(AEM)는 Sling을 기반으로 하며 두 가지 모두에서 제공하는 노드 유형이 있는 JCR 저장소를 사용하지만 AEM에서는 다양한 사용자 지정 노드 유형을 제공합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: bfd50aa9-579e-47d5-997d-ec764c782497
source-git-commit: 939132e8b461b51e1c49237e481243bcc5de3bf6
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 9%

---

# 사용자 지정 노드 유형{#custom-node-types}

Adobe Experience Manager(AEM)는 Sling을 기반으로 하며 JCR 저장소를 사용하므로 다음 두 가지 모두에서 제공하는 노드 유형을 사용할 수 있습니다.

* [JCR 노드 유형](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling 노드 유형](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

이 외에도. AEM은 다양한 사용자 지정 노드 유형을 제공합니다.

## 감사 {#audit}

### cq:AuditEvent {#cq-auditevent}

**설명**

감사 이벤트 노드의 노드 유형을 정의합니다.

* `@prop cq:time`
* `@prop cq:userid`
* `@prop cq:path`
* `@prop cq:type`
* `@prop cq:category`
* `@prop cq:properties`

**정의**

* `[cq:AuditEvent]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
* `- cq:time (date)`
* `- cq:userid (string)`
* `- cq:path (string)`
* `- cq:type (string)`
* `- cq:category (string)`
* `- cq:properties (binary)`

## 설명 {#comment}

### cq:Comment {#cq-comment}

**설명**

주석 노드의 노드 유형을 정의합니다.

* `@prop userIdentifier`

**정의**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:CommentAttachment {#cq-commentattachment}

**설명**

의 노드 유형을 정의합니다. `commentattachment` 노드

**정의**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:CommentContent {#cq-commentcontent}

**설명**

주석 컨텐츠 노드의 노드 유형을 정의합니다.

**정의**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:GeoLocation {#cq-geolocation}

**설명**

지리적 위치를 소수점(DD)로 정의하는 mixin

* `@prop latitude` - 소수를 사용하여 이중으로 인코딩된 위도
* `@prop longitude` - 10진도를 사용하여 이중으로 인코딩된 경도

**정의**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq:Trackback {#cq-trackback}

**설명**

트랙백 노드의 노드 유형을 정의합니다.

**정의**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## 코어 {#core}

### cq:Page {#cq-page}

**설명**

기본 CQ 페이지를 정의합니다.

* `@node jcr:content` - 페이지의 기본 콘텐츠.

**정의**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq:PseudoPage {#cq-pseudopage}

**설명**

노드를 의사 페이지로 표시하는 mixin 형식을 정의합니다. 즉, 페이지 및 WCM 편집 지원에 맞게 조정할 수 있습니다.

**정의**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**설명**

WCM에서 사용되는 최소 속성으로 페이지 콘텐츠의 기본 노드를 정의합니다.

* `@prop jcr:title` - 페이지 제목
* `@prop jcr:description` - 이 페이지에 대한 설명.
* `@prop cq:template` - 페이지를 만드는 데 사용되는 템플릿 경로.
* `@prop cq:allowedTemplates` - 허용된 템플릿에 대한 경로를 결정하는 데 사용되는 정규 표현식 목록입니다.
* `@prop pageTitle` - 일반적으로 제목은 `<title>` 태그에 가깝게 배치하십시오.
* `@prop navTitle` - 일반적으로 탐색에서 사용되는 제목입니다.
* `@prop hideInNav` - 탐색 시 페이지를 숨길지 여부를 지정합니다.
* `@prop onTime` - 이 페이지가 유효해지는 시간.
* `@prop offTime` - 이 페이지가 유효하지 않게 되는 시간.
* `@prop cq:lastModified` - 페이지(또는 해당 단락)가 마지막으로 수정된 날짜입니다.
* `@prop cq:lastModifiedBy` - 페이지(또는 해당 단락)를 변경할 마지막 사용자.
* `@prop jcr:language` - 페이지 콘텐츠의 언어.

>[!NOTE]
>
>페이지 콘텐츠에서 이 유형을 사용해야 하는 것은 아닙니다.

**정의**
* `[cq:PageContent] > nt:unstructured, mix:title, mix:created, cq:OwnerTaggable, sling:VanityPath, cq:ReplicationStatus, sling:Resource orderable`
   * `- cq:template (string)`
   * `- cq:allowedTemplates (string) multiple`
   * `- pageTitle (string)`
   * `- navTitle (string)`
   * `- hideInNav (boolean)`
   * `- onTime (date)`
   * `- offTime (date)`
   * `- cq:lastModified (date)`
   * `- cq:lastModifiedBy (string)`
   * `- cq:designPath (string)`
   * `- jcr:language (string)`

### cq:Template {#cq-template}

**설명**

CQ 템플릿을 정의합니다.

* `@node jcr:content` - 새 페이지에 대한 기본 콘텐츠.
* `@node icon.png` - 특성 아이콘이 있는 파일.
* `@node thumbnail.png` - 특성 썸네일 이미지가 들어 있는 파일입니다.
* `@node workflows` - 워크플로 구성 자동 할당 구성은 아래 구조를 따릅니다.
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents` - 상위 템플릿으로 허용되는 템플릿에 대한 경로를 결정하는 정규 표현식 패턴입니다.
* `@prop allowedChildren` - 하위 템플릿으로 허용되는 템플릿에 대한 경로를 결정하는 정규 표현식 패턴입니다.
* `@prop ranking` - 페이지 만들기 대화 상자에서 템플릿 목록 내에 배치합니다.

**정의**

* `[cq:Template] > nt:hierarchyNode, mix:title`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ jcr:content (nt:base) copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `+ workflows (nt:base) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `- ranking (long)`

### cq:Component {#cq-component}

**설명**

CQ 구성 요소를 정의합니다.

* `@prop jcr:title` - 구성 요소 제목
* `@prop jcr:description` - 구성 요소에 대한 설명.
* `@node dialog` - 기본 대화 상자.
* `@prop dialogPath` - 기본 대화 상자 경로(대화 상자 대체).
* `@node design_dialog` - 디자인 대화 상자
* `@prop cq:cellName` - 디자인 셀의 이름입니다.
* `@prop cq:isContainer` - 컨테이너 구성 요소인지 여부를 나타냅니다. 이렇게 하면 경로 이름 대신 하위 구성 요소의 셀 이름이 사용됩니다. 예를 들어 `parsys` 는 컨테이너 구성 요소입니다. 이 값이 정의되지 않으면 확인은 `cq:childEditConfig`.
* `@prop cq:noDecoration` - true이면 데코레이션 없음 `div` 이 구성 요소를 포함할 때 태그가 그려집니다.
* `@node cq:editConfig` - 편집 막대의 매개 변수를 정의하는 구성입니다.
* `@node cq:childEditConfig` - 하위 구성 요소에 상속된 편집 구성입니다.
* `@node cq:htmlTag` - &quot;주변&quot;에 추가되는 추가 태그 속성을 정의합니다. `div` 태그 지정(구성 요소가 포함된 경우)
* `@node icon.png`- 특성 아이콘이 있는 파일.
* `@node thumbnail.png` - 특성 썸네일 이미지가 들어 있는 파일입니다.
* `@prop allowedParents` - 상위 구성 요소로 허용되는 구성 요소의 경로를 결정하는 정규 표현식 패턴입니다.
* `@prop allowedChildren` - 하위 구성 요소로 허용되는 구성 요소의 경로를 결정하는 정규 표현식 패턴입니다.
* `@node virtual` - 구성 요소 끌어서 놓기에 사용된 가상 구성 요소를 반영하는 하위 노드를 포함합니다.
* `@prop componentGroup` - 구성 요소 드래그 앤 드롭에 사용되는 구성 요소 그룹의 이름입니다.
* `@node cq:infoProviders` - 각각 속성이 있는 하위 노드를 포함합니다. `className` 이(가) 다음을 참조합니다. `PageInfoProvider`.

**정의**

* `[cq:Component] > nt:folder, mix:title, sling:ResourceSuperType`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ dialog (nt:base) = nt:unstructured copy`
   * `- dialogPath (string)`
   * `+ design_dialog (nt:base) = nt:unstructured copy`
   * `- cq:cellName (string)`
   * `- cq:isContainer (boolean)`
   * `- cq:noDecoration (boolean)`
   * `+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:childEditConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:htmlTag (nt:base) = nt:unstructured copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `+ virtual (nt:base) = sling:Folder copy`
   * `- componentGroup (string)`
   * `+ cq:infoProviders (nt:base) = nt:unstructured copy`

### cq:ComponentMixin {#cq-componentmixin}

**설명**

CQ 구성 요소를 mixin 유형으로 정의합니다.

**정의**

`[cq:ComponentMixin] > cq:Component mixin`

### cq:EditConfig {#cq-editconfig}

**설명**

&quot;편집 막대&quot;에 대한 구성을 정의합니다.

* `@prop cq:dialogMode` - 대화 상자의 모드:
   * `floating` - 보통의 부동 대화 상자
   * `inline` - 인라인 편집
   * `auto` - 자동 감지(사용 가능한 공간에 따라 다름)
* `@node cq:inplaceEditing` - 이 구성 요소에 대한 편집 구성을 즉석으로 설정합니다.
* `@prop cq:layout`- 편집 막대 레이아웃:
   * `editbar` - 편집 막대
   * `rollover` - 롤오버 프레임
   * `auto` - 자동 감지
* `@node cq:formParameters`- 대화 상자 양식에 추가할 추가 매개 변수
* `@prop cq:actions`- 작업 목록(편집 막대 단추 또는 메뉴 항목)
* `@node cq:actionConfigs` - 편집 막대 또는 메뉴 항목에 대한 위젯 구성
* `@prop cq:emptyText` - 시각적 컨텐츠가 없는 경우 표시될 텍스트입니다.
* `@node cq:dropTargets` - 컬렉션 `{@link cq:DropTargetConfig}` 노드.

**정의**

* `[cq:EditConfig] > nt:unstructured, nt:hierarchyNode orderable`
   * `- cq:dialogMode (string) < 'auto', 'floating', 'inline'`
   * `- cq:layout (string) < 'editbar', 'rollover', 'auto' + cq:formParameters (nt:base) = nt:unstructured`
   * `- cq:actions (string) multiple`
   * `+ cq:actionConfigs (nt:base) = nt:unstructured`
   * `- cq:emptyText (string)`
   * `+ cq:dropTargets (nt:base) = nt:unstructured`
   * `+ cq:listeners (nt:base) = cq:EditListenersConfig`

### cq:DropTargetConfig {#cq-droptargetconfig}

**설명**

구성 요소의 한 개 놓기 대상을 구성합니다. 이 노드의 이름은 드래그 앤 드롭의 ID로 사용됩니다.

* `@prop accept` - 이 드롭 대상에서 수락된 MIME 유형 목록. 예: `["image/*"]`
* `@prop groups` - 소스를 허용하는 드래그 앤 드롭 그룹 목록입니다.
* `@prop propertyName` - 참조를 저장하는 데 사용되는 속성의 이름입니다.

**정의**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq:VirtualComponent {#cq-virtualcomponent}

**설명**

가상 CQ 구성 요소를 정의합니다. 현재 새 구성 요소 드래그 앤 드롭 마법사에만 사용됩니다.

* `@prop jcr:title` - 이 구성 요소의 제목
* `@prop jcr:description` - 이 구성 요소에 대한 설명입니다.
* `@node cq:editConfig` - 편집 막대의 매개 변수를 정의하는 구성을 편집합니다.
* `@node cq:childEditConfig`- 하위 구성 요소에 상속된 구성을 편집합니다.
* `@node icon.png` - 특성 아이콘이 있는 파일.
* `@node thumbnail.png` - 특성 썸네일 이미지가 들어 있는 파일입니다.
* `@prop allowedParents` - 상위 구성 요소로 허용되는 구성 요소의 경로를 결정하는 정규 표현식 패턴입니다.
* `@prop allowedChildren` - 하위 구성 요소로 허용되는 구성 요소의 경로를 결정하는 정규 표현식 패턴입니다.
* `@prop componentGroup` - 구성 요소 드래그 앤 드롭의 구성 요소 그룹 이름.

**정의**

`[cq:VirtualComponent] > nt:folder, mix:title`
`- * (undefined)`
`- * (undefined) multiple`
`+ * (nt:base) = nt:base multiple version`
`+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
`+ icon.png (nt:file) copy`
`+ thumbnail.png (nt:file) copy`
`- allowedParents (string) multiple`
`- allowedChildren (string) multiple`
`- componentGroup (string)`

### cq:EditListenersConfig {#cq-editlistenersconfig}

**설명**

편집 이벤트에서 실행할 (클라이언트측) 리스너를 정의합니다. 값은 유효한 클라이언트측 리스너 함수를 참조하거나 미리 정의된 단축키를 포함해야 합니다.

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate` - 구성 요소가 만들어진 후 실행됩니다.
* `@prop afteredit` - 구성 요소를 편집(수정)한 후 실행됩니다.
* `@prop afterdelete` - 구성 요소가 삭제된 후 실행됩니다.
* `@prop afterinsert` - 구성 요소가 이 컨테이너에 추가된 후 실행됩니다.
* `@prop afterremove` - 구성 요소가 이 컨테이너에서 제거된 후 실행됩니다.
* `@prop aftermove` - 구성 요소가 이 컨테이너에서 이동된 후 발생합니다.

**정의**

* `[cq:EditListenersConfig]`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `+ &ast; (nt:base) = nt:base multiple version`
   * `- aftercreate (string)`
   * `- afteredit (string)`
   * `- afterdelete (string)`
   * `- afterinsert (string)`
   * `- afterremove (string)`
   * `- aftermove (string)`

## DAM {#dam}

### dam:AssetContent {#dam-assetcontent}

**설명**

DAM 에셋의 콘텐츠.

**정의**

* `[dam:AssetContent] > nt:unstructured`
   * `+ metadata (nt:unstructured)`
   * `+ renditions (nt:folder)`

### dam:Asset {#dam-asset}

**설명**

DAM 에셋.

**정의**

`[dam:Asset] > nt:hierarchyNode`
`+ jcr:content (dam:AssetContent) = dam:AssetContent copy primary`
`+ * (nt:base) = nt:base version`

### dam:썸네일 {#dam-thumbnail}

**설명**

DAM 자산을 나타내는 축소판입니다.

**정의**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## 게재 컨테이너 목록 {#delivery-container-list}

### cq:containerList {#cq-containerlist}

**설명**

컨테이너 목록.

**정의**

* `[cq:containerList]`
   * `mixin`

## 게재 페이지 {#delivery-page}

### cq:Cq4PageAttributes {#cq-cq-pageattributes}

**설명**

`cq:attributes` 는 ContentBus 버전 태그에 대한 노드 유형입니다. 이 노드에는 일련의 속성만 있습니다. 이 속성 중 사전 정의된 &quot;created&quot;, &quot;csd&quot; 및 &quot;timestampe&quot;가 있습니다.

* `@prop created (long) mandatory copy` - 버전 정보 생성 타임스탬프(일반적으로 이전 버전의 체크 인 시간 또는 페이지 생성 시간).
* `@prop csd (string) mandatory copy` - csd 표준 속성, 페이지 노드의 cq:csd 속성 사본
* `@prop timestamp (long) mandatory copy` - 마지막 버전 수정 타임스탬프(일반적으로 체크인 시간).
* `@prop * (string) copy` - 상위 노드로 버전이 지정된 추가 속성입니다.

**정의**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq:Cq4ContentPage {#cq-cq-contentpage}

**설명**

노드 유형 `cq:contentPage` ContentBus 컨텐츠 페이지에 대한 속성 및 하위 노드 정의를 포함합니다. 이 mixin 유형이 유형의 노드에 추가되는 경우에만 `cq:page`그러면 노드가 ContentBus 컨텐츠 페이지가 됩니다.

의 항목 `cq:Cq4ContentPage` 은(는)

* `@prop cq:csd` - 페이지의 ContentBus CSD입니다.
* `@node cq:content` - 페이지 콘텐츠. 페이지 노드가 &quot;컨텐츠 없이 존재함&quot; 또는 &quot;삭제됨&quot; 상태인 경우 이 하위 노드가 존재하지 않습니다.
* `@node cq:attributes` - 이전에 버전 태그라고 했던 페이지 속성 목록입니다. 이 노드는 cq:contentPage 유형에 필수입니다. 페이지의 버전이 관리될 때 속성 노드의 버전이 관리됩니다.

**정의**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## 가져오기 {#importer}

### cq:PollConfig {#cq-pollconfig}

**설명**

폴 구성.

* `@prop source (String) mandatory` - 데이터 소스 URI이며, 반드시 입력해야 합니다.
* `@prop target (String)` - 데이터 소스에서 검색된 데이터가 저장되는 대상 위치입니다. 이 옵션은 선택 사항이며 기본값은 cq:PollConfig 노드로 설정됩니다.
* `@prop interval (Long)` - 데이터 소스에서 새 데이터나 업데이트된 데이터를 폴링하는 간격(초)입니다. 이 옵션은 선택 사항이며 기본값은 30분(1800초)입니다.
* [Adobe Experience Manager용 사용자 지정 데이터 가져오기 서비스 만들기](https://helpx.adobe.com/experience-manager/using/polling.html)

**정의**

* `[cq:PollConfig]`
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**설명**

폴링 구성 노드를 쉽게 만들 수 있는 편리한 기본 노드 유형입니다.

**정의**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## 위치 {#location}

### cq:GeoLocation {#cq-geolocation-1}

**설명**

지리적 위치를 DD(소수점)로 정의하는 mixin.

* `@prop latitude` - 소수를 사용하여 이중으로 인코딩된 위도입니다.
* `@prop longitude` - 10진도를 사용하여 이중으로 인코딩된 경도입니다.

**정의**

* `[cq:GeoLocation]`
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## 발송자 {#mailer}

### cq:mailerMessage {#cq-mailermessage}

**설명**

MailerService 노드 유형입니다. 발송자는 해당 mixin을 갖는 노드를 메시지 정의의 루트 노드로 사용합니다.

**정의**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## MSM {#msm}

### cq:LiveRelationship {#cq-liverelationship}

**설명**

LiveRelationship 믹스인을 정의합니다. 기본 소스(제어) 노드와 라이브 카피(제어) 노드는 LiveRelationship을 통해 가상으로 연결될 수 있습니다.

**정의**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq:LiveSync {#cq-livesync}

**설명**

LiveSync mixin을 정의합니다. 노드가 기본 소스(제어) 노드 및 라이브 카피(제어) 노드와 LiveRelationship에 포함된 경우 LiveSync로 표시됩니다.

* `@prop cq:master` - LiveRelationship의 기본 소스(제어) 경로.
* `@prop cq:isDeep` - 1차 하위 구성요소에 대해 관계를 사용할 수 있는지 정의합니다.
* `@prop cq:syncTrigger` - 이 동기화를 트리거하는 시기를 정의합니다.
* `@node * LiveSyncAction` - 동기화 시 수행할 작업

**정의**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq:LiveSyncCanceled {#cq-livesynccancelled}

**설명**

LiveSyncCanceled 믹스인을 정의합니다. 상위 항목 중 하나로 인해 LiveRelationship에 포함될 수 있는 Live Copy(제어됨) 노드의 LiveSync 동작을 취소합니다.

* `@prop cq:isCancelledForChildren` - LiveSync의 취소 여부를 정의합니다(하위 항목도).

**정의**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq:LiveSyncAction {#cq-livesyncaction}

**설명**

LiveSync에 첨부된 LiveSyncAction을 정의합니다.

* `@prop name` - 작업 이름
* `@prop value` - 작업 값

**정의**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq:LiveSyncConfig {#cq-livesyncconfig}

**설명**

Live Sync 구성.

**정의**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

AEM 5.4의 경우 목록 끝에 을 추가합니다.

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq:BlueprintAction {#cq-blueprintaction}

**설명**

블루프린트 작업

**정의**

* `[cq:BlueprintAction] > nt:unstructured`

## Platform {#platform}

### cq:Console {#cq-console}

**설명**

콘솔 노드의 노드 유형을 정의합니다.

**정의**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## 복제 {#replication}

### cq:ReplicationStatus {#cq-replicationstatus}

**설명**

복제 상태 정보 mixin을 정의합니다.

* `@prop cq:lastPublished`- 페이지를 마지막으로 게시한 날짜(더 이상 사용되지 않음).
* `@prop cq:lastPublishedBy`- 페이지를 마지막으로 게시한 사용자(더 이상 사용되지 않음).
* `@prop cq:lastReplicated` - 페이지를 마지막으로 복제한 날짜입니다.
* `@prop cq:lastReplicatedBy` - 페이지를 마지막으로 복제한 사용자입니다.
* `@prop cq:lastReplicationAction` - 복제 작업: 활성화 또는 비활성화.
* `@prop cq:lastReplicationStatus` - 복제 상태(더 이상 사용되지 않음).

**정의**

* `[cq:ReplicationStatus]`
   * `mixin`
   * `- cq:lastPublished (date) ignore`
   * `- cq:lastPublishedBy (string) ignore`
   * `- cq:lastReplicated (date) ignore`
   * `- cq:lastReplicatedBy (string) ignore`
   * `- cq:lastReplicationAction (string) ignore`
   * `- cq:lastReplicationStatus (string) ignore`

## 보안 {#security}

### cq:ApplicationPrivilege {#cq-applicationprivilege}

**설명**

응용 프로그램 권한을 정의합니다.

**정의**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl}

**설명**

응용 프로그램 권한 ACL을 정의합니다.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**정의**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace}

**설명**

응용 프로그램 권한 ACE를 정의합니다.

* `@prop path`
* `@prop deny`

**정의**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

### cq:ApplicationPrivilege {#cq-applicationprivilege-1}

**설명**

응용 프로그램 권한을 정의합니다.

**정의**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl-1}

**설명**

응용 프로그램 권한 ACL을 정의합니다.

* `@prop cq:isPathDependent`
* `@node * ACEs`

**정의**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace-1}

**설명**

응용 프로그램 권한 ACE를 정의합니다.

* `@prop path`
* `@prop deny`

**정의**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## 사이트 가져오기 {#site-importer}

### cq:ComponentExtractorSource {#cq-componentextractorsource}

**설명**

구성 요소 추출기로 열 수 있는 파일을 표시하는 mixin 형식을 정의합니다.

**정의**

`[cq:ComponentExtractorSource] mixin`

## 태그 지정 {#tagging}

### cq:Tag {#cq-tag}

**설명**

단일 태그를 정의하지만 태그를 포함할 수도 있으므로 분류법을 만듭니다

**정의**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**설명**

태그 지정 가능한 콘텐츠에 대한 추상 기본 mixin.

* `@node cq:tags`

**정의**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq:OwnerTaggable {#cq-ownertaggable}

**설명**

작성자/소유자만 콘텐츠에 태그를 지정할 수 있습니다(중재/관리되는 태그 지정).

**정의**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq:UserTaggable {#cq-usertaggable}

**설명**

모든 사용자/공개 웹 사이트는 cq:userContent 내에서 사용되는 콘텐츠(Web2.0 스타일)에 태그를 지정할 수 있습니다.

**정의**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq:AllowsUserContent {#cq-allowsusercontent}

**설명**

를 추가합니다. `cq:userContent` 사용자가 수정할 수 있는 하위 노드. 각 사용자는 고유한 이름을 갖게 됩니다. `cq:userContent/<userid>` 일반적으로 mixin이 있는 하위 노드 `cq:UserTaggable`.

**정의**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

를 보다 명시적으로 정의하는 확장된 변형 `cq:userContent` 트리

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq:UserContent {#cq-usercontent}

**설명**

사용자가 수정할 수 있습니다.

**정의**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq:UserData {#cq-userdata}

**설명**

사용자 데이터

**정의**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## 위젯 {#widgets}

### cq:ClientLibraryFolder {#cq-clientlibraryfolder}

**설명**

클라이언트 라이브러리 폴더

**정의**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq:Widget {#cq-widget}

**설명**

위젯

**정의**

* `[cq:Widget] > nt:unstructured orderable`
   * `- xtype (string)`
   * `- name (string)`
   * `- title (string)`
   * `+ items (nt:base) = cq:WidgetCollection copy`

### cq:WidgetCollection {#cq-widgetcollection}

**설명**

위젯 컬렉션

**정의**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq:Dialog {#cq-dialog}

**설명**

대화 상자

**정의**

* `[cq:Dialog] > cq:Widget orderable`

### cq:Panel {#cq-panel}

**설명**

패널

**정의**

`[cq:Panel] > cq:Widget orderable`

### cq:TabPanel {#cq-tabpanel}

**설명**

탭 패널

**정의**

* `[cq:TabPanel]` > `cq:Panel orderable`
   * `- activeTab (long)`

### cq:Field {#cq-field}

**설명**

필드

**정의**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## Wiki {#wiki}

### wiki:Topic {#wiki-topic}

**설명**

Wiki 주제

**정의**

* `[wiki:Topic] > nt:unstructured, nt:hierarchyNode, mix:versionable, mix:lockable`
   * `+ * (wiki:Topic) version`
   * `+ wiki:attachments (nt:folder) = nt:folder version`
   * `+ wiki:properties (wiki:Properties) = wiki:Properties copy`
   * `- wiki:text (string) mandatory primary`
   * `- wiki:lastModified (date) mandatory`
   * `- wiki:lastModifiedBy (string) mandatory`
   * `- wiki:topicName`
   * `- wiki:topicTitle`
   * `- wiki:lockedBy`
   * `- wiki:logMessage (string)`
   * `- wiki:quietSave (boolean)`

### wiki:User {#wiki-user}

**설명**

위키 사용자

**정의**

* `[wiki:User] mixin`
   * `- wiki:subscriptions (string) multiple`

### wiki:속성 {#wiki-properties}

**설명**

Wiki 속성

**정의**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## 워크플로우 {#workflow}

### cq:Workflow {#cq-workflow}

**설명**

워크플로우 인스턴스를 나타냅니다.

**정의**

* `[cq:Workflow] > nt:base, mix:referenceable`
   * `- modelId (String)`
   * `- modelVersion (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- initiator (String)`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `- sling:resourceType (String) = "cq/workflow/components/instance" mandatory autocreated`
   * `+ workflowStack (nt:unstructured)`
   * `+ wait (nt:unstructured)`
   * `+ orTab (nt:unstructured)`
   * `+ data (cq:WorkflowData)`
   * `+ history (nt:unstructured)`
   * `+ metaData (nt:unstructured)`
   * `+ workItems (nt:unstructured)`

### cq:WorkItem {#cq-workitem}

**설명**

작업 항목.

**정의**

* `[cq:WorkItem]`
   * `- assignee (String)`
   * `- workflowId (String)`
   * `- nodeId (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- dueTime (Date)`
   * `- sling:resourceType (String) = "cq/workflow/components/workitem" mandatory autocreated`
   * `+ metaData (nt:unstructured)`

### cq:Load {#cq-payload}

**설명**

페이로드

**정의**

* `[cq:Payload]`
   * `- path (Path)`
   * `- uuid (String)`
   * `- jcr:url (String)`
   * `- binary (Binary)`
   * `- javaObject (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:WorkflowData {#cq-workflowdata}

**설명**

워크플로우 데이터

**정의**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq:WorkflowModel {#cq-workflowmodel}

**설명**

워크플로우 구성 자동 할당 구성은 아래 구조를 따릅니다.
* `workflows`
   * `+ name1`
      * `- cq:path`
      * `- cq:workflowName`
   * `+ workflows (nt:base)`

**정의**

* `[cq:WorkflowModel] > nt:base, mix:versionable`
   * `orderable`
   * `- title (String)`
   * `- description (String)`
   * `- sling:resourceType (String) = "cq/workflow/components/model" mandatory autocreated`
   * `+ nodes (nt:unstructured)`
      * `copy`
   * `+ transitions (nt:unstructured)`
      * `copy`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:WorkflowNode {#cq-workflownode}

**설명**

워크플로 노드

**정의**

* `[cq:WorkflowNode] orderable`
   * `- title (String)`
   * `- description (String)`
   * `- maxIdleTime (long)`
   * `- type (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ metaData (nt:unstructured)`
      * `copy`
   * `+ timeoutConfiguration (nt:unstructured)`
      * `copy`

### cq:WorkflowTransition {#cq-workflowtransition}

**설명**

워크플로우 전환

**정의**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:OrTab {#cq-ortab}

**설명**

또는 탭

**정의**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq:Wait {#cq-wait}

**설명**

대기

**정의**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq:WorkflowStack {#cq-workflowstack}

**설명**

워크플로 스택

**정의**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq:ProcessStack {#cq-processstack}

**설명**

프로세스 스택

**정의**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq:WorkflowLaunch {#cq-workflowlauncher}

**설명**

워크플로우 런처

**정의**

* `[cq:WorkflowLauncher]`
   * `- nodetype (String)`
   * `- glob (String)`
   * `- eventType (Long)`
   * `- description (String)`
   * `- condition (String)`
   * `- workflow (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
