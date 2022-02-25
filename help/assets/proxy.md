---
title: '"[!DNL Assets] 프록시 개발"'
description: 프록시는 [!DNL Experience Manager] 프록시 작업자를 사용하여 작업을 처리하는 인스턴스입니다. 구성 방법 알아보기 [!DNL Experience Manager] 프록시, 지원되는 작업, 프록시 구성 요소 및 사용자 정의 프록시 작업자를 개발하는 방법
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# [!DNL Assets] 프록시 개발 {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] 프록시를 사용하여 특정 작업에 대한 처리를 배포합니다.

프록시는 작업을 처리하고 결과를 생성하는 처리자로 프록시 작업자를 사용하는 특정(및 경우에 따라 별개인) Experience Manager 인스턴스입니다. 프록시 작업자는 다양한 작업에 사용될 수 있습니다. 의 경우 [!DNL Assets] 프록시 자산 내에서 렌더링하기 위해 자산을 로드하는 데 사용할 수 있습니다. 예: [ID 프록시 작업자](indesign.md) 사용 [!DNL Adobe InDesign] Assets에서 사용할 파일을 처리하는 서버입니다.

프록시가 별도의 경우 [!DNL Experience Manager] 인스턴스 이렇게 하면 [!DNL Experience Manager] 작성 인스턴스. 기본적으로 [!DNL Assets] 에서는 자산 처리 작업을 동일한 JVM(프록시를 통해 외부화됨)에서 실행하여 [!DNL Experience Manager] 작성 인스턴스.

## 프록시(HTTP 액세스) {#proxy-http-access}

프록시는 다음에 처리 작업을 수락하도록 구성된 경우 HTTP 서블릿을 통해 사용할 수 있습니다. `/libs/dam/cloud/proxy`. 이 서블릿은 게시된 매개 변수에서 sling 작업을 생성합니다. 그러면 프록시 작업 큐에 추가되고 해당 프록시 작업자에 연결됩니다.

### 지원되는 작업 {#supported-operations}

* `job`

   **요구 사항**: 매개 변수 `jobevent` 직렬화된 값 맵으로 설정해야 합니다. 이 템플릿은 `Event` 작업 처리자용.

   **결과**: 새 작업을 추가합니다. 성공하면 고유 작업 ID가 반환됩니다.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **요구 사항**: 매개 변수 `jobid` 설정해야 합니다.

   **결과**: 작업 프로세서에서 만든 결과 노드의 JSON 표현을 반환합니다.

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **요구 사항**: 매개 변수 jobid를 설정해야 합니다.

   **결과**: 지정된 작업과 연결된 리소스를 반환합니다.

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **요구 사항**: 매개 변수 jobid를 설정해야 합니다.

   **결과**: 찾은 경우 작업을 제거합니다.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### 프록시 작업자 {#proxy-worker}

프록시 작업자는 작업 처리 및 결과 생성을 담당하는 프로세서입니다. 작업자는 프록시 인스턴스에 상주하며 다음을 구현해야 합니다 [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) 프록시 작업자로 인식될 수 있습니다.

>[!NOTE]
>
>작업자는 [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) 프록시 작업자로 인식될 수 있습니다.

### 클라이언트 API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) 는 작업을 만들고, 작업을 제거하고, 해당 작업에서 결과를 가져오는 방법을 제공하는 OSGi 서비스로 사용할 수 있습니다. 이 서비스의 기본 구현(`JobServiceImpl`)은 HTTP 클라이언트를 사용하여 원격 프록시 서블릿과 통신합니다.

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

### Cloud Service 구성 {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

프록시 및 프록시 작업자 구성은 모두 [!DNL Assets] **도구** 콘솔 또는 아래의 `/etc/cloudservices/proxy`. 각 프록시 작업자는 `/etc/cloudservices/proxy` 작업자 특정 구성 세부 정보(예: `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>자세한 내용은 [InDesign Server 프록시 작업자 구성](indesign.md#configuring-the-proxy-worker-for-indesign-server) 및 [Cloud Services 구성](../sites-developing/extending-cloud-config.md) 추가 정보.

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

다음 [ID 프록시 작업자](indesign.md) 는 [!DNL Assets] InDesign 자산 처리를 아웃소싱하기 위해 이미 기본적으로 제공되는 프록시 작업자.

직접 개발하고 구성할 수도 있습니다 [!DNL Assets] 전문 작업자를 생성하여 [!DNL Assets] 처리 작업.

고유한 사용자 지정 프록시 작업자를 설정하려면 다음을 수행해야 합니다.

* 설정 및 구현(Sling 이벤트 사용):

   * 사용자 정의 작업 주제
   * 사용자 지정 작업 이벤트 처리기

* 그런 다음 JobService API를 사용하여 다음을 수행합니다.

   * 프록시에 사용자 지정 작업 발송
   * 작업 관리

* 워크플로우의 프록시를 사용하려면 WorkflowExternalProcess API 및 JobService API를 사용하여 사용자 지정 외부 단계를 구현해야 합니다.

다음 다이어그램과 단계는 진행 방법에 대해 자세히 설명합니다.

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>다음 단계에서 InDesign 상당 부분은 참조 예로 표시됩니다.

1. A [Sling 작업](https://sling.apache.org/site/eventing-and-jobs.html) 가 사용되므로 사용 사례에 대한 작업 항목을 정의해야 합니다.

   예를 들어 `IDSJob.IDS_EXTENDSCRIPT_JOB` ID 프록시 작업자에 대한 정보입니다.

1. 외부 단계는 이벤트를 트리거한 다음 완료될 때까지 기다리는 데 사용됩니다. 이 작업은 id를 폴링하여 수행됩니다. 새 기능을 구현하려면 자체 단계를 개발해야 합니다.

   구현 `WorkflowExternalProcess`그런 다음 JobService API 및 작업 항목을 사용하여 작업 이벤트를 준비하고 JobService(OSGi 서비스)에 발송합니다.

   예를 들어 `INDDMediaExtractProcess`IDS 프록시 작업자의 .java입니다.

1. 항목의 작업 핸들러를 구현합니다. 이 처리기는 특정 작업을 수행하고 작업자 구현으로 간주되도록 개발을 필요로 합니다.

   예를 들어 `IDSJobProcessor.java` ID 프록시 작업자에 대한 정보입니다.

1. 사용 `ProxyUtil.java` dam-commons에서 사용할 수 있습니다. 이를 통해 dam 프록시를 사용하여 작업자에게 작업을 전달할 수 있습니다.

>[!NOTE]
>
>무슨 [!DNL Assets] 프록시 프레임워크는 풀 메커니즘으로 기본 제공 기능을 제공하지 않습니다.
>
>다음 [!DNL InDesign] 통합을 통해 풀 액세스 가능 [!DNL InDesign] 서버(IDSPool). 이 풀링은 다음과 같습니다 [!DNL InDesign] 통합 및 일부가 아님 [!DNL Assets] 프록시 프레임워크.

>[!NOTE]
>
>결과 동기화:
>
>동일한 프록시를 사용하는 인스턴스가 없는 경우 처리 결과는 프록시에 유지됩니다. 작업 생성 시 클라이언트에 제공된 것과 동일한 고유한 작업 ID를 사용하여 결과를 요청하는 것은 클라이언트(Experience Manager 작성자)의 작업입니다. 프록시는 작업을 완료하고 결과를 요청할 준비가 된 상태로 유지합니다.
