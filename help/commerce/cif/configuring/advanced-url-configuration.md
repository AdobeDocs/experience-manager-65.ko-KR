---
title: 고급 URL 구성
description: 제품 및 카테고리 페이지의 URL을 사용자 지정하는 방법을 알아봅니다. 이를 통해 구현은 검색 엔진에 대한 URL을 최적화하고 검색을 승격할 수 있습니다.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: 014731aa9c5c4d7d419ff8b037142b47e7b7da01
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 4%

---

# 고급 URL 구성 {#url}

>[!NOTE]
>
> SEO(검색 엔진 최적화)는 많은 마케터의 주요 관심사가 되었습니다. 따라서 많은 AEM 프로젝트에서 SEO 문제를 해결해야 합니다. 자세한 내용 [SEO 및 URL 관리 우수 사례](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) 추가 정보.

[AEM CIF 코어 구성 요소](https://github.com/adobe/aem-core-cif-components) 제품 및 카테고리 페이지의 URL을 사용자 지정하는 고급 구성을 제공합니다. 많은 구현이 SEO(검색 엔진 최적화) 목적으로 이러한 URL을 사용자 지정합니다. 다음 비디오에서는 을 구성하는 방법을 자세히 설명합니다 `UrlProvider` 의 서비스 및 기능 [Sling 매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 제품 및 카테고리 페이지의 URL을 사용자 지정하는 방법.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 구성 {#configuration}

를 구성하려면 `UrlProvider` 서비스는 SEO 요구 사항에 따라 제공되며 프로젝트가 필요한 경우 &quot;CIF URL 공급자 구성&quot;에 대한 OSGI 구성을 제공해야 합니다.

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

의 경우 [Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 교체 `/content/venia/us/en/products/product-page`
* `{{sku}}` 은 제품의 sku(예: )로 대체됩니다. `VP09`
* `{{url_key}}` 이 제품의 `url_key` 속성(예: `lenora-crochet-shorts`
* `{{url_path}}` 이 제품의 `url_path`예: `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 은 현재 선택한 변형으로 대체됩니다(예: ). `VP09-KH-S`

다음 이후 `url_path` 가 더 이상 사용되지 않는 경우, 사전 정의된 제품 URL 형식은 제품의 `url_rewrites` 및 를 선택하는 경우 경로 세그먼트가 가장 큰 세그먼트를 대체 항목으로 선택합니다 `url_path` 을(를) 사용할 수 없습니다.

위의 예제 데이터를 사용하면 기본 URL 형식을 사용하여 형식이 지정된 제품 변형 URL은 다음과 같습니다 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 카테고리 페이지 URL 형식 {#product-list}

카테고리 또는 제품 목록 페이지의 URL을 구성하고 다음 옵션을 지원합니다.

* `{{page}}.html/{{url_path}}.html` (기본값)
* `{{page}}.html/{{url_key}}.html`

의 경우 [Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 교체 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 은(는) 카테고리의 `url_key` 속성
* `{{url_path}}` 은(는) 카테고리의 `url_path`

위의 예제 데이터를 사용하면 기본 URL 형식을 사용하여 형식이 지정된 카테고리 페이지 URL은 다음과 같습니다 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> 다음 `url_path` 는 `url_keys` 제품 또는 카테고리의 상위 항목 및 제품 또는 카테고리의 `url_key` 분리 `/` 슬래시.

### 특정 카테고리-/제품 페이지 {#specific-pages}

만들 수 있습니다 [여러 카테고리 및 제품 페이지](multi-template-usage.md) 를 참조하십시오.

다음 `UrlProvider` 작성자 계층 인스턴스의 해당 페이지에 대한 딥 링크를 생성하도록 사전 구성되어 있습니다. 이 기능은 미리 보기 모드를 사용하여 사이트를 탐색하고, 특정 제품 또는 카테고리 페이지로 이동한 다음, 편집 모드로 전환하여 페이지를 편집하는 편집자에게 유용합니다.

반면 게시 계층 인스턴스에서는 카탈로그 페이지 URL을 안정적으로 유지하여 검색 엔진 순위가 더 이상 떨어지지 않도록 해야 합니다. 이러한 게시 계층 인스턴스로 인해 기본적으로 특정 카탈로그 페이지에 대한 딥 링크가 렌더링되지 않습니다. 이 동작을 변경하려면 _CIF URL 공급자 특정 페이지 전략_ 항상 특정 페이지 url을 생성하도록 구성할 수 있습니다.

## 사용자 지정 URL 형식 {#custom-url-format}

사용자 지정 URL 형식을 제공하려면 프로젝트가 다음을 구현할 수 있습니다 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 또는 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 서비스 인터페이스를 사용하여 구현을 OSGI 서비스로 등록합니다. 이러한 구현은 사용 가능한 경우 구성된 사전 정의된 형식을 대체합니다. 등록된 여러 개의 구현이 있는 경우 서비스 등급이 높은 구현은 해당 구현이 낮은 서비스 등급을 대체합니다.

사용자 지정 URL 형식 구현은 지정된 매개 변수에서 URL을 빌드하고 URL을 구문 분석하여 각각 동일한 매개 변수를 반환하는 한 쌍의 메서드를 구현해야 합니다.

## Sling 매핑과 결합 {#sling-mapping}

추가 `UrlProvider`를 설정하는 것도 가능합니다 [Sling 매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 를 재작성하고 처리하기 위해 입니다. AEM Archetype 프로젝트에서도 사용할 수 있습니다 [구성 예](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 포트 4503(게시) 및 80(dispatcher)에 대한 일부 Sling 매핑을 구성하려면 다음을 수행하십시오.

## AEM Dispatcher와 결합 {#dispatcher}

또한 URL 다시 쓰기는 AEM Dispatcher HTTP 서버를 `mod_rewrite` 모듈. 다음 [AEM 프로젝트 원형](https://github.com/adobe/aem-project-archetype) 에서는 이미 기본 항목이 포함된 참조 AEM Dispatcher 구성을 제공합니다 [rewrite 규칙](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 생성되었습니다.

## 예

다음 [Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia) 프로젝트에는 제품 및 카테고리 페이지에 대한 사용자 지정 URL의 사용을 보여주는 샘플 구성이 포함되어 있습니다. 이렇게 하면 각 프로젝트에서 SEO 요구 사항에 따라 제품 및 카테고리 페이지에 대한 개별 URL 패턴을 설정할 수 있습니다. CIF의 조합 `UrlProvider` 및 위에 설명된 Sling 매핑이 사용됩니다.

>[!NOTE]
>
>이 구성은 프로젝트에서 사용하는 외부 도메인으로 조정해야 합니다. Sling 매핑은 호스트 이름 및 도메인을 기반으로 작동합니다. 따라서 이 구성은 기본적으로 비활성화되어 있으므로 배포 전에 활성화해야 합니다. 이렇게 하려면 Sling 매핑의 이름을 변경합니다 `hostname.adobeaemcloud.com` 폴더 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 사용된 도메인 이름에 따라 다음을 추가하여 이 구성을 활성화하십시오. `resource.resolver.map.location="/etc/map.publish"` 변환 후 `JcrResourceResolver` 프로젝트에 대한 구성.

## 추가 리소스

* [Venia 참조 저장소](https://github.com/adobe/aem-cif-guides-venia)
* [AEM 리소스 매핑](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling 매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
