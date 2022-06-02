---
title: 특정 버전의 Oracle JDK에서 Experience Manager Forms을 사용할 수 없습니다
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: 특정 버전의 Oracle JDK에서 Experience Manager Forms을 사용할 수 없습니다
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
source-git-commit: 91b012f8024350effc19613bcecfc42dee4130d9
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 4%

---

# 특정 버전의 Oracle JDK에서 Experience Manager Forms을 사용할 수 없습니다 {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

이 문제는 다음 버전에 적용됩니다.

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## 문제 {#issue}

사용자는 다음과 같은 예외가 발생합니다.
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 이유 {#reason}

다음 버전보다 크거나 같은 Oracle JDK(Java Development Kit) 버전과 함께 Experience Manager Forms을 실행하는 경우 예외가 발생합니다.

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

위에서 언급한 Java 및 이후 버전에는 특정 Forms 특정 작업이 실패하는 JVM(Java Virtual Machine)의 새로운 XML 처리 제한이 포함되어 있습니다.

## 해결 방법 {#workaround}

1. Experience Manager Forms 서버를 중지합니다.
1. 애플리케이션 서버에 대해 다음 JVM 인수를 구성합니다.

   `-Djdk.xml.xpathExprOpLimit=2000`

   기본 제한이 히트되지 않도록 JVM의 시스템 속성을 상당히 높은 값으로 설정합니다.

1. Experience Manager Forms 서버를 시작합니다.
