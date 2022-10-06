---
title: 웹 애플리케이션에서 AEM Forms 작업 공간 구성 요소 통합
seo-title: Integrating AEM Forms workspace components in web applications
description: 고유한 웹 앱에서 AEM Forms 작업 공간 구성 요소를 다시 사용하여 기능을 활용하고 긴밀한 통합을 제공하는 방법입니다.
seo-description: How to reuse AEM Forms workspace components in your own webapps to leverage functionality and provide tight integration.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 웹 애플리케이션에서 AEM Forms 작업 공간 구성 요소 통합 {#integrating-aem-forms-workspace-components-in-web-applications}

AEM Forms 작업 공간을 사용할 수 있습니다 [구성 요소](/help/forms/using/description-reusable-components.md) 사용 중인 웹 응용 프로그램에서 사용할 수 있습니다. 다음 샘플 구현에서는 CRX™ 인스턴스에 설치된 AEM Forms 작업 공간 개발 패키지의 구성 요소를 사용하여 웹 애플리케이션을 만듭니다. 특정 요구 사항에 맞게 아래 솔루션을 사용자 정의합니다. 샘플 구현은 를 다시 사용합니다 `UserInfo`, `FilterList`, 및 `TaskList`구성 요소를 생성하지 않습니다.

1. 의 CRXDE Lite 환경에 로그인합니다. `https://'[server]:[port]'/lc/crx/de/`. AEM Forms 작업 공간 개발 패키지가 설치되어 있는지 확인합니다.
1. 경로 만들기 `/apps/sampleApplication/wscomponents`.
1. css, 이미지, js/libs, js/runtime 및 js/registry.js 을 복사합니다.

   * 변환 전: `/libs/ws`
   * 끝 `/apps/sampleApplication/wscomponents`.

1. /apps/sampleApplication/wscomponents/js 폴더 내에 demomain.js 파일을 만듭니다. /libs/ws/js/main.js에서 demomain.js로 코드를 복사합니다.
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

1. 이름별로 /content 아래에 노드를 만듭니다. `sampleApplication` 및 유형 `nt:unstructured`. 이 노드의 속성에서 `sling:resourceType` 유형 및 값 `sampleApplication`. 이 노드의 액세스 제어 목록에서 `PERM_WORKSPACE_USER` jcr:read 권한 허용 또한 `/apps/sampleApplication` 에 대한 항목 추가 `PERM_WORKSPACE_USER` jcr:read 권한 허용
1. in `/apps/sampleApplication/wscomponents/js/registry.js` 에서 경로 업데이트 `/lc/libs/ws/` to `/lc/apps/sampleApplication/wscomponents/` 참조하십시오.
1. 포털 홈 페이지의 JSP 파일에서 `/apps/sampleApplication/GET.jsp`를 눌러 포털 내에 필요한 구성 요소를 포함하려면 다음 코드를 추가합니다.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   AEM Forms 작업 공간 구성 요소에 필요한 CSS 파일도 포함합니다.

   >[!NOTE]
   >
   >렌더링하는 동안 각 구성 요소가 구성 요소 태그(클래스 구성 요소 있음)에 추가됩니다. 홈 페이지에 이러한 태그가 포함되어 있는지 확인합니다. 자세한 내용은 `html.jsp` AEM Forms 작업 공간 파일로 이러한 기본 제어 태그에 대해 자세히 알아보십시오.

1. 구성 요소를 사용자 지정하려면 다음과 같이 필요한 구성 요소에 대한 기존 보기를 확장할 수 있습니다.

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

1. 포털 CSS를 수정하여 포털에서 필요한 구성 요소의 레이아웃, 위치 지정 및 스타일을 구성합니다. 예를 들어 이 포털에서 userInfo 구성 요소를 잘 볼 수 있도록 배경색을 검정색으로 유지하려는 경우가 있습니다. 이렇게 하려면 배경색을 `/apps/sampleApplication/wscomponents/css/style.css` 아래와 같이 변경하는 것을 의미합니다.

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
