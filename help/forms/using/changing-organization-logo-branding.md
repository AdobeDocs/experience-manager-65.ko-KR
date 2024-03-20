---
title: 브랜딩에 대한 조직 로고 변경
description: AEM Forms 작업 영역을 브랜딩하려면 기본 로고를 사용자 정의하여 조직의 로고를 제공합니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '119'
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
   >자세한 내용은 [WebDAV 액세스](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en).

   [WebDAV 액세스](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en)

1. 다음 스타일을 추가하여 스타일 시트(/apps/ws/css/newStyle.css)의 새 로고 이미지를 참조합니다.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
