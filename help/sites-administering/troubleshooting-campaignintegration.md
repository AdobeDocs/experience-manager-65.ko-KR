---
title: Adobe Campaign 통합 문제 해결
seo-title: Troubleshooting your Adobe Campaign Integration
description: Adobe Campaign 통합 문제를 해결하는 방법을 알아봅니다.
seo-description: Learn how to troubleshoot issues with the Adobe Campaign Integration.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# Adobe Campaign 통합 문제 해결{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>이 페이지는 Campaign Classic에 적용됩니다.

다음 문제 해결 팁은 AEM을 Adobe Campaign과 통합할 때 발생할 수 있는 가장 일반적인 문제를 해결하는 데 도움이 됩니다.

## 일반 문제 해결 팁 {#general-troubleshooting-tips}

두 통합의 경우 HTTP 호출이 전송되는지(AEM > Adobe Campaign, Adobe Campaign > AEM) 여부를 확인할 수 있습니다.

* 통합이 실패하면 이러한 호출이 다른 쪽 끝에 도착하는지 확인합니다(방화벽/SSL 문제를 방지하기 위해).
* AEM 기능의 경우 AEM 작성자 인터페이스에서 json 호출이 요청된다는 것을 볼 수 있습니다. 이로 인해 HTTP-500 오류가 발생하지 않습니다. HTTP-500 오류가 표시되면 `error.log` 자세한 내용
* AEM에서 campaign-class에 대한 디버그 수준을 높이면 문제를 해결하는 데 도움이 됩니다.

## 연결에 실패하면 {#if-the-connection-fails}

다음을 구성했는지 확인합니다 **aemserver** 연산자를 사용할 수 있습니다.

## Adobe Campaign 콘솔에 이미지가 표시되지 않는 경우 {#if-images-do-not-appear-in-the-adobe-campaign-console}

HTML 소스를 확인하고 클라이언트 시스템에서 URL을 열 수 있는지 확인합니다. URL에 localhost:4503이 있는 경우 작성 인스턴스에서 Day CQ Link Externalizer의 구성을 변경하여 Adobe Campaign 콘솔 시스템에서 도달할 수 있는 게시 인스턴스를 가리킵니다.

자세한 내용은 [Externalizer 구성](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## AEM에서 Adobe Campaign으로 연결할 수 없는 경우 {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Adobe Campaign에서 다음 오류 메시지를 찾습니다.

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

이 문제를 해결하려면 **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml**:

`<dataStore hosts="*" lang="en_GB">`

## Adobe Campaign 대화 상자에 데이터가 표시되지 않는 경우 {#if-no-data-displays-in-the-adobe-campaign-dialog}

Adobe Campaign에서 포트 번호 뒤에 후행 슬래시(/)가 없는지 확인합니다.

![chlimage_1-149](assets/chlimage_1-149.png)

## setlocale에 대한 경고가 나타나면 {#if-you-get-a-warning-about-your-setlocale}

Apache HTTPD 서비스를 시작하는 경우 오류가 표시됩니다 `"Warning: setlocale: LC_CTYPE cannot change locale"` 다음 사항을 확인하십시오. **en_CA.ISO-8859-15 로케일** 시스템에 설치되었습니다.

를 사용하여 설치 여부를 확인할 수 있습니다 `local -a`. 설치되어 있지 않으면 패치할 수 있습니다 **/usr/local/neolane/nl6/env.sh** 스크립트를 작성하고 로케일을 설치된 로케일로 변경합니다.

## &#39;get_nms_amcGetSeedMetaData_jssp&#39; 스크립트를 컴파일하는 동안 오류가 발생하면 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

AEM 로그 파일에 다음 오류 메시지가 표시되는 경우,

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

다음 해결 방법을 사용하십시오.

1. 파일 열기 **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. &quot;amcGetSeedMetaData&quot; 메서드의 467행을 수정합니다.
1. 변경 `label : [inclView.@label](mailto:inclView.@label)` to `label : String([inclView.@label](mailto:inclView.@label))`

1. 저장.
1. 서버를 다시 시작합니다.

## 동기화 단추를 클릭할 때 Adobe Campaign에 오류가 표시되는 경우 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

을 클릭할 때 **동기화** Adobe Campaign Classic 버튼을 클릭하면 다음 오류가 표시됩니다.

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

이 문제를 해결하려면 외부 계정에 구성된 AEM 연결 URL에 컴퓨터에서 연결할 수 있는지 확인합니다.

스위치 **localhost** IP 주소로 가 이 문제를 해결했습니다.

## &#39;XTK Date+Time &#39;undefined&#39;를 구문 분석할 수 없음&#39; 오류가 발생하는 경우 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

동기화를 클릭하면 페이지의 스크립트가 발생했을 때 오류가 발생합니다. XTK 날짜+시간 &#39;정의되지 않음&#39;을 구문 분석할 수 없습니다. 올바른 XTK 값이 아닙니다.

AEM 인스턴스에 대한 오래된 Adobe Campaign 정보가 여전히 있는 경우 이 문제가 발생합니다. AEM에 있는 모든 캠페인 통합 구성을 제거하고 다시 빌드하여 이 문제를 해결합니다. 그런 다음 새 템플릿을 만듭니다.

## 클라우드 서비스를 설정할 때 SSL에 연결된 오류가 표시되는 경우 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

AEM의 error.log에서 다음 내용이 표시됩니다.

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

Adobe Campaign 지원 팀과 티켓을 제출하세요.

## 동기화 대화 상자에 필요한 https 링크 대신 http가 표시되는 경우 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

다음 설정을 사용하여 다음을 수행하십시오.

* AEM 작성자와의 통신을 위해 https를 사용하여 Adobe Campaign 호스팅
* SSL을 종료하는 역방향 프록시
* 온-프레미스 AEM 작성자 인스턴스

Adobe Campaign 게재에서 컨텐츠를 동기화하려 하면 AEM에서 뉴스레터 목록을 반환합니다. 그러나 목록의 뉴스레터 URL은 http 주소입니다. 목록에서 항목 중 하나를 선택하면 오류가 발생합니다.

이 문제를 해결하려면

* 원래 프로토콜을 헤더로 전달하도록 디스패처 또는 역방향 프록시를 구성해야 합니다.
* 다음 *Apache Felix Http Service SSL 필터* OSGi 구성([https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr))을 각 헤더 설정으로 구성해야 합니다. 자세한 내용은 [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## 만든 사용자 지정 템플릿을 페이지 속성에서 선택할 수 없는 경우 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Adobe Campaign용 메일 템플릿을 만들 때는 속성을 포함해야 합니다 **acMapping** 값 사용 **mapRecipient** 에서 **jcr:content** 템플릿의 노드 또는 **페이지 속성** AEM의 경우(필드가 비활성화되어 있음).

## 로그에 &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; 오류가 발생하면 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

사용자 지정 템플릿을 사용하는 경우 로그에 &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; 오류가 표시됩니다. 이 이벤트에서 Featurepack 6576을 설치하십시오. [패키지 공유](/help/sites-administering/package-manager.md#package-share). 이 문제는 acMapping 속성이 recipient.firstName 이외의 값으로 설정된 경우 Adobe Campaign Manager 측에 빈 값이 생성됩니다.
