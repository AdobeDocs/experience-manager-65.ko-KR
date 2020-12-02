---
title: AEM의 서비스 사용자
seo-title: AEM의 서비스 사용자
description: AEM의 서비스 사용자에 대해 알아봅니다.
seo-description: AEM의 서비스 사용자에 대해 알아봅니다.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 0%

---


# AEM의 서비스 사용자{#service-users-in-aem}

## 개요 {#overview}

AEM에서 관리 세션이나 리소스 확인자를 가져오는 주된 방법은 Sling에서 제공하는 `SlingRepository.loginAdministrative()` 및 `ResourceResolverFactory.getAdministrativeResourceResolver()` 메서드를 사용하는 것입니다.

그러나 이러한 방법 중 어느 것도 최소 권한[의 원칙을 중심으로 설계되지 않았으며 개발자가 초기에 컨텐츠에 적합한 구조와 해당 ACL(액세스 제어 수준)을 계획하지 않도록 너무 쉽게 할 수 있습니다. ](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 이러한 서비스에 취약점이 있는 경우 코드 자체에 관리자 권한이 없어도 종종 `admin` 사용자에게 권한 에스컬레이션이 발생합니다.

## 종료 관리자 세션 위상 방법 {#how-to-phase-out-admin-sessions}

### 우선 순위 0:이 기능은 활성 상태입니까/필수 입니까/방치입니까?{#priority-is-the-feature-active-needed-derelict}

관리 세션이 사용되지 않거나 기능이 완전히 비활성화되어 있을 수 있습니다. 구현의 경우 기능을 모두 제거하거나 [NOP 코드](https://en.wikipedia.org/wiki/NOP)에 맞추십시오.

### 우선 순위 1:요청 세션 사용 {#priority-use-the-request-session}

가능한 한 해당 인증된 요청 세션을 컨텐츠 읽기 또는 쓰기에 사용할 수 있도록 기능을 리팩터링할 수 있습니다. 이렇게 할 수 없는 경우 아래 우선 순위를 적용하여 얻을 수 있습니다.

### 우선 순위 2:콘텐츠 재구성 {#priority-restructure-content}

콘텐츠를 재조정하면 많은 문제가 해결된다. 구조 조정을 수행할 때 다음과 같은 간단한 규칙을 염두에 두십시오.

* **액세스 제어 변경**

   * 액세스 권한이 정말로 필요한 사용자나 그룹이 실제로 액세스 권한을 가지고 있는지 확인하십시오.

* **콘텐츠 구조 조정**

   * 액세스 제어가 사용 가능한 요청 세션과 일치하는 경우 등 다른 위치로 이동합니다.
   * 컨텐츠 세부기간 변경;

* **코드를 적절한 서비스로 재지정**

   * JSP 코드에서 서비스로 비즈니스 로직을 이동합니다. 이를 통해 다양한 컨텐츠 모델링을 수행할 수 있습니다.

또한 다음과 같은 원칙을 준수하는 새로운 기능을 개발할 수 있습니다.

* **보안 요구 사항은 컨텐츠 구조를 주도해야 합니다.**

   * 액세스 제어 관리 시 자연스러워
   * 액세스 제어는 애플리케이션이 아니라 보관소에서 적용해야 합니다

* **노데티프 사용**

   * 설정할 수 있는 속성 집합 제한

* **개인 정보 설정 준수**

   * 비공개 프로필의 경우, 한 가지 예로는 비공개 `/profile` 노드에 있는 프로필 사진, 이메일 또는 전체 이름을 노출하지 않는 것입니다.

## 엄격한 액세스 제어 {#strict-access-control}

컨텐츠를 재구성할 때 액세스 제어를 적용하거나 새 서비스 사용자를 위해 수행하는 경우, 가능한 엄격한 ACL을 적용해야 합니다. 가능한 모든 액세스 제어 기능 사용:

* 예를 들어 `/apps`에 `jcr:read`을 적용하는 대신 `/apps/*/components/*/analytics`에만 적용합니다.

* [restrictions](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html) 사용

* 노드 유형에 ACL 적용
* 권한 제한

   * 예를 들어 속성을 쓸 필요 없이 `jcr:write` 권한을 부여하지 마십시오.대신 `jcr:modifyProperties` 사용

## 서비스 사용자 및 매핑 {#service-users-and-mappings}

상기에 오류가 발생하면 Sling 7은 번들-사용자 매핑 및 두 개의 해당 API 방법을 구성할 수 있는 서비스 사용자 매핑 서비스를 제공합니다.구성된 사용자의 권한으로 세션/리소스 확인자를 반환하는 ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` 및 ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` 이러한 메서드에는 다음과 같은 특성이 있습니다.

* 사용자에게 매핑 서비스를 허용합니다.
* 하위 서비스 사용자를 정의할 수 있습니다.
* 중앙 구성 지점은 다음과 같습니다.`org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` =  `service-name` [ &quot;:&quot; subservice-name  ] 

* `service-id` is mapped to resource resolver and/or JCR repository user ID for authentication
* `service-name` 서비스를 제공하는 번들의 상징적인 이름입니다.

## 기타 Recommendations {#other-recommendations}

### admin-session을 service-user {#replacing-the-admin-session-with-a-service-user}으로 교체

서비스 사용자는 암호를 설정하지 않은 JCR 사용자이며 특정 작업을 수행하는 데 필요한 최소한의 권한 집합입니다. 암호를 설정하지 않으면 서비스 사용자와 로그인할 수 없습니다.

관리 세션을 사용하지 않는 방법은 서비스 사용자 세션으로 바꾸는 것입니다. 필요한 경우 여러 하위 서비스 사용자로 대체될 수도 있습니다.

관리 세션을 서비스 사용자로 교체하려면 다음 단계를 수행해야 합니다.

1. 최소 권한 원칙을 고려하여 서비스에 필요한 권한을 식별합니다.
1. 필요한 권한 설정으로 사용할 수 있는 사용자가 이미 있는지 확인합니다. 기존 사용자가 요구 사항에 맞지 않을 경우 새 시스템 서비스 사용자를 만듭니다. 새 서비스 사용자를 만들려면 RTC가 필요합니다. 경우에 따라 여러 하위 서비스 사용자(예: 쓰기 사용자 및 읽기 사용자)를 만들어 액세스를 구분하는 것이 적절합니다.
1. 사용자의 ACE를 설정하고 테스트합니다.
1. 서비스 및 `user/sub-users`에 대한 `service-user` 매핑 추가

1. 번들에서 서비스 사용자 슬링 기능을 사용할 수 있도록 하십시오.`org.apache.sling.api`의 최신 버전으로 업데이트합니다.

1. 코드의 `admin-session`을 `loginService` 또는 `getServiceResourceResolver` API로 바꿉니다.

## 새 서비스 사용자 {#creating-a-new-service-user} 만들기

AEM 서비스 사용자 목록의 사용자가 사용 사례에 적용할 수 없고 해당 RTC 문제가 승인되었음을 확인한 후 기본 컨텐츠에 새 사용자를 추가할 수 있습니다.

권장 방법은 서비스 사용자를 만들어 *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*&#x200B;에서 저장소 탐색기를 사용하는 것입니다.

목표는 컨텐츠 패키지 설치를 통해 사용자를 만들기 위해 필수인 유효한 `jcr:uuid` 속성을 가져오는 것입니다.

다음 방법을 통해 서비스 사용자를 만들 수 있습니다.

1. *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*&#x200B;의 저장소 탐색기로 이동
1. 화면의 왼쪽 위 모서리에 있는 **로그인** 링크를 눌러 관리자로 로그인합니다.
1. 그런 다음 시스템 사용자를 만들고 이름을 지정합니다. 사용자를 시스템 사용자로 만들려면 중간 경로를 `system`으로 설정하고 필요에 따라 하위 폴더를 추가합니다.

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 시스템 사용자 노드가 다음과 같이 표시되는지 확인합니다.

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >서비스 사용자와 연관된 혼합 유형은 없습니다. 이는 시스템 사용자에 대한 액세스 제어 정책이 없음을 의미합니다.

번들의 컨텐츠에 해당 .content.xml을 추가할 때 `rep:authorizableId`을 설정했는지, 기본 유형은 `rep:SystemUser`인지 확인하십시오. 다음과 같이 표시됩니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## ServiceUserMapper 구성에 구성 수정 추가 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

서비스의 매핑을 해당 시스템 사용자에게 추가하려면 ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` 서비스에 대한 공장 구성을 만들어야 합니다. 이 모듈형 구성을 유지하려면 [Sling upwards mechanism](https://issues.apache.org/jira/browse/SLING-3578)을 사용하여 이러한 구성을 제공할 수 있습니다. 이러한 구성을 번들과 함께 설치하는 데 권장되는 방법은 [Sling Initial Content Loading](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html)을 사용하는 것입니다.

1. 번들의 src/main/resources 폴더 아래에 하위 폴더 SLING-INF/content 만들기
1. 이 폴더에서 org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.re정한-&lt;공장 구성에 대한 일부 고유한 이름>.xml 파일을 만듭니다(모든 하위 서비스 사용자 매핑 포함). 예:

1. 번들의 `src/main/resources` 폴더 아래에 `SLING-INF/content` 폴더를 만듭니다.
1. 이 폴더에서 모든 하위 서비스 사용자 매핑을 포함하여 공장 구성의 콘텐트가 있는 `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` 파일을 만듭니다.

   일러스트레이션을 위해 `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. 번들의 `pom.xml`에 있는 `maven-bundle-plugin`의 구성에서 Sling 초기 컨텐츠를 참조합니다. 예:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 번들을 설치하고 공장 구성이 설치되어 있는지 확인합니다. 다음을 통해 이 작업을 수행할 수 있습니다.

   * *https://serverhost:serveraddress/system/console/configMgr*&#x200B;의 웹 콘솔로 이동
   * **Apache Sling Service User Mapper 서비스 개정안 검색**
   * 링크를 클릭하여 적절한 구성이 적절한지 확인합니다.

## 서비스 {#dealing-with-shared-sessions-in-services}에서 공유 세션 처리

`loginAdministrative()`에 대한 호출은 종종 공유 세션과 함께 표시됩니다. 이러한 세션은 서비스 활성화에서 획득되며 서비스가 중단된 후에만 로그아웃됩니다. 이 방법은 일반적인 방법이지만 두 가지 문제로 이어집니다.

* **보안:** 이러한 관리 세션은 공유 세션에 바인딩되는 리소스 또는 기타 개체를 캐시하고 반환하는 데 사용됩니다. 나중에 호출 스택에서 이러한 개체는 더 높은 권한을 가진 세션이나 리소스 해결자에 맞게 조정될 수 있으며, 호출자에게 사용 중인 관리 세션이라는 것은 확실하지 않은 경우가 많습니다.
* **성능:** Oak 공유 세션에서 성능 문제가 발생할 수 있으며 현재 이 문제를 사용하지 않는 것이 좋습니다.

보안 위험에 대한 가장 확실한 해결 방법은 `loginAdministrative()` 호출을 `loginService()` 호출로 간단히 대체하여 제한된 권한이 있는 사용자에게 보내는 것입니다. 그러나 이는 잠재적인 성능 저하에 영향을 주지 않습니다. 세션과 연결되지 않은 개체에 요청된 모든 정보를 둘러싸는 것이 완화 가능입니다. 그런 다음 세션을 On-Demand로 생성(또는 제거)합니다.

권장되는 방법은 서비스의 API를 리팩터링하여 호출자가 세션의 생성/삭제를 제어하는 것입니다.

## JSP {#administrative-sessions-in-jsps}의 관리 세션

연결된 서비스가 없으므로 JSP는 `loginService()`을 사용할 수 없습니다. 그러나 JSP의 관리 세션은 일반적으로 MVC 패러다임 위반의 신호입니다.

이 문제는 다음 두 가지 방법으로 수정할 수 있습니다.

1. 사용자 세션에 맞게 컨텐츠를 조작할 수 있도록 컨텐츠를 재구성합니다.
1. JSP에서 사용할 수 있는 API를 제공하는 서비스에 로직을 추출합니다.

첫 번째 방법이 선호된다.

## 처리 이벤트, 복제 프리프로세서 및 작업 {#processing-events-replication-preprocessors-and-jobs}

이벤트나 작업을 처리할 때, 그리고 일부 워크플로우에서는 이벤트를 트리거한 해당 세션이 대개 손실됩니다. 이로 인해 이벤트 핸들러와 작업 프로세서가 관리 세션을 사용하여 작업을 수행할 수 있습니다. 이 문제를 해결하기 위한 다양한 접근 방법이 있으며, 각각 장점과 단점을 가지고 있습니다.

1. 이벤트 페이로드에서 `user-id`을(를) 전달하고 가장을 사용하십시오.

   **장점:** 사용하기 쉽습니다.

   **단점:** 여전히  `loginAdministrative()`사용합니다. 이미 인증된 요청을 다시 인증합니다.

1. 데이터에 액세스할 수 있는 서비스 사용자를 만들거나 재사용합니다.

   **장점:** 현재 디자인과 일관되게 표시됩니다. 최소한의 변화가 필요합니다.

   **단점:** 매우 강력한 서비스 사용자가 유연해야 하며, 이를 통해 권한 에스컬레이션이 쉽게 발생할 수 있습니다. 보안 모델을 우회합니다.

1. 이벤트 페이로드에서 `Subject`의 정리를 전달하고 해당 제목을 기준으로 `ResourceResolver`을 만듭니다. 한 예로 `ResourceResolverFactory`에서 JAAS `doAsPrivileged`을 사용할 수 있습니다.

   **장점:** 보안 관점에서 구현을 깔끔하게 구성할 수 있습니다. 재인증을 피하고 원래 권한으로 작동합니다. 관련 코드는 이벤트 소비자에게 투명하게 표시됩니다.

   **단점: 리팩토링** 이 필요합니다. 이벤트 소비자에게 관련된 보안 관련 코드가 투명하게 처리되면 문제가 발생할 수 있습니다.

세 번째 방법은 현재 기본 처리 방법입니다.

## 워크플로 프로세스 {#workflow-processes}

워크플로우 프로세스 내에서 워크플로우를 트리거한 해당 사용자 세션이 일반적으로 손실됩니다. 이로 인해 작업을 수행하기 위해 관리 세션을 사용하는 워크플로우 프로세스가 발생합니다.

이러한 문제를 해결하려면 [처리 이벤트, 복제 프리프로세서 및 작업](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs)에 언급된 것과 동일한 접근 방식을 사용하는 것이 좋습니다.

## 슬링 POST 프로세서 및 삭제된 페이지 {#sling-post-processors-and-deleted-pages}

슬링 POST 프로세서 구현에 사용되는 관리 세션은 몇 가지입니다. 일반적으로 관리 세션은 처리 중인 POST 내에서 삭제 보류 중인 노드에 액세스하는 데 사용됩니다. 따라서 요청 세션을 통해 더 이상 사용할 수 없습니다. 삭제 대기 중인 노드는 액세스할 수 없는 메타데이터를 공개하기 위해 액세스할 수 있습니다.
