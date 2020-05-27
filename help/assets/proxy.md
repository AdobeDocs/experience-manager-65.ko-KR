---
title: 자산 프록시 개발
description: 프록시는 프록시 작업자를 사용하여 작업을 처리하는 Experience Manager 인스턴스입니다. Experience Manager 프록시, 지원되는 작업, 프록시 구성 요소 및 사용자 지정 프록시 작업자 개발 방법을 구성하는 방법에 대해 학습합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---


# 자산 프록시 개발 {#assets-proxy-development}

Adobe Experience Manager Assets는 프록시를 사용하여 특정 작업에 대한 처리를 배포합니다.

프록시는 작업을 처리하고 결과를 만드는 처리자로 프록시 작업자를 사용하는 특정(또는 경우에 따라 분리) Experience Manager 인스턴스입니다. 프록시 작업자는 다양한 작업에 사용할 수 있습니다. 자산 프록시의 경우 자산 내에서 렌더링하기 위해 자산을 로드하는 데 사용할 수 있습니다. 예를 들어 [IDS 프록시](indesign.md) 작업자는 [!DNL Adobe InDesign] 서버를 사용하여 자산에서 사용할 파일을 처리합니다.

프록시가 별도의 Experience Manager 인스턴스인 경우 Experience Manager 작성 인스턴스의 로드를 줄이는 데 도움이 됩니다. 기본적으로 자산은 동일한 JVM의 자산 처리 작업(프록시를 통해 외부화됨)을 실행하여 Experience Manager 작성 인스턴스의 로드를 줄입니다.

## 프록시(HTTP 액세스) {#proxy-http-access}

프록시는 다음 위치에서 처리 작업을 수락하도록 구성된 경우 HTTP 서블릿을 통해 사용할 수 있습니다. `/libs/dam/cloud/proxy`. 이 서블릿은 게시된 매개 변수에서 슬링 작업을 생성합니다. 그러면 프록시 작업 대기열에 추가되고 해당 프록시 작업자에 연결됩니다.

### 지원되는 작업 {#supported-operations}

* `job`

   **요구 사항**: 이 매개 변수는 직렬화된 값 맵으로 설정해야 `jobevent` 합니다. 작업 프로세서용 `Event` 을 만드는 데 사용됩니다.

   **결과**: 새 작업을 추가합니다. 성공하면 고유한 작업 ID가 반환됩니다.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **요구 사항**: 매개 변수를 설정해야 `jobid` 합니다.

   **결과**: 작업 프로세서에서 만든 결과 노드의 JSON 표현을 반환합니다.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **요구 사항**: 매개 변수 jobid를 설정해야 합니다.

   **결과**: 주어진 작업과 연관된 리소스를 반환합니다.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **요구 사항**: 매개 변수 jobid를 설정해야 합니다.

   **결과**: 발견된 경우 작업을 제거합니다.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Proxy Worker {#proxy-worker}

프록시 작업자는 작업을 처리하고 결과를 만드는 책임을 지는 프로세서입니다. 작업자는 프록시 인스턴스에 상주하며 [프록시 작업자로 인식되도록](https://sling.apache.org/site/eventing-and-jobs.html) 처리 과정을 구현해야 합니다.

>[!NOTE]
>
>작업자는 [프록시](https://sling.apache.org/site/eventing-and-jobs.html) 작업자로 인식되도록 처리 작업 프로세서를 구현해야 합니다.

### 클라이언트 API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) 작업 생성, 작업 제거 및 해당 작업에서 결과를 얻는 방법을 제공하는 OSGi 서비스로 사용할 수 있습니다. 이 서비스의 기본 구현(`JobServiceImpl`)은 HTTP 클라이언트를 사용하여 원격 프록시 서블릿과 통신합니다.

다음은 API 사용의 예입니다.

```java
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### 클라우드 서비스 구성 {#cloud-service-configurations}

>[!NOTE]
>
>프록시 API에 대한 참조 설명서는 아래에서 확인할 수 있습니다 [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).

Assets **Tools 콘솔 또는 아래에서 액세스할 수 있는 클라우드 서비스 구성을 통해 프록시 및 프록시** 작업자 구성을 모두 사용할 수 있습니다 `/etc/cloudservices/proxy`. 각 프록시 작업자는 작업자별 구성 세부 정보 `/etc/cloudservices/proxy` (예: `/etc/cloudservices/proxy/workername`)에 대한 노드를 추가해야 합니다.

>[!NOTE]
>
>자세한 내용은 [InDesign Server 프록시 작업자 구성](indesign.md#configuring-the-proxy-worker-for-indesign-server) 및 [클라우드 서비스 구성을](../sites-developing/extending-cloud-config.md) 참조하십시오.

다음은 API 사용의 예입니다.

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### 사용자 지정된 프록시 작업자 개발 {#developing-a-customized-proxy-worker}

IDS [프록시 작업자](indesign.md) 는 InDesign 자산의 처리를 아웃소싱하기 위해 이미 기본적으로 제공되는 에셋 프록시 작업자의 예입니다.

또한 자체 Assets 프록시 작업자를 개발 및 구성하여 전문 작업자를 만들어 Assets 처리 작업을 전달하고 아웃소싱할 수도 있습니다.

자신만의 고유한 사용자 지정 프록시 레이어를 설정하려면 다음을 수행해야 합니다.

* 설정 및 구현(Sling 이벤트 사용):

   * 사용자 정의 작업 주제
   * 사용자 지정 작업 이벤트 처리기

* 그런 다음 JobService API를 사용하여 다음을 수행합니다.

   * 사용자 지정 작업을 프록시에 전달합니다.
   * 작업 관리

* 워크플로에서 프록시를 사용하려면 WorkflowExternalProcess API 및 JobService API를 사용하여 사용자 지정 외부 단계를 구현해야 합니다.

다음 다이어그램과 단계는 진행하는 방법에 대해 자세히 설명합니다.

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>다음 단계에서 InDesign 상당 부분이 참조 예로 표시됩니다.

1. Sling 작업 [이](https://sling.apache.org/site/eventing-and-jobs.html) 사용되므로 사용 사례에 대한 작업 항목을 정의해야 합니다.

   예를 들어 IDS 프록시 작업자 `IDSJob.IDS_EXTENDSCRIPT_JOB` 에 대해 참조하십시오.

1. 외부 단계는 이벤트를 트리거한 다음 완료될 때까지 기다리는 데 사용됩니다. 이것은 id를 폴링하여 수행됩니다. 새 기능을 구현하려면 자신만의 단계를 개발해야 합니다.

   작업 이벤트 `WorkflowExternalProcess`를 구현한 다음 JobService API와 작업 항목을 사용하여 작업 이벤트를 준비한 다음 JobService(OSGi 서비스)에 전달합니다.

   예를 들어 IDS 프록시 `INDDMediaExtractProcess`작업자의 경우.java를 참조하십시오.

1. 주제에 대한 작업 핸들러를 구현합니다. 이 처리기는 특정 작업을 수행하고 작업자 구현으로 간주되도록 개발을 필요로 합니다.

   예를 들어 IDS 프록시 작업자 `IDSJobProcessor.java` 에 대해 참조하십시오.

1. 댐 `ProxyUtil.java` 에서 사용 그러면 dam 프록시를 사용하여 작업자에게 작업을 전달할 수 있습니다.

>[!NOTE]
>
>Assets 프록시 프레임워크에서 제공하지 않는 것은 풀 메커니즘입니다.
>
>이 [!DNL InDesign] 통합을 통해 [!DNL InDesign] 서버 풀(IDSPool)에 액세스할 수 있습니다. 이 풀링은 통합 전용이며 [!DNL InDesign] [!DNL Assets] 프록시 프레임워크의 일부가 아닙니다.

>[!NOTE]
>
>결과 동기화:
>
>동일한 프록시를 사용하는 인스턴스가 없으면 처리 결과는 프록시에 유지됩니다. 작업을 만들 때 클라이언트에 제공된 것과 동일한 고유한 작업 ID를 사용하여 결과를 요청하는 것은 클라이언트(Experience Manager 작성자)의 작업입니다. 프록시는 작업을 완료하고 결과를 요청할 준비가 되도록 유지합니다.
