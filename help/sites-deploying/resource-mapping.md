---
title: 리소스 매핑
seo-title: Resource Mapping
description: 리소스 매핑을 사용하여 AEM용 리디렉션, 별칭 URL 및 가상 호스트를 정의하는 방법을 알아봅니다.
seo-description: Learn how to define redirects, vanity URLs and virtual hosts for AEM by using resource mapping.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
source-git-commit: 7c24379c01f247f5ad45e3ecd40f3edef4ac3cfb
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 3%

---

# 리소스 매핑{#resource-mapping}

리소스 매핑은 AEM에 대한 리디렉션, 별칭 URL 및 가상 호스트를 정의하는 데 사용됩니다.

예를 들어 다음 매핑을 사용하여 다음을 수행할 수 있습니다.

* 모든 요청에 접두사 지정 `/content` 방문자가 웹 사이트를 방문하지 못하도록 내부 구조가 숨겨져 있습니다.
* 에 대한 모든 요청이 가능하도록 리디렉션 정의 `/content/en/gateway` 웹 사이트의 페이지가 `https://gbiv.com/`.

모든 요청의 HTTP 매핑 접두사를 한 개만 매핑할 수 있습니다 `localhost:4503` with `/content`. 다음과 같은 매핑을 사용하여 방문자가 웹 사이트를 방문하도록 내부 구조를 숨길 수 있습니다.

`localhost:4503/content/we-retail/en/products.html`

를 사용하여 액세스하려면

`localhost:4503/we-retail/en/products.html`

매핑은 자동으로 접두사를 추가합니다 `/content` to `/we-retail/en/products.html`.

>[!CAUTION]
>
>별칭 URL은 정규 표현식 패턴을 지원하지 않습니다.

>[!NOTE]
>
>Sling 설명서 및 [리소스 확인을 위한 매핑](https://sling.apache.org/site/resources.html) 및 [리소스](https://sling.apache.org/site/mappings-for-resource-resolution.html) 추가 정보.

## 매핑 정의 보기 {#viewing-mapping-definitions}

매핑은 JCR Resource Resolver가 평가하고(하향식) 일치하는 항목을 찾는 두 개의 목록에서 가져옵니다.

이러한 목록은 **JCR ResourceResolver** Felix 콘솔의 옵션; 예 `https://<*host*>:<*port*>/system/console/jcrresolver`:

* 구성 (에 대해 정의된 대로) 현재 구성을 표시합니다 [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* 구성 테스트 URL 또는 리소스 경로를 입력할 수 있습니다. 클릭 **해결** 또는 **맵** 시스템이 항목을 변형하는 방법을 확인하려면

* **확인자 맵 항목**
ResourceResolver.resolver 메서드에서 URL을 리소스에 매핑하는 데 사용하는 항목 목록입니다.

* **맵 항목 매핑**
리소스 경로를 URL에 매핑하기 위해 ResourceResolver.map 메서드에서 사용하는 항목 목록입니다.

두 목록에는 응용 프로그램에 의해 기본값으로 정의된 항목을 포함하여 다양한 항목이 표시됩니다. 이러한 목표는 종종 사용자의 URL을 단순화하는 것입니다.

이 목록은 **패턴**&#x200B;와 일치하고 요청에 일치하는 정규 표현식을 **교체** 지정할 리디렉션을 정의합니다.

예를 들어,

**패턴** `^[^/]+/[^/]+/welcome$`

은(는) 다음을 트리거합니다.

**대체** `/libs/cq/core/content/welcome.html`.

요청을 리디렉션하려면:

`https://localhost:4503/welcome` ``

끝:

`https://localhost:4503/libs/cq/core/content/welcome.html`

저장소 내에 새 매핑 정의가 만들어집니다.

>[!NOTE]
>
>정규 표현식을 정의하는 방법을 설명하는 데 도움이 되는 사용 가능한 리소스는 많습니다. 예 [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### AEM에서 매핑 정의 생성 {#creating-mapping-definitions-in-aem}

표준 AEM 설치에서 폴더를 찾을 수 있습니다.

`/etc/map/http`

HTTP 프로토콜에 대한 매핑을 정의할 때 사용되는 구조입니다. 기타 폴더( `sling:Folder`)는에서 만들 수 있습니다. `/etc/map` 매핑할 기타 프로토콜에 대해 설명합니다.

#### /content로 내부 리디렉션 구성 {#configuring-an-internal-redirect-to-content}

모든 요청의 접두사를 https://localhost:4503/에 게시하는 매핑을 생성하려면 `/content`:

1. CRXDE를 사용하면 다음 위치로 이동합니다. `/etc/map/http`.

1. 새 노드를 만듭니다.

   * **유형** `sling:Mapping`
이 노드 유형은 필수가 아니지만 매핑에 사용됩니다.

   * **이름** `localhost_any`

1. 클릭 **모두 저장**.
1. **추가** 이 노드에 대한 다음 속성:

   * **이름** `sling:match`

      * **유형** `String`

      * **값** `localhost.4503/`
   * **이름** `sling:internalRedirect`

      * **유형** `String[]`

      * **값** `/content/`


1. 클릭 **모두 저장**.

이렇게 하면 다음과 같은 요청이 처리됩니다.
`localhost:4503/geometrixx/en/products.html`
로서의
`localhost:4503/content/geometrixx/en/products.html`
이 요청되었습니다.

>[!NOTE]
>
>자세한 내용은 [리소스](https://sling.apache.org/site/mappings-for-resource-resolution.html) sling 설명서에서 사용 가능한 sling 속성 및 이 속성을 구성하는 방법에 대한 자세한 내용을 참조하십시오.

>[!NOTE]
>
>다음을 사용할 수 있습니다 `/etc/map.publish` 을 눌러 게시 환경에 대한 구성을 저장합니다. 그런 다음 이 파일을 복제하고 새 위치( `/etc/map.publish`)에 대해 구성된 **매핑 위치** 의 [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) 게시 환경의 일부입니다.
