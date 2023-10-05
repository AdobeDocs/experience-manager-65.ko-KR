---
title: AEM의 폐쇄형 사용자 그룹
description: AEM의 폐쇄형 사용자 그룹에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
source-git-commit: 71b3f7c6ad2c7712762a29518de6cf0639081cb7
workflow-type: tm+mt
source-wordcount: '6845'
ht-degree: 1%

---

# AEM의 폐쇄형 사용자 그룹{#closed-user-groups-in-aem}

## 소개 {#introduction}

AEM 6.3 이후, 기존 구현에 존재하는 성능, 확장성 및 보안 문제를 해결하기 위한 새로운 폐쇄형 사용자 그룹 구현이 있습니다.

>[!NOTE]
>
>간결성을 위해, CUG 약어는 본 문서 전체에서 사용될 것이다.

새 구현의 목표는 기존 버전의 문제와 디자인 제한 사항을 해결하는 동시에 필요한 기존 기능을 다루는 것입니다. 그 결과 다음과 같은 특성을 가진 새로운 CUG 설계가 이루어졌습니다.

* 개별적으로 또는 함께 사용할 수 있는 인증 및 권한 부여 요소의 명확한 분리
* 다른 액세스 제어 설정 및 권한 요구 사항에 간섭하지 않고 구성된 CUG 트리에서 제한된 읽기 액세스를 반영하기 위한 전용 인증 모델
* 작성 인스턴스에 일반적으로 필요한 제한된 읽기 액세스의 액세스 제어 설정과 게시에만 일반적으로 필요한 권한 평가 간의 구분
* 권한 에스컬레이션 없이 제한된 읽기 액세스 편집
* 인증 요구 사항을 표시하는 전용 노드 유형 확장
* 인증 요구 사항과 연결된 선택적 로그인 경로입니다.

### 새로운 사용자 지정 사용자 그룹 구현 {#the-new-custom-user-group-implementation}

AEM의 컨텍스트에서 알려진 CUG는 다음 단계로 구성됩니다.

* 보호해야 하는 트리에서 읽기 액세스를 제한하고 지정된 CUG 인스턴스와 함께 나열되거나 CUG 평가에서 모두 제외된 주도자에 대해서만 읽기를 허용합니다. 이를 라고 합니다. **authorization** 요소를 생성하지 않습니다.
* 지정된 트리에 인증을 적용하고 선택적으로 해당 트리에 대해 이후에 제외되는 전용 로그인 페이지를 지정합니다. 이를 라고 합니다. **인증** 요소를 생성하지 않습니다.

새로운 구현은 인증과 권한 부여 요소 사이에 선을 긋도록 설계되었습니다. AEM 6.3부터는 인증 요구 사항을 명시적으로 추가하지 않고 읽기 액세스를 제한할 수 있습니다. 예를 들어, 지정된 인스턴스가 인증을 모두 필요로 하거나 지정된 트리가 이미 인증을 필요로 하는 하위 트리에 있는 경우.

마찬가지로, 주어진 트리는 유효 권한 설정을 변경하지 않고 인증 요구 사항으로 표시될 수 있습니다. 조합 및 결과는 [CUG 정책 및 인증 요구 사항 결합](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) 섹션.

## 개요 {#overview}

### 인증: 읽기 액세스 제한 {#authorization-restricting-read-access}

CUG의 주요 기능은 선택된 주도자를 제외한 모든 사용자에 대해 컨텐츠 저장소의 특정 트리에 대한 읽기 액세스를 제한하는 것입니다. 새로운 구현에서는 즉시 기본 액세스 제어 콘텐츠를 조작하는 대신 CUG를 나타내는 전용 유형의 액세스 제어 정책을 정의하여 다른 접근 방식을 사용합니다.

#### CUG에 대한 액세스 제어 정책 {#access-control-policy-for-cug}

이 새로운 유형의 정책에는 다음과 같은 특성이 있습니다.

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy(Apache Jackrabbit API로 정의됨) 유형의 액세스 제어 정책
* PrincipalSetPolicy는 수정 가능한 주체 집합에 권한을 부여합니다.
* 부여된 권한 및 정책 범위는 구현 세부 정보입니다.

또한 CUG를 나타내는 데 사용되는 PrincipalSetPolicy 구현은 다음을 정의합니다.

* CUG 정책은 일반 JCR 항목에 대한 읽기 액세스만 허용합니다(예: 액세스 제어 콘텐츠는 제외됨).
* 범위는 CUG 정책을 보유하는 액세스 제어 노드에 의해 정의됩니다.
* CUG 정책은 중첩될 수 있으며, 중첩된 CUG는 &#39;상위&#39; CUG의 주 집합을 상속하지 않고 새 CUG를 시작합니다.
* 평가가 활성화된 경우 정책의 효과는 다음 중첩 CUG까지 전체 하위 트리에 상속됩니다.

이러한 CUG 정책은 oak-authorization-cug라는 별도의 인증 모듈을 통해 AEM 인스턴스에 배포됩니다. 이 모듈에는 자체 액세스 제어 관리 및 권한 평가가 함께 제공됩니다. 즉, 기본 AEM 설정에는 여러 인증 메커니즘을 결합하는 Oak 콘텐츠 저장소 구성이 제공됩니다. 자세한 내용은 [apache Oak 설명서의 이 페이지](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

이 복합 설정에서 새 CUG는 대상 노드에 연결된 기존 액세스 제어 콘텐츠를 대체하지 않지만, 나중에 원래 액세스 제어에 영향을 주지 않고 제거할 수 있는 보충 콘텐츠로 설계되었습니다. 즉, AEM의 기본 액세스 제어 목록이 됩니다.

이전 구현과 달리 새로운 CUG 정책은 항상 액세스 제어 콘텐츠로 인식되고 처리됩니다. 이는 JCR 액세스 제어 관리 API를 사용하여 만들고 편집함을 의미합니다. 자세한 내용은 [CUG 정책 관리](#managing-cug-policies) 섹션.

#### CUG 정책의 권한 평가 {#permission-evaluation-of-cug-policies}

CUG에 대한 전용 액세스 제어 관리 외에도 새로운 인증 모델을 사용하면 정책에 대한 권한 평가를 조건부로 활성화할 수 있습니다. 이렇게 하면 스테이징 환경에서 CUG 정책을 설정할 수 있으며, 프로덕션 환경에 복제되는 경우에만 유효 권한을 평가할 수 있습니다.

CUG 정책 및 기본 또는 추가 인증 모델과의 상호 작용에 대한 권한 평가는 Apache Jackrabbit Oak의 여러 인증 메커니즘용으로 설계된 패턴을 따릅니다. 주어진 권한 집합은 모든 모델이 액세스를 허용하는 경우에만 부여됩니다. 다음을 참조하십시오 [이 페이지](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) 을 참조하십시오.

CUG 정책을 처리하고 평가하기 위해 설계된 권한 모델과 연관된 권한 평가에는 다음과 같은 특성이 적용됩니다.

* 일반 노드 및 속성에 대한 읽기 권한만 처리하지만 액세스 제어 컨텐츠는 읽지 않습니다
* 쓰기 권한이나 보호된 JCR 콘텐츠를 수정하는 데 필요한 권한(액세스 제어, 노드 유형 정보, 버전 관리, 잠금 또는 사용자 관리 등)은 처리하지 않습니다. 이러한 권한은 CUG 정책의 영향을 받지 않으며 관련 인증 모델로 평가되지 않습니다. 이러한 권한을 부여할지 여부는 보안 설정에 구성된 다른 모델에 따라 다릅니다.

허가 평가에 따른 단일 CUG 정책의 효과는 다음과 같이 요약할 수 있다.

* 정책에 나열된 제외된 주도자 또는 주도자가 포함된 주제를 제외한 모든 사용자에 대해 읽기 액세스가 거부됩니다.
* 정책은 정책 및 해당 속성을 보유하는 액세스 제어 노드에 적용됩니다.
* 이 효과는 계층 아래(즉, 액세스 제어 노드에 의해 정의된 항목 트리)에서 추가로 상속됩니다.
* 그러나 액세스 제어 노드의 형제 자매나 조상은 영향을 받지 않습니다.
* 주어진 CUG의 상속은 중첩된 CUG에서 중단된다.

#### 모범 사례 {#best-practices}

CUG를 통한 제한된 읽기 액세스를 정의하기 위해 다음 모범 사례를 고려해야 합니다.

* CUG가 읽기 액세스를 제한해야 하는지 또는 인증 요구 사항을 제한해야 하는지에 대해 의식적으로 판단하십시오. 후자 또는 둘 다 필요한 경우 인증 요구 사항과 관련된 자세한 내용은 모범 사례 섹션을 참조하십시오
* 위협 경계를 식별하고 인증된 액세스와 관련된 데이터 및 역할의 민감도에 대한 명확한 그림을 얻기 위해 보호해야 하는 데이터 또는 컨텐츠에 대한 위협 모델을 만듭니다
* 일반적인 인증 관련 측면 및 모범 사례를 염두에 두고 저장소 콘텐츠 및 CUG를 모델링합니다.

   * 지정된 CUG와 설정 부여에 배포된 다른 모듈의 평가로 지정된 주체가 지정된 저장소 항목을 읽을 수 있는 경우에만 읽기 권한이 부여됩니다
   * 다른 인증 모듈에 의해 읽기 액세스가 이미 제한된 중복 CUG를 만들지 마십시오.
   * 중첩된 CUG가 과도하게 필요한 경우 콘텐츠 디자인에서 문제가 잠재적으로 강조될 수 있습니다
   * CUG에 대한 요구(예: 모든 단일 페이지에서)가 너무 과도하면 애플리케이션 및 콘텐츠의 특정 보안 요구 사항에 보다 적합할 수 있는 사용자 지정 인증 모델이 필요할 수 있습니다.

* CUG 정책에 대해 지원되는 경로를 저장소의 몇 개 트리로 제한하여 최적화된 성능을 허용합니다. 예를 들어 AEM 6.3 이후 기본값으로 제공되는 /content 노드 아래의 CUG만 허용합니다.
* CUG 정책은 작은 주체 집합에 대한 읽기 액세스 권한을 부여하도록 설계되었습니다. 많은 교장이 필요하므로 콘텐츠 또는 애플리케이션 디자인에서 문제가 부각될 수 있으므로 재고해야 합니다.

### 인증: 인증 요구 사항 정의 {#authentication-defining-the-auth-requirement}

CUG 기능의 인증 관련 부분을 사용하면 인증이 필요한 트리를 표시하고 선택적으로 전용 로그인 페이지를 지정할 수 있습니다. 이전 버전에 따라 새 구현을 사용하면 콘텐츠 저장소에서 인증이 필요한 트리를 표시하고 과의 동기화를 조건부로 활성화할 수 있습니다. `Sling org.apache.sling.api.auth.Authenticator`궁극적으로 요구 사항을 적용하고 로그인 리소스로 리디렉션할 책임이 있습니다.

이러한 요구 사항은 다음을 제공하는 OSGi 서비스를 통해 인증자에게 등록됩니다. `sling.auth.requirements` 등록 정보. 그런 다음 이러한 속성을 사용하여 인증 요구 사항을 동적으로 확장합니다. 자세한 내용은 [Sling 설명서](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### 전용 Mixin 유형을 사용하여 인증 요구 사항 정의 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

보안상의 이유로 새 구현은 잔여 JCR 속성의 사용을 라는 전용 mixin 유형으로 대체합니다. `granite:AuthenticationRequired`로그인 경로에 대해 STRING 유형의 단일 선택적 속성을 정의합니다. `granite:loginPath`. 이 mixin 유형과 관련된 콘텐츠 변경 사항만 Apache Sling Authenticator에 등록된 요구 사항을 업데이트하게 됩니다. 이러한 수정은 일시적인 수정이 지속되면 추적되므로 `javax.jcr.Session.save()` 효력을 발휘하라고 외치다.

이는 다음과 같습니다. `granite:loginPath` 속성. 인증 요구 사항 관련 mixin 유형에 의해 정의되는 경우에만 존중됩니다. 구조화되지 않은 JCR 노드에서 이 이름을 가진 잔여 속성을 추가해도 원하는 효과가 표시되지 않으며 속성은 OSGi 등록 업데이트를 담당하는 핸들러에서 무시됩니다.

>[!NOTE]
>
>로그인 경로 속성을 설정하는 것은 선택 사항이며, 인증이 필요한 트리가 기본 또는 상속된 로그인 페이지로 돌아갈 수 없는 경우에만 필요합니다. 다음을 참조하십시오. [로그인 경로 평가](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) 아래요.

#### Sling 인증자에 인증 요구 사항 및 로그인 경로 등록 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

이 유형의 인증 요구 사항은 특정 실행 모드 및 컨텐츠 저장소 내의 작은 트리 하위 집합으로 제한될 것으로 예상되므로 요구 사항 mixin 유형 및 로그인 경로 등록 정보 추적은 조건부이며 지원되는 경로를 정의하는 해당 구성에 바인딩됩니다(아래 구성 옵션 참조). 따라서 이러한 지원되는 경로의 범위 내에서 변경 사항만 OSGi 등록 업데이트를 트리거하고, 다른 곳에서는 mixin 유형과 속성이 모두 무시됩니다.

이제 기본 AEM 설정은 작성자 실행 모드에서 mixin을 설정할 수 있도록 하여 이 구성을 활용하지만 게시 인스턴스에 복제할 때만 영향을 줍니다. 다음을 참조하십시오 [이 페이지](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) 슬링이 인증 요구 사항을 적용하는 방법에 대해 자세히 설명합니다.

추가 `granite:AuthenticationRequired` 구성된 지원 경로 내의 mixin 유형을 사용하면 책임 처리기의 OSGi 등록이 다음과 같은 새로운 추가 항목을 포함하여 업데이트됩니다. `sling.auth.requirements` 속성. 지정된 인증 요구 사항이 옵션을 지정하는 경우 `granite:loginPath` 속성, 값을 인증 요구 사항에서 제외하기 위해 &#39;-&#39; 접두사가 있는 인증자로 추가로 등록합니다.

#### 인증 요구 사항의 평가 및 상속 {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling 인증 요구 사항은 페이지 또는 노드 계층 구조를 통해 상속될 예정입니다. 상속의 세부 사항과 순서 및 우선 순위 등 인증 요구 사항에 대한 평가는 구현 세부 사항으로 간주되며 이 문서에 문서화되지 않습니다.

#### 로그인 경로 평가 {#evaluation-of-login-path}

로그인 경로 평가 및 인증 시 해당 리소스로 리디렉션은 현재 Adobe Granite Login Selector Authentication Handler( )의 구현 세부 사항입니다. `com.day.cq.auth.impl.LoginSelectorHandler`): 기본적으로 AEM으로 구성된 Apache Sling AuthenticationHandler입니다.

호출 시 `AuthenticationHandler.requestCredentials` 이 처리기는 사용자를 리디렉션할 매핑 로그인 페이지를 결정하려고 합니다. 여기에는 다음 단계가 포함됩니다.

* 리디렉션의 이유로 만료된 암호와 일반 로그인의 필요성을 구별합니다.
* 일반 로그인의 경우 은 다음 순서로 로그인 경로를 얻을 수 있는지 테스트합니다.

   * 을 사용하여 새로 구현한 대로 LoginPathProvider에서 `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * 더 이상 사용되지 않는 이전 CUG 구현에서
   * 로 정의된 로그인 페이지 매핑에서 `LoginSelectorHandler`,
   * 마지막으로, 로 정의한 대로 기본 로그인 페이지로 돌아갑니다. `LoginSelectorHandler`.

* 위에 나열된 호출을 통해 올바른 로그인 경로를 얻으면 사용자의 요청이 해당 페이지로 리디렉션됩니다.

이 설명서의 대상은 내부에 의해 노출된 로그인 경로에 대한 평가입니다 `LoginPathProvider` 인터페이스. AEM 6.3 이후 제공된 구현은 다음과 같이 작동합니다.

* 로그인 경로의 등록은 만료된 암호를 구별하는 것에 따라 다르며 리디렉션의 이유로 일반 로그인이 필요합니다
* 일반 로그인의 경우 은 다음 순서로 로그인 경로를 얻을 수 있는지 테스트합니다.

   * 다음에서 `LoginPathProvider` 새로운 `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * 더 이상 사용되지 않는 이전 CUG 구현에서
   * (으)로 정의된 로그인 페이지 매핑 `LoginSelectorHandler`,
   * 및 를 포함하여 정의된 기본 로그인 페이지로 돌아갑니다. `LoginSelectorHandler`.

* 위에 나열된 호출을 통해 올바른 로그인 경로를 얻으면 사용자의 요청이 해당 페이지로 리디렉션됩니다.

다음 `LoginPathProvider` granite의 새로운 인증 요구 사항 지원에 의해 구현되면 `granite:loginPath` 위에서 설명한 대로 mixin 유형에 의해 정의되는 속성입니다. 로그인 경로를 포함하는 리소스 경로와 속성 값 자체의 매핑은 메모리에 유지되며 계층의 다른 노드에 적합한 로그인 경로를 찾기 위해 평가됩니다.

>[!NOTE]
>
>평가는 구성된 지원 경로에 있는에 있는 리소스와 연결된 요청에 대해서만 수행됩니다. 다른 모든 요청의 경우 로그인 경로를 결정하는 대체 방법이 평가됩니다.

#### 모범 사례 {#best-practices-1}

인증 요구 사항을 정의할 때 다음 모범 사례를 고려해야 합니다.

* 인증 요구 사항을 중첩하지 마십시오. 트리 시작 부분에 단일 인증 요구 사항 마커를 배치하면 충분하며 대상 노드에 의해 정의된 전체 하위 트리에 상속됩니다. 해당 트리 내에서 추가 인증 요구 사항은 중복으로 간주해야 하며 Apache Sling 내에서 인증 요구 사항을 평가하는 동안 성능 문제가 발생할 수 있습니다. 권한 부여 및 인증 관련 CUG 영역을 분리하면 전체 트리에 대한 인증을 시행하는 동시에 CUG 또는 다른 유형의 정책을 통해 읽기 액세스를 제한할 수 있습니다.
* 중첩된 하위 트리를 요구 사항에서 다시 제외하지 않고도 인증 요구 사항이 전체 트리에 적용되도록 저장소 콘텐츠를 모델링합니다.
* 중복 로그인 경로를 지정하지 않고 나중에 등록하려면 다음을 수행하십시오.

   * 상속을 사용하고 중첩된 로그인 경로를 정의하지 마십시오.
   * 선택적 로그인 경로를 기본값이나 상속된 값에 해당하는 값으로 설정하지 마십시오.
   * 애플리케이션 개발자는 과 연관된 전역 로그인 경로 구성(기본값 및 매핑 모두)에서 구성할 로그인 경로를 식별해야 합니다. `LoginSelectorHandler`.

## 저장소에서의 표시 {#representation-in-the-repository}

### 저장소의 CUG 정책 표시 {#cug-policy-representation-in-the-repository}

Oak 설명서는 새로운 CUG 정책이 저장소 컨텐츠에 반영되는 방식을 다룹니다. 자세한 내용은 [이 페이지](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### 저장소의 인증 요구 사항 {#authentication-requirement-in-the-repository}

별도의 인증 요구 사항이 필요한 경우 대상 노드에 배치된 전용 mixin 노드 유형을 사용하는 저장소 콘텐츠에 반영됩니다. mixin 유형은 대상 노드가 정의한 트리에 대한 전용 로그인 페이지를 지정하는 선택적 속성을 정의합니다.

로그인 경로와 연관된 페이지는 해당 트리의 내부 또는 외부에 위치할 수 있다. 인증 요구 사항에서 제외됩니다.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## CUG 정책 및 인증 요구 사항 관리 {#managing-cug-policies-and-authentication-requirement}

### CUG 정책 관리 {#managing-cug-policies}

CUG에 대한 읽기 액세스를 제한하는 새로운 유형의 액세스 제어 정책은 JCR 액세스 제어 관리 API를 사용하여 관리되며 다음과 같이 설명된 메커니즘을 따릅니다. [JCR 2.0 사양](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### 새 CUG 정책 설정 {#set-a-new-cug-policy}

이전에 CUG가 설정되지 않은 노드에서 새 CUG 정책을 적용하는 코드입니다. 다음을 참고하십시오. `getApplicablePolicies` 은 이전에 설정되지 않은 새 정책만 반환합니다. 마지막에 정책을 다시 기록해야 하며 변경 사항을 지속해야 합니다.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (for example,
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 기존 CUG 정책 편집 {#edit-an-existing-cug-policy}

기존 CUG 정책을 편집하려면 다음 단계를 수행해야 합니다. 수정된 정책은 다시 작성해야 하며 변경 사항은 를 사용하여 지속해야 합니다 `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### 효과적인 CUG 정책 검색 {#retrieve-effective-cug-policies}

JCR 액세스 제어 관리는 지정된 경로에서 적용되는 정책을 검색하기 위한 최상의 방법을 정의합니다. CUG 정책의 평가는 조건부이며, 활성화할 해당 구성에 따라 다르기 때문에 를 호출합니다. `getEffectivePolicies` 는 특정 CUG 정책이 특정 설치에서 적용되는지 확인하는 편리한 방법입니다.

>[!NOTE]
>
>다음 사이에 차이점이 있는지 확인하십시오. `getEffectivePolicies` 및 다음 코드 예제에서는 주어진 경로가 이미 기존 CUG의 일부인지 계층 구조를 살펴봅니다.

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### 상속된 CUG 정책 검색 {#retrieve-inherited-cug-policies}

적용 여부에 관계없이 주어진 경로에 정의된 모든 중첩 CUG 찾기 자세한 내용은 [구성 옵션](/help/sites-administering/closed-user-groups.md#configuration-options) 섹션.

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### 주도자별 CUG 정책 관리 {#managing-cug-policies-by-pincipal}

에서 정의한 확장 `JackrabbitAccessControlManager` 주체가 액세스 제어 정책을 편집할 수 있도록 허용하는 것은 CUG 액세스 제어 관리를 사용하여 구현되지 않습니다. 정의에 따라 CUG 정책은 모든 주체(다음과 함께 나열된 주체)에 항상 영향을 미칩니다. `PrincipalSetPolicy` 읽기 액세스 권한이 부여되지만 다른 모든 주도자는 대상 노드에 의해 정의된 트리에서 콘텐츠를 읽을 수 없습니다.

해당 메서드는 항상 빈 정책 배열을 반환하지만 예외를 throw하지 않습니다.

### 인증 요구 사항 관리 {#managing-the-authentication-requirement}

대상 노드의 유효 노드 유형을 변경하여 새 인증 요구 사항을 생성, 수정 또는 제거합니다. 그런 다음 일반 JCR API를 사용하여 선택적 로그인 경로 속성을 작성할 수 있습니다.

>[!NOTE]
>
>위에 언급된 특정 대상 노드에 대한 수정 사항은 다음 경우에만 Apache Sling 인증자에 반영됩니다. `RequirementHandler` 가 구성되었으며 타겟이 지원되는 경로에 정의된 트리에 포함되어 있습니다( 구성 옵션 섹션 참조).
>
>자세한 내용은 [Mixin 노드 유형 할당](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Mixin 노드 유형 할당) 및 [노드 추가 및 속성 설정](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 노드 추가 및 속성 설정)

#### 새 인증 요구 사항 추가 {#adding-a-new-auth-requirement}

새 인증 요구 사항을 만드는 단계는 아래에 자세히 설명되어 있습니다. 이 경우 요구 사항은 Apache Sling 인증자에만 등록됩니다. `RequirementHandler` 대상 노드가 포함된 트리에 대해 가 구성되었습니다.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 로그인 경로로 새 인증 요구 사항 추가 {#add-a-new-auth-requirement-with-login-path}

로그인 경로를 포함한 새 인증 요구 사항을 만드는 단계입니다. 로그인 경로에 대한 요구 사항 및 제외는 `RequirementHandler` 대상 노드가 포함된 트리에 대해 가 구성되었습니다.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 기존 로그인 경로 수정 {#modify-an-existing-login-path}

기존 로그인 경로를 변경하는 단계는 아래에 자세히 설명되어 있습니다. 다음과 같은 경우에만 Apache Sling 인증자에 수정 사항이 등록됩니다. `RequirementHandler` 대상 노드가 포함된 트리에 대해 가 구성되었습니다. 이전 로그인 경로 값이 등록에서 제거됩니다. 대상 노드와 연결된 인증 요구 사항은 이 수정 사항의 영향을 받지 않습니다.

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### 기존 로그인 경로 제거 {#remove-an-existing-login-path}

기존 로그인 경로를 제거하는 절차. 다음과 같은 경우에만 로그인 경로 항목이 Apache Sling Authenticator에서 등록 취소됩니다. `RequirementHandler` 대상 노드가 포함된 트리에 대해 가 구성되었습니다. 대상 노드와 연결된 인증 요구 사항은 영향을 받지 않습니다.

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

또는 동일한 목적을 달성하기 위해 아래 방법을 사용할 수 있습니다.

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### 인증 요구 사항 제거 {#remove-an-auth-requirement}

기존 인증 요구 사항을 제거하는 절차. 다음과 같은 경우에만 Apache Sling 인증자에서 요구 사항이 등록 취소됩니다. `RequirementHandler` 대상 노드가 포함된 트리에 대해 가 구성되었습니다.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 유효한 인증 요구 사항 검색 {#retrieve-effective-auth-requirements}

Apache Sling Authenticator에 등록된 모든 유효 인증 요구 사항을 읽을 수 있는 전용 공개 API는 없습니다. 그러나 이 목록은 의 시스템 콘솔에 표시됩니다. `https://<serveraddress>:<serverport>/system/console/slingauth` 의 아래에&#x200B;**인증 요구 사항 구성**&quot; 섹션.

다음 이미지는 데모 콘텐츠가 있는 AEM 게시 인스턴스의 인증 요구 사항을 보여줍니다. 커뮤니티 페이지의 강조 표시된 경로는 이 문서에 설명된 구현에서 추가한 요구 사항이 Apache Sling 인증자에 어떻게 반영되는지 보여줍니다.

>[!NOTE]
>
>이 예제에서 선택적 로그인 경로 속성이 설정되지 않았습니다. 따라서 인증자에 두 번째 항목이 등록되지 않았습니다.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 유효한 로그인 경로 검색 {#retrieve-the-effective-login-path}

현재 인증이 필요한 리소스에 익명으로 액세스할 때 적용되는 로그인 경로를 검색할 공개 API가 없습니다. 로그인 경로를 검색하는 방법에 대한 자세한 내용은 로그인 경로 평가 섹션을 참조하십시오.

그러나 이 기능으로 정의된 로그인 경로 외에도 로그인으로 리디렉션을 지정하는 대체 방법이 있습니다. 이는 지정된 AEM 설치의 콘텐츠 모델 및 인증 요구 사항을 디자인할 때 고려해야 합니다.

#### 상속된 인증 요구 사항 검색 {#retrieve-the-inherited-auth-requirement}

로그인 경로와 마찬가지로 콘텐츠에 정의된 상속된 인증 요구 사항을 검색하는 공개 API는 없습니다. 다음 예제에서는 적용 여부에 관계없이 주어진 계층으로 정의된 모든 인증 요구 사항을 나열하는 방법을 보여줍니다. 자세한 내용은 [구성 옵션](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>인증 요구 사항과 로그인 경로 모두에 대해 상속 메커니즘을 사용하고 중첩된 인증 요구 사항을 만들지 않는 것이 좋습니다.
>
>자세한 내용은 [인증 요구 사항의 평가 및 상속](#evaluation-and-inheritance-of-the-authentication-requirement), [로그인 경로 평가](#evaluation-of-login-path) 및 [우수 사례](#best-practices).

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### CUG 정책 및 인증 요구 사항 결합 {#combining-cug-policies-and-the-authentication-requirement}

다음 표에는 구성을 통해 두 모듈을 모두 활성화한 AEM 인스턴스의 유효한 CUG 정책 조합과 인증 요구 사항이 나와 있습니다.

| **인증 필요** | **로그인 경로** | **제한된 읽기 액세스** | **기대 효과** |
|---|---|---|---|
| 예 | 예 | 예 | 유효 권한 평가에서 액세스 권한을 부여하는 경우 지정된 사용자는 CUG 정책으로 표시된 하위 트리만 볼 수 있습니다. 인증되지 않은 사용자는 지정된 로그인 페이지로 리디렉션됩니다. |
| 예 | 아니요 | 예 | 유효 권한 평가에서 액세스 권한을 부여하는 경우 지정된 사용자는 CUG 정책으로 표시된 하위 트리만 볼 수 있습니다. 인증되지 않은 사용자는 상속된 기본 로그인 페이지로 리디렉션됩니다. |
| 예 | 예 | 아니요 | 인증되지 않은 사용자는 지정된 로그인 페이지로 리디렉션됩니다. 인증 요구 사항으로 표시된 트리를 볼 수 있는지 여부는 해당 하위 트리에 포함된 개별 항목의 유효 권한에 따라 다릅니다. 읽기 액세스를 적절히 제한하는 전용 CUG가 없습니다. |
| 예 | 아니요 | 아니요 | 인증되지 않은 사용자는 상속된 기본 로그인 페이지로 리디렉션됩니다. 인증 요구 사항으로 표시된 트리를 볼 수 있는지 여부는 해당 하위 트리에 포함된 개별 항목의 유효 권한에 따라 다릅니다. 읽기 액세스를 적절히 제한하는 전용 CUG가 없습니다. |
| 아니요 | 아니요 | 예 | 지정된 인증된 사용자 또는 인증되지 않은 사용자는 유효 권한 평가에서 액세스 권한을 부여하는 경우 CUG 정책으로 표시된 하위 트리만 볼 수 있습니다. 인증되지 않은 사용자는 동일하게 처리되며 로그인을 위해 리디렉션되지 않습니다. |

>[!NOTE]
>
>&#39;로그인 경로&#39;는 인증 요구 사항과 연결된 선택적 속성이므로 &#39;인증 요구 사항&#39; = No와 &#39;로그인 경로&#39; = Yes의 조합은 위에 나열되지 않습니다. 정의 mixin 형식을 추가하지 않고 해당 이름으로 JCR 속성을 지정하면 효과가 없으며 해당 처리기에서 무시됩니다.

## OSGi 구성 요소 및 구성 {#osgi-components-and-configuration}

이 섹션에서는 OSGi 구성 요소 및 새로운 CUG 구현과 함께 도입된 개별 구성 옵션에 대한 개요를 제공합니다.

이전 구현과 새 구현 간의 구성 옵션에 대한 포괄적인 매핑은 CUG 매핑 설명서 를 참조하십시오.

### 인증: 설정 및 구성 {#authorization-setup-and-configuration}

새로운 인증 관련 부분이에 포함되어 있습니다. **Oak CUG 인증** 번들 ( `org.apache.jackrabbit.oak-authorization-cug`): AEM 기본 설치의 일부입니다. 번들은 읽기 액세스를 관리하기 위한 추가 방법으로 배포되는 것을 목표로 하는 분리된 인증 모델을 정의한다.

#### CUG 인증 설정 {#setting-up-cug-authorization}

CUG 권한 설정에 대해서는 다음에서 자세히 설명합니다. [관련 Apache 설명서](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). 기본적으로 AEM에는 모든 실행 모드에서 배포된 CUG 인증이 있습니다. 다른 인증 설정이 필요한 설치에서 CUG 인증을 비활성화하는 데 단계별 지침을 사용할 수도 있습니다.

#### 레퍼러 필터 구성 {#configuring-the-referrer-filter}

또한 다음을 구성해야 합니다. [Sling 레퍼러 필터](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) CDN, 로드 밸런서 등을 통해 AEM에 액세스하는 데 사용할 수 있는 모든 호스트 이름

레퍼러 필터가 구성되지 않은 경우 사용자가 CUG 사이트에 로그인하려고 하면 다음과 유사한 오류가 표시됩니다.

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi 구성 요소의 특성 {#characteristics-of-osgi-components}

인증 요구 사항을 정의하고 전용 로그인 경로를 지정하기 위해 다음 두 가지 OSGi 구성 요소가 도입되었습니다.

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>레이블</td>
   <td>Apache Jackrabbit Oak CUG 구성</td>
  </tr>
  <tr>
   <td>설명</td>
   <td>CUG 권한을 설정하고 평가하는 데 필요한 인증 구성입니다.</td>
  </tr>
  <tr>
   <td>구성 속성</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>또한 다음을 참조하십시오 <a href="#configuration-options">구성 옵션</a> 아래요.</p> </td>
  </tr>
  <tr>
   <td>구성 정책</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>참조</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>레이블</td>
   <td>Apache Jackrabbit Oak CUG 제외 목록</td>
  </tr>
  <tr>
   <td>설명</td>
   <td>구성된 이름의 주체를 CUG 평가에서 제외할 수 있습니다.</td>
  </tr>
  <tr>
   <td>구성 속성</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>아래의 구성 옵션 섹션도 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>구성 정책</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>참조</td>
   <td>NA</td>
  </tr>
 </tbody>
</table>

#### 구성 옵션 {#configuration-options}

주요 구성 옵션은 다음과 같습니다.

* `cugSupportedPaths`: CUG를 포함할 수 있는 하위 트리를 지정합니다. 기본값이 설정되지 않음
* `cugEnabled`: 현재 CUG 정책에 대한 권한 평가를 활성화하는 구성 옵션입니다.

CUG 인증 모듈과 연관된 사용 가능한 구성 옵션이 나열되고 다음에서 자세히 설명합니다. [Apache Oak 설명서](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### CUG 평가에서 주도자 제외 {#excluding-principals-from-cug-evaluation}

개별 학교장은 CUG 평가에서 면제하는 것이 전자의 시행에서 채택되었다. 새로운 CUG 인증은 CugExclude라는 전용 인터페이스를 통해 이를 다룹니다. Apache Jackrabbit Oak 1.4는 고정된 주도자 세트와 개별 주도자 이름을 구성할 수 있는 확장 구현을 제외하는 기본 구현과 함께 제공됩니다. 후자는 AEM 게시 인스턴스에 구성됩니다.

AEM 6.3부터 기본적으로 다음 주도자가 CUG 정책의 영향을 받지 않습니다.

* 관리 주체(관리 사용자, 관리자 그룹)
* 서비스 사용자 주체
* 저장소 내부 시스템 사용자

자세한 내용은 [AEM 6.3 이후 기본 구성](#default-configuration-since-aem) 아래 섹션.

&quot;관리자&quot; 그룹의 제외는 의 구성 섹션에 있는 시스템 콘솔에서 변경되거나 확장될 수 있습니다. **Apache Jackrabbit Oak CUG 제외 목록**.

또는 CugExclude 인터페이스의 사용자 지정 구현을 제공 및 배포하여 특별한 필요가 있는 경우 제외된 주도자 집합을 조정할 수 있습니다. 다음에서 설명서를 참조하십시오. [CUG 플러그성](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 자세한 내용 및 예제 구현

### 인증: 설정 및 구성 {#authentication-setup-and-configuration}

인증과 관련된 새로운 부분이에 포함되어 있습니다. **Adobe Granite 인증 핸들러** 번들 ( `com.adobe.granite.auth.authhandler` 버전 5.6.48). 이 번들은 AEM 기본 설치의 일부입니다.

더 이상 사용되지 않는 CUG 지원에 대한 인증 요구 사항 대체를 설정하려면 주어진 AEM 설치 시 일부 OSGi 구성 요소가 존재하고 활성 상태여야 합니다. 자세한 내용은 다음을 참조하십시오. **OSGi 구성 요소의 특성** 아래요.

>[!NOTE]
>
>RequirementHandler의 필수 구성 옵션으로 인해 지원되는 경로 집합을 지정하여 기능이 활성화된 경우에만 인증 관련 부분이 활성화됩니다. 표준 AEM 설치를 사용하면 작성자 실행 모드에서 이 기능이 비활성화되고 게시 실행 모드에서 /content에 대해 이 기능이 활성화됩니다.

**OSGi 구성 요소의 특성**

인증 요구 사항을 정의하고 전용 로그인 경로를 지정하기 위해 다음 두 가지 OSGi 구성 요소가 도입되었습니다.

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirement.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>레이블</td>
   <td>-</td>
  </tr>
  <tr>
   <td>설명</td>
   <td>인증 요구 사항에 영향을 주는 콘텐츠 변경 사항에 대한 관찰자를 등록하는 인증 요구 사항에 대한 전용 OSGi 서비스( 를 통해 ) <code>granite:AuthenticationRequirement</code> mixin 유형)과 가 있는 로그인 경로가 <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>구성 속성</td>
   <td>-</td>
  </tr>
  <tr>
   <td>구성 정책</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>참조</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler**

| 레이블 | Adobe Granite 인증 요구 사항 및 로그인 경로 핸들러 |
|---|---|
| 설명 | `RequirementHandler` apache Sling 인증 요구 사항 및 관련 로그인 경로에 대한 해당 제외를 업데이트하는 구현입니다. |
| 구성 속성 | `supportedPaths` |
| 구성 정책 | `ConfigurationPolicy.REQUIRE` |
| 참조 | NA |

#### 구성 옵션 {#configuration-options-1}

CUG 재작성의 인증 관련 부분은 Adobe Granite 인증 요구 사항 및 로그인 경로 핸들러와 연결된 단일 구성 옵션으로만 제공됩니다.

**&quot;인증 요구 사항 및 로그인 경로 핸들러&quot;**

<table>
 <tbody>
  <tr>
   <td>속성</td>
   <td>유형</td>
   <td>기본 값</td>
   <td>설명</td>
  </tr>
  <tr>
   <td><p>레이블 = 지원되는 경로</p> <p>이름 = 'supportedPaths'</p> </td>
   <td>설정&lt;string&gt;</td>
   <td>-</td>
   <td>이 처리기가 인증 요구 사항을 준수하는 경로입니다. 을(를) 추가하려면 이 구성을 설정하지 마십시오. <code>granite:AuthenticationRequirement</code> 를 적용하지 않고 노드에 믹스인 유형(예: 작성자 인스턴스에서). 누락된 경우 기능이 비활성화됩니다. </td>
  </tr>
 </tbody>
</table>

## AEM 6.3 이후 기본 구성 {#default-configuration-since-aem}

AEM을 새로 설치하면 기본적으로 CUG 기능의 권한 부여 및 인증 관련 부분에 대해 새 구현이 모두 사용됩니다. 이전 구현인 &quot;Adobe Granite CUG(폐쇄형 사용자 그룹) 지원&quot;은 더 이상 사용되지 않으며 기본적으로 모든 AEM 설치에서 비활성화됩니다. 대신 새 구현은 다음과 같이 활성화됩니다.

### 작성자 인스턴스 {#author-instances}

| **&quot;Apache Jackrabbit Oak CUG 구성&quot;** | **설명** |
|---|---|
| 지원되는 경로 `/content` | CUGpolicies에 대한 액세스 제어 관리가 활성화됩니다. |
| CUG 평가 활성화됨 FALSE | 권한 평가가 비활성화되었습니다. CUG 정책은 적용되지 않습니다. |
| 등급 | 200 | Oak 설명서 를 참조하십시오. |

>[!NOTE]
>
>에 대한 구성 없음 **Apache Jackrabbit Oak CUG 제외 목록** 및 **Adobe Granite 인증 요구 사항 및 로그인 경로 핸들러** 는 기본 작성 인스턴스에 있습니다.

### 게시 인스턴스 {#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG 구성&quot;** | **설명** |
|---|---|
| 지원되는 경로 `/content` | CUG 정책에 대한 액세스 제어 관리가 구성된 경로 아래에서 활성화됩니다. |
| CUG 평가 활성화됨 TRUE | 권한 평가는 구성된 경로 아래에서 활성화됩니다. CUG 정책은 다음에 적용됩니다. `Session.save()`. |
| 등급 | 200 | Oak 설명서 를 참조하십시오. |

| **&quot;Apache Jackrabbit Oak CUG 제외 목록&quot;** | **설명** |
|---|---|
| 주도자 이름 관리자 | CUG 평가에서 관리자 주도자를 제외합니다. |

| **&quot;Adobe Granite 인증 요구 사항 및 로그인 경로 핸들러&quot;** | **설명** |
|---|---|
| 지원되는 경로  `/content` | 다음을 통해 저장소에 정의된 인증 요구 사항 `granite:AuthenticationRequired` 믹스인 유형은 아래에 적용됩니다. `/content` 다음에 대해 `Session.save()`. Sling 인증자가 업데이트되었습니다. 지원되는 경로 외부에 믹스인 유형을 추가하는 것은 무시됩니다. |

## CUG 인증 및 인증 요구 사항 비활성화 {#disabling-cug-authorization-and-authentication-requirement}

주어진 설치가 CUG를 사용하지 않거나 인증 및 권한 부여에 다른 수단을 사용하는 경우 새 구현이 완전히 비활성화될 수 있습니다.

### CUG 인증 비활성화 {#disable-cug-authorization}

다음을 참조하십시오. [CUG 플러그성](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 복합 인증 설정에서 CUG 인증 모델을 제거하는 방법에 대한 자세한 내용은 설명서를 참조하십시오.

### 인증 요구 사항 비활성화 {#disable-the-authentication-requirement}

에서 제공하는 인증 요구 사항에 대한 지원을 비활성화하려면 `granite.auth.authhandler` 모듈 연결된 구성을 제거하는 것으로 충분합니다. **Adobe Granite 인증 요구 사항 및 로그인 경로 핸들러**.

>[!NOTE]
>
>단, 구성을 제거해도 믹스인 유형의 등록이 취소되지 않으며, 이는 적용되지 않고 노드에 계속 적용되었습니다.

## 다른 모듈과의 상호 작용 {#interaction-with-other-modules}

### Apache Jackrabbit API {#apache-jackrabbit-api}

CUG 인증 모델에서 사용하는 새로운 유형의 액세스 제어 정책을 반영하기 위해 Apache Jackrabbit에서 정의한 API를 확장했습니다. 버전 2.11.0 이후 `jackrabbit-api` 모듈은 라는 새 인터페이스를 정의합니다. `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, 다음을 확장함: `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Apache Jackrabbit FileVault의 가져오기 메커니즘이 유형의 액세스 제어 정책을 처리하도록 조정되었습니다 `PrincipalSetPolicy`.

### Apache Sling 컨텐츠 배포 {#apache-sling-content-distribution}

위 참조 [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) 섹션.

### Adobe Granite 복제 {#adobe-granite-replication}

다른 AEM 인스턴스 간에 CUG 정책을 복제할 수 있도록 복제 모듈이 약간 조정되었습니다.

* `DurboImportConfiguration.isImportAcl()` 는 문자 그대로 해석되며 를 구현하는 액세스 제어 정책에만 영향을 줍니다. `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` 은 true ACL에 대해서만 이 구성을 준수합니다.
* 기타 정책: `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` CUG 인증 모델로 생성된 인스턴스는 항상 복제되고 구성 옵션이 제공됩니다 `DurboImportConfiguration.isImportAcl`()은(는) 무시됩니다.

CUG 정책을 복제하는 데는 한 가지 제한이 있습니다. 해당 믹스인 노드 유형을 제거하지 않고 주어진 CUG 정책이 제거되는 경우 `rep:CugMixin,` 제거는 복제 시 반영되지 않습니다. 이 문제는 정책 제거 시 항상 mixin을 제거하여 해결되었습니다. 그러나 mixin 유형을 수동으로 추가하는 경우 제한 사항이 표시될 수 있습니다.

### Adobe Granite 인증 핸들러 {#adobe-granite-authentication-handler}

인증 핸들러 **Adobe Granite HTTP 헤더 인증 핸들러** 과 함께 제공됨 `com.adobe.granite.auth.authhandler` 번들은 `CugSupport` 동일한 모듈에서 정의된 인터페이스입니다. 특정 상황에서 &#39;영역&#39;을 계산하는 데 사용되므로 핸들러로 구성된 영역으로 돌아갑니다.

이 은(는) 을(를) 참조하도록 조정되었습니다. `CugSupport` 지정된 설정이 더 이상 사용되지 않는 구현을 다시 활성화하기로 결정하는 경우 이전 버전과의 호환성을 최대한 보장하기 위해 선택 사항입니다. 구현을 사용한 설치는 더 이상 CUG 구현에서 영역을 추출하지 않지만 로 정의된 대로 항상 영역을 표시합니다. **Adobe Granite HTTP 헤더 인증 핸들러**.

>[!NOTE]
>
>기본적으로 **Adobe Granite HTTP 헤더 인증 핸들러** 은(는) &quot;로그인 페이지 비활성화&quot;를 사용하는 게시 실행 모드에서만 구성됩니다( `auth.http.nologin`) 옵션이 활성화되었습니다.

### AEM LiveCopy {#aem-livecopy}

LiveCopy와 함께 CUG를 구성하는 것은 다음과 같이 한 개의 추가 노드와 한 개의 추가 속성을 추가하여 저장소에 표시됩니다.

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

이 두 요소는 모두 `cq:Page`. 현재 디자인에서 MSM은 아래에 있는 노드 및 속성만 처리합니다. `cq:PageContent` (`jcr:content`) 노드.

따라서 CUG 그룹은 블루프린트에서 라이브 카피로 롤아웃할 수 없습니다. Live Copy를 구성할 때 이를 염두에 두고 계획을 세우십시오.

## 새로운 CUG 구현의 변경 사항 {#changes-with-the-new-cug-implementation}

이 섹션의 목표는 CUG 기능에 대한 변경 사항에 대한 개요와 이전 및 새 구현 간의 비교를 제공하는 것입니다. CUG 지원 구성 방식에 영향을 주는 변경 사항을 나열하고 저장소 콘텐츠에서 CUG를 관리하는 방법 및 사용자를 설명합니다.

### CUG 설정 및 구성의 차이점 {#differences-in-cug-setup-and-configuration}

더 이상 사용되지 않는 OSGi 구성 요소 **Adobe Granite CUG(폐쇄형 사용자 그룹) 지원** ( `com.day.cq.auth.impl.cug.CugSupportImpl`)는 이전 CUG 기능의 인증 및 인증 관련 부분을 별도로 처리할 수 있도록 새 구성 요소로 대체되었습니다.

## 저장소 컨텐츠에서 CUG 관리의 차이점 {#differences-in-managing-cugs-in-the-repository-content}

다음 섹션에서는 구현 및 보안 관점에서 이전 구현과 새 구현 간의 차이점에 대해 설명합니다. 새로운 구현은 동일한 기능을 제공하는 것을 목표로 하지만 새로운 CUG를 사용할 때 알아야 할 미묘한 변화가 있습니다.

### 권한 부여와 관련된 차이점 {#differences-with-regards-to-authorization}

인증 관점의 주요 차이점은 아래 목록에 요약되어 있습니다.

**CUG용 전용 액세스 제어 콘텐츠**

이전 구현에서는 기본 인증 모델을 사용하여 게시에서 액세스 제어 목록 정책을 조작하고 CUG에서 지정한 설정으로 기존 ACE를 교체했습니다. 이는 게시에서 해석된 일반적이고 잔여 JCR 속성을 작성함으로써 트리거되었습니다.

새로운 구현에서는 생성, 수정 또는 제거되는 CUG의 영향을 받지 않는 기본 인증 모델의 액세스 제어 설정입니다. 대신 이라는 새로운 유형의 정책이 `PrincipalSetPolicy` 는 타겟 노드에 추가 액세스 제어 콘텐츠로 적용됩니다. 이 추가 정책은 대상 노드의 하위 노드로 배치되며, 존재하는 경우 기본 정책 노드의 형제 노드가 됩니다.

**액세스 제어 관리에서 CUG 정책 편집**

이렇게 하면 나머지 JCR 속성에서 전용 액세스 제어 정책으로 이동하면 CUG 기능의 권한 부분을 만들거나 수정하는 데 필요한 권한에 영향을 줍니다. 이는 액세스 제어 컨텐츠를 수정한 것으로 간주되므로 `jcr:readAccessControl` 및 `jcr:modifyAccessControl` 저장소에 쓸 수 있는 권한. 따라서 페이지의 액세스 제어 콘텐츠를 수정할 권한이 있는 콘텐츠 작성자만 이 콘텐츠를 설정하거나 수정할 수 있습니다. 이는 일반 JCR 속성을 작성할 수 있는 기능이 충분하여 권한이 에스컬레이션된 이전 구현과 대조됩니다.

**정책에 의해 정의된 대상 노드**

CUG 정책은 제한된 읽기 액세스를 가질 하위 트리를 정의하는 JCR 노드에 생성되어야 합니다. CUG가 전체 트리에 영향을 줄 것으로 예상되는 경우 AEM 페이지일 수 있습니다.

지정된 페이지 아래에 있는 jcr:content 노드에만 CUG 정책을 배치하면 지정된 페이지의 content s.str에 대한 액세스만 제한되지만 동위 멤버나 하위 페이지에는 적용되지 않습니다. 이는 유효한 사용 사례일 수 있으며 세분화된 액세스 콘텐츠를 적용할 수 있는 저장소 편집기로 구현할 수 있습니다. 그러나 jcr:content 노드에 cq:cugEnabled 속성을 배치하는 것이 내부적으로 페이지 노드에 다시 매핑된 이전 구현과 대조됩니다. 이 매핑은 더 이상 수행되지 않습니다.

**CUG 정책으로 권한 평가**

이전 CUG 지원에서 추가 인증 모델로 이동하여 효과적인 읽기 권한을 평가하는 방식이 변경됩니다. 에 설명된 대로 [Jackrabbit 설명서](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), 특정 주체가 볼 수 있음 `CUGcontent` oak 저장소에 구성된 모든 모델의 권한 평가에서 읽기 액세스 권한을 부여하는 경우에만 읽기 액세스 권한이 부여됩니다.

즉, 유효 권한 평가의 경우 두 가지 모두 `CUGPolicy` 또한 기본 액세스 제어 항목을 고려하여 CUG 콘텐츠에 대한 읽기 액세스 권한은 두 가지 유형의 정책에서 모두 부여된 경우에만 부여됩니다. 에 대한 읽기 권한이 완료되는 기본 AEM 게시 설치에서 `/content` 트리는 모든 사람에게 부여되며, CUG 정책의 효과는 이전 구현과 동일합니다.

**온디맨드 평가**

CUG 인증 모델을 통해 개별적으로 액세스 제어 관리 및 권한 평가를 켤 수 있습니다.

* 모듈에 CUG를 만들 수 있는 하나 이상의 지원 경로가 있는 경우 액세스 제어 관리가 활성화됩니다
* 권한 평가는 옵션인 경우에만 활성화됩니다. **CUG 평가 활성화됨** 이(가) 추가로 확인되었습니다.

CUG 정책의 새 AEM 기본 설정 평가에서는 &#39;게시&#39; 실행 모드에서만 활성화됩니다. 다음에서 세부 사항 보기 [AEM 6.3 이후 기본 구성](#default-configuration-since-aem) 을 참조하십시오. 지정된 경로에 대한 유효 정책을 콘텐츠에 저장된 정책과 비교하여 확인할 수 있습니다. CUG에 대한 권한 평가가 활성화된 경우에만 유효 정책이 표시됩니다.

위에서 설명한 대로 CUG 액세스 제어 정책은 이제 항상 콘텐츠에 저장되지만, 이러한 정책으로 인해 발생하는 유효 권한에 대한 평가는 다음과 같은 경우에만 시행됩니다. **CUG 평가 활성화됨** 가 Apache Jackrabbit Oak의 시스템 콘솔에서 켜져 있습니다. **CUG 구성** 기본적으로 &#39;게시&#39; 실행 모드에서만 활성화됩니다.

### 인증 관련 차이점 {#differences-with-regards-to-authentication}

인증과 관련된 차이점은 아래에 설명되어 있습니다.

#### 인증 요구 사항에 대한 전용 Mixin 유형 {#dedicated-mixin-type-for-authentication-requirement}

이전 구현에서 CUG의 인증 및 인증 측면이 모두 단일 JCR 속성에 의해 트리거되었습니다( `cq:cugEnabled`). 인증에 관한 한 Apache Sling Authenticator 구현에 저장된 인증 요구 사항 목록이 업데이트되었습니다. 새 구현에서 대상 노드를 전용 mixin 유형( )으로 표시하면 동일한 결과가 나옵니다. `granite:AuthenticationRequired`).

#### 로그인 경로 제외를 위한 속성 {#property-for-excluding-login-path}

mixin 유형은 다음과 같은 단일 선택적 속성을 정의합니다. `granite:loginPath`, 기본적으로 다음에 해당 `cq:cugLoginPage` 속성. 이전 구현과 달리 로그인 경로 속성은 해당 선언 노드 유형이 언급된 mixin인 경우에만 적용됩니다. mixin 유형을 설정하지 않고 해당 이름의 속성을 추가해도 효과가 없으며 로그인 경로에 대한 새 요구 사항이나 제외 사항이 인증자에게 보고되지 않습니다.

#### 인증 요구 사항에 대한 권한 {#privilege-for-authentication-requirement}

mixin 유형을 추가하거나 제거하려면 다음 작업이 필요합니다. `jcr:nodeTypeManagement` 권한이 부여되고 있습니다. 이전 구현에서 `jcr:modifyProperties` 권한은 잔여 속성을 편집하는 데 사용됩니다.

에 관한 한 `granite:loginPath` 를 사용하는 경우 속성을 추가, 수정 또는 제거하는 데 동일한 권한이 필요합니다.

#### 믹스인 유형으로 정의된 대상 노드 {#target-node-defined-by-mixin-type}

강제 로그인을 적용할 하위 트리를 정의하는 JCR 노드에 인증 요구 사항이 생성되어야 합니다. CUG가 전체 트리에 영향을 주고 새 구현에 대한 UI가 결과적으로 페이지 노드에 인증 요구 사항 믹스인 유형을 추가하는 경우 AEM 페이지일 수 있습니다.

지정된 페이지 아래에 있는 jcr:content 노드에만 CUG 정책을 배치하면 콘텐츠에 대한 액세스만 제한되지만, 페이지 노드 자체 또는 하위 페이지에는 영향을 미치지 않습니다.

유효한 시나리오일 수 있으며, 모든 노드에 믹스인을 배치할 수 있는 저장소 편집기에서 가능합니다. 그러나 이 동작은 jcr:content 노드에 cq:cugEnabled 또는 cq:cugLoginPage 속성을 배치하는 것이 궁극적으로 페이지 노드에 내부적으로 다시 매핑되는 이전 구현과 대조됩니다. 이 매핑은 더 이상 수행되지 않습니다.

#### 구성된 지원 경로 {#configured-supported-paths}

두 가지 모두 `granite:AuthenticationRequired` mixin 유형 및 granite:loginPath 속성은 다음 집합에 의해 정의된 범위 내에서만 유지됩니다. **지원되는 경로** 구성 옵션이 **Adobe Granite 인증 요구 사항 및 로그인 경로 핸들러**. 경로를 지정하지 않으면 인증 요구 사항 기능이 모두 비활성화됩니다. 이 경우 mixin 유형 및 속성은 주어진 JCR 노드에 추가되거나 설정될 때 적용됩니다.

### JCR 컨텐츠, OSGi 서비스 및 구성 매핑 {#mapping-of-jcr-content-osgi-services-and-configurations}

아래 문서는 이전 구현과 새 구현 간에 OSGi 서비스, 구성 및 저장소 컨텐츠의 포괄적인 매핑을 제공합니다.

AEM 6.3 이후 CUG 매핑

[파일 가져오기](assets/cug-mapping.pdf)

## 업그레이드 CUG {#upgrade-cug}

### 더 이상 사용되지 않는 CUG를 사용한 기존 설치 {#existing-installations-using-the-deprecated-cug}

이전 CUG 지원 구현은 더 이상 사용되지 않으며 이후 버전에서 제거됩니다. AEM 6.3 이전 버전에서 업그레이드할 때에는 새 구현으로 이동하는 것이 좋습니다.

업그레이드된 AEM 설치의 경우 CUG 구현이 하나만 활성화되어 있는지 확인하는 것이 중요합니다. 더 이상 사용되지 않는 신규 및 기존 CUG 지원의 조합은 테스트되지 않으며 원하지 않은 비헤이비어를 초래할 수 있습니다.

* 인증 요구 사항과 관련된 Sling Authenticator의 충돌
* 이전 CUG와 연결된 ACL 설정이 새 CUG 정책과 충돌하는 경우 읽기 액세스가 거부되었습니다.

### 기존 CUG 콘텐츠 마이그레이션 {#migrating-existing-cug-content}

Adobe은 새로운 CUG 구현으로 마이그레이션할 수 있는 도구를 제공합니다. 사용하려면 다음 단계를 수행하십시오.

1. 다음으로 이동 `https://<serveraddress>:<serverport>/system/console/cug-migration` 을 클릭하여 도구에 액세스합니다.
1. CUG를 확인할 루트 경로를 입력하고 **시험 실행 수행** 단추를 클릭합니다. 선택한 위치에서 전환 가능한 CUG를 검색합니다.
1. 결과를 검토한 후 **마이그레이션 수행** 단추를 클릭하여 새 구현으로 마이그레이션합니다.

>[!NOTE]
>
>문제가 발생하는 경우 다음에서 특정 로거를 설정할 수 있습니다. **디버그** 레벨 `com.day.cq.auth.impl.cug` 마이그레이션 도구의 출력을 가져옵니다. 다음을 참조하십시오 [로깅](/help/sites-deploying/configure-logging.md) 자세한 내용은 을 참조하십시오.
