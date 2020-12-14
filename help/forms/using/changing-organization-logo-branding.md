---
title: 브랜딩을 위한 조직 로고 변경
seo-title: 브랜딩을 위한 조직 로고 변경
description: AEM Forms 작업 공간을 브랜딩하려면 기본 로고를 사용자 정의하여 조직의 로고를 제공합니다.
seo-description: AEM Forms 작업 공간을 브랜딩하려면 기본 로고를 사용자 정의하여 조직의 로고를 제공합니다.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 브랜딩 {#changing-the-organization-logo-for-branding} 조직의 로고 변경

조직 로고는 AEM Forms 작업 영역의 왼쪽 위 모서리에 표시됩니다. 로고를 업데이트하려면 AEM Forms 작업 영역 사용자 정의](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)의 [일반 단계를 수행한 다음 다음 단계를 수행합니다.

1. 로고를 만들고 파일의 이름을 `NewWorkspace.png`으로 지정합니다. WebDAV 클라이언트를 사용하여 /apps/ws/images 폴더에 이미지 파일을 배치합니다.

   >[!NOTE]
   >
   >로고 이미지의 권장 크기는 218px × 20px입니다.

   >[!NOTE]
   >
   >WebDAV 액세스에 대한 자세한 내용은 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)을 참조하십시오.

1. 다음 스타일을 추가하여 스타일 시트(/apps/ws/css/newStyle.css)에서 새 로고 이미지를 참조하십시오.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
