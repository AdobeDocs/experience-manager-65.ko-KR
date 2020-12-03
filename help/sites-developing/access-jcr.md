---
title: 프로그래밍 방식으로 AEM JCR에 액세스하는 방법
seo-title: 프로그래밍 방식으로 AEM JCR에 액세스하는 방법
description: Adobe Marketing Cloud의 일부인 AEM 저장소 내에 있는 노드와 속성을 프로그래밍 방식으로 수정할 수 있습니다
seo-description: Adobe Marketing Cloud의 일부인 AEM 저장소 내에 있는 노드와 속성을 프로그래밍 방식으로 수정할 수 있습니다
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 3%

---


# 프로그래밍 방식으로 AEM JCR에 액세스하는 방법{#how-to-programmatically-access-the-aem-jcr}

Adobe Marketing Cloud의 일부인 Adobe CQ 저장소 내에 있는 노드와 속성을 프로그래밍 방식으로 수정할 수 있습니다. CQ 저장소에 액세스하려면 JCR(Java Content Repository) API를 사용합니다. Java JCR API를 사용하여 Adobe CQ 저장소 내에 있는 컨텐츠에 대한 CRUD(생성, 교체, 업데이트 및 삭제) 작업을 수행할 수 있습니다. Java JCR API에 대한 자세한 내용은 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)을 참조하십시오.

>[!NOTE]
>
>이 개발 아티클은 외부 Java 응용 프로그램에서 Adobe CQ JCR을 수정합니다. 반면 JCR API를 사용하여 OSGi 번들 내에서 JCR을 수정할 수 있습니다. 자세한 내용은 Java 컨텐츠 저장소의 [CQ 데이터 지속](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html)을 참조하십시오.

>[!NOTE]
>
>JCR API를 사용하려면 Java 애플리케이션의 클래스 경로에 `jackrabbit-standalone-2.4.0.jar` 파일을 추가합니다. 이 JAR 파일은 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)의 Java JCR API 웹 페이지에서 가져올 수 있습니다.

>[!NOTE]
>
>JCR 쿼리 API를 사용하여 Adobe CQ JCR을 쿼리하는 방법을 알아보려면 [JCR API](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)를 사용하여 Adobe Experience Manager 데이터 쿼리를 참조하십시오.

## 저장소 인스턴스 {#create-a-repository-instance} 만들기

저장소에 연결하고 연결을 설정하는 방법은 다르지만 이 개발 아티클에서는 `org.apache.jackrabbit.commons.JcrUtils` 클래스에 속하는 정적 메서드를 사용합니다. 메서드 이름은 `getRepository`입니다. 이 메서드는 Adobe CQ 서버의 URL을 나타내는 문자열 매개 변수를 사용합니다. 예 `http://localhost:4503/crx/server`.

`getRepository`메서드는 다음 코드 예제와 같이 `Repository`인스턴스를 반환합니다.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 세션 인스턴스 {#create-a-session-instance} 만들기

`Repository`인스턴스는 CRX 저장소를 나타냅니다. `Repository`인스턴스를 사용하여 보관소와 함께 세션을 설정합니다. 세션을 만들려면 `Repository`인스턴스의 `login` 메서드를 호출하고 `javax.jcr.SimpleCredentials` 개체를 전달합니다. `login`메서드는 `javax.jcr.Session` 인스턴스를 반환합니다.

생성자를 사용하여 `SimpleCredentials`개체를 만들고 다음 문자열 값을 전달합니다.

* 사용자 이름;
* 해당 암호

두 번째 매개 변수를 전달할 때 String 개체의 `toCharArray`메서드를 호출합니다. 다음 코드는 `javax.jcr.Sessioninstance`을 반환하는 `login` 메서드를 호출하는 방법을 보여 줍니다.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 노드 인스턴스 {#create-a-node-instance} 만들기

`Session`인스턴스를 사용하여 `javax.jcr.Node` 인스턴스를 만듭니다. `Node`인스턴스를 사용하면 노드 작업을 수행할 수 있습니다. 예를 들어 새 노드를 만들 수 있습니다. 루트 노드를 나타내는 노드를 만들려면 다음 코드 행에 표시된 대로 `Session`인스턴스의 `getRootNode` 메서드를 호출합니다.

```java
//Create a Node
Node root = session.getRootNode();
```

`Node`인스턴스를 만들면 다른 노드를 만들고 여기에 값을 추가하는 등의 작업을 수행할 수 있습니다. 예를 들어 다음 코드는 두 개의 노드를 만들고 두 번째 노드에 값을 추가합니다.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 노드 값 검색 {#retrieve-node-values}

노드 및 해당 값을 검색하려면 `Node`인스턴스의 `getNode` 메서드를 호출하고 정규화된 경로를 나타내는 문자열 값을 노드에 전달합니다. 이전 코드 예제에서 만들어진 노드 구조를 고려하십시오. 날짜 노드를 검색하려면 다음 코드와 같이 adobe/day를 지정합니다.

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Adobe CQ 저장소의 노드 만들기 {#create-nodes-in-the-adobe-cq-repository}

다음 Java 코드 예는 Adobe CQ에 연결하고, `Session`인스턴스를 만들고, 새 노드를 추가하는 Java 클래스를 나타냅니다. 노드에는 데이터 값이 할당되고, 그 다음에 노드의 값과 경로가 콘솔에 기록됩니다. 세션 작업이 완료되면 반드시 로그아웃하십시오.

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

전체 코드 예를 실행하고 노드를 만든 후 다음 그림과 같이 **[!UICONTROL CRXDE Lite]**&#x200B;에서 새 노드를 볼 수 있습니다.

![chlimage_1-68](assets/chlimage_1-68a.png)

