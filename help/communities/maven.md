---
title: Maven for Communities 사용
description: 커뮤니티에서 사용할 Adobe Experience Manager Uber API Jar에 대해 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3df90511-e43e-442b-bf73-44c22c1886b7
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Maven for Communities 사용 {#using-maven-for-communities}

## 개요 {#overview}

Adobe Experience Manager(AEM) Communities 설명서의 이 섹션에는 다음 사항이 포함됩니다.

* [Apache Maven을 사용하여 AEM 프로젝트 빌드](../../help/sites-developing/ht-projects-maven.md).

개별 아티팩트를 대체하는 &quot;uber&quot; 아티팩트는 하나만 있습니다.

* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

>[!NOTE]
>
>AEM 6.4 이상에서는 커뮤니티 API가 명시적으로 릴리스되지 않습니다. 이제 모든 Communities API가 Uber jar 자체에 포함됩니다.
>
>최신 Communities 릴리스를 최신 상태로 유지합니다.
>
>다음을 참조하십시오. [최신 릴리스](deploy-communities.md#latest-releases) 가장 최근 버전을 식별할 수 있는 섹션입니다.

## Maven 종속성 예 {#maven-dependency-example}

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.7</version>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>다음을 참조하십시오. [AEM Uber jar 저장소](https://mvnrepository.com/artifact/com.adobe.aem/uber-jar) 여기서 최신 Uber jar 아티팩트를 식별할 수 있습니다.

<!--
There are now two "uber" artifacts that replace individual artifacts:

* AEM [Communities API jar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Communities API Jar Artifact {#communities-api-jar-artifact}

Following is an example of a GAV for the AEM Communities API jar:

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>

```

Ensure thet the version specified corresponds with the Communities package version installed for AEM Communities. To verify the installed version number:

1. Log in with adminstrative privileges.
1. Browse to [Package Manager](../../help/sites-administering/package-manager.md). For example, [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. Locate the package: `cq-socialcommunities-pkg-1.x.xxx`
1. Extract the version from the package name:
   * First version for AEM 6.3 is version 1.11.170.
   * Feature packs is versions 1.12.xxx.

>[!NOTE]
>
>It is recommended to keep up-to-date with the most recent Communities release.
>
>Visit the [Latest Releases](deploy-communities.md#latest-releases) section to identify the most recent version.

## Maven Dependency Example {#maven-dependency-example}

The Communities API jar must be specified before the Uber API jar.

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.3.0</version>
    <scope>provided</scope>
    <classifier>apis</classifier>
</dependency>
```
-->
