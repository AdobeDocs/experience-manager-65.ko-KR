---
title: 활동 스트림과 자산 통합
description: AEM의 레코딩 기능과 특정 이벤트를 기록하도록 AEM을 구성하는 방법에 대해 설명합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 활동 스트림과 자산 통합 {#integrating-assets-with-activity-stream}

AEM(Adobe Experience Manager) 자산 사용자는 자산 만들기, 업로드 및 삭제와 같은 다양한 작업을 수행합니다. 이러한 작업을 기록하여 사용자가 수행한 작업의 내역을 제공할 수 있습니다. 이 섹션에서는 AEM의 레코딩 기능과 특정 이벤트를 기록하기 위해 AEM을 구성하는 방법에 대해 설명합니다.

## 성능 고려 사항 및 기본 동작 {#performance-considerations-and-default-behavior}

이 통합은 벌크 가져오기를 수행할 때 예를 들어 CPU 및 디스크 공간을 소비할 수 있습니다. 이러한 이유로 AEM 자산과 활동 스트림은 기본적으로 비활성화되어 있습니다.

## 지원되는 작업 이벤트 {#supported-action-events}

다음 이벤트를 레코딩하도록 구성할 수 있습니다.

* 라이센스 수락(수락)
* 자산 생성됨(ASSET_CREATED)
* 자산이 이동됨(ASSET_MOVED)
* 자산 제거됨(ASSET_REMOVED)
* 라이선스 거부됨(거부됨)
* 자산 다운로드(다운로드됨)
* 에셋 버전 관리(VERSIONED)
* 자산 버전 복원(복원됨)
* 자산 메타데이터 업데이트됨(METADATA_UPDATED)
* 외부 시스템에 게시된 자산(PUBLISHED_EXTERNAL 파섹)
* 자산의 원래 업데이트(ORIGINAL_UPDATED)
* 자산 변환 업데이트됨(RENDITION_UPDATED)
* 자산 표현물이 제거됨(RENDITION_REMOVED)
* 하위 자산 업데이트됨(SUBASSET_UPDATED)
* 하위 자산이 제거됨(SUBASSET_REMOVED)

## AEM 자산 이벤트 기록 구성 {#configuring-aem-assets-events-recording}

웹 [콘솔에서는](/help/sites-deploying/configuring-osgi.md) AEM 자산 이벤트 레코더 조정에 액세스할 수 있습니다. AEM 자산 이벤트 레코더를 구성하려면 다음과 같이 하십시오.

1. 웹 **[!UICONTROL 콘솔로 이동]**

1. 구성을 **[!UICONTROL 클릭합니다]**.

1. Day **[!UICONTROL CQ DAM 이벤트 레코더를 두 번 클릭합니다]**.

1. 이 **[!UICONTROL 서비스를]**&#x200B;활성화합니다.

1. 사용자 **[!UICONTROL 활동]** 스트림에 기록하려는 이벤트 유형을 확인합니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 기록된 이벤트 읽기 {#reading-recorded-events}

기록된 이벤트는 활동으로 저장됩니다. ActivityManager API를 사용하여 프로그래밍 방식으로 읽을 [수 있습니다](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
