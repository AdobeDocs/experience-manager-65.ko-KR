---
title: 리소스 매핑
description: 리소스 매핑을 사용하여 Adobe Experience Manager에 대한 리디렉션, vanity URL 및 가상 호스트를 정의하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 3eebdd38-da5b-4c38-868a-22c3c7a97b66
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 2%

---

# 리소스 매핑{#resource-mapping}

리소스 매핑은 AEM(Adobe Experience Manager)의 리디렉션, vanity URL 및 가상 호스트를 정의하는 데 사용됩니다.

예를 들어 이러한 매핑을 사용하여 다음을 수행할 수 있습니다.

* 웹 사이트 방문자에게 내부 구조를 숨기도록 모든 요청에 `/content`을(를) 접두사로 사용합니다.
* 웹 사이트의 `/content/en/gateway` 페이지에 대한 모든 요청이 `https://gbiv.com/`(으)로 리디렉션되도록 리디렉션을 정의합니다.

가능한 HTTP 매핑 접두사는 `/content`을(를) 사용하여 `localhost:4503`에 대한 모든 요청을 접두사로 추가합니다. 이와 같은 매핑은 웹 사이트 방문자가 허용하는 대로 내부 구조를 숨기는 데 사용할 수 있습니다.

`localhost:4503/content/we-retail/en/products.html`

다음을 사용하여 액세스:

`localhost:4503/we-retail/en/products.html`

매핑이 접두사 `/content`을(를) `/we-retail/en/products.html`에 자동으로 추가하므로

>[!CAUTION]
>
>별칭 URL은 정규 표현식 패턴을 지원하지 않습니다.

>[!NOTE]
>
>자세한 내용은 Sling 설명서 및 [리소스 확인을 위한 매핑](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 및 [리소스](https://sling.apache.org/documentation/the-sling-engine/resources.html)을 참조하십시오.

## 매핑 정의 보기 {#viewing-mapping-definitions}

매핑은 JCR Resource Resolver가 일치 항목을 찾기 위해 평가(하향식)하는 두 개의 목록을 형성합니다.

이러한 목록은 Felix 콘솔의 **JCR ResourceResolver** 옵션(예: `https://<*host*>:<*port*>/system/console/jcrresolver`)에서 구성 정보와 함께 볼 수 있습니다.

* 구성
[Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)에 대해 정의된 대로 현재 구성을 표시합니다.

* 구성 테스트
URL 또는 리소스 경로를 입력할 수 있습니다. **확인** 또는 **맵**&#x200B;을 클릭하여 시스템에서 항목을 변환하는 방법을 확인합니다.

* **해결 프로그램 맵 항목**
URL을 리소스에 매핑하기 위해 ResourceResolver.resolve 메서드에서 사용하는 항목 목록입니다.

* **맵 항목 매핑**
리소스 경로를 URL에 매핑하기 위해 ResourceResolver.map 메서드에서 사용하는 항목 목록입니다.

두 목록에는 응용 프로그램에서 기본값으로 정의한 항목을 포함하여 다양한 항목이 표시됩니다. 이는 종종 사용자의 URL을 단순화하는 것을 목표로 합니다.

이 목록은 요청에 일치하는 정규 표현식인 **Pattern**&#x200B;과(와) 적용할 리디렉션을 정의하는 **Replacement**&#x200B;을(를) 연결합니다.

예를 들어,

**패턴** `^[^/]+/[^/]+/welcome$`

이(가) 다음을 트리거합니다.

**바꾸기** `/libs/cq/core/content/welcome.html`.

요청을 리디렉션하려면:

`https://localhost:4503/welcome` &quot;

끝:

`https://localhost:4503/libs/cq/core/content/welcome.html`

저장소 내에 새 매핑 정의가 만들어집니다.

>[!NOTE]
>
>정규 표현식을 정의하는 방법을 설명하는 데 도움이 되는 다양한 리소스가 있습니다. 예: [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### AEM에서 매핑 정의 생성 {#creating-mapping-definitions-in-aem}

AEM의 표준 설치에서 폴더를 찾을 수 있습니다.

`/etc/map/http`

HTTP 프로토콜에 대한 매핑을 정의할 때 사용되는 구조입니다. 매핑할 다른 프로토콜에 대해 `/etc/map`에 다른 폴더(`sling:Folder`)를 만들 수 있습니다.

#### /content로 내부 리디렉션 구성 {#configuring-an-internal-redirect-to-content}

`/content`을(를) 사용하여 https://localhost:4503/에 대한 요청 접두사를 사용하는 매핑을 만들려면 다음을 수행하십시오.

1. CRXDE를 사용하여 `/etc/map/http`(으)로 이동합니다.

1. 노드 만들기:

   * **유형** `sling:Mapping`
이 노드 유형은 그러한 매핑에 사용되지만 반드시 사용해야 하는 것은 아닙니다.

   * **이름** `localhost_any`

1. **모두 저장**&#x200B;을 클릭합니다.
1. **다음 속성을 이 노드에 추가**&#x200B;합니다.

   * **이름** `sling:match`

      * **유형** `String`

      * **값** `localhost.4503/`

   * **이름** `sling:internalRedirect`

      * **유형** `String[]`

      * **값** `/content/`

1. **모두 저장**&#x200B;을 클릭합니다.

다음과 같은 요청을 처리합니다.
`localhost:4503/geometrixx/en/products.html`
다음과 같이:
`localhost:4503/content/geometrixx/en/products.html`
이(가) 요청되었습니다.

>[!NOTE]
>
>사용 가능한 슬링 속성 및 구성 방법에 대한 자세한 내용은 슬링 설명서의 [리소스](https://sling.apache.org/documentation/the-sling-engine/resources.html)를 참조하십시오.

>[!NOTE]
>
>`/etc/map.publish`을(를) 사용하여 게시 환경에 대한 구성을 유지할 수 있습니다. 이러한 매개 변수는 복제해야 하며 게시 환경의 [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)의 **매핑 위치**&#x200B;에 대해 새 위치(`/etc/map.publish`)가 구성되었습니다.
