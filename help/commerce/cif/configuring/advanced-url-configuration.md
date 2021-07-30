---
title: 고급 URL 구성
description: 제품 및 카테고리 페이지의 URL을 사용자 지정하는 방법을 알아봅니다. 이를 통해 구현은 검색 엔진에 대한 URL을 최적화하고 검색을 승격할 수 있습니다.
sub-product: 상거래
doc-type: technical-video
activity: setup
audience: administrator
feature: 전자 상거래 통합 프레임워크
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: dbd38aa75caa7c3c2feee79702ab85ab397eb583
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 4%

---

# 고급 URL 구성 {#url}

[AEM CIF 핵심 ](https://github.com/adobe/aem-core-cif-components) 구성 요소는 제품 및 카테고리 페이지의 URL을 사용자 지정하는 고급 구성을 제공합니다. 많은 구현이 SEO(검색 엔진 최적화) 목적으로 이러한 URL을 사용자 지정합니다. 다음 비디오에서는 `UrlProvider` 서비스 및 [Sling Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)의 기능을 구성하여 제품 및 카테고리 페이지의 URL을 사용자 지정하는 방법에 대해 자세히 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 구성 {#configuration}

SEO 요구 사항에 따라 `UrlProvider` 서비스를 구성하려면 프로젝트가 필요합니다. &quot;CIF URL 공급자 구성&quot;에 대한 OSGI 구성을 제공해야 합니다.

>[!NOTE]
>
> AEM CIF 코어 구성 요소 의 릴리스 2.0.0부터 URL 공급자 구성에서는 1.x 릴리스에서 제공되는 자유 텍스트 구성 가능 형식 대신 미리 정의된 URL 형식만 제공합니다. 또한 URL에서 데이터를 전달하는 선택기를 사용하여 접미사로 대체되었습니다.

### 제품 페이지 URL 형식 {#product}

제품 페이지의 URL을 구성하고 다음 옵션을 지원합니다.

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (기본값)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

[Venia 참조 저장소의 경우](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 교체  `/content/venia/us/en/products/product-page`
* `{{sku}}` 은 제품의 sku(예: )로 대체됩니다.  `VP09`
* `{{url_key}}` 은 제품의  `url_key` 속성으로 대체됩니다(예: ).  `lenora-crochet-shorts`
* `{{url_path}}` 은(는) 제품의  `url_path`예:  `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 은 현재 선택한 변형으로 대체됩니다(예: ).  `VP09-KH-S`

위의 예제 데이터를 사용하면 기본 URL 형식을 사용하여 형식이 지정된 제품 변형 URL은 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S` 과 같습니다.

### 카테고리 페이지 URL 형식 {#product-list}

카테고리 또는 제품 목록 페이지의 URL을 구성하고 다음 옵션을 지원합니다.

* `{{page}}.html/{{url_path}}.html` (기본값)
* `{{page}}.html/{{url_key}}.html`

[Venia 참조 저장소의 경우](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 교체  `/content/venia/us/en/products/category-page`
* `{{url_key}}` 은 카테고리의 속성으로  `url_key` 대체됩니다
* `{{url_path}}` 은(는) 카테고리의  `url_path`

위의 예제 데이터를 사용할 경우 기본 URL 형식을 사용하여 형식이 지정된 카테고리 페이지 URL은 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html` 과 같습니다.

>[!NOTE]
> 
> `url_path`은(는) 제품 또는 카테고리의 상위 항목 `url_keys`과 `/` 슬래시로 구분된 제품 또는 카테고리의 `url_key`의 연결입니다.

## 사용자 지정 URL 형식 {#custom-url-format}

사용자 지정 URL 형식을 제공하기 위해 프로젝트는 [`UrlFormat` 인터페이스](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/UrlFormat.html)를 구현하고 카테고리 페이지 또는 제품 페이지 URL 형식으로 사용하여 구현을 OSGI 서비스로 등록할 수 있습니다. `UrlFormat#PROP_USE_AS` 서비스 속성은 바꿀 사전 정의된 형식 중 하나를 나타냅니다.

* `useAs=productPageUrlFormat`이 구성된 제품 페이지 url 형식을 대체합니다
* `useAs=categoryPageUrlFormat`은 구성된 카테고리 페이지 url 형식을 대체합니다

OSGI 서비스로 등록된 `UrlFormat` 의 구현이 여러 개 있는 경우 서비스 등급이 높은 구현은 해당 구현이 더 낮은 서비스 등급을 대체합니다.

`UrlFormat` 은 주어진 매개 변수 맵에서 URL을 작성하고 동일한 매개 변수 맵을 반환하기 위해 URL을 구문 분석하기 위한 한 쌍의 메서드를 구현해야 합니다. 매개 변수는 위에서 설명한 것과 동일하며, 카테고리에 대해서만 추가 `{{uid}}` 매개 변수가 `UrlFormat`에 제공됩니다.

## Sling 매핑과 결합 {#sling-mapping}

`UrlProvider` 외에 URL을 다시 작성하고 처리하기 위해 [Sling 매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)을 구성할 수도 있습니다. AEM Archetype 프로젝트는 포트 4503(게시) 및 80(디스패처)에 대한 일부 Sling 매핑을 구성하기 위한 [예제 구성](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)도 제공합니다.

## AEM Dispatcher와 결합 {#dispatcher}

`mod_rewrite` 모듈과 함께 AEM Dispatcher HTTP 서버를 사용하여 URL 다시 쓰기를 수행할 수도 있습니다. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)은 생성된 크기에 대한 기본 [rewrite 규칙](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)을 이미 포함하는 참조 AEM Dispatcher 구성을 제공합니다.

## 예

[Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) 프로젝트에는 제품 및 카테고리 페이지에 대한 사용자 지정 URL의 사용을 보여 주는 샘플 구성이 포함되어 있습니다. 이렇게 하면 각 프로젝트에서 SEO 요구 사항에 따라 제품 및 카테고리 페이지에 대한 개별 URL 패턴을 설정할 수 있습니다. 위에 설명된 대로 CIF `UrlProvider` 및 Sling 매핑의 조합이 사용됩니다.

>[!NOTE]
>
>이 구성은 프로젝트에서 사용하는 외부 도메인으로 조정해야 합니다. Sling 매핑은 호스트 이름 및 도메인을 기반으로 작동합니다. 따라서 이 구성은 기본적으로 비활성화되어 있으므로 배포 전에 활성화해야 합니다. 이렇게 하려면 사용된 도메인 이름에 따라 `ui.content/src/main/content/jcr_root/etc/map.publish/https`에 있는 Sling 매핑 `hostname.adobeaemcloud.com` 폴더의 이름을 변경하고, `resource.resolver.map.location="/etc/map.publish"` 를 프로젝트의 `JcrResourceResolver` 구성에 추가하여 이 구성을 활성화합니다.

## 추가 리소스

* [Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
* [AEM 리소스 매핑](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling 매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
