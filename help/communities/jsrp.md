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
source-git-commit: c798eb79dc9f8e58cef86cf90af02622c3a2ed78
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# JSRP - JCR 스토리지 리소스 공급자 {#jsrp-jcr-storage-resource-provider}

## JSRP 정보 {#about-jsrp}

AEM Communities에서 JSRP를 저장 옵션으로 사용하는 경우(기본값), 커뮤니티 컨텐츠는 JCR에 저장되고 UGC(사용자 생성 컨텐츠)는 게시된 작성자 또는 게시 인스턴스에서만 액세스할 수 있습니다.

배포의 단순성 때문에 JSRP는 일반적으로 하나의 게시 인스턴스와 하나의 작성 인스턴스의 데모 또는 개발 환경에 가장 적합합니다.

SRP 옵션 [및 권장 토폴로지](working-with-srp.md#characteristics-of-srp-options) 의 [특성을 참조하십시오](topologies.md).

## 구성 {#configuration}

### JSRP 선택 {#select-jsrp}

기본적으로 JSRP는 UGC의 스토리지 옵션입니다.

스토리지 [구성 콘솔에서는](srp-config.md) 사용할 SRP 구현을 식별하는 기본 스토리지 구성을 선택할 수 있습니다.

작성 환경에서 스토리지 구성 콘솔에 도달하려면

* 전역 탐색에서: **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 스토리지 구성]**

* Select **[!UICONTROL JCR Storage Resource Provider (JSRP)]**

* **[!UICONTROL 제출]**&#x200B;을 선택합니다

![chlimage_1-234](assets/chlimage_1-234.png)

### 구성 게시 {#publishing-the-configuration}

JSRP는 기본 구성이지만 게시 환경에서 동일한 구성이 설정되어 있는지 확인합니다.

* 작성자:

   * 전역 탐색에서: **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]**
   * 트리 **[!UICONTROL 활성화]** > **[!UICONTROL 시작 경로를 선택합니다]**.

      * 검색 대상 `/conf/global/settings/community/srpc/`
   * 활성화 **[!UICONTROL 선택]**


## 사용자 데이터 관리 {#managing-user-data}

게시 환경에 자주 입력되는 *사용자*, *사용자 프로필* 및 *사용자 그룹에*&#x200B;대한 자세한 내용은 다음을 참조하십시오.

* [사용자 동기화](sync.md)
* [사용자 및 사용자 그룹 관리](users.md)

## 문제 해결 {#troubleshooting}

### JCR에 UGC 표시 안 됨 {#ugc-not-visible-in-jcr}

저장소 옵션의 구성을 확인하여 JSRP가 기본 공급자로 구성되었는지 확인하십시오. 기본적으로 저장소 리소스 공급자는 JSRP입니다.

모든 작성 및 AEM 인스턴스에서 스토리지 구성 콘솔을 다시 방문하거나 AEM 저장소를 확인합니다.

* JCR에서, if [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * srpc 노드가 [포함되어](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) 있지 않으므로 스토리지 공급자가 JSRP임을 의미합니다.
   * srpc 노드가 있고 노드 [기본 구성을](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)포함하는 경우, defaultconfiguration의 속성은 JSRP를 기본 공급자로 정의해야 합니다.

### 작성자 인스턴스에 UGC가 표시되지 않음 {#ugc-not-visible-on-author-instance}

버그가 아닙니다. JSRP의 특징은 게시 환경에 입력된 커뮤니티 컨텐츠는 게시 환경에서만 표시된다는 것입니다.

### 게시 인스턴스에 UGC가 표시되지 않음 {#ugc-not-visible-on-publish-instance}

단일 게시 인스턴스 또는 게시 클러스터가 배포된 경우 JCR에 표시되지 않는 [UGC에 대한 지침을 따릅니다](#ugc-not-visible-in-jcr).

게시 팜이 배포된 경우 JSRP의 특징은 커뮤니티 컨텐츠가 게시된 게시 인스턴스에만 표시될 수 있다는 것입니다.

모든 게시 인스턴스에서 UGC를 표시하려면 게시 클러스터가 필요합니다.
