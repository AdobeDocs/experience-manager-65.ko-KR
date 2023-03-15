---
title: 브랜딩에 대한 조직 로고 변경
seo-title: Changing the organization logo for branding
description: AEM Forms 작업 영역을 브랜딩하려면 기본 로고를 사용자 정의하여 조직의 로고를 제공합니다.
seo-description: To brand AEM Forms workspace provide the logo of your organization by customizing the default logo.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# 브랜딩에 대한 조직 로고 변경 {#changing-the-organization-logo-for-branding}

AEM Forms 작업 영역의 왼쪽 상단 모서리에 조직 로고가 표시됩니다. 로고를 업데이트하려면 [AEM Forms 작업 공간 사용자 지정의 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) 그런 다음 다음 다음 단계를 수행합니다.

1. 로고 만들기 및 파일 이름 지정 `NewWorkspace.png`. WebDAV 클라이언트를 사용하여 /apps/ws/images 폴더에 이미지 파일을 넣습니다.

   >[!NOTE]
   >
   >로고 이미지의 권장 크기는 218px × 20px입니다.

   >[!NOTE]
   >
   >WebDAV 액세스에 대한 자세한 내용은 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. 다음 스타일을 추가하여 스타일 시트(/apps/ws/css/newStyle.css)의 새 로고 이미지를 참조합니다.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
