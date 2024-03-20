---
title: 웹 사이트 콘솔 사용자 지정(클래식 UI)
description: 웹 사이트 관리 콘솔을 확장하여 사용자 지정 열을 표시할 수 있습니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 2b9b4857-821c-4f2f-9ed9-78a1c9f5ac67
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 0%

---

# 웹 사이트 콘솔 사용자 지정(클래식 UI){#customizing-the-websites-console-classic-ui}

## 웹 사이트(siteadmin) 콘솔에 사용자 지정 열 추가 {#adding-a-custom-column-to-the-websites-siteadmin-console}

웹 사이트 관리 콘솔을 확장하여 사용자 지정 열을 표시할 수 있습니다. 콘솔은 를 구현하는 OSGI 서비스를 만들어 확장할 수 있는 JSON 개체를 기반으로 빌드됩니다. `ListInfoProvider` 인터페이스. 이러한 서비스는 콘솔을 빌드하기 위해 클라이언트에 전송되는 JSON 개체를 수정합니다.

이 단계별 자습서에서는 웹 사이트 관리 콘솔에서 를 구현하여 새 열을 표시하는 방법을 설명합니다. `ListInfoProvider` 인터페이스. 다음 단계로 구성됩니다.

1. [OSGI 서비스 만들기](#creating-the-osgi-service) 및 가 포함된 번들을 AEM 서버에 배포합니다.
1. (선택 사항) [새 서비스 테스트](#testing-the-new-service) JSON 호출을 실행하여 콘솔을 빌드하는 데 사용되는 JSON 개체를 요청합니다.
1. [새 열 표시](#displaying-the-new-column) 저장소에서 콘솔의 노드 구조를 확장합니다.

>[!NOTE]
>
>이 자습서는 다음 관리 콘솔을 확장하는 데에도 사용할 수 있습니다.
>
>* 디지털 자산 콘솔
>* 커뮤니티 콘솔
>

### OSGI 서비스 만들기 {#creating-the-osgi-service}

다음 `ListInfoProvider` 인터페이스는 다음 두 가지 방법을 정의합니다.

* `updateListGlobalInfo`, 목록의 전역 속성을 업데이트하려면,
* `updateListItemInfo`를 클릭하여 단일 목록 항목을 업데이트합니다.

두 메서드의 인수는 다음과 같습니다.

* `request`, 연결된 Sling HTTP 요청 개체,
* `info`, 업데이트할 JSON 개체(각각 전역 목록 또는 현재 목록 항목),
* `resource`Sling 리소스

샘플 구현은 다음과 같습니다.

* 를 추가합니다. *별모양* 각 항목에 대한 속성, `true` 페이지 이름이 *e*, 및 `false` 그렇지 않으면.

* 를 추가합니다. *startedCount* 목록에 대해 전역이고 표시된 목록 항목의 수를 포함하는 속성입니다.

OSGI 서비스를 만들려면:

1. CRXDE Lite, [번들 만들기](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. 아래에 샘플 코드를 추가합니다.
1. 번들을 빌드합니다.

새 서비스가 실행 중입니다.

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
>* 구현은 제공된 요청 및/또는 리소스를 기반으로 정보를 JSON 개체에 추가해야 하는지 여부를 결정해야 합니다.
>* 다음의 경우 `ListInfoProvider` 구현은 응답 개체에 있는 속성을 정의하며, 해당 값은 사용자가 제공한 값으로 덮어쓰여집니다.
>
>  다음을 사용할 수 있습니다. [서비스 순위](https://docs.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) 복수 실행 순서를 관리하려면 `ListInfoProvider` 구현.

### 새 서비스 테스트 {#testing-the-new-service}

웹 사이트 관리 콘솔을 열고 사이트를 탐색하면 브라우저가 콘솔을 빌드하는 데 사용되는 JSON 개체를 가져오기 위해 Ajax 호출을 실행합니다. 예를 들어 `/content/geometrixx` 폴더에서는 콘솔을 빌드하도록 다음 요청이 AEM 서버로 전송됩니다.

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

새 서비스가 포함된 번들을 배포한 후 실행되고 있는지 확인하려면 다음을 수행하십시오.

1. 브라우저를 다음 URL로 지정합니다.
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 응답에는 다음과 같이 새 속성이 표시됩니다.

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 새 열 표시 {#displaying-the-new-column}

마지막 단계는 웹 사이트 관리 콘솔의 노드 구조를 조정하여 오버레이하여 모든 Geometrixx 페이지에 대한 새 속성을 표시하는 것입니다 `/libs/wcm/core/content/siteadmin`. 다음과 같이 진행합니다.

1. CRXDE Lite에서 노드 구조를 생성합니다 `/apps/wcm/core/content` 유형의 노드 포함 `sling:Folder` 구조를 반영하기 `/libs/wcm/core/content`.

1. 노드 복사 `/libs/wcm/core/content/siteadmin` 아래에 붙여 넣습니다. `/apps/wcm/core/content`.

1. 노드 복사 `/apps/wcm/core/content/siteadmin/grid/assets` 끝 `/apps/wcm/core/content/siteadmin/grid/geometrixx` 및 가 속성을 변경합니다.

   * 제거 **pageText**

   * 설정 **pathRegex** 끝 `/content/geometrixx(/.*)?`
이렇게 하면 모든 Geometrixx 웹 사이트에 대해 그리드 구성이 활성화됩니다.

   * 설정 **storeProxySuffix** 끝 `.pages.json`

   * 편집 **storeReaderFields** 다중 값 속성 및 추가 `starred` 값.

   * MSM 기능을 활성화하려면 다중 문자열 속성에 다음 MSM 매개 변수를 추가하십시오 **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 추가 `starred` 노드(유형) **nt:unstructured**) 아래 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` 다음 속성을 사용합니다.

   * **dataIndex**: `starred` 문자열 유형의

   * **머리글**: `Starred` 문자열 유형의

   * **xtype**: `gridcolumn` 문자열 유형의

1. (선택 사항) 표시하지 않을 열을 삭제합니다. `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 는 기본적으로 을 가리키는 단축 경로입니다. `/libs/wcm/core/content/siteadmin`.
에서 내 siteadmin 버전으로 리디렉션하려면 `/apps/wcm/core/content/siteadmin`, 속성 정의 `sling:vanityOrder` 에 정의된 값보다 큰 값을 가지려면 `/libs/wcm/core/content/siteadmin`. 기본값은 300이므로 더 높은 값이 적합합니다.

1. 웹 사이트 관리 콘솔로 이동하여 Geometrixx 사이트로 이동합니다.
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. 새 열 호출됨 **별색** 을 사용할 수 있으며 다음과 같이 사용자 정의 정보를 표시합니다.

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>여러 그리드 구성이 다음에 의해 정의된 요청된 경로와 일치하는 경우 **pathRegex** 속성은 가장 구체적인 속성이 아니라 첫 번째 속성이 사용되므로 구성의 순서가 중요합니다.

### 샘플 패키지 {#sample-package}

이 자습서의 결과는 [웹 사이트 관리 콘솔 사용자 지정](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) 패키지 공유 패키지
