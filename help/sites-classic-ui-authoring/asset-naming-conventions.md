---
title: 자산 테스트를 위한 명명 규칙
description: 저장소의 노드는 Java Content Repository의 이름 지정 규칙에 따릅니다. 하지만 Adobe Experience Manager은 에셋 노드의 이름에 대한 추가 규칙을 지정합니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 9%
---
# 자산 테스트를 위한 명명 규칙{#naming-conventions-for-assets-testing}

저장소의 노드는 [Java 콘텐츠 저장소](/help/sites-developing/the-basics.md#java-content-repository)의 이름 지정 규칙을 따릅니다. 하지만 Adobe Experience Manager은 에셋 노드의 이름에 대한 추가 규칙을 지정합니다.

## 클래식 UI {#classic-ui}

클래식 UI는 더 엄격한 제한을 적용합니다.

* 명시적 노드 이름이 다음 중 하나에 해당할 경우 자산 이름을 확인합니다.

  * 노드 이름으로 변환하기 위한 자산 제목이 제공됩니다.
  * 명시적인 노드 이름이 입력되었습니다.

* 유효한 문자(이 문자만 클래식 UI 내에서 에셋을 만드는 경우 실제로 유효함):

  * &#39;a&#39;에서 &#39;z&#39;로
  * &#39;A&#39;에서 &#39;Z&#39;로
  * &#39;0&#39;에서 &#39;9&#39;
  * _(밑줄)
  * `-`(대시/빼기)
