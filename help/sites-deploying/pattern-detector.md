---
title: 패턴 감지기를 사용한 업그레이드 복잡성 평가
description: 패턴 감지기를 사용하여 업그레이드의 복잡성을 평가하는 방법에 대해 알아봅니다.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
docset: aem65
feature: Upgrading
exl-id: c42373e9-712e-4c11-adbb-4e3626e0b217
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# 패턴 감지기를 사용한 업그레이드 복잡성 평가

## 개요 {#overview}

이 기능을 사용하면 사용 중인 패턴을 감지하여 기존 AEM 인스턴스의 업그레이드 가능성을 확인할 수 있습니다.

1. 특정 규칙을 위반하고 업그레이드의 영향을 받거나 덮어쓸 영역에서 수행됩니다.
1. AEM 6.5에서 역으로 호환되지 않으며 업그레이드 후 잠재적으로 중단될 수 있는 AEM 6.x 기능 또는 API를 사용합니다.

이는 AEM 6.5로의 업그레이드와 관련된 개발 노력을 평가하는 역할을 할 수 있습니다.

## 설정 방법 {#how-to-set-up}

패턴 감지기는 로 별도로 릴리스됩니다. [패키지 1개](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65) 6.1에서 6.5 타겟팅 AEM 6.5 업그레이드로 소스 AEM 버전에서 작업할 수 있습니다. 다음을 사용하여 설치할 수 있습니다. [패키지 관리자](/help/sites-administering/package-manager.md).

## 사용 방법 {#how-to-use}

>[!NOTE]
>
>패턴 감지기는 로컬 개발 인스턴스를 포함하여 모든 환경에서 실행할 수 있습니다. 그러나 다음을 수행합니다.
>
>* 탐지율 향상
>* 비즈니스 크리티컬 인스턴스의 속도 저하 방지
>
>두 가지 모두 동시에 실행하는 것이 좋습니다. **스테이징 환경에서** 사용자 애플리케이션, 콘텐츠 및 구성 영역의 프로덕션 환경에 최대한 가깝습니다.

다음과 같은 여러 방법을 사용하여 패턴 감지기 출력을 확인할 수 있습니다.

* **Felix Inventory 콘솔을 통해:**

1. 을 찾아 AEM 웹 콘솔로 이동합니다. *https://serveraddress:serverport/system/console/configMgr*
1. 선택 **상태 - 패턴 탐지기** 아래 이미지에 표시된 대로:

   ![screenshot-2018-2-5pattern-detector](assets/screenshot-2018-2-5pattern-detector.png)

* **반응형 텍스트 기반 또는 일반 JSON 인터페이스를 통해**
* **각 행에 별도의 JSON 문서를 생성하는 **반응성 JSON 라인 인터페이스를 통해).

이 두 방법은 아래에 자세히 설명되어 있습니다.

## 반응형 인터페이스 {#reactive-interface}

반응형 인터페이스는 의혹이 감지되는 즉시 위반 신고 처리를 허용한다.

출력은 현재 2개의 URL에서 사용할 수 있습니다.

1. 일반 텍스트 인터페이스
1. JSON 인터페이스

## 일반 텍스트 인터페이스 처리 {#handling-the-plain-text-interface}

출력의 정보는 일련의 이벤트 항목으로 서식이 지정됩니다. 두 가지 채널이 있습니다. 하나는 게시 위반에 대한 것이고 다른 하나는 현재 진행률을 게시하기 위한 것입니다.

다음 명령을 사용하여 가져올 수 있습니다.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

출력은 다음과 같이 표시됩니다.

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

진행률은 다음을 사용하여 필터링할 수 있습니다. `grep` 명령:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

그 결과 다음과 같은 결과가 나옵니다.

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## JSON 인터페이스 처리 {#handling-the-json-interface}

마찬가지로 JSON은 [jq 도구](https://stedolan.github.io/jq/) 게시되는 즉시.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

출력:

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

진행률은 5초마다 보고되며 의심으로 표시된 메시지 이외의 다른 메시지를 제외하여 가져올 수 있습니다.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

출력:

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
>권장되는 방법은 curl의 전체 출력을 파일에 저장한 다음 를 통해 처리하는 것입니다. `jq` 또는 `grep` 을 클릭하여 정보 유형을 필터링하십시오.

## 감지 범위 {#scope}

현재 패턴 감지기를 사용하여 다음을 확인할 수 있습니다.

* OSGi 번들 내보내기 및 가져오기 불일치
* Sling 리소스 유형 및 슈퍼 유형(검색 경로 컨텐츠 오버레이 포함) 오버레이
* oak 색인의 정의(호환성)
* VLT 패키지(초과 사용)
* rep:사용자 노드 호환성(OAuth 구성 컨텍스트)

>[!NOTE]
>
>패턴 감지기는 업그레이드에 대한 경고를 정확하게 예측하려고 합니다. 그러나 일부 시나리오에서는 긍정 오류(false positive)가 생성될 수 있습니다.
