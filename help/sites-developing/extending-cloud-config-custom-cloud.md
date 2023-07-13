---
title: 사용자 지정 클라우드 서비스 만들기
description: 사용자 지정 Cloud Service 유형을 사용하여 기본 Cloud Services 세트를 확장할 수 있습니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 13%

---

# 사용자 지정 클라우드 서비스 만들기{#creating-a-custom-cloud-service}

사용자 지정 Cloud Service 유형을 사용하여 기본 Cloud Services 세트를 확장할 수 있습니다. 이렇게 하면 사용자 지정 마크업을 구조화된 방식으로 페이지에 삽입할 수 있습니다. 이는 주로 Google Analytics, Chartbeat 등과 같은 서드파티 분석 공급자에게 사용됩니다. Cloud Services은 상위 페이지에서 하위 페이지로 상속되며, 어떤 수준에서든 상속을 중단할 수 있습니다.

>[!NOTE]
>
>Cloud Service 만들기에 대한 이 단계별 안내서는 Google Analytics을 사용하는 예제입니다. 모든 항목이 사용 사례에 적용되지 않을 수 있습니다.

1. CRXDE Lite에서 `/apps`:

   * **이름**: `acs`
   * **유형**: `nt:folder`

1. 아래에 노드 만들기 `/apps/acs`:

   * **이름**: `analytics`
   * **유형**: `sling:Folder`

1. 아래에 두 개의 노드 만들기 `/apps/acs/analytics`:

   * **이름**: 구성 요소
   * **유형**: `sling:Folder`

   및

   * **이름**: 템플릿
   * **유형**: `sling:Folder`

1. 마우스 오른쪽 단추 클릭 `/apps/acs/analytics/components`. 선택 **만들기...** 뒤에 오는 **구성 요소 만들기...** 열리는 대화 상자에서 다음을 지정할 수 있습니다.

   * **레이블**: `googleanalyticspage`
   * **제목**: `Google Analytics Page`
   * **Super Type**: `cq/cloudserviceconfigs/components/configpage`
   * **그룹**: `.hidden`

1. 클릭 **다음** 두 번 지정하고 다음을 지정합니다.

   * **허용된 상위:** `acs/analytics/templates/googleanalytics`

   클릭 **다음** 두 번 클릭 **확인**.

1. 에 속성 추가 `googleanalyticspage`:

   * **이름:** `cq:defaultView`
   * **값:** `html`

1. 이름이 인 파일 만들기 `content.jsp` 아래에 `/apps/acs/analytics/components/googleanalyticspage`, 다음 컨텐츠 포함:

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

1. 아래에 노드 만들기 `/apps/acs/analytics/components/googleanalyticspage/`:

   * **이름**: `dialog`
   * **유형**: `cq:Dialog`
   * **속성**:

      * **이름**: `title`
      * **유형**: `String`
      * **값**: `Google Analytics Config`
      * **이름**: `xtype`
      * **유형**: `String`
      * **값**: `dialog`

1. 아래에 노드 만들기 `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **이름**: `items`
   * **유형**: `cq:Widget`
   * **속성**:

      * **이름**: `xtype`
      * **유형**: `String`
      * **값**: `tabpanel`

1. 아래에 노드 만들기 `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **이름**: `items`
   * **유형**: `cq:WidgetCollection`

1. 아래에 노드 만들기 `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **이름**: tab1
   * **유형**: `cq:Panel`
   * **속성**:

      * **이름**: `title`
      * **유형**: `String`
      * **값**: `Config`

1. 아래에 노드 만들기 `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

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

1. 복사 `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` 끝 `/apps/acs/analytics/components/googleanalyticspage/body.jsp` 및 변경 `libs` 끝 `apps` 34행에서 79행의 스크립트 참조를 정규화된 경로로 만듭니다.
1. 아래에 템플릿 만들기 `/apps/acs/analytics/templates/`:

   * 포함 **리소스 유형** = `acs/analytics/components/googleanalyticspage`
   * 포함 **레이블** = `googleanalytics`
   * 포함 **제목**= `Google Analytics Configuration`
   * 포함 **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * 포함 **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * 포함 **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (jcr:content 노드가 아닌 템플릿 노드에서)
   * 포함 **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (jcr:content)

1. 구성 요소 만들기: `/apps/acs/analytics/components/googleanalytics`.

   에 다음 콘텐츠 추가 `googleanalytics.jsp`:

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

1. 다음으로 이동 `http://localhost:4502/miscadmin#/etc/cloudservices` 페이지를 만듭니다.

   * **제목**: `Google Analytics`
   * **이름**: `googleanalytics`

   CRXDE Lite으로 돌아가서 `/etc/cloudservices/googleanalytics`, 다음 속성을 추가합니다. `jcr:content`:

   * **이름**: `componentReference`
   * **유형**: `String`
   * **값**: `acs/analytics/components/googleanalytics`

1. 새로 생성된 서비스 페이지 ( )로 이동합니다. `http://localhost:4502/etc/cloudservices/googleanalytics.html`)을 클릭하고 **+** 구성을 만들려면 다음 작업을 수행하십시오.

   * **상위 구성**: `/etc/cloudservices/googleanalytics`
   * **제목:**  `My First GA Config`

   선택 **Google Analytics 구성** 및 클릭 **만들기**.

1. 다음을 입력하십시오. **계정 ID**, 예 `AA-11111111-1`. **확인**&#x200B;을 클릭합니다.
1. 페이지로 이동하여 페이지 속성 아래의 새로 만든 구성을 추가합니다. **Cloud Services** 탭.
1. 페이지에 사용자 지정 마크업이 추가됩니다.
