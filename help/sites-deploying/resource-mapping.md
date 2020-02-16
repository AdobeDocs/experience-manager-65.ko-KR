---
title: 리소스 매핑
seo-title: 리소스 매핑
description: 리소스 매핑을 사용하여 AEM용 리디렉션, 별칭 URL 및 가상 호스트를 정의하는 방법에 대해 알아봅니다.
seo-description: 리소스 매핑을 사용하여 AEM용 리디렉션, 별칭 URL 및 가상 호스트를 정의하는 방법에 대해 알아봅니다.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 리소스 매핑{#resource-mapping}

리소스 매핑은 AEM에 대한 리디렉션, 별칭 URL 및 가상 호스트를 정의하는 데 사용됩니다.

예를 들어 다음과 같은 매핑을 사용할 수 있습니다.

* 웹 사이트 방문자가 내부 구조를 숨길수 `/content` 있도록 모든 요청에 접두사를 붙입니다.
* 웹 사이트의 `/content/en/gateway` 페이지에 대한 모든 요청이 리디렉션되도록 리디렉션을 `https://gbiv.com/`정의합니다.

하나의 가능한 HTTP 매핑은 모든 요청에 대해 접두사를 `localhost:4503` 부여합니다 `/content`. 이와 같은 매핑을 사용하여 웹 사이트 방문자로부터 내부 구조를 숨길 수 있습니다.

`localhost:4503/content/we-retail/en/products.html`

을 사용하여 액세스하십시오.

`localhost:4503/we-retail/en/products.html`

를 매핑하면 접두사가 자동으로 `/content` 추가됩니다 `/we-retail/en/products.html`.

>[!CAUTION]
>
>별칭 URL은 정규식 패턴을 지원하지 않습니다.

>[!NOTE]
>
>자세한 내용은 Sling 설명서 및 리소스 [해상도](https://sling.apache.org/site/resources.html) 및 리소스에 [대한](https://sling.apache.org/site/mappings-for-resource-resolution.html) 매핑을참조하십시오.

## 매핑 정의 보기 {#viewing-mapping-definitions}

매핑은 JCR 리소스 확인자가 일치된 항목을 찾기 위해 평가한 두 개의 목록(하향식)에서 이루어집니다.

이러한 목록은 Felix 콘솔의 JCR ResourceResolver **옵션 아래에서 구성** 정보와 함께 볼 수 있습니다.예를 들면 다음과 같습니다 `https://<*host*>:<*port*>/system/console/jcrresolver`.

* 구성현재 구성을 표시합니다(Apache Sling 리소스 [해결 프로그램에 대해 정의됨](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* 구성 테스트URL 또는 리소스 경로를 입력할 수 있습니다. 확인 **또는** **맵을** 클릭하여 시스템이 항목을 어떻게 변형하는지 확인합니다.

* **해결 프로그램 맵**&#x200B;항목 ResourceResolver에서 사용하는 항목 목록입니다. resolve 메서드는 URL을 리소스에 매핑합니다.

* **매핑 맵**&#x200B;항목ResourceResolver.map 메서드에서 리소스 경로를 URL에 매핑하는 데 사용되는 항목 목록입니다.

이 두 목록은 애플리케이션에서 기본값으로 정의된 항목을 비롯하여 다양한 항목을 보여줍니다. 이러한 URL은 사용자의 URL을 단순화하기 위한 목적으로 사용됩니다.

목록은 요청에 **대응한**&#x200B;정규 표현식인 Pattern과 적용할 리디렉션을 **정의하는** Replacement를 함께 제공합니다.

예를 들면 다음과 같습니다.

**패턴**`^[^/]+/[^/]+/welcome$`

는 다음을 트리거합니다.

**대체** `/libs/cq/core/content/welcome.html`.

요청을 리디렉션하려면:

`https://localhost:4503/welcome` ``

끝:

`https://localhost:4503/libs/cq/core/content/welcome.html`

저장소 내에 새 매핑 정의가 만들어집니다.

>[!NOTE]
>
>정규 표현식을 정의하는 방법을 설명하는 데 도움이 되는 많은 리소스가 있습니다.예: [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### AEM에서 매핑 정의 만들기 {#creating-mapping-definitions-in-aem}

AEM의 표준 설치에서 폴더를 찾을 수 있습니다.

`/etc/map/http`

HTTP 프로토콜에 대한 매핑을 정의할 때 사용되는 구조입니다. 매핑할 다른 프로토콜에 대해 다른 폴더( `sling:Folder`)를 만들 `/etc/map` 수 있습니다.

#### /content로 내부 리디렉션 구성 {#configuring-an-internal-redirect-to-content}

모든 요청의 접두사를 https://localhost:4503/으로 지정하는 매핑을 만들려면 `/content`:

1. CRXDE를 사용하여 탐색합니다 `/etc/map/http`.

1. 새 노드 만들기:

   * **유형** 이 `sling:Mapping`노드 유형은 반드시 사용해야 하는 것은 아니지만 이러한 매핑을 위해 만들어졌습니다.

   * **이름** `localhost_any`

1. 모두 **저장을 클릭합니다**.
1. **이** 노드에 다음 속성을 추가합니다.

   * **이름** `sling:match`

      * **유형** `String`

      * **값**`localhost.4503/`
   * **이름** `sling:internalRedirect`

      * **유형** `String`

      * **값**`/content/`


1. 모두 **저장을 클릭합니다**.

이렇게 하면 다음과 같은 요청이 처리됩니다.`localhost:4503/geometrixx/en/products.html`as:요청되었습니다.`localhost:4503/content/geometrixx/en/products.html`

>[!NOTE]
>
>사용 [가능한](https://sling.apache.org/site/mappings-for-resource-resolution.html) 슬링 속성과 이러한 속성을 구성할 수 있는 방법에 대한 자세한 내용은 Sling 설명서의 리소스를 참조하십시오.

>[!NOTE]
>
>을 사용하여 게시 `/etc/map.publish` 환경에 대한 구성을 저장할 수 있습니다. 그런 다음 이러한 항목을 복제해야 하며, 게시 환경의 Apache Sling `/etc/map.publish`리소스 **해결 프로그램의** 매핑 [위치에 대해 구성된 새 위치](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) ()를복제해야 합니다.

