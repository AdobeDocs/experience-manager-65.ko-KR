---
title: 서버 측 사용자 지정
seo-title: Server-side Customization
description: AEM Communities에서 서버측 사용자 지정
seo-description: Customizing server-side in AEM Communities
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---

# 서버 측 사용자 지정 {#server-side-customization}

| **[⇐ 기능 핵심 사항](essentials.md)** | **[클라이언트측 사용자 지정 ⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>Communities API의 패키지 위치는 한 주요 릴리스에서 다음 릴리스로 업그레이드할 때 변경될 수 있습니다.

### SocialComponent 인터페이스 {#socialcomponent-interface}

SocialComponents는 AEM Communities 기능에 대한 리소스를 나타내는 POJO입니다. 가장 좋은 방법은 각 SocialComponent가 클라이언트에 데이터를 제공하는 노출된 GETter를 사용하여 특정 resourceType을 나타내므로 리소스가 정확하게 표현됩니다. 필요한 경우 사이트 방문자의 세션 정보를 포함하여 모든 비즈니스 논리 및 보기 로직은 SocialComponent에 캡슐화됩니다.

인터페이스는 리소스를 나타내는 데 필요한 기본 GETters 집합을 정의합니다. 중요한 것은 인터페이스에 맵 이 지정되어 있다는 것입니다&lt;string object=&quot;&quot;> Handlebars 템플릿을 렌더링하고 리소스에 대한 GET JSON 엔드포인트를 노출하는 데 필요한 getAsMap() 및 String toJSONString() 메서드.

모든 SocialComponent 클래스는 인터페이스를 구현해야 합니다 `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent 인터페이스 {#socialcollectioncomponent-interface}

SocialCollectionComponent 인터페이스는 SocialComponent 인터페이스를 확장하여 다른 리소스의 컬렉션인 리소스를 더 잘 나타냅니다.

모든 SocialCollectionComponent 클래스는 com.adobe.cq.social.scf.SocialCollectionComponent 인터페이스를 구현해야 합니다

### SocialComponentFactory 인터페이스 {#socialcomponentfactory-interface}

SocialComponentFactory(factory)는 프레임워크에 SocialComponent를 등록합니다. 팩터리는 여러 SocialComponents가 식별될 때 주어진 resourceType에 사용할 수 있는 SocialComponents와 해당 우선순위 등급을 프레임워크에 알리는 수단을 제공합니다.

SocialComponentFactory는 선택한 SocialComponent의 인스턴스를 만들 책임이 있으므로 ID 방법을 사용하여 팩터리에서 SocialComponent에 필요한 모든 종속성을 삽입할 수 있습니다.

SocialComponentFactory는 OSGi 서비스이며 생성자를 통해 SocialComponent에 전달할 수 있는 다른 OSGi 서비스에 액세스할 수 있습니다.

모든 SocialComponentFactory 클래스는 인터페이스를 구현해야 합니다 `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority() 메서드 구현은 getResourceType()에서 반환한 대로 팩토리를 주어진 resourceType에 사용하려면 가장 높은 값을 반환해야 합니다.

### SocialComponentFactoryManager 인터페이스 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager(manager)는 프레임워크에 등록된 모든 Social 구성 요소를 관리하고 주어진 리소스(resourceType)에 사용할 SocialComponentFactory를 선택해야 합니다. 특정 resourceType에 대해 등록된 공장이 없는 경우 관리자는 해당 자원에 가장 가까운 슈퍼 유형을 가진 공장을 반환합니다.

SocialComponentFactoryManager는 OSGi 서비스이며 생성자를 통해 SocialComponent에 전달할 수 있는 다른 OSGi 서비스에 액세스할 수 있습니다.

OSGi 서비스의 핸들은 `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API - POST 요청 {#http-api-post-requests}

#### 사후 작업 클래스 {#postoperation-class}

HTTP API POST 끝점은 를 구현하여 정의한 PostOperation 클래스입니다 `SlingPostOperation` 인터페이스(패키지 `org.apache.sling.servlets.post`).

다음 `PostOperation` 엔드포인트 구현 세트 `sling.post.operation` 작업이 응답할 값으로 설정됩니다. :operation 매개 변수를 해당 값으로 설정한 모든 POST 요청은 이 구현 클래스에 위임됩니다.

다음 `PostOperation` 는 를 호출합니다 `SocialOperation` 작업에 필요한 작업을 수행합니다.

다음 `PostOperation` 는 `SocialOperation` 및 는 클라이언트에 대한 적절한 응답을 반환합니다.

#### SocialOperation 클래스 {#socialoperation-class}

각 `SocialOperation` endpoint는 AbstractSocialOperation 클래스를 확장하고 메서드를 무시합니다 `performOperation()`. 이 메서드는 작업을 완료하고 를 반환하는 데 필요한 모든 작업을 수행합니다 `SocialOperationResult` 또는 `OperationException`: 사용 가능한 경우 일반 JSON 응답 또는 성공 HTTP 상태 코드 대신 메시지가 포함된 HTTP 오류 상태가 반환됩니다.

확장 `AbstractSocialOperation` 의 재사용 가능 `SocialComponents` JSON 응답을 전송하는 중입니다.

#### SocialOperationResult 클래스 {#socialoperationresult-class}

다음 `SocialOperationResult` 클래스는 `SocialOperation` 및 는 `SocialComponent`, HTTP 상태 코드 및 HTTP 상태 메시지.

다음 `SocialComponent` 작업의 영향을 받는 리소스를 나타냅니다.

만들기 작업의 경우, `SocialComponent` 에 포함됨 `SocialOperationResult` 방금 생성된 리소스를 나타내며 업데이트 작업의 경우 작업에 의해 변경된 리소스를 나타냅니다. 아니요 `SocialComponent` 삭제 작업에 대해 반환됩니다.

사용된 성공 HTTP 상태 코드는 다음과 같습니다.

* 생성 작업에 201
* 업데이트 작업에 200개
* 삭제 작업에 204

#### 작업 예외 클래스 {#operationexception-class}

An `OperationExcepton` 요청이 올바르지 않거나 내부 오류, 잘못된 매개 변수 값, 부적절한 권한 등과 같은 일부 다른 오류가 발생하는 경우 작업을 수행할 때 throw될 수 있습니다. An `OperationException` 는 HTTP 상태 코드와 오류 메시지로 구성되며 이 코드는 HTTP에 대한 응답으로 클라이언트에 반환됩니다 `PostOperatoin`.

#### 작업 서비스 클래스 {#operationservice-class}

소셜 구성 요소 프레임워크에서는 작업을 수행하는 비즈니스 로직을 `SocialOperation` 클래스 이름을 지정합니다. 비즈니스 로직에 OSGi 서비스를 사용하는 것은 `SocialComponent`에 의해 `SocialOperation` 엔드포인트. 다른 코드와 통합되고 서로 다른 비즈니스 로직이 적용되어야 합니다.

모두 `OperationService` 클래스 확장 `AbstractOperationService`를 추가하여 수행 중인 작업에 연결할 수 있는 추가 확장을 허용합니다. 서비스의 각 작업은 `SocialOperation` 클래스 이름을 지정합니다. 다음 `OperationExtensions` 메서드는 호출 시 클래스를 호출할 수 있습니다

* `performBeforeActions()`

   사전 확인/사전 처리 및 유효성 검사 허용
* `performAfterActions()`

   리소스를 추가로 수정하거나 사용자 지정 이벤트, 워크플로우 등을 호출할 수 있습니다

#### 작업 확장 클래스 {#operationextension-class}

`OperationExtension` 클래스는 비즈니스 요구 사항에 맞게 작업을 사용자 지정할 수 있도록 작업에 삽입할 수 있는 사용자 지정 코드 조각입니다. 구성 요소의 소비자는 구성 요소에 기능을 동적으로 그리고 점진적으로 추가할 수 있습니다. 확장/후크 패턴을 사용하면 개발자가 확장 자체에만 집중할 수 있으며 전체 작업 및 구성 요소를 복사하고 재정의할 필요가 없습니다.

## 샘플 코드 {#sample-code}

샘플 코드는 [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) 저장소. 다음 중 하나가 접두사로 추가된 프로젝트를 검색합니다. `aem-communities` 또는 `aem-scf`.

## 모범 사례 {#best-practices}

보기 [코딩 지침](code-guide.md) AEM Communities 개발자를 위한 다양한 코딩 지침 및 우수 사례에 대한 섹션을 참조하십시오.

참조 - [UGC용 SRP(Storage Resource Provider)](srp.md) 사용자가 생성한 컨텐츠에 액세스하는 방법에 대해 알아봅니다.

| **[⇐ 기능 핵심 사항](essentials.md)** | **[클라이언트측 사용자 지정 ⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
