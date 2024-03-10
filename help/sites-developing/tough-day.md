---
title: Tough Day
description: Tough Day 테스트는 모든 작업이 동시에 진행되는 최악의 상황에서 작성자 1000명의 일일 부하를 시뮬레이션합니다.
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 1%

---

# Tough Day{#tough-day}

## 힘든 하루 2 {#what-is-tough-day}

&quot;Tough Day 2&quot;는 AEM 인스턴스의 제한을 강조할 수 있는 애플리케이션입니다. 기본 테스트 도구 모음을 사용하여 즉시 실행하거나 테스트 요구 사항에 맞게 구성할 수 있습니다. 볼 수 있습니다. [이 녹음/녹화](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html) 응용 프로그램 프레젠테이션용

>[!CAUTION]
>
>Tough Day 2에는 Java™ 8이 필요합니다.

## How to Run Tough Day 2 {#how-to-run-tough-day}

에서 Tough Day 2 최신 버전을 다운로드하십시오. [Adobe 저장소](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). 응용 프로그램을 다운로드한 후 다음을 제공하여 즉시 실행할 수 있습니다. `host` 매개 변수. 다음 예에서는 AEM 인스턴스가 로컬로 실행되므로 `localhost` 값이 사용됨:

```xml
java -jar toughday2.jar --host=localhost
```

매개 변수를 추가한 후에 실행되는 기본 세트 이름은 입니다 `toughday`. 여기에는 다음과 같은 사용 사례가 포함되어 있습니다.

* 페이지 및 라이브 카피 만들기(롤아웃 포함)
* 홈 페이지 가져오기
* queryBuilder에서 쿼리 실행
* 자산 계층 만들기
* 에셋 삭제

이 제품군에는 15%의 쓰기 작업과 85%의 읽기 작업이 포함되어 있습니다.

Suite 테스트를 실행하기 위해 Tough Day 2는 기본 콘텐츠 패키지를 설치합니다. 다음을 설정하여 이를 방지할 수 있습니다. `installsamplecontent`매개 변수 `false`, 하지만 실행하려는 테스트의 기본 경로도 변경해야 합니다. jar가 매개 변수 없이 실행되면 Tough Day 2에 [도움말 정보](/help/sites-developing/tough-day.md#getting-help).

일반적으로 다음 패턴을 따라 애플리케이션을 사용할 수 있습니다.

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Tough Day 2에는 정리 단계가 없습니다. 따라서 주 프로덕션 인스턴스가 아닌 복제된 스테이징 인스턴스에서 Tough Day 2를 실행하는 것이 좋습니다. 테스트 후에 스테이징 인스턴스를 삭제해야 합니다.
>

### 도움말 보기 {#getting-help}

Tough Day 2는 명령줄에서 액세스할 수 있는 다양한 도움말 옵션을 제공합니다. 예:

```xml
java -jar toughday2.jar --help_full
```

아래 표에서 관련 도움말 매개 변수를 찾을 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>매개변수</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예</strong></td>
  </tr>
  <tr>
   <td>—도움말</td>
   <td>사용 가능한 작업, 사전 정의된 세트, 실행 모드 및 글로벌 매개 변수와 같은 글로벌 정보를 인쇄합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>사용 가능한 모든 게시자를 인쇄합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>테스트 클래스와 해당 설명을 인쇄합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>위의 모든 항목과 테스트, 게시자 및 세트 구성 요소를 인쇄합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode 유형=&lt;mode&gt;</td>
   <td>지정된 실행 또는 게시 모드에 대한 정보를 나열합니다.</td>
   <td><p>Java™ -jar toughday2.jar —help —runmode type=constantload</p> <p>Java™ -jar toughday2.jar —help —publishmode type=interval</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;suitename&gt;</td>
   <td>주어진 세트의 모든 테스트와 각 구성 가능한 속성을 나열합니다.</td>
   <td><br /> Java™ -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;tag&gt;</td>
   <td><br /> 지정된 태그가 있는 모든 항목을 나열합니다.</td>
   <td>Java™ -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—도움말 &lt;testclass publisherclass=""&gt;</td>
   <td><br /> 주어진 테스트 또는 게시자에 대해 구성 가능한 모든 속성을 나열합니다.</td>
   <td><p>Java™ -jar toughday2.jar —help UploadPDFTest</p> <p>Java™ -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### 전역 매개 변수 {#global-parameters}

Tough Day 2는 테스트에 대한 환경을 설정하거나 변경하는 글로벌 매개 변수를 제공합니다. 여기에는 타겟팅되는 호스트, 포트 번호, 사용된 프로토콜, 인스턴스에 대한 사용자 및 암호 등이 포함됩니다. 예:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

아래 목록에서 관련 매개변수를 찾을 수 있습니다.

| **매개 변수** | **설명** | **기본값** | **가능한 값** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | 기본 Tough Day 2 콘텐츠 패키지를 설치하거나 건너뜁니다. | true | true 또는 false |
| `--protocol=<Val>` | 호스트에 사용되는 프로토콜입니다. | http | http 또는 https |
| `--host=<Val>` | 타겟팅할 호스트 이름 또는 IP입니다. |  |  |
| `--port=<Val>` | 호스트의 포트입니다. | 4502 |  |
| `--user=<Val>` | 인스턴스의 사용자 이름입니다. | admin |  |
| `--password=<Val>` | 지정된 사용자의 암호입니다. | admin |  |
| `--duration=<Val>` | 테스트 기간. 다음에서 표현할 수 있습니다. **s**&#x200B;통화, **m**&#x200B;잠시 후 **h**&#x200B;및 **d** ays. | 1d |  |
| `--timeout=<Val>` | 테스트가 중단되고 실패로 표시되기 전까지 테스트가 실행되는 시간입니다. 초 단위로 표시됩니다. | 180 |  |
| `--suite=<Val>` | 값은 하나 또는 사전 정의된 테스트 세트의 목록(쉼표로 구분)일 수 있습니다. | 힘든 날 |  |
| `--configfile=<Val>` | 타겟팅된 yaml 구성 파일입니다. |  |  |
| `--contextpath=<Val>` | 인스턴스의 컨텍스트 경로. |  |  |
| `--loglevel=<Val>` | Tough Day 2 엔진의 로그 수준입니다. | 정보 | 모두, 디버그, 정보, 경고, 오류, 치명적, 해제 |
| `--dryrun=<Val>` | true이면 결과 구성을 인쇄하고 테스트를 실행하지 않습니다. | false | true 또는 false |

## 사용자 정의 {#customizing}

사용자 지정은 명령줄 매개 변수 또는 yaml 구성 파일의 두 가지 방법으로 수행할 수 있습니다. **구성 파일은 대규모 사용자 정의 세트에 사용되며 Tough Day 2 기본 매개 변수를 재정의합니다. 명령줄 매개 변수는 구성 파일과 기본 매개 변수를 모두 재정의합니다.**

테스트 구성을 저장하는 유일한 방법은 yaml 형식으로 복사하는 것입니다.

### 새 테스트 추가 {#adding-a-new-test}

기본값을 사용하지 않으려면 `toughday` 제품군 을 사용하여 선택한 테스트를 추가할 수 있습니다. `add` 매개 변수. 아래 예는 를 추가하는 방법을 보여줍니다. `CreateAssetTreeTest` 명령줄 매개 변수 또는 yaml 구성 파일을 사용하여 테스트합니다.

명령줄 매개 변수 사용:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

yaml 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### 동일한 테스트의 여러 인스턴스 추가  {#adding-multiple-instances-of-the-same-test}

동일한 테스트의 여러 인스턴스를 추가하고 실행할 수도 있지만 각 인스턴스의 이름은 고유해야 합니다. 아래 예는 명령줄 매개 변수 또는 yaml 구성 파일을 사용하여 동일한 테스트의 두 인스턴스를 추가하는 방법을 보여 줍니다.

명령줄 매개 변수 사용:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

yaml 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### 테스트 속성 변경 {#changing-the-test-properties}

하나 이상의 테스트 속성을 변경해야 하는 경우 해당 속성을 명령줄 또는 yaml 구성 파일에 추가할 수 있습니다. 사용 가능한 모든 테스트 속성을 보려면 `--help <TestClass/PublisherClass>` 매개 변수를 명령줄에 추가합니다. 예:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Yaml 구성 파일은 Tough Day 2 기본 매개변수를 덮어쓰고 명령줄 매개변수는 구성 파일과 기본값을 모두 재정의합니다.

아래 예는 를 변경하는 방법을 보여 줍니다. `template` 속성 `CreatePageTreeTest` 명령줄 매개 변수 또는 yaml 구성 파일을 사용하여 테스트합니다.

명령줄 매개 변수 사용:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

yaml 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### 사전 정의된 테스트 세트 작업 {#working-with-predefined-test-suites}

아래 예는 사전 정의된 세트에 테스트를 추가하는 방법과 사전 정의된 세트에서 기존 테스트를 다시 구성하고 제외하는 방법을 보여줍니다.

다음을 사용하여 사전 정의된 세트에 새 테스트를 추가할 수 있습니다. `add` 매개 변수 및 타겟팅된 사전 정의된 세트를 지정합니다.

명령줄 매개 변수 사용:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

yaml 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

주어진 세트의 기존 테스트는 `config`* *매개 변수. 또한 테스트 클래스 이름이 아닌 테스트 세트 이름과 실제 이름을 지정합니다. 테스트 이름은 `name` Test 클래스의 속성입니다. 테스트 속성을 찾는 방법에 대한 자세한 내용은 [테스트 속성 변경](/help/sites-developing/tough-day.md#changing-the-test-properties) 섹션.

아래 예에서 의 기본 에셋 제목 `CreatePageTreeTest` (명명된) `UploadAsset`)이 &quot;NewAsset&quot;로 변경되었습니다.

명령줄 매개 변수 사용:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

yaml 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

또한 을 사용하여 기본 구성에서 사전 정의된 세트 또는 게시자에서 테스트를 제거할 수도 있습니다. `exclude` 매개 변수. 또한 테스트 C가 아닌 세트 이름과 테스트의 실제 이름을 지정합니다 `lass` name). 테스트 이름은 `name` 테스트 클래스의 속성입니다. 아래 예에서는 `CreatePageTreeTest` (명명된) `UploadAsset`) 테스트를 toughday suite에서 제거합니다.

명령줄 매개 변수 사용:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

yaml 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### 실행 모드 {#run-modes}

Tough Day 2는 다음 모드 중 하나로 실행할 수 있습니다. **표준** 및 **정하중**.

다음 **표준** 실행 모드에는 두 개의 매개 변수가 있습니다.

* `concurrency` - 동시성은 Tough Day 2가 테스트 실행을 위해 만들 스레드 수를 나타냅니다. 이러한 스레드에서는 기간이 만료되거나 실행할 테스트가 더 이상 없을 때까지 테스트가 실행됩니다.

* `waittime` - 동일한 스레드에서 두 개의 연속 테스트 실행 사이의 대기 시간입니다. 값은 밀리초 단위로 표현해야 합니다.

아래 예는 명령줄을 사용하여 매개 변수를 추가하는 방법을 보여줍니다.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

또는 yaml 구성 파일을 사용하여 다음을 수행합니다.

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

다음 **정하중** 실행 모드는 일반 실행 모드와 다릅니다. 시작된 테스트 실행의 개수가 일정하지 않고 스레드의 개수가 일정합니다. 같은 이름의 실행 모드 매개변수를 사용하여 로드를 설정할 수 있습니다.

### 테스트 선택 {#test-selection}

테스트 선택 프로세스는 두 실행 모드 모두에 대해 동일하며 다음과 같이 진행됩니다. 모든 테스트에는 `weight` 스레드에서 실행될 가능성을 결정하는 속성입니다. 예를 들어 가중치가 5인 테스트와 가중치가 10인 테스트가 두 개 있는 경우 후자가 전자 테스트보다 두 배 더 많이 실행될 가능성이 있습니다.

또한 검사에는 다음이 있을 수 있습니다. `count` 속성, 실행 수를 지정된 숫자로 제한합니다. 이 숫자가 전달되면 테스트가 더 이상 실행되지 않습니다. 이미 실행 중인 모든 테스트 인스턴스는 구성된 대로 실행을 완료합니다. 다음 예에서는 명령줄에서 또는 yaml 구성 파일을 사용하여 이러한 매개변수를 추가하는 방법을 보여 줍니다.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

또는

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
>병렬 실행으로 인해 실제 테스트 실행 수가 `count` 매개 변수. 실행 중인 스레드 수에 비례하는 편차 예상(에 의해 제어됨) `concurrency parameter`).

### 시험 실행 {#dry-run}

드라이 실행은 주어진 입력(명령줄 매개 변수 또는 구성 파일)을 모두 구문 분석하여 이를 기본값과 병합한 다음 결과를 출력합니다. 아무 테스트도 실행되지 않습니다.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 출력 {#output}

Tough Day 2는 테스트 지표와 로그를 모두 출력합니다. 자세한 내용은 다음 섹션을 참조하십시오.

### 테스트 지표 {#test-metrics}

Tough Day 2는 현재 평가할 수 있는 9개의 테스트 지표를 보고합니다. 를 사용하는 지표 **&#42;** 기호는 성공적으로 실행된 후에만 보고됩니다.

| **이름** | **설명** |
|---|---|
| 타임스탬프 | 마지막으로 완료된 테스트 실행의 타임스탬프입니다. |
| 전달됨 | 성공한 실행 수입니다. |
| 실패 | 실패한 실행 수입니다. |
| 분&#42; | 테스트 실행 기간이 가장 짧습니다. |
| 최대&#42; | 테스트 실행 기간이 가장 깁니다. |
| 중간값&#42; | 모든 테스트 실행의 계산된 중간 값입니다. |
| 평균&#42; | 모든 테스트 실행의 계산된 평균 기간입니다. |
| 표준 개발&#42; | 표준 편차입니다. |
| 90p&#42; | 90백분위수입니다. |
| 99p&#42; | 99백분위수입니다. |
| 99.9p&#42; | 99.9백분위수 |
| 실제 처리량&#42; | 실행 횟수를 경과 실행 시간으로 나눈 값입니다. |

이러한 지표는 게시자의 도움을 받아 작성되며 `add` 매개 변수(테스트 추가와 유사)입니다. 현재 다음 두 가지 옵션이 있습니다.

* **CSVPublisher** - 출력이 CSV 파일입니다.
* **ConsolePublisher** - 콘솔에 출력이 표시됩니다.

기본적으로 두 게시자가 모두 활성화됩니다.

또한 지표가 보고되는 두 가지 모드가 있습니다.

* 다음 **단순** 게시 모드 - 실행 시작부터 게시 시점까지의 결과를 보고합니다.
* 다음 **간격** 게시 모드 - 주어진 시간대에 결과를 보고합니다. 다음을 사용하여 기간을 설정할 수 있습니다. **간격** 게시 모드 매개 변수.

다음 예에서는 를 구성하는 방법을 보여 줍니다. `intervals` 명령줄에서 또는 yaml 구성 파일을 사용하여 매개변수를 설정합니다.

명령줄 매개 변수 사용:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

yaml 구성 파일을 사용하여 다음을 수행합니다.

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### 로깅 {#logging}

Tough Day 2는 Tough Day 2를 실행한 동일한 디렉터리에 로그 폴더를 만듭니다. 이 폴더에는 두 가지 유형의 로그가 있습니다.

* **toughday.log**: 애플리케이션 상태, 디버깅 정보 및 글로벌 메시지와 관련된 메시지가 포함되어 있습니다.
* **toughday_&lt;testname>.log**: 지정된 테스트와 관련된 메시지입니다.

로그는 덮어쓰지 않으며 후속 실행은 메시지를 기존 로그에 추가합니다. 로그에는 여러 수준이 있습니다. 자세한 내용은 다음을 참조하십시오. [loglevel 매개 변수.](#global-parameters).

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
