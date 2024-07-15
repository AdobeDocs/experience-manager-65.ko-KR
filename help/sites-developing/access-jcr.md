---
title: 프로그래밍 방식으로 AEM JCR에 액세스하는 방법
description: Adobe Experience Cloud의 일부인 AEM 저장소 내에 있는 노드 및 속성을 프로그래밍 방식으로 수정할 수 있습니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 프로그래밍 방식으로 AEM JCR에 액세스하는 방법{#how-to-programmatically-access-the-aem-jcr}

Adobe Experience Cloud의 일부인 Adobe CQ 저장소 내에 있는 노드 및 속성을 프로그래밍 방식으로 수정할 수 있습니다. CQ 저장소에 액세스하려면 Java™ Content Repository(JCR) API를 사용합니다. Java™ JCR API를 사용하여 Adobe CQ 저장소 내에 있는 (CRUD) 콘텐츠를 생성, 교체, 업데이트 및 삭제할 수 있습니다. Java™ JCR API에 대한 자세한 내용은 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)을(를) 참조하십시오.

>[!NOTE]
>
>이 개발 문서는 외부 Java™ 애플리케이션에서 Adobe CQ JCR을 수정합니다. 반대로 JCR API를 사용하여 OSGi 번들 내에서 JCR을 수정할 수 있습니다. 자세한 내용은 [Java™ 콘텐츠 저장소에서 CQ 데이터 유지](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html)를 참조하십시오.

>[!NOTE]
>
>JCR API를 사용하려면 `jackrabbit-standalone-2.4.0.jar` 파일을 Java™ 응용 프로그램의 클래스 경로에 추가하십시오. 이 JAR 파일은 Java™ JCR API 웹 페이지 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)에서 가져올 수 있습니다.

>[!NOTE]
>
>JCR 쿼리 API를 사용하여 Adobe CQ JCR을 쿼리하는 방법은 [JCR API를 사용하여 Adobe Experience Manager 데이터 쿼리](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)를 참조하십시오.

## 저장소 인스턴스 만들기 {#create-a-repository-instance}

저장소에 연결하고 연결을 설정하는 방법은 서로 다르지만 이 개발 문서에서는 `org.apache.jackrabbit.commons.JcrUtils` 클래스에 속하는 정적 메서드를 사용합니다. 메서드 이름은 `getRepository`입니다. 이 메서드는 Adobe CQ 서버의 URL을 나타내는 문자열 매개 변수를 사용합니다. 예: `http://localhost:4503/crx/server`

`getRepository` 메서드는 다음 코드 예제와 같이 `Repository` 인스턴스를 반환합니다.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 세션 인스턴스 만들기 {#create-a-session-instance}

`Repository` 인스턴스는 CRX 저장소를 나타냅니다. `Repository` 인스턴스를 사용하여 리포지토리에 세션을 설정합니다. 세션을 만들려면 `Repository` 인스턴스의 `login` 메서드를 호출하고 `javax.jcr.SimpleCredentials` 개체를 전달하십시오. `login` 메서드가 `javax.jcr.Session` 인스턴스를 반환합니다.

생성자를 사용하고 다음 문자열 값을 전달하여 `SimpleCredentials` 개체를 만듭니다.

* 사용자 이름;
* 해당 암호

두 번째 매개 변수를 전달할 때 String 개체의 `toCharArray` 메서드를 호출합니다. 다음 코드에서는 `javax.jcr.Sessioninstance`을(를) 반환하는 `login` 메서드를 호출하는 방법을 보여 줍니다.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 노드 인스턴스 만들기 {#create-a-node-instance}

`Session` 인스턴스를 사용하여 `javax.jcr.Node` 인스턴스를 만듭니다. `Node` 인스턴스를 사용하여 노드 작업을 수행할 수 있습니다. 예를 들어 노드를 만들 수 있습니다. 루트 노드를 나타내는 노드를 만들려면 다음 코드 행에 표시된 대로 `Session` 인스턴스의 `getRootNode` 메서드를 호출합니다.

```java
//Create a Node
Node root = session.getRootNode();
```

`Node` 인스턴스를 만들면 다른 노드를 만들고 값을 추가하는 등의 작업을 수행할 수 있습니다. 예를 들어 다음 코드는 두 개의 노드를 만들고 두 번째 노드에 값을 추가합니다.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 노드 값 검색 {#retrieve-node-values}

노드 및 해당 값을 검색하려면 `Node` 인스턴스의 `getNode` 메서드를 호출하고 정규화된 경로를 나타내는 문자열 값을 노드에 전달하십시오. 이전 코드 예제에서 만든 노드 구조를 생각해 보십시오. 일 노드를 검색하려면 다음 코드와 같이 adobe/day를 지정합니다.

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Adobe CQ 저장소에 노드 만들기 {#create-nodes-in-the-adobe-cq-repository}

다음 Java™ 코드 예제는 Adobe CQ에 연결하고 `Session` 인스턴스를 만들고 새 노드를 추가하는 Java™ 클래스를 나타냅니다. 노드에 데이터 값이 할당되면 노드 및 해당 경로의 값이 콘솔에 기록됩니다. 세션이 완료되면 로그아웃해야 합니다.

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

전체 코드 예제를 실행하고 노드를 만들면 다음 그림과 같이 **[!UICONTROL CRXDE Lite]**&#x200B;에서 새 노드를 볼 수 있습니다.

![chlimage_1-68](assets/chlimage_1-68a.png)
