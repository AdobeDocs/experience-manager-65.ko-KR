---
title: 사용자 지정 Cloud Service 만들기
description: 사용자 지정 Cloud Service 유형을 사용하여 기본 Cloud Services 세트를 확장할 수 있습니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 11%

---

# 사용자 지정 Cloud Service 만들기{#creating-a-custom-cloud-service}

사용자 지정 Cloud Service 유형을 사용하여 기본 Cloud Services 세트를 확장할 수 있습니다. 이렇게 하면 사용자 지정 마크업을 구조화된 방식으로 페이지에 삽입할 수 있습니다. 이는 주로 Google Analytics, Chartbeat 등과 같은 서드파티 분석 공급자에게 사용됩니다. Cloud Service은 상위 페이지에서 하위 페이지로 상속되며, 어떤 수준에서든 상속을 중단할 수 있습니다.

>[!NOTE]
>
>Cloud Service 만들기에 대한 이 단계별 안내서는 Google Analytics을 사용하는 예제입니다. 모든 항목이 사용 사례에 적용되지 않을 수 있습니다.

1. CRXDE Lite에서 `/apps` 아래에 노드를 만드십시오.

   * **이름**: `acs`
   * **유형**: `nt:folder`

1. `/apps/acs` 아래에 노드 만들기:

   * **이름**: `analytics`
   * **유형**: `sling:Folder`

1. `/apps/acs/analytics` 아래에 두 개의 노드를 만듭니다.

   * **이름**: 구성 요소
   * **유형**: `sling:Folder`

   및

   * **이름**: 템플릿
   * **유형**: `sling:Folder`

1. `/apps/acs/analytics/components`을(를) 마우스 오른쪽 단추로 클릭합니다. **만들기..**, **구성 요소 만들기...**&#x200B;를 차례로 선택합니다. 열리는 대화 상자에서는 다음을 지정할 수 있습니다.

   * **레이블**: `googleanalyticspage`
   * **제목**: `Google Analytics Page`
   * **수퍼 유형**: `cq/cloudserviceconfigs/components/configpage`
   * **그룹**: `.hidden`

1. **다음**&#x200B;을(를) 두 번 클릭하고 다음을 지정하십시오.

   * **허용된 부모:** `acs/analytics/templates/googleanalytics`

   **다음**&#x200B;을 두 번 클릭하고 **확인**&#x200B;을 클릭합니다.

1. `googleanalyticspage`에 속성 추가:

   * **이름:** `cq:defaultView`
   * **값:** `html`

1. 다음 내용이 포함된 `content.jsp` 파일을 `/apps/acs/analytics/components/googleanalyticspage` 아래에 만듭니다.

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

1. `/apps/acs/analytics/components/googleanalyticspage/` 아래에 노드 만들기:

   * **이름**: `dialog`
   * **유형**: `cq:Dialog`
   * **속성**:

      * **이름**: `title`
      * **유형**: `String`
      * **값**: `Google Analytics Config`
      * **이름**: `xtype`
      * **유형**: `String`
      * **값**: `dialog`

1. `/apps/acs/analytics/components/googleanalyticspage/dialog` 아래에 노드 만들기:

   * **이름**: `items`
   * **유형**: `cq:Widget`
   * **속성**:

      * **이름**: `xtype`
      * **유형**: `String`
      * **값**: `tabpanel`

1. `/apps/acs/analytics/components/googleanalyticspage/dialog/items` 아래에 노드 만들기:

   * **이름**: `items`
   * **유형**: `cq:WidgetCollection`

1. `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items` 아래에 노드 만들기:

   * **이름**: tab1
   * **유형**: `cq:Panel`
   * **속성**:

      * **이름**: `title`
      * **유형**: `String`
      * **값**: `Config`

1. `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1` 아래에 노드 만들기:

   * **이름**: 항목
   * **유형**: `nt:unstructured`
   * **속성**:

      * **이름**: `fieldLabel`
      * **유형**: 문자열
      * **값**: 계정 ID

      * **이름**: `fieldDescription`
      * **유형**: `String`
      * **값**: `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **이름**: `name`
      * **유형**: `String`
      * **값**: `./accountID`
      * **이름**: `validateOnBlur`
      * **유형**: `String`
      * **값**: `true`
      * **이름**: `xtype`
      * **유형**: `String`
      * **값**: `textfield`

1. `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp`을(를) `/apps/acs/analytics/components/googleanalyticspage/body.jsp`(으)로 복사하고 `libs`을(를) 34행의 `apps`(으)로 변경하고 79행의 스크립트 참조를 정규화된 경로로 만듭니다.
1. `/apps/acs/analytics/templates/` 아래에 템플릿 만들기:

   * **리소스 종류** = `acs/analytics/components/googleanalyticspage` 사용
   * (**레이블** = `googleanalytics`)
   * **제목**= `Google Analytics Configuration` 사용
   * (**allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`)
   * (**allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`)
   * **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` 포함(jcr:content 노드가 아닌 템플릿 노드에서)
   * (포함: **cq:designPath** = `/etc/designs/cloudservices/googleanalytics`(jcr:content))

1. 구성 요소 만들기: `/apps/acs/analytics/components/googleanalytics`.

   `googleanalytics.jsp`에 다음 콘텐츠 추가:

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

1. `http://localhost:4502/miscadmin#/etc/cloudservices`(으)로 이동하여 페이지를 만드십시오.

   * **제목**: `Google Analytics`
   * **이름**: `googleanalytics`

   CRXDE Lite으로 돌아가서 `/etc/cloudservices/googleanalytics`에서 `jcr:content`에 다음 속성을 추가하십시오.

   * **이름**: `componentReference`
   * **유형**: `String`
   * **값**: `acs/analytics/components/googleanalytics`

1. 새로 만든 서비스 페이지(`http://localhost:4502/etc/cloudservices/googleanalytics.html`)로 이동하고 **+**&#x200B;을(를) 클릭하여 구성을 만듭니다.

   * **상위 구성**: `/etc/cloudservices/googleanalytics`
   * **제목:** `My First GA Config`

   **Google Analytics 구성**&#x200B;을 선택하고 **만들기**&#x200B;를 클릭합니다.

1. **계정 ID**(예: `AA-11111111-1`)를 입력하십시오. **확인**&#x200B;을 클릭합니다.
1. 페이지로 이동하여 **Cloud Service** 탭의 페이지 속성에 새로 만든 구성을 추가합니다.
1. 페이지에 사용자 지정 마크업이 추가됩니다.
