---
title: Analytics에 대한 서버측 페이지 이름 지정 구현
description: Adobe Analytics은 s.pageName 속성을 사용하여 페이지를 고유하게 식별하고 페이지에 대해 수집된 데이터를 연결합니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Analytics에 대한 서버측 페이지 이름 지정 구현{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics은 `s.pageName` 속성을 사용하여 페이지를 고유하게 식별하고 페이지에 대해 수집된 데이터를 연결합니다. 일반적으로 AEM에서 다음 작업을 수행하여 AEM이 Analytics에 전송하는 이 속성에 값을 할당합니다.

* Analytics 클라우드 서비스 프레임워크를 사용하여 CQ 변수를 Analytics `s.pageName` 속성에 매핑합니다. ([구성 요소 데이터를 Adobe Analytics 속성과 매핑](/help/sites-administering/adobeanalytics-mapping.md)을(를) 참조하십시오.)

* `s.pageName` 속성에 매핑하는 CQ 변수를 포함하도록 페이지 구성 요소를 디자인합니다. ([사용자 지정 구성 요소에 대한 Adobe Analytics 추적 구현](/help/sites-developing/extending-analytics-components.md)을 참조하세요.)

Sites 콘솔 및 Content Insight에서 Analytics 보고서 데이터를 노출하려면 AEM에 각 페이지의 `s.pageName` 속성 값이 필요합니다. AEM Analytics Java API는 사이트 콘솔 및 콘텐츠 인사이트에 `s.pageName` 속성의 값을 제공하기 위해 구현하는 `AnalyticsPageNameProvider` 인터페이스를 정의합니다. `AnaltyicsPageNameProvider` 서비스는 추적 목적으로 클라이언트의 JavaScript을 사용하여 동적으로 설정할 수 있으므로 보고 목적으로 서버의 pageName 속성을 확인합니다.

## 기본 Analytics 페이지 이름 공급자 서비스 {#the-default-analytics-page-name-provider-service}

`DefaultPageNameProvider` 서비스는 페이지의 Analytics 데이터를 검색하는 데 사용할 `s.pageName` 속성의 값을 결정하는 기본 서비스입니다. 이 서비스는 AEM Foundation 페이지 구성 요소(`/libs/foundation/components/page`)와 함께 작동합니다. 이 페이지 구성 요소는 `s.pageName` 속성에 매핑되는 다음 CQ 변수를 정의합니다.

* `pagedata.path`: 값이 페이지 경로로 설정되어 있습니다.
* `pagedata.title`: 값이 페이지 제목으로 설정되어 있습니다.
* `pagedata.navTitle`: 값이 페이지 탐색 제목으로 설정되어 있습니다.

`DefaultPageNameProvider` 서비스는 Analytics 클라우드 서비스 프레임워크의 `s.pageName` 속성에 매핑되는 CQ 변수를 결정합니다. 그런 다음 서비스는 분석 보고서 데이터를 검색하는 데 사용할 적절한 페이지 속성을 결정합니다.

* `pagedata.path`: 서비스에서 `page.getPath()` 사용

* `pagedata.title`: 서비스에서 `page.getTitle()` 사용

* `pagedata.navTitle`: 서비스에서 `page.getNavigationTitle()` 사용

`page` 개체는 페이지의 [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Java 개체입니다.

CQ 변수를 프레임워크의 `s.pageName` 속성에 매핑하지 않으면 `s.pageName`의 값이 페이지 경로에서 생성됩니다. 예를 들어 경로가 `/content/geometrixx/en`인 페이지는 `s.pageName`에 대해 `content:geometrixx:en` 값을 사용합니다.

>[!NOTE]
>
>DefaultPageNameProvider 서비스는 100개의 서비스 순위를 사용합니다.

## Analytics 보고의 연속성 유지 {#maintaining-continuity-in-analytics-reporting}

페이지에 대한 분석 데이터의 전체 내역을 유지 관리하려면 페이지에 사용되는 s.pageName 속성의 값이 변경되지 않아야 합니다. 그러나 기본 페이지 구성 요소가 정의하는 분석 속성은 쉽게 변경할 수 있습니다. 예를 들어 페이지를 이동하면 `pagedata.path` 값이 변경되고 보고 내역의 연속성이 끊어집니다.

* 이전 경로에 대해 수집된 데이터는 더 이상 페이지와 연결되지 않습니다.
* 다른 페이지가 한 번 사용한 경로를 사용하는 경우 다른 페이지는 해당 경로에 대한 데이터를 상속합니다.

보고 연속성을 보장하려면 `s.pageName` 값에 다음 특성이 있어야 합니다.

* 고유.
* 안정적이군
* 사람이 읽을 수 있습니다.

예를 들어, 사용자 지정 페이지 구성 요소에는 작성자가 `s.pageProperties` 속성의 값으로 사용되는 페이지의 고유 ID를 지정하는 데 사용하는 페이지 속성이 포함될 수 있습니다.

* 페이지에는 페이지 속성에 저장된 고유 ID의 값으로 설정된 analytics 변수가 포함되어 있습니다.
* Analytics 변수가 Analytics 프레임워크의 `s.pageProperties` 속성에 매핑됩니다.
* AnalyticsPageNameProvider 인터페이스를 구현하면 페이지 Analytics 데이터를 쿼리하는 데 사용할 페이지 속성의 값을 검색합니다.

>[!NOTE]
>
>`s.pageName` 값에 대한 효과적인 전략을 개발하는 데 도움이 필요하면 Analytics 컨설턴트에게 문의하십시오.

### Analytics 페이지 이름 공급자 서비스 구현 {#implementing-an-analytics-page-name-provider-service}

`com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` 인터페이스를 OSGi 서비스로 구현하여 `s.pageName` 속성 값을 검색하는 논리를 사용자 지정합니다. 사이트 페이지 분석 및 컨텐츠 인사이트는 이 서비스를 사용하여 Analytics에서 보고서 데이터를 검색합니다.

AnalyticsPageNameProvider 인터페이스는 구현해야 하는 두 가지 메서드를 정의합니다.

* `getPageName`: `s.pageName` 속성으로 사용할 값을 나타내는 `String` 값을 반환합니다.

* `getResource`: `s.pageName` 속성과 연결된 페이지를 나타내는 `org.apache.sling.api.resource.Resource` 개체를 반환합니다.

두 메서드 모두 `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` 개체를 매개 변수로 사용합니다. `AnalyticsPageNameContext` 클래스는 Analytics 호출의 컨텍스트에 대한 정보를 제공합니다.

* 페이지 리소스의 기본 경로입니다.
* Analytics 클라우드 서비스 구성에 대한 `Framework` 개체입니다.
* 페이지의 `Resource` 개체입니다.
* 페이지의 `ResourceResolver` 개체입니다.

클래스는 페이지 이름에 대한 setter도 제공합니다.

### 예제 AnalyticsPageNameProvider 구현 {#example-analyticspagenameprovider-implementation}

다음 예제 `AnalyticsPageNameProvider` 구현은 사용자 지정 페이지 구성 요소를 지원합니다.

* 구성 요소가 기초 페이지 구성 요소를 확장합니다.
* 대화 상자에는 작성자가 `s.pageName` 속성의 값을 지정하는 데 사용하는 필드가 포함되어 있습니다.
* 속성 값은 페이지 인스턴스의 `jcr:content`노드에 있는 pageName 속성에 저장됩니다.
* `s.pageName` 속성을 저장하는 Analytics 속성을 `pagedata.pagename`이라고 합니다. 이 속성은 Analytics 프레임워크의 `s.pageName` 속성에 매핑됩니다.

`getPageName` 메서드의 다음 구현에서는 프레임워크 매핑이 올바르게 구성된 경우 pageName 노드 속성 값을 반환합니다.

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

다음 getResource 메서드 구현은 페이지에 대한 Resource 개체를 반환합니다.

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

다음 코드는 서비스를 구성하는 SCR 주석을 포함하여 전체 클래스를 나타냅니다. 서비스 순위는 200이며 기본 서비스를 재정의합니다.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```
