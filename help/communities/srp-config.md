---
title: 스토리지 구성
description: 사용자 생성 콘텐츠라고도 하는 커뮤니티 콘텐츠에 대해 선택한 저장소를 식별하는 수단으로서 저장소 구성 콘솔에 대해 알아봅니다.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 4%
---
# 스토리지 구성 {#storage-configuration}

스토리지 구성은 UGC(사용자 생성 컨텐츠)라고도 하는 커뮤니티 컨텐츠에 대해 선택된 스토리지를 식별하는 수단입니다.

이 설정은 UGC에 액세스할 때 SRP(저장소 리소스 제공자) 구현이 사용되는지를 AEM Communities 코드에 알려 줍니다. Adobe Experience Manager(AEM)가 배포되었을 때 설정된 토폴로지를 반영해야 합니다.

스토리지 옵션 및 구축 토폴로지에 대한 자세한 내용은 다음을 참조하십시오.

* [커뮤니티 콘텐츠 저장소](working-with-srp.md)
* [권장 토폴로지](topologies.md)

## 스토리지 구성 콘솔 {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

작성자 환경에서 스토리지 구성 콘솔로 이동합니다.

* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 저장소 구성]**&#x200B;을 선택합니다.

기본 JCR 이외의 저장 영역 옵션을 선택하려면 다음과 같이 하십시오.

* 옵션 선택
* 적절히 구성

  * [MSRP 선택](msrp.md#select-msrp)에 대한 세부 정보 보기
  * [DSRP 선택](dsrp.md#select-dsrp)에 대한 세부 정보 보기
  * [ASRP 선택](asrp.md#select-asrp)에 대한 세부 정보 보기

* **[!UICONTROL 제출]**&#x200B;을 선택합니다.

### JCR 저장소 정보 {#about-jcr-storage}

선택하지 않으면 기본값은 AEM 저장소인 JCR입니다.

JCR은 작성자 및 게시 환경에서 공유하는 일반 저장소로 *not*&#x200B;입니다. 커뮤니티 콘텐츠는 콘텐츠가 만들어진 작성자 또는 게시 환경에서만 볼 수 있습니다.

자세한 내용은 [JCR 저장소](jsrp.md)를 참조하세요.

>[!NOTE]
>
>`/etc/socialconfig` 아래에 `srpc` 노드가 없으면 기본 [JCR 저장소](jsrp.md)를 나타냅니다.
