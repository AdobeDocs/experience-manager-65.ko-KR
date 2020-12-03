---
title: 사용자 지정 확장 프로그램 만들기
seo-title: 사용자 지정 확장 프로그램 만들기
description: AEM 또는 AEM에서 Adobe Campaign으로 사용자 정의 코드를 호출할 수 있습니다
seo-description: AEM 또는 AEM에서 Adobe Campaign으로 사용자 정의 코드를 호출할 수 있습니다
uuid: 8392aa0d-06cd-4b37-bb20-f67e6a0550b1
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f536bcc1-7744-4f05-ac6a-4cec94a1ffb6
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---


# 사용자 지정 확장 프로그램 만들기{#creating-custom-extensions}

일반적으로 프로젝트를 구현할 때 AEM 및 Adobe Campaign 모두에 사용자 정의 코드가 있습니다. 기존 API를 사용하면 AEM 또는 AEM에서 Adobe Campaign으로 Adobe Campaign에서 사용자 정의 코드를 호출할 수 있습니다. 이 문서에서는 이러한 작업을 수행하는 방법에 대해 설명합니다.

## 전제 조건 {#prerequisites}

다음을 설치해야 합니다.

* Adobe Experience Manager
* Adobe Campaign 6.1

자세한 내용은 [Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md)과 AEM 통합을 참조하십시오.

## 예 1:AEM to Adobe Campaign {#example-aem-to-adobe-campaign}

AEM과 캠페인 간의 표준 통합은 JSON과 JSSP(JavaScript Server 페이지)를 기반으로 합니다. 이러한 JSSP 파일은 캠페인 콘솔에서 찾을 수 있으며, 모두 **amc**(Adobe Marketing Cloud)으로 시작합니다.

![chlimage_1-15](assets/chlimage_1-15a.png)

>[!NOTE]
>
>[이 예는 패키지 공유에서 사용할 수 있는 Geometrixx](/help/sites-developing/we-retail.md)를 참조하십시오.

이 예에서는 새 사용자 지정 JSSP 파일을 만들고 AEM 쪽에서 이 파일을 호출하여 결과를 가져옵니다. 예를 들어 Adobe Campaign에서 데이터를 검색하거나 Adobe Campaign에 데이터를 저장하는 데 사용할 수 있습니다.

1. Adobe Campaign에서 새 JSSP 파일을 만들려면 **새로 만들기** 아이콘을 클릭합니다.

   ![](do-not-localize/chlimage_1-4a.png)

1. 이 JSSP 파일의 이름을 입력합니다. 이 예에서는 **cus:custom.jssp**(즉, **cus** 네임스페이스에 있어야 함)을 사용합니다.

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. jssp-file에 다음 코드를 넣습니다.

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. 작업 저장 남은 일은 AEM입니다
1. 이 JSSP를 호출하려면 AEM 측에 단순 서블릿을 만듭니다. 이 예에서는 다음을 가정합니다.

   * AEM과 캠페인 간의 연결
   * 캠페인 클라우드 서비스는 **/content/geometrixx-outdoors**&#x200B;에 구성됩니다.

   이 예에서 가장 중요한 개체는 Adobe Campaign 측에서 jssp 파일을 호출(가져오기 및 게시)할 수 있는 **GenericCampaignConnector**&#x200B;입니다.

   다음은 작은 코드 조각입니다.

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. 이 예에서 보듯이 자격 증명을 호출로 전달해야 합니다. Campaign 클라우드 서비스가 구성된 페이지를 전달하는 getCredentials() 메서드를 통해 이것을 얻을 수 있습니다.

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

전체 코드는 다음과 같습니다.

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.ServletException;

import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.sling.SlingServlet;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.mcm.campaign.CallResults;
import com.day.cq.mcm.campaign.CampaignCredentials;
import com.day.cq.mcm.campaign.GenericCampaignConnector;
import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageManager;
import com.day.cq.wcm.api.PageManagerFactory;
import com.day.cq.wcm.webservicesupport.Configuration;

@SlingServlet(paths="/bin/campaign", methods="GET")
public class CustomServlet extends SlingSafeMethodsServlet {

 private final Logger log = LoggerFactory.getLogger(this.getClass());

 @Reference
 private GenericCampaignConnector campaignConnector;

 @Reference
 private PageManagerFactory pageManagerFactory;

 @Override
 protected void doGet(SlingHttpServletRequest request,
   SlingHttpServletResponse response) throws ServletException,
   IOException {

  PageManager pm = pageManagerFactory.getPageManager(request.getResourceResolver());

  Page page = pm.getPage("/content/geometrixx-outdoors");

  String result = null;
  if ( page != null) {
   result = callCustomFunction(page);
  }
  if ( result != null ) {
   PrintWriter pw = response.getWriter();
   pw.print(result);
  }
 }

 private String callCustomFunction(Page page ) {
  try {
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);

   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
  } catch (Exception e ) {
   log.error("Something went wrong during the connection", e);
  }
  return null;

 }

}
```

## 예 2:Adobe Campaign - AEM {#example-adobe-campaign-to-aem}

AEM은 siteadmin 탐색기 보기에서 사용할 수 있는 개체를 검색할 수 있는 특별한 API를 제공합니다.

![chlimage_1-17](assets/chlimage_1-17a.png)

>[!NOTE]
>
>[이 예는 패키지 공유에서 사용할 수 있는 Geometrixx](/help/sites-developing/we-retail.md)를 참조하십시오.

탐색기의 각 노드에 대해 연결된 API가 있습니다. For example for the node:

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

API는 다음과 같습니다.

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

모두 얻으려는 하위 수준(모두 포함)의 수에 따라 URL **.1.json**&#x200B;의 끝을 **.2.json**, **.3.json**&#x200B;으로 바꿀 수 있습니다. **무한** 키워드를 모두 사용할 수 있습니다.

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

이제 API를 사용하려면 기본적으로 AEM에서 기본 인증을 사용한다는 사실을 알아야 합니다.

이름이 **amcIntegration.js**&#x200B;인 JS 라이브러리는 6.1.1(빌드 8624 이상)에서 사용할 수 있으며 다른 라이브러리 중에서 해당 논리를 구현합니다.

### AEM API 호출 {#aem-api-call}

```java
loadLibrary("nms:amcIntegration.js");

var cmsAccountId = sqlGetInt("select iExtAccountId from NmsExtAccount where sName=$(sz)","aemInstance")
var cmsAccount = nms.extAccount.load(String(cmsAccountId));
var cmsServer = cmsAccount.server;

var request = new HttpClientRequest(cmsServer+"/content/campaigns/geometrixx.infinity.json")
aemAddBasicAuthentication(cmsAccount, request);
request.method = "GET"
request.header["Content-Type"] = "application/json; charset=UTF-8";
request.execute();
var response = request.response;
```

