---
title: 클라우드 서비스 구성
seo-title: 클라우드 서비스 구성
description: 기존 인스턴스를 확장하여 고유한 구성을 만들 수 있습니다
seo-description: 기존 인스턴스를 확장하여 고유한 구성을 만들 수 있습니다
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 4%

---

# 클라우드 서비스 구성{#cloud-service-configurations}

구성은 서비스 구성을 저장하는 논리 및 구조를 제공하도록 설계되었습니다.

기존 인스턴스를 확장하여 고유한 구성을 만들 수 있습니다.

## 개념 {#concepts}

구성 개발에 사용되는 원칙은 다음 개념을 기반으로 했습니다.

* 서비스/어댑터는 구성을 검색하는 데 사용됩니다.
* 구성(예: 속성/단락)은 상위 항목에서 상속됩니다.
* 경로별로 analytics 노드에서 참조됩니다.
* 쉽게 확장할 수 있습니다.
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)과 같은 더 복잡한 구성을 처리할 수 있는 유연성을 제공합니다.
* 종속성 지원(예:[Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 플러그인에는 [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) 구성이 필요합니다.

## 구조 {#structure}

구성의 기본 경로는 다음과 같습니다.

`/etc/cloudservices`.

각 구성 유형에 대해 템플릿과 구성 요소가 제공됩니다.이렇게 하면 사용자 지정된 후 대부분의 요구 사항을 충족할 수 있는 구성 템플릿이 있을 수 있습니다.

새 서비스에 대한 구성을 제공하려면 다음을 수행해야 합니다.

* 에서 서비스 페이지 만들기

   `/etc/cloudservices`

* 아래와 같이 변경하는 것을 의미합니다.

   * 구성 템플릿
   * 구성 구성 요소

템플릿과 구성 요소는 기본 템플릿에서 `sling:resourceSuperType`을 상속해야 합니다.

`cq/cloudserviceconfigs/templates/configpage`

또는 기본 구성 요소 각각

`cq/cloudserviceconfigs/components/configpage`

서비스 공급자는 서비스 페이지도 제공해야 합니다.

`/etc/cloudservices/<service-name>`

### 템플릿 {#template}

템플릿이 기본 템플릿을 확장합니다.

`cq/cloudserviceconfigs/templates/configpage`

및 은 사용자 지정 구성 요소를 가리키는 `resourceType` 을 정의합니다.

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### 구성 요소 {#components}

구성 요소는 기본 구성 요소를 확장해야 합니다.

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

템플릿 및 구성 요소를 설정한 후 아래에 하위 페이지를 추가하여 구성을 추가할 수 있습니다.

`/etc/cloudservices/<service-name>`

### 컨텐츠 모델 {#content-model}

컨텐츠 모델은 다음 위치에 `cq:Page`로 저장됩니다.

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

구성은 하위 노드 `jcr:content` 아래에 저장됩니다.

* 대화 상자에 정의된 속성이 `jcr:node`에 직접 저장되어야 하는 문제를 해결했습니다.
* 동적 요소(`parsys` 또는 `iparsys` 사용)는 하위 노드를 사용하여 구성 요소 데이터를 저장합니다.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

API에 대한 참조 설명서는 [com.day.cq.wcm.webservicessupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html)을 참조하십시오.

### AEM 통합 {#aem-integration}

사용 가능한 서비스는 `foundation/components/page` 또는 `wcm/mobile/components/page`에서 상속되는 모든 페이지의 **페이지 속성** 대화 상자의 **Cloud Services** 탭에 나열됩니다.

이 탭에서는 다음 작업도 제공됩니다.

* 서비스를 활성화할 수 있는 위치에 대한 링크
* 경로 필드에서 구성(서비스의 하위 노드)을 선택합니다

#### 암호 암호화 {#password-encryption}

서비스에 대한 사용자 자격 증명을 저장할 때 모든 암호는 암호화되어야 합니다.

숨겨진 양식 필드를 추가하여 이 작업을 수행할 수 있습니다. 이 필드에는 속성 이름에 주석 `@Encrypted`이 있어야 합니다.즉, `password` 필드의 이름은 다음과 같이 작성됩니다.

`password@Encrypted`

그러면 속성이 `EncryptionPostProcessor`에 의해 자동으로 암호화됩니다( `CryptoSupport` 서비스 사용).

>[!NOTE]
>
>이는 표준 ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` 주석과 유사합니다.

>[!NOTE]
>
>기본적으로 `EcryptionPostProcessor`은 `/etc/cloudservices`에 대한 `POST` 요청만 암호화합니다.

#### 서비스 페이지 jcr:content 노드 {#additional-properties-for-service-page-jcr-content-nodes}에 대한 추가 속성

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>페이지에 자동으로 포함할 구성 요소에 대한 참조 경로입니다.<br /> 추가 기능 및 JS 포함에 사용됩니다.<br /> 여기에는 포함된 페이지의 구성 <br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> 요소(일반적으로  <code>body</code> 태그 앞)가 포함됩니다.<br /> Analytics 및 Target의 경우 방문자 행동을 추적하기 위한 JavaScript 호출과 같은 추가 기능을 포함하도록 이 기능을 사용합니다.</td>
  </tr>
  <tr>
   <td>설명</td>
   <td>서비스에 대한 간략한 설명입니다.<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>서비스에 대한 확장된 설명입니다.</td>
  </tr>
  <tr>
   <td>등급</td>
   <td>목록에 사용할 서비스 등급입니다.</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>페이지 속성 대화 상자에 구성을 표시하기 위한 필터입니다.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>서비스 웹 사이트의 URL.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>서비스 URL에 대한 레이블입니다.</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>서비스에 대한 축소판 그림 경로.</td>
  </tr>
  <tr>
   <td>표시</td>
   <td>페이지 속성 대화 상자의 가시성기본적으로 표시(선택 사항)</td>
  </tr>
 </tbody>
</table>

### 사용 사례 {#use-cases}

이러한 서비스는 기본적으로 제공됩니다.

* [추적기 코드 조각](/help/sites-administering/external-providers.md) (Google, WebTrends 등)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
* [Search&amp;Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote)
* [다이내믹 미디어](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>[사용자 지정 Cloud Service 만들기](/help/sites-developing/extending-cloud-config-custom-cloud.md)도 참조하십시오.
