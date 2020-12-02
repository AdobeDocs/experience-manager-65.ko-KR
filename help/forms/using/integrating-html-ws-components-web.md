---
title: 웹 애플리케이션에서 AEM Forms 작업 영역 구성 요소 통합
seo-title: 웹 애플리케이션에서 AEM Forms 작업 영역 구성 요소 통합
description: 웹 앱에서 AEM Forms 작업 영역 구성 요소를 재사용하여 기능을 활용하고 긴밀한 통합을 제공하는 방법을 살펴봅니다.
seo-description: 웹 앱에서 AEM Forms 작업 영역 구성 요소를 재사용하여 기능을 활용하고 긴밀한 통합을 제공하는 방법을 살펴봅니다.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# 웹 응용 프로그램에서 AEM Forms 작업 영역 구성 요소 통합 {#integrating-aem-forms-workspace-components-in-web-applications}

자신의 웹 응용 프로그램에서 AEM Forms 작업 영역 [components](/help/forms/using/description-reusable-components.md)을 사용할 수 있습니다. 다음 샘플 구현에서는 CRX™ 인스턴스에 설치된 AEM Forms 작업 공간 개발 패키지의 구성 요소를 사용하여 웹 애플리케이션을 만듭니다. 특정 요구 사항에 맞게 아래 솔루션을 사용자 정의합니다. 샘플 구현에서는 웹 포털 내에 `UserInfo`, `FilterList` 및 `TaskList`구성 요소를 다시 사용합니다.

1. `https://'[server]:[port]'/lc/crx/de/`에 CRXDE Lite 환경에 로그인합니다. AEM Forms 작업 공간 개발 패키지가 설치되어 있는지 확인합니다.
1. 경로 `/apps/sampleApplication/wscomponents`을(를) 만듭니다.
1. css, images, js/libs, js/runtime 및 js/registry.js 복사

   * 변환 전: `/libs/ws`
   * 끝 `/apps/sampleApplication/wscomponents`.

1. /apps/sampleApplication/wscomponents/js 폴더 내에 demomain.js 파일을 만듭니다. /libs/ws/js/main.js의 코드를 demomain.js로 복사합니다.
1. demomain.js에서 라우터를 초기화할 코드를 제거하고 다음 코드를 추가합니다.

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. /content by name `sampleApplication` 아래에 노드를 만들고 `nt:unstructured`을 입력합니다. 이 노드의 속성에서 String 형식의 `sling:resourceType` 및 값 `sampleApplication`을 추가합니다. 이 노드의 액세스 제어 목록에서 jcr:read 권한을 허용하는 `PERM_WORKSPACE_USER`에 대한 항목을 추가합니다. 또한 `/apps/sampleApplication`의 액세스 제어 목록에서 jcr:read 권한을 허용하는 `PERM_WORKSPACE_USER`에 대한 항목을 추가합니다.
1. `/apps/sampleApplication/wscomponents/js/registry.js`에서 템플릿 값의 경로를 `/lc/libs/ws/`에서 `/lc/apps/sampleApplication/wscomponents/`로 업데이트합니다.
1. 포털 홈 페이지 JSP 파일(`/apps/sampleApplication/GET.jsp`)에서 다음 코드를 추가하여 포털 내에 필요한 구성 요소를 포함합니다.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   AEM Forms 작업 영역 구성 요소에 필요한 CSS 파일도 포함합니다.

   >[!NOTE]
   >
   >렌더링하는 동안 각 구성 요소는 구성 요소 태그(클래스 구성 요소 포함)에 추가됩니다. 홈 페이지에 이러한 태그가 포함되어 있는지 확인합니다. 이러한 기본 제어 태그에 대한 자세한 내용은 AEM Forms 작업 영역의 `html.jsp` 파일을 참조하십시오.

1. 구성 요소를 사용자 정의하려면 다음과 같이 필요한 구성 요소에 대한 기존 보기를 확장할 수 있습니다.

   ```javascript
   define([
       ‘jquery’,
       ‘underscore’,
       ‘backbone’,
       ‘runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. 포털 CSS를 수정하여 포털에서 필요한 구성 요소의 레이아웃, 배치 및 스타일을 구성합니다. 예를 들어 이 포털에서 userInfo 구성 요소를 잘 볼 수 있도록 배경색을 검은색으로 유지하고자 합니다. 다음과 같이 `/apps/sampleApplication/wscomponents/css/style.css`의 배경색을 변경하여 이 작업을 수행할 수 있습니다.

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
