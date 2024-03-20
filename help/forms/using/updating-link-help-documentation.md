---
title: 설명서 링크 업데이트
description: 사용자 지정 설명서 링크를 가리키도록 AEM Forms 작업 공간에서 작업 공간 도움말 링크의 대상을 업데이트하는 방법.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---

# 설명서 링크 업데이트 {#updating-the-link-to-the-documentation}

을 선택하여 AEM Forms 작업 영역에 대한 기본 도움말 콘텐츠에 액세스할 수 있습니다. **도움말 > 작업 공간 도움말**. Adobe 웹 사이트의 온라인 설명서를 가리킵니다. 그러나 다른 URL을 가리키도록 업데이트할 수 있습니다.

기본 도움말 URL을 변경하려는 경우 다음 사용 사례를 고려하십시오.

* 원하는 언어로 현지화된 도움말을 제공합니다.
* 맞춤화된 작업 영역에 맞춤화된 도움말 콘텐츠를 제공하기 위한 것입니다.

온라인 설명서의 URL을 업데이트하려면 다음을 따르십시오. [사용자 지정의 일반 단계](/help/forms/using/generic-steps-html-workspace-customization.md) 그런 다음 다음 다음 단계를 수행합니다.

1. 다음을 복사합니다. `userinfo.html` 파일 출처: `/libs/ws/js/runtime/templates` 끝 `/apps/ws/js/runtime/templates`.
1. 변경:

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   대상

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. 다음 작업을 수행합니다.

   1. 편집하려면 /apps/ws/js/registry.js을 여십시오.
   1. 검색 및 바꾸기 `text!/lc/libs/ws/js/runtime/templates/userinfo.html` 포함 `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
