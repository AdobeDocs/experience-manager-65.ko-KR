---
title: 타임라인 보기에서 디지털 자산의 활동 스트림
description: 이 문서에서는 타임라인에 있는 자산에 대한 활동 로그를 표시하는 방법에 대해 설명합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 7%

---


# 타임라인의 활동 스트림 {#activity-stream-in-timeline}

이 기능은 타임라인의 자산에 대한 활동 로그를 표시합니다. 다음 자산 관련 작업을 에서 수행하는 경우 활동 스트림 기능 [!DNL Adobe Experience Manager Assets]은 활동을 반영하도록 타임라인을 업데이트합니다.

다음 작업이 활동 스트림에 기록됩니다.

* 만들기
* 삭제
* 다운로드(변환 포함)
* 게시
* 게시 취소
* 승인
* 거부
* 이동

타임라인에 표시할 작업 로그는 로그 파일이 저장되는 CRX의 위치 `/var/audit/com.day.cq.dam/content/dam` 에서 가져옵니다. 또한, 타임라인 활동은 Adobe 에셋 링크 [!DNL Experience Manager] 또는 [Experience Manager 데스크탑 앱을](https://helpx.adobe.com/kr/enterprise/using/manage-assets-using-adobe-asset-link.html) 통해 새로운 에셋이 업로드되거나 기존 에셋이 수정 및 체크 인될 때 기록됩니다 [](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>이러한 워크플로에 대해 내역 정보가 저장되지 않으므로 임시 워크플로우는 타임라인에 표시되지 않습니다.

활동 스트림을 보려면 자산에 대해 하나 이상의 작업을 수행하고 자산을 선택한 다음 전역 탐색 목록에서 **[!UICONTROL 타임라인을]** 선택합니다.

![timeline-2](assets/timeline-2.png)

타임라인은 자산에 대해 수행하는 작업에 대한 활동 스트림을 표시합니다.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>게시 및 게시 취소 작업의 기본 **[!UICONTROL 로그]** 저장소 **[!UICONTROL 위치는]** 입니다 `/var/audit/com.day.cq.replication/content`. 이동 **[!UICONTROL 작업의 경우]** 기본 위치는 입니다 `/var/audit/com.day.cq.wcm.core.page`.
