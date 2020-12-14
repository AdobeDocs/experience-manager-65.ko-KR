---
title: 페이지 편집에 대한 실행 취소 구성
seo-title: 페이지 편집에 대한 실행 취소 구성
description: AEM에서 페이지 편집에 대한 실행 취소 지원을 구성하는 방법을 알아봅니다.
seo-description: AEM에서 페이지 편집에 대한 실행 취소 지원을 구성하는 방법을 알아봅니다.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---


# 페이지 편집에 대한 실행 취소 구성{#configuring-undo-for-page-editing}

[OSGi 서비스](/help/sites-deploying/configuring-osgi.md) **Day CQ WCM 실행 취소 구성**( `com.day.cq.wcm.undo.UndoConfigService`)은 페이지 편집을 위한 실행 취소 및 다시 실행 명령의 동작을 제어하는 여러 속성을 표시합니다.

## 기본 구성 {#default-configuration}

표준 설치에서 기본 설정은 `sling:OsgiConfig`node에 속성으로 정의됩니다.

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

이 노드에는 기본값을 가져오는 다른 속성에 대해 `cq.wcm.undo.whitelist` 및 `cq.wcm.undo.blacklist` 속성이 포함됩니다.

>[!CAUTION]
>
>***은(는) `/libs` 경로에서 아무 것도 변경하지 않아야 합니다.***
>
>이는 다음 번에 인스턴스를 업그레이드할 때 `/libs`의 콘텐트가 덮어쓰기되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓰여질 수 있음).

## 실행 취소 구성 및 다시 실행 {#configuring-undo-and-redo}

자신의 인스턴스에 대해 이러한 OSGi 서비스 속성을 구성할 수 있습니다.

>[!NOTE]
>
>AEM으로 작업할 때 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 여러 가지가 있습니다.자세한 내용 및 권장 방법은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성을 참조하십시오.

다음은 웹 콘솔에 표시된 속성과 해당 OSGi 매개 변수의 이름, 설명 및 기본값(적절한 경우)을 차례로 나열합니다.

* **사용**
( 
`cq.wcm.undo.enabled`)

   * **설명**:페이지 작성자가 변경 사항을 실행 취소하거나 재실행할 수 있는지 여부를 결정합니다.
   * **기본값**:  `Selected`
   * **유형**: `Boolean`

* **경로**
( 
`cq.wcm.undo.path`)

   * **설명**:이진 실행 취소 데이터를 지속하기 위한 저장소 경로입니다. 작성자가 이미지와 같은 이진 데이터를 변경하면 데이터의 원래 버전이 여기에 유지됩니다. 이진 데이터의 변경 내용이 실행 취소되면 이 이진 실행 취소 데이터가 페이지에 복원됩니다.
   * **기본값**:  `/var/undo`
   * **유형**: `String`

   >[!NOTE]
   >
   >기본적으로 관리자만 `/var/undo` 노드에 액세스할 수 있습니다. 이진 실행 취소 데이터에 액세스할 수 있는 권한이 부여된 후에만 이진 컨텐츠에 대해 실행 취소 및 다시 실행 작업을 수행할 수 있습니다.

* **최소. validity**
( 
`cq.wcm.undo.validity`)

   * **설명**:이진 실행 취소 데이터가 저장되는 최소 시간(시간)입니다. 이 기간이 지나면 이진 데이터를 사용하여 디스크 공간을 유지할 수 있습니다.
   * **기본값**:  `10`
   * **유형**: `Integer`

* **단계**
( 
`cq.wcm.undo.steps`)

   * **설명**:실행 취소 내역에 저장되는 페이지 작업의 최대 수입니다.
   * **기본값**:  `20`
   * **유형**: `Integer`

* **지속성**
( 
`cq.wcm.undo.persistence`)

   * **설명**:작업 내역을 실행 취소할 수 있는 클래스입니다. 2개의 지속성 클래스가 제공됩니다.

      * `CQ.undo.persistence.WindowNamePersistence`:window.name 속성을 사용하여 작업 내역을 유지합니다.
      * `CQ.undo.persistence.CookiePersistance`:쿠키를 사용한 기록을 유지합니다.
   * **기본값**:  `CQ.undo.persistence.WindowNamePersistence`
   * **유형**: `String`


* **지속성 모드**
( 
`cq.wcm.undo.persistence.mode`)

   * **설명**:실행 취소 내역이 지속되는 시기를 결정합니다. 각 페이지를 편집한 후 실행 취소 내역을 유지하려면 이 옵션을 선택합니다. 페이지를 다시 로드할 때만 유지되도록 하려면 이 옵션을 지우십시오(예: 사용자가 다른 페이지로 이동).

      실행 취소 내역은 웹 브라우저 리소스를 사용합니다. 사용자의 브라우저가 페이지 편집에 느리게 반응하는 경우 페이지를 다시 로드할 때 실행 취소 내역을 지속해 보십시오.

   * **기본값**:  `Selected`
   * **유형**: `Boolean`

* **마커 모드**
( 
`cq.wcm.undo.markermode`)

   * **설명**:실행 취소 또는 다시 실행이 발생할 때 영향을 받는 단락을 나타내는 데 사용할 시각적 단서를 지정합니다. 다음 값이 유효합니다.

      * flash:단락의 선택 표시기가 일시적으로 깜박입니다.
      * 선택:단락이 선택됩니다.
   * **기본값**:  `flash`
   * **유형**: `String`


* **우수한 구성 요소**
( 
`cq.wcm.undo.whitelist`)

   * **설명**:실행 취소 및 다시 실행 명령의 영향을 받을 구성 요소 목록입니다. 실행 취소/다시 실행으로 올바르게 작동할 때 이 목록에 구성 요소 경로를 추가합니다. 별표(&amp;ast;)를 추가하여 구성 요소 그룹을 지정합니다.

      * 다음 값은 기본 텍스트 구성 요소를 지정합니다.

         `foundation/components/text`

      * 다음 값은 모든 기본 구성 요소를 지정합니다.

         `foundation/components/*`
   * 이 목록에 없는 구성 요소에 실행 취소 또는 다시 실행이 실행되면 명령을 신뢰할 수 없음을 나타내는 메시지가 나타납니다.

   * **기본값**:이 속성은 AEM에서 제공하는 많은 구성 요소로 채워집니다.
   * **유형**: `String[]`


* **잘못된 구성 요소**
( 
`cq.wcm.undo.blacklist`)

   * **설명**:실행 취소 명령의 영향을 받지 않을 구성 요소 및/또는 구성 요소 작업의 목록입니다. 실행 취소 명령으로 올바르게 동작하지 않는 구성 요소 및 구성 요소 작업을 추가합니다.

      * 실행 취소 내역에서 구성 요소의 작업을 선택하지 않으려면 구성 요소 경로를 추가합니다(예: `collab/forum/components/post`).
      * 실행 취소 내역(다른 작업 기능이 올바르게 작동함)에서 특정 작업을 생략하려면 콜론(:)과 작업을 경로에 추가합니다. 예를 들어 `collab/forum/components/post:insertParagraph.`

   >[!NOTE]
   >
   >작업이 이 목록에 있는 경우에도 실행 취소 내역에 계속 추가됩니다. 사용자는 실행 취소 내역에서 **잘못된 구성 요소** 작업 이전에 존재하는 작업을 실행 취소할 수 없습니다.

   * 일반적인 작업 이름은 다음과 같습니다.

      * `insertParagraph`:구성 요소가 페이지에 추가됩니다.
      * `removeParagraph`:구성 요소가 삭제됩니다.
      * `moveParagraph`:단락이 다른 위치로 이동됩니다.
      * `updateParagraph`:단락 속성이 변경됩니다.
   * **기본값**:속성은 여러 구성 요소 작업으로 채워집니다.
   * **유형**: `String[]`




