---
title: 서버측 사용자 지정
description: Adobe Experience Manager Communities에서 서버측 사용자 지정을 사용하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# 서버측 사용자 지정 {#server-side-customization}

| **[⇐ 기능 기본 사항](essentials.md)** | **[클라이언트측 사용자 지정 ⇒](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars 도우미 ⇒](handlebars-helpers.md)** |

## Java™ API {#java-apis}

>[!NOTE]
>
>Communities API의 패키지 위치는 한 주요 릴리스에서 다음 릴리스로 업그레이드할 때 변경될 수 있습니다.

### SocialComponent 인터페이스 {#socialcomponent-interface}

SocialComponents는 AEM Communities 기능에 대한 리소스를 나타내는 POJO입니다. 이상적으로 각 SocialComponent는 리소스에 정확하게 표현되도록 클라이언트에 데이터를 제공하는 노출된 GETter가 있는 특정 resourceType을 나타냅니다. 모든 비즈니스 및 보기 논리는 필요한 경우 사이트 방문자의 세션 정보를 포함하여 SocialComponent에 캡슐화됩니다.

인터페이스는 리소스를 나타내는 데 필요한 기본 GETter 집합을 정의합니다. 중요한 점은 인터페이스가 Handlebars 템플릿을 렌더링하고 리소스에 대한 GET JSON 끝점을 표시하는 데 필요한 Map&lt;String, Object> getAsMap() 및 String toJSONString() 메서드를 규정하고 있다는 것입니다.

모든 SocialComponent 클래스는 `com.adobe.cq.social.scf.SocialComponent` 인터페이스를 구현해야 합니다.

### SocialCollectionComponent 인터페이스 {#socialcollectioncomponent-interface}

SocialCollectionComponent 인터페이스는 SocialComponent 인터페이스를 확장하여 다른 리소스의 컬렉션인 리소스를 더 잘 나타냅니다.

모든 SocialCollectionComponent 클래스는 com.adobe.cq.social.scf.SocialCollectionComponent 인터페이스를 구현해야 합니다

### SocialComponentFactory 인터페이스 {#socialcomponentfactory-interface}

SocialComponentFactory(공장)는 프레임워크에 SocialComponent를 등록합니다. 팩토리는 여러 SocialComponents가 식별될 때 특정 resourceType에 사용할 수 있는 SocialComponents와 해당 우선 순위 순위를 프레임워크에 알려주는 수단을 제공합니다.

SocialComponentFactory는 DI 사례를 사용하여 팩토리에서 SocialComponent에 필요한 모든 종속성을 주입할 수 있도록 선택한 SocialComponent의 인스턴스를 만들 책임이 있습니다.

SocialComponentFactory는 OSGi 서비스이며 생성자를 통해 SocialComponent에 전달할 수 있는 다른 OSGi 서비스에 액세스할 수 있습니다.

모든 SocialComponentFactory 클래스는 `com.adobe.cq.social.scf.SocialComponentFactory` 인터페이스를 구현해야 합니다.

SocialComponentFactory.getPriority() 메서드를 구현하면 getResourceType()에서 반환된 것처럼 지정된 resourceType에 사용할 팩토리에 대해 가장 높은 값이 반환됩니다.

### SocialComponentFactoryManager 인터페이스 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager(관리자)는 프레임워크에 등록된 모든 SocialComponents를 관리하며 지정된 리소스(resourceType)에 사용할 SocialComponentFactory를 선택합니다. 특정 resourceType에 등록된 공장이 없으면 관리자는 지정된 리소스에 가장 가까운 수퍼 유형이 있는 공장을 반환합니다.

SocialComponentFactoryManager는 OSGi 서비스이며 생성자를 통해 SocialComponent에 전달할 수 있는 다른 OSGi 서비스에 액세스할 수 있습니다.

`com.adobe.cq.social.scf.SocialComponentFactoryManager`을(를) 호출하여 OSGi 서비스에 대한 핸들을 가져옵니다.

### HTTP API - POST 요청 {#http-api-post-requests}

#### PostOperation 클래스 {#postoperation-class}

HTTP API POST 끝점은 `SlingPostOperation` 인터페이스(패키지 `org.apache.sling.servlets.post`)를 구현하여 정의된 PostOperation 클래스입니다.

`PostOperation` 끝점 구현은 `sling.post.operation`을(를) 작업이 응답하는 값으로 설정합니다. 해당 값으로 설정된 an:operation 매개 변수를 사용하는 모든 POST 요청은 이 구현 클래스로 위임됩니다.

`PostOperation`은(는) 작업에 필요한 작업을 수행하는 `SocialOperation`을(를) 호출합니다.

`PostOperation`이(가) `SocialOperation`에서 결과를 받고 클라이언트에 적절한 응답을 반환합니다.

#### SocialOperation 클래스 {#socialoperation-class}

각 `SocialOperation` 끝점은 AbstractSocialOperation 클래스를 확장하고 `performOperation()` 메서드를 재정의합니다. 이 메서드는 작업을 완료하고 `SocialOperationResult`을(를) 반환하거나 `OperationException`을(를) throw하는 데 필요한 모든 작업을 수행합니다. 이러한 경우, 사용 가능한 경우 일반적인 JSON 응답 또는 성공 HTTP 상태 코드 대신 메시지와 함께 HTTP 오류 상태가 반환됩니다.

`AbstractSocialOperation`을(를) 확장하면 `SocialComponents`을(를) 재사용하여 JSON 응답을 보낼 수 있습니다.

#### SocialOperationResult 클래스 {#socialoperationresult-class}

`SocialOperationResult` 클래스는 `SocialOperation`의 결과로 반환되며 `SocialComponent`, HTTP 상태 코드 및 HTTP 상태 메시지로 구성됩니다.

`SocialComponent`은(는) 작업의 영향을 받은 리소스를 나타냅니다.

만들기 작업의 경우 `SocialOperationResult`에 포함된 `SocialComponent`은(는) 만들어진 리소스를 나타내며 업데이트 작업의 경우 작업에 의해 변경된 리소스를 나타냅니다. 삭제 작업에 대해 `SocialComponent`이(가) 반환되지 않습니다.

사용되는 성공 HTTP 상태 코드는 다음과 같습니다.

* 만들기 작업용 201
* 업데이트 작업용 200
* 삭제 작업용 204

#### OperationException 클래스 {#operationexception-class}

요청이 잘못되었거나 다른 오류가 발생하면 작업을 수행할 때 `OperationExcepton`이(가) throw됩니다. 예를 들어, 내부 오류, 잘못된 매개 변수 값 또는 부적절한 권한이 있습니다. `OperationException`은(는) HTTP 상태 코드와 오류 메시지로 구성되며, 이 오류 메시지는 `PostOperatoin`에 대한 응답으로 클라이언트에 반환됩니다.

#### OperationService 클래스 {#operationservice-class}

소셜 구성 요소 프레임워크에서는 작업을 수행하는 비즈니스 논리를 `SocialOperation` 클래스 내에서 구현하지 않고 대신 OSGi 서비스로 위임하도록 권장합니다. 비즈니스 논리에 OSGi 서비스를 사용하면 `SocialOperation` 끝점에서 작동하는 `SocialComponent`을(를) 다른 코드와 통합하고 다른 비즈니스 논리를 적용할 수 있습니다.

모든 `OperationService` 클래스는 `AbstractOperationService`을(를) 확장하여 수행 중인 작업에 연결할 수 있는 추가 확장을 허용합니다. 서비스의 각 작업은 `SocialOperation` 클래스로 표시됩니다. 메서드를 호출하여 작업을 실행하는 동안 `OperationExtensions` 클래스를 호출할 수 있습니다.

* `performBeforeActions()`

  사전 확인/사전 처리 및 유효성 검사 허용
* `performAfterActions()`

  리소스를 추가로 편집하거나 사용자 지정 이벤트, 워크플로 등을 호출할 수 있습니다.

#### OperationExtension 클래스 {#operationextension-class}

`OperationExtension` 클래스는 비즈니스 요구 사항에 맞는 작업을 사용자 지정할 수 있도록 하는 작업에 삽입할 수 있는 사용자 지정 코드 조각입니다. 구성 요소의 소비자는 구성 요소에 기능을 동적으로 점증적으로 추가할 수 있습니다. 확장/후크 패턴을 통해 개발자는 확장 자체에만 집중할 수 있으며 전체 작업 및 구성 요소를 복사하고 오버라이드할 필요가 없습니다.

## 샘플 코드 {#sample-code}

샘플 코드는 [Adobe Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) 리포지토리에서 사용할 수 있습니다. `aem-communities` 또는 `aem-scf` 접두사가 있는 프로젝트를 검색합니다.

## 모범 사례 {#best-practices}

AEM Communities 개발자를 위한 다양한 코딩 지침 및 모범 사례를 보려면 [코딩 지침](code-guide.md) 섹션을 참조하십시오.

사용자 생성 콘텐츠에 액세스하는 방법에 대한 자세한 내용은 [UGC용 SRP(저장소 리소스 공급자)](srp.md)도 참조하세요.

| **[⇐ 기능 기본 사항](essentials.md)** | **[클라이언트측 사용자 지정 ⇒](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars 도우미 ⇒](handlebars-helpers.md)** |
