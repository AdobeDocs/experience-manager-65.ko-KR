---
title: 타임라인의 활동 스트림
description: 이 문서에서는 타임라인에 있는 자산에 대한 활동 로그를 표시하는 방법에 대해 설명합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 12%

---


# 타임라인의 활동 스트림 {#activity-stream-in-timeline}

이 기능은 타임라인의 자산에 대한 활동 로그를 표시합니다. Adobe Experience Manager Assets에서 다음 자산 관련 작업을 수행하면 활동 스트림 기능이 타임라인을 업데이트하여 활동을 반영합니다.

다음 작업이 활동 스트림에 기록됩니다.

* 만들기
* 삭제
* 다운로드(변환 포함)
* 게시
* 게시 취소
* 승인
* 거부
* 이동

타임라인에 표시할 작업 로그는 로그 파일이 저장되는 CRX의 위치 `/var/audit/com.day.cq.dam/content/dam` 에서 가져옵니다.  또한, 타임라인 활동은 [Adobe Asset Link](https://helpx.adobe.com/kr/enterprise/using/manage-assets-using-adobe-asset-link.html) 또는 [Experience Manager 데스크탑 앱을 통해](https://docs.adobe.com/content/help/ko-KR/experience-manager-desktop-app/using/release-notes.html)새로운 자산을 업로드하거나 기존 에셋을 수정하고 Experience Manager에 체크 인하면 기록됩니다.

>[!NOTE]
>
>이러한 워크플로우에 대해 내역 정보가 저장되지 않으므로 임시 워크플로우는 타임라인에 표시되지 않습니다.

활동 스트림을 보려면 자산에 대해 하나 이상의 작업을 수행하고 자산을 선택한 다음 전역 탐색 목록에서 **[!UICONTROL 타임라인을]** 선택합니다.

![timeline-2](assets/timeline-2.png)

타임라인은 자산에 대해 수행하는 작업에 대한 활동 스트림을 표시합니다.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>게시 및 게시 취소 작업의 기본 **[!UICONTROL 로그]** 저장소 **[!UICONTROL 위치는]** 입니다 `/var/audit/com.day.cq.replication/content`. 이동 **[!UICONTROL 작업의 경우]** 기본 위치는 입니다 `/var/audit/com.day.cq.wcm.core.page`.
