---
title: AEM Forms의 감시 폴더
seo-title: Watched folder in AEM Forms
description: 관리자는 감시 대상 폴더에 파일이 있을 때 폴더를 감시하고 워크플로, 서비스 또는 스크립트 작업을 시작할 수 있습니다.
seo-description: An administrator can put a folder on watch and start a workflow, service, or script operation when a file is placed in the folder being watched.
uuid: 39eac0fd-8212-46ff-b75d-8b4320d448a9
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: db38972c-be3f-49fd-8cc1-45b16ed244af
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '7148'
ht-degree: 0%

---

# AEM Forms의 감시 폴더{#watched-folder-in-aem-forms}

관리자는 사용자가 감시 폴더에 파일(예: PDF 파일)을 배치할 때 추가된 파일을 처리하기 위해 사전 구성된 워크플로우, 서비스 또는 스크립트 작업이 시작되도록 감시 폴더라고 하는 네트워크 폴더를 구성할 수 있습니다. 이 서비스는 지정된 작업을 수행한 후 결과 파일을 지정된 출력 폴더에 저장합니다. 워크플로우, 서비스 및 스크립트에 대한 자세한 내용은 [파일을 처리하는 다양한 방법](#variousmethodsforprocessingfiles).

## 감시 폴더 만들기 {#create-a-watched-folder}

다음 방법 중 하나를 사용하여 파일 시스템에서 감시 폴더를 만들 수 있습니다.

* 감시 폴더 구성 노드의 속성을 구성하는 동안 다음 예제와 같이 folderPath 속성에 상위 디렉토리의 전체 경로를 입력하고 만들 감시 폴더의 이름을 추가합니다. `C:/MyPDFs/MyWatchedFolder`
다음 `MyWatchedFolder`폴더가 없습니다. AEM Forms은 지정된 경로에 폴더를 만들려고 합니다.

* 감시 폴더 끝점을 구성하기 전에 파일 시스템에 폴더를 만든 다음 folderPath 속성에 전체 경로를 제공합니다. folderPath 속성에 대한 자세한 내용은 [감시 폴더 속성](#watchedfolderproperties).

>[!NOTE]
>
>클러스터 환경에서는 감시 폴더로 사용되는 폴더를 액세스, 쓰기 및 공유할 수 있어야 합니다. 클러스터의 각 응용 프로그램 서버 인스턴스는 동일한 공유 폴더에 액세스할 수 있어야 합니다. Windows의 경우 모든 서버에 매핑된 네트워크 드라이브를 만들고 folderPath 속성에 매핑된 네트워크 드라이브의 경로를 지정합니다.

## 감시 폴더 구성 노드 만들기 {#create-watched-folder-configuration-node}

감시 폴더를 구성하려면 감시 폴더 구성 노드를 만듭니다. 구성 노드를 만들려면 다음 단계를 수행하십시오.

1. CRX-DE lite에 관리자로 로그인하고 /etc/fd/watchfolder/config 폴더로 이동합니다.

1. 유형의 노드 만들기 `nt:unstructured`. 예: watchedfolder

   >[!NOTE]
   >
   >감시 폴더 노드 이름에는 공백과 특수 문자를 포함할 수 없습니다.

1. 노드에 다음 속성을 추가합니다.

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   지원되는 속성의 전체 목록은 다음을 참조하십시오. [감시 폴더 속성](#watchedfolderproperties).

1. **모두 저장**&#x200B;을 클릭합니다. 노드가 만들어지고 속성이 저장되면 다음 `input`, `result`, `failure`, `preserve`, 및 `stage`폴더는에 지정된 경로에 만들어집니다. `folderPath` 속성.

   스캔 작업은 정의된 시간 간격으로 감시 폴더 스캔을 시작합니다.

## 감시 폴더 속성 {#watchedfolderproperties}

감시 폴더에 대해 다음 속성을 구성할 수 있습니다.

* **folderPath (String)**: 정의된 시간 간격으로 검사할 폴더의 경로 클러스터된 환경의 경우 폴더는 서버에 대한 전체 액세스 권한이 있는 모든 서버와 공유 위치에 있어야 합니다. 필수 속성입니다.
* **inputProcessorType(문자열)**: 시작할 프로세스의 유형입니다. 워크플로우, 스크립트 또는 서비스를 지정할 수 있습니다. 필수 속성입니다.
* **inputProcessorId (문자열)**: inputProcessorId 속성의 동작은 inputProcessorType 속성에 지정된 값을 기반으로 합니다. 필수 속성입니다. 다음 목록은 inputProcessorType 속성의 가능한 모든 값과 inputProcessorType 속성에 대한 해당 요구 사항을 자세히 설명합니다.

   * 워크플로우의 경우 실행할 워크플로우 모델을 지정합니다. 예: /etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * 스크립트의 경우 실행할 스크립트의 JCR 경로를 지정합니다. 예: /etc/fd/watchfolder/test/testScript.ecma
   * 서비스의 경우 OSGi 서비스를 찾는 데 사용되는 필터를 지정합니다. 이 서비스는 com.adobe.aemfd.watchfolder.service.api.ContentProcessor 인터페이스의 구현으로 등록됩니다.

* **runModes(문자열)**: 워크플로우 실행에 허용된 실행 모드를 쉼표로 구분한 목록입니다. 몇 가지 예는 다음과 같습니다.

   * 작성자

   * 페이지를

   * 작성자,게시

   * 게시, 작성자

>[!NOTE]
>
>감시 폴더를 호스팅하는 서버에 지정된 실행 모드가 없으면 서버의 실행 모드에 관계없이 감시 폴더가 항상 활성화됩니다.

* **outputFilePattern(문자열)**: 출력 파일의 패턴입니다. 폴더 또는 파일 패턴을 지정할 수 있습니다. 폴더 패턴이 지정된 경우 출력 파일의 이름은 워크플로우에 설명된 대로 지정됩니다. 파일 패턴이 지정된 경우 출력 파일의 이름은 파일 패턴에 설명된 대로 지정됩니다. [파일 및 폴더 패턴](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 출력 파일에 대한 디렉터리 구조를 지정할 수도 있습니다. 필수 속성입니다.

* **stageFileExpirationDuration(Long, 기본값 -1)**: 처리를 위해 이미 선택된 입력 파일/폴더가 시간 초과로 처리되고 오류로 표시될 때까지 대기하는 시간(초)입니다. 이 만료 메커니즘은 이 속성에 대한 값이 양수일 때만 활성화됩니다.

>[!NOTE]
>
>이 메커니즘을 사용하여 입력이 시간 초과된 것으로 표시된 경우에도 백그라운드에서 계속 처리 중일 수 있지만 예상보다 많은 시간이 소요됩니다. 시간 제한 메커니즘이 시작되기 전에 입력 콘텐츠가 소비된 경우 나중에 처리가 완료되어 출력이 결과 폴더로 덤프될 수도 있습니다. 시간 제한 전에 콘텐츠를 사용하지 않은 경우 콘텐츠를 사용하려고 할 때 나중에 처리 오류가 발생할 수 있으며 이 오류는 동일한 입력의 실패 폴더에도 기록됩니다. 반면, 간헐적인 작업/워크플로우 불량으로 인해 입력에 대한 처리가 활성화되지 않은 경우(만료 메커니즘이 해결하려는 시나리오), 두 가지 결과 모두 발생하지 않습니다. 따라서 시간 초과로 인해 실패로 표시된 실패 폴더의 모든 항목에 대해 &quot;상당한 시간 후에 처리되지 않은 파일, 실패로 표시!&quot; 형식의 메시지를 찾습니다. 실패 로그에서 이전에 설명한 결과가 실제로 발생했는지 여부를 확인하기 위해 결과 폴더(및 실패 폴더 자체에서 동일한 입력에 대한 다른 항목을 검색함)를 검색하는 것이 좋습니다.

* **deleteExpiredStageFileOnlyWhenThrottled(부울, 기본값 true):** 감시 폴더가 제한된 경우에만 만료 메커니즘을 활성화할지 여부입니다. 이 메커니즘은 처리되지 않은 상태(간헐적인 작업/워크플로 오발로 인해)에서 지속되는 적은 수의 파일이 스로틀링이 활성화되면 전체 배치에 대한 처리가 초크될 수 있으므로 스로틀링된 감시 폴더와 더 관련이 있습니다. 이 속성이 true(기본값)로 유지되면 스로틀되지 않은 감시 폴더에 대해 만료 메커니즘이 활성화되지 않습니다. 속성이 false로 유지되면 stageFileExpirationDuration 속성이 양수이면 메커니즘이 항상 활성화됩니다.

* **pollInterval(긴)**: 감시 폴더에서 입력을 검색하는 간격(초)입니다. 스로틀 설정을 사용하지 않으면 폴링 간격이 평균 작업을 처리하는 시간보다 길어야 합니다. 그렇지 않으면 시스템이 오버로드될 수 있습니다. 기본값은 5입니다. 자세한 내용은 배치 크기 설명을 참조하십시오. 수분의 값은 1보다 크거나 같아야 합니다.
* **excludeFilePattern (String)**: 감시 폴더가 스캔하고 가져올 파일 및 폴더를 결정하는 데 사용하는 패턴의 세미콜론(;)으로 구분된 목록입니다. 이 패턴을 가진 모든 파일 또는 폴더는 처리를 위해 스캔되지 않습니다. 이 설정은 입력이 여러 파일이 있는 폴더인 경우 유용합니다. 폴더의 내용은 감시 폴더에서 선택한 이름으로 폴더에 복사할 수 있습니다. 이렇게 하면 폴더가 입력 폴더로 완전히 복사되기 전에 감시 폴더가 처리할 폴더를 선택하지 못합니다. 기본값은 null입니다.
다음을 사용할 수 있습니다. [파일 패턴](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) 제외하려면 다음 작업을 수행하십시오.

   * 특정 파일 확장명을 가진 파일(예: &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * 특정 이름을 가진 파일(예: 데이터)&#42; 는 data1, data2 등으로 명명된 파일 및 폴더를 제외합니다.
   * 다음 예제와 같이 이름과 확장명에 복합 표현식이 있는 파일

      * Data[0-9][0-9][0-9].[dD][aA]&#39;포트&#39;
      * &#42;[dD][Aa]&#39;포트&#39;
      * &#42;[Xx][Mm][Ll]

파일 패턴에 대한 자세한 내용은 [파일 패턴 정보](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern (String)**: 감시 폴더가 스캔하고 가져올 폴더 및 파일을 결정하는 데 사용하는 패턴의 세미콜론(;)으로 구분된 목록입니다. 예를들어, IncludeFilePattern을&#42;, 입력과 일치하는 모든 파일 및 폴더&#42; 가져왔습니다. 여기에는 input1, input2 등으로 명명된 파일 및 폴더가 포함됩니다. 기본값은 입니다. &#42; 모든 파일과 폴더를 나타냅니다. 파일 패턴을 사용하여 다음을 포함할 수 있습니다.

   * 특정 파일 확장명을 가진 파일(예: &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * 특정 이름을 가진 파일(예: 데이터).&#42; 에는 data1, data2 등으로 명명된 파일 및 폴더가 포함됩니다.

* 다음 예제와 같이 이름과 확장명에 복합 표현식이 있는 파일

   * Data[0-9][0-9][0-9].[dD][aA]&#39;포트&#39;

      * &#42;[dD][Aa]&#39;포트&#39;
      * &#42;[Xx][Mm][Ll]

파일 패턴에 대한 자세한 내용은 [파일 패턴 정보](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime (Long)**: 폴더 또는 파일을 만든 후 스캔하기 전에 대기하는 시간(밀리초)입니다. 예를 들어 대기 시간이 3,600,000밀리초(1시간)이고 1분 전에 파일을 만든 경우 59분 이상 경과하면 이 파일이 선택됩니다. 기본값은 0입니다. 이 설정은 파일이나 폴더가 입력 폴더에 완전히 복사되도록 하는 데 유용합니다. 예를 들어 처리할 대형 파일이 있고 파일을 다운로드하는 데 10분이 걸리는 경우 대기 시간을 10으로 설정합니다&#42;60 &#42;1000밀리초. 이렇게 하면 감시 폴더가 10분이 되지 않은 경우 파일을 스캔하지 않습니다.
* **purgeDuration(긴)**: 결과 폴더의 파일과 폴더가 이 값보다 오래되면 제거됩니다. 이 값은 일 단위로 측정됩니다. 이 설정은 결과 폴더가 꽉 차지 않도록 하는 데 유용합니다. -1일 값은 결과 폴더를 삭제하지 않음을 나타냅니다. 기본값은 -1입니다.
* **resultFolderName(문자열)**: 저장된 결과가 저장되는 폴더입니다. 결과가 이 폴더에 표시되지 않으면 실패 폴더를 확인하십시오. 읽기 전용 파일은 처리되지 않고 실패 폴더에 저장됩니다. 이 값은 다음 파일 패턴을 사용하는 절대 또는 상대 경로일 수 있습니다.

   * %F = 파일 이름 접두사
   * %E = 파일 이름 확장명
   * %Y = 연도(전체)
   * %y = 연도(마지막 두 자리)
   * %M = 월
   * %D = 일
   * %d = 일(연 기준)
   * %H = 시간(24시간 시계)
   * %h = 시간(12시간 시계)
   * %m = 분
   * %s = 초
   * %l = 밀리초
   * %R = 난수(0~9 사이)
   * %P = 프로세스 또는 작업 ID

  예를 들어, 2009년 7월 17일 오후 8시이고 C:/Test/WF0/failure/%Y/%M/%D/%H/를 지정한 경우 결과 폴더는 C:/Test/WF0/failure/2009/07/17/20입니다

  경로가 절대적이 아니라 상대적이면 폴더가 감시 폴더 내에 만들어집니다. 기본값은 감시 폴더 내의 결과 폴더인 result/%Y/%M/%D/입니다. 파일 패턴에 대한 자세한 내용은 [파일 패턴 정보](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>결과 폴더의 크기가 작을수록 감시 폴더가 더 잘 수행됩니다. 예를 들어 감시 폴더의 예상 로드가 매시간 1,000개의 파일인 경우 매시간마다 새 하위 폴더가 생성되도록 결과/%Y%M%D%H와 같은 패턴을 시도하십시오. 부하가 더 작은 경우(예: 하루에 1000개의 파일) result/%Y%M%D과 같은 패턴을 사용할 수 있습니다.

* **failureFolderName(문자열)**: 오류 파일이 저장되는 폴더입니다. 이 위치는 항상 감시 폴더를 기준으로 합니다. 결과 폴더에 설명된 대로 파일 패턴을 사용할 수 있습니다. 읽기 전용 파일은 처리되지 않고 실패 폴더에 저장됩니다. 기본값은 failure/%Y/%M/%D/입니다.
* **preserveFolderName(문자열):** 처리 성공 후 파일이 저장되는 위치입니다. 경로는 절대, 상대 또는 null 디렉터리 경로일 수 있습니다. 결과 폴더에 설명된 대로 파일 패턴을 사용할 수 있습니다. 기본값은 preserve/%Y/%M/%D/입니다.
* **batchSize(긴)**: 스캔당 선택할 파일 또는 폴더 수입니다. 시스템의 오버로드를 방지하기 위해 사용합니다. 한 번에 너무 많은 파일을 스캔하면 충돌이 발생할 수 있습니다. 기본값은 2입니다.

  폴링 간격 및 배치 크기 설정은 모든 검사에서 감시 폴더가 선택하는 파일 수를 결정합니다. 감시 폴더는 석영 스레드 풀을 사용하여 입력 폴더를 스캔합니다. 스레드 풀이 다른 서비스와 공유됩니다. 스캔 간격이 작으면 스레드에서 종종 입력 폴더를 스캔합니다. 파일이 자주 감시 폴더로 드롭되는 경우 스캔 간격을 작게 유지해야 합니다. 파일을 자주 삭제하지 않는 경우 다른 서비스가 스레드를 사용할 수 있도록 스캔 간격을 크게 사용합니다.

  삭제할 파일이 많은 경우 배치 크기를 크게 만듭니다. 예를 들어, 감시 폴더 끝점에서 시작된 서비스가 분당 700개의 파일을 처리할 수 있고, 사용자가 동일한 비율로 파일을 입력 폴더에 놓는 경우 배치 크기를 350으로 설정하고 폴링 간격을 30초로 설정하면 감시 폴더를 너무 자주 검색하는 비용을 발생시키지 않고도 감시 폴더 성능이 향상됩니다.

  파일이 감시 폴더로 드롭되면 입력에 있는 파일이 나열되므로 매 초마다 스캔이 발생하는 경우 성능이 저하될 수 있습니다. 스캔 간격을 늘리면 성능이 향상될 수 있습니다. 삭제할 파일 볼륨이 작은 경우 배치 크기 및 폴링 간격을 적절하게 조정합니다. 예를 들어 1초마다 10개의 파일을 삭제하는 경우 pollInterval을 1초로 설정하고 Batch Size를 10으로 설정하십시오

* **throttleOn(부울)**: 이 옵션을 선택하면 AEM Forms이 지정된 시간에 처리하는 감시 폴더 작업 수가 제한됩니다. 최대 작업 수는 [일괄 처리 크기] 값에 의해 결정됩니다. 기본값은 true입니다. (참조: [조절 기본 정보](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).)

* **overwriteDuplicateFilename(부울)**: True로 설정하면 결과 폴더 및 유지 폴더의 파일이 덮어쓰기됩니다. False로 설정하면 이름에 숫자 인덱스 접미사가 있는 파일과 폴더가 사용됩니다. 기본값은 False입니다.
* **preserveOnFailure(부울)**: 서비스에서 작업을 실행하지 못하는 경우 입력 파일을 유지합니다. 기본값은 true입니다.
* **inputFilePattern (String)**: 감시 폴더의 입력 파일 패턴을 지정합니다. 파일 허용 목록을 생성합니다.
* **비동기(부울)**: 호출 유형을 비동기 또는 동기식으로 식별합니다. 기본값은 true(비동기)입니다. 파일 처리는 리소스를 사용하는 작업입니다. 스캔 작업의 주 스레드가 닫히지 않도록 비동기 플래그 값을 true로 유지하십시오. 클러스터된 환경에서는 사용 가능한 서버에서 처리되는 파일에 대한 로드 밸런싱을 활성화하려면 플래그를 true로 유지하는 것이 중요합니다. 플래그가 false이면 스캔 작업은 자체 스레드 내에서 각 최상위 수준 파일/폴더에 대한 처리를 순차적으로 수행합니다. 단일 서버 설정에서 워크플로 기반 처리와 같은 특정 이유 없이 플래그를 false로 설정하지 마십시오.

>[!NOTE]
>
>설계상 워크플로는 비동기적입니다. 값을 false로 설정해도 워크플로우가 비동기 모드로 실행됩니다.

* **활성화됨(부울)**: 감시 폴더에 대한 검색을 비활성화하고 활성화합니다. 감시 폴더 검색을 시작하려면 enabled를 true로 설정합니다. 기본값은 true입니다.
* **payloadMapperFilter:** 폴더가 감시 폴더로 구성되면 감시 폴더 내에 폴더 구조가 생성됩니다. 이 구조에는 입력을 제공하고, 출력(결과)을 수신하고, 오류에 대한 데이터를 저장하고, 오래 지속되는 프로세스에 대한 데이터를 보존하고, 다양한 단계에 대한 데이터를 저장하는 폴더가 있습니다. 감시 폴더의 폴더 구조는 Forms 중심 워크플로의 페이로드 역할을 할 수 있습니다. 페이로드 매퍼를 사용하면 입력, 출력 및 처리를 위해 감시 폴더를 사용하는 페이로드 구조를 정의할 수 있습니다. 예를 들어 기본 매퍼를 사용하는 경우 감시 폴더의 컨텐츠를 [페이로드]\input 및 [페이로드]\output 폴더. 두 가지 기본 페이로드 매퍼 구현을 사용할 수 있습니다. 없는 경우 [사용자 지정 구현](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), 기본 구현 중 하나를 사용합니다.

   * **기본 매퍼:** 기본 페이로드 매퍼를 사용하여 감시 폴더의 입력 및 출력 컨텐츠를 페이로드의 별도 입력 및 출력 폴더에 유지합니다. 또한 워크플로우의 페이로드 경로에서 [페이로드]/input/ 및 [페이로드]컨텐츠를 검색하고 저장할 경로를 /output합니다.

   * **간단한 파일 기반 페이로드 매퍼:** 단순 파일 기반 페이로드 매퍼를 사용하여 입력 및 출력 내용을 페이로드 폴더에 직접 유지합니다. 기본 매퍼와 같은 추가 계층은 생성되지 않습니다.

### 사용자 지정 구성 매개 변수 {#custom-configuration-parameters}

위에 나열된 감시 폴더 구성 속성과 함께 사용자 지정 구성 매개 변수를 지정할 수도 있습니다. 사용자 지정 매개 변수가 파일 처리 코드에 전달됩니다. 이렇게 하면 코드가 매개 변수 값에 따라 비헤이비어를 변경할 수 있습니다. 매개 변수를 지정하려면 다음을 수행하십시오.

1. CRXDE-Lite에 로그인하고 감시 폴더 구성 노드로 이동합니다.
1. 속성 매개 변수를 추가합니다.&lt;property_name> 감시 폴더 구성 노드로 이동합니다. 속성 유형은 부울, 날짜, 십진수, 더블, 긴 및 문자열만 될 수 있습니다. 단일 및 다중 값 속성을 지정할 수 있습니다.

>[!NOTE]
>
>속성의 데이터 형식이 Double이면 이러한 속성의 값에 소수점을 지정합니다. 데이터 형식이 Double이고 값에 소수점이 지정되지 않은 모든 속성의 경우 형식이 Long으로 변환됩니다.

이러한 속성은 맵 유형의 변경 불가능한 맵으로 전달됩니다&lt;string object=&quot;&quot;> 을 처리 코드에 추가합니다. 처리 코드는 ECMAScript, Workflow 또는 Service일 수 있습니다. 속성에 대해 제공된 값은 맵에서 키-값 쌍으로 사용할 수 있습니다. 키는 속성의 이름이고 값은 속성의 값입니다. 사용자 지정 구성 매개 변수에 대한 자세한 내용은 다음 이미지를 참조하십시오.

![필수 속성, 몇 가지 선택적 속성, 몇 가지 구성 매개 변수가 있는 샘플 감시 폴더 구성 노드](assets/custom-configuration-parameters.png)

필수 속성, 몇 가지 선택적 속성, 몇 가지 구성 매개 변수가 있는 샘플 감시 폴더 구성 노드.

#### 워크플로우에 대한 변수 변경 가능 {#mutable-variables-for-workflows}

워크플로우 기반 파일 처리 메서드에 대해 변경 가능한 변수를 만들 수 있습니다. 이러한 변수는 워크플로우의 단계 간에 흐르는 데이터에 대한 컨테이너 역할을 합니다. 이러한 변수를 만들려면 다음 작업을 수행하십시오.

1. CRXDE-Lite에 로그인하고 감시 폴더 구성 노드로 이동합니다.

1. 속성 workflow.var를 추가합니다.&lt;variable_name> 감시 폴더 구성 노드로 이동합니다.

   속성 유형은 부울, 날짜, 십진수, 더블, 긴 및 문자열만 될 수 있습니다. 다중 값 속성도 지원됩니다. 다중 값 속성의 경우 워크플로 단계에 사용할 수 있는 값은 지정된 유형의 배열입니다.

   >[!NOTE]
   >
   >속성의 데이터 형식이 Double이면 이러한 속성의 값에 소수점을 지정합니다. 데이터 형식이 Double이고 값에 소수점이 지정되지 않은 모든 속성의 경우 형식이 Long으로 변환됩니다.

>[!NOTE]
>
>JCR 사양에서는 속성에 대한 기본값을 지정합니다. 기본값은 워크플로우 처리 단계에서 사용할 수 있습니다. 따라서 적절한 기본값을 지정합니다.

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## 파일을 처리하는 다양한 방법 {#variousmethodsforprocessingfiles}

워크플로, 서비스 또는 스크립트를 시작하여 감시 폴더의 문서 위치를 처리할 수 있습니다.

### 서비스를 사용하여 감시 폴더 파일 처리   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

서비스는 의 사용자 지정 구현입니다. `com.adobe.aemfd.watchfolder.service.api.ContentProcessor` 인터페이스. 몇 가지 사용자 지정 속성과 함께 OSGi에 등록됩니다. 구현의 사용자 지정 속성을 사용하면 구현이 고유해지고 구현을 식별하는 데 도움이 됩니다.

#### ContentProcessor 인터페이스의 사용자 지정 구현 {#custom-implementation-of-the-contentprocessor-interface}

사용자 지정 구현은 처리 컨텍스트(com.adobe.aemfd.watchfolder.service.api.ProcessorContext 유형의 개체)를 수락하고, 컨텍스트에서 입력 문서 및 구성 매개 변수를 읽고, 입력을 처리하고, 출력을 컨텍스트에 다시 추가합니다. ProcessorContext에는 다음 API가 있습니다.

* **getWatchFolderId**: 감시 폴더의 ID를 반환합니다.
* **getInputMap**: 맵 유형의 맵을 반환합니다. 맵의 키는 입력 파일의 파일 이름과 파일 내용이 포함된 문서 객체입니다. getinputMap API를 사용하여 입력 파일을 읽습니다.
* **getConfigParameters**: 맵 유형의 변경할 수 없는 맵을 반환합니다. 맵에는 감시 폴더의 구성 매개 변수가 포함되어 있습니다.

* **setResult**: ContentProcessor 구현은 API를 사용하여 출력 문서를 결과 폴더에 씁니다. setResult API에 출력 파일의 이름을 제공할 수 있습니다. API는 지정된 출력 폴더/파일 패턴에 따라 제공된 파일을 사용하거나 무시하도록 선택할 수 있습니다. 폴더 패턴이 지정된 경우 출력 파일의 이름은 워크플로우에 설명된 대로 지정됩니다. 파일 패턴이 지정된 경우 출력 파일의 이름은 파일 패턴에 설명된 대로 지정됩니다.

예를 들어 다음 코드는 사용자 지정 foo=bar 속성을 사용한 ContentProcessor 인터페이스의 사용자 지정 구현입니다.

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

While [감시 폴더 구성](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p), inputProcessorId 속성을 (foo=bar)로 지정하고 inputProcessorType 속성을 Service로 지정하는 경우 위에서 언급한 Service(사용자 지정 구현)가 감시 폴더의 입력 파일을 처리하는 데 사용됩니다.

다음 예는 ContentProcessor 인터페이스의 사용자 지정 구현입니다. 이 예제에서 서비스는 입력 파일을 수락하고 파일을 임시 위치에 복사한 다음 파일 내용이 포함된 문서 개체를 반환합니다. 문서 객체의 컨텐트가 결과 폴더에 저장됩니다. 결과 폴더의 실제 경로가 [감시 폴더 구성 노드](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### 스크립트를 사용하여 감시 폴더 파일 처리 {#using-scripts-to-process-files-of-a-watched-folder}

스크립트는 감시 폴더에 배치된 문서를 처리하기 위해 작성된 ECMAScript 컴플레인 사용자 지정 코드입니다. 스크립트는 JCR 노드로 표시됩니다. 표준 ECMAScript 변수(log, sling 등)와 별도로 스크립트에는 processorContext 변수가 있습니다. 변수는 ProcessorContext 형식입니다. ProcessorContext에는 다음 API가 있습니다.

* **getWatchFolderId**: 감시 폴더의 ID를 반환합니다.
* **getInputMap**: 맵 유형의 맵을 반환합니다. 맵의 키는 입력 파일의 파일 이름과 파일 내용이 포함된 문서 객체입니다. getinputMap API를 사용하여 입력 파일을 읽습니다.
* **getConfigParameters**: 맵 유형의 변경할 수 없는 맵을 반환합니다. 맵에는 감시 폴더의 구성 매개 변수가 포함되어 있습니다.
* **setResult**: ContentProcessor 구현은 API를 사용하여 출력 문서를 결과 폴더에 씁니다. setResult API에 출력 파일의 이름을 제공할 수 있습니다. API는 지정된 출력 폴더/파일 패턴에 따라 제공된 파일을 사용하거나 무시하도록 선택할 수 있습니다. 폴더 패턴이 지정된 경우 출력 파일의 이름은 워크플로우에 설명된 대로 지정됩니다. 파일 패턴이 지정된 경우 출력 파일의 이름은 파일 패턴에 설명된 대로 지정됩니다.

다음 코드는 예제 ECMAScript입니다. 입력 파일을 수락하고 임시 위치에 파일을 복사한 다음 파일 내용이 포함된 문서 객체를 반환합니다. 문서 객체의 컨텐트가 결과 폴더에 저장됩니다. 결과 폴더의 실제 경로가 [감시 폴더 구성 노드](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>출력 폴더 및 파일 이름 접두사는 감시 폴더 구성 매개 변수를 기반으로 결정됩니다.

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### 스크립트 위치 및 보안 고려 사항 {#location-of-scripts-and-security-considerations}

기본적으로 고객이 스크립트를 배치할 수 있는 컨테이너 폴더(/etc/fd/watchfolder/scripts)가 제공되며, watch-folder 프레임워크에서 사용하는 기본 서비스 사용자에게는 이 위치에서 스크립트를 읽는 데 필요한 권한이 있습니다.

스크립트를 사용자 지정 위치에 배치하려는 경우 기본 서비스 사용자가 사용자 지정 위치에 대한 읽기 권한을 가지고 있지 않을 수 있습니다. 이러한 시나리오의 경우 다음 단계를 수행하여 사용자 지정 위치에 필요한 권한을 제공합니다.

1. 프로그래밍 방식으로 또는 콘솔을 통해 시스템 사용자 만들기 https://&#39;[server]:[포트]&#39;/crx/explorer. 기존 시스템 사용자를 사용할 수도 있습니다. 일반 사용자 대신 여기에서 시스템 사용자와 작업하는 것이 중요합니다.
1. 스크립트가 저장되는 사용자 지정 위치에서 새로 만들었거나 기존 시스템 사용자에게 읽기 권한을 제공합니다. 여러 사용자 지정 위치가 있을 수 있습니다. 모든 사용자 지정 위치에 대해 최소한 읽기 권한을 제공하십시오.
1. Felix 구성 콘솔(/system/console/configMgr)에서 감시 폴더에 대한 서비스 사용자 매핑을 찾습니다. 이 매핑은 &#39;매핑: adobe-aemds-core-watch-folder=...&#39;와 비슷합니다.
1. 매핑을 클릭합니다. &quot;adobe-aemds-core-watch-folder:scripts=fd-service&quot; 항목의 경우 fd-service를 사용자 지정 시스템 사용자의 ID로 변경합니다. 저장을 클릭합니다.

이제 구성된 사용자 지정 위치를 사용하여 스크립트를 저장할 수 있습니다.

### 워크플로를 사용하여 감시 폴더 파일 처리 {#using-a-workflow-to-process-files-of-a-watched-folder}

워크플로우를 사용하면 Experience Manager 활동을 자동화할 수 있습니다. 워크플로우는 특정 순서로 실행되는 일련의 단계로 구성됩니다. 각 단계는 페이지 활성화 또는 이메일 메시지 전송과 같은 고유한 활동을 수행합니다. 워크플로우는 저장소, 사용자 계정 및 Experience Manager 서비스의 에셋과 상호 작용할 수 있습니다. 따라서 워크플로우는 복잡하게 조정할 수 있습니다.

* 워크플로우를 만들기 전에 다음 사항을 고려하십시오.
* 단계의 출력은 모든 후속 단계에서 사용할 수 있어야 합니다.
이전 단계에서 생성된 기존 출력을 업데이트(또는 삭제)할 수 있어야 합니다.
* 변경 가능한 변수는 단계 간에 사용자 지정 동적 데이터를 전달하는 데 사용됩니다.

워크플로우를 사용하여 파일을 처리하려면 다음 단계를 수행하십시오.

1. 의 구현 만들기 `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor` 인터페이스. 이는 서비스용으로 생성된 구현과 유사합니다.

   >[!NOTE]
   >
   >완전히 ECMAScript에서 전체 구현을 만들 수 있습니다.

1. 워크플로 단계에서 com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService 유형의 OSGi 서비스를 찾고 다음 인수를 사용하여 서비스의 execute() 메서드를 호출합니다.

   * WorkflowContextProcessor 인터페이스의 사용자 지정 구현
   * 작업 항목
   * workflowSession
   * 메타데이터

Java 프로그래밍 언어를 사용하여 워크플로를 구현하는 경우 AEM 워크플로 엔진은 workItem, workflowSession 및 메타데이터 변수에 대한 값을 제공합니다. 이러한 변수는 사용자 지정 WorkflowProcess 구현의 execute() 메서드에 인수로 전달됩니다.

ECMAScript를 사용하여 워크플로를 구현하는 경우 AEM 워크플로 엔진은 graniteWorkItem, graniteWorkflowSession 및 메타데이터 변수에 대한 값을 제공합니다. 이러한 변수는 WorkflowContextService.execute() 메서드에 인수로 전달됩니다.

processWorkflowContext()에 대한 인수는 com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext 유형의 객체입니다. WorkflowContext 인터페이스에는 위에서 언급한 워크플로 관련 고려 사항을 용이하게 하기 위해 다음과 같은 API가 있습니다.

* getWorkItem: WorkItem 변수의 값을 반환합니다. 변수는 WorkflowContextService.execute() 메서드에 전달됩니다.
* getWorkflowSession: WorkflowSession 변수의 값을 반환합니다. 변수는 WorkflowContextService.execute() 메서드에 전달됩니다.
* getMetadata: 메타데이터 변수의 값을 반환합니다. 변수는 WorkflowContextService.execute() 메서드에 전달됩니다.
* getCommittedVariables: 이전 단계에서 설정한 변수를 나타내는 읽기 전용 개체 맵을 반환합니다. 이전 단계에서 변수가 수정되지 않으면 감시 폴더를 구성하는 동안 지정된 기본값이 반환됩니다.
* getCommittedResults: 읽기 전용 문서 맵을 반환합니다. 맵은 이전 단계에서 생성된 출력 파일을 나타냅니다.
* setVariable: WorkflowContextProcessor 구현은 변수를 사용하여 단계 간에 흐르는 사용자 지정 동적 데이터를 나타내는 변수를 조작합니다. 변수의 이름 및 유형은 다음 기간 동안 지정된 변수의 이름과 동일합니다 [감시 폴더 구성](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). 변수의 값을 변경하려면 null이 아닌 값으로 setVariable API를 호출합니다. 변수를 제거하려면 null 값으로 setVariable()을 호출합니다.

다음 ProcessorContext API도 사용할 수 있습니다.

* getWatchFolderId: 감시 폴더의 ID를 반환합니다.
* getInputMap: Map 유형의 맵을 반환합니다.&lt;string document=&quot;&quot;>. 맵의 키는 입력 파일의 파일 이름과 파일 내용이 포함된 문서 객체입니다. getinputMap API를 사용하여 입력 파일을 읽습니다.
* getConfigParameters: Map 형식의 변경할 수 없는 맵을 반환합니다.&lt;string object=&quot;&quot;>. 맵에는 감시 폴더의 구성 매개 변수가 포함되어 있습니다.
* setResult: ContentProcessor 구현은 API를 사용하여 결과 폴더에 출력 문서를 기록합니다. setResult API에 출력 파일의 이름을 제공할 수 있습니다. API는 지정된 출력 폴더/파일 패턴에 따라 제공된 파일을 사용하거나 무시하도록 선택할 수 있습니다. 폴더 패턴이 지정된 경우 출력 파일의 이름은 워크플로우에 설명된 대로 지정됩니다. 파일 패턴이 지정된 경우 출력 파일의 이름은 파일 패턴에 설명된 대로 지정됩니다

워크플로우에서 사용할 경우 setResult API에 대한 고려 사항:

* 전체 워크플로 출력에 기여하는 새 출력 문서를 추가하려면 이전 단계에서 출력 파일 이름으로 사용되지 않은 파일 이름으로 setResult API를 호출하십시오.
* 이전 단계에서 생성된 출력을 업데이트하려면 이전 단계에서 이미 사용한 파일 이름으로 setResult API를 호출합니다.
* 이전 단계에서 생성된 출력을 삭제하려면 이전 단계에서 이미 사용한 파일 이름과 null을 내용으로 하는 setResult를 호출합니다.

>[!NOTE]
>
>다른 시나리오에서 null 콘텐츠가 있는 setResult API를 호출하면 오류가 발생합니다.

다음 예제는 워크플로우 단계로 구현됩니다. 이 예에서 ECMAscript는 stepCount 변수를 사용하여 현재 워크플로우 인스턴스에서 단계가 호출된 횟수를 추적합니다.
출력 폴더의 이름은 현재 단계 번호, 원본 파일 이름 및 outPrefix 매개 변수에 지정된 접두사의 조합입니다.

ECMAScript는 워크플로 컨텍스트 서비스의 참조를 가져오고 WorkflowContextProcessor 인터페이스의 구현을 만듭니다. WorkflowContextProcessor 구현은 입력 파일을 수락하고 파일을 임시 위치에 복사한 다음 복사한 파일을 나타내는 문서를 반환합니다. 현재 단계는 부울 변수 purgePrevious의 값을 기반으로 현재 워크플로우 인스턴스에서 단계가 시작되었을 때 동일한 단계에서 마지막으로 생성된 출력을 삭제합니다. 마지막으로 wfSvc.execute 메서드를 호출하여 WorkflowContextProcessor 구현을 실행합니다. 출력 문서의 내용은 감시 폴더 구성 노드에 언급된 실제 경로의 결과 폴더에 저장됩니다.

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### 페이로드 매퍼 필터 를 만들어 감시 폴더의 구조를 워크플로의 페이로드에 매핑 {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

감시 폴더를 만들면 감시 대상 폴더 내에 폴더 구조가 만들어집니다. 폴더 구조에는 단계, 결과, 유지, 입력 및 실패 폴더가 있습니다. 폴더 구조는 워크플로우에 대한 입력 페이로드의 역할을 하며 워크플로우의 출력을 수락할 수 있습니다. 필요한 경우 실패 지점을 나열할 수도 있습니다.

페이로드 구조가 감시 폴더 구조와 다른 경우 사용자 정의 스크립트를 작성하여 감시 폴더 구조를 페이로드에 매핑할 수 있습니다. 이러한 스크립트를 페이로드 매퍼 필터라고 합니다. 기본적으로 AEM Forms은 감시 폴더의 구조를 페이로드에 매핑하는 페이로드 매퍼 필터를 제공합니다.

#### 사용자 지정 페이로드 매퍼 필터 만들기 {#creating-a-custom-payload-mapper-filter}

1. 다운로드 [Adobe 클라이언트 SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. Maven 기반 프로젝트의 빌드 경로에서 클라이언트 SDK를 설정합니다. 시작하려면 원하는 IDE에서 다음 Maven 기반 프로젝트를 다운로드하여 열 수 있습니다.
1. 요구 사항에 맞게 샘플 번들에서 사용할 수 있는 페이로드 매퍼 필터 코드를 편집합니다.
1. Maven을 사용하여 사용자 지정 페이로드 매퍼 필터 번들을 만듭니다.
1. 사용 [AEM 번들 콘솔](https://localhost:4502/system/console/bundles) 번들을 설치합니다.

   이제 사용자 지정 페이로드 매퍼 필터가 AEM 감시 폴더 UI에 나열됩니다. 워크플로우에서 사용할 수 있습니다.

   다음 예제 코드는 페이로드를 기준으로 저장된 파일에 대해 간단한 파일 기반 매퍼를 구현합니다. 시작하는 데 사용할 수 있습니다.

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## 사용자가 감시 폴더와 상호 작용하는 방법 {#how-users-interact-with-a-watched-folder}

감시 폴더 끝점의 경우 사용자는 데스크탑에서 감시 폴더로 입력 파일 또는 폴더를 복사하거나 드래그하여 파일 처리 작업을 시작할 수 있습니다. 파일은 도착한 순서대로 처리됩니다.

감시 폴더 엔드포인트의 경우, 작업에 하나의 입력 파일만 필요한 경우 사용자는 해당 파일을 감시 폴더의 루트에 복사할 수 있습니다.

작업에 두 개 이상의 입력 파일이 포함된 경우 사용자는 모든 필수 파일이 포함된 감시 폴더 계층 구조 외부에 폴더를 만들어야 합니다. 이 새 폴더에는 입력 파일(및 프로세스에 필요한 경우 DDX 파일)이 포함되어야 합니다. 작업 폴더가 생성되면 사용자는 이를 감시 폴더의 입력 폴더에 복사합니다.

>[!NOTE]
>
>응용 프로그램 서버가 감시 폴더의 파일에 대한 액세스 권한을 삭제했는지 확인합니다. 파일을 스캔한 후 AEM Forms이 입력 폴더에서 파일을 삭제할 수 없는 경우 관련 프로세스는 무기한 시작됩니다.

## 감시 폴더에 대한 추가 정보 {#additional-information-about-the-watched-folders}

### 조절 정보 {#about-throttling}

감시 폴더 끝점에 대해 제한이 활성화되면 지정된 시간에 처리되는 감시 폴더 작업 수가 제한됩니다. 최대 작업 수는 [배치 크기] 값에 의해 결정되며, [감시 폴더] 엔드포인트에서 구성할 수도 있습니다. 제한 한도에 도달하면 감시 폴더의 입력 디렉터리에 있는 수신 문서가 폴링되지 않습니다. 다른 감시 폴더 작업이 완료되고 다른 폴링 시도가 수행될 때까지 문서가 입력 디렉터리에 유지됩니다. 동기 처리의 경우 작업이 단일 스레드에서 연속적으로 처리되더라도 단일 폴링에서 처리된 모든 작업은 제한 한도에 계산됩니다.

>[!NOTE]
>
>조절은 클러스터로 조절되지 않습니다. 제한이 활성화된 경우 클러스터는 지정된 시간에 일괄 처리 크기에 지정된 작업 수 이상을 처리하지 않습니다. 이 제한은 클러스터 전체에 적용되며 클러스터의 각 노드에만 국한되지 않습니다. 예를 들어 일괄 처리 크기가 2인 경우, 단일 노드가 두 개의 작업을 처리하면 제한 제한에 도달할 수 있으며, 다른 노드는 작업 중 하나가 완료될 때까지 입력 디렉토리를 폴링하지 않습니다.

#### 조절 작동 방식 {#how-throttling-works}

감시 폴더는 각 pollInterval마다 입력 폴더를 스캔하고 배치 크기에 지정된 파일 수를 선택한 다음 각 파일에 대해 대상 서비스를 호출합니다. 예를 들어, 배치 크기가 4인 경우, 스캔할 때마다 감시 폴더는 4개의 파일을 선택하고, 4개의 호출 요청을 생성하고, 대상 서비스를 호출합니다. 이러한 요청이 완료되기 전에 감시 폴더가 호출되면 이전 4개의 작업이 완료되었는지 여부에 관계없이 4개의 작업이 다시 시작됩니다.

조절은 이전 작업이 완료되지 않은 경우 감시 폴더가 새 작업을 호출하지 못하도록 합니다. 감시 폴더는 진행 중인 작업을 감지하고 일괄 처리 크기에서 진행 중인 작업을 뺀 값을 기준으로 새 작업을 처리합니다. 예를 들어 두 번째 호출에서 완료된 작업 수가 3개뿐이고 한 작업이 아직 진행 중인 경우 감시 폴더는 3개의 작업만 더 호출합니다.

* 감시 폴더는 스테이지 폴더에 있는 파일 수에 따라 얼마나 많은 작업이 진행 중인지 확인합니다. 단계 폴더에서 파일이 처리되지 않은 상태로 유지되면 감시 폴더는 더 이상 작업을 호출하지 않습니다. 예를 들어 배치 크기가 4개이고 세 개의 작업이 정지된 경우 감시 폴더는 후속 호출에서 한 작업만 호출합니다. 스테이지 폴더에서 파일이 처리되지 않은 상태로 유지될 수 있는 시나리오가 여러 가지가 있습니다. 작업이 정지되면 관리자는 프로세스 관리 관리 관리 페이지에서 프로세스를 종료하여 감시 폴더가 파일을 스테이지 폴더 밖으로 이동할 수 있습니다.
* 감시 폴더가 작업을 호출하기 전에 AEM Forms 서버가 다운되는 경우 관리자는 스테이지 폴더에서 파일을 이동할 수 있습니다. 자세한 내용은 [장애 지점 및 복구](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* AEM Forms 서버가 실행 중이지만 Job Manager 서비스가 다시 호출될 때 감시 폴더가 실행되지 않는 경우(서비스가 순서가 지정된 시퀀스에서 시작되지 않을 때 발생) 관리자는 스테이지 폴더 밖으로 파일을 이동할 수 있습니다. 자세한 내용은 [장애 지점 및 복구](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### 장애 지점 및 복구장애 지점 및 복구 {#failure-points-and-recoveryfailure-points-and-recovery}

각 폴 이벤트에서 감시 폴더는 입력 폴더를 잠그고 포함 파일 패턴과 일치하는 파일을 스테이지 폴더로 이동한 다음 입력 폴더의 잠금을 해제합니다. 두 스레드가 동일한 파일 세트를 선택하여 두 번 처리하지 않도록 잠가야 합니다. 작은 pollInterval과 큰 일괄 처리 크기를 사용하면 이러한 상황이 발생할 가능성이 높아집니다. 파일을 스테이지 폴더로 이동한 후 다른 스레드에서 폴더를 검색할 수 있도록 입력 폴더의 잠금이 해제됩니다. 이 단계는 한 스레드가 파일을 처리하는 동안 다른 스레드가 검색할 수 있으므로 처리량이 높습니다.

파일을 스테이지 폴더로 이동한 후 각 파일에 대해 호출 요청이 생성되고 대상 서비스가 호출됩니다. 감시 폴더가 스테이지 폴더의 파일을 복구할 수 없는 경우가 있을 수 있습니다.

* [감시 폴더]에서 호출 요청을 만들기 전에 서버가 다운되는 경우 스테이지 폴더의 파일이 스테이지 폴더에 남아 있으며 복구되지 않습니다.

* 감시 폴더가 스테이지 폴더의 각 파일에 대한 호출 요청을 성공적으로 만들었으며 서버가 충돌하는 경우 호출 유형에 따라 두 가지 동작이 있습니다.

   * **동기**: 감시 폴더가 서비스를 동기적으로 호출하도록 구성된 경우 스테이지 폴더의 모든 파일이 스테이지 폴더에서 처리되지 않은 상태로 유지됩니다.
   * **비동기**: 이 경우 감시 폴더는 작업 관리자 서비스를 사용합니다. Job Manager 서비스가 감시 폴더를 다시 호출하면 호출 결과에 따라 스테이지 폴더의 파일이 유지 또는 실패 폴더로 이동됩니다. 작업 관리자 서비스가 다시 감시 폴더를 호출하지 않으면 파일이 스테이지 폴더에서 처리되지 않은 상태로 유지됩니다. 이 상황은 작업 관리자가 다시 호출할 때 감시 폴더가 실행되고 있지 않을 때 발생합니다.

#### 스테이지 폴더에서 처리되지 않은 소스 파일 복구 {#recover-unprocessed-source-files-in-the-stage-folder}

감시 폴더가 스테이지 폴더의 소스 파일을 처리할 수 없는 경우 처리되지 않은 파일을 복구할 수 있습니다.

1. 응용 프로그램 서버 또는 노드를 다시 시작합니다.

1. 감시 폴더에서 새 입력 파일을 처리하지 않습니다. 이 단계를 건너뛸 경우 스테이지 폴더에서 처리되지 않은 파일을 확인하는 것이 훨씬 어렵습니다. 감시 폴더가 새 입력 파일을 처리하지 못하도록 하려면 다음 작업 중 하나를 수행합니다.

   * 새 입력 파일과 일치하지 않는 감시 폴더의 includeFilePattern 속성을 변경합니다(예: NOMATCH 입력).
   * 새 입력 파일을 만드는 프로세스를 일시 중단합니다.

   AEM Forms이 모든 파일을 복구하고 처리할 때까지 기다립니다. 대부분의 파일은 복구해야하고 새로운 입력 파일은 올바르게 처리해야합니다. 감시 폴더가 파일을 복구하고 처리할 때까지 기다리는 시간은 호출할 작업의 길이와 복구할 파일의 수에 따라 달라집니다.

1. 처리할 수 없는 파일을 확인합니다. 적절한 시간을 기다린 후 이전 단계를 완료했지만 스테이지 폴더에 처리되지 않은 파일이 남아 있는 경우 다음 단계로 이동합니다.

   >[!NOTE]
   >
   >스테이지 디렉터리에서 파일의 날짜 및 타임스탬프를 확인할 수 있습니다. 파일 수와 일반 처리 시간에 따라 중단 상태로 간주할 만큼 오래된 파일을 확인할 수 있습니다.

1. 처리되지 않은 파일을 스테이지 디렉토리에서 입력 디렉토리로 복사합니다.

1. 2단계에서 감시 폴더가 새 입력 파일을 처리하지 못하게 한 경우 포함 파일 패턴을 이전 값으로 변경하거나 비활성화한 프로세스를 다시 활성화하십시오.

### 감시 폴더 함께 체인 {#chain-watched-folders-together}

감시 폴더는 하나의 감시 폴더의 결과 문서가 다음 감시 폴더의 입력 문서가 되도록 함께 체인화될 수 있습니다. 각 감시 폴더는 다른 서비스를 호출할 수 있습니다. 이러한 방식으로 감시 폴더를 구성하면 여러 서비스를 호출할 수 있습니다. 예를 들어 하나의 감시 폴더는 PDF 파일을 Adobe PostScript®로 변환할 수 있고 두 번째 감시 폴더는 PostScript 파일을 PDF/A 형식으로 변환할 수 있습니다. 이렇게 하려면 첫 번째 끝점에 의해 정의된 감시 폴더의 결과 폴더를 두 번째 끝점에 의해 정의된 감시 폴더의 입력 폴더를 가리키도록 설정하기만 하면 됩니다.

첫 번째 변환의 출력은 \path\result로 이동합니다. 두 번째 변환에 대한 입력은 \path\result이고 두 번째 변환의 출력은 \path\result\result(또는 두 번째 변환에 대해 결과 폴더 상자에 정의한 디렉토리)로 이동합니다.

### 파일 및 폴더 패턴 {#file-and-folder-patterns}

관리자는 서비스를 호출할 수 있는 파일 유형을 지정할 수 있습니다. 각 감시 폴더에 대해 여러 파일 패턴을 설정할 수 있습니다. 파일 패턴은 다음 파일 속성 중 하나일 수 있습니다.

* 특정 파일 이름 확장명을 가진 파일(예: &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
* 특정 이름을 가진 파일(예: 데이터).&#42;
* 다음 예제와 같이 이름과 확장명에 복합 표현식이 있는 파일

   * Data[0-9][0-9][0-9].[dD][aA]&#39;포트&#39;
   * &#42;[dD][Aa]&#39;포트&#39;
   * &#42;[Xx][Mm][Ll]

* 관리자는 결과를 저장할 출력 폴더의 파일 패턴을 정의할 수 있습니다. 출력 폴더(결과, 유지 및 실패)에 대해 관리자는 다음 파일 패턴 중 하나를 지정할 수 있습니다.
* %Y = 연도(전체)
* %y = 연도(마지막 두 자리)
* %M = 월,
* %D = 날짜,
* %d = 일(한 해 기준),
* %h = 시간,
* %m = 분,
* %s = 초,
* %R = 0-9 사이의 난수
* %J = 작업 이름

예를 들어 결과 폴더의 경로는 C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d일 수 있습니다.

출력 매개 변수 매핑은 다음과 같은 추가 패턴을 지정할 수도 있습니다.

* %F = 소스 파일 이름
* %E = 소스 파일 이름 확장명

출력 매개 변수 매핑 패턴이 &quot;File.separator&quot;(경로 구분 기호)로 끝나면 폴더가 생성되고 콘텐츠가 해당 폴더에 복사됩니다. 패턴이 &quot;File.separator&quot;로 끝나지 않으면 컨텐츠(결과 파일 또는 폴더)가 해당 이름으로 만들어집니다.

## 감시 폴더로 PDF Generator 사용 {#using-pdf-generator-with-a-watched-folder}

워크플로, 서비스 또는 스크립트를 시작하여 입력 파일을 처리하도록 감시 폴더를 구성할 수 있습니다. 다음 섹션에서는 ECMAScript를 시작하도록 감시 폴더를 구성합니다. ECMAScript는 PDF Generator을 사용하여 Microsoft Word(.docx) 문서를 PDF 문서로 변환합니다.

PDF Generator으로 감시 폴더를 구성하려면 다음 단계를 수행하십시오.

1. [ECMAScript 만들기](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [워크플로우 만들기](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [감시 폴더 구성](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### ECMAScript 만들기 {#create-an-ecmascript}

ECMAScript는 PDF Generator의 createPDF API를 사용하여 Microsoft Word(.docx) 문서를 PDF 문서로 변환합니다. 스크립트를 만들려면 다음 단계를 수행하십시오.

1. 브라우저 창에서 CRXDE lite를 엽니다. URL은 https://&#39; 입니다.[server]:[포트]&#39;/crx/de.

1. /etc/workflow/scripts 로 이동하여 PDFG라는 폴더를 만듭니다.

1. PDFG 폴더에서 pdfg-openOffice-sample.ecma라는 파일을 만들고 파일에 다음 코드를 추가합니다.

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. 파일을 저장하고 닫습니다.

### 워크플로우 만들기 {#create-a-workflow}

1. 브라우저 창에서 AEM Workflow UI를 엽니다.
   <https://[servername>]:&#39;port&#39;/workflow

1. 모델 보기에서 **신규**. 새 워크플로우 대화 상자에서 다음을 지정합니다. **제목**, 및 클릭 **확인**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. 새로 만든 워크플로우를 선택하고 을(를) 클릭합니다. **편집**. 워크플로우가 새 창에서 열립니다.

1. 기본 워크플로우 단계를 삭제합니다. Sidekick에서 워크플로우로 프로세스 단계를 드래그 앤 드롭합니다.

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. 프로세스 단계를 마우스 오른쪽 버튼으로 클릭하고 를 선택합니다. **편집**. 단계 속성 창이 나타납니다.

1. 프로세스 탭에서 ECMAScript를 선택합니다. 예를 들어 pdfg-openOffice-sample.ecma 스크립트는에서 [ECMAScript 만들기](#p-create-an-ecmascript-p). 활성화 **핸들러 진행** 옵션 및 클릭 **확인**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### 감시 폴더 구성 {#configure-the-watched-folder}

1. 브라우저 창에서 CRXDE lite를 엽니다. https://&#39;[server]:[포트]&#39;/crx/de/

1. /etc/fd/watchfolder/config/ 폴더로 이동하고 nt:unstructured 유형의 노드를 만듭니다.

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. 노드에 다음 속성을 추가합니다.

   * folderPath (String): 정의된 시간 간격으로 검사할 폴더의 경로입니다. 폴더는 서버에 대한 전체 액세스 권한이 있는 모든 서버가 있는 공유 위치에 있어야 합니다.
inputProcessorType (String): 시작할 프로세스의 유형입니다. 이 자습서에서는 워크플로우를 지정합니다.

   * inputProcessorId(문자열): inputProcessorId 속성의 동작은 inputProcessorType 속성에 지정된 값을 기반으로 합니다. 이 예제에서 inputProcessorType 속성의 값은 workflow입니다. 따라서 inputProcessorId 속성에 대해 PDFG 워크플로의 /etc/workflow/models/pdfg/jcr:content/model 경로를 지정합니다.

   * outputFilePattern(String): 출력 파일의 패턴입니다. 폴더 또는 파일 패턴을 지정할 수 있습니다. 폴더 패턴이 지정된 경우 출력 파일의 이름은 워크플로우에 설명된 대로 지정됩니다. 파일 패턴이 지정된 경우 출력 파일의 이름은 파일 패턴에 설명된 대로 지정됩니다.

   위에서 언급한 필수 속성 외에도 감시 폴더는 몇 가지 선택적 속성을 지원합니다. 선택적 속성에 대한 전체 목록 및 설명은 다음을 참조하십시오. [감시 폴더 속성](#watchedfolderproperties).

## 알려진 문제 {#watched-folder-known-issues}

JEE에서 AEM 6.5 Forms을 시작할 때 JBoss가 완전히 시작되고 파일이 처리되지 않기 전에 파일 처리가 시작됩니다. 이를 방지하려면 JBoss를 시작하기 전에 모든 감시 폴더를 지웁니다.
