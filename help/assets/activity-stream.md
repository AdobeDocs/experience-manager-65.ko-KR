---
title: 타임라인 보기의 디지털 에셋에 대한 활동 스트림
description: 이 문서에서는 타임라인에 자산에 대한 활동 로그를 표시하는 방법에 대해 설명합니다.
contentOwner: AG
feature: Asset Management
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 12%

---

# 타임라인의 활동 스트림 {#activity-stream-in-timeline}

이 기능은 타임라인에 에셋에 대한 활동 로그를 표시합니다. 에서 다음 에셋 관련 작업을 수행하는 경우 [!DNL Adobe Experience Manager Assets], 활동 스트림 기능은 활동을 반영하도록 타임라인을 업데이트합니다.

다음 작업이 활동 스트림에 기록됩니다.

* 만들기
* 삭제
* 다운로드(렌디션 포함)
* 게시
* 게시 취소
* 승인
* 거부
* 이동

타임라인에 표시될 활동 로그를 위치에서 가져옵니다 `/var/audit/com.day.cq.dam/content/dam` 로그 파일이 저장되는 CRX에서 또한 타임라인 활동은 새 에셋이 업로드되거나 기존 에셋을 수정하고 체크 인하면 기록됩니다 [!DNL Experience Manager] 경유 [Adobe 에셋 링크](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) 또는 [Experience Manager 데스크탑 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>내역 정보가 저장되지 않아 임시 워크플로우는 타임라인에 표시되지 않습니다.

활동 스트림을 보려면 에셋에서 하나 이상의 작업을 수행하고 에셋을 선택한 다음 를 선택합니다 **[!UICONTROL 타임라인]** GlobalNav 목록에서

![timeline-2](assets/timeline-2.png)

타임라인에는 에셋에서 수행하는 작업에 대한 활동 스트림이 표시됩니다.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>The default log storage location for **[!UICONTROL Publish]** and **[!UICONTROL Unpublish]** tasks is `/var/audit/com.day.cq.replication/content`. For **[!UICONTROL Move]** tasks, the default location is `/var/audit/com.day.cq.wcm.core.page`.
