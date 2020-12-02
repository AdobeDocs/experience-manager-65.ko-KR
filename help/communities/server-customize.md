---
title: 서버측 사용자 정의
seo-title: 서버측 사용자 정의
description: AEM Communities의 서버측 사용자 정의
seo-description: AEM Communities의 서버측 사용자 정의
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---


# 서버측 사용자 지정 {#server-side-customization}

| **[Feature ⇐ Essentials](essentials.md)** | **[클라이언트 측 맞춤화 =](client-customize.md)** |
|---|---|
|  | **[SCF 핸들바르를 돕는 사람 =](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>Communities API의 패키지 위치는 한 주요 릴리스에서 다음 릴리스로 업그레이드할 때 변경될 수 있습니다.

### SocialComponent 인터페이스 {#socialcomponent-interface}

소셜 구성 요소는 AEM Communities 기능에 대한 리소스를 나타내는 POJO입니다. 가장 좋은 방법은 각 SocialComponent가 클라이언트에 데이터를 제공하여 리소스가 정확하게 표현되도록 노출된 GETter가 있는 특정 resourceType을 나타냅니다. 필요한 경우 사이트 방문자의 세션 정보를 포함하여 모든 비즈니스 논리 및 보기 로직은 SocialComponent에 캡슐화됩니다.

인터페이스는 리소스를 나타내는 데 필요한 기본 GETters 집합을 정의합니다. 중요한 것은 인터페이스에 Handlebars 템플릿을 렌더링하고 리소스에 대한 GET JSON 끝점을 노출하기 위해 필요한 Map&lt;String, Object> getAsMap() 및 String toJSONString() 메서드가 포함되어 있다는 것입니다.

모든 SocialComponent 클래스는 인터페이스 `com.adobe.cq.social.scf.SocialComponent`을(를) 구현해야 합니다.

### SocialCollectionComponent 인터페이스 {#socialcollectioncomponent-interface}

SocialCollectionComponent 인터페이스는 SocialComponent 인터페이스를 확장하여 다른 리소스의 컬렉션인 리소스를 보다 잘 나타냅니다.

모든 SocialCollectionComponent 클래스는 com.adobe.cq.sosocial.scf.SocialCollectionComponent 인터페이스를 구현해야 합니다

### SocialComponentFactory 인터페이스 {#socialcomponentfactory-interface}

SocialComponentFactory(공장)는 프레임워크에 SocialComponent를 등록합니다. 팩터리는 프레임워크에서 주어진 resourceType에 사용할 수 있는 SocialComponents와 여러 SocialComponents가 식별될 때 해당 우선 순위 등급을 알 수 있도록 하는 수단을 제공합니다.

SocialComponentFactory는 선택한 SocialComponent의 인스턴스를 만드는 작업을 수행하므로 DI 방법을 사용하여 팩터리에서 SocialComponent에 필요한 모든 종속성을 삽입할 수 있습니다.

SocialComponentFactory는 OSGi 서비스이며 생성자를 통해 SocialComponent에 전달할 수 있는 다른 OSGi 서비스에 액세스할 수 있습니다.

모든 SocialComponentFactory 클래스는 인터페이스 `com.adobe.cq.social.scf.SocialComponentFactory`을 구현해야 합니다.

SocialComponentFactory.getPriority() 메서드 구현은 getResourceType()에서 반환되는 대로 팩터리가 지정된 resourceType에 사용되도록 하려면 가장 높은 값을 반환해야 합니다.

### SocialComponentFactoryManager 인터페이스 {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager(관리자)는 프레임워크에 등록된 모든 SocialComponents를 관리하고 주어진 리소스(resourceType)에 사용할 SocialComponentFactory를 선택해야 합니다. 특정 resourceType에 대해 등록된 공고가 없는 경우 관리자는 해당 리소스에 대해 가장 가까운 슈퍼 유형을 가진 공장을 반환합니다.

SocialComponentFactoryManager는 OSGi 서비스이며 생성자를 통해 SocialComponent에 전달할 수 있는 다른 OSGi 서비스에 액세스할 수 있습니다.

`com.adobe.cq.social.scf.SocialComponentFactoryManager`을 호출하여 OSGi 서비스의 핸들을 가져옵니다.

### HTTP API - POST 요청 {#http-api-post-requests}

#### PostOperation 클래스 {#postoperation-class}

HTTP API POST 끝점은 `SlingPostOperation` 인터페이스(패키지 `org.apache.sling.servlets.post`)를 구현하여 정의된 PostOperation 클래스입니다.

`PostOperation` 종료 구현은 `sling.post.operation`을(를) 작업이 응답할 값으로 설정합니다. :operation 매개 변수가 해당 값으로 설정된 모든 POST 요청은 이 구현 클래스에 위임됩니다.

`PostOperation`은 작업에 필요한 작업을 수행하는 `SocialOperation`을 호출합니다.

`PostOperation`은 `SocialOperation`의 결과를 수신하고 해당 응답을 클라이언트에 반환합니다.

#### SocialOperation 클래스 {#socialoperation-class}

각 `SocialOperation` 끝점은 AbstractSocialOperation 클래스를 확장하고 `performOperation()` 메서드를 무시합니다. 이 메서드는 작업을 완료하고 `SocialOperationResult`을 반환하거나 `OperationException`을 반환하는 데 필요한 모든 작업을 수행합니다. 이 경우 메시지가 있는 HTTP 오류 상태가 일반적인 JSON 응답 또는 성공 HTTP 상태 코드 대신 반환됩니다.

`AbstractSocialOperation`을 확장하면 `SocialComponents`을 다시 사용하여 JSON 응답을 보낼 수 있습니다.

#### SocialOperationResult 클래스 {#socialoperationresult-class}

`SocialOperationResult` 클래스는 `SocialOperation`의 결과로 반환되며 `SocialComponent`, HTTP 상태 코드 및 HTTP 상태 메시지로 구성됩니다.

`SocialComponent`은 작업의 영향을 받은 리소스를 나타냅니다.

만들기 작업의 경우 `SocialOperationResult`에 포함된 `SocialComponent`은 방금 만든 리소스를 나타내며 업데이트 작업의 경우 작업에 의해 변경되는 리소스를 나타냅니다. 삭제 작업에 대해 `SocialComponent`이(가) 반환되지 않았습니다.

사용된 성공 HTTP 상태 코드는 다음과 같습니다.

* 제작 작업을 위한 201
* 업데이트 작업을 위한 200
* 삭제 작업에 204

#### OperationException 클래스 {#operationexception-class}

요청이 유효하지 않거나 내부 오류, 잘못된 매개 변수 값, 부적절한 권한 등과 같은 일부 다른 오류가 발생하는 경우 작업을 수행할 때 `OperationExcepton`이(가) 발생할 수 있습니다. `OperationException`은 HTTP 상태 코드와 오류 메시지로 구성되며 이 메시지는 `PostOperatoin`에 대한 응답으로 클라이언트에 반환됩니다.

#### OperationService 클래스 {#operationservice-class}

소셜 구성 요소 프레임워크에서는 작업을 수행하는 비즈니스 논리를 `SocialOperation` 클래스 내에 구현하지 않고 대신 OSGi 서비스에 위임하는 것이 좋습니다. 비즈니스 로직용 OSGi 서비스를 사용하면 `SocialOperation` 종점에 의해 작동되는 `SocialComponent`이 다른 코드와 통합되고 다른 비즈니스 로직이 적용되도록 할 수 있습니다.

모든 `OperationService` 클래스는 `AbstractOperationService`을(를) 확장하여 수행 중인 작업에 연결할 수 있는 추가 확장을 허용합니다. 서비스의 각 작업은 `SocialOperation` 클래스로 표시됩니다. `OperationExtensions` 클래스는 메서드를 호출하여 작업을 실행하는 동안 호출할 수 있습니다

* `performBeforeActions()`

   사전 검사/사전 처리 및 유효성 검사 허용
* `performAfterActions()`

   리소스를 추가로 수정하거나 사용자 지정 이벤트, 워크플로우 등을 호출할 수 있습니다.

#### OperationExtension 클래스 {#operationextension-class}

`OperationExtension` 클래스는 비즈니스 요구 사항에 맞게 작업을 사용자 정의할 수 있는 작업에 삽입될 수 있는 사용자 정의 코드 조각입니다. 구성 요소의 소비자는 구성 요소에 기능을 동적으로 그리고 점진적으로 추가할 수 있습니다. 익스텐션/후크 패턴을 사용하면 개발자는 익스텐션 자체에만 집중할 수 있으며 전체 작업과 구성 요소를 복사하고 재정의할 필요가 없습니다.

## 샘플 코드 {#sample-code}

샘플 코드는 [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) 저장소에서 사용할 수 있습니다. `aem-communities` 또는 `aem-scf`로 접두사가 붙은 프로젝트를 검색합니다.

## 우수 사례 {#best-practices}

AEM Communities 개발자를 위한 다양한 코딩 지침 및 모범 사례에 대한 [코딩 가이드라인](code-guide.md) 섹션을 참조하십시오.

사용자 생성 컨텐츠에 액세스하는 방법에 대한 자세한 내용은 UGC](srp.md)용 [SRP(저장소 리소스 공급자)를 참조하십시오.

| **[Feature ⇐ Essentials](essentials.md)** | **[클라이언트 측 맞춤화 =](client-customize.md)** |
|---|---|
|  | **[SCF 핸들바르를 돕는 사람 =](handlebars-helpers.md)** |

