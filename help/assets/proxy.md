---
title: "[!DNL Assets] 프록시 개발"
description: 프록시는 [!DNL Experience Manager] 프록시 작업자를 사용하여 작업을 처리하는 인스턴스입니다. 구성 방법 알아보기 [!DNL Experience Manager] 프록시, 지원되는 작업, 프록시 구성 요소 및 사용자 지정 프록시 작업자를 개발하는 방법.
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# [!DNL Assets] 프록시 개발 {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] 프록시를 사용하여 특정 작업에 대한 처리를 분산합니다.

프록시는 프록시 작업자를 작업 처리 및 결과 생성을 담당하는 처리자로 사용하는 특정(및 경우에 따라 별도의) Experience Manager 인스턴스입니다. 프록시 작업자는 매우 다양한 작업에 사용할 수 있습니다. 의 경우에는 [!DNL Assets] 프록시 자산 내에서 렌더링할 자산을 로드하는 데 사용할 수 있습니다. 예를 들어 [IDS 프록시 작업자](indesign.md) 다음 사용: [!DNL Adobe InDesign] 에셋에서 사용할 파일을 처리하는 서버입니다.

프록시가 별개인 경우 [!DNL Experience Manager] 인스턴스 를 사용하면 [!DNL Experience Manager] 작성 인스턴스. 기본적으로, [!DNL Assets] 은 동일한 JVM(프록시를 통해 외부화됨)에서 자산 처리 작업을 실행하여 의 로드를 줄입니다. [!DNL Experience Manager] 작성 인스턴스.

## 프록시(HTTP 액세스) {#proxy-http-access}

다음 위치의 처리 작업을 수락하도록 구성된 경우 HTTP 서블릿을 통해 프록시를 사용할 수 있습니다. `/libs/dam/cloud/proxy`. 이 서블릿은 게시된 매개 변수에서 슬링 작업을 만듭니다. 그런 다음 프록시 작업 대기열에 추가되고 해당 프록시 작업자에 연결됩니다.

### 지원되는 작업 {#supported-operations}

* `job`

  **요구 사항**: 매개 변수 `jobevent` 은(는) 직렬화된 값 맵으로 설정해야 합니다. 다음을 만드는 데 사용됩니다. `Event` 작업 처리자의 경우.

  **결과**: 새 작업을 추가합니다. 성공하면 고유한 작업 ID가 반환됩니다.

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

  **요구 사항**: 매개 변수 `jobid` 을(를) 설정해야 합니다.

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

  **결과**: 작업이 있는 경우 제거합니다.

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### 프록시 작업자 {#proxy-worker}

프록시 작업자는 작업을 처리하고 결과를 만드는 역할을 담당하는 프로세서입니다. 작업자는 프록시 인스턴스에 상주하며 다음을 구현해야 합니다. [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) 프록시 작업자로 인식될 수 있습니다.

>[!NOTE]
>
>작업자는 다음을 구현해야 합니다. [sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) 프록시 작업자로 인식될 수 있습니다.

### 클라이언트 API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) 는 작업을 만들고, 작업을 제거하고, 해당 작업에서 결과를 가져오는 메서드를 제공하는 OSGi 서비스로 사용할 수 있습니다. 이 서비스의 기본 구현(`JobServiceImpl`)는 HTTP 클라이언트를 사용하여 원격 프록시 서블릿과 통신합니다.

다음은 API 사용의 예입니다.

```java
@Reference
 JobService proxyJobService;

 // to create a job
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

프록시 및 프록시 작업자 구성은 모두 클라우드 서비스 구성을 통해 사용할 수 있습니다. [!DNL Assets] **도구** 콘솔 또는 그 이하 `/etc/cloudservices/proxy`. 각 프록시 작업자는 아래에 노드를 추가해야 합니다. `/etc/cloudservices/proxy` 작업자별 구성 세부 정보(예: `/etc/cloudservices/proxy/workername`).

>[!NOTE]
>
>다음을 참조하십시오 [InDesign Server 프록시 작업자 구성](indesign.md#configuring-the-proxy-worker-for-indesign-server) 및 [Cloud Service 구성](../sites-developing/extending-cloud-config.md) 추가 정보.

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

다음 [IDS 프록시 작업자](indesign.md) 의 예입니다. [!DNL Assets] InDesign 에셋 처리를 아웃소싱하기 위해 기본 제공되는 프록시 작업자입니다.

또한 나만의 고유한 개발 및 구성을 할 수도 있습니다 [!DNL Assets] 프록시 작업자를 통해 파견 및 아웃소싱을 수행할 전문 작업자를 만들 수 있습니다. [!DNL Assets] 작업 처리 중.

사용자 정의 프록시 작업자를 설정하려면 다음을 수행해야 합니다.

* Sling 이벤트 사용 설정 및 구현:

   * 사용자 정의 작업 항목
   * 사용자 지정 작업 이벤트 핸들러

* 그런 다음 JobService API를 사용하여 다음을 수행합니다.

   * 사용자 정의 작업을 프록시로 디스패치
   * 작업 관리

* 워크플로우에서 프록시를 사용하려면 WorkflowExternalProcess API 및 JobService API를 사용하여 사용자 지정 외부 단계를 구현해야 합니다.

다음 다이어그램과 단계는 진행 방법에 대해 자세히 설명합니다.

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>다음 단계에서는 InDesign 등가물을 참조 예제로 표시합니다.

1. A [Sling 작업](https://sling.apache.org/site/eventing-and-jobs.html) 이 사용되므로 사용 사례에 대한 작업 주제를 정의해야 합니다.

   예를 들어 다음을 참조하십시오. `IDSJob.IDS_EXTENDSCRIPT_JOB` IDS 프록시 작업자.

1. 외부 단계는 이벤트를 트리거한 다음 완료될 때까지 기다리는 데 사용됩니다. 이 작업은 ID에 대한 폴링을 통해 수행됩니다. 새로운 기능을 구현하려면 나만의 단계를 개발해야 합니다.

   구현 `WorkflowExternalProcess`그런 다음 JobService API와 작업 주제를 사용하여 작업 이벤트를 준비하고 JobService(OSGi 서비스)에 발송합니다.

   예를 들어 다음을 참조하십시오. `INDDMediaExtractProcess`.java(IDS 프록시 작업자)

1. 주제에 대한 작업 핸들러를 구현합니다. 이 처리기는 특정 작업을 수행하고 작업자 구현으로 간주되도록 개발이 필요합니다.

   예를 들어 다음을 참조하십시오. `IDSJobProcessor.java` IDS 프록시 작업자.

1. 활용 `ProxyUtil.java` dam-commons에서. DAM 프록시를 사용하여 작업을 작업자에게 발송할 수 있습니다.

>[!NOTE]
>
>무엇입니까? [!DNL Assets] 프록시 프레임워크는 풀 메커니즘을 기본적으로 제공하지 않습니다.
>
>다음 [!DNL InDesign] 통합을 통해 다음 풀의 액세스 허용 [!DNL InDesign] 서버(IDSPool). 이 풀링은 다음과 관련이 있습니다. [!DNL InDesign] 통합(일부 아님) [!DNL Assets] 프록시 프레임워크.

>[!NOTE]
>
>결과 동기화:
>
>동일한 프록시를 사용하는 인스턴스가 n개 있는 경우 처리 결과는 프록시에 유지됩니다. 작업 생성 시 클라이언트에 제공되는 것과 동일한 고유 작업 ID를 사용하여 결과를 요청하는 것은 클라이언트(Experience Manager 작성자)의 작업입니다. 프록시는 단순히 작업을 완료하고 결과를 요청할 준비가 된 상태로 유지합니다.
