---
title: 통합 문제 해결
seo-title: 통합 문제 해결
description: 통합 문제를 해결하는 방법을 알아봅니다.
seo-description: 통합 문제를 해결하는 방법을 알아봅니다.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 2%

---

# 통합 문제 해결{#troubleshooting-integration-issues}

## 일반 문제 해결 팁 {#general-troubleshooting-tips}

### JavaScript 오류 {#ensure-there-are-no-javascript-errors}가 없는지 확인합니다

브라우저의 JavaScript 콘솔에 오류가 표시되는지 확인합니다. 처리되지 않은 오류로 인해 후속 코드가 제대로 실행되지 않을 수 있습니다. 오류가 있는 경우 오류를 일으키는 스크립트 및 어떤 영역을 확인하십시오. 스크립트 경로는 스크립트가 속하는 기능을 나타낼 수 있습니다.

### 구성 요소 수준 {#logging-on-component-level}에 로그인하는 중

경우에 따라 구성 요소 수준에서 추가 구문을 추가하는 것이 도움이 될 수 있습니다. 구성 요소가 렌더링되므로 잠재적인 문제를 식별하는 데 도움이 되는 변수 값을 표시하는 임시 마크업을 추가할 수 있습니다. 예:

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

로깅에 대한 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md) 및 [감사 레코드 및 로그 파일 작업](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 페이지를 참조하십시오.

## Analytics 통합 문제 {#analytics-integration-issues}

### 보고서 가져오기로 인해 CPU/메모리 사용량이 많습니다. {#the-report-importer-causes-high-cpu-memory-usage}

보고서 가져오기 프로그램으로 인해 CPU/메모리 사용량이 높거나 `OutOfMemoryError` 예외가 발생합니다.

#### 솔루션 {#solution}

이 문제를 해결하려면 다음을 수행하십시오.

* 등록된 많은 수의 PollingImporter가 없는지 확인합니다(아래 &quot;PollingImporter로 인해 시스템 종료가 오래 걸립니다&quot; 섹션 참조).
* [OSGi 콘솔](/help/sites-deploying/configuring-osgi.md)에서 `ManagedPollingImporter` 구성에 대한 CRON 표현식을 사용하여 특정 시간에 보고서 가져오기 프로그램을 실행합니다.

AEM에서 사용자 지정 데이터 가져오기 서비스를 만드는 방법에 대한 자세한 내용은 다음 문서 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html)를 참조하십시오.

### PollingImporter {#shutdown-takes-a-long-time-due-to-the-pollingimporter}(으)로 인해 종료에 시간이 오래 걸립니다.

Analytics는 상속 메커니즘을 염두에 두고 디자인되었습니다. 일반적으로 페이지 속성 [Cloud Services](/help/sites-developing/extending-cloud-config.md) 탭 내에서 Analytics 구성에 참조를 추가하여 사이트에 대한 Analytics를 활성화합니다. 그런 다음 페이지에 다른 구성이 필요하지 않은 경우 구성을 다시 참조할 필요 없이 자동으로 모든 하위 페이지에 상속됩니다. 사이트에 참조를 추가하면 몇 개의 노드(AEM 6.3 및 이전 버전의 경우 12 또는 AEM 6.4의 경우 6)가 자동으로 생성됩니다   및 이후)입니다. `cq;PollConfig` 그 결과:

* Analytics를 참조하는 페이지가 많으면 PollingImporter가 많습니다.
* 또한 Analytics 구성을 참조하여 페이지를 복사하고 붙여넣으면 해당 PollingImporter가 중복됩니다.

#### 솔루션 {#solution-1}

먼저 [error.log](/help/sites-deploying/configure-logging.md)를 분석하면 활성 또는 등록된 PollingImporter의 양에 대한 통찰력을 얻을 수 있습니다. 예:

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

둘째, 상위 페이지(계층 구조에서 높음)만 Analytics 구성을 참조하는지 확인합니다.

AEM에서 사용자 지정 데이터 가져오기 서비스를 만드는 방법에 대한 자세한 내용은 다음 문서 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html)를 참조하십시오.

## DTM(기존) 문제 {#dtm-legacy-issues}

### DTM 스크립트 태그가 페이지 소스 {#the-dtm-script-tag-is-not-rendered-in-the-page-source}에 렌더링되지 않습니다.

페이지 속성 [Cloud Services](/help/sites-developing/extending-cloud-config.md) 탭에서 구성이 참조되었더라도 [DTM](/help/sites-administering/dtm.md) 스크립트 태그가 페이지에 제대로 포함되지 않습니다.

#### 솔루션 {#solution-2}

문제를 해결하려면 다음을 시도해 볼 수 있습니다.

* 암호화된 속성의 암호를 해독할 수 있는지 확인합니다(암호화는 각 AEM 인스턴스에서 자동으로 생성된 다른 키를 사용할 수 있습니다). 자세한 내용은 [구성 속성에 대한 암호화 지원](/help/sites-administering/encryption-support-for-configuration-properties.md)을 참조하십시오.
* `/etc/cloudservices/dynamictagmanagement`에 있는 구성을 다시 게시합니다.
* `/etc/cloudservices`의 ACL을 확인합니다. ACL은 다음과 같습니다.

   * 허용;jcr:read;webservice-support-servicelibfinder
   * 허용;jcr:read;모두rep:glob:&amp;ast;/defaults/&amp;ast;
   * 허용;jcr:read;모두rep:glob:&amp;ast;/defaults
   * 허용;jcr:read;모두rep:glob:&amp;ast;/public/&amp;ast;
   * 허용;jcr:read;모두rep:glob:&amp;ast;/public

ACL 관리에 대한 자세한 내용은 [사용자 관리 및 보안](/help/sites-administering/security.md#permissions-in-aem) 페이지를 참조하십시오.

## Target 통합 문제 {#target-integration-issues}

### 사용자 지정 페이지 구성 요소 {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components} 를 사용할 때 미리 보기 모드에 타깃팅된 컨텐츠가 표시되지 않습니다

이 문제는 사용자 지정 페이지 구성 요소에 Target DTM 통합을 처리하는 올바른 JSP 또는 클라이언트 라이브러리가 포함되지 않기 때문에 발생합니다.

#### 솔루션 {#solution-3}

다음 솔루션을 사용해 볼 수 있습니다.

* 사용자 지정 `headlibs.jsp`(`/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`)에 다음이 포함되어 있는지 확인하십시오.

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* 사용자 지정 `head.html`(`/apps/<CUSTOM-COMPONENTS-PATH>/head.html` 있는 경우) **이 아래 예와 같이 특정 통합 헤더를 선택적으로 포함하지 않는지 확인합니다.**

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

`servicelibs.jsp`은 필요한 Analytics JavaScript 개체를 추가하고 웹 사이트와 연결된 클라우드 서비스 라이브러리를 로드합니다. Target 서비스의 경우 라이브러리는 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`을 통해 로드됩니다

로드된 라이브러리 집합은 Target 구성에 사용되는 대상 클라이언트 라이브러리( `mbox.js` 또는 `at.js`)의 유형에 따라 다릅니다.

DTM을 사용하여 `mbox.js` 또는 `at.js`을 제공할 때 컨텐츠가 렌더링되기 전에 라이브러리가 로드되었는지 확인합니다. 이러한 라이브러리를 비동기식으로 로드하는 태그 관리 시스템을 사용하면 Target용 JavaScript 코드를 실행할 때 문제가 발생할 수 있습니다.

자세한 내용은 [타깃팅된 컨텐츠를 위한 개발](/help/sites-developing/target.md#understanding-the-target-component) 페이지를 참조하십시오.

### AppMeasurement 초기화에 보고서 세트 ID 누락 오류가 브라우저 콘솔 {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}에 표시됩니다

이 문제는 DTM을 사용하여 웹 사이트에서 Adobe Analytics이 구현되고 사용자 지정 코드를 사용할 때 나타날 수 있습니다. 원인은 `s = new AppMeasurement()`을 사용하여 `s` 개체를 인스턴스화합니다.

#### 솔루션 {#solution-4}

`new AppMeasurement` 인스턴스화 메서드 대신 `s_gi`을 사용하십시오. 예:

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 기본 오퍼가 올바른 오퍼 {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer} 대신 임의로 표시됩니다

이 문제에는 다음과 같은 여러 원인이 있을 수 있습니다.

* 타사 태그 관리 시스템을 사용하여 비동기적으로 Target 클라이언트 라이브러리( `mbox.js` 또는 `at.js`)를 로드하면 타깃팅이 임의로 중단될 수 있습니다. Target 라이브러리는 페이지 헤드에서 동기식으로 로드되어야 합니다. AEM에서 라이브러리가 전달되면 항상 true입니다.

* DTM을 사용하는 라이브러리 및 AEM에서 Target 구성을 사용하는 라이브러리 등 두 개의 Target 클라이언트 라이브러리( `at.js`)를 동시에 로드합니다. 따라서 `at.js` 버전이 다른 경우 `adobe.target` 정의에 충돌이 발생할 수 있습니다.

#### 솔루션 {#solution-5}

다음 솔루션을 사용해 볼 수 있습니다.

* DTM과 유사한 라이브러리를 로드하는 고객 코드(이 라이브러리를 차례로 로드함)가 [페이지 헤드](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages)에서 동기식으로 실행되는지 확인합니다.
* 사이트가 DTM을 사용하여 Target 라이브러리를 전달하도록 구성된 경우 DTM **에 의해 전달된** Clientlib 옵션이 사이트에 대한 [Target 구성](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html)에서 선택되어 있는지 확인합니다.

### AT.js 1.3+ {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js} 를 사용할 때에는 항상 올바른 오퍼 대신 기본 오퍼가 표시됩니다

기본적으로 AEM 6.2 및 6.3은 AT.js 버전 1.3.0+와 호환되지 않습니다. API에 대한 매개 변수 유효성 검사를 도입하는 AT.js 버전 1.3.0에서 `adobe.target.applyOffer()`에는 `atjs-itegration.js` 코드에서 제공하지 않는 &quot;mbox&quot; 매개 변수가 필요합니다.

#### 솔루션 {#solution-6}

이 문제를 해결하려면 `atjs-itegration.js` 을 편집하고 `adobe.target.applyOffer()`의 매개 변수 개체에 `"mbox": mboxName` 필드를 다음과 같이 추가합니다.

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### 목표 및 설정 페이지에 보고 소스 섹션 {#the-goals-settings-page-does-not-show-the-reporting-sources-section}이 표시되지 않습니다

이 문제는 [A4T Analytics Cloud 구성](/help/sites-administering/target-configuring.md) 프로비저닝 문제일 수 있습니다.

#### 솔루션 {#solution-7}

AEM에 다음 확인 요청을 실행하여 Target 계정에 대해 A4T가 제대로 활성화되었는지 확인해야 합니다.

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

응답에 `a4tEnabled:false` 줄이 포함되어 있는 경우 [고객 지원 센터 Adobe](https://helpx.adobe.com/contact.html)에 문의하여 계정이 올바르게 프로비저닝되도록 하십시오.

### 유용한 Target API {#helpful-target-apis}

아래에 나와 있는 두 가지 Target API는 Target 문제를 해결할 때 유용할 수 있습니다.

* 지정된 clientcode에 대한 Target 끝점을 검색합니다

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* 클라이언트의 프로필 검색

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
