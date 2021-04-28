---
title: AEM에서 닫힌 사용자 그룹
seo-title: AEM에서 닫힌 사용자 그룹
description: AEM의 닫힌 사용자 그룹에 대해 알아봅니다.
seo-description: AEM의 닫힌 사용자 그룹에 대해 알아봅니다.
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: 보안
translation-type: tm+mt
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '6886'
ht-degree: 0%

---

# AEM{#closed-user-groups-in-aem}에서 닫힌 사용자 그룹

## 소개 {#introduction}

AEM 6.3부터는 기존 구현과 관련된 성능, 확장성 및 보안 문제를 해결하기 위한 새로운 폐쇄 사용자 그룹 구현이 있습니다.

>[!NOTE]
>
>단순함을 위해 이 설명서 전체에서 CUG 약어를 사용합니다.

새로운 구현의 목표는 기존 버전의 문제점과 디자인 제한을 해결하는 동시에 필요한 기존 기능을 해결하는 것입니다. 그 결과 다음과 같은 특성을 갖는 새로운 CUG 디자인이 생성됩니다.

* 개별적으로 또는 결합하여 사용할 수 있는 인증 및 인증 요소의 명확한 분리
* 다른 액세스 제어 설정 및 권한 요구 사항에 영향을 주지 않고 구성된 CUG 트리에서 제한된 읽기 액세스를 반영하는 전용 인증 모델
* 일반적으로 작성 인스턴스 작성 시 필요한 제한된 읽기 액세스의 액세스 제어 설정과 일반적으로 게시 시에만 필요한 권한 평가 간의 분리;
* 권한 에스컬레이션 없이 제한된 읽기 액세스 편집;
* 인증 요구 사항을 표시하는 전용 노드 유형 확장;
* 인증 요구 사항과 연관된 선택적 로그인 경로입니다.

### 새 사용자 지정 사용자 그룹 구현 {#the-new-custom-user-group-implementation}

AEM 컨텍스트에서 알려진 CUG는 다음 단계로 구성됩니다.

* 보호되어야 하는 트리에서 읽기 액세스를 제한하고 주어진 CUG 인스턴스로 나열되거나 CUG 평가에서 모두 제외된 주체를 읽기 허용만 허용합니다. 이를 **authorization** 요소라고 합니다.
* 지정된 트리에 인증을 적용하고 나중에 제외되는 해당 트리에 대한 전용 로그인 페이지를 선택적으로 지정합니다. 이를 **인증** 요소라고 합니다.

새 구현은 인증과 인증 요소 사이에 선을 긋도록 설계되었습니다. AEM 6.3부터는 인증 요구 사항을 명시적으로 추가하지 않고도 읽기 액세스를 제한할 수 있습니다. 예를 들어, 지정된 인스턴스에 인증이 모두 필요하거나 지정된 트리가 이미 인증이 필요한 하위 트리에 있는 경우

또한, 유효한 권한 설정을 변경하지 않고 지정된 트리를 인증 요구 사항으로 표시할 수 있습니다. 조합과 결과는 [CUG 정책 결합 및 인증 요구 사항](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) 섹션에 나열됩니다.

## 개요 {#overview}

### 인증:읽기 액세스 제한 {#authorization-restricting-read-access}

CUG의 주요 기능은 선택한 주도자를 제외한 모든 사용자에 대해 컨텐츠 저장소의 지정된 트리에서 읽기 액세스를 제한하는 것입니다. 새로운 구현은 CUG를 나타내는 전용 액세스 제어 정책 유형을 정의하여 기본 액세스 제어 컨텐츠를 즉시 조작하는 대신 다른 접근 방식을 사용합니다.

#### CUG {#access-control-policy-for-cug}에 대한 액세스 제어 정책

이 새 정책 유형은 다음과 같은 특성을 가집니다.

* org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy 유형의 액세스 제어 정책(Apache Jackrabbit API에 의해 정의됨);
* PrincipalSetPolicy는 수정 가능한 주도자 집합에 권한을 부여합니다.
* 부여된 권한 및 정책 범위는 구현 세부 사항입니다.

CUG를 나타내는 데 사용되는 PrincipalSetPolicy 구현은 다음을 정의합니다.

* CUG 정책은 일반 JCR 항목에 대한 읽기 액세스 권한만 부여합니다(예: 액세스 제어 컨텐트는 제외됨).
* 범위는 CUG 정책을 포함하는 액세스 제어 노드에 의해 정의됩니다.
* CUG 정책은 중첩될 수 있고, 중첩된 CUG는 &#39;parent&#39; CUG의 기본 세트를 상속하지 않고 새 CUG를 시작합니다.
* 평가가 활성화된 경우 정책의 효과는 다음 중첩된 CUG로 이어지는 전체 하위 트리에 상속됩니다.

이러한 CUG 정책은 oak-authorization-cug라는 별도의 인증 모듈을 통해 AEM 인스턴스에 배포됩니다. 이 모듈에는 자체 액세스 제어 관리 및 권한 평가가 포함되어 있습니다. 즉, 기본 AEM 설정은 여러 인증 메커니즘을 결합하는 Oak 컨텐츠 저장소 구성을 제공합니다. 자세한 내용은 Apache Oak 설명서](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)의 [이 페이지를 참조하십시오.

이 복합 설정에서 새 CUG는 대상 노드에 첨부된 기존 액세스 제어 컨텐츠를 대체하지 않지만 원래 액세스 제어에 영향을 주지 않고 나중에 제거할 수 있는 보완책으로 설계되었으며 기본적으로 AEM에서는 액세스 제어 목록이 됩니다.

이전 구현과 달리 새로운 CUG 정책은 항상 액세스 제어 컨텐츠로 인식되고 처리됩니다. 이것은 JCR 액세스 제어 관리 API를 사용하여 만들고 편집함을 의미합니다. 자세한 내용은 [CUG 정책 관리](#managing-cug-policies) 섹션을 참조하십시오.

#### CUG 정책 {#permission-evaluation-of-cug-policies} 권한 평가

CUG에 대한 전용 액세스 제어 관리 외에, 새로운 인증 모델은 정책에 대한 권한 평가를 조건부로 활성화할 수 있도록 허용합니다. 이렇게 하면 스테이징 환경에서 CUG 정책을 설정할 수 있으며 프로덕션 환경에 복제한 후 효과적인 권한을 평가만 할 수 있습니다.

CUG 정책에 대한 권한 평가 및 기본값이나 추가 인증 모델과의 상호 작용은 Apache Jackrabbit Oak의 다중 인증 메커니즘을 위해 설계된 패턴을 따릅니다.모든 모델에서 액세스 권한을 부여하는 경우에만 주어진 권한 세트가 부여됩니다. 자세한 내용은 [이 페이지](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)를 참조하십시오.

다음 특성은 CUG 정책을 처리하고 평가하도록 설계된 인증 모델과 연관된 권한 평가에 적용됩니다.

* 일반 노드 및 속성에 대한 읽기 권한만 처리하지만 액세스 제어 내용을 읽지 않습니다.
* 또한 쓰기 권한이나 보호된 JCR 컨텐츠를 수정하는 데 필요한 어떠한 종류의 권한도 처리하지 않습니다(액세스 제어, 노드 유형 정보, 버전 관리, 잠금 또는 사용자 관리).이러한 권한은 CUG 정책의 영향을 받지 않으며 관련 인증 모델로 평가되지 않습니다. 이러한 권한이 부여되는지 여부는 보안 설정에 구성된 다른 모델에 따라 다릅니다.

권한 평가에 따른 단일 CUG 정책의 효과는 다음과 같이 요약할 수 있습니다.

* 본 정책에 명시된 제외 주체 또는 주도자가 포함된 항목을 제외한 모든 사용자에 대해 읽기 액세스가 거부되었습니다.
* 정책은 정책 및 해당 속성을 포함하는 액세스 제어 노드에 적용됩니다.
* 이 효과는 계층 구조(즉, 액세스 제어 노드에 의해 정의된 항목 트리)를 추가로 상속합니다.
* 그러나 액세스 제어 노드의 형제나 조상은 영향을 주지 않습니다.
* 지정된 CUG의 상속은 중첩된 CUG에서 중지됩니다.

#### 우수 사례 {#best-practices}

CUG를 통한 제한된 읽기 액세스 정의를 위해 다음 우수 사례를 고려해야 합니다.

* CUG의 필요성이 읽기 액세스를 제한하는지 또는 인증 요구 사항을 제한하는지에 대한 신중한 결정을 내릴 수 있습니다. 후자의 경우 또는 둘 다 필요할 경우, 인증 요구 사항에 대한 자세한 내용은 우수 사례 섹션을 참조하십시오.
* 위협 경계를 식별하고 데이터의 민감도와 공식 액세스와 관련된 역할에 대한 이해를 명확하게 하기 위해 보호해야 하는 데이터 또는 컨텐츠에 대한 위협 모델을 생성합니다.
* 일반적인 인증 관련 측면과 모범 사례를 고려하여 저장소 컨텐츠와 CUG를 모델링합니다.

   * 주어진 CUG와 설치 허여에 배포된 다른 모듈의 평가가 지정된 주체가 지정된 저장소 항목을 읽을 수 있도록 허용하는 경우에만 읽기 권한이 부여된다는 점을 기억하십시오
   * 다른 인증 모듈로 읽기 액세스가 이미 제한된 중복 CUG를 만들지 마십시오.
   * 중첩된 CUG에 대한 과도한 요구가 컨텐츠 디자인에서 문제를 잠재적으로 강조할 수 있습니다.
   * CUG에 대한 매우 과도한 요구 사항(예: 모든 단일 페이지에서)은 사용자 정의 인증 모델이 필요한 필요성을 나타낼 수 있으며, 이는 해당 애플리케이션과 컨텐츠의 특정 보안 요구 사항에 맞게 잠재적으로 더 적합합니다.

* CUG 정책에 대해 지원되는 경로를 저장소의 일부 트리로 제한하여 성능을 최적화할 수 있습니다. 예를 들어 AEM 6.3 이후 기본값으로 제공된 /content 노드 아래의 CUG만 허용합니다.
* CUG 정책은 소규모 주도자에 대한 읽기 액세스 권한을 부여하도록 설계되었습니다. 다수의 주관이 필요한 경우 컨텐츠 또는 애플리케이션 디자인 시 문제를 강조할 수 있으므로 다시 고려해야 합니다.

### 인증:인증 요구 사항 정의 {#authentication-defining-the-auth-requirement}

CUG 기능의 인증 관련 부분을 사용하면 인증이 필요한 트리를 표시하고 선택적으로 전용 로그인 페이지를 지정할 수 있습니다. 이전 버전에 따라 새 구현을 사용하면 컨텐츠 저장소에서 인증이 필요한 트리를 표시할 수 있고, 요구 사항을 최종적으로 적용하고 로그인 리소스로 리디렉션할 책임이 있는 `Sling org.apache.sling.api.auth.Authenticator`과의 동기화를 조건부로 활성화할 수 있습니다.

이러한 요구 사항은 `sling.auth.requirements` 등록 속성을 제공하는 OSGi 서비스를 통해 인증자에게 등록됩니다. 그런 다음 이러한 속성을 사용하여 인증 요구 사항을 동적으로 확장합니다. 자세한 내용은 [Sling 설명서](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS)를 참조하십시오.

#### 전용 믹싱 유형이 {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}인 인증 요구 사항 정의

보안상의 이유로 새 구현은 JCR 속성의 사용을 로그인 경로 `granite:loginPath`에 대해 STRING 유형의 단일 선택적 속성을 정의하는 `granite:AuthenticationRequired` 전용 믹싱 유형으로 바꿉니다. 이 혼합 유형과 관련된 컨텐츠 변경 사항만 Apache Sling Authenticator에 등록된 요구 사항을 업데이트합니다. 수정은 일시적인 수정을 지속할 때 추적되므로 `javax.jcr.Session.save()` 호출이 유효해야 합니다.

`granite:loginPath` 속성에도 동일하게 적용됩니다. 인증 요구 사항 관련 믹싱 유형으로 정의된 경우에만 적용됩니다. 구조화되지 않은 JCR 노드에서 이 이름을 가진 잔여속성을 추가하면 원하는 효과가 나타나지 않으며 OSGi 등록을 업데이트하는 핸들러에 의해 속성이 무시됩니다.

>[!NOTE]
>
>로그인 경로 속성을 설정하는 것은 선택 사항이며 인증이 필요한 트리가 기본값이나 상속된 로그인 페이지로 돌아갈 수 없는 경우에만 필요합니다. 아래의 [로그인 경로 평가](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path)를 참조하십시오.

#### 인증 요구 사항 등록 및 Sling 인증자를 사용하여 로그인 경로 등록 {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

이러한 유형의 인증 요구 사항은 특정 실행 모드 및 컨텐츠 저장소 내의 일부 트리만 제한될 수 있으므로 요구 사항 혼합 유형과 로그인 경로 속성을 추적하는 것은 조건이며 지원되는 경로를 정의하는 해당 구성에 바인딩됩니다(아래의 구성 옵션 참조). 따라서 지원되는 경로의 범위 내에서만 변경하면 OSGi 등록으로 업데이트되고 다른 부분에서는 mixin 유형과 속성이 모두 무시됩니다.

이제 기본 AEM 설정은 작성자 실행 모드에서 믹싱을 설정할 수 있도록 허용하지만 게시 인스턴스에 복제만 적용하도록 허용하여 이 구성을 사용합니다. Sling이 인증 요구 사항을 실행하는 방법에 대한 자세한 내용은 [이 페이지](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html)을 참조하십시오.

구성된 지원되는 경로 내에 `granite:AuthenticationRequired` 혼합 유형을 추가하면 `sling.auth.requirements` 속성을 사용하여 새 추가 항목이 포함된 책임 핸들러의 OSGi 등록이 업데이트됩니다. 지정된 인증 요구 사항이 선택적 `granite:loginPath` 속성을 지정하는 경우 인증 요구 사항에서 제외되도록 값이 &#39;-&#39; 접두어로 인증자에 추가로 등록됩니다.

#### 인증 요구 사항 평가 및 상속 {#evaluation-and-inheritance-of-the-authentication-requirement}

Apache Sling 인증 요구 사항은 페이지 또는 노드 계층 구조를 통해 상속되어야 합니다. 상속 및 순서 및 우선 순위와 같은 인증 요구 사항에 대한 평가에 대한 자세한 내용은 구현 세부 사항으로 간주되며 이 문서에 문서화되지 않습니다.

#### 로그인 경로 평가 {#evaluation-of-login-path}

인증 시 로그인 경로 평가 및 해당 리소스로 리디렉션되는 리디렉션은 현재 AEM으로 기본적으로 구성된 Apache Sling AuthenticationHandler인 Adobe Granite Login Selector 인증 핸들러( `com.day.cq.auth.impl.LoginSelectorHandler`)의 구현 세부 정보입니다.

`AuthenticationHandler.requestCredentials`을(를) 호출할 때 이 핸들러는 사용자를 리디렉션할 매핑 로그인 페이지를 결정합니다. 여기에는 다음 단계가 포함됩니다.

* 리디렉션의 이유로 만료된 암호와 일반 로그인 필요 간을 구분합니다.
* 정기적으로 로그인하는 경우 다음 순서로 로그인 경로를 얻을 수 있는지 테스트합니다.

   * 새 `com.adobe.granite.auth.requirement.impl.RequirementService`에 의해 구현된 LoginPathProvider에서
   * 이전, 사용되지 않는 CUG 구현,
   * 로그인 페이지 매핑에서`LoginSelectorHandler`
   * 마지막으로, `LoginSelectorHandler`에 정의된 기본 로그인 페이지로 폴백합니다.

* 위에 나열된 호출을 통해 유효한 로그인 경로를 가져오면 사용자의 요청이 해당 페이지로 리디렉션됩니다.

이 문서의 대상은 내부 `LoginPathProvider` 인터페이스에 표시되는 로그인 경로의 평가입니다. AEM 6.3 이후 제공되는 구현은 다음과 같이 작동합니다.

* 로그인 경로 등록은 만료된 암호 구분과 리디렉션 이유로 정기적인 로그인 필요 여부에 따라 다릅니다
* 정기적으로 로그인하는 경우 다음 순서로 로그인 경로를 얻을 수 있는지 테스트합니다.

   * 새 `com.adobe.granite.auth.requirement.impl.RequirementService`에 의해 구현된 `LoginPathProvider`에서
   * 이전, 사용되지 않는 CUG 구현,
   * 을 사용하여 `LoginSelectorHandler`,
   * 마지막으로 `LoginSelectorHandler`에 정의된 기본 로그인 페이지로 폴백합니다.

* 위에 나열된 호출을 통해 유효한 로그인 경로를 가져오면 사용자의 요청이 해당 페이지로 리디렉션됩니다.

Granite의 새로운 인증 요구 사항 지원에 의해 구현된 `LoginPathProvider`은(는) 위에서 설명한 대로 혼합 유형에 의해 정의된 로그인 경로를 표시합니다. `granite:loginPath` 로그인 경로와 속성 값 자체를 포함하는 리소스 경로의 매핑은 메모리에 보관되며 계층 구조의 다른 노드에 적합한 로그인 경로를 찾기 위해 평가됩니다.

>[!NOTE]
>
>평가는 구성된 지원 경로에 있는 리소스와 연결된 요청에 대해서만 수행됩니다. 다른 요청의 경우 로그인 경로를 결정하는 대체 방법이 평가됩니다.

#### 우수 사례 {#best-practices-1}

인증 요구 사항을 정의할 때는 다음 우수 사례를 고려해야 합니다.

* 중첩 인증 요구 사항 방지:트리 시작 부분에 단일 인증 요구 사항 표시자를 배치해도 충분하며 대상 노드에서 정의한 전체 하위 트리에 상속됩니다. 해당 트리 내의 추가 인증 요구 사항은 중복으로 간주되어야 하며 Apache Sling 내의 인증 요구 사항을 평가하는 동안 성능 문제가 발생할 수 있습니다. 인증 및 인증 관련 CUG 영역이 분리되어 있으면 전체 트리에 대한 인증을 적용하면서 CUG 또는 다른 유형의 정책을 통해 읽기 액세스를 제한할 수 있습니다.
* 인증 요구 사항이 요구 사항에서 중첩된 하위 트리를 다시 제외하지 않고도 전체 트리에 대한 인증 요구 사항이 적용되도록 하는 모델 리포지토리 컨텐츠
* 중복 로그인 경로를 지정하고 이후에 등록하지 않도록 하려면:

   * 상속을 사용하고 중첩 로그인 경로를 정의하지 마십시오.
   * 선택적 로그인 경로를 기본값 또는 상속된 값에 해당하는 값으로 설정하지 마십시오.
   * 응용 프로그램 개발자는 `LoginSelectorHandler`과(와) 연관된 전역 로그인 경로 구성(기본 및 매핑 모두)에 구성해야 할 로그인 경로를 식별해야 합니다.

## 보관소의 표현 {#representation-in-the-repository}

### 보관소의 CUG 정책 표현 {#cug-policy-representation-in-the-repository}

Oak 설명서는 새 CUG 정책이 저장소 컨텐츠에 어떻게 반영되는지 설명합니다. 자세한 내용은 [이 페이지](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository)를 참조하십시오.

### 보관소의 인증 요구 사항 {#authentication-requirement-in-the-repository}

별도의 인증 요구 사항에 대한 필요는 대상 노드에 전용 믹싱 노드 유형을 배치하여 저장소 컨텐츠에 반영됩니다. mixin 유형은 대상 노드가 정의하는 트리의 전용 로그인 페이지를 지정하는 선택적 속성을 정의합니다.

로그인 경로와 연관된 페이지는 해당 트리 내부 또는 외부에 있을 수 있습니다. 인증 요구 사항에서 제외됩니다.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## CUG 정책 및 인증 요구 사항 관리 {#managing-cug-policies-and-authentication-requirement}

### CUG 정책 관리 {#managing-cug-policies}

CUG에 대한 읽기 액세스를 제한하는 새로운 유형의 액세스 제어 정책은 JCR 액세스 제어 관리 API를 사용하여 관리되며 [JCR 2.0 사양](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html)에 설명된 메커니즘을 따릅니다.

#### 새 CUG 정책 {#set-a-new-cug-policy} 설정

이전에 CUG가 설정되지 않은 노드에 새 CUG 정책을 적용하는 코드. `getApplicablePolicies`은(는) 이전에 설정되지 않은 새 정책만 반환합니다. 결국 정책을 다시 기록해야 하고 변경 사항을 지속해야 한다.

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
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### 기존 CUG 정책 {#edit-an-existing-cug-policy} 편집

기존 CUG 정책을 편집하려면 다음 단계가 필요합니다. 수정된 정책은 다시 기록해야 하며 변경 사항은 `javax.jcr.Session.save()`을(를) 사용하여 지속해야 합니다.

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

### 유효한 CUG 정책 검색 {#retrieve-effective-cug-policies}

JCR 액세스 제어 관리는 지정된 경로에서 적용되는 정책을 검색하기 위한 최상의 작업 방법을 정의합니다. CUG 정책 평가가 조건적이며 활성화할 해당 구성에 따라 다르므로 `getEffectivePolicies`을(를) 호출하면 지정된 설치 환경에서 해당 CUG 정책이 적용되는지 확인하는 편리한 방법입니다.

>[!NOTE]
>
>지정된 경로가 이미 기존 CUG의 일부인지 확인하기 위해 계층 구조를 표시하는 `getEffectivePolicies`과(와) 이후의 코드 예제의 차이를 참고하십시오.

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

적용 여부에 관계없이 지정된 경로에 정의된 중첩된 모든 CUG를 찾습니다. 자세한 내용은 [구성 옵션](/help/sites-administering/closed-user-groups.md#configuration-options) 섹션을 참조하십시오.

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

#### Pincipal {#managing-cug-policies-by-pincipal}별 CUG 정책 관리

CUG 정책은 항상 모든 주체에 영향을 주므로, 주체별 액세스 제어 정책을 편집할 수 있도록 `JackrabbitAccessControlManager`에서 정의한 확장명은 CUG 액세스 제어 관리에서 구현되지 않습니다.`PrincipalSetPolicy`에 나열된 항목에는 읽기 액세스 권한이 부여되지만 다른 모든 주체는 대상 노드에서 정의한 트리의 컨텐츠를 읽을 수 없습니다.

해당 메서드는 항상 빈 정책 배열을 반환하지만 예외를 throw하지 않습니다.

### 인증 요구 사항 관리 {#managing-the-authentication-requirement}

대상 노드의 유효한 노드 유형을 변경하여 새로운 인증 요구 사항을 생성, 수정 또는 제거할 수 있습니다. 그런 다음 일반 JCR API를 사용하여 선택적 로그인 경로 속성을 작성할 수 있습니다.

>[!NOTE]
>
>위에 언급된 특정 대상 노드의 수정 사항은 `RequirementHandler`이(가) 구성되고 대상이 지원되는 경로로 정의된 트리에 포함된 경우에만 Apache Sling Authenticator에 반영됩니다(구성 옵션 섹션 참조).
>
>자세한 내용은 [Assigning Mixin 노드 유형 지정](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Mixin 노드 유형 지정) 및 [노드 추가 및 속성 설정](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 노드 추가 및 속성 설정)을 참조하십시오.

#### 새 인증 요구 사항 추가 {#adding-a-new-auth-requirement}

새 인증 요구 사항을 만드는 단계는 아래에 자세히 설명되어 있습니다. 대상 노드를 포함하는 트리에 대해 `RequirementHandler`이(가) 구성된 경우 요구 사항은 Apache Sling Authenticator에만 등록됩니다.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### 로그인 경로 {#add-a-new-auth-requirement-with-login-path}에 새 인증 요구 사항 추가

로그인 경로를 포함하여 새 인증 요구 사항을 만드는 절차. 참고: `RequirementHandler`이(가) 대상 노드를 포함하는 트리에 대해 구성된 경우 로그인 경로에 대한 요구 사항 및 제외는 Apache Sling Authenticator에만 등록됩니다.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### 기존 로그인 경로 수정 {#modify-an-existing-login-path}

기존 로그인 경로를 변경하는 단계는 아래에 자세히 설명되어 있습니다. 수정 사항은 대상 노드를 포함하는 트리에 대해 `RequirementHandler`이(가) 구성된 경우에만 Apache Sling Authenticator에 등록됩니다. 이전 로그인 경로 값이 등록에서 제거됩니다. 대상 노드와 연관된 인증 요구 사항은 이 수정으로 영향을 받지 않습니다.

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

기존 로그인 경로를 제거하는 절차. 대상 노드를 포함하는 트리에 대해 `RequirementHandler`이(가) 구성된 경우 로그인 경로 항목은 Apache Sling Authenticator에서 등록되지 않습니다. 대상 노드와 연관된 인증 요구 사항은 영향을 받지 않습니다.

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

또는 아래 방법을 사용하여 동일한 목적을 달성할 수 있습니다.

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

기존 인증 요구 사항을 제거하는 절차. 대상 노드를 포함하는 트리에 대해 `RequirementHandler`이(가) 구성된 경우 Apache Sling Authenticator에서 이 요구 사항이 등록되지 않습니다.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### 유효한 인증 요구 사항 검색 {#retrieve-effective-auth-requirements}

Apache Sling Authenticator에 등록된 모든 효과적인 인증 요구 사항을 읽을 수 있는 전용 공개 API는 없습니다. 그러나 목록은 &quot;**인증 요구 사항 구성**&quot; 섹션 아래의 `https://<serveraddress>:<serverport>/system/console/slingauth`의 시스템 콘솔에 표시됩니다.

다음 이미지는 데모 컨텐츠가 있는 AEM 게시 인스턴스의 인증 요구 사항을 보여줍니다. 커뮤니티 페이지의 강조 표시된 경로는 이 문서에 설명된 구현에 의해 추가된 요구 사항이 Apache Sling 인증자에 어떻게 반영되는지 보여줍니다.

>[!NOTE]
>
>이 예에서 선택적 로그인 경로 속성이 설정되지 않았습니다. 따라서 인증자에게 두 번째 항목이 등록되지 않았습니다.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### 유효 로그인 경로 {#retrieve-the-effective-login-path} 검색

현재 인증이 필요한 리소스에 익명으로 액세스할 때 적용되는 로그인 경로를 검색할 공개 API가 없습니다. 로그인 경로가 검색되는 방식에 대한 구현 세부 사항은 로그인 경로 평가 섹션을 참조하십시오.

그러나 이 기능에 정의된 로그인 경로 외에, 컨텐츠 모델을 디자인할 때와 지정된 AEM 설치의 인증 요구 사항을 고려할 때 로그인으로 리디렉션할 수 있는 다른 방법이 있습니다.

#### 상속된 인증 요구 사항 검색 {#retrieve-the-inherited-auth-requirement}

로그인 경로와 마찬가지로 컨텐츠에 정의된 상속된 인증 요구 사항을 검색할 공개 API가 없습니다. 다음 샘플에서는 해당 계층에 정의된 모든 인증 요구 사항을 적용 여부와 관계없이 나열하는 방법을 보여 줍니다. 자세한 내용은 [구성 옵션](/help/sites-administering/closed-user-groups.md#configuration-options)을 참조하십시오.

>[!NOTE]
>
>인증 요구 사항과 로그인 경로에 상속 메커니즘에 의존하여 중첩된 인증 요구 사항을 만들지 않는 것이 좋습니다.
>
>자세한 내용은 [인증 요구 사항의 평가 및 상속](#evaluation-and-inheritance-of-the-authentication-requirement), [로그인 경로 평가](#evaluation-of-login-path) 및 [우수 사례](#best-practices)를 참조하십시오.

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

### CUG 정책과 인증 요구 사항 결합 {#combining-cug-policies-and-the-authentication-requirement}

다음 표는 구성을 통해 두 모듈을 모두 활성화한 AEM 인스턴스에서 CUG 정책의 유효한 조합과 인증 요구 사항을 나열합니다.

| **인증 필요** | **로그인 경로** | **제한된 읽기 액세스** | **예상 효과** |
|---|---|---|---|
| 예 | 예 | 예 | 유효한 권한 평가가 액세스 권한을 부여하는 경우 지정된 사용자는 CUG 정책으로 표시된 하위 트리만 볼 수 있습니다. 인증되지 않은 사용자는 지정된 로그인 페이지로 리디렉션됩니다. |
| 예 | 아니오 | 예 | 유효한 권한 평가가 액세스 권한을 부여하는 경우 지정된 사용자는 CUG 정책으로 표시된 하위 트리만 볼 수 있습니다. 인증되지 않은 사용자는 상속된 기본 로그인 페이지로 리디렉션됩니다. |
| 예 | 예 | 아니오 | 인증되지 않은 사용자는 지정된 로그인 페이지로 리디렉션됩니다. 인증 요구 사항으로 표시된 트리를 볼 수 있는지 여부는 해당 하위 트리에 포함된 개별 항목의 유효 권한에 따라 다릅니다. 읽기 액세스를 제한하는 전용 CUG가 없습니다. |
| 예 | 아니오 | 아니오 | 인증되지 않은 사용자는 상속된 기본 로그인 페이지로 리디렉션됩니다. 인증 요구 사항으로 표시된 트리를 볼 수 있는지 여부는 해당 하위 트리에 포함된 개별 항목의 유효 권한에 따라 다릅니다. 읽기 액세스를 제한하는 전용 CUG가 없습니다. |
| 아니오 | 아니오 | 예 | 인증된 지정된 사용자 또는 인증되지 않은 사용자는 유효한 권한 평가를 통해 액세스 권한을 부여하는 경우 CUG 정책으로 표시된 하위 트리만 볼 수 있습니다. 인증되지 않은 사용자는 동일하게 취급되고 로그인으로 리디렉션되지 않습니다. |

>[!NOTE]
>
>&#39;인증 요구 사항&#39; = 아니요 및 &#39;로그인 경로&#39; = [예]의 조합이 위에 표시되지 않습니다. &#39;로그인 경로&#39;는 인증 요구 사항과 연관된 선택적 속성입니다. 정의 mixin 유형을 추가하지 않고 해당 이름으로 JCR 속성을 지정하면 아무런 효과가 없으며 해당 처리기에서 무시됩니다.

## OSGi 구성 요소 및 구성 {#osgi-components-and-configuration}

이 섹션에서는 OSGi 구성 요소에 대한 개요와 새로운 CUG 구현에 도입된 개별 구성 옵션에 대한 개요를 제공합니다.

이전 버전과 새 구현 간의 구성 옵션에 대한 포괄적인 매핑은 CUG 매핑 설명서를 참조하십시오.

### 인증:설정 및 구성 {#authorization-setup-and-configuration}

새로운 인증 관련 부분은 AEM 기본 설치의 일부인 **Oak CUG 인증** 번들( `org.apache.jackrabbit.oak-authorization-cug`)에 포함되어 있습니다. 번들은 읽기 액세스를 관리하는 추가 방법으로 배포하려는 분리된 인증 모델을 정의합니다.

#### CUG 인증 설정 {#setting-up-cug-authorization}

CUG 인증 설정은 [관련 Apache 설명서](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)에 자세히 설명되어 있습니다. 기본적으로 AEM에는 모든 실행 모드에 배포되는 CUG 인증이 있습니다. 단계별 지침은 다른 인증 설정이 필요한 설치에서 CUG 인증을 비활성화하는 데 사용할 수도 있습니다.

#### 레퍼러 필터 구성 {#configuring-the-referrer-filter}

또한 AEM 액세스에 사용할 수 있는 모든 호스트 이름으로 [Sling 레퍼러 필터](/help/sites-administering/security-checklist.md#the-sling-referrer-filter)를 구성해야 합니다.예를 들어, CDN, 부하 균형 조정기 등을 통해 제공됩니다.

레퍼러 필터가 구성되지 않은 경우, 사용자가 CUG 사이트에 로그인을 시도하면 다음과 유사한 오류가 표시됩니다.

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### OSGi 구성 요소 {#characteristics-of-osgi-components} 특성

인증 요구 사항을 정의하고 전용 로그인 경로를 지정하기 위해 다음 2개의 OSGi 구성 요소가 도입되었습니다.

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
   <td>CUG 권한을 설정 및 평가하는 데 사용되는 인증 구성</td>
  </tr>
  <tr>
   <td>구성 속성</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>또한 아래 <a href="#configuration-options">구성 옵션</a>을 참조하십시오.</p> </td>
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
   <td>CUG 평가에서 변환된 이름이 있는 주체를 제외시킬 수 있습니다.</td>
  </tr>
  <tr>
   <td>구성 속성</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>아래의 구성 옵션 섹션을 참조하십시오.</p> </td>
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

* `cugSupportedPaths`:CUG를 포함할 수 있는 하위 트리를 지정합니다. 기본값이 설정되지 않음
* `cugEnabled`:구성 옵션을 사용하여 현재 CUG 정책에 대한 권한 평가를 활성화합니다.

CUG 인증 모듈과 연관된 사용 가능한 구성 옵션이 나열되며 자세한 내용은 [Apache Oak 설명서](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration)에서 자세히 설명합니다.

#### CUG 평가에서 주도자 제외 {#excluding-principals-from-cug-evaluation}

개별 주도자에 대한 CUG 평가 면제는 이전 구현에서 채택되었습니다. 새로운 CUG 권한 부여에서는 CugExclude라는 전용 인터페이스를 통해 이 문제를 다룹니다. Apache Jackrabbit Oak 1.4는 기본 구현과 개별 사용자 이름을 구성할 수 있는 확장된 구현 및 고정된 주도자 집합을 제외합니다. 후자는 AEM 게시 인스턴스에 구성됩니다.

AEM 6.3에서는 다음 주체가 CUG 정책에 영향을 받지 않으므로 기본값이 됩니다.

* 관리 주체(관리자 사용자, 관리자 그룹)
* 서비스 사용자 관리자
* 저장소 내부 시스템 주체

자세한 내용은 아래의 [AEM 6.3 이후의 기본 구성](#default-configuration-since-aem) 섹션에 있는 표를 참조하십시오.

&#39;관리자&#39; 그룹의 제외는 시스템 콘솔에서 **Apache Jackrabbit Oak CUG 제외 목록**&#x200B;의 구성 섹션에 있는 변경 또는 확장할 수 있습니다.

또는 CugExclude 인터페이스의 사용자 지정 구현을 제공하고 배포하여 특별한 필요가 있을 경우 제외된 주도자 집합을 조정할 수 있습니다. 자세한 내용 및 예제 구현은 [CUG 플러그인](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability)에 대한 설명서를 참조하십시오.

### 인증:설정 및 구성 {#authentication-setup-and-configuration}

새 인증 관련 부분은 **Adobe Granite Authentication Handler** 번들( `com.adobe.granite.auth.authhandler` 버전 5.6.48)에 포함되어 있습니다. 이 번들은 AEM 기본 설치의 일부입니다.

더 이상 사용되지 않는 CUG 지원에 대한 인증 요구 사항 교체를 설정하려면 특정 AEM 설치 시 일부 OSGi 구성 요소가 있어야 하며 활성화되어 있어야 합니다. 자세한 내용은 아래의 **OSGi 구성 요소의 특성**&#x200B;을 참조하십시오.

>[!NOTE]
>
>RequirementsHandler의 필수 구성 옵션으로 인해 인증 관련 부분은 지원되는 경로 집합을 지정하여 기능이 활성화된 경우에만 활성화됩니다. 표준 AEM 설치에서는 작성 실행 모드에서 기능이 비활성화되고 게시 실행 모드에서 /content에 대해 활성화됩니다.

**OSGi 컴포넌트의 특성**

다음 2개의 OSGi 구성 요소가 인증 요구 사항을 정의하고 전용 로그인 경로를 지정하기 위해 도입되었습니다.

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirements.impl.RequirementsService**

<table>
 <tbody>
  <tr>
   <td>레이블</td>
   <td>-</td>
  </tr>
  <tr>
   <td>설명</td>
   <td>인증 요구 사항(<code>granite:AuthenticationRequirement</code> 혼합 유형을 통해)에 영향을 주는 컨텐츠 변경 사항을 옵저버에게 등록하는 인증 요구 사항에 대한 전용 OSGi 서비스와 함께 로그인 경로가 <code>LoginSelectorHandler</code>에 노출됩니다. </td>
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

**com.adobe.granite.auth.requirements.impl.DefaultRequirementsHandler**

| 레이블 | Adobe Granite 인증 요구 사항 및 로그인 경로 처리기 |
|---|---|
| 설명 | `RequirementHandler` 구현 - Apache Sling 인증 요구 사항 및 관련 로그인 경로에 대한 해당 제외를 업데이트합니다. |
| 구성 속성 | `supportedPaths` |
| 구성 정책 | `ConfigurationPolicy.REQUIRE` |
| 참조 | NA |

#### 구성 옵션 {#configuration-options-1}

CUG 다시 작성의 인증 관련 부분은 Adobe Granite Authentication Requirements 및 로그인 경로 핸들러와 연결된 단일 구성 옵션에만 제공됩니다.

**&quot;인증 요구 사항 및 로그인 경로 처리기&quot;**

<table>
 <tbody>
  <tr>
   <td>속성</td>
   <td>유형</td>
   <td>기본 값</td>
   <td>설명</td>
  </tr>
  <tr>
   <td><p>Label = 지원되는 경로</p> <p>이름 = 'supportedPaths'</p> </td>
   <td>&lt;문자열&gt; 설정</td>
   <td>-</td>
   <td>이 처리기가 인증 요구 사항을 준수하도록 하는 경로입니다. 노드(예: 작성자 인스턴스의 경우)를 강제 적용하지 않고 노드에 <code>granite:AuthenticationRequirement</code> 혼합 유형을 추가하려는 경우 이 구성을 설정이 해제되도록 하십시오. 없는 경우 이 기능은 비활성화됩니다. </td>
  </tr>
 </tbody>
</table>

## AEM 6.3 {#default-configuration-since-aem} 이후의 기본 구성

AEM의 새로운 설치에서는 기본적으로 CUG 기능의 인증 및 인증 관련 부분 모두에 새 구현을 사용합니다. 이전 구현 &quot;CUG(Adobe Granite Closed User Group) Support&quot;는 더 이상 사용되지 않으며, 기본적으로 모든 AEM 설치에서 비활성화됩니다. 대신 새 구현이 다음과 같이 활성화됩니다.

### 작성자 인스턴스 {#author-instances}

| **&quot;Apache Jackrabbit Oak CUG 구성&quot;** | **설명** |
|---|---|
| 지원되는 경로 `/content` | CUG 정책에 대한 액세스 제어 관리가 활성화되어 있습니다. |
| CUG 평가 활성화 FALSE | 권한 평가를 사용할 수 없습니다. CUG 정책은 효과적이지 않습니다. |
| 등급 | 200 | Oak 설명서를 참조하십시오. |

>[!NOTE]
>
>기본 제작 인스턴스에 **Apache Jackrabbit Oak CUG 제외 목록** 및 **Adobe Granite 인증 요구 사항 및 로그인 경로 처리기**&#x200B;에 대한 구성이 없습니다.

### 게시 인스턴스 {#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG 구성&quot;** | **설명** |
|---|---|
| 지원되는 경로 `/content` | CUG 정책에 대한 액세스 제어 관리가 구성된 경로 아래에서 활성화됩니다. |
| CUG 평가 활성화 TRUE | 권한 평가는 구성된 경로 아래에서 활성화됩니다. CUG 정책은 `Session.save()`에 적용됩니다. |
| 등급 | 200년 | Oak 설명서를 참조하십시오. |

| **&quot;Apache Jackrabbit Oak CUG Exclude List&quot;** | **설명** |
|---|---|
| 주체 이름 관리자 | CUG 평가에서 관리자 주체를 제외합니다. |

| **&quot;Adobe Granite 인증 요구 사항 및 로그인 경로 처리기&quot;** | **설명** |
|---|---|
| 지원되는 경로 `/content` | `granite:AuthenticationRequired` 혼합 유형을 통해 저장소에 정의된 인증 요구 사항은 `Session.save()`에 `/content` 아래로 적용됩니다. Sling Authenticator가 업데이트됩니다. 지원되는 경로의 외부에 혼합 유형을 추가하는 것은 무시됩니다. |

## CUG 인증 및 인증 요구 사항 {#disabling-cug-authorization-and-authentication-requirement} 비활성화

특정 설치에서 CUG를 사용하지 않거나 인증 및 인증에 다른 방법을 사용하는 경우 새 구현을 모두 사용할 수 없습니다.

### CUG 인증 사용 안 함 {#disable-cug-authorization}

합성 인증 설정에서 CUG 인증 모델을 제거하는 방법에 대한 자세한 내용은 [CUG 플러그인](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) 설명서를 참조하십시오.

### 인증 요구 사항 {#disable-the-authentication-requirement} 비활성화

`granite.auth.authhandler` 모듈에서 제공하는 인증 요구 사항에 대한 지원을 비활성화하려면 **Adobe Granite 인증 요구 사항 및 로그인 경로 처리기**&#x200B;과(와) 연관된 구성을 제거하기에 충분합니다.

>[!NOTE]
>
>그러나 구성을 제거하면 영향을 받지 않고 노드에 적용할 수 있는 혼합 유형이 등록 취소되지 않습니다.

## 다른 모듈 {#interaction-with-other-modules}과의 상호 작용

### Apache Jackrabbit API {#apache-jackrabbit-api}

CUG 인증 모델에서 사용되는 새로운 유형의 액세스 제어 정책을 반영하기 위해 Apache Jackrabbit에서 정의한 API가 확장되었습니다. `jackrabbit-api` 모듈 버전 2.11.0에서는 `javax.jcr.security.AccessControlPolicy`부터 확장되는 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`라는 새 인터페이스를 정의합니다.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Apache Jackrabbit FileVault의 가져오기 메커니즘이 `PrincipalSetPolicy` 유형의 액세스 제어 정책을 처리하도록 조정되었습니다.

### Apache Sling 콘텐츠 배포 {#apache-sling-content-distribution}

위의 [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) 섹션을 참조하십시오.

### Adobe Granite Replication {#adobe-granite-replication}

다른 AEM 인스턴스 간에 CUG 정책을 복제할 수 있도록 복제 모듈이 약간 조정되었습니다.

* `DurboImportConfiguration.isImportAcl()` 문자 그대로 해석되며,  `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` true ACL에 대해서만 이 구성을 준수합니다.
* CUG 인증 모델에서 생성된 `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` 인스턴스와 같은 다른 정책은 항상 복제되고 구성 옵션 `DurboImportConfiguration.isImportAcl`()은 무시됩니다.

CUG 정책 복제에는 하나의 제한이 있습니다. 해당 믹싱 노드 유형 `rep:CugMixin,`을(를) 제거하지 않고 지정된 CUG 정책이 제거되면 제거가 복제 시 반영되지 않습니다. 정책 제거 시 항상 믹싱을 제거하여 이러한 문제를 해결했습니다. 그러나 mixin 유형을 수동으로 추가하는 경우에는 제한이 나타날 수 있습니다.

### Adobe Granite 인증 처리기 {#adobe-granite-authentication-handler}

`com.adobe.granite.auth.authhandler` 번들과 함께 제공되는 인증 핸들러 **Adobe Granite HTTP 헤더 인증 핸들러**&#x200B;에는 동일한 모듈에서 정의한 `CugSupport` 인터페이스에 대한 참조가 들어 있습니다. 처리기로 구성된 영역으로 넘어가면서 특정 상황에서 &#39;영역&#39;을 계산하는 데 사용됩니다.

이 옵션은 `CugSupport`에 대한 참조를 선택 항목으로 지정하여, 지정된 설정에서 더 이상 사용되지 않는 구현을 다시 활성화하기로 결정할 경우 역호환성을 최대한 보장하기 위해 조정되었습니다. 구현을 사용한 설치는 더 이상 CUG 구현에서 추출된 영역을 가져오지 않지만 항상 **Adobe Granite HTTP 헤더 인증 핸들러**&#x200B;로 정의된 영역을 표시합니다.

>[!NOTE]
>
>기본적으로 **Adobe Granite HTTP Header Authentication Handler**&#x200B;은 &quot;로그인 페이지 비활성화&quot;( `auth.http.nologin`) 옵션이 활성화된 게시 실행 모드에서만 구성됩니다.

### AEM LiveCopy {#aem-livecopy}

LiveCopy와 함께 CUG를 구성하는 작업은 다음과 같이 추가 노드 1개와 추가 속성 1개를 추가하여 저장소에 표시됩니다.

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

이 두 요소는 모두 `cq:Page` 아래에 만들어집니다. 현재 디자인을 사용하는 경우 MSM은 `cq:PageContent`(`jcr:content`) 노드 아래에 있는 노드 및 속성만 처리합니다.

따라서 Blueprint에서 CUG 그룹을 Live Copy로 롤아웃할 수 없습니다. Live Copy를 구성할 때 이 사항에 대해 계획하십시오.

## 새 CUG 구현의 변경 사항 {#changes-with-the-new-cug-implementation}

이 섹션의 목적은 CUG 기능에 대한 변경 사항에 대한 개요와 이전 버전과 새 구현 간의 비교를 제공하는 것입니다. 여기에는 CUG 지원 구성 방식에 영향을 주는 변경 사항이 나열되며 저장소 컨텐츠에서 CUG를 관리하는 방법과 그에 따른 변경 사항이 설명되어 있습니다.

### CUG 설정 및 구성 {#differences-in-cug-setup-and-configuration} 차이점

사용되지 않는 OSGi 구성 요소 **Adobe CUG(Granite Closed User Group) 지원**( `com.day.cq.auth.impl.cug.CugSupportImpl`)이 이전 CUG 기능의 인증 및 인증 관련 부분을 별도로 처리할 수 있도록 새 구성 요소로 대체되었습니다.

## 저장소 컨텐츠 {#differences-in-managing-cugs-in-the-repository-content}에서 CUG 관리의 차이점

다음 섹션에서는 이전 구현과 새 구현과 구현 및 보안 관점에서 차이가 있는지 설명합니다. 새로운 구현은 동일한 기능을 제공하려고 하지만 새로운 CUG를 사용할 때 알아야 할 미묘한 차이가 있습니다.

### 인증 {#differences-with-regards-to-authorization}과(와) 관련된 차이점

인증 관점에서의 주요 차이점은 아래 목록에 요약되어 있습니다.

**CUG용 전용 액세스 제어 컨텐츠**

이전 구현에서는 기본 인증 모델이 게시 시 액세스 제어 목록 정책을 조작하는 데 사용되었으며 CUG에서 지정한 설정으로 기존 ACE를 대체합니다. 이는 게시에 해석된 영구 잔존 JCR 속성을 작성하여 트리거되었습니다.

새로운 구현을 통해 기본 인증 모델의 액세스 제어 설정은 작성, 수정 또는 제거되는 CUG의 영향을 받지 않습니다. 대신 `PrincipalSetPolicy`이라는 새 유형의 정책이 대상 노드에 대한 추가 액세스 제어 컨텐츠로 적용됩니다. 이 추가 정책은 대상 노드의 자식으로 위치하며, 있을 경우 기본 정책 노드의 동위가 됩니다.

**액세스 제어 관리에서 CUG 정책 편집**

이러한 이동은 CUG 기능의 인증 부분을 만들거나 수정하는 데 필요한 권한에 영향을 줍니다. 이는 제어 컨텐츠에 대한 액세스를 수정하는 것으로 간주되므로 저장소에 기록하려면 `jcr:readAccessControl` 및 `jcr:modifyAccessControl` 권한이 필요합니다. 따라서 페이지의 액세스 제어 컨텐츠를 수정할 수 있는 컨텐츠 작성자만 이 컨텐츠를 설정하거나 수정할 수 있습니다. 이는 일반 JCR 속성을 작성할 수 있는 기능이 충분하여 권한 에스컬레이션 문제가 발생한 이전 구현과 대비됩니다.

**정책에 의해 정의된 Target 노드**

CUG 정책은 제한된 읽기 액세스가 적용될 하위 트리를 정의하는 JCR 노드에서 작성되어야 합니다. CUG가 트리 전체에 영향을 줄 것으로 예상되는 경우 AEM 페이지가 될 수 있습니다.

CUG 정책을 지정된 페이지 아래에 있는 jcr:content 노드에만 배치하면 지정된 페이지의 컨텐츠 s.str에 대한 액세스 권한만 제한되지만 형제 페이지 또는 하위 페이지에는 적용되지 않습니다. 이것은 유효한 사용 사례이며, 세부적으로 분류된 액세스 컨텐츠 컨텐츠를 적용할 수 있는 저장소 편집기를 사용할 수 있습니다. 하지만, 이것은 jcr:content 노드에 cq:cugEnabled 속성을 배치하는 이전 구현이 내부적으로 페이지 노드에 다시 매핑되는 것과 대비가 됩니다. 이 매핑은 더 이상 수행되지 않습니다.

**CUG 정책을 사용한 권한 평가**

이전 CUG 지원에서 추가 인증 모델로 이동하면 효과적인 읽기 권한이 평가되는 방식이 변경됩니다. [Jackrabbit 설명서](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html)에 설명된 대로, Oak 저장소에 구성된 모든 모델의 권한 평가가 읽기 액세스 권한을 부여하는 경우에만 `CUGcontent`을(를) 볼 수 있는 지정된 주체에 읽기 액세스 권한이 부여됩니다.

즉, 유효한 권한을 평가하기 위해 `CUGPolicy` 및 기본 액세스 제어 항목을 모두 고려하며 CUG 컨텐츠에 대한 읽기 액세스 권한은 두 가지 정책 유형에 의해 부여되는 경우에만 부여됩니다. 전체 `/content` 트리에 대한 읽기 액세스 권한이 모든 사람에게 부여된 기본 AEM 게시 설치에서 CUG 정책의 효과는 이전 구현과 동일합니다.

**주문형 평가**

CUG 인증 모델을 사용하면 액세스 제어 관리 및 권한 평가를 개별적으로 설정할 수 있습니다.

* CUG를 만들 수 있는 지원되는 경로가 하나 이상 있는 경우 액세스 제어 관리가 활성화됩니다
* 권한 평가는 **CUG 평가 활성화** 옵션이 추가로 선택된 경우에만 활성화됩니다.

CUG 정책의 새로운 AEM 기본 설정 평가에서는 &#39;게시&#39; 실행 모드에서만 사용할 수 있습니다. 자세한 내용은 AEM 6.3](#default-configuration-since-aem)이후의 기본 구성에 대한 세부 사항을 참조하십시오. [ 지정된 경로에 대한 효과적인 정책을 컨텐츠에 저장된 정책과 비교하여 확인할 수 있습니다. 유효한 정책은 CUG에 대한 권한 평가가 활성화된 경우에만 표시됩니다.

위에서 설명한 바와 같이 CUG 액세스 제어 정책은 이제 항상 컨텐츠에 저장되지만, 이러한 정책으로 인한 유효 권한에 대한 평가는 **CUG 평가 활성화**&#x200B;가 Apache Jackrabbit Oak **CUG Configuration의 시스템 콘솔에서 켜져 있는 경우에만 적용됩니다.** 기본적으로 &#39;게시&#39; 실행 모드에서만 활성화됩니다.

### 인증 {#differences-with-regards-to-authentication}과(와) 관련된 차이점

인증 관련 기본 사항은 아래에 설명되어 있습니다.

#### 인증 요구 사항에 대한 전용 믹싱 유형 {#dedicated-mixin-type-for-authentication-requirement}

이전 구현에서 CUG의 인증 및 인증 양상은 단일 JCR 속성( `cq:cugEnabled`)에 의해 트리거되었습니다. 인증에 관한 한 Apache Sling Authenticator 구현에 저장된 인증 요구 사항 목록이 업데이트되었습니다. 새 구현을 사용하면 대상 노드를 전용 믹싱 유형( `granite:AuthenticationRequired`)으로 표시하여 동일한 결과를 얻을 수 있습니다.

#### 로그인 경로 {#property-for-excluding-login-path} 제외 속성

mixin 유형은 기본적으로 `cq:cugLoginPage` 속성에 해당하는 `granite:loginPath`이라는 단일 선택적 속성을 정의합니다. 이전 구현과 달리, 선언된 노드 유형이 언급된 믹스인 경우에만 로그인 경로 속성이 유지됩니다. 혼합 유형을 설정하지 않고 해당 이름의 속성을 추가하면 아무런 영향을 주지 않으며 새로운 요구 사항이나 로그인 경로에 대한 제외가 인증자에게 보고되지 않습니다.

#### 인증 요구 사항에 대한 권한 {#privilege-for-authentication-requirement}

혼합 유형을 추가하거나 제거하려면 `jcr:nodeTypeManagement` 권한이 부여되어야 합니다. 이전 구현에서, `jcr:modifyProperties` 권한은 잔여 속성을 편집하는 데 사용됩니다.

`granite:loginPath`에 관한한 속성을 추가, 수정 또는 제거하는 데에는 동일한 권한이 필요합니다.

#### 혼합형 유형에 의해 정의된 Target 노드 {#target-node-defined-by-mixin-type}

인증 요구 사항은 강제 로그인에 적용할 하위 트리를 정의하는 JCR 노드에서 작성되어야 합니다. CUG가 전체 트리에 영향을 주고 새 구현의 UI가 결과적으로 페이지 노드에 인증 요구 사항 믹싱 유형을 추가하는 경우에 AEM 페이지일 수 있습니다.

CUG 정책을 지정된 페이지 아래에 있는 jcr:content 노드에만 배치하면 컨텐츠에 대한 액세스만 제한되지만 페이지 노드 자체나 하위 페이지에서는 영향을 받지 않습니다.

이것은 유효한 시나리오일 수 있으며 모든 노드에 믹싱을 배치할 수 있는 저장소 편집기를 사용할 수 있습니다. 하지만 이러한 동작은 이전 구현과 대비되며, jcr:content 노드에 cq:cugEnabled 또는 cq:cugLoginPage 속성을 삽입하는 것은 궁극적으로 페이지 노드에 내부적으로 다시 매핑되었습니다. 이 매핑은 더 이상 수행되지 않습니다.

#### 구성된 지원되는 경로 {#configured-supported-paths}

`granite:AuthenticationRequired` 혼합 유형과 granite:loginPath 속성은 모두 **Adobe Granite 인증 요구 사항 및 로그인 경로 처리기**&#x200B;에 있는 **Supported Paths** 구성 옵션 집합에 의해 정의된 범위 내에서만 적용됩니다. 경로를 지정하지 않으면 인증 요구 사항 기능이 모두 비활성화됩니다. 이 경우 지정된 JCR 노드에 추가하거나 설정할 때 mixin 유형 또는 속성이 적용됩니다.

### JCR 컨텐트, OSGi 서비스 및 구성 매핑 {#mapping-of-jcr-content-osgi-services-and-configurations}

아래 문서는 이전 및 새 구현 간에 OSGi 서비스, 구성 및 저장소 컨텐츠의 포괄적인 매핑을 제공합니다.

AEM 6.3 이후의 CUG 매핑

[파일 가져오기](assets/cug-mapping.pdf)

## 업그레이드 CUG {#upgrade-cug}

### 사용되지 않는 CUG {#existing-installations-using-the-deprecated-cug}을(를) 사용하는 기존 설치

이전 CUG 지원 구현은 더 이상 사용되지 않으며 향후 버전에 대해 제거됩니다. AEM 6.3 이전 버전에서 업그레이드할 때에는 새 구현으로 이동하는 것이 좋습니다.

업그레이드된 AEM 설치의 경우 하나의 CUG 구현만 활성화되어 있는지 확인해야 합니다. 사용되지 않는 새 CUG 지원과 이전 CUG 지원의 조합은 테스트되지 않으며 원하지 않는 동작을 초래할 수 있습니다.

* 인증 요구 사항과 관련된 Sling Authenticator 충돌
* 이전 CUG와 연결된 ACL 설정이 새로운 CUG 정책과 충돌할 때 읽기 액세스가 거부되었습니다.

### 기존 CUG 컨텐츠 마이그레이션 {#migrating-existing-cug-content}

Adobe은 새 CUG 구현으로 마이그레이션하는 도구를 제공합니다. 이 기능을 사용하려면 다음 단계를 수행하십시오.

1. 도구에 액세스하려면 `https://<serveraddress>:<serverport>/system/console/cug-migration`로 이동합니다.
1. CUG를 확인할 루트 경로를 입력하고 **연습 실행 수행** 단추를 누릅니다. 그러면 선택한 위치에서 변환 가능한 CUG가 검색됩니다.
1. 결과를 검토한 후 **마이그레이션 수행** 단추를 눌러 새 구현으로 마이그레이션합니다.

>[!NOTE]
>
>문제가 발생하는 경우 마이그레이션 도구의 출력을 얻기 위해 `com.day.cq.auth.impl.cug`에서 **DEBUG** 수준으로 특정 로거를 설정할 수 있습니다. 이 방법에 대한 자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md)을 참조하십시오.
