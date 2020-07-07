---
title: 웹 사이트 콘솔 사용자 지정(클래식 UI)
seo-title: 웹 사이트 콘솔 사용자 지정(클래식 UI)
description: 웹 사이트 관리 콘솔을 확장하여 사용자 정의 열을 표시할 수 있습니다
seo-description: 웹 사이트 관리 콘솔을 확장하여 사용자 정의 열을 표시할 수 있습니다
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# 웹 사이트 콘솔 사용자 지정(클래식 UI){#customizing-the-websites-console-classic-ui}

## 웹 사이트(siteadmin) 콘솔에 사용자 지정 열 추가 {#adding-a-custom-column-to-the-websites-siteadmin-console}

웹 사이트 관리 콘솔을 확장하여 사용자 정의 열을 표시할 수 있습니다. 콘솔은 인터페이스를 구현하는 OSGI 서비스를 만들어 확장할 수 있는 JSON 개체를 기반으로 `ListInfoProvider` 구축됩니다. 이러한 서비스는 콘솔을 빌드하기 위해 클라이언트에 전송된 JSON 개체를 수정합니다.

이 단계별 자습서에서는 인터페이스를 구현하여 웹 사이트 관리 콘솔에서 새 열을 표시하는 방법을 `ListInfoProvider` 설명합니다. 다음 단계로 구성됩니다.

1. [OSGI 서비스를](#creating-the-osgi-service) 만들고 이 서비스가 포함된 번들을 AEM 서버에 배포합니다.
1. (선택 사항) [콘솔을 만드는 데 사용되는 JSON 개체를 요청하기 위해 JSON 호출을 실행하여 새로운 서비스를](#testing-the-new-service) 테스트하십시오.
1. [저장소에서 콘솔의 노드 구조를 확장하여 새 열](#displaying-the-new-column) 표시

>[!NOTE]
>
>이 자습서는 다음 관리 콘솔을 확장하는 데에도 사용할 수 있습니다.
>
>* 디지털 자산 콘솔
>* 커뮤니티 콘솔
>



### OSGI 서비스 만들기 {#creating-the-osgi-service}

이 `ListInfoProvider` 인터페이스는 다음 두 가지 방법을 정의합니다.

* `updateListGlobalInfo`, to update global properties of list,
* `updateListItemInfo`를 클릭하여 단일 목록 항목을 업데이트합니다.

두 메서드 모두에 대한 인수는 다음과 같습니다.

* `request`, 관련 HTTP 요청 객체
* `info`, the JSON object to update, which is each the global list or the current list item,
* `resource`, a Sling resource.

아래 샘플 구현:

* 페이지 이름이 e로 시작하는 *경우, 각 항목에 대해* 별표 `true` 의 *속성*&#x200B;을 `false` 추가합니다.

* 목록 *에 대해* 전역 항목이며 별표 목록 항목의 수를 포함하는 stledCount 속성을 추가합니다.

OSGI 서비스를 만들려면:

1. CRXDE Lite에서 번들 [을 만듭니다](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. 아래 샘플 코드를 추가합니다.
1. 번들 제작

새 서비스가 가동되고 있습니다.

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* 구현은 제공된 요청 및/또는 리소스를 기반으로 JSON 개체에 정보를 추가할지 여부를 결정해야 합니다.
>* 구현에서 응답 개체에 이미 존재하는 속성을 정의하면 해당 값을 사용자가 제공한 속성으로 덮어씁니다. `ListInfoProvider`
>
>  
여러 구현의 [실행 순서를](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) 관리하는 데 `ListInfoProvider` 서비스 등급을 사용할 수있습니다.

### 새 서비스 테스트 {#testing-the-new-service}

웹 사이트 관리 콘솔을 열고 사이트를 검색할 때 브라우저는 콘솔을 빌드하는 데 사용되는 JSON 개체를 가져오기 위한 ajax 호출을 실행합니다. 예를 들어 폴더를 탐색하면 AEM `/content/geometrixx` 서버로 다음 요청이 전송되어 콘솔을 만듭니다.

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

새 서비스가 포함된 번들을 배포한 후에 실행되고 있는지 확인하려면 다음을 수행하십시오.

1. 브라우저를 다음 URL로 가리킵니다.
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 응답에 다음과 같이 새 속성이 표시되어야 합니다.

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 새 열 표시 {#displaying-the-new-column}

마지막 단계는 오버레이하여 모든 Geometrixx 페이지에 대한 새 속성을 표시하도록 웹 사이트 관리 콘솔의 노드 구조를 수정하는 것입니다 `/libs/wcm/core/content/siteadmin`. 다음과 같이 진행합니다.

1. CRXDE Lite에서 구조를 반영하도록 유형 노드 `/apps/wcm/core/content` 가 있는 노드 구조 `sling:Folder` 를 생성합니다 `/libs/wcm/core/content`.

1. 노드를 복사하고 아래 `/libs/wcm/core/content/siteadmin` 에 붙여넣습니다 `/apps/wcm/core/content`.

1. 노드를 다음 `/apps/wcm/core/content/siteadmin/grid/assets` 에 복사하고 속성 `/apps/wcm/core/content/siteadmin/grid/geometrixx` 을 변경합니다.

   * pageText **제거**

   * pathRegex **를** 다음으로 `/content/geometrixx(/.*)?`설정합니다. 그러면 모든 geometrixx 웹 사이트에 격자 구성이 활성화됩니다.

   * storeProxySuffix **를 다음으로** 설정 `.pages.json`

   * storeReaderFields **다중 값** 속성을 편집하고 `starred` 값을 추가합니다.

   * MSM 기능을 활성화하려면 다음 MSM 매개 변수를 다중 문자열 속성 storeReaderFields에 **추가합니다**.

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 다음 속성을 사용하여 `starred` 아래 **노드(nt:unstructured**&#x200B;유형 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` )를 추가합니다.

   * **dataIndex**: `starred` 문자열 유형

   * **헤더**: `Starred` 문자열 유형

   * **xtype**: `gridcolumn` 문자열 유형

1. (선택 사항) 표시하지 않을 열을 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 는 기본적으로 가리키는 별칭 경로입니다 `/libs/wcm/core/content/siteadmin`.
이 값을 siteadmin 버전으로 리디렉션하려면 속성 `/apps/wcm/core/content/siteadmin` 을 정의하면 속성 `sling:vanityOrder` 이 정의된 값보다 더 높은 값으로 정의됩니다 `/libs/wcm/core/content/siteadmin`. 기본값은 300이므로 더 높은 값은 적절합니다.

1. 웹 사이트 관리 콘솔로 이동하여 Geometrixx 사이트로 이동합니다.
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. Started라는 새 열 **을** 사용할 수 있으며 다음과 같이 사용자 지정 정보를 표시할 수 있습니다.

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>여러 그리드 구성이 pathRegex **속성에 의해 정의된 요청된** 경로와 일치하는 경우 가장 구체적인 구성 구성이 아닌 첫 번째 격자 구성이 사용됩니다. 즉, 구성 순서가 중요합니다.

### 샘플 패키지 {#sample-package}

이 자습서의 결과는 패키지 공유에서 웹 사이트 관리 콘솔 [사용자](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) 지정에서 확인할 수 있습니다.
