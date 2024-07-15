---
title: 프로그래밍 방식으로 워크플로우와 상호 작용
description: Adobe Experience Manager에서 프로그래밍 방식으로 워크플로우와 상호 작용하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 2b396850-e9fb-46d9-9daa-ebd410a9e1a5
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 0%

---

# 프로그래밍 방식으로 워크플로우와 상호 작용{#interacting-with-workflows-programmatically}

[워크플로 사용자 지정 및 확장](/help/sites-developing/workflows-customizing-extending.md)할 때 워크플로 개체에 액세스할 수 있습니다.

* [워크플로우 Java API 사용](#using-the-workflow-java-api)
* [ECMA 스크립트에서 워크플로우 개체 가져오기](#obtaining-workflow-objects-in-ecma-scripts)
* [워크플로우 REST API 사용](#using-the-workflow-rest-api)

## 워크플로우 Java API 사용 {#using-the-workflow-java-api}

워크플로우 Java API는 [`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) 패키지와 여러 하위 패키지로 구성됩니다. API의 가장 중요한 멤버는 `com.adobe.granite.workflow.WorkflowSession` 클래스입니다. `WorkflowSession` 클래스는 디자인 타임 및 런타임 워크플로 개체에 모두 액세스할 수 있습니다.

* 워크플로 모델
* 작업 항목
* 워크플로 인스턴스
* 워크플로우 데이터
* 받은 편지함 항목

이 클래스는 워크플로우 주기에 개입하는 몇 가지 방법도 제공합니다.

다음 표에서는 워크플로우와 프로그래밍 방식으로 상호 작용할 때 사용할 여러 주요 Java 개체의 참조 설명서에 대한 링크를 제공합니다. 다음 예제에서는 코드에서 클래스 개체를 가져오고 사용하는 방법을 보여 줍니다.

| 기능 | 개체 |
|---|---|
| 워크플로우 액세스 | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| 워크플로우 인스턴스 실행 및 쿼리 | [`Workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| 워크플로우 모델 관리 | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| 워크플로우에 있는(또는 없는) 노드에 대한 정보 | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## ECMA 스크립트에서 워크플로우 개체 가져오기 {#obtaining-workflow-objects-in-ecma-scripts}

[스크립트 찾기](/help/sites-developing/the-basics.md#locating-the-script)에 설명된 대로 AEM(Apache Sling을 통해)은 서버측 ECMA 스크립트를 실행하는 ECMA 스크립트 엔진을 제공합니다. [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) 클래스는 스크립트에서 `sling` 변수로 즉시 사용할 수 있습니다.

`ScriptHelper` 클래스는 `WorkflowSession` 개체를 얻는 데 사용할 수 있는 `SlingHttpServletRequest`에 대한 액세스를 제공합니다. 예:

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## 워크플로우 REST API 사용 {#using-the-workflow-rest-api}

워크플로우 콘솔에서는 REST API를 많이 사용하므로 이 페이지에서는 워크플로우용 REST API에 대해 설명합니다.

>[!NOTE]
>
>curl 명령줄 도구를 사용하면 Workflow REST API를 사용하여 워크플로 개체에 액세스하고 인스턴스 주기를 관리할 수 있습니다. 이 페이지 전체의 예제에서는 curl 명령줄 도구를 통해 REST API를 사용하는 방법을 보여 줍니다.

REST API에서는 다음 작업이 지원됩니다.

* 워크플로우 서비스 시작 또는 중지
* 워크플로우 모델 만들기, 업데이트 또는 삭제
* [워크플로 인스턴스 시작, 일시 중단, 다시 시작 또는 종료](/help/sites-administering/workflows.md#workflow-status-and-actions)
* 작업 항목 완료 또는 위임

>[!NOTE]
>
>웹 개발을 위한 Firefox 확장 프로그램인 Firebug를 사용하면 콘솔을 작동할 때 HTTP 트래픽을 추적할 수 있습니다. 예를 들어 `POST` 요청을 사용하여 AEM 서버로 전송된 매개 변수와 값을 확인할 수 있습니다.

이 페이지에서는 AEM이 포트 `4502`의 localhost에서 실행되고 설치 컨텍스트가 &quot; `/`&quot;(루트)이라고 가정합니다. 설치에 해당되지 않는 경우 HTTP 요청이 적용되는 URI를 그에 따라 조정해야 합니다.

`GET` 요청에 지원되는 렌더링은 JSON 렌더링입니다. `GET`의 URL에는 `.json` 확장명이 있어야 합니다. 예:

`http://localhost:4502/etc/workflow.json`

### 워크플로우 인스턴스 관리 {#managing-workflow-instances}

다음 HTTP 요청 메서드는에 적용됩니다.

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>액션</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>사용 가능한 워크플로우 인스턴스를 나열합니다.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>새 워크플로우 인스턴스를 만듭니다. 매개 변수는 다음과 같습니다. <br /> - <code>model</code>: 각 워크플로 모델의 ID(URI)<br /> - <code>payloadType</code>: 페이로드 유형(예: <code>JCR_PATH</code> 또는 URL)을 포함합니다.<br /> 페이로드가 <code>payload</code> 매개 변수로 전송됩니다. 새 워크플로우 인스턴스 리소스의 URL이 포함된 위치 헤더로 <code>201</code>(<code>CREATED</code>) 응답이 다시 전송됩니다.</p> </td>
  </tr>
 </tbody>
</table>

#### 상태별 워크플로 인스턴스 관리 {#managing-a-workflow-instance-by-its-state}

다음 HTTP 요청 메서드는에 적용됩니다.

`http://localhost:4502/etc/workflow/instances.{state}`

| HTTP 요청 메서드 | 액션 |
|---|---|
| `GET` | 사용 가능한 워크플로 인스턴스 및 해당 상태(`RUNNING`, `SUSPENDED`, `ABORTED` 또는 `COMPLETED`)를 나열합니다. |

#### ID로 워크플로 인스턴스 관리 {#managing-a-workflow-instance-by-its-id}

다음 HTTP 요청 메서드는에 적용됩니다.

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>액션</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>해당 워크플로우 모델에 대한 링크를 포함하는 인스턴스 데이터(정의 및 메타데이터)를 가져옵니다.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>인스턴스의 상태를 변경합니다. 새 상태가 매개 변수 <code>state</code>(으)로 전송되며 <code>RUNNING</code>, <code>SUSPENDED</code> 또는 <code>ABORTED</code> 값 중 하나를 가져야 합니다.<br /> 새 상태에 연결할 수 없는 경우(예: 종료된 인스턴스를 일시 중단하는 경우) <code>409</code>(<code>CONFLICT</code>) 응답이 클라이언트로 다시 전송됩니다.</td>
  </tr>
 </tbody>
</table>

### 워크플로우 모델 관리 {#managing-workflow-models}

다음 HTTP 요청 메서드는에 적용됩니다.

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>액션</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>사용 가능한 워크플로우 모델을 나열합니다.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>새 워크플로우 모델을 만듭니다. 매개 변수 <code>title</code>을(를) 보내면 지정된 제목으로 새 모델이 만들어집니다. JSON 모델 정의를 매개 변수 <code>model</code>(으)로 첨부하면 제공된 정의에 따라 새 워크플로 모델이 만들어집니다.<br /> 새 워크플로 모델 리소스의 URL이 포함된 위치 헤더로 <code>201</code> 응답(<code>CREATED</code>)이 다시 전송됩니다.<br /> 모델 정의가 <code>modelfile</code>(이)라는 파일 매개 변수로 첨부된 경우에도 마찬가지입니다.<br /> <code>model</code> 및 <code>modelfile</code> 매개 변수의 경우 모두 serialization 형식을 정의하려면 <code>type</code>이라는 추가 매개 변수가 필요합니다. OSGI API를 사용하여 새로운 직렬화 형식을 통합할 수 있습니다. 표준 JSON 직렬 변환기는 워크플로우 엔진과 함께 제공됩니다. 유형은 JSON입니다. 형식의 예는 아래를 참조하십시오.</td>
  </tr>
 </tbody>
</table>

예: 브라우저에서 `http://localhost:4502/etc/workflow/models.json`에 대한 요청은 다음과 유사한 json 응답을 생성합니다.

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

다음 HTTP 요청 메서드는에 적용됩니다.

`http://localhost:4502*{uri}*`

여기서 `*{uri}*`은(는) 저장소의 모델 노드에 대한 경로입니다.

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>액션</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>모델의 <code>HEAD</code> 버전(정의 및 메타데이터)을 가져옵니다.</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>모델의 <code>HEAD</code> 버전을 업데이트합니다(새 버전을 만듭니다).<br /> 새 버전의 모델에 대한 전체 모델 정의를 <code>model</code> 매개 변수로 추가해야 합니다. 또한 새 모델을 만들 때와 마찬가지로 <code>type</code> 매개 변수가 필요하며 값은 <code>JSON</code>.<br />이어야 합니다. </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>PUT과 동일한 비헤이비어. AEM 위젯이 <code>PUT</code> 작업을 지원하지 않으므로 필요합니다.</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>모델을 삭제합니다. 방화벽/프록시 문제를 해결하기 위해 값이 <code>DELETE</code>인 <code>X-HTTP-Method-Override</code> 헤더 항목이 포함된 <code>POST</code>도 <code>DELETE</code> 요청으로 허용됩니다.</td>
  </tr>
 </tbody>
</table>

예: 브라우저에서 `http://localhost:4502/var/workflow/models/publish_example.json`에 대한 요청이 다음 코드와 유사한 `json` 응답을 반환합니다.

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

#### 버전별 워크플로우 모델 관리 {#managing-a-workflow-model-by-its-version}

다음 HTTP 요청 메서드는에 적용됩니다.

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| HTTP 요청 메서드 | 액션 |
|---|---|
| `GET` | 지정된 버전(있는 경우)의 모델 데이터를 가져옵니다. |

### (사용자) 받은 편지함 관리 {#managing-user-inboxes}

다음 HTTP 요청 메서드는에 적용됩니다.

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>HTTP 요청 메서드</td>
   <td>액션</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>HTTP 인증 헤더로 식별되는 사용자의 받은 편지함에 있는 작업 항목을 나열합니다.</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>URI가 매개 변수 <code>item</code>(으)로 전송되는 작업 항목을 완료하고 단계를 거치는 경우 해당 워크플로 인스턴스를 <code>route</code> 또는 <code>backroute</code> 매개 변수로 정의된 다음 노드로 진행합니다.<br /> 매개 변수 <code>delegatee</code>이(가) 전송되면 <code>item</code> 매개 변수로 식별된 작업 항목이 지정된 참가자에게 위임됩니다.</td>
  </tr>
 </tbody>
</table>

#### WorkItem ID로 (사용자) 받은 편지함 관리 {#managing-a-user-inbox-by-the-workitem-id}

다음 HTTP 요청 메서드는에 적용됩니다.

`http://localhost:4502/bin/workflow/inbox/{id}`

| HTTP 요청 메서드 | 액션 |
|---|---|
| `GET` | ID로 식별된 받은 편지함 `WorkItem`의 데이터(정의 및 메타데이터)를 가져옵니다. |

## 예 {#examples}

### ID를 사용하여 실행 중인 모든 워크플로우 목록을 가져오는 방법 {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

실행 중인 모든 워크플로 목록을 가져오려면 GET으로 다음을 수행하십시오.

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### ID를 사용하여 실행 중인 모든 워크플로우 목록을 가져오는 방법 - curl을 사용하여 REST {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

curl 사용 예:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

결과에 표시된 `uri`을(를) 다른 명령에서 `id` 인스턴스로 사용할 수 있습니다. 예:

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>이 `curl` 명령은 `RUNNING` 대신 [워크플로 상태](/help/sites-administering/workflows.md#workflow-status-and-actions)와 함께 사용할 수 있습니다.

### 워크플로우 제목을 변경하는 방법 {#how-to-change-the-workflow-title}

워크플로 콘솔의 **인스턴스** 탭에 표시되는 **워크플로 제목**&#x200B;을 변경하려면 `POST` 명령을 보냅니다.

* 받는 사람: `http://localhost:4502/etc/workflow/instances/{id}`

* 다음 매개 변수를 사용하여

   * `action`: 해당 값은 `UPDATE`이어야 합니다.
   * `workflowTitle`: 워크플로 제목

#### 워크플로우 제목을 변경하는 방법 - CURL을 사용하여 REST {#how-to-change-the-workflow-title-rest-using-curl}

curl 사용 예:

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### 모든 워크플로우 모델을 나열하는 방법 {#how-to-list-all-workflow-models}

사용 가능한 모든 워크플로 모델 목록을 가져오려면 GET을 수행하여 다음을 수행합니다.

`http://localhost:4502/etc/workflow/models.json`

#### 모든 워크플로우 모델을 나열하는 방법 - CURL을 사용하여 REST {#how-to-list-all-workflow-models-rest-using-curl}

curl 사용 예:

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>[워크플로 모델 관리](#managing-workflow-models)도 참조하세요.

### WorkflowSession 개체 가져오기 {#obtaining-a-workflowsession-object}

`com.adobe.granite.workflow.WorkflowSession` 클래스는 `javax.jcr.Session` 개체 또는 `org.apache.sling.api.resource.ResourceResolver` 개체에서 조정할 수 있습니다.

#### WorkflowSession 개체 가져오기 - Java {#obtaining-a-workflowsession-object-java}

JSP 스크립트(또는 서블릿 클래스에 대한 Java 코드)에서 HTTP 요청 개체를 사용하여 `ResourceResolver` 개체에 대한 액세스를 제공하는 `SlingHttpServletRequest` 개체를 가져옵니다. `ResourceResolver` 개체를 `WorkflowSession`(으)로 조정합니다.

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

#### WorkflowSession 개체 가져오기 - ECMA 스크립트 {#obtaining-a-workflowsession-object-ecma-script}

`ResourceResolver` 개체를 가져오는 데 사용하는 `SlingHttpServletRequest` 개체를 가져오려면 `sling` 변수를 사용하십시오. `ResourceResolver` 개체를 `WorkflowSession` 개체로 조정하십시오.

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### 워크플로우 모델 만들기, 읽기 또는 삭제 {#creating-reading-or-deleting-workflow-models}

다음 예는 워크플로우 모델에 액세스하는 방법을 보여 줍니다.

* Java 및 ECMA 스크립트용 코드는 `WorkflowSession.createNewModel` 메서드를 사용합니다.
* curl 명령은 해당 URL을 사용하여 모델에 직접 액세스합니다.

사용된 예는 다음과 같습니다.

1. ID가 `/var/workflow/models/mymodel/jcr:content/model`인 모델을 만듭니다.
1. 모델을 삭제합니다.

>[!NOTE]
>
>모델을 삭제하면 모델의 `metaData` 자식 노드의 `deleted` 속성이 `true`(으)로 설정됩니다.
>
>삭제해도 모델 노드는 제거되지 않습니다.

모델을 만들 때:

* 워크플로 모델 편집기를 사용하려면 모델이 `/var/workflow/models` 아래의 특정 노드 구조를 사용해야 합니다. 모델의 부모 노드는 다음 속성 값을 가진 `jcr:content` 노드가 있는 `cq:Page` 형식이어야 합니다.

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`: `/libs/cq/workflow/templates/model`

  모델을 만들 때는 먼저 이 `cq:Page` 노드를 만들고 해당 `jcr:content` 노드를 모델 노드의 부모로 사용해야 합니다.

* 일부 메서드에서 모델을 식별하는 데 필요한 `id` 인수는 저장소의 모델 노드의 절대 경로입니다.

  `/var/workflow/models/<*model_name>*/jcr:content/model`

  >[!NOTE]
  >
  >[모든 워크플로 모델을 나열하는 방법](#how-to-list-all-workflow-models)을 참조하세요.

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

#### 워크플로우 모델 삭제 - curl을 사용하여 REST {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>필요한 세부 수준으로 인해 curl은 모델을 생성 및/또는 읽는 데 실용적이지 않은 것으로 간주됩니다.

### 워크플로우 상태 확인 시 시스템 워크플로우 필터링 {#filtering-out-system-workflows-when-checking-workflow-status}

[WorkflowStatus API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html)를 사용하여 노드의 워크플로 상태에 대한 정보를 검색할 수 있습니다.

다양한 메서드에는 매개 변수가 있습니다.

`excludeSystemWorkflows`

이 매개 변수는 관련 결과에서 시스템 워크플로를 제외하도록 `true`(으)로 설정할 수 있습니다.

[OSGi 구성을 업데이트할 수 있습니다](/help/sites-deploying/configuring-osgi.md) **Adobe Granite 워크플로 PayloadMapCache**. 이 워크플로는 시스템 워크플로로 간주할 워크플로 `Models`을(를) 지정합니다. 기본(런타임) 워크플로우 모델은 다음과 같습니다.

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### 시간 제한 후 참가자 자동 이동 단계 {#auto-advance-participant-step-after-a-timeout}

사전 정의된 시간 내에 완료되지 않은 **참가자** 단계를 자동으로 진행해야 하는 경우 다음을 수행할 수 있습니다.

1. 작업 생성 및 수정 시 수신할 OSGI 이벤트 리스너를 구현합니다.
1. 시간 제한(기한)을 지정한 다음 해당 시간에 실행할 예약된 슬링 작업을 만듭니다.
1. 시간 제한이 만료되고 작업을 트리거할 때 알림을 받는 작업 핸들러를 작성합니다.

   작업이 아직 완료되지 않은 경우 이 처리기가 작업에 필요한 작업을 수행합니다.

>[!NOTE]
>
>이 접근법을 사용할 수 있으려면 취해야 할 행동이 명확하게 정의되어야 한다.

### 워크플로우 인스턴스와 상호 작용 {#interacting-with-workflow-instances}

다음은 워크플로 인스턴스와 상호 작용하는 방법(프로그래밍 방식으로)에 대한 기본적인 예제를 제공합니다.

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
var workflows = wfSession.getWorkflows("RUNNING");
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### 워크플로우 인스턴스와 상호 작용 - curl을 사용하여 REST {#interacting-with-workflow-instances-rest-using-curl}

* **워크플로우 시작**

  ```shell
  # starting a workflow
  curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
  
  # for example:
  curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
  ```

* **인스턴스 나열**

  ```shell
  # listing the instances
  curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
  ```

  모든 인스턴스가 나열됩니다. 예:

  ```shell
  [
      {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
      ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
  ]
  ```

  >[!NOTE]
  >
  >특정 상태의 인스턴스 목록을 만들려면 해당 ID를 사용하여 [실행 중인 모든 워크플로의 목록을 가져오는 방법](#how-to-get-a-list-of-all-running-workflows-with-their-ids)을 참조하십시오.

* **워크플로 일시 중단**

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

* **워크플로 인스턴스 종료**

  ```shell
  # terminating a workflow
  curl -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/{id}
  
  # for example:
  curl -u admin:admin -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
  ```

### 작업 항목과 상호 작용 {#interacting-with-work-items}

다음은 작업 항목과 상호 작용하는(프로그래밍 방식으로) 방법에 대한 기본 예제를 제공합니다.

#### 작업 항목과 상호 작용 - Java {#interacting-with-work-items-java}

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

#### 작업 항목과 상호 작용 - ECMA 스크립트 {#interacting-with-work-items-ecma-script}

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

#### 작업 항목과 상호 작용 - curl을 사용한 REST {#interacting-with-work-items-rest-using-curl}

* **받은 편지함에서 작업 항목 나열**

  ```shell
  # listing the work items
  curl -u admin:admin http://localhost:4502/bin/workflow/inbox
  ```

  받은 편지함에 있는 작업 항목에 대한 세부 정보가 나열됩니다. 예:

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
  >`delegatee`은(는) 워크플로 단계에 유효한 옵션이어야 합니다.

* **다음 단계로 작업 항목 완료 또는 진행 중**

  ```xml
  # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
  http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
  
  # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
  curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
  
  # for example:
  curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
  ```

### 워크플로우 이벤트 수신 {#listening-for-workflow-events}

OSGi 이벤트 프레임워크를 사용하여 [`com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html) 클래스에서 정의하는 이벤트를 수신합니다. 이 클래스에서는 이벤트 주제에 대한 정보를 얻는 데 유용한 몇 가지 방법도 제공합니다. 예를 들어 `getWorkItem` 메서드는 이벤트와 관련된 작업 항목에 대한 `WorkItem` 개체를 반환합니다.

다음 예제 코드는 워크플로 이벤트를 수신하고 이벤트 유형에 따라 작업을 수행하는 서비스를 정의합니다.

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
