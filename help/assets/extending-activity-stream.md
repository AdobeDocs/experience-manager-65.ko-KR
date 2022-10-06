---
title: 통합 [!DNL Assets] 활동 스트림 사용
description: 의 기록 기능에 대해 설명합니다. [!DNL Experience Manager] 및 특정 이벤트를 기록하도록 구성하는 방법입니다.
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 통합 [!DNL Assets] 활동 스트림 사용 {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] 사용자는 자산 만들기, 업로드 및 삭제와 같은 많은 작업을 수행합니다. 이러한 작업을 기록할 수 있으므로 사용자가 수행한 작업 내역을 제공할 수 있습니다. 이 섹션에서는 [!DNL Experience Manager] 및 구성 방법 [!DNL Experience Manager] 를 입력하여 특정 이벤트를 기록할 수 있습니다.

## 성능 고려 사항 및 기본 동작 {#performance-considerations-and-default-behavior}

대량 가져오기를 수행하는 경우와 같이 이 통합은 CPU 및 디스크 공간을 많이 사용하는 것일 수 있습니다. 이러한 이유로 [!DNL Assets] 활동 스트림과의 통합이 기본적으로 비활성화되어 있습니다.

## 지원되는 작업 이벤트 {#supported-action-events}

다음 이벤트를 기록하도록 구성할 수 있습니다.

* 라이센스 수락(수락됨)
* 생성된 자산(ASSET_CREATED)
* 이동된 자산(ASSET_MOVED)
* 자산이 제거됨(ASSET_REMOVED)
* 라이센스가 거부됨(거부됨)
* 자산 다운로드(다운로드됨)
* 자산 버전이 지정됨(버전이 지정됨)
* 자산 버전이 복원됨(복원됨)
* 자산 메타데이터가 업데이트됨(METADATA_UPDATED)
* 외부 시스템에 게시된 자산(PUBLISHED_EXTERNAL)
* 자산의 원래 업데이트(ORIGINAL_UPDATED)
* 자산 표현물 업데이트(RENDITION_UPDATED)
* 자산 표현물이 제거됨(RENDITION_REMOVED)
* 하위 자산이 업데이트됨(SUBASSET_UPDATED)
* 하위 자산이 제거됨(SUBASSET_REMOVED)

## 구성 [!DNL Assets] 이벤트 기록 {#configuring-aem-assets-events-recording}

다음 [웹 콘솔](/help/sites-deploying/configuring-osgi.md) 자산 이벤트 레코더 조정에 대한 액세스 권한을 제공합니다. Assets 이벤트 기록기를 구성하려면 다음과 같이 진행합니다.

1. 로 이동합니다 **[!UICONTROL 웹 콘솔]**

1. 클릭 **[!UICONTROL 구성]**.

1. 두 번 클릭 **[!UICONTROL 일 CQ DAM 이벤트 레코더]**.

1. 확인 **[!UICONTROL 이 서비스를 사용하도록 설정]**.

1. 확인 **[!UICONTROL 이벤트 유형]** 사용자 활동 스트림에 기록하려는 경우.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 기록된 이벤트 읽기 {#reading-recorded-events}

기록된 이벤트는 활동으로 저장됩니다. 를 사용하여 프로그래밍 방식으로 읽을 수 있습니다 [ActivityManager API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
