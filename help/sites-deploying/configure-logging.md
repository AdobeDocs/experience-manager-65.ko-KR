---
title: 로깅
seo-title: 로깅
description: 중앙 로깅 서비스에 대한 전역 매개 변수, 개별 서비스에 대한 특정 설정 또는 데이터 로깅을 요청하는 방법을 알아봅니다.
seo-description: 중앙 로깅 서비스에 대한 전역 매개 변수, 개별 서비스에 대한 특정 설정 또는 데이터 로깅을 요청하는 방법을 알아봅니다.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# 로깅{#logging}

AEM은 다음과 같은 구성 가능성을 제공합니다.

* 중앙 로깅 서비스에 대한 전역 매개 변수
* 요청 데이터 로깅;요청 정보에 대한 전문 로깅 구성
* 개별 서비스에 대한 특정 설정;예를 들어 개별 로그 파일과 로그 메시지의 형식

모두 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)입니다.

>[!NOTE]
>
>AEM에 로그인하는 것은 Sling 원칙을 기반으로 합니다. 자세한 내용은 [로깅](https://sling.apache.org/site/logging.html)을 참조하십시오.

## 전역 로깅 {#global-logging}

[Apache Sling 로깅 ](/help/sites-deploying/osgi-configuration-settings.md) 구성은 루트 로거를 구성하는 데 사용됩니다. AEM 로그인에 대한 전역 설정을 정의합니다.

* 로깅 수준
* 중앙 로그 파일의 위치
* 유지할 버전 수
* 버전 회전;최대 크기 또는 시간 간격
* 로그 메시지를 쓸 때 사용할 형식

>[!NOTE]
>
>이 [기술 자료 문서](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html)에서는 request.log 및 access.log 파일을 회전하는 방법을 설명합니다.

## 개인 서비스 로거 및 작성자 {#loggers-and-writers-for-individual-services}

AEM에서는 전역 로깅 설정 외에도 개별 서비스에 대한 특정 설정을 구성할 수 있습니다.

* 특정 로깅 수준
* 개별 로그 파일의 위치
* 유지할 버전 수
* 버전 회전;최대 크기 또는 시간 간격
* 로그 메시지를 쓸 때 사용할 형식
* 로거(로그 메시지를 제공하는 OSGi 서비스)

단일 서비스의 로그 메시지를 별도의 파일로 보낼 수 있습니다. 개발 또는 테스트 중에 특히 유용할 수 있습니다.예를 들어, 특정 서비스에 대해 로그 수준이 향상되어야 합니다.

AEM에서는 파일에 로그 메시지를 기록할 때 다음을 사용합니다.

1. **OSGi 서비스**(로거)는 로그 메시지를 기록합니다.
1. **로깅 로거**&#x200B;는 이 메시지를 가져와서 사양에 따라 형식을 지정합니다.
1. **로깅 기록기**&#x200B;는 사용자가 정의한 실제 파일에 이러한 메시지를 모두 기록합니다.

이러한 요소는 적절한 요소에 대해 다음 매개 변수로 연결됩니다.

* **로거(로깅 로거)**

   메시지를 생성하는 서비스를 정의합니다.

* **로그 파일(로깅 로거)**

   로그 메시지를 저장할 물리적 파일을 정의합니다.

   로깅 로거를 로깅 기록기와 연결하는 데 사용됩니다. 연결이 이루어지려면 로깅 기록기 구성에 있는 동일한 매개 변수와 값이 동일해야 합니다.

* **로그 파일(로깅 작성기)**

   로그 메시지를 기록할 실제 파일을 정의합니다.

   로깅 기록기 구성에서 동일한 매개 변수와 동일해야 하며 그렇지 않으면 일치되지 않습니다. 일치하는 항목이 없으면 암시적 작성기가 기본 구성(일별 로그 순환)으로 만들어집니다.

### 표준 로거 및 작성자 {#standard-loggers-and-writers}

특정 로거 및 작가는 표준 AEM 설치에 포함되어 있습니다.

첫 번째 경우는 `request.log` 파일과 `access.log` 파일을 모두 제어하기 때문에 특별한 경우입니다.

* 로거:

   * Apache Sling 사용자 정의 가능한 요청 데이터 로거

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 요청 내용에 대한 메시지를 `request.log`에 씁니다.

* 링크 대상:

   * Apache Sling 요청 로거

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 메시지를 `request.log` 또는 `access.log`에 씁니다.

표준 구성은 대부분의 설치에 적합하지만 필요할 경우 사용자 정의할 수 있습니다.

다른 쌍은 표준 구성을 따릅니다.

* 로거:

   * Apache Sling 로깅 로거 구성

      (org.apache.sling.commons.log.LogManager.factory.config)

   * `Information` 메시지를 `logs/error.log`에 씁니다.

* 작성기에 대한 링크:

   * Apache Sling 로깅 작성자 구성

      (org.apache.sling.commons.log.LogManager.factory.writer)

* 로거:

   * Apache Sling 로깅 로거 구성
(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * `org.apache.pdfbox` 서비스에 대해 `Warning` 메시지를 `../logs/error.log`에 씁니다.

* 특정 작성기에 링크하지 않으므로 기본 구성(일별 로그 순환)으로 암시적 작성기를 만들고 사용합니다.

### 자체 로거 및 작성자 만들기 {#creating-your-own-loggers-and-writers}

로거/작성기 쌍을 정의할 수 있습니다.

1. 팩토리 구성 [Apache Sling 로깅 로거 구성](/help/sites-deploying/osgi-configuration-settings.md)의 새 인스턴스를 만듭니다.

   1. 로그 파일을 지정합니다.
   1. 로거를 지정합니다.
   1. 필요에 따라 다른 매개 변수를 구성합니다.

1. 팩토리 구성 [Apache Sling 로깅 작성자 구성](/help/sites-deploying/osgi-configuration-settings.md)의 새 인스턴스를 만듭니다.

   1. 로그 파일을 지정하십시오. 로거에 대해 지정된 파일과 일치해야 합니다.
   1. 필요에 따라 다른 매개 변수를 구성합니다.

>[!NOTE]
>
>특정 상황에서는 [사용자 지정 로그 파일](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)을 만들 수 있습니다.

