---
title: 웹 애플리케이션에서 AEM Forms 작업 영역 구성 요소 통합
seo-title: 웹 애플리케이션에서 AEM Forms 작업 영역 구성 요소 통합
description: 고유한 웹 앱에서 AEM Forms 작업 영역 구성 요소를 재사용하여 기능을 활용하고 긴밀한 통합을 제공하는 방법을 살펴봅니다.
seo-description: 고유한 웹 앱에서 AEM Forms 작업 영역 구성 요소를 재사용하여 기능을 활용하고 긴밀한 통합을 제공하는 방법을 살펴봅니다.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 웹 애플리케이션에서 AEM Forms 작업 영역 구성 요소 통합 {#integrating-aem-forms-workspace-components-in-web-applications}

자체 웹 애플리케이션에서 AEM Forms 작업 영역 [구성 요소를](/help/forms/using/description-reusable-components.md) 사용할 수 있습니다. 다음 샘플 구현은 CRX™ 인스턴스에 설치된 AEM Forms 작업 영역 개발 패키지의 구성 요소를 사용하여 웹 애플리케이션을 만듭니다. 특정 요구 사항에 맞게 아래 솔루션을 사용자 정의합니다. 샘플 구현은 웹 포털 내에서 `UserInfo`구성 요소 `FilterList`및 `TaskList`구성 요소를 재사용합니다.

1. 에서 CRXDE Lite 환경에 로그인합니다 `https://'[server]:[port]'/lc/crx/de/`. AEM Forms 작업 공간 개발 패키지가 설치되어 있는지 확인합니다.
1. 패스를 `/apps/sampleApplication/wscomponents`만듭니다.
1. css, images, js/libs, js/runtime 및 js/registry.js 복사

   * 시작 시간:`/libs/ws`
   * 끝 `/apps/sampleApplication/wscomponents`.

1. /apps/sampleApplication/wscomponents/js 폴더 내에 demomain.js 파일을 만듭니다. /libs/ws/js/main.js의 코드를 demomain.js로 복사합니다.
1. demomain.js에서 라우터를 초기화할 코드를 제거하고 다음 코드를 추가합니다.

   ```
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. 이름과 유형별로 /content 아래에 노드를 `sampleApplication` 만듭니다 `nt:unstructured`. 이 노드의 속성에서 String 및 `sling:resourceType` value 유형을 추가합니다 `sampleApplication`. 이 노드의 액세스 제어 목록에서 jcr:읽기 권한을 `PERM_WORKSPACE_USER` 허용하는 항목을 추가합니다. 또한 액세스 제어 목록에 jcr:read 권한을 `/apps/sampleApplication` 허용하는 항목을 `PERM_WORKSPACE_USER` 추가합니다.
1. 템플릿 값에 대한 경로를 `/apps/sampleApplication/wscomponents/js/registry.js` 에서 `/lc/libs/ws/` `/lc/apps/sampleApplication/wscomponents/` 로 업데이트합니다.
1. 의 포털 홈 페이지 JSP 파일에서 다음 코드를 `/apps/sampleApplication/GET.jsp`추가하여 포털 내에 필요한 구성 요소를 포함합니다.

   ```as3
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   AEM Forms 작업 영역 구성 요소에 필요한 CSS 파일도 포함합니다.

   >[!NOTE]
   >
   >각 구성 요소는 렌더링하는 동안 구성 요소 태그(클래스 구성 요소 포함)에 추가됩니다. 홈 페이지에 이러한 태그가 포함되어 있는지 확인합니다. 이러한 기본 제어 태그에 대한 자세한 내용은 AEM Forms 작업 영역의 `html.jsp` 파일을 참조하십시오.

1. 구성 요소를 사용자 정의하려면 다음과 같이 필요한 구성 요소에 대한 기존 보기를 확장할 수 있습니다.

   ```as3
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

1. 포털 CSS를 수정하여 포털에서 필요한 구성 요소의 레이아웃, 배치 및 스타일을 구성합니다. 예를 들어 이 포털에서 userInfo 구성 요소를 잘 볼 수 있도록 배경색을 검은색으로 유지하고자 합니다. 이렇게 하려면 `/apps/sampleApplication/wscomponents/css/style.css` 다음과 같이 배경색을 변경하면 됩니다.

   ```as3
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
