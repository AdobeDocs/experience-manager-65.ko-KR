---
title: Tough Day
seo-title: 힘든 날
description: 더티 데이 테스트는 모든 작업이 동시에 진행되는 최악의 시나리오에서 약 1000명의 작성자의 일일 로드를 시뮬레이션합니다.
seo-description: 더티 데이 테스트는 모든 작업이 동시에 진행되는 최악의 시나리오에서 약 1000명의 작성자의 일일 로드를 시뮬레이션합니다.
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 2%

---


# Tough Day{#tough-day}

## 힘든 날 2일 {#what-is-tough-day}

&quot;터프 데이 2&quot;는 AEM 인스턴스의 한계를 강조하게 하는 애플리케이션입니다. 기본 테스트 세트와 함께 실행되거나 테스트 요구 사항에 맞게 구성할 수 있습니다. 응용 프로그램의 프레젠테이션을 보려면 [이 레코딩](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html)을 볼 수 있습니다.

## 힘든 하루 2일을 실행하는 방법 {#how-to-run-tough-day}

[Adobe 저장소](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/)에서 최신 버전의 Touch Day 2를 다운로드합니다. 애플리케이션을 다운로드한 후 `host` 매개 변수를 제공하여 즉시 실행할 수 있습니다. 다음 예에서 AEM 인스턴스는 로컬로 실행되므로 `localhost` 값이 사용됩니다.

```xml
java -jar toughday2.jar --host=localhost
```

매개 변수를 추가한 후 실행되는 기본 세트의 이름은 `toughday`입니다. 여기에는 다음과 같은 사용 사례가 포함됩니다.

* 페이지 및 Live Copy 만들기(롤아웃 포함)
* 홈 페이지 가져오기
* queryBuilder에서 쿼리 실행
* 자산 계층 만들기
* 자산 삭제

제품군에는 15%의 쓰기 작업과 85%의 읽기 작업이 포함되어 있습니다.

패키지 테스트를 실행하기 위해 Touch Day 2는 기본 컨텐츠 패키지를 설치합니다. 이 옵션은 `installsamplecontent`매개 변수를 `false`로 설정하면 방지할 수 있지만 실행하려는 테스트의 기본 경로도 변경해야 합니다. jar가 매개 변수 없이 실행되는 경우 Touch Day 2는 [도움말 정보](/help/sites-developing/tough-day.md#getting-help)를 표시합니다.

일반적인 규칙으로, 다음 패턴을 사용하여 응용 프로그램을 사용할 수 있습니다.

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>힘든 2일은 정리된 단계가 아니다. 따라서 기본 프로덕션 인스턴스가 아닌 복제된 스테이징 인스턴스에서 Touch Day 2를 실행하는 것이 좋습니다. 테스트 후에 스테이징 인스턴스를 삭제해야 합니다.


### 도움 받기 {#getting-help}

터프한 요일 2는 명령줄에서 액세스할 수 있는 다양한 도움말 옵션을 제공합니다. 예:

```xml
java -jar toughday2.jar --help_full
```

아래 표에서 관련 도움말 매개 변수를 찾을 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>매개 변수</strong></td>
   <td><strong>설명</strong></td>
   <td><strong>예</strong></td>
  </tr>
  <tr>
   <td>--도움말</td>
   <td>글로벌 정보를 인쇄합니다(예:사용 가능한 작업, 사전 정의된 세트, 실행 모드 및 글로벌 매개 변수.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>사용 가능한 모든 발행자를 인쇄합니다.</td>
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
   <td> —help —runmode/publishmode type=&lt;모드&gt;</td>
   <td>지정된 실행 또는 게시 모드에 대한 정보를 나열합니다.</td>
   <td><p>java -jar touchday2.jar —help —runmode type=constantload</p> <p>java -jar touchday2.jar —help —publishmode type=간격</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;SuiteName&gt;</td>
   <td>지정된 세트의 모든 테스트 및 해당 구성 가능한 속성을 나열합니다.</td>
   <td><br /> java -jar touchday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;태그&gt;</td>
   <td><br /> 지정된 태그가 있는 모든 항목을 나열합니다.</td>
   <td>java -jar sighday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> 지정된 테스트 또는 게시자에 대한 구성 가능한 모든 속성을 나열합니다.</td>
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### 전역 매개 변수 {#global-parameters}

Touch Day 2는 테스트의 환경을 설정하거나 변경하는 글로벌 매개 변수를 제공합니다. 여기에는 타깃팅된 호스트, 포트 번호, 사용된 프로토콜, 인스턴스에 대한 사용자 및 암호 등이 포함됩니다. 예:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

목록에서 관련 매개 변수를 찾을 수 있습니다.

| **매개 변수** | **설명** | **기본 값** | **가능한 값** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | 기본 Touch Day 2 콘텐츠 패키지를 설치하거나 건너뜁니다. | true | true 또는 false |
| `--protocol=<Val>` | 호스트에 사용되는 프로토콜입니다. | http | http 또는 https |
| `--host=<Val>` | 타깃팅할 호스트 이름 또는 IP. |  |  |
| `--port=<Val>` | 호스트의 포트입니다. | 4502년 |  |
| `--user=<Val>` | 인스턴스의 사용자 이름입니다. | admin |  |
| `--password=<Val>` | 지정된 사용자의 암호입니다. | admin |  |
| `--duration=<Val>` | 테스트의 지속 시간입니다. (**s**)초, (**m**)분, (**h**)시간 및 (**d**)일)로 표시할 수 있습니다. | 1d |  |
| `--timeout=<Val>` | 테스트가 중단되고 실패로 표시되기 전에 실행되는 시간입니다. 초 단위로 표현됩니다. | 180 |  |
| `--suite=<Val>` | 이 값은 사전 정의된 테스트 세트의 하나 또는 목록(쉼표로 구분)일 수 있습니다. | 힘든 날 |  |
| `--configfile=<Val>` | 타깃팅된 YAML 구성 파일입니다. |  |  |
| `--contextpath=<Val>` | 인스턴스의 컨텍스트 경로. |  |  |
| `--loglevel=<Val>` | Touch Day 2 엔진의 로그 수준. | 정보 | 모두, 디버그, 정보, 경고, 오류, 치명적, 해제 |
| `--dryrun=<Val>` | true이면 결과 구성을 인쇄하고 테스트를 실행하지 않습니다. | false | true 또는 false |

## {#customizing} 사용자 지정

사용자 지정은 다음 두 가지 방법으로 수행할 수 있습니다.명령줄 매개 변수 또는 yaml 구성 파일. **구성 파일은 일반적으로 대규모 사용자 정의 세트에 사용되며, Touch Day 2 기본 매개 변수를 무시합니다. 명령줄 매개 변수는 구성 파일과 기본 매개 변수를 모두 무시합니다.**

테스트 구성을 저장하는 유일한 방법은 YAML 형식으로 복사하는 것입니다. 자세한 내용은 아래 섹션의 [compenday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) 구성 및 YAML 구성 예제를 참조하십시오.

### 새 테스트 {#adding-a-new-test} 추가

기본 `toughday` 세트를 사용하지 않으려면 `add` 매개 변수를 사용하여 선택한 테스트를 추가할 수 있습니다. 아래 예제는 명령줄 매개 변수 또는 YAML 구성 파일을 사용하여 `CreateAssetTreeTest` 테스트를 추가하는 방법을 보여줍니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

YAML 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### 동일한 테스트 {#adding-multiple-instances-of-the-same-test}의 여러 인스턴스 추가

동일한 테스트의 여러 인스턴스를 추가하고 실행할 수도 있지만 각 인스턴스에는 고유한 이름이 있어야 합니다. 아래 예제는 명령줄 매개 변수 또는 YAML 구성 파일을 사용하여 동일한 테스트의 두 인스턴스를 추가하는 방법을 보여줍니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

YAML 구성 파일을 사용하여 다음을 수행합니다.

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

### 테스트 속성 {#changing-the-test-properties} 변경

하나 이상의 테스트 속성을 변경해야 하는 경우 해당 속성을 명령줄 또는 YAML 구성 파일에 추가할 수 있습니다. 사용 가능한 모든 테스트 속성을 보려면 명령줄에 `--help <TestClass/PublisherClass>` 매개 변수를 추가합니다. 예:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Yaml 구성 파일이 Touch Day 2 기본 매개 변수를 덮어쓰고 명령줄 매개 변수가 구성 파일과 기본값을 모두 덮어씁니다.

아래 예제는 명령줄 매개 변수 또는 YAML 구성 파일을 사용하여 `CreatePageTreeTest` 테스트의 `template` 속성을 변경하는 방법을 보여줍니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

YAML 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### 사전 정의된 테스트 세트 작업 {#working-with-predefined-test-suites}

아래 예제는 사전 정의된 세트에 테스트를 추가하는 방법과 사전 정의된 세트에서 기존 테스트를 재구성하고 제외하는 방법을 보여줍니다.

`add` 매개 변수를 사용하고 타깃팅된 사전 정의된 세트를 지정하여 사전 정의된 세트에 새 테스트를 추가할 수 있습니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

YAML 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

지정된 세트의 기존 테스트는 `config`* *매개 변수를 사용하여 다시 구성할 수도 있습니다. 테스트 클래스 이름이 아니라 테스트 세트 이름과 실제 이름을 지정해야 합니다. 테스트 클래스의 `name` 속성에서 테스트 이름을 찾을 수 있습니다. 테스트 속성을 찾는 방법에 대한 자세한 내용은 [테스트 속성 변경](/help/sites-developing/tough-day.md#changing-the-test-properties) 섹션을 참조하십시오.

아래 예에서 `CreatePageTreeTest`(이름 `UploadAsset`)의 기본 자산 제목이 &quot;NewAsset&quot;으로 변경되었습니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

YAML 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

또한 `exclude` 매개 변수를 사용하여 사전 정의된 세트 또는 게시자에서 테스트를 기본 구성에서 제거할 수도 있습니다. 테스트 C `lass` 이름이 아닌 세트 이름과 실제 테스트 이름을 지정해야 합니다. 테스트 클래스의 `name` 속성에서 테스트 이름을 찾을 수 있습니다. 아래 예에서 `CreatePageTreeTest`(이름 `UploadAsset`) 테스트는 Started Suite에서 제거됩니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

YAML 구성 파일을 사용하여 다음을 수행합니다.

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### 실행 모드 {#run-modes}

터프한 2일은 다음 모드 중 하나를 실행할 수 있습니다.**normal** 및 **상수 load**.

**normal** 실행 모드에는 두 개의 매개 변수가 있습니다.

* `concurrency` - concurrency는 Touch Day 2가 테스트 실행을 위해 만들 스레드의 수를 나타냅니다. 이러한 스레드에서 테스트는 기간이 초과되었거나 더 이상 실행할 테스트가 없을 때까지 실행됩니다.

* `waittime` - 동일한 스레드에서 두 개의 연속 테스트 실행 사이의 대기 시간입니다. 값은 밀리초 단위로 표현되어야 합니다.

아래 예에서는 명령줄 중 하나를 사용하여 매개 변수를 추가하는 방법을 보여 줍니다.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

또는 YAML 구성 파일 사용:

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

The **constant load** run mode different from the constant number of started test execution, not generating a constant number of started test execution. 동일한 이름의 실행 모드 매개 변수를 사용하여 로드를 설정할 수 있습니다.

### 테스트 선택 {#test-selection}

테스트 선택 프로세스는 실행 모드 모두에 대해 동일하며 다음과 같습니다.모든 테스트에는 스레드에서 실행 가능성을 결정하는 `weight` 속성이 있습니다. 예를 들어, 두 개의 테스트를 실시하면, 하나는 몸무게 5이고 다른 하나는 몸무게 10인 경우, 후자는 전자보다 두 배 더 많이 실행될 가능성이 있습니다.

또한 테스트는 실행 수를 지정된 수로 제한하는 `count` 속성을 가질 수 있습니다. 이 번호가 전달된 후에는 더 이상 테스트가 실행되지 않습니다. 이미 실행 중인 모든 테스트 인스턴스는 구성된 대로 실행을 마칩니다. 다음 예에서는 이러한 매개 변수를 명령줄에 추가하거나 YAML 구성 파일을 사용하여 추가하는 방법을 보여 줍니다.

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
>병렬 실행 때문에 실제 테스트 실행 수는 `count` 매개 변수에 구성된 양이 아닙니다. 실행 중인 스레드 수에 편차가 있을 것으로 예상합니다(`concurrency parameter`에 의해 제어됨).

### 연습 실행 {#dry-run}

연습 실행은 지정된 모든 입력(명령줄 매개 변수 또는 구성 파일)을 구문 분석하여 기본값으로 병합한 다음 결과를 출력합니다. 테스트를 실행하지 않습니다.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 출력 {#output}

Touch Day 2는 테스트 지표와 로그를 모두 출력합니다. 자세한 내용은 다음 섹션을 참조하십시오.

### 지표 테스트 {#test-metrics}

오늘 2일은 현재 사용자가 평가할 수 있는 9개의 테스트 지표를 보고합니다. ***** 기호가 있는 지표는 성공적인 실행 후에만 보고됩니다.

| **이름** | **설명** |
|---|---|
| 타임스탬프 | 마지막으로 완료된 테스트 실행의 타임스탬프. |
| 전달됨 | 성공한 실행 수입니다. |
| 실패 | 실패한 실행 수입니다. |
| 최소* | 테스트 실행의 가장 낮은 기간입니다. |
| 최대* | 테스트 실행의 최고 기간입니다. |
| 중간* | 모든 테스트 실행의 평균 계산 기간입니다. |
| 평균* | 모든 테스트 실행의 계산된 평균 기간입니다. |
| StdDev* | 표준 편차 |
| 90p* | 90 백분위수 |
| 99p* | 99 백분위수 |
| 99.9p* | 99.9 백분위수. |
| Real Throughput* | 경과된 실행 시간으로 나눈 실행 수입니다. |

이러한 지표는 테스트 추가와 마찬가지로 `add` 매개 변수로 추가할 수 있는 게시자의 도움을 받아 작성됩니다. 현재 두 가지 옵션이 있습니다.

* **CSVPublisher**  - 출력이 CSV 파일입니다.
* **ConsolePublisher**  - 출력이 콘솔에 표시됩니다.

기본적으로 두 발행자는 모두 활성화됩니다.

또한 지표가 보고되는 두 가지 모드가 있습니다.

* **simple** 게시 모드 - 실행 시작부터 게시 지점까지 결과를 보고합니다.
* **간격** 게시 모드 - 지정된 기간 내에 결과를 보고합니다. **interval** 게시 모드 매개 변수를 사용하여 시간 프레임을 설정할 수 있습니다.

다음 예에서는 명령줄에서 또는 YAML 구성 파일을 사용하여 `intervals` 매개 변수를 구성하는 방법을 보여 줍니다.

명령줄 매개 변수를 사용하여 다음을 수행합니다.

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

YAML 구성 파일을 사용하여 다음을 수행합니다.

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### 로깅 {#logging}

터프한 요일 2를 실행한 동일한 디렉토리에 로그 폴더가 생성됩니다. 이 폴더에는 두 가지 유형의 로그가 포함되어 있습니다.

* **powerday.log**:에는 응용 프로그램 상태, 디버깅 정보 및 전역 메시지와 관련된 메시지가 포함되어 있습니다.
* **powerday_&lt;testname>.log**:지정된 테스트와 관련된 메시지.

로그가 덮어쓰이지 않으며, 이후 실행은 기존 로그에 메시지를 추가합니다. 로그에 여러 수준이 있습니다. 자세한 내용은 ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`을 참조하십시오.

#### 사용 예 {#example-usage}

#### 알려진 문제 {#known-issues}

[파일 가져오기](assets/toughday-6_1.jar)
