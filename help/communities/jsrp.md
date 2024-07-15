---
title: JSRP - JCR 저장소 리소스 제공자
description: JSRP는 하나의 Publish 인스턴스와 하나의 작성자 인스턴스의 데모 또는 개발 환경에 가장 적합합니다
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# JSRP - JCR 저장소 리소스 제공자 {#jsrp-jcr-storage-resource-provider}

## JSRP 정보 {#about-jsrp}

AEM Communities이 JSRP를 저장소 옵션(기본값)으로 사용하는 경우 커뮤니티 콘텐츠는 JCR에 저장되고 UGC(사용자 생성 콘텐츠)는 해당 콘텐츠가 게시된 작성자 또는 게시 인스턴스에서만 액세스할 수 있습니다.

배포가 단순하기 때문에 JSRP는 하나의 Publish 인스턴스와 하나의 작성자 인스턴스의 데모 또는 개발 환경에 가장 적합합니다.

[SRP 옵션의 특성](working-with-srp.md#characteristics-of-srp-options) 및 [권장 토폴로지](topologies.md)도 참조하세요.

## 구성 {#configuration}

### JSRP 선택 {#select-jsrp}

기본적으로 JSRP는 UGC에 대한 저장소 옵션입니다.

[저장소 구성 콘솔](srp-config.md)에서 사용할 SRP 구현을 식별하는 기본 저장소 구성을 선택할 수 있습니다.

작성 환경에서 스토리지 구성 콘솔로 이동합니다.

* 전역 탐색에서: **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 저장소 구성]**

* **[!UICONTROL JCR 저장소 리소스 공급자(JSRP) 선택]**

* **[!UICONTROL 제출]** 선택

![jsrp-configuration](assets/jsrp-configuration.png)

### 구성 게시 {#publishing-the-configuration}

JSRP가 기본 구성이지만 게시 환경에 동일한 구성이 설정되도록 하려면 다음을 수행하십시오.

* 전역 탐색에서: **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]**
* **[!UICONTROL 트리 활성화]** > **[!UICONTROL 시작 경로]**&#x200B;를 선택합니다.

   * `/conf/global/settings/community/srpc/`(으)로 이동

* **[!UICONTROL 활성화]** 선택

## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 종종 입력된 *사용자*, *사용자 프로필* 및 *사용자 그룹*&#x200B;에 대한 자세한 내용을 보려면 다음을 방문하십시오.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## 문제 해결 {#troubleshooting}

### JCR에서 UGC가 표시되지 않음 {#ugc-not-visible-in-jcr}

저장소 옵션의 구성을 확인하여 JSRP가 기본 공급자로 구성되었는지 확인하십시오. 기본적으로 저장소 리소스 공급자는 JSRP입니다.

모든 Author 및 Publish AEM 인스턴스에서 저장소 구성 콘솔을 다시 방문하거나 AEM 저장소를 확인합니다.

* JCR에서, [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)인 경우

   * [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) 노드가 포함되어 있지 않습니다. 저장소 공급자가 JSRP입니다.
   * srpc 노드가 존재하고 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration) 노드를 포함하는 경우 defaultconfiguration의 속성은 JSRP를 기본 공급자로 정의해야 합니다.

### 작성자 인스턴스에 UGC가 표시되지 않음 {#ugc-not-visible-on-author-instance}

버그가 아닙니다. JSRP의 특징은 게시 환경에 입력된 커뮤니티 콘텐츠가 Publish 환경에서만 표시된다는 것입니다.

### UGC가 Publish 인스턴스에 표시되지 않음 {#ugc-not-visible-on-publish-instance}

단일 Publish 인스턴스 또는 게시 클러스터가 배포된 경우 [UGC가 JCR에 표시되지 않음](#ugc-not-visible-in-jcr)에 대한 지침을 따르십시오.

게시 팜이 배포된 경우 JSRP의 특징은 커뮤니티 콘텐츠가 게시된 Publish 인스턴스에만 표시된다는 것입니다.

UGC가 Publish 인스턴스에서 표시되도록 하려면 게시 클러스터가 필요합니다.
