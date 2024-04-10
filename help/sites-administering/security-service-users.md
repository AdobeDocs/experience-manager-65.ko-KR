---
title: Adobe Experience Manager의 서비스 사용자
description: Adobe Experience Manager의 서비스 사용자에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 0%

---


# Adobe Experience Manager(AEM)의 서비스 사용자 {#service-users-in-aem}

## 개요 {#overview}

AEM에서 관리 세션 또는 리소스 확인자를 가져오는 기본 방법은 `SlingRepository.loginAdministrative()` 및 `ResourceResolverFactory.getAdministrativeResourceResolver()` sling에서 제공하는 메서드입니다.

그러나 이 두 가지 방법 중 어느 것도 [최소 특권의 원칙](https://en.wikipedia.org/wiki/Principle_of_least_privilege). 개발자가 초기에 콘텐츠에 대한 적절한 구조와 해당 ACL(액세스 제어 수준)을 계획하지 않을 수 있기 때문입니다. 그러한 서비스에 취약점이 존재하는 경우 해당 서비스로의 권한 에스컬레이션으로 이어지는 경우가 많습니다. `admin` 코드 자체가 작동하는 데 관리 권한이 필요하지 않더라도 사용자

## 관리 세션을 단계적으로 종료하는 방법 {#how-to-phase-out-admin-sessions}

### 우선 순위 0: 기능이 활성/필요/중단되었습니까? {#priority-is-the-feature-active-needed-derelict}

관리 세션이 사용되지 않거나 기능이 완전히 비활성화된 경우가 있을 수 있습니다. 구현과 함께 그런 경우에는 기능을 모두 제거하거나 크기에 맞게 조정해야 합니다 [NOP 코드](https://en.wikipedia.org/wiki/NOP).

### 우선 순위 1: 요청 세션 사용 {#priority-use-the-request-session}

가능하면 콘텐츠를 읽거나 쓰는 데 지정된 인증된 요청 세션을 사용할 수 있도록 기능을 리팩터링하십시오. 이렇게 할 수 없는 경우, 아래 우선순위에 따라 우선 순위를 적용하여 달성할 수도 있다.

### 우선 순위 2: 컨텐츠 재구성 {#priority-restructure-content}

많은 이슈들은 내용을 재구조화하여 해결할 수 있다. 재구성을 수행할 때 다음과 같은 간단한 규칙을 염두에 두십시오.

* **액세스 제어 변경**

   * 실제로 액세스할 필요가 있는 사용자 또는 그룹이 실제로 액세스할 수 있는지 확인하십시오.

* **콘텐츠 구조 세분화**

   * 예를 들어 액세스 제어가 사용 가능한 요청 세션과 일치하는 다른 위치로 이동합니다.
   * 컨텐츠 세부기간을 변경합니다.

* **적절한 서비스로 코드 리팩터링**

   * 비즈니스 논리를 JSP 코드에서 서비스로 이동합니다. 이를 통해 다양한 콘텐츠 모델링을 수행할 수 있습니다.

또한 개발하는 새로운 기능이 다음 원칙을 준수하는지 확인하십시오.

* **보안 요구 사항이 콘텐츠 구조를 주도해야 함**

   * 액세스 제어 관리는 자연스럽게 느껴져야 합니다.
   * 액세스 제어는 애플리케이션이 아닌 저장소에서 적용해야 합니다.

* **노드 유형 사용**

   * 설정할 수 있는 속성 집합 제한

* **개인 정보 설정 준수**

   * 비공개 프로필이 있는 경우, 한 가지 예를 들자면 비공개 프로필에 있는 프로필 사진, 이메일 또는 전체 이름을 노출하지 않는 것입니다 `/profile` 노드.

## 엄격한 액세스 제어 {#strict-access-control}

컨텐츠를 재구성하는 동안 액세스 제어를 적용하든 새 서비스 사용자에 대해 적용하든 가능한 가장 엄격한 ACL을 적용해야 합니다. 액세스 제어의 가능한 모든 시설 사용:

* 예를 들어 를 적용하는 대신 `jcr:read` 날짜 `/apps`, 다음에만 적용 `/apps/*/components/*/analytics`

* 사용 [제한 사항](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* 노드 유형에 ACL 적용
* 권한 제한

   * 예를 들어 속성을 작성해야 하는 경우에만 `jcr:write` 권한; 사용 `jcr:modifyProperties` 대신

## 서비스 사용자 및 매핑 {#service-users-and-mappings}

위에서 언급한 내용이 실패하면 Sling 7은 번들 대 사용자 매핑과 두 개의 해당 API 방법을 구성할 수 있는 서비스 사용자 매핑 서비스를 제공합니다.

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

이 메서드는 구성된 사용자의 권한만 있는 세션/리소스 확인자를 반환합니다. 이러한 방법에는 다음과 같은 특성이 있습니다.

* 사용자에게 매핑 서비스를 허용합니다.
* 하위 서비스 사용자를 정의할 수 있습니다
* 중앙 구성 지점은 다음과 같습니다. `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [&quot;:&quot; subservice-name]

* `service-id` 인증용 리소스 확인자 및/또는 JCR 저장소 사용자 ID에 매핑됩니다.
* `service-name` 는 서비스를 제공하는 번들의 기호 이름입니다

## 기타 Recommendations {#other-recommendations}

### admin-session을 service-user로 바꾸기 {#replacing-the-admin-session-with-a-service-user}

서비스 사용자는 암호가 설정되지 않고 특정 작업을 수행하는 데 필요한 최소 권한 집합이 있는 JCR 사용자입니다. 암호가 설정되지 않았다는 것은 서비스 사용자로 로그인할 수 없음을 의미합니다.

관리 세션을 사용하지 않는 방법은 서비스 사용자 세션으로 바꾸는 것입니다. 또한 필요한 경우 여러 하위 서비스 사용자로 대체될 수 있습니다.

관리 세션을 서비스 사용자로 바꾸려면 다음 단계를 수행해야 합니다.

1. 최소 권한의 원칙을 고려하여 서비스에 필요한 권한을 식별합니다.
1. 필요한 권한 설정을 정확히 가진 사용자가 이미 있는지 확인합니다. 기존 사용자가 요구 사항과 일치하지 않는 경우 시스템 서비스 사용자를 만듭니다. 서비스 사용자를 만들려면 RTC가 필요합니다. 경우에 따라 액세스를 더 구분하기 위해 여러 하위 서비스 사용자(예: 쓰기용 사용자 및 읽기용 사용자)를 만드는 것이 적절합니다.
1. 사용자에 대한 ACE를 설정하고 테스트합니다.
1. 추가 `service-user` 서비스 및 를 위한 매핑 `user/sub-users`

1. 서비스 사용자 슬링 기능을 번들에서 사용할 수 있도록 설정: 의 최신 버전으로 업데이트 `org.apache.sling.api`.

1. 바꾸기 `admin-session` 을 사용한 코드 내 `loginService` 또는 `getServiceResourceResolver` API.

## 서비스 사용자 만들기 {#creating-a-new-service-user}

AEM 서비스 사용자 목록에 사용 사례에 적용할 수 있는 사용자가 없고 해당 RTC 문제가 승인되었음을 확인한 후 새 사용자를 기본 콘텐츠에 추가합니다.

권장되는 접근 방법은 저장소 탐색기를 사용할 서비스 사용자를 만드는 것입니다. *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

목표는 유효한 을 얻는 것입니다. `jcr:uuid` 콘텐츠 패키지 설치를 통해 사용자를 만드는 데 필요한 속성입니다.

다음을 수행하여 서비스 사용자를 만들 수 있습니다.

1. 다음 위치의 저장소 탐색기로 이동 *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. 을 눌러 관리자로 로그인 **로그인** 화면 왼쪽 상단에 있는 링크.
1. 그런 다음 시스템 사용자를 만들고 이름을 지정합니다. 사용자를 시스템 경로로 생성하려면 중간 경로를 로 설정합니다. `system` 필요에 따라 다음과 같은 하위 폴더를 추가합니다.

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. 시스템 사용자 노드가 다음과 같이 표시되는지 확인합니다.

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >서비스 사용자와 연결된 mixin 유형이 없습니다. 즉, 시스템 사용자에 대한 액세스 제어 정책이 없습니다.

해당 .content.xml을 번들의 내용에 추가할 때 `rep:authorizableId` 기본 유형이 `rep:SystemUser`. 다음과 같이 표시되어야 합니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## ServiceUserMapper 구성에 구성 수정 사항 추가 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

서비스에서 해당 시스템 사용자에 대한 매핑을 추가하려면 [`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html) 서비스. 이러한 모듈화를 유지하기 위해, 이러한 구성은 다음을 사용하여 제공될 수 있다. [Sling 수정 메커니즘](https://issues.apache.org/jira/browse/SLING-3578). 번들과 함께 이러한 구성을 설치하는 데 권장되는 방법은 [Sling 초기 컨텐츠 로드 중](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. 번들의 src/main/resources 폴더 아래에 하위 폴더 SLING-INF/컨텐츠를 만듭니다
1. 이 폴더에서 org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.revised라는 파일을 만듭니다.&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>모든 하위 서비스 사용자 매핑을 포함하여 공장 구성 콘텐츠가 포함된 .xml 예:

1. 만들기 `SLING-INF/content` 폴더 아래 `src/main/resources` 번들의 폴더
1. 이 폴더에서 파일을 만듭니다. `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` 모든 하위 서비스 사용자 매핑을 포함하여 공장 구성 콘텐츠 포함

   설명을 위해 라는 파일을 가져옵니다. `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. 의 구성에서 Sling 초기 컨텐츠 참조 `maven-bundle-plugin` 다음에서 `pom.xml` 번들의 예:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. 번들을 설치하고 출하 시 구성이 설치되었는지 확인합니다. 다음을 통해 이 작업을 수행할 수 있습니다.

   * 의 웹 콘솔로 이동 *https://serverhost:serveraddress/system/console/configMgr*
   * 검색 대상 **Apache Sling Service User Mapper 서비스 수정**
   * 링크를 클릭하면 적절한 구성이 적용되었는지 확인할 수 있습니다.

## 서비스에서 공유 세션 처리 {#dealing-with-shared-sessions-in-services}

호출 대상 `loginAdministrative()` 공유 세션과 함께 표시되는 경우가 많습니다. 이러한 세션은 서비스 활성화 시 획득되며 서비스가 중지된 후에만 로그아웃됩니다. 일반적인 방법이지만 두 가지 문제로 이어집니다.

* **보안:** 이러한 관리 세션은 공유 세션에 바인딩된 리소스 또는 기타 개체를 캐시하고 반환하는 데 사용됩니다. 나중에 호출 스택에서 이러한 개체는 높은 권한을 가진 세션 또는 리소스 확인자에 맞게 조정될 수 있습니다. 종종 호출자가 운영 중인 관리 세션인지 명확하지 않습니다.
* **성능:** Oak에서 공유 세션은 성능 문제를 일으킬 수 있으므로 사용하지 않는 것이 좋습니다.

보안 위험에 대한 가장 명백한 해결 방법은 `loginAdministrative()` 을 사용하여 호출 `loginService()` 하나는 제한된 권한을 가진 사용자에게 표시됩니다. 그러나 이는 잠재적인 성능 저하에는 영향을 주지 않습니다. 세션과 연관성이 없는 객체에서 모든 요청된 정보를 래핑하는 문제를 완화할 수 있습니다. 그런 다음 필요에 따라 세션을 생성(또는 제거)합니다.

권장되는 접근 방법은 호출자에게 세션의 생성/소멸을 제어할 수 있도록 서비스 API를 리팩터링하는 것입니다.

## JSP의 관리 세션 {#administrative-sessions-in-jsps}

JSP는 `loginService()`: 연결된 서비스가 없기 때문입니다. 그러나 JSP의 관리 세션은 일반적으로 MVC 패러다임 위반의 징후입니다.

이 문제는 다음 두 가지 방법으로 해결할 수 있습니다.

1. 사용자 세션에서 콘텐츠를 조작할 수 있는 방식으로 콘텐츠를 재구성합니다.
1. JSP에서 사용할 수 있는 API를 제공하는 서비스에 논리 추출

첫 번째 방법이 선호됩니다.

## 이벤트, 복제 전처리기 및 작업 처리 {#processing-events-replication-preprocessors-and-jobs}

이벤트 또는 작업, 경우에 따라 워크플로우를 처리할 때 이벤트를 트리거한 해당 세션이 손실됩니다. 이렇게 되면 이벤트 처리기와 작업 처리기가 종종 관리 세션을 사용하여 작업을 수행하게 됩니다. 각각 장점과 단점을 가진 이 문제를 해결하기 위해 생각할 수 있는 접근 방식이 다릅니다.

1. 전달 `user-id` 이벤트 페이로드에서 가장을 사용합니다.

   **장점:** 사용하기 쉽습니다.

   **단점:** 여전히 사용 `loginAdministrative()`. 이미 인증된 요청을 재인증합니다.

1. 데이터에 액세스할 수 있는 서비스 사용자를 만들거나 재사용합니다.

   **장점:** 현재 디자인과 일치합니다. 최소한의 변경이 필요합니다.

   **단점:** 강력한 서비스 사용자가 유연하게 대처해야 하므로 권한 에스컬레이션이 쉽게 발생할 수 있습니다. 보안 모델을 우회합니다.

1. 의 직렬화 전달 `Subject` 이벤트 페이로드에서 `ResourceResolver` 그 주제에 근거를 두었습니다. 한 가지 예는 JAAS를 사용하는 것입니다 `doAsPrivileged` 다음에서 `ResourceResolverFactory`.

   **장점:** 보안 관점에서 깔끔한 구현. 재인증을 피하고 원래 권한으로 작동합니다. 보안 관련 코드는 이벤트 소비자에게 투명합니다.

   **단점:** 리팩터링이 필요합니다. 보안 관련 코드가 이벤트 소비자에게 투명하다는 점도 문제를 일으킬 수 있습니다.

세 번째 접근법은 선호되는 처리 기술이다.

## 워크플로우 프로세스 {#workflow-processes}

워크플로우 프로세스 구현 내에서 워크플로우를 트리거한 해당 사용자 세션이 손실됩니다. 이렇게 되면 관리 세션을 사용하여 작업을 수행하는 워크플로우 프로세스가 시작됩니다.

이러한 문제를 수정하려면에 언급된 것과 동일한 접근 방식을 사용하는 것이 좋습니다. [이벤트, 복제 전처리기 및 작업 처리](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) 사용합니다.

## Sling POST 프로세서 및 삭제된 페이지 {#sling-post-processors-and-deleted-pages}

슬링 POST 프로세서 구현에 사용되는 두 가지 관리 세션이 있습니다. 일반적으로 관리 세션은 처리 중인 POST 내에서 삭제 보류 중인 노드에 액세스하는 데 사용됩니다. 따라서 요청 세션을 통해 더 이상 사용할 수 없습니다. 삭제 보류 중인 노드는 액세스해서는 안 되는 메타데이터를 공개하기 위해 액세스할 수 있습니다.
