---
title: Adobe Campaign 통합 문제 해결
seo-title: Adobe Campaign 통합 문제 해결
description: Adobe Campaign 통합 문제를 해결하는 방법을 알아봅니다.
seo-description: Adobe Campaign 통합 문제를 해결하는 방법을 알아봅니다.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Adobe Campaign 통합 문제 해결{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>이 페이지는 Campaign Classic에 적용됩니다.

다음 문제 해결 팁은 AEM을 Adobe Campaign과 통합할 때 발생할 수 있는 가장 일반적인 문제를 해결하는 데 도움이 됩니다.

## 일반 문제 해결 팁 {#general-troubleshooting-tips}

두 통합의 경우 HTTP 호출이 전송되었는지 여부를 확인할 수 있습니다(AEM > Adobe Campaign, Adobe Campaign > AEM).

* 통합이 실패할 경우 이러한 호출이 다른 쪽 끝에 도달하는지 확인합니다(방화벽/SSL 문제를 방지하려면).
* AEM 기능의 경우, AEM 작성자 인터페이스에서 json 호출이 요청되었음을 확인할 수 있습니다.이로 인해 HTTP-500 오류가 발생하지 않습니다. HTTP-500 오류가 표시되는 경우 에 `error.log` 대한 자세한 내용을 확인하십시오.
* AEM 파섹

## 연결이 실패한 경우 {#if-the-connection-fails}

Adobe Campaign에서 **aemserver** 연산자를 구성했는지 확인합니다.

## 이미지가 Adobe Campaign 콘솔에 표시되지 않는 경우 {#if-images-do-not-appear-in-the-adobe-campaign-console}

HTML 소스를 확인하고 클라이언트 컴퓨터에서 URL을 열 수 있는지 확인합니다. URL에 localhost:4503이 있는 경우 작성 인스턴스에서 일 CQ 링크 외부라이저 구성을 변경하여 Adobe Campaign 콘솔 컴퓨터에서 액세스할 수 있는 게시 인스턴스를 가리킵니다.

Externalizer [구성을 참조하십시오.](/help/sites-administering/campaignstandard.md#configuring-the-externalizer)

## AEM에서 Adobe Campaign에 연결할 수 없는 경우 {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Adobe Campaign에서 다음 오류 메시지를 찾습니다.

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

이 문제를 해결하려면 다음을 **$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml에서**&#x200B;변경하십시오.

`<dataStore hosts="*" lang="en_GB">`

## Adobe Campaign 대화 상자에 데이터가 표시되지 않는 경우 {#if-no-data-displays-in-the-adobe-campaign-dialog}

Adobe Campaign에서 포트 번호 뒤에 후행 슬래시(/)가 없는지 확인합니다.

![chlimage_1-149](assets/chlimage_1-149.png)

## setlocale에 대한 경고가 표시되는 경우 {#if-you-get-a-warning-about-your-setlocale}

Apache HTTPD 서비스를 시작하고 있는 경우 시스템에 `"Warning: setlocale: LC_CTYPE cannot change locale"` en_CA.ISO-8859-15 로케일이 **** 설치되어 있는지 확인하십시오.

를 사용하여 설치되어 있는지 여부를 확인할 수 `local -a`있습니다. 설치되어 있지 않은 경우 /usr/local/neolane/nl6/env.sh **스크립트를** 패치하고 로케일을 설치된 스크립트로 변경할 수 있습니다.

## 스크립트 &#39;get_nms_amcGetSeedMetaData_jssp&#39;를 컴파일하는 동안 오류가 발생하는 경우 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

AEM 로그 파일에 다음 오류 메시지가 표시되는 경우:

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

다음 해결 방법을 사용하십시오.

1. 파일 열기 **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js**
1. &quot;amcGetSeedMetaData&quot; 메서드의 467행 수정
1. Change `label : [inclView.@label](mailto:inclView.@label)` to `label : String([inclView.@label](mailto:inclView.@label))`

1. 저장.
1. 서버를 다시 시작합니다.

## 동기화 단추를 클릭할 때 Adobe Campaign에 오류가 표시되는 경우 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Adobe Campaign Classic **에서** 동기화 단추를 클릭하면 다음 오류가 표시됩니다.

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

이 문제를 해결하려면 외부 계정에 구성된 AEM 연결 URL에 컴퓨터에서 연결할 수 있는지 확인하십시오.

localhost에서 **IP 주소로** 전환하면 이 문제가 해결되었습니다.

## &#39;Cannot parse XTK Date+Time &#39;undefined&quot; 오류가 발생하는 경우 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

동기화를 클릭하면 페이지의 스크립트가 발생했다는 오류가 표시됩니다.XTK Date+Time &#39;undefined&#39;를 구문 분석할 수 없습니다.올바른 XTK 값이 아닙니다.

AEM 인스턴스에 여전히 오래된 Adobe Campaign 정보가 있는 경우 이 문제가 발생합니다. AEM에 있는 모든 캠페인 통합 구성을 제거하고 다시 빌드하여 이 문제를 해결하십시오. 그런 다음 새 템플릿을 만듭니다.

## 클라우드 서비스를 설정할 때 SSL에 대한 연결에 오류가 표시되는 경우 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

AEM 파섹

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

Adobe Campaign 지원 팀과 함께 티켓 제시

## 동기화 대화 상자에 예상 https 링크 대신 http가 표시되는 경우 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

다음 설정 사용:

* AEM 작성자와의 통신을 위해 https를 사용하여 Adobe Campaign 호스팅
* SSL을 종료하는 역방향 프록시
* 온-프레미스 AEM 작성자 인스턴스

Adobe Campaign 게재의 컨텐츠를 동기화하려고 하면 AEM은 뉴스레터 목록을 반환합니다. 하지만 목록의 뉴스레터에 대한 URL은 http 주소입니다. 목록에서 항목 중 하나를 선택하면 오류가 발생합니다.

이 문제를 해결하려면 다음을 수행하십시오.

* 원래 프로토콜을 헤더로 전달하려면 디스패처 또는 역방향 프록시를 구성해야 합니다.
* OSGi *구성의* Apache Felix Http 서비스 SSL 필터([https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr))를 각 헤더 설정으로 구성해야 합니다. https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter을 [참조하십시오.](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter)

## 만든 사용자 지정 템플릿을 페이지 속성에서 선택할 수 없는 경우 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Adobe Campaign에 대한 메일 템플릿을 만들 때는 값 **map** 받는 사람이 **있는 속성 acMapping을 템플릿의** jcr:content **노드에 포함시켜야** 합니다 **. 그렇지 않으면 AEM의 페이지 속성에서 Adobe Campaign** 템플릿을 선택할 수 없습니다(필드가 비활성화됨).

## 로그에 &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; 오류가 표시되는 경우 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

사용자 지정 템플릿을 사용하는 경우 로그에 &quot;com.day.cq.mcm.campaign.servlets.util.ParameterMapper&quot; 오류가 표시됩니다. 이 경우 [패키지 공유]에서 FeaturePack 6576을 [설치하십시오](/help/sites-administering/package-manager.md#package-share). 이 문제는 acMapping 속성이 recipient.firstName 이외의 값으로 설정된 경우 Adobe Campaign Manager 측에서 빈 값이 생성되는 문제입니다.
