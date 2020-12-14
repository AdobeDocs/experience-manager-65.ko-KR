---
title: 커뮤니티에 대한 Maven 사용
seo-title: 커뮤니티에 대한 Maven 사용
description: AEM Communities API jar 및 AEM Uber API jar
seo-description: AEM Communities API jar 및 AEM Uber API jar
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 2%

---


# 커뮤니티 {#using-maven-for-communities}에 대한 마비사항 사용

## 개요 {#overview}

AEM Communities 설명서의 이 섹션에서는 다음과 같은 항목을 다룹니다.

* [Apache Maven을 사용하여 AEM 프로젝트 제작](../../help/sites-developing/ht-projects-maven.md).

이제 개별 아티팩트를 대체하는 두 가지 &quot;우버&quot; 아티팩트가 있습니다.

* AEM [커뮤니티 API jar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## 커뮤니티 API Jar 아티팩트 {#communities-api-jar-artifact}

다음은 AEM Communities API jar용 GAV의 예입니다.

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
```

지정된 버전이 AEM Communities용으로 설치된 커뮤니티 패키지 버전과 일치하는지 확인합니다. 설치된 버전 번호를 확인하려면:

1. 관리자 권한으로 로그인합니다.
1. [패키지 관리자](../../help/sites-administering/package-manager.md)로 이동합니다. 예: [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

1. 패키지를 찾습니다.`cq-socialcommunities-pkg-1.x.xxx`
1. 패키지 이름에서 버전 추출:
   * AEM 6.3의 첫 번째 버전은 버전 1.11.170.
   * 기능 팩은 버전 1.12.xxx입니다.

>[!NOTE]
>
>최신 커뮤니티 릴리스를 최신 상태로 유지하는 것이 좋습니다.
>
>최신 버전을 확인하려면 [최신 릴리스](deploy-communities.md#latest-releases) 섹션을 참조하십시오.

## 종속 관계 예 {#maven-dependency-example}

커뮤니티 API jar를 Uber API jar 앞에 지정해야 합니다.

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
