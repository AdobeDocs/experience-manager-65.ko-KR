---
title: AEM의 서비스 사용자
seo-title: Service Users in AEM
description: AEM의 서비스 사용자에 대해 알아봅니다.
seo-description: Learn about Service Users in AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 0%

---

# AEM의 서비스 사용자{#service-users-in-aem}

## 개요 {#overview}

AEM에서 관리 세션 또는 리소스 확인자를 가져오는 주요 방법은 `SlingRepository.loginAdministrative()` 및 `ResourceResolverFactory.getAdministrativeResourceResolver()` Sling에서 제공하는 메서드를 참조하십시오.

그러나 이 두 방법 모두 [무권리주의](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 또한 개발자가 일찍 컨텐츠에 적절한 구조 및 해당 ACL(액세스 제어 수준)을 계획하지 않도록 너무 쉽게 할 수 있습니다. 이러한 서비스에 취약점이 있으면 종종 권한 에스컬레이션이 `admin` 사용자. 코드 자체가 작동하는 관리 권한이 필요하지 않더라도

## 관리자 세션을 단계적으로 종료하는 방법 {#how-to-phase-out-admin-sessions}

### 우선순위 0: 이 기능이 활성/필수/방치되어 있습니까? {#priority-is-the-feature-active-needed-derelict}

관리 세션을 사용하지 않거나 기능이 완전히 비활성화된 경우가 있을 수 있습니다. 구현이 이러한 경우라면 기능을 완전히 제거하거나 기능에 맞게 조정하십시오 [NOP 코드](https://en.wikipedia.org/wiki/NOP).

### 우선순위 1: 요청 세션 사용 {#priority-use-the-request-session}

가능한 경우 지정된 인증된 요청 세션을 컨텐츠 읽기 또는 쓰기에 사용할 수 있도록 기능을 리팩터링할 수 있습니다. 이 작업을 수행할 수 없는 경우, 아래 우선순위 다음에 나오는 우선순위를 적용하여 종종 달성할 수 있습니다.

### 우선순위 2: 컨텐츠 재구성 {#priority-restructure-content}

콘텐츠를 재구성함으로써 많은 문제를 해결할 수 있습니다. 구조 조정을 수행할 때는 다음 간단한 규칙을 염두에 두십시오.

* **액세스 제어 변경**

   * 실제로 액세스 권한이 필요한 사용자 또는 그룹이 실제로 액세스할 수 있는지 확인합니다.

* **콘텐츠 구조 세분화**

   * 액세스 제어가 사용 가능한 요청 세션과 일치하는 경우 등 다른 위치로 이동합니다.
   * 컨텐츠 세부기간을 변경합니다.

* **코드를 적절한 서비스로 리팩터링**

   * 비즈니스 로직을 JSP 코드에서 서비스로 이동합니다. 이렇게 하면 다른 컨텐츠 모델링을 수행할 수 있습니다.

또한 개발하는 새로운 기능은 다음 원칙을 따라야 합니다.

* **보안 요구 사항이 컨텐츠 구조를 주도해야 합니다**

   * 액세스 제어를 관리하는 것은 자연스러운 것으로 느껴져야 합니다
   * 액세스 제어는 애플리케이션이 아니라 리포지토리에 의해 적용되어야 합니다

* **노드 사용**

   * 설정할 수 있는 속성 집합을 제한합니다

* **개인 정보 설정 준수**

   * 비공개 프로필의 경우 한 가지 예를 들자면 비공개 프로필에 있는 프로필 사진, 이메일 또는 전체 이름을 노출하지 않는 것이 됩니다 `/profile` 노드 아래에 있어야 합니다.

## 엄격한 액세스 제어 {#strict-access-control}

컨텐츠를 재구성하는 동안 액세스 제어를 적용하든, 새 서비스 사용자에 대해 액세스 제어를 적용하든 간에 가장 엄격한 ACL을 적용해야 합니다. 액세스 제어의 가능한 모든 기능을 사용하십시오.

* 예를 들어, `jcr:read` on `/apps`에만 적용 `/apps/*/components/*/analytics`

* 사용 [제한 사항](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 노드 유형에 ACL 적용
* 권한 제한

   * 예를 들어 속성을 작성해야 할 때만 `jcr:write` 권한 사용 `jcr:modifyProperties` 대신

## 서비스 사용자 및 매핑 {#service-users-and-mappings}

위의 작업이 실패하면 Sling 7에서는 번들-사용자 매핑 과 두 개의 해당 API 메서드를 구성할 수 있는 서비스 사용자 매핑 서비스를 제공합니다. ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` 및 ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` 구성된 사용자의 권한으로 세션/리소스 확인자를 반환합니다. 이러한 방법에는 다음과 같은 특성이 있습니다.

* 이를 통해 사용자에게 서비스를 매핑할 수 있습니다
* 이를 통해 하위 서비스 사용자를 정의할 수 있습니다
* 중앙 구성 포인트는 다음과 같습니다. `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [ &quot;:&quot; subservice-name ] 

* `service-id` 인증을 위해 리소스 확인자 및/또는 JCR 저장소 사용자 ID에 매핑됩니다
* `service-name` 은 서비스를 제공하는 번들의 상징적인 이름입니다

## 기타 Recommendations {#other-recommendations}

### admin-session을 service-user로 바꾸기 {#replacing-the-admin-session-with-a-service-user}

서비스 사용자는 특정 작업을 수행하는 데 필요한 최소한의 권한 집합과 암호가 설정되지 않은 JCR 사용자입니다. 설정된 암호가 없으면 서비스 사용자로 로그인할 수 없습니다.

관리 세션을 사용하지 않는 방법은 서비스 사용자 세션으로 교체하는 것입니다. 필요한 경우 여러 하위 서비스 사용자로 대체할 수도 있습니다.

관리 세션을 서비스 사용자로 대체하려면 다음 단계를 수행해야 합니다.

1. 최소 권한 원칙을 고려하여 서비스에 필요한 권한을 식별합니다.
1. 필요한 권한 설정으로 사용 가능한 사용자가 이미 있는지 확인합니다. 기존 사용자가 사용자의 요구 사항에 맞지 않을 경우 새 시스템 서비스 사용자를 만듭니다. 새 서비스 사용자를 만들려면 RTC가 필요합니다. 경우에 따라 여러 하위 서비스 사용자(예: 쓰기 및 읽기 위한 사용자)를 만들어 액세스를 더 구분하는 것이 적절합니다.
1. 사용자를 위한 ACE 설정 및 테스트
1. 추가 `service-user` 서비스 및 대상 매핑 `user/sub-users`

1. 서비스 사용자 sling 기능을 번들에 사용할 수 있도록 합니다. 최신 버전의 `org.apache.sling.api`.

1. 바꾸기 `admin-session` 를 사용하여 `loginService` 또는 `getServiceResourceResolver` API.

## 새 서비스 사용자 만들기 {#creating-a-new-service-user}

AEM 서비스 사용자 목록에 있는 사용자가 사용 사례에 적용할 수 없고 해당 RTC 문제가 승인되었음을 확인한 후 기본 콘텐츠에 새 사용자를 추가할 수 있습니다.

권장되는 접근 방법은 저장소 탐색기를 사용할 서비스 사용자를 만드는 것입니다. *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

목표는 유효함을 얻는 것이다 `jcr:uuid` 속성(컨텐츠 패키지 설치를 통해 사용자를 만들려면 반드시 필요합니다.)

다음 방법으로 서비스 사용자를 만들 수 있습니다.

1. 저장소 탐색기로 이동 *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. 을 눌러 관리자로 로그인합니다. **로그인** 화면의 왼쪽 위 모서리에 연결합니다.
1. 그런 다음 시스템 사용자를 만들고 이름을 지정합니다. 사용자를 시스템 사용자로 만들려면 중간 경로를 로 설정합니다. `system` 필요에 따라 하위 폴더를 추가할 수 있습니다.

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 시스템 사용자 노드가 다음과 같이 표시되는지 확인합니다.

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >서비스 사용자와 연관된 혼합 유형은 없습니다. 즉, 시스템 사용자에 대한 액세스 제어 정책이 없습니다.

해당 .content.xml을 번들의 내용에 추가할 때는 `rep:authorizableId` 기본 유형은 `rep:SystemUser`. 다음과 같이 표시되어야 합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## ServiceUserMapper 구성에 구성 수정을 추가하는 중 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

서비스에서 해당 시스템 사용자에게 매핑을 추가하려면 ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)` 서비스. 이러한 모듈식 구성을 유지하려면 [Sling 수정 메커니즘](https://issues.apache.org/jira/browse/SLING-3578). 이러한 구성을 번들에 설치하는 데 권장되는 방법은 [Sling 초기 컨텐츠 로드](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. 번들의 src/main/resources 폴더 아래에 하위 폴더 SLING-INF/content를 만듭니다
1. 이 폴더에서 org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.개정- 파일을 만듭니다.&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>모든 하위 서비스 사용자 매핑 포함)의 내용을 포함하는 .xml을 만듭니다. 예:

1. 만들기 `SLING-INF/content` 폴더 아래 `src/main/resources` 번들 폴더
1. 이 폴더에서 파일을 만듭니다. `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` 모든 하위 서비스 사용자 매핑을 포함하여 공장 구성의 컨텐츠로 가져오기.

   예를 들어, `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. 의 구성에서 Sling 초기 컨텐츠를 참조합니다. `maven-bundle-plugin` 에서 `pom.xml` 번들의 예:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 번들을 설치하고 공장 구성이 설치되었는지 확인하십시오. 다음을 통해 이 작업을 수행할 수 있습니다.

   * 의 웹 콘솔로 이동 *https://serverhost:serveraddress/system/console/configMgr*
   * 검색 대상 **Apache Sling Service User Mapper Service 수정 사항**
   * 적절한 구성이 있는지 확인하려면 링크를 클릭하십시오.

## 서비스의 공유 세션 처리 {#dealing-with-shared-sessions-in-services}

호출 대상 `loginAdministrative()` 종종 공유 세션과 함께 표시됩니다. 이러한 세션은 서비스 활성화 시 획득되며 서비스를 중지한 후에만 로그아웃됩니다. 이 방법은 일반적인 방법이지만, 두 가지 문제로 이어집니다.

* **보안:** 이러한 관리 세션은 공유 세션에 바인딩된 리소스 또는 다른 개체를 캐시하고 반환하는 데 사용됩니다. 나중에 호출 스택에서 이러한 개체는 높은 권한을 가진 세션이나 리소스 확인자에 적응할 수 있으며, 호출자에게 해당 개체가 사용 중인 관리 세션이라는 것을 명확하지 않은 경우가 있습니다.
* **성능:** Oak 공유 세션에서 성능 문제가 발생할 수 있으며 현재 이러한 세션을 사용하지 않는 것이 좋습니다.

보안 위험에 대한 가장 분명한 해결 방법은 `loginAdministrative()` 를 사용하여 호출 `loginService()` 제한된 권한을 가진 사용자에게 한 가지 액세스. 그러나 이는 잠재적인 성능 저하에 영향을 주지 않습니다. 세션과의 연관성이 없는 개체에 요청된 모든 정보를 래핑하는 것을 줄일 수 있습니다. 그런 다음 세션을 요청 시 만들거나 삭제합니다.

권장되는 접근 방법은 서비스의 API를 리팩터링하여 호출자에게 세션의 생성/삭제를 제어하는 것입니다.

## JSP의 관리 세션 {#administrative-sessions-in-jsps}

JSP에서 `loginService()`로 설정되면 연결된 서비스가 없으므로 그러나 JSP의 관리 세션은 일반적으로 MVC 패러다임을 위반하는 표시입니다.

다음과 같은 두 가지 방법으로 수정할 수 있습니다.

1. 사용자 세션을 사용하여 컨텐츠를 조작할 수 있는 방식으로 컨텐츠를 재구성합니다.
1. JSP에서 사용할 수 있는 API를 제공하는 서비스에 논리를 추출합니다.

첫 번째 방법이 선호됩니다

## 처리 이벤트, 복제 전처리기 및 작업 {#processing-events-replication-preprocessors-and-jobs}

이벤트 또는 작업을 처리할 때, 일부 경우에 워크플로우에서 이벤트를 트리거한 해당 세션이 일반적으로 손실됩니다. 이로 인해 이벤트 핸들러 및 작업 처리자가 종종 관리 세션을 사용하여 작업을 수행합니다. 이 문제를 해결하기 위한 각각의 장점과 단점이 있습니다.

1. 전달 `user-id` 이벤트 페이로드에서 및 가장을 사용합니다.

   **장점:** 사용하기 쉬움.

   **단점:** 여전히 사용 `loginAdministrative()`. 이미 인증된 요청을 다시 인증합니다.

1. 데이터에 액세스할 수 있는 서비스 사용자를 만들거나 재사용합니다.

   **장점:** 현재 설계와 일치합니다. 최소한의 변경이 필요합니다.

   **단점:** 매우 강력한 서비스 사용자가 유연해야 하며, 이로 인해 권한 에스컬레이션이 쉽게 발생할 수 있습니다. 보안 모델을 우회합니다.

1. 의 직렬화 전달 `Subject` 이벤트 페이로드에서 그리고 `ResourceResolver` 그 주제에 근거해서 한 가지 예를 들자면 JAAS를 사용하는 것입니다 `doAsPrivileged` 에서 `ResourceResolverFactory`.

   **장점:** 보안 관점에서 구현을 정리합니다. 재인증을 피하고 원래 권한으로 작동합니다. 보안 관련 코드는 이벤트 소비자에게 투명합니다.

   **단점:** 리팩터링이 필요합니다. 이벤트 소비자에 대해 관련 코드가 투명하게 처리되면 문제가 발생할 수도 있습니다.

세 번째 방법은 현재 기본 처리 방법입니다.

## 워크플로우 프로세스 {#workflow-processes}

워크플로우 프로세스 구현 내에서 워크플로우를 트리거한 해당 사용자 세션은 일반적으로 손실됩니다. 이로 인해 워크플로우 프로세스는 종종 관리 세션을 사용하여 작업을 수행합니다.

이러한 문제를 수정하려면에 언급된 것과 동일한 접근 방식이 좋습니다. [처리 이벤트, 복제 전처리기 및 작업](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) 사용할 수 없습니다.

## Sling POST 프로세서 및 삭제된 페이지 {#sling-post-processors-and-deleted-pages}

sling POST 프로세서 구현에 사용되는 관리 세션은 두 가지가 있습니다. 일반적으로 관리 세션은 처리 중인 POST 내에서 삭제 보류 중인 노드에 액세스하는 데 사용됩니다. 따라서 요청 세션을 통해 더 이상 사용할 수 없습니다. 삭제 보류 중인 노드는 액세스할 수 없으며 액세스하면 안 되는 메타데이터를 표시하기 위해 액세스할 수 있습니다.
