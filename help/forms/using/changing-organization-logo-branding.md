---
title: 브랜딩을 위한 조직 로고 변경
description: AEM Forms 작업 영역을 브랜딩하려면 기본 로고를 사용자 정의하여 조직의 로고를 제공합니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 9%
---
# 브랜딩을 위한 조직 로고 변경 {#changing-the-organization-logo-for-branding}

AEM Forms 작업 영역의 왼쪽 상단 모서리에 조직 로고가 표시됩니다. 로고를 업데이트하려면 [AEM Forms 작업 영역 사용자 지정의 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)를 수행한 후 다음 단계를 수행합니다.

1. 로고를 만들고 파일 이름을 `NewWorkspace.png`(으)로 지정합니다. WebDAV 클라이언트를 사용하여 /apps/ws/images 폴더에 이미지 파일을 넣습니다.

   >[!NOTE]
   >
   >로고 이미지의 권장 크기는 218px × 20px입니다.

   >[!NOTE]
   >
   >자세한 내용은 [WebDAV 액세스](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=ko)를 참조하십시오.

   [WebDAV 액세스](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=ko)

1. 다음 스타일을 추가하여 스타일 시트(/apps/ws/css/newStyle.css)의 새 로고 이미지를 참조합니다.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
