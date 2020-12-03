---
title: 오프로드용 작업 만들기 및 소비
seo-title: 오프로드용 작업 만들기 및 소비
description: Apache Sling Discovery 기능은 JobManager 작업 및 이를 사용하는 JobConsumer 서비스를 생성할 수 있도록 해주는 Java API를 제공합니다
seo-description: Apache Sling Discovery 기능은 JobManager 작업 및 이를 사용하는 JobConsumer 서비스를 생성할 수 있도록 해주는 Java API를 제공합니다
uuid: d6a5beb0-0618-4b61-9b52-570862eac920
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: e7b6b9ee-d807-4eb0-8e96-75ca1e66a4e4
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 4%

---


# 오프로드용 작업 만들기 및 소비{#creating-and-consuming-jobs-for-offloading}

Apache Sling Discovery 기능은 JobManager 작업 및 이를 사용하는 JobConsumer 서비스를 만들 수 있도록 해주는 Java API를 제공합니다.

오프로드 토폴로지 만들기 및 주제 사용 구성에 대한 자세한 내용은 [작업 오프로딩](/help/sites-deploying/offloading.md)을 참조하십시오.

## 작업 페이로드 처리 {#handling-job-payloads}

오프로드 프레임워크는 작업 페이로드를 식별하는 데 사용하는 두 개의 작업 속성을 정의합니다. 오프로드 복제 에이전트는 다음 속성을 사용하여 토폴로지의 인스턴스에 복제할 리소스를 식별합니다.

* `offloading.job.input.payload`:쉼표로 구분된 컨텐츠 경로 목록입니다. 컨텐츠는 작업을 실행하는 인스턴스에 복제됩니다.
* `offloading.job.output.payload`:쉼표로 구분된 컨텐츠 경로 목록입니다. 작업 실행이 완료되면 작업을 생성한 인스턴스의 이러한 경로에 작업 페이로드가 복제됩니다.

속성 이름을 참조하려면 `OffloadingJobProperties` 열거형을 사용하십시오.

* `OffloadingJobProperties.INPUT_PAYLOAD.propertyName()`
* `OffloadingJobProperties.OUTPUT_PAYLOAD.propetyName()`

작업은 페이로드를 필요로 하지 않습니다. 그러나 작업에 리소스를 조작해야 하고 작업이 작업을 만들지 않은 컴퓨터에 오프로드된 경우 페이로드가 필요합니다.

## {#creating-jobs-for-offloading} 오프로드용 작업 만들기

자동으로 선택된 JobConsumer가 실행하는 작업을 만들기 위해 JobManager.addJob 메서드를 호출하는 클라이언트를 만듭니다. 작업을 만들려면 다음 정보를 입력합니다.

* 주제:작업 주제입니다.
* 이름:(선택 사항)
* 속성 맵:입력 페이로드 경로 및 출력 페이로드 경로와 같은 많은 속성을 포함하는 `Map<String, Object>` 개체 이 맵 개체는 작업을 실행하는 JobConsumer 개체에서 사용할 수 있습니다.

다음 예제 서비스는 주어진 주제 및 입력 페이로드 경로에 대한 작업을 만듭니다.

```java
package com.adobe.example.offloading;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;

import java.util.HashMap;

import org.apache.sling.event.jobs.Job;
import org.apache.sling.event.jobs.JobManager;

import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.ResourceResolver;

import com.adobe.granite.offloading.api.OffloadingJobProperties;

@Component
@Service
public class JobGeneratorImpl implements JobGenerator  {

 @Reference
 private JobManager jobManager;
 @Reference ResourceResolverFactory resolverFactory;

 public String createJob(String topic, String payload) throws Exception {
  Job offloadingJob;

  ResourceResolver resolver = resolverFactory.getResourceResolver(null);
  if(resolver.getResource(payload)!=null){

   HashMap<String, Object> jobprops = new HashMap<String, Object>();
   jobprops.put(OffloadingJobProperties.INPUT_PAYLOAD.propertyName(), payload);

   offloadingJob = jobManager.addJob(topic, null, jobprops);
  } else {
   throw new Exception("Payload for job cannot be found");
  }
  if (offloadingJob == null){
   throw new Exception ("Offloading job could not be created");
  }
  return offloadingJob.getId();
 }
}
```

`com/adobe/example/offloading` 주제와 `/content/geometrixx/de/services` 페이로드에 대해 JobGeneratorImpl.createJob이 호출될 때 로그에 다음 메시지가 포함됩니다.

```shell
10.06.2013 15:43:33.868 *INFO* [JobHandler: /etc/workflow/instances/2013-06-10/model_1554418768647484:/content/geometrixx/en/company] com.adobe.example.offloading.JobGeneratorImpl Received request to make job for topic com/adobe/example/offloading and payload /content/geometrixx/de/services
```

## 작업 소비자 개발 {#developing-a-job-consumer}

작업을 소비하려면 `org.apache.sling.event.jobs.consumer.JobConsumer` 인터페이스를 구현하는 OSGi 서비스를 개발하십시오. `JobConsumer.PROPERTY_TOPICS` 속성을 사용하여 소비할 주제와 함께 식별합니다.

다음 예인 JobConsumer 구현이 `com/adobe/example/offloading` 항목에 등록합니다. 소비자는 페이로드 컨텐츠 노드의 소비됨 속성을 true로 설정하기만 하면 됩니다.

```java
package com.adobe.example.offloading;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.event.jobs.Job;
import org.apache.sling.event.jobs.JobManager;
import org.apache.sling.event.jobs.consumer.JobConsumer;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Session;
import javax.jcr.Node;

import com.adobe.granite.offloading.api.OffloadingJobProperties;

@Component
@Service
public class MyJobConsumer implements JobConsumer {

 public static final String TOPIC = "com/adobe/example/offloading";

 @Property(value = TOPIC)
 static final String myTopic = JobConsumer.PROPERTY_TOPICS;

 @Reference
 private ResourceResolverFactory resolverFactory;

 @Reference
 private JobManager jobManager;

 private final Logger log = LoggerFactory.getLogger(getClass());

 public JobResult process(Job job) {
  JobResult result = JobResult.FAILED;
  String topic = job.getTopic();
  log.info("Consuming job of topic: {}", topic);
  String payloadIn =  (String) job.getProperty(OffloadingJobProperties.INPUT_PAYLOAD.propertyName());
  String payloadOut =  (String) job.getProperty(OffloadingJobProperties.OUTPUT_PAYLOAD.propertyName());

  log.info("Job has Input Payload {} and Output Payload {}",payloadIn, payloadOut);

  ResourceResolver resolver = null;
  try {
   resolver = resolverFactory.getAdministrativeResourceResolver(null);
   Session session = resolver.adaptTo(Session.class);
   Node inNode = session.getNode(payloadIn);
   inNode.getNode(Node.JCR_CONTENT).setProperty("consumed",true);
   result = JobResult.OK;
  }catch (Exception e){
   log.info("ERROR -- JOB RESULT IS FAILURE " + e.getMessage());
   result = JobResult.FAILED;
  }
  log.info("Job OK for payload {}",payloadIn);
  return result;
 }
}
```

MyJobConsumer 클래스는 /content/geometrixx/de/services의 입력 페이로드에 대해 다음 로그 메시지를 생성합니다.

```shell
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Consuming job of topic: com/adobe/example/offloading
10.06.2013 16:02:40.803 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job has Input Payload /content/geometrixx/de/services and Output Payload /content/geometrixx/de/services
10.06.2013 16:02:40.884 *INFO* [pool-7-thread-17-<main queue>(com/adobe/example/offloading)] com.adobe.example.offloading.MyJobConsumer Job OK for payload /content/geometrixx/de/services
```

Used 속성은 CRXDE Lite을 사용하여 확인할 수 있습니다.

![chlimage_1-25](assets/chlimage_1-25a.png)

## Maven 종속성 {#maven-dependencies}

Maven이 Offloading 관련 클래스를 해결할 수 있도록 pom.xml 파일에 다음 종속성 보호를 추가합니다.

```xml
<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.event</artifactId>
   <version>3.1.5-R1485539</version>
   <scope>provided</scope>
</dependency>
<dependency>
   <groupId>com.adobe.granite</groupId>
   <artifactId>com.adobe.granite.offloading.core</artifactId>
   <version>1.0.4</version>
   <scope>provided</scope>
</dependency>
```

이전 예제는 다음 종속성 정의도 필요했습니다.

```xml
<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.api</artifactId>
   <version>2.4.3-R1488084</version>
   <scope>provided</scope>
</dependency>

<dependency>
   <groupId>org.apache.sling</groupId>
   <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
   <version>2.0.0</version>
   <scope>provided</scope>
</dependency>
```

