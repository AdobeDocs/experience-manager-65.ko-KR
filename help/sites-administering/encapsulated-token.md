---
title: 캡슐화된 토큰 지원
seo-title: Encapsulated Token Support
description: AEM에서 캡슐화된 토큰 지원에 대해 알아봅니다.
seo-description: Learn about the Encapsulated Token support in AEM.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
exl-id: e24d815c-83e2-4639-8273-b4c0a6bb008a
source-git-commit: ed2cb35593780cd627c15f493e58d3b68c55519b
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# 캡슐화된 토큰 지원{#encapsulated-token-support}

## 소개 {#introduction}

기본적으로 AEM은 토큰 인증 핸들러를 사용하여 각 요청을 인증합니다. 그러나 인증 요청을 처리하려면 모든 요청에 대해 토큰 인증 핸들러가 리포지토리에 액세스해야 합니다. 이러한 문제는 쿠키가 인증 상태를 유지 관리하는 데 사용되기 때문에 발생합니다. 논리적으로, 후속 요청의 유효성을 검사하려면 상태가 리포지토리에서 유지되어야 합니다. 즉, 인증 메커니즘이 stateful입니다.

이는 수평적 확장성을 위해 특히 중요합니다. 아래에 표시된 게시 팜과 같은 다중 인스턴스 설정에서 최적의 방식으로 로드 밸런싱을 수행할 수 없습니다. 상태 저장 인증을 사용할 때는 사용자가 처음 인증되는 인스턴스에서만 지속적인 인증 상태를 사용할 수 있습니다.

![chlimage_1-33](assets/chlimage_1-33a.png)

다음 시나리오를 예로 들어보겠습니다.

사용자가 게시 인스턴스 1에서 인증될 수 있지만, 후속 요청이 게시 인스턴스 2로 이동하면 해당 상태가 게시 1 및 게시 2의 리포지토리에 유지되므로 해당 인스턴스에는 해당 인증 상태가 유지되지 않습니다.

이를 위한 해결 방법은 로드 밸런서 수준에서 고정 연결을 구성하는 것입니다. 고정 연결을 사용하면 사용자가 항상 동일한 게시 인스턴스로 이동됩니다. 따라서 진정한 최적의 로드 밸런싱은 불가능합니다.

게시 인스턴스를 사용할 수 없게 되면 해당 인스턴스에서 인증된 모든 사용자는 세션을 잃게 됩니다. 인증 쿠키의 유효성을 검사하려면 리포지토리 액세스 권한이 필요하기 때문입니다.

## 캡슐화된 토큰을 사용한 상태 비저장 인증 {#stateless-authentication-with-the-encapsulated-token}

수평 확장성을 위한 솔루션은 AEM에서 새로운 캡슐화된 토큰 지원을 사용하여 상태를 저장하지 않는 인증입니다.

캡슐화된 토큰은 AEM이 저장소에 액세스하지 않고 인증 정보를 오프라인으로 안전하게 만들고 확인할 수 있도록 하는 암호화 부분입니다. 이렇게 하면 모든 게시 인스턴스에서 인증 요청이 발생할 수 있으며 고정 연결이 필요하지 않습니다. 또한 모든 인증 요청에 대해 리포지토리에 액세스할 필요가 없으므로 인증 성능을 향상시키는 이점이 있습니다.

아래에 MongoMK 작성자 및 TarMK 게시 인스턴스를 사용하여 지리적으로 분산된 배포에서 이 작업이 어떻게 작동하는지 확인할 수 있습니다.

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>캡슐화된 토큰은 인증에 대한 것입니다. 따라서 저장소에 액세스할 필요 없이 쿠키의 유효성을 확인할 수 있습니다. 그러나 사용자가 모든 인스턴스에 존재하며 해당 사용자 아래에 저장된 정보에 모든 인스턴스가 액세스할 수 있어야 합니다.
>
>예를 들어, 캡슐화된 토큰이 작동하는 방식으로 인해 새 사용자가 게시 인스턴스 번호 1에 만들어지는 경우 게시 번호 2에서 성공적으로 인증됩니다. 사용자가 두 번째 게시 인스턴스에 없는 경우 요청이 계속 성공하지 못합니다.

## 캡슐화된 토큰 구성 {#configuring-the-encapsulated-token}

>[!NOTE]
>사용자를 동기화하고 토큰 인증을 사용하는 모든 인증 핸들러(SAML 및 OAuth 등)는 다음과 같은 경우에만 캡슐화된 토큰과 작동합니다.
>
>* 고정 세션이 활성화되거나
>
>* 동기화가 시작될 때 사용자가 AEM에 이미 만들어져 있습니다. 즉, 핸들러가 있는 상황에서는 캡슐화된 토큰이 지원되지 않습니다 **만들기** 동기화 프로세스 중에 사용자가 사용됩니다.


캡슐화된 토큰을 구성할 때 고려해야 할 몇 가지 사항이 있습니다.

1. 암호화 관련 때문에 모든 인스턴스는 동일한 HMAC 키를 가져야 합니다. AEM 6.3 이후 주요 자료는 더 이상 저장소에 저장되지 않고 실제 파일 시스템에 저장됩니다. 이러한 점을 염두에 두고 키를 복제하는 가장 좋은 방법은 키를 복제할 소스 인스턴스의 파일 시스템에서 타겟 인스턴스의 SIS(Server Control Center Server Node Server Server Load Manager) 로 키를 복사하는 것입니다. 아래의 &quot;HMAC 키 복제&quot;에서 자세한 내용을 참조하십시오.
1. 캡슐화된 토큰을 활성화해야 합니다. 이 작업은 웹 콘솔을 통해 수행할 수 있습니다.

### HMAC 키 복제 {#replicating-the-hmac-key}

인스턴스 간에 키를 복제하려면 다음을 수행해야 합니다.

1. 복사할 주요 자료가 포함된 AEM 인스턴스(일반적으로 작성자 인스턴스)에 액세스합니다.
1. 을(를) 찾습니다 `com.adobe.granite.crypto.file` 로컬 파일 시스템에 번들로 구성합니다. 예를 들어, 이 경로 아래에서:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25`

   다음 `bundle.info` 각 폴더 내의 파일은 번들 이름을 식별합니다.

1. 데이터 폴더로 이동합니다. 예:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. HMAC 및 마스터 파일을 복사합니다.
1. 그런 다음 HMAC 키를 복제할 대상 인스턴스로 이동하여 데이터 폴더로 이동합니다. 예:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle25/data`

1. 이전에 복사한 두 파일을 붙여넣습니다.
1. [암호화 번들 새로 고침](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) target 인스턴스가 이미 실행 중인 경우.

1. 키를 복제할 모든 인스턴스에 대해 위의 단계를 반복합니다.

#### 캡슐화된 토큰 활성화 {#enabling-the-encapsulated-token}

HMAC 키가 복제되면 웹 콘솔을 통해 캡슐화된 토큰을 활성화할 수 있습니다.

1. 브라우저를 `https://serveraddress:port/system/console/configMgr`
1. 라는 항목을 찾습니다. **Adobe Granite 토큰 인증 핸들러** 클릭하여 선택합니다.
1. 다음 창에서 **캡슐화된 토큰 지원 사용** 상자 및 누르기 **저장**.
