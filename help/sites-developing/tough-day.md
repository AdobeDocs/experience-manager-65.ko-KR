---
title: Tough Day
seo-title: Tough Day
description: Tough Day 테스트는 모든 작업이 동시에 진행되는 최악의 상황에서 약 1000명의 작성자가 매일 로드하는 것을 시뮬레이션합니다.
seo-description: The Tough Day test simulates the daily load of around 1000 authors in a worst-case scenario with all the operations going on at the same time.
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: 0b1f28963d9294c7aa9ae45c6b9fc9a9b8b4f6e6
workflow-type: tm+mt
source-wordcount: '1879'
ht-degree: 2%

---

# Tough Day{#tough-day}

## Tough Day 2 {#what-is-tough-day}

&quot;Tough Day 2&quot;는 AEM 인스턴스의 한계를 테스트할 수 있는 애플리케이션입니다. 기본 테스트 세트로 즉시 실행하거나 테스트 요구 사항에 맞게 구성할 수 있습니다. 구경하실 수 있습니다 [이 기록](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-toughday2-stress-testing-benchmarking-tool.html) 응용 프로그램 프레젠테이션

>[!CAUTION]
>
>Tough Day 2 는 Java 8이 필요합니다.

## Tough Day 2 실행 방법 {#how-to-run-tough-day}

Tough Day 2의 최신 버전을 [Adobe 저장소](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). 애플리케이션을 다운로드한 후에는 `host` 매개 변수. 다음 예에서는 AEM 인스턴스가 로컬로 실행되어 `localhost` 값이 사용됨:

```xml
java -jar toughday2.jar --host=localhost
```

매개 변수를 추가한 후 실행되는 기본 세트의 이름은 다음과 같습니다 `toughday`. 여기에는 다음 사용 사례가 포함되어 있습니다.

* 페이지 및 Live Copy 만들기(롤아웃 포함)
* 홈 페이지 가져오기
* QueryBuilder에서 쿼리 실행
* 자산 계층 만들기
* 자산 삭제

제품군에는 15% 쓰기 작업과 85% 읽기 작업이 포함되어 있습니다.

세트 테스트를 실행하려면 Tough Day 2가 기본 컨텐츠 패키지를 설치합니다. 이 기능은 `installsamplecontent`매개 변수 대상 `false`, 그러나 실행하려는 테스트에 대한 기본 경로를 변경해야 합니다. jar가 매개 변수 없이 실행되면 Tough Day 2에 [도움말 정보](/help/sites-developing/tough-day.md#getting-help).

일반적인 규칙에서는 다음 패턴을 사용하여 응용 프로그램을 사용할 수 있습니다.

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Tough Day 2 는 정리 단계를 포함하지 않습니다. 따라서 주 프로덕션 인스턴스가 아닌 복제된 스테이징 인스턴스에서 Tough Day 2를 실행하는 것이 좋습니다. 스테이징 인스턴스는 테스트 후에 삭제해야 합니다.

### 도움 받기 {#getting-help}

Tough Day 2는 명령줄에서 액세스할 수 있는 다양한 도움말 옵션을 제공합니다. 예:

```xml
java -jar toughday2.jar --help_full
```

아래 표에는 관련 도움말 매개 변수가 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>매개 변수</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예</strong></td>
  </tr>
  <tr>
   <td>--도움말</td>
   <td>다음과 같이 글로벌 정보를 인쇄합니다. 사용 가능한 작업, 사전 정의된 세트, 실행 모드 및 글로벌 매개 변수.</td>
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
   <td>위의 모든 것, 테스트, 게시자 및 세트 구성 요소를 인쇄합니다.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;mode&gt;</td>
   <td>지정된 실행 또는 게시 모드에 대한 정보를 나열합니다.</td>
   <td><p>java -jar touchday2.jar —help —runmode type=constantload</p> <p>java -jar touchday2.jar —help —publishmode type=interval</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;suitename&gt;</td>
   <td>지정된 세트의 모든 테스트 및 해당 구성 가능한 속성을 나열합니다.</td>
   <td><br /> java -jar touchday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;tag&gt;</td>
   <td><br /> 지정된 태그가 있는 모든 항목을 나열합니다.</td>
   <td>java -jar touchday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;testclass publisherclass=""&gt;</td>
   <td><br /> 지정된 테스트 또는 게시자에 대해 구성 가능한 모든 속성을 나열합니다.</td>
   <td><p>java -jar toughday2.jar - help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### 글로벌 매개 변수 {#global-parameters}

Tough Day 2는 테스트에 대한 환경을 설정하거나 변경하는 전역 매개 변수를 제공합니다. 여기에는 타겟팅된 호스트, 포트 번호, 사용된 프로토콜, 인스턴스에 대한 사용자 및 암호 등이 포함됩니다. 예:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

아래의 목록에서 관련 매개 변수를 찾을 수 있습니다.

| **매개 변수** | **설명** | **기본 값** | **가능한 값** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | 기본 Tough Day 2 컨텐츠 패키지를 설치하거나 건너뜁니다. | true | true 또는 false |
| `--protocol=<Val>` | 호스트에 사용되는 프로토콜입니다. | http | http 또는 https |
| `--host=<Val>` | 타깃팅할 호스트 이름 또는 IP입니다. |  |  |
| `--port=<Val>` | 호스트의 포트입니다. | 4502년 |  |
| `--user=<Val>` | 인스턴스에 대한 사용자 이름입니다. | admin |  |
| `--password=<Val>` | 지정된 사용자의 암호입니다. | 관리 |  |
| `--duration=<Val>` | 테스트 기간입니다. ()으로 표시할 수 있습니다.**s**)초, (**m**)은&#x200B;**h**)과 (**d**)에 사용할 수 있습니다. | 1d |  |
| `--timeout=<Val>` | 테스트가 중단되고 실패로 표시되기 전에 실행되는 기간입니다. 초 단위로 표시됩니다. | 180 |  |
| `--suite=<Val>` | 이 값은 사전 정의된 테스트 세트의 하나 또는 목록(쉼표로 구분)일 수 있습니다. | 인성 |  |
| `--configfile=<Val>` | 타깃팅된 YAML 구성 파일입니다. |  |  |
| `--contextpath=<Val>` | 인스턴스의 컨텍스트 경로입니다. |  |  |
| `--loglevel=<Val>` | Tough Day 2 엔진의 로그 수준입니다. | 정보 | 모두, 디버그, 정보, 경고, 오류, 치명적, 해제 |
| `--dryrun=<Val>` | true이면 결과 구성을 인쇄하고 테스트를 실행하지 않습니다. | false | true 또는 false |

## 사용자 지정 {#customizing}

사용자 지정은 다음 두 가지 방법으로 수행할 수 있습니다. 명령줄 매개 변수 또는 yaml 구성 파일 **구성 파일은 일반적으로 큰 사용자 지정 세트에 사용되며 Tough Day 2 기본 매개 변수를 무시합니다. 명령줄 매개 변수는 구성 파일과 기본 매개 변수를 모두 덮어씁니다.**

테스트 구성을 저장하는 유일한 방법은 yaml 형식으로 복사하는 것입니다. 자세한 내용은 다음을 참조하십시오 [touday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) 구성 및 기본 구성 예는 아래 섹션에 있습니다.

### 새 테스트 추가 {#adding-a-new-test}

기본값을 사용하지 않으려면 `toughday` suite를 사용하여 원하는 테스트를 추가할 수 있습니다 `add` 매개 변수. 아래 예는 를 추가하는 방법을 보여줍니다. `CreateAssetTreeTest` 명령줄 매개 변수 또는 yaml 구성 파일을 사용하여 테스트합니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

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

동일한 테스트의 여러 인스턴스를 추가하고 실행할 수도 있지만 각 인스턴스의 이름은 고유해야 합니다. 아래 예제는 명령줄 매개 변수 또는 yaml 구성 파일을 사용하여 동일한 테스트의 두 인스턴스를 추가하는 방법을 보여줍니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

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

테스트 속성 중 하나 이상을 변경해야 하는 경우 해당 속성을 명령줄 또는 yaml 구성 파일에 추가할 수 있습니다. 사용 가능한 모든 테스트 속성을 보려면 `--help <TestClass/PublisherClass>` 명령줄에서 매개 변수(예:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Yaml 구성 파일은 Tough Day 2 기본 매개 변수와 명령줄 매개 변수가 구성 파일과 기본값을 모두 덮어씁니다.

아래 예는 를 변경하는 방법을 보여줍니다. `template` 에 대한 속성 `CreatePageTreeTest` 명령줄 매개 변수 또는 yaml 구성 파일을 사용하여 테스트합니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

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

를 사용하여 사전 정의된 세트에 새 테스트를 추가할 수 있습니다 `add` 매개 변수 및 타깃팅된 사전 정의된 세트 지정.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

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

지정된 세트의 기존 테스트도 `config`* *매개 변수. 테스트 클래스 이름이 아닌 테스트의 세트 이름과 실제 이름을 지정해야 합니다. 에서 테스트 이름을 찾을 수 있습니다. `name` 테스트 클래스의 속성입니다. 테스트 속성을 찾는 방법에 대한 자세한 내용은 [테스트 속성 변경](/help/sites-developing/tough-day.md#changing-the-test-properties) 섹션을 참조하십시오.

아래 예에는 `CreatePageTreeTest` (이름이 지정됨) `UploadAsset`)이 &quot;새 자산&quot;으로 변경되었습니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

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

또한, `exclude` 매개 변수. 테스트 C가 아니라 테스트 이름과 실제 이름을 지정해야 합니다 `lass` name)으로 그룹화됩니다. 에서 테스트 이름을 찾을 수 있습니다. `name` 테스트 클래스의 속성입니다. 아래 예에서는 `CreatePageTreeTest` (이름이 지정됨) `UploadAsset`) 테스트가 toughday suite에서 제거됩니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

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

Tough Day 2는 다음 모드 중 하나로 실행될 수 있습니다. **정상** 및 **상수 로드**.

다음 **정상** 실행 모드에는 두 가지 매개 변수가 있습니다.

* `concurrency` - concurrency는 Tough Day 2가 테스트 실행을 위해 만들 스레드 수를 나타냅니다. 이러한 스레드에서 테스트가 더 이상 실행할 테스트가 없을 때까지 실행됩니다.

* `waittime` - 동일한 스레드에서 두 개의 연속 테스트 실행 사이의 대기 시간입니다. 값은 밀리초 단위로 표시되어야 합니다.

아래 예제는 명령줄을 사용하여 매개 변수를 추가하는 방법을 보여 줍니다.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

또는 yaml 구성 파일을 사용하여 다음을 수행하십시오.

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

다음 **상수 로드** 실행 모드는 스레드 수가 일정하지 않고 시작된 테스트 실행을 일정하게 생성하여 일반 실행 모드와 다릅니다. 동일한 이름의 실행 모드 매개 변수를 사용하여 로드를 설정할 수 있습니다.

### 선택 테스트 {#test-selection}

테스트 선택 프로세스는 실행 모드 모두에 대해 동일하며 다음과 같습니다. 모든 테스트에 `weight` 스레드에서 실행 가능성을 결정하는 속성입니다. 예를 들어, 두 개의 테스트가 있는데, 하나는 가중치가 5이고 다른 하나는 가중치가 10인 경우, 후자는 이전의 것보다 두 배 더 많이 실행될 가능성이 있습니다.

또한 테스트에는 `count` 속성. 지정된 수로 실행 횟수를 제한합니다. 이 번호가 전달되면 더 이상 테스트가 실행되지 않습니다. 이미 실행 중인 모든 테스트 인스턴스는 구성된 대로 실행을 완료합니다. 다음 예제에서는 명령줄에 이러한 매개 변수를 추가하거나 yaml 구성 파일을 사용하여 이러한 매개 변수를 추가하는 방법을 보여 줍니다.

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
>병렬 실행으로 인해 실제 테스트 실행 수가 `count` 매개 변수. 실행 중인 스레드 수(다음으로 제어됨)에 비례하는 편차를 예상합니다. `concurrency parameter`).

### 시험 실행 {#dry-run}

연습 실행은 지정된 모든 입력(명령줄 매개 변수 또는 구성 파일)을 구문 분석하고, 기본값으로 병합한 다음 결과를 출력합니다. 테스트를 실행하지 않습니다.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 출력 {#output}

Tough Day 2는 테스트 지표와 로그를 모두 출력합니다. 자세한 내용은 다음 섹션을 참조하십시오.

### 테스트 지표 {#test-metrics}

Tough Day 2 는 현재 사용자가 평가할 수 있는 9개의 테스트 지표를 보고합니다. 을 사용하는 지표 ***** 기호는 성공적인 실행 후에만 보고됩니다.

| **이름** | **설명** |
|---|---|
| Timestamp | 마지막으로 완료된 테스트 실행의 타임스탬프입니다. |
| 전달됨 | 성공한 실행 수입니다. |
| 실패 | 실패한 실행 수입니다. |
| 최소* | 테스트 실행 시간이 가장 짧습니다. |
| 최대* | 테스트 실행 최대 기간입니다. |
| 중간* | 모든 테스트 실행의 평균 기간을 계산했습니다. |
| 평균* | 모든 테스트 실행의 계산된 평균 기간입니다. |
| StdDev* | 표준 편차. |
| 90p* | 90번째 백분위수. |
| 99p* | 99번째 백분위수. |
| 99.9p* | 99.9백분위수. |
| 실제 처리량* | 경과된 실행 시간으로 나눈 실행 수입니다. |

이러한 지표는 와 함께 추가할 수 있는 게시자의 도움을 받아 작성됩니다 `add` 매개 변수(테스트 추가와 유사) 현재, 다음 두 가지 옵션이 있습니다.

* **CSVPublisher** - 출력이 CSV 파일입니다.
* **콘솔 게시자** - 출력이 콘솔에 표시됩니다.

기본적으로 두 게시자가 모두 활성화되어 있습니다.

또한 지표를 보고하는 두 가지 모드가 있습니다.

* 다음 **단순** 게시 모드 - 실행 시작부터 게시 시점까지 결과를 보고합니다.
* 다음 **간격** 게시 모드 - 결과를 지정된 기간에 보고합니다. 을 사용하여 기간을 설정할 수 있습니다 **간격** 게시 모드 매개 변수.

다음 예는 를 구성하는 방법을 보여줍니다. `intervals` 매개 변수(명령줄 또는 yaml 구성 파일 사용)를 참조하십시오.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

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

Tough Day 2 는 Tough Day 2 를 실행한 동일한 디렉토리에 로그 폴더를 만듭니다. 이 폴더에는 두 가지 유형의 로그가 포함되어 있습니다.

* **toughday.log**: 응용 프로그램 상태, 디버깅 정보 및 글로벌 메시지와 관련된 메시지를 포함합니다.
* **toughday_&lt;testname>.log**: 지정된 테스트와 관련된 메시지입니다.

로그를 덮어쓰지 않고 후속 실행에서 기존 로그에 메시지를 추가합니다. 로그에는 몇 가지 수준이 있습니다. 자세한 내용은 ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
