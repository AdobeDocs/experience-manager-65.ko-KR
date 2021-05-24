---
title: Adobe Analytics 및 Adobe Target 선택
seo-title: Adobe Analytics 및 Adobe Target 선택
description: Adobe Analytics 및 Adobe Target에 옵트인하는 방법을 알아봅니다.
seo-description: Adobe Analytics 및 Adobe Target에 옵트인하는 방법을 알아봅니다.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
exl-id: 3603e929-2aa1-4c25-ad9a-b10ff52a59f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 0%

---

# Adobe Analytics 및 Adobe Target 선택{#opting-into-adobe-analytics-and-adobe-target}

AEM에는 Adobe Analytics 및 Adobe Target과 통합하는 데 도움이 되는 옵트인 절차가 있습니다. 관리자 사용자 그룹에 할당된 미리 로드된 작업으로 즉시 사용할 수 있습니다.

관리자로 로그인하면 [받은 편지함](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks)에서 이 작업(**Analytics 및 타깃팅 구성**)을 사용할 수 있습니다. 제공한 자격 증명을 기반으로 이러한 서비스를 구성하고 통합하는 데 도움이 됩니다.

통합을 구성하기 위한 다음 옵션이 있습니다.

* 작업을 통해 통합을 구성합니다.

   이 작업은 즉시 또는 나중에 수행할 수 있으며, 일부 작업이 수행될 때까지 작업이 받은 편지함에 유지됩니다. 두 경우 모두 UI에서 직접 또는 사전 정의된 `.properties` 파일을 사용하여 구성을 수행할 수 있습니다.

* 통합을 옵트아웃합니다.

   [수동으로 통합](/help/sites-administering/marketing-cloud.md)을 구성하려면 이 옵션을 고려하십시오. DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)을 사용하여 AEM과 Adobe Target 및 Adobe Analytics 통합 을 참조하십시오.[

* 스크립트를 사용하여 설정 및 프로비전을 구성합니다.

## 통합 구성 {#configuring-the-integration}

통합 선택:

* Analytics 를 사용하여 페이지 추적 및 분석 기능을 사용할 수 있도록 합니다.
* Target 를 사용하여 개인화 기능을 사용할 수 있습니다.

두 옵션 중 하나에 대해 사용자 계정 정보를 제공하고 추적할 페이지를 지정해야 합니다.

>[!NOTE]
>
>서버 시작 시 읽히는 속성 파일을 사용하여 Analytics 및 Target 계정 정보를 선택적으로 제공할 수 있습니다. [속성 파일을 사용하여 계정 정보 제공](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file)을 참조하십시오.

통합을 선택하면 AEM에서 다음 작업을 수행합니다.

* Analytics 및 Target에 연결할 수 있도록 하는 클라우드 구성을 만듭니다.
* 추적되는 데이터를 결정하는 프레임워크를 만듭니다.
* 이 서비스를 사용하도록 웹 페이지를 구성합니다.

>[!NOTE]
>
>AT.js는 기본 클라이언트 라이브러리입니다. 이는 [target 클라우드 서비스 구성](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration) 아래에 구성되어 있습니다.
>
>Adobe은 AT.js를 클라이언트 라이브러리로 사용하는 것을 권장합니다.

사전 로드된 기본 제공 작업에서 옵트인하려면 다음을 수행하십시오.

1. [받은 편지함에서 및 **Open** Analytics &amp; Targeting](/help/sites-authoring/inbox.md#taking-action-on-an-item) 작업을 선택합니다.

   ![optin-01](assets/optin-01.png)

1. Analytics의 경우:

   1. Analytics에 대한 사용자 계정 정보를 입력한 다음 해당 **추가** 단추를 클릭합니다.
   1. 적절한 자격 증명이 인증됩니다.
   1. Analytics 계정이 인증되면 사용할 Analytics 보고서 세트를 선택합니다. AEM은 그러한 Analytics 보고서 세트를 검색합니다. 상태가 **추가됨**&#x200B;으로 업데이트됩니다.

1. Target:

   1. Target에 대한 사용자 계정 정보를 입력한 다음 해당 **추가** 단추를 클릭합니다.
   1. 적절한 자격 증명이 인증됩니다. 상태가 **추가됨**&#x200B;으로 업데이트됩니다.

1. **다음**&#x200B;을 선택합니다.
1. Analytics 및/또는 Target을 사용해야 하는 사이트를 선택합니다.

1. **완료**&#x200B;를 선택하여 완료합니다.

   >[!CAUTION]
   >
   >구성에 옵트인한 후 영향을 받는 사이트/페이지를 게시하여 이러한 변경 사항을 게시 인스턴스에 복제해야 합니다.

## 통합 선택 {#opting-out-of-the-integration}

다음 중 하나를 수행할 때 Analytics 및 Target와의 통합을 옵트아웃합니다.

* 이러한 제품과 통합하지 않으려는 경우
* 통합을 수동으로 구성하는 것이 좋습니다.

   수동 통합 구성에 대한 내용은 [Adobe Analytics과 통합](/help/sites-administering/adobeanalytics.md) 및 [Adobe Target과 통합](/help/sites-administering/target.md)을 참조하십시오.

옵트아웃하려면 사전 로드된 작업을 완료해야 합니다.

* [받은 편지함에서 및 **Complete** Analytics &amp; Targeting ](/help/sites-authoring/inbox.md#taking-action-on-an-item) 작업을 선택합니다.

## 속성 파일 {#providing-account-information-using-a-properties-file}을 사용하여 계정 정보 제공

서버 시작 시 AEM이 읽는 속성 파일을 설치하여 Analytics 및 Target와의 통합을 위한 계정 속성을 구성합니다. 속성 파일을 사용하면 옵트인 마법사가 파일의 속성을 자동으로 사용하고 그에 따라 클라우드 구성이 만들어집니다.

속성 파일은 AEM 프로세스가 사용하는 작업 디렉토리(일반적으로 JAR 파일과 동일한 디렉토리)에 저장하는 marketingcloud.properties라는 텍스트 파일입니다. 파일에는 다음 속성이 포함되어 있습니다.

* analytics.server:사용하는 Analytics 데이터 센터의 URL입니다.
* analytics.company:Analytics 사용자 계정과 연결된 회사입니다.
* analytics.username:Analytics 사용자 이름입니다.
* analytics.secret:Analytics 사용자 이름과 연결된 암호입니다.
* analytics.reportsuite:사용할 Analytics 보고서 세트의 이름입니다.
* target.clientcode:Target 계정과 연결된 클라이언트 코드입니다.
* target.email:Target 계정을 인증하는 데 사용하는 이메일 주소입니다.
* target.password:이메일 주소와 연결된 암호입니다.

속성과 값은 등호(=)로 구분됩니다. Analytics 속성 앞에는 `analytics` 이 붙고 Target 속성 앞에는 `target` 이 붙습니다. 서비스를 구성하려면 해당 서비스의 모든 속성에 대한 값을 제공합니다. 서비스를 구성하지 않으려면 해당 서비스에 대한 값을 제공하지 않습니다.

다음 예제 `.properties` 파일에는 Analytics에 대한 클라우드 구성을 만드는 속성 값이 포함되어 있습니다.

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

다음 절차에서는 속성 파일을 사용하여 통합을 옵트인하는 방법을 설명합니다.

1. AEM 프로세스가 사용 중인 작업 디렉토리(작성자 인스턴스)에 `marketingcloud.properties` 파일을 만듭니다.

   >[!NOTE]
   >
   >작업 디렉토리는 일반적으로 jar 또는 `license.properties` 파일을 포함하는 디렉토리입니다.
   >
   >하지만 시스템 속성에 의해 절대 경로로 정의할 수도 있습니다.
   >
   >`mac.provisioning.file.container`

1. Analytics 및/또는 Target 계정에 따라 속성 값을 추가합니다.
1. 서버를 시작하거나 다시 시작한 다음 관리자 계정을 사용하여 로그인합니다.
1. [통합 구성](/help/sites-administering/opt-in.md#configuring-the-integration)에 설명된 대로 Analytics 및 타깃팅 구성 작업을 엽니다. 계정 정보를 요청하는 대신 `.properties` 파일의 값을 사용합니다.

   해당 서비스에 대해 **추가**&#x200B;를 선택한 다음 마법사를 계속 진행합니다.

   ![optin-02](assets/optin-02.png)

## 클라우드 구성 {#about-the-cloud-configurations} 정보

Analytics 및 Target와의 통합을 구성하면 AEM에서 필요한 클라우드 구성 및 프레임워크를 자동으로 만듭니다. 예를 들어 Analytics 클라우드 구성을 프로비저닝된 Analytics 계정이라고 합니다.

클라우드 구성을 변경할 필요가 없습니다. 그러나 필요에 따라 프레임워크를 구성할 수 있습니다. ([Adobe Analytics 속성을 사용하여 구성 요소 데이터 매핑](/help/sites-administering/adobeanalytics-mapping.md) 및 [Target 프레임워크 추가](/help/sites-administering/target.md)를 참조하십시오.)

>[!NOTE]
>
>기본적으로 Adobe Target 구성 마법사를 선택하면 정확한 타겟 지정이 활성화됩니다.
>
>정확한 타겟 지정은 클라우드 서비스 구성이 컨텐츠를 로드하기 전에 컨텍스트가 로드될 때까지 대기함을 의미합니다. 따라서 성능 측면에서 정확한 타겟 지정이 콘텐츠를 로드하기 전에 몇 밀리초 지연을 만들 수 있습니다.
>
>작성자 인스턴스에서 항상 정확한 타겟 지정이 활성화되어 있습니다. 그러나 게시 인스턴스에서 클라우드 서비스 구성(**http://localhost:4502/etc/cloudservices.html**)의 정확한 타겟 지정 옆에 있는 확인 표시를 지워서 전체적으로 정확한 타겟 지정을 해제할 수 있습니다. 클라우드 서비스 구성에서 설정에 관계없이 개별 구성 요소에 대해 정확한 타겟 지정을 설정 및 해제할 수도 있습니다.
>
>***이미***&#x200B;에서 타깃팅된 구성 요소를 만들고 이 설정을 변경하는 경우 변경 사항이 해당 구성 요소에 영향을 주지 않습니다. 해당 구성 요소를 직접 변경해야 합니다.

>[!CAUTION]
>
>Analytics 구성을 선택하고 특정 `reportsuite`을 선택한 경우 프레임워크가 게시 실행 모드로 제한됩니다. 즉, 추적은 게시 인스턴스에서만 작동합니다.
>
>작성 인스턴스에서 추적이 필요한 경우 값을 `all`(으)로 변경해야 합니다.

## 스크립트 {#configuring-the-setup-and-provisioning-via-script}를 통해 설정 및 프로비저닝 구성

관리자는 마법사를 수동으로 stepping하지 않고 스크립트를 사용하여 설정 및 프로비전을 트리거할 수 있습니다. 다음을 통해 다음을 수행할 수 있습니다.

* 필요한 매개 변수와 함께 **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json**&#x200B;에 POST 요청을 보내는 중입니다.

보내는 매개 변수는 다음과 같은 경우에 따라 다릅니다.

* 필요한 모든 자격 증명으로 채워진 **marketingcloud.properties** 파일을 사용하려면 다음 매개 변수를 보내야 합니다.

   * `automaticProvisioning`= `true`
   * `servicename`=  `analytics|target`
   * `path`= 생성된 클라우드 서비스 구성을 첨부할 AEM 페이지의 경로입니다

   예를 들어 Analytics 및 Target 구성을 모두 생성하고 we.retail 페이지에 연결하는 curl 요청은 다음과 같습니다.

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* **marketingcloud.properties** 파일을 사용하지 않으려면 매개 변수와 자격 증명을 보내야 합니다.예:

   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=만든 클라우드 서비스 구성을 첨부할 AEM 페이지의 경로입니다.여러 경로를 정의할 수 있습니다
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

   이 경우 Analytics 및 Target 구성을 모두 생성하고 we-retail 페이지에 연결하는 curl 요청은 다음과 같습니다.

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```
