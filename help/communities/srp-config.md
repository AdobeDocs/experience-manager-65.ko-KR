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
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 5%

---


# 저장소 구성 {#storage-configuration}

스토리지 구성은 UGC(사용자 생성 컨텐츠)라고도 하는 커뮤니티 컨텐츠에 대해 선택한 스토리지를 식별하는 방법입니다.

이 설정은 UGC에 액세스할 때 어떤 SRP(저장소 리소스 공급자)의 구현을 사용할지 AEM Communities 코드에 알려 주고 AEM 배포 시 설정된 토폴로지를 반영해야 합니다.

스토리지 옵션 및 배포 토폴로지에 대한 자세한 내용은 다음을 참조하십시오.

* [커뮤니티 콘텐츠 스토어](working-with-srp.md)
* [권장 토폴로지](topologies.md)

## 스토리지 구성 콘솔 {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

작성 환경에서 스토리지 구성 콘솔에 도달합니다.

* 전역 탐색에서 **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 스토리지 구성]**&#x200B;을 선택합니다.

기본 JCR 이외의 저장 영역 옵션을 선택하려면 다음을 수행합니다.

* 옵션 선택
* 적절하게 구성

   * [MSRP](msrp.md#select-msrp)에 대한 세부 정보를 참조하십시오.
   * [DSRP](dsrp.md#select-dsrp)에 대한 세부 정보를 참조하십시오.
   * [ASRP](asrp.md#select-asrp)에 대한 세부 정보를 참조하십시오.

* **[!UICONTROL 제출]**&#x200B;을 선택합니다.

### JCR 스토리지 정보 {#about-jcr-storage}

선택하지 않으면 기본적으로 AEM 저장소인 JCR이 사용됩니다.

JCR은 작성 및 게시 환경에서 공유되는 공용 저장소가 아닌 *입니다.* 커뮤니티 컨텐츠는 커뮤니티 컨텐츠가 만들어진 작성자 또는 게시 환경에서만 표시됩니다.

자세한 내용은 [JCR 스토어](jsrp.md)를 참조하십시오.

>[!NOTE]
>
>`/etc/socialconfig` 아래의 `srpc` 노드가 없는 것은 기본 [JCR 스토어](jsrp.md)를 나타냅니다.
