---
title: 저장소 구성
seo-title: 저장소 구성
description: 스토리지 구성 콘솔에 액세스하는 방법
seo-description: 스토리지 구성 콘솔에 액세스하는 방법
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Administrator
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 5%

---

# 저장소 구성 {#storage-configuration}

스토리지 구성은 UGC(사용자 생성 컨텐츠)라고도 하는 커뮤니티 컨텐츠에 대해 선택한 스토리지를 식별하는 방법입니다.

이 설정은 UGC에 액세스할 때 SRP(저장소 리소스 제공자)의 구현을 사용할 것인지 AEM Communities 코드에 알려주며, AEM이 배포될 때 설정된 토폴로지를 반영해야 합니다.

스토리지 옵션 및 배포 토폴로지에 대해 알아보려면 다음 페이지를 참조하십시오.

* [커뮤니티 콘텐츠 저장소](working-with-srp.md)
* [권장 토폴로지](topologies.md)

## 스토리지 구성 콘솔 {#storage-configuration-console}

![jsrp 구성](assets/jsrp-configuration.png)

작성 환경에서 스토리지 구성 콘솔에 연결합니다.

* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 저장소 구성]**&#x200B;을 선택합니다.

기본 JCR 이외의 저장소 옵션을 선택하려면 다음을 수행합니다.

* 옵션 선택
* 적절하게 구성

   * [MSRP](msrp.md#select-msrp)에 대한 세부 정보를 참조하십시오
   * [DSRP](dsrp.md#select-dsrp)에 대한 세부 정보를 참조하십시오
   * [ASRP](asrp.md#select-asrp)에 대한 세부 정보를 참조하십시오

* **[!UICONTROL 제출]**&#x200B;을 선택합니다.

### JCR 스토리지 정보 {#about-jcr-storage}

선택하지 않으면 기본값은 AEM 저장소인 JCR입니다.

JCR은 작성 및 게시 환경에 의해 공유되는 공통 저장소가 아닌 *입니다.* 커뮤니티 콘텐츠는 만든 작성자 또는 게시 환경에서만 표시됩니다.

추가 정보를 보려면 [JCR Store](jsrp.md)를 방문하십시오.

>[!NOTE]
>
>`/etc/socialconfig` 아래에 `srpc` 노드가 없으면 기본 [JCR store](jsrp.md)가 표시됩니다.
