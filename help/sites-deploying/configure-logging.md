---
title: 로깅
description: 중앙 로깅 서비스에 대한 전역 매개 변수를 구성하는 방법, 개별 서비스에 대한 특정 설정 또는 데이터 로깅을 요청하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# 로깅{#logging}

AEM에서는 다음을 구성할 수 있습니다.

* 중앙 로깅 서비스에 대한 전역 매개 변수
* 요청 데이터 로깅, 요청 정보에 대한 전문 로깅 구성
* 개별 서비스에 대한 특정 설정(예: 로그 메시지의 개별 로그 파일 및 형식)

모두 [OSGi 구성](/help/sites-deploying/configuring-osgi.md)입니다.

>[!NOTE]
>
>AEM에서의 로그인은 Sling 원칙을 기반으로 합니다. 자세한 내용은 [Sling 로깅](https://sling.apache.org/site/logging.html)을 참조하십시오.

## 글로벌 로깅 {#global-logging}

[Apache Sling 로깅 구성](/help/sites-deploying/osgi-configuration-settings.md)을 사용하여 루트 로거를 구성합니다. AEM 로그인에 대한 전역 설정을 정의합니다.

* 로깅 수준
* 중앙 로그 파일의 위치
* 보관할 버전 수
* 버전 회전(최대 크기 또는 시간 간격)
* 로그 메시지를 작성할 때 사용할 형식

## 개인 서비스용 로거 및 라이터 {#loggers-and-writers-for-individual-services}

글로벌 로깅 설정 외에도 AEM을 사용하여 개별 서비스에 대한 특정 설정을 구성할 수 있습니다.

* 특정 로깅 수준
* 개별 로그 파일의 위치
* 보관할 버전 수
* 버전 회전(최대 크기 또는 시간 간격)
* 로그 메시지를 작성할 때 사용할 형식
* 로거(로그 메시지를 제공하는 OSGi 서비스)

이렇게 하면 단일 서비스에 대한 로그 메시지를 별도의 파일로 전달할 수 있습니다. 이 기능은 개발 또는 테스트 중(예: 특정 서비스에 대해 증가된 로그 수준이 필요한 경우) 특히 유용합니다.

AEM은 다음을 사용하여 로그 메시지를 파일에 기록합니다.

1. **OSGi 서비스**(로거)가 로그 메시지를 씁니다.
1. **Logging Logger**&#x200B;은(는) 이 메시지를 사용하고 사용자의 사양에 따라 형식을 지정합니다.
1. **Logging Writer**&#x200B;는 사용자가 정의한 실제 파일에 이 모든 메시지를 씁니다.

이러한 요소는 적절한 요소에 대해 다음 매개 변수로 연결됩니다.

* **로거(로거 로깅)**

  메시지를 생성하는 서비스를 정의합니다.

* **로그 파일(로깅 로거)**

  로그 메시지를 저장할 실제 파일을 정의합니다.

  이 로그는 로깅 작성기에 로깅 로거를 연결하는 데 사용됩니다. 연결할 로깅 작성기 구성의 매개 변수와 값이 동일해야 합니다.

* **로그 파일(Logging Writer)**

  로그 메시지가 기록될 물리적 파일을 정의합니다.

  이것은 로깅 작성기 구성의 동일한 매개 변수와 동일해야 합니다. 그렇지 않으면 일치가 수행되지 않습니다. 일치하는 항목이 없으면 기본 구성(일별 로그 회전)을 사용하여 암시적 작성기가 만들어집니다.

### 표준 로거 및 작성자 {#standard-loggers-and-writers}

특정 로거 및 작성기는 표준 AEM 설치에 포함되어 있습니다.

첫 번째는 `request.log` 및 `access.log` 파일을 모두 제어하기 때문에 특별한 경우입니다.

* 로거:

   * Apache Sling 사용자 지정 가능 요청 데이터 로거

     (org.apache.sling.engine.impl.log.RequestLoggerService)

   * `request.log`에 요청 콘텐츠에 대한 메시지를 씁니다.

* 링크 대상:

   * Apache Sling 요청 로거

     (org.apache.sling.engine.impl.log.RequestLogger)

   * 메시지를 `request.log` 또는 `access.log`에 씁니다.

표준 구성은 대부분의 설치에 적합하지만 필요한 경우 사용자 정의할 수 있습니다.

다른 쌍은 표준 구성을 따릅니다.

* 로거:

   * Apache Sling 로깅 로거 구성

     (org.apache.sling.commons.log.LogManager.factory.config)

   * `Information`개의 메시지를 `logs/error.log`에 씁니다.

* 작성기 링크:

   * Apache Sling 로깅 작성기 구성

     (org.apache.sling.commons.log.LogManager.factory.writer)

* 로거:

   * Apache Sling 로깅 로거 구성
(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * `org.apache.pdfbox` 서비스에 대해 `../logs/error.log`에 `Warning`개의 메시지를 씁니다.

* 특정 작성기에 연결되지 않으므로 기본 구성(일별 로그 회전)을 사용하는 암시적 작성기가 작성 및 사용됩니다.

### 나만의 로거 및 작성기 만들기 {#creating-your-own-loggers-and-writers}

고유한 로거/작성기 쌍을 정의할 수 있습니다.

1. 팩터리 구성 [Apache Sling 로깅 로거 구성](/help/sites-deploying/osgi-configuration-settings.md)의 인스턴스를 만듭니다.

   1. 로그 파일을 지정합니다.
   1. 로거를 지정합니다.
   1. 필요에 따라 다른 매개 변수를 구성합니다.

1. 팩터리 구성 [Apache Sling Logging Writer 구성](/help/sites-deploying/osgi-configuration-settings.md)의 인스턴스를 만듭니다.

   1. 로그 파일을 지정하십시오. 이 파일은 로거에 대해 지정된 것과 일치해야 합니다.
   1. 필요에 따라 다른 매개 변수를 구성합니다.

>[!NOTE]
>
>경우에 따라 [사용자 지정 로그 파일](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)을 만들 수 있습니다.
