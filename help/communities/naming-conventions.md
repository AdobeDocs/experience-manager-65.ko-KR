---
title: Java&trade; 패키지 이름의 이름 지정 규칙
description: Java&trade; 패키지 이름에서 이름 지정 규칙 및 하이픈 사용에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---

# 이름 지정 규칙 {#naming-conventions}

## Java™ 패키지 이름의 하이픈 {#hyphens-in-java-package-name}

Java™ 클래스의 위치를 만들 때 패키지 이름은 경로에 있는 하이픈이 올바르게 이스케이프되는 저장소 폴더 위치의 이름과 일치해야 합니다.

AEM 개발에서는 저장소 항목 이름에 하이픈을 사용하는 것이 권장되지만 Java™ 패키지 이름 내에서는 하이픈을 사용할 수 없습니다.

기본 CRX 플랫폼은 실제 밑줄을 구별할 수 있어야 합니다 `_ `및 하이픈 `-`. 따라서 JCR에서 하이픈은 유니코드 값(u002d)으로 대체하고 밑줄로 이스케이프해야 합니다 `_`.

예를 들어 저장소 경로가 인 경우 **/apps/my-example/component/info/Info.java**, 패키지 이름은 다음과 같아야 합니다. `java package apps.my_002dexample.component.info;`

밑줄도 비슷하게 이스케이프해야 하므로 `_` 다음과 같음 `_005f`.
