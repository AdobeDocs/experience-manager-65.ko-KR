---
title: JEE Workbench의 AEM Forms에서 실행 스크립트 서비스를 사용하여 XML 데이터를 작성하는 방법
description: JEE Workbench의 AEM Forms에서 실행 스크립트 서비스를 사용하여 XML 데이터 작성
exl-id: 2ec57cd4-f41b-4e5c-849d-88ca3d2cfe19
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# JEE Workbench의 AEM Forms에서 실행 스크립트 서비스를 사용하여 XML 데이터 작성 {#using-execute-script-service-forms-jee-workbench}

JEE 프로세스 관리 워크플로우에서 AEM Forms과 관련된 많은 XML이 있습니다. 예를 들면 다음과 같습니다. XML 정보는 프로세스에 빌드되어 JEE Workspace의 AEM Forms에 있는 Flex 애플리케이션으로 전송되거나 시스템 설정에 사용되거나 양식에서 정보를 전달하는 데 사용될 수 있습니다. JEE 개발자의 AEM Forms에서 XML을 관리해야 하는 인스턴스가 많이 있으며, 많은 경우 JEE 프로세스의 AEM Forms을 통해 XML을 관리해야 합니다.

간단한 XML 설정을 처리할 때 `Set Value` 서비스: JEE 서비스의 기본 AEM Forms입니다. 이 서비스는 프로세스 데이터 모델에서 하나 이상의 데이터 항목의 값을 설정합니다. 매우 간단한 조건부 논리 &quot;if this, then that&quot; 시나리오의 경우 이 서비스는 목적에 부합할 수 있습니다.

하지만 더 복잡한 상황에서는 값 설정 서비스가 효과적이지 않습니다. 이러한 경우에는 Java와 같은 프로그래밍 언어로 제공되는 명령 등 보다 강력한 프로그래밍 명령에 의존해야 합니다. Java를 사용하여 복잡한 XML을 작성할 때 Set Value 서비스 내의 단순 텍스트에서 XML 문서를 작성하는 것보다 훨씬 쉽고 명확히 처리할 수 있습니다. 또한 값 설정 서비스 내보다 Java에 조건부 프로그래밍을 포함하기가 더 쉽습니다.

## 프로세스에서 스크립트 서비스 실행 {#using-execute-script-service-in-process}

JEE Workbench의 AEM Forms에서 사용할 수 있는 JEE 서비스의 표준 AEM Forms 세트 내에 이 있습니다. `Execute Script` 서비스. 이 서비스를 사용하면 프로세스에서 스크립트를 실행할 수 있으며 `executeScript` 작업을 수행합니다.

### 활동으로 정의된 &quot;스크립트 실행&quot; 서비스를 사용하여 응용 프로그램 및 프로세스 생성 {#create-an-application}

이 자습서에서는 전체 응용 프로그램 및 프로세스 만들기가 범위를 벗어나지만 이 지침을 위해 &quot;DemoApplication02&quot;라는 응용 프로그램을 만들었습니다. 애플리케이션이 이미 만들어졌다고 가정할 경우 이 애플리케이션에서 executeScript 서비스를 호출하는 프로세스를 만들어야 합니다. 를 포함하는 프로세스를 응용 프로그램에 추가하려면 `Execute Script` 서비스:

1. 애플리케이션을 마우스 오른쪽 버튼으로 클릭하고 을 선택합니다. [!UICONTROL 새로 만들기]. in [!UICONTROL 새로 만들기] 슬라이드 아웃 메뉴에서 [!UICONTROL 프로세스]. 프로세스에 이름을 지정하고 필요한 경우 설명을 추가하고 이 프로세스를 나타낼 아이콘을 선택합니다. 이 자습서를 위해 프로세스를 만들고 이름을 로 지정했습니다.  `executeScriptDemoProcess`.
1. 시작점을 정의하거나, 나중에 시작점을 추가하기 위해 간단한 선택을 합니다.
1. 이제 프로세스가 만들어지는에서 자동으로 열립니다 [!UICONTROL 프로세스 설계] 창을 엽니다. 이 창에서 프로세스 디자인 창 상단의 활동 선택기 아이콘을 클릭하고 새 활동을 수영 레인으로 드래그합니다. 이 시점에서 [!UICONTROL 활동 정의 창] 이 표시됩니다(아래 그림 참조).
   ![활동 정의](assets/define-activity.jpg)
1. executeScript 서비스는 `Foundation` 서비스 집합입니다. Services 이름은 객체를 `Execute Script – 1.0` 작업 이름 사용 `executeScript`. 이 항목을 선택하려면 클릭하십시오.
1. 이제 이 프로세스를 만들어야 하며, 기본적으로 [!UICONTROL 프로세스 속성] 창이 왼쪽 창에 나타납니다.

#### &quot;스크립트 실행&quot; 서비스를 사용하여 프로세스에 스크립트 추가 {#add-script-to-process-with-execute-script}

프로세스가 정의된 &quot;스크립트 실행&quot; 서비스 활동을 사용하여 생성되면 스크립트를 이 프로세스에 추가할 수 있습니다. 이 프로세스에 스크립트를 추가하려면

1. 로 이동합니다 [!UICONTROL 프로세스 속성] 팔레트. 이 팔레트 내에서 [!UICONTROL 입력] 섹션을 클릭하고 &quot;...&quot; 아이콘을 클릭합니다.

1. 나타나는 텍스트 상자에 스크립트를 작성합니다. 스크립트가 작성되면 확인을 누릅니다(아래 그림 참조).
   ![스크립트 실행](assets/execute-script.jpg)

## 스크립트 실행 서비스를 사용하여 XML 생성 {#create-xml-execute-script-service}

포함된 Execute Script 서비스를 사용하여 프로세스를 작성하면 이 스크립트를 사용하여 XML을 만들 수 있습니다. Add a Script to the Process에 스크립트 추가에 설명된 텍스트 상자에 아래 설명된 스크립트를 `Execute Script` 위의 서비스 섹션.

**Execute Script Service 기술 정보**

Execute Script 서비스의 기능 및 제한 사항을 알기 위해서는 서비스의 기술적 이해 내용을 알아야 합니다. AEM Forms on JEE에서는 Apache Xerces Document Object Model(DOM) 구문 분석기를 사용하여 프로세스 내에서 XML 변수를 만들고 저장합니다. Xerces는 W3C의 문서 객체 모델 사양에 대한 Java 구현입니다. 정의 [여기](https://dom.spec.whatwg.org/). DOM 사양은 1998년부터 XML을 조작하는 표준 방법입니다. Xerces-J의 Java 구현은 DOM 레벨 2 버전 1.0을 지원합니다.

XML 변수를 저장하는 데 사용되는 Java 클래스는 다음과 같습니다.

* org.apache.xerces.dom.NodeImpl 및

* org.apache.xerces.dom.DocumentImpl

DocumentImpl은 NodeImpl의 하위 클래스이므로 XML 프로세스 변수가 NodeImpl 파생이라고 할 수 있습니다. NodeImpl에 대한 설명서를 찾을 수 있습니다 [여기](https://xerces.apache.org/xerces-j/apiDocs/org/apache/xerces/dom/NodeImpl.html).

**Execute Script Service를 사용한 샘플 XML 생성**

다음은 실행 스크립트 서비스 내에서 XML을 만드는 예입니다. 프로세스에 XML 유형의 변수, 노드 유형이 있습니다. 이 활동의 최종 결과는 XML 문서가 됩니다. 이 문서의 기능 또는 전체 프로세스에 적용되는 방법은 이 자습서에서 범위를 벗어납니다. 궁극적으로 XML이 전체 응용 프로그램에서 수행해야 하는 작업에 따릅니다. 소개에서 언급했듯이 XML은 JEE 양식 및 프로세스의 AEM Forms에서 많은 용도로 사용할 수 있습니다. 이는 간단한 XML 문서를 출력하도록 스크립트 실행 활동을 코딩하는 방법에 대한 설명입니다.

XML을 출력하는 간단한 Java 스크립트는 다음과 같습니다.

```xml
import org.apache.xerces.dom.DocumentImpl;

import org.w3c.dom.Document;

import org.w3c.dom.Element;



Document document = new DocumentImpl();

Element topLevelResources = document.createElement("resources");

Element resource = document.createElement("resource");

resource.setAttribute("id", "first item id");

resource.setAttribute("value", "first item value");

topLevelResources.appendChild(resource);

document.appendChild(topLevelResources);

patExecContext.setProcessDataValue("/process_data/node", document);
```

>[!NOTE]
>
>앞서 언급한 DOM 개체를 스크립트로 가져와야 합니다.

이 단순 스크립트의 결과는 다음과 같이 설정된 변수 노드가 있는 새 XML 문서입니다.

```xml
<resources>

<resource id="first item id" value="first item value"/>

</resources>
```

**반복적 루프를 사용하여 XML에 노드 추가**

또한 프로세스 내의 기존 XML 변수에 노드를 추가할 수 있습니다. 변수인 노드에는 방금 만든 XML 개체가 포함되어 있습니다.

```xml
Document document = patExecContext.getProcessDataValue("/process_data/node");

NodeList childNodes = document.getChildNodes();

int numChildren = childNodes.getLength();

for (int i = 0; i < numChildren; i++)

{

Node currentChild = childNodes.item(i);

if (currentChild.getNodeType() == Node.ELEMENT_NODE)

{

// found the top level node

Element newResource = document.createElement("resource");

newResource.setAttribute("id", "second item id");

newResource.setAttribute("value", "second item value");

currentChild.appendChild(newResource);

break;

}

}

patExecContext.setProcessDataValue("/process_data/node", document);
The variable node in the XML is now set to:

<resources> 

<resource id="first item id" value="first item value"/> 

<resource id="second item id" value="second item value"/> 

</resources>
```
