---
title: 통합 [!DNL Assets] 활동 스트림 포함
description: 의 기록 기능에 대해 설명합니다. [!DNL Experience Manager] 특정 이벤트를 기록하도록 구성하는 방법.
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 통합 [!DNL Assets] 활동 스트림 포함 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] 사용자는 에셋 생성, 업로드 및 삭제와 같은 다양한 작업을 수행합니다. 이러한 작업을 기록하여 사용자가 수행한 작업의 내역을 제공할 수 있습니다. 이 섹션에서는 의 기록 기능에 대해 설명합니다. [!DNL Experience Manager] 및 구성 방법 [!DNL Experience Manager] 특정 이벤트를 기록합니다.

## 성능 고려 사항 및 기본 동작 {#performance-considerations-and-default-behavior}

예를 들어 일괄 가져오기를 수행할 때 이 통합은 CPU 및 디스크 공간을 소모할 수 있습니다. 이러한 이유로 [!DNL Assets] 활동 스트림과의 통합은 기본적으로 비활성화되어 있습니다.

## 지원되는 작업 이벤트 {#supported-action-events}

다음 이벤트를 기록하도록 구성할 수 있습니다.

* 라이선스 수락됨(수락됨)
* 자산이 생성됨(ASSET_CREATED)
* 자산이 이동됨(ASSET_MOVED)
* 자산 제거됨(ASSET_REMOVED)
* 라이선스 거부됨(거부됨)
* 에셋 다운로드됨(다운로드됨)
* 에셋의 버전이 지정됨(버전이 지정됨)
* 자산 버전 복원됨(복원됨)
* 자산 메타데이터 업데이트됨(METADATA_UPDATED)
* 외부 시스템에 게시된 자산(PUBLISHED_EXTERNAL)
* 에셋의 원래 업데이트(ORIGINAL_UPDATED)
* 자산 렌디션 업데이트됨(RENDITION_UPDATED)
* 자산 렌디션 제거됨(RENDITION_REMOVED)
* 하위 자산 업데이트됨(SUBASSET_UPDATED)
* 하위 자산 제거됨(SUBASSET_REMOVED)

## 구성 [!DNL Assets] 이벤트 기록 {#configuring-aem-assets-events-recording}

다음 [웹 콘솔](/help/sites-deploying/configuring-osgi.md) 는 Assets 이벤트 레코더 조정에 대한 액세스를 제공합니다. Assets 이벤트 레코더를 구성하려면 다음과 같이 진행합니다.

1. 다음 위치로 이동 **[!UICONTROL 웹 콘솔]**

1. 클릭 **[!UICONTROL 구성]**.

1. 두 번 클릭 **[!UICONTROL 일별 CQ DAM 이벤트 레코더]**.

1. 확인 **[!UICONTROL 이 서비스 사용]**.

1. 확인 **[!UICONTROL 이벤트 유형]** 사용자 활동 스트림에 기록할 것입니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 기록된 이벤트 읽기 {#reading-recorded-events}

기록된 이벤트는 활동으로 저장됩니다. 다음을 사용하여 프로그래밍 방식으로 읽을 수 있습니다. [ActivityManager API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
