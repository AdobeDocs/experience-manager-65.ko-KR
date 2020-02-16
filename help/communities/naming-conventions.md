---
title: 이름 지정 규칙
seo-title: 이름 지정 규칙
description: Java 패키지 이름의 하이픈
seo-description: Java 패키지 이름의 하이픈
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 이름 지정 규칙 {#naming-conventions}

## Java 패키지 이름의 하이픈 {#hyphens-in-java-package-name}

Java 클래스의 위치를 만들 때는 패키지 이름이 경로에 하이픈이 있는 저장소 폴더 위치의 이름과 일치해야 합니다.

저장소 항목 이름에 하이픈을 사용하는 것은 AEM 개발 시 권장되지만 Java 패키지 이름 내에서는 하이픈이 잘못되었습니다.

기본 CRX 플랫폼은 실제 밑줄 &#39;_&#39;과 하이픈 &#39;-&#39;를 구분할 수 있어야 합니다. 따라서 JCR에서 하이픈은 유니코드 값(u002d)으로 대체되어야 하며 밑줄 &#39;_&#39;로 이스케이프해야 합니다.

예를 들어 저장소 경로가 /apps/my-example/component/info/Info.java **인**&#x200B;경우 패키지 이름은 `java package apps.my_002dexample.component.info;`

밑줄이 유사한 방식으로 이스케이프되어야 합니다. 이렇게 `_` 하면 `_005f`됩니다.
