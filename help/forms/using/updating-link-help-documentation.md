---
title: 설명서에 대한 링크 업데이트
seo-title: 설명서에 대한 링크 업데이트
description: AEM Forms 작업 공간에서 Workspace 도움말 링크의 대상을 업데이트하여 사용자 지정 설명서 링크를 가리키는 방법
seo-description: AEM Forms 작업 공간에서 Workspace 도움말 링크의 대상을 업데이트하여 사용자 지정 설명서 링크를 가리키는 방법
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# 설명서 {#updating-the-link-to-the-documentation}에 대한 링크 업데이트

**도움말 > 작업 공간 도움말**&#x200B;을 선택하여 AEM Forms 작업 공간의 기본 도움말 콘텐츠에 액세스할 수 있습니다. Adobe 웹 사이트의 온라인 설명서를 가리킵니다. 그러나 다른 URL을 가리키도록 업데이트할 수 있습니다.

기본 도움말 URL을 변경할 수 있는 다음 사용 사례를 고려하십시오.

* 원하는 언어로 현지화된 도움말 제공
* 사용자 지정된 작업 공간에 대한 사용자 지정 도움말 컨텐츠를 제공하는 경우.

온라인 설명서의 URL을 업데이트하려면 [사용자 지정](/help/forms/using/generic-steps-html-workspace-customization.md)의 일반 단계 를 선택하고 다음 단계를 따르십시오.

1. `/libs/ws/js/runtime/templates`에서 `/apps/ws/js/runtime/templates`로 `userinfo.html` 파일을 복사합니다.
1. 변경:

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   끝

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. 다음을 수행합니다.

   1. /apps/ws/js/registry.js 을 열어 편집합니다.
   1. `text!/lc/libs/ws/js/runtime/templates/userinfo.html` 을 `text!/lc/apps/ws/js/runtime/templates/userinfo.html` 로 검색하고 바꿉니다.
