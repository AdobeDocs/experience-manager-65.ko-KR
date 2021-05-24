---
title: 패턴 탐지기를 사용한 업그레이드 복잡성 평가
seo-title: 패턴 탐지기를 사용한 업그레이드 복잡성 평가
description: 패턴 탐지기 를 사용하여 업그레이드의 복잡성을 평가하는 방법을 알아봅니다.
seo-description: 패턴 탐지기 를 사용하여 업그레이드의 복잡성을 평가하는 방법을 알아봅니다.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
feature: 업그레이드
exl-id: c42373e9-712e-4c11-adbb-4e3626e0b217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---

# 패턴 탐지기를 사용한 업그레이드 복잡성 평가

## 개요 {#overview}

이 기능을 사용하면 사용 중인 패턴을 감지하여 기존 AEM 인스턴스에서 업그레이드 가능성을 확인할 수 있습니다.

1. 특정 규칙을 위반하고 업그레이드에 의해 영향을 받거나 덮어쓸 영역에서 수행됩니다
1. AEM 6.5에서 이전 버전과 호환되지 않으며 업그레이드 후 중단될 수 있는 AEM 6.x 기능 또는 API를 사용하십시오.

AEM 6.5로 업그레이드하는 작업에 대한 평가 역할을 할 수 있습니다.

## 설정 방법 {#how-to-set-up}

패턴 탐지기는 AEM 6.5를 대상으로 하는 6.1에서 6.5로 소스 AEM 버전에서 작동하는 [하나의 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65)로 별도로 릴리스됩니다. [패키지 관리자](/help/sites-administering/package-manager.md)를 사용하여 설치할 수 있습니다.

## 사용 방법 {#how-to-use}

>[!NOTE]
>
>패턴 탐지기는 로컬 개발 인스턴스를 비롯한 모든 환경에서 실행할 수 있습니다. 그러나 이를 위해서는
>
>* 검출 속도 증가
>* 비즈니스 크리티컬 인스턴스를 지연시키지 않도록 합니다.

>
>
동시에 사용자 애플리케이션, 컨텐츠 및 구성 영역의 프로덕션 환경에 최대한 가까운 **을 스테이징 환경에서 실행하는 것이 좋습니다.**

몇 가지 방법을 사용하여 패턴 탐지기 출력을 확인할 수 있습니다.

* **Felix Inventory 콘솔을 통해**

1. *https://serveraddress:serverport/system/console/configMgr*&#x200B;로 이동하여 AEM 웹 콘솔로 이동합니다.
1. 아래 그림과 같이 **상태 - 패턴 탐지기**&#x200B;를 선택합니다.

   ![스크린샷-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **반응형 텍스트 기반 또는 일반 JSON 인터페이스를 통해**
* **각 행에 별도의 JSON 문서를 **는 반응형 JSON 라인 인터페이스를 통해 .

이 두 방법 모두 아래에 자세히 설명되어 있습니다.

## 반응형 인터페이스 {#reactive-interface}

상기 반응형 인터페이스는 혐의가 감지되는 즉시 상기 위반보고서를 처리할 수 있다.

출력은 현재 2개의 URL에서 사용할 수 있습니다.

1. 일반 텍스트 인터페이스
1. JSON 인터페이스

## 일반 텍스트 인터페이스 처리 {#handling-the-plain-text-interface}

출력에 있는 정보는 일련의 이벤트 항목으로 서식이 지정됩니다. 위반 게시용 채널과 현재 진행 상황을 게시하는 데 사용할 수 있는 두 개의 채널이 있습니다.

다음 명령을 사용하여 가져올 수 있습니다.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

출력은 다음과 같습니다.

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

진행 상태는 `grep` 명령을 사용하여 필터링할 수 있습니다.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

결과:

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## JSON 인터페이스 처리 {#handling-the-json-interface}

마찬가지로 JSON은 게시되는 즉시 [jq tool](https://stedolan.github.io/jq/)을 사용하여 처리할 수 있습니다.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

출력 사용:

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

진행 상황을 5초마다 보고하며 의혹 이외의 다른 메시지는 제외하고 불러도 된다.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

출력 사용:

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>curl의 전체 출력을 파일에 저장한 다음 `jq` 또는 `grep` 을 통해 처리하여 정보 유형을 필터링하는 것이 좋습니다.

## 검색 범위 {#scope}

현재 패턴 탐지기에서 다음을 확인할 수 있습니다.

* OSGi 번들 내보내기 및 가져오기 불일치
* Sling 리소스 유형 및 수퍼 유형(검색 경로 컨텐츠 오버레이 사용) 초과 사용
* Oak 색인 정의(호환성)
* VLT 패키지(초과 사용)
* rep:사용자 노드 호환성(OAuth 구성 컨텍스트)

>[!NOTE]
>
>패턴 탐지기는 업그레이드에 대한 경고를 정확하게 예측하려고 합니다. 그러나 일부 시나리오에서 긍정 오류(false positive)가 발생할 수 있습니다.
