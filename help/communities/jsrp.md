---
title: JSRP - JCR 스토리지 리소스 공급자
seo-title: JSRP - JCR 스토리지 리소스 공급자
description: JSRP는 일반적으로 하나의 게시 인스턴스와 하나의 작성 인스턴스의 데모 또는 개발 환경에 가장 적합합니다
seo-description: JSRP는 일반적으로 하나의 게시 인스턴스와 하나의 작성 인스턴스의 데모 또는 개발 환경에 가장 적합합니다
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
translation-type: tm+mt
source-git-commit: e7268e43620860b7a1f7aa0a1f1a54199dadcf17
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# JSRP - JCR 저장소 리소스 공급자 {#jsrp-jcr-storage-resource-provider}

## JSRP {#about-jsrp} 정보

AEM Communities이 JSRP를 저장 옵션(기본값)으로 사용하는 경우, 커뮤니티 컨텐츠는 JCR에 저장되고 사용자가 생성한 컨텐츠(UGC)는 게시된 작성자 또는 게시 인스턴스에서만 액세스할 수 있습니다.

배포의 단순성 때문에 JSRP는 일반적으로 하나의 게시 인스턴스와 하나의 작성 인스턴스의 데모 또는 개발 환경에 가장 적합합니다.

[SRP 옵션](working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](topologies.md)도 참조하십시오.

## 구성 {#configuration}

### JSRP {#select-jsrp} 선택

기본적으로 JSRP는 UGC의 스토리지 옵션입니다.

[스토리지 구성 콘솔](srp-config.md)에서는 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성 환경에서 스토리지 구성 콘솔에 도달하려면

* 전역 탐색에서:**[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 스토리지 구성]**

* **[!UICONTROL JCR JSRP(Storage Resource Provider)]** 선택

* **[!UICONTROL 제출]**&#x200B;을 선택합니다

![jsrp 구성](assets/jsrp-configuration.png)

### 구성 {#publishing-the-configuration} 게시

JSRP는 기본 구성이지만 게시 환경에서 동일한 구성이 설정되어 있는지 확인합니다.

* 전역 탐색에서:**[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]**
* **[!UICONTROL 트리 활성화]** > **[!UICONTROL 시작 경로]**&#x200B;를 선택합니다.

   * `/conf/global/settings/community/srpc/` 찾아보기

* **[!UICONTROL 활성화]** 선택

## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 종종 입력되는 *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;에 대한 자세한 내용은 다음을 참조하십시오.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## 문제 해결 {#troubleshooting}

### JCR {#ugc-not-visible-in-jcr}에 UGC가 표시되지 않음

저장소 옵션의 구성을 확인하여 JSRP가 기본 공급자로 구성되었는지 확인하십시오. 기본적으로 저장소 리소스 공급자는 JSRP입니다.

모든 작성 및 게시 AEM 인스턴스에서 스토리지 구성 콘솔을 다시 방문하거나 AEM 저장소를 확인합니다.

* JCR에서 [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) 노드가 포함되어 있지 않습니다. 이는 저장소 공급자가 JSRP임을 의미합니다.
   * srpc 노드가 존재하며 노드 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)을 포함하는 경우 기본 구성의 속성은 JSRP를 기본 공급자로 정의해야 합니다.

### 작성자 인스턴스 {#ugc-not-visible-on-author-instance}에 UGC가 표시되지 않음

버그가 아닙니다. JSRP의 특징은 게시 환경에 입력된 커뮤니티 컨텐츠는 게시 환경에서만 표시된다는 것입니다.

### 게시 인스턴스 {#ugc-not-visible-on-publish-instance}에 UGC가 표시되지 않음

단일 게시 인스턴스나 게시 클러스터가 배포된 경우, JCR](#ugc-not-visible-in-jcr)에 표시되지 않음 [UGC에 대한 지침을 따르십시오.

게시 팜이 배포된 경우 JSRP의 특징은 커뮤니티 컨텐츠가 게시된 게시 인스턴스에만 표시될 수 있다는 것입니다.

모든 게시 인스턴스에서 UGC를 표시하려면 게시 클러스터가 필요합니다.
