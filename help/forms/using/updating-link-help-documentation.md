---
title: 설명서에 대한 링크 업데이트
seo-title: 설명서에 대한 링크 업데이트
description: AEM Forms 작업 영역에서 작업 영역 도움말 링크 대상을 업데이트하여 사용자 정의 문서 링크를 가리키는 방법.
seo-description: AEM Forms 작업 영역에서 작업 영역 도움말 링크 대상을 업데이트하여 사용자 정의 문서 링크를 가리키는 방법.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---


# 문서 {#updating-the-link-to-the-documentation} 링크를 업데이트하는 중

**도움말 > 작업 공간 도움말**&#x200B;을 선택하여 AEM Forms 작업 영역의 기본 도움말 내용에 액세스할 수 있습니다. Adobe 웹 사이트에 있는 온라인 설명서를 가리킵니다. 그러나 다른 URL을 가리키도록 업데이트할 수 있습니다.

기본 도움말 URL을 변경할 수 있는 다음 사용 사례를 고려하십시오.

* 원하는 언어로 현지화된 지원을 제공할 수 있습니다.
* 사용자 정의된 작업 영역에 대한 사용자 지정 도움말 컨텐츠를 제공하는 경우

온라인 설명서의 URL을 업데이트하려면 [사용자 정의 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md)를 수행한 후 다음 단계를 수행합니다.

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

   1. /apps/ws/js/registry.js편집을 위해 엽니다.
   1. `text!/lc/libs/ws/js/runtime/templates/userinfo.html`을(를) 검색하여 `text!/lc/apps/ws/js/runtime/templates/userinfo.html`로 바꿉니다.
