---
title: 타임라인의 활동 스트림
description: 이 문서에서는 타임라인에서 자산에 대한 활동 로그를 표시하는 방법에 대해 설명합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 타임라인의 활동 스트림 {#activity-stream-in-timeline}

이 기능은 타임라인에 있는 자산에 대한 활동 로그를 표시합니다. AEM(Adobe Experience Manager) 자산에서 다음 자산 관련 작업을 수행하는 경우 활동 스트림 기능이 활동을 반영하도록 타임라인을 업데이트합니다.

다음 작업이 활동 스트림에 기록됩니다.

* 만들기
* 삭제
* 다운로드(변환 포함)
* 게시
* 게시 취소
* 승인
* 거부
* 이동

타임라인에 표시할 작업 로그는 로그 파일이 저장되는 CRX의 위치에서 가져옵니다. `/var/audit/com.day.cq.dam/content/dam` 이 위치에서 타임라인에 표시할 작업 로그를 가져옵니다.  또한, 타임라인 활동은 Adobe Asset Link 또는 AEM 데스크탑 앱을 [통해 새 자산이 업로드되거나 기존 자산이 수정되어](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) AEM에 [체크인될 때](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)기록됩니다.

>[!NOTE]
>
>이러한 워크플로우에 대해 내역 정보가 저장되지 않으므로 임시 워크플로우는 타임라인에 표시되지 않습니다.

활동 스트림을 보려면 자산에서 하나 이상의 작업을 수행하고 자산을 선택한 다음 전역 탐색 **[!UICONTROL 목록에서 타임라인을]** 선택합니다.

![타임라인-2](assets/timeline-2.png)

타임라인에는 자산에서 수행하는 작업에 대한 활동 스트림이 표시됩니다.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>게시 및 게시 취소 **[!UICONTROL 작업의 기본]** 로그 **[!UICONTROL 저장]** 위치는 `/var/audit/com.day.cq.replication/content`입니다. 이동 **[!UICONTROL 작업의]** 경우 기본 위치는 입니다 `/var/audit/com.day.cq.wcm.core.page`.
