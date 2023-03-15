---
title: 저장소 구성
seo-title: Storage Configuration
description: 스토리지 구성 콘솔에 액세스하는 방법
seo-description: How to access the Storage Configuration Console
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 4%

---

# 저장소 구성 {#storage-configuration}

저장소 구성은 UGC(사용자 생성 컨텐츠)라고도 하는 커뮤니티 컨텐츠에 대해 선택된 저장소를 식별하는 수단입니다.

이 설정은 UGC에 액세스할 때 SRP(저장소 리소스 제공자) 구현을 사용할 AEM Communities 코드를 알려 주며 AEM 배포 시 설정된 토폴로지를 반영해야 합니다.

스토리지 옵션 및 구축 토폴로지에 대한 자세한 내용은 다음을 참조하십시오.

* [커뮤니티 콘텐츠 저장소](working-with-srp.md)
* [권장 토폴로지](topologies.md)

## 스토리지 구성 콘솔 {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

작성 환경에서 스토리지 구성 콘솔로 이동합니다.

* 전역 탐색에서 을 선택합니다. **[!UICONTROL 도구]** > **[!UICONTROL 커뮤니티]** > **[!UICONTROL 스토리지 구성]**

기본 JCR 이외의 저장 영역 옵션을 선택하려면 다음과 같이 하십시오.

* 옵션 선택
* 적절히 구성

   * 다음에 대한 세부 사항 보기 [msrp 선택](msrp.md#select-msrp)
   * 다음에 대한 세부 사항 보기 [dsrp 선택](dsrp.md#select-dsrp)
   * 다음에 대한 세부 사항 보기 [ASRP 선택](asrp.md#select-asrp)

* **[!UICONTROL 제출]**&#x200B;을 선택합니다.

### JCR 저장소 정보 {#about-jcr-storage}

선택하지 않으면 기본값은 AEM 저장소인 JCR입니다.

JCR: *아님* 작성자 및 게시 환경에서 공유하는 공통 저장소입니다. 커뮤니티 콘텐츠는 콘텐츠가 만들어진 작성자 또는 게시 환경에서만 볼 수 있습니다.

방문 [JCR 저장소](jsrp.md) 추가 정보.

>[!NOTE]
>
>노드가 없음 `srpc` 아래에 `/etc/socialconfig` 기본값을 나타냅니다. [JCR 저장소](jsrp.md).
