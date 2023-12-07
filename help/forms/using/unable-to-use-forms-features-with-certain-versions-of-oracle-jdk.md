---
title: 특정 버전의 Oracle JDK에서 Experience Manager Forms을 사용할 수 없음
description: 특정 버전의 Oracle JDK에서 Experience Manager Forms을 사용할 수 없음
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---

# 특정 버전의 Oracle JDK에서 Experience Manager Forms을 사용할 수 없음 {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

이 문제는 다음 버전에 적용됩니다.

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## 문제 {#issue}

사용자에게 다음 예외가 발생했습니다.
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 원인 {#reason}

단, Experience Manager Forms을 다음 버전보다 크거나 같은 Oracle JDK(Java Development Kit) 버전으로 실행할 때는 예외입니다.

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

위에서 언급한 버전 및 이후 버전의 Java에는 특정 Forms 특정 작업이 실패하는 JVM(Java Virtual Machine)의 새로운 XML 처리 제한이 포함되어 있습니다.

## 해결 방법 {#workaround}

1. Experience Manager Forms 서버를 중지합니다.
1. 애플리케이션 서버에 대해 다음 JVM 인수를 구성합니다.

   `-Djdk.xml.xpathExprOpLimit=2000`

   기본 제한에 도달하지 않도록 JVM의 시스템 속성을 상당히 높은 값으로 설정합니다.

1. Experience Manager Forms 서버를 시작합니다.
