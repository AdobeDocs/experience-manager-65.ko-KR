---
title: 서버측 사용자 정의
seo-title: 서버측 사용자 정의
description: AEM Communities에서 서버측 사용자 정의
seo-description: AEM Communities에서 서버측 사용자 정의
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# 서버측 사용자 정의 {#server-side-customization}

| **[Feature ⇐ Essentials](essentials.md)** | **[클라이언트측 맞춤화 =](client-customize.md)** |
|---|---|
|  | **[SCF 핸들바 도우미 =](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>Communities API의 패키지 위치는 주요 릴리스에서 다음 릴리스로 업그레이드할 때 변경될 수 있습니다.


### SocialComponent 인터페이스 {#socialcomponent-interface}

SocialComponents는 AEM Communities 기능에 대한 리소스를 나타내는 POJO입니다. 이상적으로 각 SocialComponent는 리소스를 정확하게 표현하도록 클라이언트에 데이터를 제공하는 노출된 GETter를 사용하여 특정 resourceType을 나타냅니다. 필요한 경우 사이트 방문자의 세션 정보를 포함하여 모든 비즈니스 논리 및 보기 로직은 SocialComponent에 캡슐화됩니다.

인터페이스는 리소스를 나타내는 데 필요한 기본 GETter 집합을 정의합니다. 중요한 것은, 인터페이스에 Map&lt;String, Object> getAsMap() 및 String toJSONString() 메서드가 포함되어 있는데, 이는 Handlebars 템플릿을 렌더링하고 리소스에 대한 GET JSON 끝점을 노출하기 위해 필요합니다.

모든 SocialComponent 클래스는 인터페이스를 구현해야 합니다. `com.adobe.cq.social.scf.SocialComponent`

### SocialCollection구성 요소 인터페이스 {#socialcollectioncomponent-interface}

SocialCollectionComponent 인터페이스는 SocialComponent 인터페이스를 확장하여 다른 리소스의 컬렉션인 리소스를 보다 잘 나타냅니다.

모든 SocialCollectionComponent 클래스는 com.adobe.cq.sosocial.scf.SocialCollectionComponent 인터페이스를 구현해야 합니다

### SocialComponentFactory 인터페이스 {#socialcomponentfactory-interface}

SocialComponentFactory(공장)는 프레임워크에 SocialComponent를 등록합니다. 이 팩터리는 프레임워크에서 주어진 resourceType에 사용할 수 있는 SocialComponents와 여러 SocialComponents가 식별될 때 해당 우선 순위 등급을 알 수 있도록 하는 수단을 제공합니다.

SocialComponentFactory는 선택한 SocialComponent의 인스턴스를 만들 책임이 있으므로 DI 방법을 사용하여 팩터리에서 SocialComponent에 필요한 모든 종속성을 삽입할 수 있습니다.

SocialComponentFactory는 OSGi 서비스이며 생성자를 통해 SocialComponent로 전달할 수 있는 다른 OSGi 서비스에 액세스할 수 있습니다.

모든 SocialComponentFactory 클래스는 인터페이스를 구현해야 합니다. `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority() 메서드의 구현은 getResourceType()이 반환한 대로 팩터리가 지정된 resourceType에 사용되도록 하려면 가장 높은 값을 반환해야 합니다.

### SocialComponentFactoryManager 인터페이스 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager(관리자)는 프레임워크에 등록된 모든 SocialComponents를 관리하고 주어진 리소스(resourceType)에 사용할 SocialComponentFactory를 선택할 책임이 있습니다. 특정 resourceType에 대해 등록된 공장이 없는 경우 관리자는 해당 리소스에 대해 가장 가까운 슈퍼 유형을 가진 공장을 반환합니다.

SocialComponentFactoryManager는 OSGi 서비스이며 생성자를 통해 SocialComponent로 전달할 수 있는 다른 OSGi 서비스에 액세스할 수 있습니다.

OSGi 서비스의 핸들은 `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API - POST 요청 {#http-api-post-requests}

#### PostOperation 클래스 {#postoperation-class}

HTTP API POST 끝점은 `SlingPostOperation` 인터페이스(패키지 `org.apache.sling.servlets.post`)를 구현하여 정의된 PostOperation 클래스입니다.

끝 `PostOperation` 구현은 `sling.post.operation` 작업이 응답할 값으로 설정됩니다. :operation 매개 변수가 해당 값으로 설정된 모든 POST 요청은 이 구현 클래스에 위임됩니다.

는 `PostOperation` 작업에 필요한 작업을 수행하는 `SocialOperation` 작업을 호출합니다.

는 `PostOperation` Client로부터 결과를 `SocialOperation` 수신하고 적절한 응답을 클라이언트에 반환합니다.

#### SocialOperation 클래스 {#socialoperation-class}

각 `SocialOperation` 끝점은 AbstractSocialOperation 클래스를 확장하고 메서드를 `performOperation()`무시합니다. 이 메서드는 작업을 완료하고, `SocialOperationResult` 또는 다른 실행에서 실행하는 데 필요한 모든 작업을 수행합니다. `OperationException`이 경우 메시지가 있는 HTTP 오류 상태가 일반적인 JSON 응답 또는 성공 HTTP 상태 코드 대신 반환됩니다.

확장을 `AbstractSocialOperation` 통해 JSON 응답을 전송할 `SocialComponents` 수 있습니다.

#### SocialOperationResult 클래스 {#socialoperationresult-class}

이 `SocialOperationResult` 클래스는 `SocialOperation` `SocialComponent`의 결과로 반환되며, HTTP 상태 코드 및 HTTP 상태 메시지로 구성됩니다.

작업의 영향을 받은 리소스를 `SocialComponent` 나타냅니다.

생성 작업의 경우, 에 `SocialComponent` 포함된 자원은 방금 생성된 자원을 `SocialOperationResult` 나타내며 갱신 작업의 경우 공정에 의해 변경된 자원을 나타냅니다. 삭제 작업에 대해 반환되지 `SocialComponent` 않습니다.

사용된 성공 HTTP 상태 코드는 다음과 같습니다.

* 제작 작업을 위한 201
* 업데이트 작업 200
* 삭제 작업에 204

#### OperationException 클래스 {#operationexception-class}

요청이 유효하지 않거나 내부 오류, 잘못된 매개 변수 값, 부적절한 권한 등과 같은 일부 다른 오류가 발생하는 경우 작업을 수행할 때 An `OperationExcepton` 을 실행할 수 있습니다. HTTP 상태 코드와 오류 메시지로 `OperationException` 구성되며 이 메시지는 클라이언트에 대한 응답으로 반환됩니다 `PostOperatoin`.

#### OperationService 클래스 {#operationservice-class}

소셜 구성 요소 프레임워크에서는 작업을 수행하는 비즈니스 논리를 `SocialOperation` 클래스 내에서 구현하지 말고 대신 OSGi 서비스에 위임하는 것이 좋습니다. 비즈니스 로직용 OSGi 서비스를 사용하면 종단점에 의해 `SocialComponent`작동되는 `SocialOperation` 종단점에 의해 다른 코드와 통합되고 다른 비즈니스 로직을 적용할 수 있습니다.

모든 `OperationService` `AbstractOperationService`클래스가 확장되어 수행되는 작업에 연결할 수 있는 추가 확장이 가능합니다. 서비스의 각 작업은 `SocialOperation` 클래스로 표시됩니다. 이 `OperationExtensions` 클래스는 작업 실행 중에 메서드를 호출하여 호출할 수 있습니다

* `performBeforeActions()`

   사전 검사/사전 처리 및 유효성 검사 허용
* `performAfterActions()`

   리소스를 추가로 수정하거나 사용자 지정 이벤트, 워크플로우 등을 호출할 수 있습니다.

#### OperationExtension 클래스 {#operationextension-class}

`OperationExtension` 클래스는 비즈니스 요구 사항에 맞게 작업을 사용자 정의할 수 있도록 작업에 삽입될 수 있는 사용자 정의 코드 조각입니다. 구성 요소의 소비자는 구성 요소에 기능을 동적으로 그리고 점진적으로 추가할 수 있습니다. 익스텐션/후크 패턴을 사용하면 개발자는 익스텐션 자체에만 집중할 수 있고 전체 작업 및 구성 요소를 복사하고 재정의할 필요가 없습니다.

## 샘플 코드 {#sample-code}

샘플 코드는 Adobe Marketing Cloud GitHub [저장소에서 사용할 수](https://github.com/Adobe-Marketing-Cloud) 있습니다. 또는 `aem-communities` 으로 접두사가 붙은 프로젝트를 검색할 수 `aem-scf`있습니다.

## 우수 사례 {#best-practices}

AEM [Communities](code-guide.md) 개발자를 위한 다양한 코딩 지침 및 모범 사례에 대한 코딩 지침 섹션을 참조하십시오.

UGC [용 SRP(Storage Resource Provider](srp.md) )에서 사용자 생성 컨텐츠에 액세스하는 방법에 대한 자세한 내용을 참조하십시오.

| **[Feature ⇐ Essentials](essentials.md)** | **[클라이언트측 맞춤화 =](client-customize.md)** |
|---|---|
|  | **[SCF 핸들바 도우미 =](handlebars-helpers.md)** |

