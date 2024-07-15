---
title: 고급 URL 구성
description: 제품 및 카테고리 페이지의 URL을 사용자 지정하는 방법을 알아봅니다. 이를 통해 구현에서는 검색 엔진에 대한 URL을 최적화하고 검색을 홍보할 수 있습니다.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 3%

---

# 고급 URL 구성 {#url}

>[!NOTE]
>
>SEO(검색 엔진 최적화)는 많은 마케터의 주요 관심사가 되었습니다. 따라서 많은 AEM 프로젝트에서 SEO 문제를 해결해야 합니다. 자세한 내용은 [SEO 및 URL 관리 모범 사례](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html)를 참조하세요.

[AEM CIF 핵심 구성 요소](https://github.com/adobe/aem-core-cif-components)는 제품 및 범주 페이지의 URL을 사용자 지정하는 고급 구성을 제공합니다. 많은 구현이 SEO(검색 엔진 최적화) 목적으로 이러한 URL을 사용자 지정합니다. 다음 비디오에서는 `UrlProvider` 서비스 및 [Sling 매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)의 기능을 구성하여 제품 및 범주 페이지의 URL을 사용자 지정하는 방법에 대해 자세히 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 구성 {#configuration}

SEO 요구 사항에 따라 `UrlProvider` 서비스를 구성하려면 프로젝트에서 &quot;CIF URL 공급자 구성&quot;에 대한 OSGI 구성을 제공해야 합니다.

>[!NOTE]
>
>AEM CIF 핵심 구성 요소 릴리스 2.0.0부터 URL 공급자 구성은 1.x 릴리스에 알려진 자유 텍스트 구성 가능 형식 대신 사전 정의된 URL 형식만 제공합니다. 또한 선택기를 사용하여 URL에 데이터를 전달하던 방식이 접미사로 대체되었습니다.

### 제품 페이지 URL 형식 {#product}

제품 페이지의 URL을 구성하고 다음 옵션을 지원합니다.

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`(기본값)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

[Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)가 있는 경우:

* `{{page}}`이(가) `/content/venia/us/en/products/product-page`(으)로 대체되었습니다.
* `{{sku}}`은(는) 제품의 SKU로 대체됩니다(예: `VP09`).
* `{{url_key}}`은(는) 제품의 `url_key` 속성(예: `lenora-crochet-shorts`)으로 대체됩니다.
* `{{url_path}}`은(는) 제품의 `url_path`(예: `venia-bottoms/venia-pants/lenora-crochet-shorts`)로 대체됩니다.
* `{{variant_sku}}`은(는) 현재 선택한 변형(예: `VP09-KH-S`)으로 대체됩니다.

`url_path`이(가) 더 이상 사용되지 않으므로 미리 정의된 제품 URL 형식은 제품 `url_rewrites`을(를) 사용하고 `url_path`을(를) 사용할 수 없는 경우 대체 요소로 경로 세그먼트가 가장 많은 URL 형식을 선택합니다.

위의 예제 데이터를 사용하면 기본 URL 형식을 사용하여 형식이 지정된 제품 변형 URL은 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`과(와) 같습니다.

### 카테고리 페이지 URL 형식 {#product-list}

범주 또는 제품 목록 페이지의 URL을 구성하고 다음 옵션을 지원합니다.

* `{{page}}.html/{{url_path}}.html`(기본값)
* `{{page}}.html/{{url_key}}.html`

[Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)가 있는 경우:

* `{{page}}`이(가) `/content/venia/us/en/products/category-page`(으)로 대체되었습니다.
* `{{url_key}}`이(가) 범주의 `url_key` 속성으로 대체되었습니다.
* `{{url_path}}`이(가) 범주의 `url_path`(으)로 대체되었습니다.

위의 예제 데이터를 사용하면 기본 URL 형식을 사용하여 형식이 지정된 카테고리 페이지 URL이 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`처럼 보입니다.

>[!NOTE]
> 
>`url_path`은(는) `/` 슬래시로 구분된 제품이나 범주의 상위 항목 `url_keys`과(와) 제품이나 범주의 `url_key`의 연결입니다.

### 특정 범주/제품 페이지 {#specific-pages}

카탈로그의 특정 범주 또는 제품에 대해서만 [여러 범주 및 제품 페이지](multi-template-usage.md)를 만들 수 있습니다.

`UrlProvider`은(는) 작성자 계층 인스턴스에서 이러한 페이지에 대한 딥링크를 생성하도록 사전 구성되어 있습니다. 이 기능은 미리보기 모드를 사용하여 사이트를 탐색하고 특정 제품 또는 카테고리 페이지로 이동한 다음 편집 모드로 다시 전환하여 페이지를 편집하는 편집자에게 유용합니다.

반면에 게시 계층 인스턴스에서는 카탈로그 페이지 URL을 안정적으로 유지해야 검색 엔진 순위에서 이득을 잃지 않습니다. 이러한 게시 계층 인스턴스로 인해 기본적으로 특정 카탈로그 페이지에 대한 딥 링크가 렌더링되지 않습니다. 이 동작을 변경하려면 항상 특정 페이지 url을 생성하도록 _CIF URL 공급자별 페이지 전략_&#x200B;을 구성할 수 있습니다.

## 사용자 정의 URL 형식 {#custom-url-format}

프로젝트가 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 또는 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 서비스 인터페이스를 구현하고 구현을 OSGI 서비스로 등록할 수 있는 사용자 지정 URL 형식을 제공하기 위해. 이러한 구현은 사용 가능한 경우 구성된 사전 정의된 형식을 대체합니다. 등록된 구현이 여러 개일 경우 서비스 순위가 높은 구현이 서비스 순위가 낮은 구현을 대체합니다.

사용자 지정 URL 형식 구현은 주어진 매개 변수에서 URL을 작성하고 URL을 구문 분석하여 동일한 매개 변수를 각각 반환하기 위한 메서드 쌍을 구현해야 합니다.

## Sling 매핑과 결합 {#sling-mapping}

`UrlProvider` 외에도 URL을 다시 작성하고 처리하도록 [Sling 매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)을 구성할 수 있습니다. AEM Archetype 프로젝트에서는 포트 4503(게시) 및 80(Dispatcher)에 대한 일부 Sling 매핑을 구성할 수 있도록 [예제 구성](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)도 제공합니다.

## AEM Dispatcher과 결합 {#dispatcher}

`mod_rewrite` 모듈과 함께 AEM Dispatcher HTTP 서버를 사용하여 URL 재쓰기를 수행할 수도 있습니다. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)은(는) 생성된 크기에 대한 기본 [다시 작성 규칙](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)이 이미 포함된 참조 AEM Dispatcher 구성을 제공합니다.

## 예

[Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia) 프로젝트에는 제품 및 범주 페이지에 대한 사용자 지정 URL의 사용을 보여 주는 샘플 구성이 포함되어 있습니다. 이를 통해 각 프로젝트는 SEO 요구 사항에 따라 제품 및 카테고리 페이지에 대한 개별 URL 패턴을 설정할 수 있습니다. 위에서 설명한 대로 CIF `UrlProvider`과(와) Sling 매핑의 조합이 사용됩니다.

>[!NOTE]
>
>프로젝트에서 사용하는 외부 도메인을 사용하여 이 구성을 조정해야 합니다. Sling 매핑은 호스트 이름과 도메인을 기반으로 작동합니다. 따라서 이 구성은 기본적으로 비활성화되며 배포 전에 활성화해야 합니다. 이를 위해 `ui.content/src/main/content/jcr_root/etc/map.publish/https`에서 Sling 매핑 `hostname.adobeaemcloud.com` 폴더의 이름을 사용된 도메인 이름에 따라 바꾸고 `resource.resolver.map.location="/etc/map.publish"`을(를) 프로젝트의 `JcrResourceResolver` 구성에 추가하여 이 구성을 사용하도록 설정합니다.

## 추가 리소스

* [Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
* [AEM 리소스 매핑](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling 매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
