---
title: 프로그래밍 방식으로 워크플로우와 상호 작용
seo-title: 프로그래밍 방식으로 워크플로우와 상호 작용
description: 프로그래밍 방식으로 워크플로우와 상호 작용
seo-description: 'null'
uuid: a0f19fc6-b9bd-4b98-9c0e-fbf4f7383026
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: cb621332-a149-4f8d-9425-fd815b033c38
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2009'
ht-degree: 1%

---


# 프로그래밍 방식으로 워크플로우와 상호 작용{#interacting-with-workflows-programmatically}

[워크플로](/help/sites-developing/workflows-customizing-extending.md)를 사용자 지정하고 확장할 때 워크플로우 개체에 액세스할 수 있습니다.

* [워크플로우 Java API 사용](#using-the-workflow-java-api)
* [ECMA 스크립트에서 워크플로우 객체 얻기](#obtaining-workflow-objects-in-ecma-scripts)
* [Workflow REST API 사용](#using-the-workflow-rest-api)

## 워크플로우 Java API {#using-the-workflow-java-api} 사용

워크플로 Java API는 [`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) 패키지와 여러 하위 패키지로 구성됩니다. API의 가장 중요한 멤버는 `com.adobe.granite.workflow.WorkflowSession` 클래스입니다. `WorkflowSession` 클래스는 디자인 타임 및 런타임 워크플로 개체에 대한 액세스를 제공합니다.

* 워크플로우 모델
* 작업 항목
* 워크플로 인스턴스
* 워크플로 데이터
* 받은 편지함 항목

또한 이 클래스는 워크플로우 수명주기에 개입하는 여러 가지 방법을 제공합니다.

다음 표는 작업 과정과 프로그래밍 방식으로 상호 작용할 때 사용할 여러 주요 Java 객체의 참조 설명서에 대한 링크를 제공합니다. 다음 예제에서는 코드에서 클래스 개체를 가져와 사용하는 방법을 보여 줍니다.

| 기능 | 개체 |
|---|---|
| 워크플로우 액세스 | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| 워크플로우 인스턴스 실행 및 쿼리 | [`Workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| 워크플로우 모델 관리 | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| 워크플로우에 있는(또는 그렇지 않은) 노드에 대한 정보 | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## ECMA 스크립트에서 워크플로우 객체 얻기 {#obtaining-workflow-objects-in-ecma-scripts}

[스크립트](/help/sites-developing/the-basics.md#locating-the-script)를 찾는 방법에 설명된 대로 AEM(Apache Sling을 통해)는 서버측 ECMA 스크립트를 실행하는 ECMA 스크립트 엔진을 제공합니다. [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) 클래스는 스크립트에 `sling` 변수로 즉시 사용할 수 있습니다.

`ScriptHelper` 클래스는 `WorkflowSession` 개체를 최종적으로 가져오는 데 사용할 수 있는 `SlingHttpServletRequest`에 대한 액세스를 제공합니다.예를 들면 다음과 같습니다.

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## 워크플로 REST API 사용 {#using-the-workflow-rest-api}

워크플로우 콘솔에서는 REST API를 많이 사용합니다.따라서 이 페이지에서는 워크플로우에 대한 REST API에 대해 설명합니다.

>[!NOTE]
>
>말림 명령줄 도구를 사용하면 Workflow REST API를 사용하여 워크플로우 개체에 액세스하고 인스턴스 주기를 관리할 수 있습니다. 이 페이지의 예제는 말림 명령줄 도구를 통해 REST API를 사용하는 방법을 보여 줍니다.

다음 작업이 REST API에서 지원됩니다.

* 워크플로우 서비스 시작 또는 중지
* 워크플로우 모델 생성, 업데이트 또는 삭제
* [워크플로우 인스턴스 시작, 일시 중지, 다시 시작 또는 종료](/help/sites-administering/workflows.md#workflow-status-and-actions)
* 작업 항목 완료 또는 위임

>[!NOTE]
>
>웹 개발을 위한 Firefox 확장인 Firebug를 사용하면 콘솔을 실행할 때 HTTP 트래픽을 따를 수 있습니다. 예를 들어 매개 변수와 `POST` 요청을 사용하여 AEM 서버로 전송된 값을 확인할 수 있습니다.

이 페이지에서는 AEM이 `4502` 포트의 localhost에서 실행되고 설치 컨텍스트는 &quot; `/`&quot;(루트)라고 가정합니다. 설치가 아닌 경우 HTTP 요청이 적용되는 URI를 적절히 조정해야 합니다.

`GET` 요청에 대해 지원되는 렌더링은 JSON 렌더링입니다. `GET`의 URL에는 `.json` 확장자가 있어야 합니다. 예:

`http://localhost:4502/etc/workflow.json`

### 워크플로 인스턴스 관리 {#managing-workflow-instances}

다음 HTTP 요청 메서드가 다음에 적용됩니다.

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>작업</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>사용 가능한 워크플로우 인스턴스를 나열합니다.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>새 워크플로우 인스턴스를 만듭니다. 매개 변수는 <br /> - <code>model</code>:해당 워크플로 모델<br /> - <code>payloadType</code>의 ID(URI):페이로드 유형(예: <code>JCR_PATH</code> 또는 URL)을 포함합니다.<br /> 페이로드가 매개 변수로 전송됩니다 <code>payload</code>. 새 워크플로 인스턴스 리소스의 URL이 포함된 위치 헤더와 함께 <code>201</code>(<code>CREATED</code>) 응답이 다시 전송됩니다.</p> </td>
  </tr>
 </tbody>
</table>

#### 상태 {#managing-a-workflow-instance-by-its-state}별로 워크플로우 인스턴스 관리

다음 HTTP 요청 메서드가 다음에 적용됩니다.

`http://localhost:4502/etc/workflow/instances.{state}`

| HTTP 요청 메서드 | 작업 |
|---|---|
| `GET` | 사용 가능한 워크플로 인스턴스 및 상태( `RUNNING`, `SUSPENDED`, `ABORTED` 또는 `COMPLETED`)를 나열합니다. |

#### ID {#managing-a-workflow-instance-by-its-id}로 워크플로우 인스턴스 관리

다음 HTTP 요청 메서드가 다음에 적용됩니다.

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>작업</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>각 워크플로우 모델에 대한 링크를 포함하여 인스턴스 데이터(정의 및 메타데이터)를 가져옵니다.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>인스턴스의 상태를 변경합니다. 새 상태는 매개 변수 <code>state</code>으로 전송되며 다음 값 중 하나가 있어야 합니다.<code>RUNNING</code>, <code>SUSPENDED</code> 또는 <code>ABORTED</code>.<br /> 새 상태에 연결할 수 없는 경우(예: 종료된 인스턴스를 일시 중단하는 경우)  <code>409</code> (<code>CONFLICT</code>) 응답이 클라이언트로 다시 전송됩니다.</td>
  </tr>
 </tbody>
</table>

### 워크플로우 모델 관리 {#managing-workflow-models}

다음 HTTP 요청 메서드가 다음에 적용됩니다.

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>작업</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>사용 가능한 워크플로우 모델을 나열합니다.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>새 워크플로우 모델 만들기. 매개 변수 <code>title</code>이(가) 전송되면 지정된 제목으로 새 모델이 생성됩니다. JSON 모델 정의를 매개 변수 <code>model</code>으로 첨부하면 제공된 정의에 따라 새 워크플로우 모델이 만들어집니다.<br /> 새  <code>201</code> 워크플로우 모델 리소스의 URL이 포함된 위치 헤더와 함께 응답(<code>CREATED</code>)이 다시 전송됩니다.<br /> 모델 정의가 파일 매개 변수(  <code>modelfile</code><br /> 직렬화 형식 <code>model</code> 을 정의하려면  <code>modelfile</code> 매개 변수와 매개 변수의 두  <code>type</code> 경우 모두에 이 추가 매개 변수가 필요합니다. OSGI API를 사용하여 새로운 직렬화 형식을 통합할 수 있습니다. 표준 JSON 직렬 변환기는 워크플로 엔진과 함께 제공됩니다. JSON 형식입니다. 서식의 예는 아래를 참조하십시오.</td>
  </tr>
 </tbody>
</table>

예:브라우저에서 `http://localhost:4502/etc/workflow/models.json`에 대한 요청은 다음과 유사한 json 응답을 생성합니다.

```
[
    {"uri":"/var/workflow/models/activationmodel"}
    ,{"uri":"/var/workflow/models/dam/adddamsize"}
    ,{"uri":"/var/workflow/models/cloudconfigs/dtm-reactor/library-download"}
    ,{"uri":"/var/workflow/models/ac-newsletter-workflow-simple"}
    ,{"uri":"/var/workflow/models/dam/dam-create-language-copy"}
    ,{"uri":"/var/workflow/models/dam/dam-create-and-translate-language-copy"}
    ,{"uri":"/var/workflow/models/dam-indesign-proxy"}
    ,{"uri":"/var/workflow/models/dam-xmp-writeback"}
    ,{"uri":"/var/workflow/models/dam-parse-word-documents"}
    ,{"uri":"/var/workflow/models/dam/process_subasset"}
    ,{"uri":"/var/workflow/models/dam/dam_set_last_modified"}
    ,{"uri":"/var/workflow/models/dam/dam-autotag-assets"}
    ,{"uri":"/var/workflow/models/dam/update_asset"}
    ,{"uri":"/var/workflow/models/dam/update_asset_offloading"}
    ,{"uri":"/var/workflow/models/dam/dam-update-language-copy"}
    ,{"uri":"/var/workflow/models/dam/update_from_lightbox"}
    ,{"uri":"/var/workflow/models/cloudservices/DTM_bundle_download"}
    ,{"uri":"/var/workflow/models/dam/dam_download_asset"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-encode-video"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-thumbnail-replacement"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail"}
    ,{"uri":"/var/workflow/models/newsletter_bounce_check"}
    ,{"uri":"/var/workflow/models/projects/photo_shoot_submission"}
    ,{"uri":"/var/workflow/models/projects/product_photo_shoot"}
    ,{"uri":"/var/workflow/models/projects/approval_workflow"}
    ,{"uri":"/var/workflow/models/prototype-01"}
    ,{"uri":"/var/workflow/models/publish_example"}
    ,{"uri":"/var/workflow/models/publish_to_campaign"}
    ,{"uri":"/var/workflow/models/screens/publish_to_author_bin"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_publish_to_youtube"}
    ,{"uri":"/var/workflow/models/projects/request_copy"}
    ,{"uri":"/var/workflow/models/projects/request_email"}
    ,{"uri":"/var/workflow/models/projects/request_landing_page"}
    ,{"uri":"/var/workflow/models/projects/request_launch"}
    ,{"uri":"/var/workflow/models/request_for_activation"}
    ,{"uri":"/var/workflow/models/request_for_deactivation"}
    ,{"uri":"/var/workflow/models/request_for_deletion"}
    ,{"uri":"/var/workflow/models/request_for_deletion_without_deactivation"}
    ,{"uri":"/var/workflow/models/request_to_complete_move_operation"}
    ,{"uri":"/var/workflow/models/reverse_replication"}
    ,{"uri":"/var/workflow/models/salesforce-com-export"}
    ,{"uri":"/var/workflow/models/scene7"}
    ,{"uri":"/var/workflow/models/scheduled_activation"}
    ,{"uri":"/var/workflow/models/scheduled_deactivation"}
    ,{"uri":"/var/workflow/models/screens/screens-update-asset"}
    ,{"uri":"/var/workflow/models/translation"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_remove_from_youtube"}
    ,{"uri":"/var/workflow/models/wcm-translation/create_language_copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/prepare_translation_project"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-i18n-dictionary"}
    ,{"uri":"/var/workflow/models/wcm-translation/sync_translation_job"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-language-copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/update_language_copy"}
]
```

#### 특정 워크플로우 모델 관리 {#managing-a-specific-workflow-model}

다음 HTTP 요청 메서드가 다음에 적용됩니다.

`http://localhost:4502*{uri}*`

여기서 `*{uri}*`은 저장소의 모델 노드의 경로입니다.

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>작업</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>모델의 <code>HEAD</code> 버전(정의 및 메타데이터)을 가져옵니다.</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>모델의 <code>HEAD</code> 버전을 업데이트합니다(새 버전 만들기).<br /> 모델의 새 버전에 대한 전체 모델 정의를 호출되는 매개 변수로 추가해야 합니다 <code>model</code>. 또한 새 모델을 만들 때는 <code>type</code> 매개 변수가 필요하므로 <code>JSON</code> 값이 필요합니다.<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>PUT과 동일한 비헤이비어 AEM 위젯이 <code>PUT</code> 작업을 지원하지 않으므로 필요합니다.</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>모델을 삭제합니다. 방화벽/프록시 문제를 해결하기 위해 값이 <code>DELETE</code>인 <code>X-HTTP-Method-Override</code> 헤더 항목이 포함된 <code>POST</code>도 <code>DELETE</code> 요청으로 수락됩니다.</td>
  </tr>
 </tbody>
</table>

예:브라우저에서 `http://localhost:4502/var/workflow/models/publish_example.json`에 대한 요청은 다음 코드와 유사한 `json` 응답을 반환합니다.

```shell
{
  "id":"/var/workflow/models/publish_example",
  "title":"Publish Example",
  "version":"1.0",
  "description":"This example shows a simple review and publish process.",
  "metaData":
  {
    "multiResourceSupport":"true",
    "tags":"wcm,publish"
  },
  "nodes":
  [{
    "id":"node0",
    "type":"START",
    "title":"Start",
    "description":"The start node of the workflow.",
    "metaData":
    {
    }
  },
  {
    "id":"node1",
    "type":"PARTICIPANT",
    "title":"Validate Content",
    "description":"Validate the modified content.",
    "metaData":
    {
      "PARTICIPANT":"admin"
    }
  },
  {
    "id":"node2",
    "type":"PROCESS",
    "title":"Publish Content",
    "description":"Publish the modified content.",
    "metaData":
    {
      "PROCESS_AUTO_ADVANCE":"true",
      "PROCESS":"com.day.cq.wcm.workflow.process.ActivatePageProcess"
    }
  },
  {
    "id":"node3",
    "type":"END",
    "title":"End",
    "description":"The end node of the workflow.",
    "metaData":
    {
    }
  }],
  "transitions":
  [{
    "from":"node0",
    "to":"node1",
    "metaData":
    {
    }
  },
  {
    "from":"node1",
    "to":"node2",
    "metaData":
    {
    }
  },
  {
    "from":"node2",
    "to":"node3",
    "metaData":
    {
    }
  }
]}
```

#### 버전 {#managing-a-workflow-model-by-its-version}별로 워크플로우 모델 관리

다음 HTTP 요청 메서드가 다음에 적용됩니다.

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| HTTP 요청 메서드 | 작업 |
|---|---|
| `GET` | 지정된 버전에서 모델의 데이터를 가져옵니다(있는 경우). |

### {#managing-user-inboxes} 받은 편지함 관리(사용자)

다음 HTTP 요청 메서드가 다음에 적용됩니다.

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>작업</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>HTTP 인증 헤더로 식별되는 사용자의 받은 편지함에 있는 작업 항목을 나열합니다.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>URI가 매개 변수 <code>item</code>으로 전송되는 작업 항목을 완료하고 한 단계 뒤로 이동할 경우 매개 변수 <code>route</code> 또는 <code>backroute</code>에 의해 정의된 다음 노드로 작업 흐름 인스턴스를 전달합니다.<br /> 매개 변수 <code>delegatee</code> 가 전송되면 매개 변수로 식별된 작업 항목 <code>item</code> 이 지정된 참가자에게 위임됩니다.</td>
  </tr>
 </tbody>
</table>

#### WorkItem ID {#managing-a-user-inbox-by-the-workitem-id}에 의한 받은 편지함 관리

다음 HTTP 요청 메서드가 다음에 적용됩니다.

`http://localhost:4502/bin/workflow/inbox/{id}`

| HTTP 요청 메서드 | 작업 |
|---|---|
| `GET` | ID로 식별되는 받은 편지함 `WorkItem`의 데이터(정의 및 메타데이터)를 가져옵니다. |

## 예 {#examples}

### ID가 {#how-to-get-a-list-of-all-running-workflows-with-their-ids}인 모든 실행 워크플로우 목록을 가져오는 방법

실행 중인 모든 워크플로우의 목록을 보려면 GET을 사용하여 다음을 수행합니다.

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### ID가 있는 모든 실행 워크플로우 목록을 가져오는 방법 - curl {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}을 사용하여 REST

말림 사용 예:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

결과에 표시된 `uri`는 다른 명령에서 `id` 인스턴스로 사용할 수 있습니다.예를 들면 다음과 같습니다.

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>이 `curl` 명령은 `RUNNING` 대신 [워크플로 상태](/help/sites-administering/workflows.md#workflow-status-and-actions)와 함께 사용할 수 있습니다.

### 워크플로우 제목 {#how-to-change-the-workflow-title}을 변경하는 방법

워크플로우 콘솔의 **인스턴스** 탭에 표시된 **워크플로우 제목**&#x200B;을 변경하려면 `POST` 명령을 보내십시오.

* 끝: `http://localhost:4502/etc/workflow/instances/{id}`

* 다음 매개 변수와 함께 사용할 수 있습니다.

   * `action`:값은 다음과 같습니다.  `UPDATE`
   * `workflowTitle`:워크플로우 제목

#### 말림 {#how-to-change-the-workflow-title-rest-using-curl}을 사용하여 워크플로 제목 - REST를 변경하는 방법

말림 사용 예:

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### 모든 워크플로 모델 목록 방법 {#how-to-list-all-workflow-models}

사용 가능한 모든 워크플로우 모델 목록을 보려면 GET을 사용하여 다음을 수행합니다.

`http://localhost:4502/etc/workflow/models.json`

#### 모든 워크플로우 모델을 나열하는 방법 - 말림 {#how-to-list-all-workflow-models-rest-using-curl}을 사용하여 REST

말림 사용 예:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>자세한 내용은 [워크플로우 모델 관리](#managing-workflow-models)를 참조하십시오.

### WorkflowSession 개체 {#obtaining-a-workflowsession-object} 얻기

`com.adobe.granite.workflow.WorkflowSession` 클래스는 `javax.jcr.Session` 개체 또는 `org.apache.sling.api.resource.ResourceResolver` 개체에서 사용할 수 있습니다.

#### WorkflowSession 개체 얻기 - Java {#obtaining-a-workflowsession-object-java}

JSP 스크립트(또는 servlet 클래스의 Java 코드)에서 HTTP 요청 객체를 사용하여 `ResourceResolver` 객체에 대한 액세스를 제공하는 `SlingHttpServletRequest` 객체를 가져옵니다. `ResourceResolver` 개체를 `WorkflowSession`에 적용합니다.

```java
<%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
    import="com.adobe.granite.workflow.WorkflowSession,
  org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
%>
```

#### WorkflowSession 개체 얻기 - ECMA 스크립트 {#obtaining-a-workflowsession-object-ecma-script}

`sling` 변수를 사용하여 `ResourceResolver` 개체를 가져오는 데 사용하는 `SlingHttpServletRequest` 개체를 가져옵니다. `ResourceResolver` 개체를 `WorkflowSession` 개체에 적용합니다.

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### 워크플로우 모델 만들기, 읽기 또는 삭제 {#creating-reading-or-deleting-workflow-models}

다음 예는 워크플로우 모델에 액세스하는 방법을 보여줍니다.

* Java 및 ECMA 스크립트의 코드는 `WorkflowSession.createNewModel` 메서드를 사용합니다.
* curl 명령은 해당 URL을 사용하여 모델에 직접 액세스합니다.

사용된 예:

1. 모델을 만듭니다(ID `/var/workflow/models/mymodel/jcr:content/model` 포함).
1. 모델을 삭제합니다.

>[!NOTE]
>
>모델을 삭제하면 모델의 `metaData` 하위 노드의 `deleted` 속성이 `true`로 설정됩니다.
>
>삭제해도 모델 노드가 제거되지 않습니다.

새 모델을 생성할 때:

* 워크플로우 모델 편집기에서는 모델이 `/var/workflow/models` 아래의 특정 노드 구조를 사용해야 합니다. 모델의 부모 노드는 다음 속성 값을 갖는 `jcr:content` 노드가 있는 `cq:Page` 유형이어야 합니다.

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`:  `/libs/cq/workflow/templates/model`

   모델을 생성할 때 먼저 이 `cq:Page` 노드를 만들고 해당 `jcr:content` 노드를 모델 노드의 상위로 사용해야 합니다.

* 모델을 식별하기 위해 일부 메서드에서 필요로 하는 `id` 인수는 저장소의 모델 노드의 절대 경로입니다.

   `/var/workflow/models/<*model_name>*/jcr:content/model`

   >[!NOTE]
   >
   >[모든 워크플로 모델 목록 방법](#how-to-list-all-workflow-models)을 참조하십시오.

#### 워크플로우 모델 만들기, 읽기 또는 삭제 - Java {#creating-reading-or-deleting-workflow-models-java}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" import="com.adobe.granite.workflow.WorkflowSession,
                 com.adobe.granite.workflow.model.WorkflowModel,
             org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
/* Create the parent page */
String modelRepo = new String("/var/workflow/models");
String modelTemplate = new String ("/libs/cq/workflow/templates/model");
String modelName = new String("mymodel");
Page modelParent = pageManager.create(modelRepo, modelName, modelTemplate, "My workflow model");

/* create the model */
String modelId = new String(modelParent.getPath()+"/jcr:content/model")
WorkflowModel model = wfSession.createNewModel("Made using Java",modelId);

/* delete the model */
wfSession.deleteModel(modelId);
%>
```

#### 워크플로우 모델 만들기, 읽기 또는 삭제 - ECMA 스크립트 {#creating-reading-or-deleting-workflow-models-ecma-script}

```
var resolver = sling.getRequest().getResource().getResourceResolver();
var wfSession = resolver.adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
var pageManager = resolver.adaptTo(Packages.com.day.cq.wcm.api.PageManager);

//create the parent page node
var workflowPage = pageManager.create("/var/workflow/models", "mymodel", "/libs/cq/workflow/templates/model", "Created via ECMA Script");
var modelId = workflowPage.getPath()+ "/jcr:content/model";
//create the model
var model = wfSession.createNewModel("My Model", modelId);
//delete the model
var model = wfSession.deleteModel(modelId);
```

#### 워크플로우 모델 삭제 - 말림 {#deleting-a-workflow-model-rest-using-curl}을 사용하여 REST

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>필요한 세부 수준 때문에 curl은 모델을 생성 및/또는 읽을 때 실용적이지 않습니다.

### 워크플로우 상태 확인 시 시스템 워크플로우 필터링 {#filtering-out-system-workflows-when-checking-workflow-status}

[WorkflowStatus API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html)를 사용하여 노드의 워크플로 상태에 대한 정보를 검색할 수 있습니다.

다양한 메서드에는 다음과 같은 매개 변수가 있습니다.

`excludeSystemWorkflows`

이 매개 변수를 `true`으로 설정하여 시스템 작업 과정이 관련 결과에서 제외되도록 할 수 있습니다.

[시스템 워크플로로 간주할 워크플로 `Models`를 지정하는 OSGi 구성](/help/sites-deploying/configuring-osgi.md) **Adobe Granite Workflow PayloadMapCache**&#x200B;을 업데이트할 수 있습니다. 기본(런타임) 워크플로우 모델은 다음과 같습니다.

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### 참가자 이동 시간 초과 후 자동 진행 {#auto-advance-participant-step-after-a-timeout}

사전 정의된 시간 내에 완료되지 않은 **참가자** 단계를 자동으로 진행해야 하는 경우 다음을 수행할 수 있습니다.

1. OSGI 이벤트 리스너를 구현하여 작업 생성 및 수정 내용을 수신합니다.
1. 시간 제한(마감 시간)을 지정한 다음, 해당 시간에 실행할 예약된 슬링 작업을 만듭니다.
1. 시간 초과가 만료되고 작업이 트리거될 때 알림을 받는 작업 핸들러를 작성합니다.

   작업이 아직 완료되지 않은 경우 이 처리기는 작업에 필요한 작업을 수행합니다

>[!NOTE]
>
>이 방법을 사용할 수 있도록 조치를 명확히 정의해야 합니다.

### 워크플로 인스턴스 상호 작용 {#interacting-with-workflow-instances}

다음은 워크플로우 인스턴스와 상호 작용(프로그래밍)하는 방법에 대한 기본 예를 제공합니다.

#### 워크플로우 인스턴스와 상호 작용 - Java {#interacting-with-workflow-instances-java}

```java
// starting a workflow
WorkflowModel model = wfSession.getModel(workflowId);
WorkflowData wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
Workflow[] workflows workflows = wfSession.getAllWorkflows();
Workflow workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### 워크플로우 인스턴스와 상호 작용 - ECMA 스크립트 {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows(“RUNNING“);
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### 워크플로 인스턴스와 상호 작용 - 말림 {#interacting-with-workflow-instances-rest-using-curl}을(를) 사용하여 REST

* **워크플로우 시작**

   ```shell
   # starting a workflow
   curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
   
   # for example:
   curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
   ```

* **인스턴스 목록**

   ```shell
   # listing the instances
   curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
   ```

   모든 인스턴스가 나열됩니다.예를 들면 다음과 같습니다.

   ```shell
   [
       {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
       ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
   ]
   ```

   >[!NOTE]
   >
   >특정 상태의 인스턴스를 나열하려면 [실행 중인 모든 워크플로 목록](#how-to-get-a-list-of-all-running-workflows-with-their-ids)을 ID로 가져오는 방법을 참조하십시오.

* **워크플로우 일시 중단**

   ```shell
   # suspending a workflow
   curl -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **워크플로우 다시 시작**

   ```shell
   # resuming a workflow
   curl -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **워크플로우 인스턴스 종료**

   ```shell
   # terminating a workflow
   curl -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

### 작업 항목 상호 작용 {#interacting-with-work-items}

다음은 작업 항목과 상호 작용(프로그래밍) 방법에 대한 기본 예를 제공합니다.

#### 작업 항목과의 상호 작용 - Java {#interacting-with-work-items-java}

```java
// querying work items
WorkItem[] workItems = wfSession.getActiveWorkItems();
WorkItem workItem = wfSession.getWorkItem(id);

// getting routes
List<Route> routes = wfSession.getRoutes(workItem);

// delegating
Iterator<Participant> delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### 작업 항목과의 상호 작용 - ECMA 스크립트 {#interacting-with-work-items-ecma-script}

```
// querying work items
var workItems = wfSession.getActiveWorkItems();
var workItem = wfSession.getWorkItem(id);

// getting routes
var routes = wfSession.getRoutes(workItem);

// delegating
var delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### 작업 항목과의 상호 작용 - 말림 {#interacting-with-work-items-rest-using-curl}을 사용하여 REST

* **받은 편지함에서 작업 항목 나열**

   ```shell
   # listing the work items
   curl -u admin:admin http://localhost:4502/bin/workflow/inbox
   ```

   현재 받은 편지함에 있는 작업 항목에 대한 세부 사항이 나열됩니다.예를 들면 다음과 같습니다.

   ```shell
   [{
       "uri_xss": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
       "uri": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
       "currentAssignee_xss": "workflow-administrators",
       "currentAssignee": "workflow-administrators",
       "startTime": 1519656289274,
       "payloadType_xss": "JCR_PATH",
       "payloadType": "JCR_PATH",
       "payload_xss": "/content/we-retail/es/es",
       "payload": "/content/we-retail/es/es",
       "comment_xss": "Process resource is null",
       "comment": "Process resource is null",
       "type_xss": "WorkItem",
       "type": "WorkItem"
     },{
       "uri_xss": "configuration/configure_analyticstargeting",
       "uri": "configuration/configure_analyticstargeting",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/securitychecklist",
       "uri": "configuration/securitychecklist",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/enable_collectionofanonymoususagedata",
       "uri": "configuration/enable_collectionofanonymoususagedata",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/configuressl",
       "uri": "configuration/configuressl",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     }
   ```

* **작업 항목 위임**

   ```xml
   # delegating
   curl -d "item={item}&delegatee={delegatee}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_act_1&delegatee=administrators" http://localhost:4502/bin/workflow/inbox
   ```

   >[!NOTE]
   >
   >`delegatee`은(는) 워크플로우 단계에 유효한 옵션이어야 합니다.

* **다음 단계로 작업 항목 완료 또는 진행**

   ```xml
   # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
   http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
   
   # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
   curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
   ```

### 워크플로 이벤트 수신 대기 중 {#listening-for-workflow-events}

OSGi 이벤트 프레임워크를 사용하여 [ `com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html) 클래스가 정의하는 이벤트를 수신합니다. 또한 이 클래스는 이벤트의 제목에 대한 정보를 얻는 데 유용한 여러 가지 방법을 제공합니다. 예를 들어 `getWorkItem` 메서드는 이벤트에 관련된 작업 항목에 대한 `WorkItem` 객체를 반환합니다.

다음 예제 코드는 워크플로우 이벤트를 수신하고 이벤트 유형에 따라 작업을 수행하는 서비스를 정의합니다.

```java
package com.adobe.example.workflow.listeners;

import org.apache.sling.event.jobs.JobProcessor;
import org.apache.sling.event.jobs.JobUtil;

import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import com.adobe.granite.workflow.event.WorkflowEvent;
import com.adobe.granite.workflow.exec.WorkItem;

/**
 * The <code>WorkflowEventCatcher</code> class listens to workflow events.
 */
@Component(metatype=false, immediate=true)
@Service(value=org.osgi.service.event.EventHandler.class)
public class WorkflowEventCatcher implements EventHandler, JobProcessor {

 @Property(value=com.adobe.granite.workflow.event.WorkflowEvent.EVENT_TOPIC)
 static final String EVENT_TOPICS = "event.topics";

 private static final Logger logger = LoggerFactory.getLogger(WorkflowEventCatcher.class);

 public void handleEvent(Event event) {
  JobUtil.processJob(event, this);
 }

 public boolean process(Event event) {
  logger.info("Received event of topic: " + event.getTopic());
  String topic = event.getTopic();

  try {
   if (topic.equals(WorkflowEvent.EVENT_TOPIC)) {
    WorkflowEvent wfevent = (WorkflowEvent)event;
    String eventType = wfevent.getEventType();
    String instanceId = wfevent.getWorkflowInstanceId();

    if (instanceId != null) {
     //workflow instance events
     if (eventType.equals(WorkflowEvent.WORKFLOW_STARTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_RESUMED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_SUSPENDED_EVENT)) {
      // your code comes here...
     } else if (
       eventType.equals(WorkflowEvent.WORKFLOW_ABORTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_COMPLETED_EVENT)) {
      // your code comes here...
     }
     // workflow node event
     if (eventType.equals(WorkflowEvent.NODE_TRANSITION_EVENT)) {
      WorkItem currentItem = (WorkItem) event.getProperty(WorkflowEvent.WORK_ITEM);
      // your code comes here...
     }
    }
   }
  } catch(Exception e){
   logger.debug(e.getMessage());
   e.printStackTrace();
  }
  return true;
 }
}
```

