---
title: Jave 컨텐츠 저장소에 있는 노드의 이름 지정 규칙
description: 저장소의 노드는 Java 컨텐츠 저장소의 이름 지정 규칙을 따릅니다
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 7%

---

# 이름 지정 규칙{#naming-conventions}

저장소의 노드는 [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). 그러나 AEM에서는 페이지 노드의 이름에 대한 추가적인 규칙을 적용합니다.

## 페이지에 대한 이름 지정 규칙 {#naming-conventions-for-pages}

이러한 이름 지정 규칙은 다음과 같은 다양한 수준에서 구현됩니다.

* JcrUtil: 의 AEM 구현 [JCR 유틸리티](#jcr-utilities).
* 페이지 관리자: a [페이지 관리자](#page-manager) 페이지 수준 작업에 대한 메서드를 제공합니다.
* 사용되는 UI에 따라:

   * [표준, 터치 지원 UI](#standard-ui)
   * [클래식 UI](#classic-ui)

### JCR 유틸리티 {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) 는 JCR 유틸리티의 AEM 구현입니다. 이름 유효성 검사에 대한 특정 관심 사항은 이 컨트롤이 제어하는 문자 매핑과 다음 유효성 검사입니다.

* `isValidName`

   * 이름이 비어 있지 않고 올바른 문자만 포함되어 있는지 확인합니다.
   * 제안된 이름이 유효한지 확인하는 데 사용할 수 있습니다.

* `createValidName`

   * 이렇게 하면 임의의 문자열로 유효한 레이블이 만들어집니다.
   * 제목에서 이름을 만드는 데 사용할 수 있습니다.

### 페이지 관리자 {#page-manager}

[PageManager](https://helpx.adobe.com/kr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) 에서는 다음을 기준으로 페이지 수준 작업에 대한 메서드를 제공합니다 [JCRUtil](#jcr-utilities).

### 표준 UI {#standard-ui}

터치 지원 표준 UI:

* 다음 경우 PageManager에서 지정한 제한에 따라 이름을 확인합니다.

   * 노드 이름으로 전환할 페이지 제목이 제공됩니다
   * 명시적 노드 이름이 제공됩니다

### 클래식 UI {#classic-ui}

클래식 UI에서는 더 엄격한 제한을 적용합니다.

* 다음 중 한 경우에 명시적 노드 이름이 있을 때 이름을 확인합니다.

   * 노드 이름으로 전환할 페이지 제목이 제공됩니다
   * 명시적 노드 이름이 제공됩니다

* 유효한 문자(클래식 UI 내에서 페이지가 작성될 때에도 실제로 유효한 문자) `PageManagerImpl` 에는 추가 문자가 허용됨:

   * &#39;a&#39;~&#39;z&#39;
   * &#39;A&#39;~&#39;Z&#39;
   * &#39;0&#39;~&#39;9&#39;
   * _(밑줄)
   * `-` (대시/빼기)
