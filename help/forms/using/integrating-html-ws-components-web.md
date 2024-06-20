---
title: 웹 애플리케이션에서 AEM Forms 작업 공간 구성 요소 통합
description: 자체 웹 앱에서 AEM Forms 작업 영역 구성 요소를 재사용하여 기능을 사용하고 긴밀한 통합을 제공하는 방법
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms, Adaptive Forms
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 웹 애플리케이션에서 AEM Forms 작업 공간 구성 요소 통합 {#integrating-aem-forms-workspace-components-in-web-applications}

AEM Forms 작업 영역을 사용할 수 있습니다 [구성 요소](/help/forms/using/description-reusable-components.md) 을 참조하십시오. 다음 샘플 구현에서는 CRX™ 인스턴스에 설치된 AEM Forms 작업 공간 개발 패키지의 구성 요소를 사용하여 웹 애플리케이션을 만듭니다. 특정 요구 사항에 맞게 아래 솔루션을 맞춤화하십시오. 샘플 구현이 재사용됨 `UserInfo`, `FilterList`, 및 `TaskList`웹 포털 내의 구성 요소

1. 다음 위치에서 CRXDE Lite 환경에 로그인합니다. `https://'[server]:[port]'/lc/crx/de/`. AEM Forms Workspace 개발 패키지가 설치되어 있는지 확인합니다.
1. 경로 만들기 `/apps/sampleApplication/wscomponents`.
1. css, 이미지, js/libs, js/runtime 및 js/registry.js 복사

   * 변환 전: `/libs/ws`
   * 끝 `/apps/sampleApplication/wscomponents`.

1. /apps/sampleApplication/wscomponents/js 폴더 내에 demomain.js 파일을 만듭니다. /libs/ws/js/main.js에서 demomain.js로 코드를 복사합니다.
1. demomain.js에서 라우터를 초기화하는 코드를 제거하고 다음 코드를 추가합니다.

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

1. 이름별로 /content 아래에 노드 만들기 `sampleApplication` 및 유형 `nt:unstructured`. 이 노드의 속성에서 다음을 추가합니다. `sling:resourceType` 문자열 및 값 유형의 `sampleApplication`. 이 노드의 액세스 제어 목록에 다음에 대한 항목을 추가합니다. `PERM_WORKSPACE_USER` jcr:read 권한을 허용합니다. 또한 의 액세스 제어 목록에서 `/apps/sampleApplication` 다음에 대한 항목 추가 `PERM_WORKSPACE_USER` jcr:read 권한을 허용합니다.
1. 위치 `/apps/sampleApplication/wscomponents/js/registry.js` 다음에서 경로 업데이트 `/lc/libs/ws/` 끝 `/lc/apps/sampleApplication/wscomponents/` 템플릿 값.
1. 포털 홈 페이지 의 JSP 파일에서 `/apps/sampleApplication/GET.jsp`를 클릭하고 다음 코드를 추가하여 포털 내에 필요한 구성 요소를 포함합니다.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   AEM Forms 작업 영역 구성 요소에 필요한 CSS 파일도 포함됩니다.

   >[!NOTE]
   >
   >렌더링하는 동안 각 구성 요소가 구성 요소 태그(클래스 구성 요소 포함)에 추가됩니다. 홈 페이지에 이러한 태그가 포함되어 있는지 확인합니다. 다음을 참조하십시오. `html.jsp` 이러한 기본 제어 태그에 대한 자세한 내용은 AEM Forms 작업 영역 의 파일을 참조하십시오.

1. 구성 요소를 사용자 정의하기 위해 필요한 구성 요소에 대한 기존 보기를 다음과 같이 확장할 수 있습니다.

   ```javascript
   define([
       'jquery',
       'underscore',
       'backbone',
       'runtime/views/userinfo'],
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

1. 포털 CSS를 수정하여 포털에 필요한 구성 요소의 레이아웃, 위치 및 스타일을 구성합니다. 예를 들어 userInfo 구성 요소를 제대로 보려면 이 포털에서 배경색을 검정색으로 유지해야 합니다. 에서 배경색을 변경하여 이 작업을 수행할 수 있습니다. `/apps/sampleApplication/wscomponents/css/style.css` 다음과 같이:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
