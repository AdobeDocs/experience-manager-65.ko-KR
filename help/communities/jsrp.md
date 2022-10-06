---
title: JSRP - JCR 저장소 리소스 공급자
seo-title: JSRP - JCR Storage Resource Provider
description: JSRP는 일반적으로 한 개의 게시 인스턴스와 한 개의 작성자 인스턴스의 데모 또는 개발 환경에 가장 적합합니다
seo-description: JSRP is generally best suited for demonstration or development environments of one publish instance and one author instance
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# JSRP - JCR 저장소 리소스 공급자 {#jsrp-jcr-storage-resource-provider}

## JSRP 정보 {#about-jsrp}

AEM Communities에서 JSRP를 저장 옵션(기본값)으로 사용하는 경우 커뮤니티 컨텐츠는 JCR에 저장되고 UGC(사용자 생성 컨텐츠)는 게시된 작성자 또는 게시 인스턴스에서만 액세스할 수 있습니다.

배포의 단순성 때문에 JSRP는 일반적으로 하나의 게시 인스턴스와 하나의 작성 인스턴스의 데모 또는 개발 환경에 가장 적합합니다.

참조 - [SRP 옵션 특성](working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](topologies.md).

## 구성 {#configuration}

### JSRP 선택 {#select-jsrp}

기본적으로 JSRP는 UGC의 저장소 옵션입니다.

다음 [스토리지 구성 콘솔](srp-config.md) 에서는 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성 환경에서 스토리지 구성 콘솔에 도달하려면

* 전역 탐색에서: **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 스토리지 구성]**

* 선택 **[!UICONTROL JCR 저장소 리소스 공급자(JSRP)]**

* **[!UICONTROL 제출]**&#x200B;을 선택합니다

![jsrp 구성](assets/jsrp-configuration.png)

### 구성 게시 {#publishing-the-configuration}

JSRP가 기본 구성이지만 게시 환경에서 동일한 구성이 설정되도록 하려면:

* 전역 탐색에서: **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]**
* 선택 **[!UICONTROL 트리 활성화]** > **[!UICONTROL 시작 경로]**:

   * 찾아보기 `/conf/global/settings/community/srpc/`

* 선택 **[!UICONTROL 활성화]**

## 사용자 데이터 관리 {#managing-user-data}

관련 정보 *사용자*, *사용자 프로필* 및 *사용자 그룹*: 게시 환경에 자주 입력되는 방문입니다.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## 문제 해결 {#troubleshooting}

### JCR에 UGC가 표시되지 않음 {#ugc-not-visible-in-jcr}

저장소 옵션의 구성을 확인하여 JSRP가 기본 공급자로 구성되었는지 확인하십시오. 기본적으로 저장소 리소스 공급자는 JSRP입니다.

모든 작성 및 게시 AEM 인스턴스에서 Storage Configuration 콘솔을 다시 방문하거나 AEM 리포지토리를 확인합니다.

* JCR에서 [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 다음을 포함하지 않음 [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) node이면 스토리지 공급자가 JSRP임을 의미합니다.
   * srpc 노드가 존재하며 노드를 포함하는 경우 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)를 지정하는 경우 기본 구성의 속성에 JSRP가 기본 공급자로 정의되어 있어야 합니다.

### 작성자 인스턴스에 UGC가 표시되지 않음 {#ugc-not-visible-on-author-instance}

버그가 아닙니다. JSRP의 특징은 게시 환경에 입력한 커뮤니티 컨텐츠가 게시 환경에서만 표시된다는 것입니다.

### 게시 인스턴스에 UGC가 표시되지 않음 {#ugc-not-visible-on-publish-instance}

단일 게시 인스턴스나 게시 클러스터가 배포되는 경우 다음에 대한 지침을 따르십시오 [JCR에 UGC가 표시되지 않음](#ugc-not-visible-in-jcr).

게시 팜이 배포된 경우 JSRP의 특징은 커뮤니티 컨텐츠가 게시된 게시 인스턴스에만 표시된다는 것입니다.

게시 인스턴스에서 UGC를 표시하려면 게시 클러스터가 필요합니다.
