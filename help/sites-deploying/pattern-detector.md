---
title: Pattern Detector를 사용한 업그레이드 복잡성 평가
seo-title: Pattern Detector를 사용한 업그레이드 복잡성 평가
description: Pattern Detector를 사용하여 업그레이드의 복잡성을 평가하는 방법을 살펴볼 수 있습니다.
seo-description: Pattern Detector를 사용하여 업그레이드의 복잡성을 평가하는 방법을 살펴볼 수 있습니다.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
translation-type: tm+mt
source-git-commit: ba7ac70858b7b2fd610d63355a22a69c3a7586e3
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 1%

---


# Pattern Detector를 사용한 업그레이드 복잡성 평가

## 개요 {#overview}

이 기능을 사용하면 사용 중인 패턴을 감지하여 기존 AEM 인스턴스에서 업그레이드 가능성을 확인할 수 있습니다.

1. 특정 규칙을 위반하고 업그레이드로 인해 영향을 받거나 덮어쓸 영역에서 수행됩니다
1. AEM 6.x 기능 또는 AEM 6.5에서 역호환이 되지 않고 업그레이드 후 중단될 가능성이 있는 API를 사용하십시오.

이는 AEM 6.5로 업그레이드하는 데 관련된 개발 작업의 평가 역할을 할 수 있습니다.

## 설정 방법 {#how-to-set-up}

패턴 탐지기는 AEM 6.5 업그레이드를 대상으로 하는 모든 소스 AEM 버전에서 작동하는 [하나의 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65)로 별도로 출시됩니다. [패키지 관리자](/help/sites-administering/package-manager.md)를 사용하여 설치할 수 있습니다.

## 사용 방법 {#how-to-use}

>[!NOTE]
>
>패턴 탐지기는 로컬 개발 인스턴스를 비롯한 모든 환경에서 실행할 수 있습니다. 그러나 다음 작업을 수행하려면:
>
>* 감지 속도 증가
>* 중요한 비즈니스 인스턴스 속도 저하 방지

>
>
동시에 사용자 응용 프로그램, 콘텐트 및 구성 영역의 프로덕션 환경에 가능한 한 가까운 **을 스테이징 환경에서 실행하는 것이 좋습니다.**

여러 가지 방법을 사용하여 패턴 탐지기 출력을 확인할 수 있습니다.

* **Felix Inventory 콘솔을 통해 다음을 수행할 수 있습니다.**

1. *https://serveraddress:serverport/system/console/configMgr*&#x200B;에서 AEM 웹 콘솔로 이동
1. 아래 이미지에 표시된 대로 **상태 - 패턴 탐지기**&#x200B;를 선택합니다.

   ![스크린샷-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **반응형 텍스트 기반 또는 일반 JSON 인터페이스를 통해**
* **각 줄에 별도의 JSON 문서를 생성하는 인터랙티브한 JSON 라인 인터페이스를 통해 **이 제공됩니다.

이러한 방법 모두 아래에 자세히 설명되어 있습니다.

## 반응형 인터페이스 {#reactive-interface}

반응형 인터페이스를 사용하면 의심스러운 점이 발견되면 즉시 위반 보고서를 처리할 수 있습니다.

출력은 현재 2개의 URL에서 사용할 수 있습니다.

1. 일반 텍스트 인터페이스
1. JSON 인터페이스

## 일반 텍스트 인터페이스 처리 {#handling-the-plain-text-interface}

출력물의 정보는 일련의 이벤트 항목으로 지정됩니다. 두 개의 채널이 있습니다. 하나는 게시 위반이고 다른 하나는 현재 진행 상황을 게시하는 채널입니다.

다음 명령을 사용하여 얻을 수 있습니다.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

결과는 다음과 같습니다.

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

진행 상태는 `grep` 명령을 사용하여 필터링할 수 있습니다.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

다음 결과를 초래합니다.

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

진행 상황은 5초에 한 번씩 보고되며, 의심이 표시된 메시지 이외의 다른 메시지는 제외하여 받아들일 수 있다:

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
>전체 출력의 말림 효과를 파일에 저장한 다음 `jq` 또는 `grep`을 통해 처리하여 정보 유형을 필터링하는 것이 좋습니다.

## 감지 범위 {#scope}

현재 패턴 탐지기 기능을 통해 다음을 확인할 수 있습니다.

* OSGi 번들 내보내기 및 가져오기 불일치
* 리소스 유형 및 슈퍼 유형(검색 경로 컨텐츠 오버레이 포함) 초과 사용
* Oak 인덱스 정의(호환성)
* VLT 패키지(초과 사용)
* rep:사용자 노드 호환성(OAuth 구성 컨텍스트)

>[!NOTE]
>
>Pattern Detector는 업그레이드에 대한 경고를 정확히 예측하려고 합니다. 하지만 일부 시나리오에서 잘못된 긍지를 생성할 수 있습니다.
