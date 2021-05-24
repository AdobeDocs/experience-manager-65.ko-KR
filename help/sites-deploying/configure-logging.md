---
title: 로깅
seo-title: 로깅
description: 중앙 로깅 서비스에 대한 글로벌 매개 변수 구성 방법, 개별 서비스에 대한 특정 설정 또는 데이터 로깅을 요청하는 방법을 알아봅니다.
seo-description: 중앙 로깅 서비스에 대한 글로벌 매개 변수 구성 방법, 개별 서비스에 대한 특정 설정 또는 데이터 로깅을 요청하는 방법을 알아봅니다.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
feature: 구성
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# 로깅{#logging}

AEM에서는 다음을 구성할 수 있는 기회를 제공합니다.

* 중앙 로깅 서비스의 전역 매개 변수
* 요청 데이터 로깅;요청 정보에 대한 전문 로깅 구성
* 개별 서비스에 대한 특정 설정예를 들어 개별 로그 파일과 로그 메시지의 형식 등이 있습니다

모두 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)입니다.

>[!NOTE]
>
>AEM에 로그인하는 것은 Sling 원칙을 기반으로 합니다. 자세한 내용은 [Sling 로깅](https://sling.apache.org/site/logging.html)을 참조하십시오.

## 전역 로깅 {#global-logging}

[Apache Sling 로깅 ](/help/sites-deploying/osgi-configuration-settings.md) 구성은 루트 로거를 구성하는 데 사용됩니다. AEM에서 로그인하기 위한 전역 설정을 정의합니다.

* 로깅 수준
* 중앙 로그 파일의 위치
* 유지할 버전 수
* 버전 순환최대 크기 또는 시간 간격
* 로그 메시지를 작성할 때 사용할 형식입니다

>[!NOTE]
>
>이 [기술 자료 문서](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html)에서는 request.log 및 access.log 파일을 회전하는 방법을 설명합니다.

## 개별 서비스의 트리거 및 작성기 {#loggers-and-writers-for-individual-services}

전역 로깅 설정 외에 AEM에서는 개별 서비스에 대한 특정 설정을 구성할 수 있습니다.

* 특정 로깅 수준
* 개별 로그 파일의 위치
* 유지할 버전 수
* 버전 순환최대 크기 또는 시간 간격
* 로그 메시지를 작성할 때 사용할 형식입니다
* 로거(로그 메시지를 제공하는 OSGi 서비스)

이렇게 하면 단일 서비스의 로그 메시지를 별도의 파일로 채널화할 수 있습니다. 이 기능은 개발 또는 테스트 중에 특히 유용할 수 있습니다.예를 들어, 특정 서비스에 대해 로그 수준을 높여야 하는 경우

AEM에서는 파일에 로그 메시지를 작성하려면 다음을 사용합니다.

1. **OSGi 서비스**(로거)는 로그 메시지를 기록합니다.
1. **로깅 로거**&#x200B;는 이 메시지를 가져와 사양에 따라 형식을 지정합니다.
1. **로깅 작성기**&#x200B;는 이러한 모든 메시지를 사용자가 정의한 실제 파일에 기록합니다.

이러한 요소는 적절한 요소에 대해 다음 매개 변수로 연결됩니다.

* **로거(로깅 로거)**

   메시지를 생성하는 서비스를 정의합니다.

* **로그 파일(로깅 로거)**

   로그 메시지를 저장할 물리적 파일을 정의합니다.

   로깅 작성기에 로깅 로거를 연결하는 데 사용됩니다. 연결을 만들려면 값이 로깅 작성기 구성에서 동일한 매개 변수와 동일해야 합니다.

* **로그 파일(로깅 작성기)**

   로그 메시지가 기록될 실제 파일을 정의합니다.

   이 매개 변수는 로깅 작성기 구성에서 동일한 매개 변수와 동일해야 합니다. 그렇지 않으면 비교가 수행되지 않습니다. 일치하는 항목이 없으면 기본 구성(일별 로그 회전)으로 암시적 작성기가 만들어집니다.

### 표준 로거 및 작성기 {#standard-loggers-and-writers}

특정 로거 및 작성기는 표준 AEM 설치에 포함됩니다.

첫 번째는 `request.log` 파일과 `access.log` 파일을 모두 제어하기 때문에 특별한 경우입니다.

* 로거:

   * Apache Sling 사용자 지정 가능 요청 데이터 로거

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 요청 내용에 대한 메시지를 `request.log`에 쓰십시오.

* 링크 대상:

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 메시지를 `request.log` 또는 `access.log`에 씁니다.

표준 구성은 대부분의 설치에 적합하지만 필요한 경우 사용자 지정할 수 있습니다.

다른 쌍은 표준 구성을 따릅니다.

* 로거:

   * Apache Sling 로깅 로거 구성

      (org.apache.sling.commons.log.LogManager.factory.config)

   * `Information` 메시지를 `logs/error.log`에 씁니다.

* 작성기에 대한 링크:

   * Apache Sling 로깅 작성기 구성

      (org.apache.sling.commons.log.LogManager.factory.writer)

* 로거:

   * Apache Sling 로깅 로거 구성
(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 서비스 `org.apache.pdfbox`에 대해 `Warning` 메시지를 `../logs/error.log`에 씁니다.

* 특정 작성기에 연결하지 않으므로 기본 구성(일별 로그 순환)으로 암시적 작성기를 만들고 사용할 수 있습니다.

### 고유한 로거 및 작성기 만들기 {#creating-your-own-loggers-and-writers}

고유한 로거/작성기 쌍을 정의할 수 있습니다.

1. 공장 구성 [Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md)의 새 인스턴스를 만듭니다.

   1. 로그 파일을 지정합니다.
   1. 로거를 지정합니다.
   1. 필요에 따라 다른 매개 변수를 구성합니다.

1. 공장 구성 [Apache Sling 로깅 작성기 구성](/help/sites-deploying/osgi-configuration-settings.md)의 새 인스턴스를 만듭니다.

   1. 로그 파일을 지정합니다. 이 파일은 로거에 지정된 파일과 일치해야 합니다.
   1. 필요에 따라 다른 매개 변수를 구성합니다.

>[!NOTE]
>
>특정 상황에서 [사용자 지정 로그 파일](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)을 만들 수 있습니다.
