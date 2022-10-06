---
title: 프로그래밍 방식으로 AEM JCR에 액세스하는 방법
seo-title: How to programmatically access the AEM JCR
description: Adobe Marketing Cloud의 일부인 AEM 리포지토리 내에 있는 노드와 속성을 프로그래밍 방식으로 수정할 수 있습니다
seo-description: You can programmatically modify nodes and properties located within the AEM repository, which is part of the Adobe Marketing Cloud
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# 프로그래밍 방식으로 AEM JCR에 액세스하는 방법{#how-to-programmatically-access-the-aem-jcr}

Adobe Marketing Cloud의 일부인 Adobe CQ 리포지토리 내에 있는 노드와 속성을 프로그래밍 방식으로 수정할 수 있습니다. CQ 리포지토리에 액세스하려면 JCR(Java Content Repository) API를 사용합니다. Java JCR API를 사용하여 Adobe CQ 리포지토리 내에 있는 콘텐츠에 대한 CRUD(만들기, 바꾸기, 업데이트 및 삭제) 작업을 수행할 수 있습니다. Java JCR API에 대한 자세한 내용은 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>이 개발 문서에서는 외부 Java 애플리케이션에서 Adobe CQ JCR을 수정합니다. 반면 JCR API를 사용하여 OSGi 번들 내에서 JCR을 수정할 수 있습니다. 자세한 내용은 [Java Content Repository에서 CQ 데이터 유지](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>JCR API를 사용하려면 을(를) 추가합니다. `jackrabbit-standalone-2.4.0.jar` 파일을 Java 애플리케이션의 클래스 경로에 추가할 수 있습니다. 의 Java JCR API 웹 페이지에서 이 JAR 파일을 가져올 수 있습니다. [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>JCR 쿼리 API를 사용하여 Adobe CQ JCR을 쿼리하는 방법에 대해 알아보려면 [JCR API를 사용하여 Adobe Experience Manager 데이터 쿼리](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## 저장소 인스턴스 만들기 {#create-a-repository-instance}

리포지토리에 연결하고 연결을 설정하는 방법은 다르지만 이 개발 문서에서는 `org.apache.jackrabbit.commons.JcrUtils` 클래스 이름을 지정합니다. 메서드 이름은 `getRepository`. 이 메서드는 Adobe CQ 서버의 URL을 나타내는 문자열 매개 변수를 사용합니다. 예 `http://localhost:4503/crx/server`.

다음 `getRepository`메서드 반환 `Repository`인스턴스. 다음 코드 예에 표시된 것처럼.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 세션 인스턴스 만들기 {#create-a-session-instance}

다음 `Repository`인스턴스는 CRX 저장소를 나타냅니다. 를 사용합니다 `Repository`리포지토리를 사용하여 세션을 설정할 인스턴스. 세션을 만들려면 `Repository`인스턴스 `login`방법 및 전달 `javax.jcr.SimpleCredentials` 개체. 다음 `login`메서드 반환 `javax.jcr.Session` 인스턴스.

을(를) 만듭니다 `SimpleCredentials`생성자를 사용하고 다음 문자열 값을 전달하여 개체를 변환합니다.

* 사용자 이름;
* 해당 암호

두 번째 매개 변수를 전달할 때 String 개체의 `toCharArray`메서드를 사용합니다. 다음 코드는 를 호출하는 방법을 보여 줍니다 `login`를 반환하는 메서드 `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 노드 인스턴스 만들기 {#create-a-node-instance}

다음 작업 `Session`생성할 인스턴스 `javax.jcr.Node` 인스턴스. A `Node`인스턴스를 사용하면 노드 작업을 수행할 수 있습니다. 예를 들어 새 노드를 만들 수 있습니다. 루트 노드를 나타내는 노드를 만들려면 `Session`인스턴스 `getRootNode` 메서드, 다음 코드 행에 표시된 대로 사용할 수 있습니다.

```java
//Create a Node
Node root = session.getRootNode();
```

일단 을(를) 만들면 `Node`예를 들어 다른 노드를 만들고 값을 추가하는 등의 작업을 수행할 수 있습니다. 예를 들어 다음 코드는 두 개의 노드를 만들고 두 번째 노드에 값을 추가합니다.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 노드 값 검색 {#retrieve-node-values}

노드 및 해당 값을 검색하려면 `Node`인스턴스 `getNode`메서드를 사용하여 노드에 정규화된 경로를 나타내는 문자열 값을 전달합니다. 이전 코드 예제에서 만든 노드 구조를 고려하십시오. day 노드를 검색하려면 다음 코드에 표시된 대로 adobe/day를 지정하십시오.

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Adobe CQ 리포지토리에서 노드 만들기 {#create-nodes-in-the-adobe-cq-repository}

다음 Java 코드 예는 Adobe CQ에 연결된 Java 클래스를 나타내며, `Session`인스턴스를 설정하고 새 노드를 추가합니다. 노드에 데이터 값이 할당되고 해당 노드 및 경로가 콘솔에 기록됩니다. 세션 을 마쳤으면 반드시 로그아웃하십시오.

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

전체 코드 예제를 실행하고 노드를 만들면 **[!UICONTROL CRXDE Lite]**&#x200B;다음 그림과 같이,

![chlimage_1-68](assets/chlimage_1-68a.png)
