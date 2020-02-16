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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 저장소 구성 {#storage-configuration}

스토리지 구성은 UGC(사용자 생성 컨텐츠)라고도 하는 커뮤니티 컨텐츠에 대해 선택한 스토리지를 식별하는 방법입니다.

이 설정은 AEM Communities 코드에 UGC에 액세스할 때 사용할 SRP(저장소 리소스 공급자)의 구현에 대해 알리고 AEM이 배포될 때 설정된 토폴로지를 반영해야 합니다.

스토리지 옵션 및 배포 토폴로지에 대한 자세한 내용은

* [커뮤니티 콘텐츠 스토어](working-with-srp.md)
* [권장 토폴로지](topologies.md)

## 스토리지 구성 콘솔 {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

작성 환경에서 스토리지 구성 콘솔에 액세스하려면

* 전역 탐색에서:도구 **[!UICONTROL > 커뮤니티 > 스토리지 구성]**

기본 JCR 이외의 저장 옵션을 선택하려면 다음을 수행합니다.

* 옵션 선택
* 적절하게 구성

   * MSRP [선택 세부 사항 보기](msrp.md#select-msrp)
   * DSRP [선택 세부 사항 보기](dsrp.md#select-dsrp)
   * ASRP [선택 세부 사항 보기](asrp.md#select-asrp)

* **[!UICONTROL 제출]**&#x200B;을 선택합니다

### JCR 스토리지 정보 {#about-jcr-storage}

선택하지 않은 경우 기본값은 AEM 리포지토리 JCR입니다.

JCR은 작성 및 게시 환경에서 공유되는 공용 저장소가 *아닙니다* . 커뮤니티 컨텐츠는 작성된 작성자 또는 게시 환경에서만 표시됩니다.

자세한 [내용은 JCR](jsrp.md) 스토어를 참조하십시오.

>[!NOTE]
>
>아래 노드가 `srpc`없으면 기본 JCR 저장소가 `/etc/socialconfig` [](jsrp.md)표시됩니다.

