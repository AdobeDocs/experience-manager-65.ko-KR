---
title: 테스트 자산에 대한 이름 지정 규칙
seo-title: Naming conventions for assets
description: 저장소의 노드는 Java 컨텐츠 저장소의 이름 지정 규칙을 따릅니다. 그러나 Adobe Experience Manager는 자산 노드의 이름에 대한 추가적인 규칙을 적용합니다.
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository. However, Adobe Experience Manager imposes further conventions for the name of asset nodes.
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 88%

---

# 자산에 대한 이름 지정 규칙 테스트{#naming-conventions-for-assets-testing}

저장소의 노드는 [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). 그러나 Adobe Experience Manager는 자산 노드의 이름에 대한 추가적인 규칙을 적용합니다.

## 클래식 UI {#classic-ui}

클래식 UI에서는 더 엄격한 제한 사항을 적용합니다.

* 다음 경우 중 하나에서 명시적 노드 이름이 있을 때 자산 이름의 유효성을 검사합니다.

   * 노드 이름으로 전환할 자산 제목이 제공됩니다.
   * 명시적 노드 이름이 제공됩니다.

* 유효한 문자(클래식 UI 내에서 자산이 만들어지는 경우 다음의 문자만 실제로 유효합니다.):

   * &#39;a&#39; ~ &#39;z&#39;
   * &#39;A&#39; ~ &#39;Z&#39;
   * &#39;0&#39; ~ &#39;9&#39;
   * _(밑줄)
   * `-` (대시/빼기 기호)
