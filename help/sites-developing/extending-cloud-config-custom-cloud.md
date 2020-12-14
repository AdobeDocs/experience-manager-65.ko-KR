---
title: 사용자 지정 클라우드 서비스 만들기
seo-title: 사용자 지정 클라우드 서비스 만들기
description: 기본 Cloud Services 세트는 사용자 정의 Cloud Service 유형으로 확장할 수 있습니다.
seo-description: 기본 Cloud Services 세트는 사용자 정의 Cloud Service 유형으로 확장할 수 있습니다.
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 15%

---


# 사용자 지정 클라우드 서비스 만들기{#creating-a-custom-cloud-service}

기본 Cloud Services 세트는 사용자 정의 Cloud Service 유형으로 확장할 수 있습니다. 이렇게 하면 사용자 지정 마크업을 구조화된 방식으로 페이지에 삽입할 수 있습니다. 이는 주로 Google Analytics, Chartbeat 등과 같은 제3자 분석 제공자에게 사용됩니다. Cloud Services은 상위 페이지에서 하위 페이지로 상속되며 모든 수준에서 상속을 나눌 수 있습니다.

>[!NOTE]
>
>새 Cloud Service을 만들기 위한 이 단계별 안내서는 Google Analytics을 사용하는 예입니다. 모든 것이 사용 사례에 적용되지 않을 수 있습니다.

1. CRXDE Lite에서 `/apps` 아래에 새 노드를 만듭니다.

   * **이름**: `acs`
   * **유형**: `nt:folder`

1. `/apps/acs` 아래에 새 노드를 만듭니다.

   * **이름**: `analytics`
   * **유형**: `sling:Folder`

1. `/apps/acs/analytics` 아래에 2개의 새 노드를 만듭니다.

   * **이름**:components
   * **유형**: `sling:Folder`

   및

   * **이름**:템플릿
   * **유형**: `sling:Folder`


1. `/apps/acs/analytics/components`을(를) 마우스 오른쪽 단추로 클릭합니다. **만들기...를 선택합니다.** 뒤에 **구성 요소 만들기...** 대화 상자가 열리면 다음을 지정할 수 있습니다.

   * **레이블**: `googleanalyticspage`
   * **제목**: `Google Analytics Page`
   * **Super Type**: `cq/cloudserviceconfigs/components/configpage`
   * **그룹**: `.hidden`

1. **다음**&#x200B;을 두 번 클릭하고 다음을 지정합니다.

   * **허용된 상위:** `acs/analytics/templates/googleanalytics`

   **다음**&#x200B;을 두 번 클릭하고 **확인**&#x200B;을 클릭합니다.

1. `googleanalyticspage`에 속성 추가:

   * **이름:** `cq:defaultView`
   * **값:** `html`

1. 다음 콘텐트를 사용하여 `/apps/acs/analytics/components/googleanalyticspage` 아래에 `content.jsp`이라는 새 파일을 만듭니다.

   ```xml
   <%@page contentType="text/html"
               pageEncoding="utf-8"%><%
   %><%@include file="/libs/foundation/global.jsp"%><div>
   
   <div>
       <h3>Google Analytics Settings</h3>
       <ul>
           <li><div class="li-bullet"><strong>accountID: </strong><br><%= xssAPI.encodeForHTML(properties.get("accountID", "")) %></div></li>
       </ul>
   </div>
   ```

1. `/apps/acs/analytics/components/googleanalyticspage/` 아래에 새 노드를 만듭니다.

   * **이름**: `dialog`
   * **유형**: `cq:Dialog`
   * **속성**:

      * **이름**: `title`
      * **유형**: `String`
      * **값**:  `Google Analytics Config`
      * **이름**: `xtype`
      * **유형**: `String`
      * **값**:  `dialog`

1. `/apps/acs/analytics/components/googleanalyticspage/dialog` 아래에 새 노드를 만듭니다.

   * **이름**: `items`
   * **유형**: `cq:Widget`
   * **속성**:

      * **이름**: `xtype`
      * **유형**: `String`
      * **값**:  `tabpanel`

1. `/apps/acs/analytics/components/googleanalyticspage/dialog/items` 아래에 새 노드를 만듭니다.

   * **이름**: `items`
   * **유형**: `cq:WidgetCollection`

1. `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items` 아래에 새 노드를 만듭니다.

   * **이름**:tab1
   * **유형**: `cq:Panel`
   * **속성**:

      * **이름**: `title`
      * **유형**: `String`
      * **값**:  `Config`

1. `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1` 아래에 새 노드를 만듭니다.

   * **이름**:항목
   * **유형**: `nt:unstructured`
   * **속성**:

      * **이름**: `fieldLabel`
      * **유형**:문자열
      * **값**:계정 ID

      * **이름**: `fieldDescription`
      * **유형**: `String`
      * **값**:  `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **이름**: `name`
      * **유형**: `String`
      * **값**:  `./accountID`
      * **이름**: `validateOnBlur`
      * **유형**: `String`
      * **값**:  `true`
      * **이름**: `xtype`
      * **유형**: `String`
      * **값**:  `textfield`

1. `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp`을 `/apps/acs/analytics/components/googleanalyticspage/body.jsp`에 복사하고 34행에서 `libs`를 `apps`으로 변경하고 79행에서 스크립트 참조를 전체 경로 지정으로 만듭니다.
1. `/apps/acs/analytics/templates/` 아래에 새 템플릿을 만듭니다.

   * **리소스 유형** = `acs/analytics/components/googleanalyticspage` 포함
   * **Label** = `googleanalytics` 포함
   * **제목**= `Google Analytics Configuration` 포함
   * with **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * with **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * with **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage`(템플릿 노드에서 jcr:content 노드가 아님)
   * with **cq:designPath** = `/etc/designs/cloudservices/googleanalytics`(jcr:content)

1. 새 구성 요소 만들기:`/apps/acs/analytics/components/googleanalytics`.

   다음 콘텐트를 `googleanalytics.jsp`에 추가합니다.

   ```xml
   <%@page import="org.apache.sling.api.resource.Resource,
                   org.apache.sling.api.resource.ValueMap,
                   org.apache.sling.api.resource.ResourceUtil,
                   com.day.cq.wcm.webservicesupport.Configuration,
                   com.day.cq.wcm.webservicesupport.ConfigurationManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   
   String[] services = pageProperties.getInherited("cq:cloudserviceconfigs", new String[]{});
   ConfigurationManager cfgMgr = resource.getResourceResolver().adaptTo(ConfigurationManager.class);
   if(cfgMgr != null) {
       String accountID = null;
       Configuration cfg = cfgMgr.getConfiguration("googleanalytics", services);
       if(cfg != null) {
           accountID = cfg.get("accountID", null);
       }
   
       if(accountID != null) {
       %>
   <script type="text/javascript">
   
     var _gaq = _gaq || [];
     _gaq.push(['_setAccount', '<%= accountID %>']);
     _gaq.push(['_trackPageview']);
   
     (function() {
       var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
       ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
     })();
   
   </script><%
       }
   }
   %>
   ```

   구성 속성을 기반으로 사용자 지정 마크업을 출력해야 합니다.

1. `http://localhost:4502/miscadmin#/etc/cloudservices`으로 이동하여 새 페이지를 만듭니다.

   * **제목**: `Google Analytics`
   * **이름**: `googleanalytics`

   CRXDE Lite으로 돌아가서 `/etc/cloudservices/googleanalytics` 아래에서 다음 속성을 `jcr:content`에 추가합니다.

   * **이름**: `componentReference`
   * **유형**: `String`
   * **값**:  `acs/analytics/components/googleanalytics`


1. 새로 만든 서비스 페이지( `http://localhost:4502/etc/cloudservices/googleanalytics.html`)로 이동하고 **+**&#x200B;를 클릭하여 새 구성을 만듭니다.

   * **상위 구성**: `/etc/cloudservices/googleanalytics`
   * **제목:**  `My First GA Config`

   **Google Analytics 구성**&#x200B;을 선택하고 **만들기**&#x200B;를 클릭합니다.

1. **계정 ID**&#x200B;를 입력합니다(예: `AA-11111111-1`). **확인**&#x200B;을 클릭합니다.
1. 페이지로 이동하여 페이지 속성에서 새로 만든 구성을 **Cloud Services** 탭 아래에 추가합니다.
1. 페이지에 사용자 지정 마크업이 추가됩니다.

