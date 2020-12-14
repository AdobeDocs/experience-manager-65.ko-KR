---
title: 캡슐화된 토큰 지원
seo-title: 캡슐화된 토큰 지원
description: AEM에서 캡슐화된 토큰 지원에 대해 알아봅니다.
seo-description: AEM에서 캡슐화된 토큰 지원에 대해 알아봅니다.
uuid: a7c6f269-bb5a-49ba-abef-ea029202ab6d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 2c263c0d-2521-49df-88ba-f304a25af8ab
translation-type: tm+mt
source-git-commit: 215f062f80e7abfe35698743ce971394d01d0ed6
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---


# 캡슐화된 토큰 지원{#encapsulated-token-support}

## 소개 {#introduction}

기본적으로 AEM은 토큰 인증 핸들러를 사용하여 각 요청을 인증합니다. 그러나 인증 요청을 처리하기 위해 토큰 인증 처리기는 모든 요청에 대해 저장소에 대한 액세스를 필요로 합니다. 이러한 경우는 쿠키를 인증 상태를 유지하는 데 사용하기 때문에 발생합니다. 논리적으로, 상태는 후속 요청을 검증하기 위해 저장소에 지속되어야 합니다. 따라서 인증 메커니즘이 상태 저장됨을 의미합니다.

이는 수평 확장성을 위해 특히 중요합니다. 아래에 설명된 게시 팜과 같은 다중 인스턴스 설정에서는 최적의 방식으로 부하 분산을 수행할 수 없습니다. 상태 저장 인증을 사용하는 경우 사용자가 처음 인증된 인스턴스에서만 지속적인 인증 상태를 사용할 수 있습니다.

![chlimage_1-33](assets/chlimage_1-33a.png)

다음 시나리오를 예로 들어 보십시오.

게시 인스턴스 1에서 사용자를 인증할 수 있지만, 후속 요청이 인스턴스 2로 이동하는 경우, 게시 1의 저장소에 유지되었고 게시 2에는 자체 저장소가 있으므로 해당 인스턴스에는 지속적인 인증 상태가 없습니다.

이 문제의 해결 방법은 로드 밸런서 수준에서 고정 연결을 구성하는 것입니다. 고정 연결을 사용하면 사용자가 항상 동일한 게시 인스턴스로 이동됩니다. 따라서 진정한 최적 부하 균형은 불가능합니다.

게시 인스턴스를 사용할 수 없게 되면 해당 인스턴스에서 인증된 모든 사용자는 세션을 잃게 됩니다. 인증 쿠키의 유효성을 검사하려면 저장소 액세스가 필요하기 때문입니다.

## 캡슐화된 토큰 {#stateless-authentication-with-the-encapsulated-token}이(가) 있는 상태 없는 인증

수평 확장성을 위한 솔루션은 AEM의 새로운 캡슐화된 토큰 지원을 사용하여 상태 비저장 인증입니다.

캡슐화된 토큰은 저장소에 액세스하지 않고도 AEM에서 인증 정보를 오프라인으로 안전하게 만들고 확인할 수 있도록 하는 암호화 기능입니다. 이렇게 하면 고정 연결이 필요 없이 모든 게시 인스턴스에서 인증 요청이 발생할 수 있습니다. 또한 모든 인증 요청에 대해 저장소에 액세스할 필요가 없으므로 인증 성능을 향상시킬 수 있습니다.

다음과 같이 MongoMK 작성자 및 TarMK 게시 인스턴스가 있는 지리적으로 분산된 배포에서 이러한 작업이 어떻게 이루어지는지 확인할 수 있습니다.

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
>캡슐화된 토큰은 인증에 대한 것입니다. 따라서 저장소에 액세스하지 않고도 쿠키의 유효성을 확인할 수 있습니다. 그러나 사용자가 모든 인스턴스에 존재하며 해당 사용자 아래에 저장된 정보에 모든 인스턴스에서 액세스할 수 있어야 합니다.
>
>예를 들어 새 사용자가 게시 인스턴스 번호 1에 작성되면 캡슐화된 토큰이 작동하는 방식 때문에 2번 게시에서 성공적으로 인증됩니다. 사용자가 두 번째 게시 인스턴스에 존재하지 않는 경우 요청은 여전히 성공적이지 않습니다.


## 캡슐화된 토큰 {#configuring-the-encapsulated-token} 구성

>[!NOTE]
>사용자를 동기화하고 토큰 인증(예: SAML 및 OAuth)에 의존하는 모든 인증 핸들러는 다음과 같은 경우 캡슐화된 토큰에서만 작동합니다.
>
>* 고정 세션이 활성화되거나
   >
   >
* 동기화가 시작되면 사용자가 이미 AEM에서 만들어집니다. 즉, 동기화 프로세스 동안 핸들러 **create** 사용자가 있을 때는 캡슐화된 토큰이 지원되지 않습니다.


캡슐화된 토큰을 구성할 때 고려해야 할 사항은 다음과 같습니다.

1. 암호 암호화와 관련되어 있기 때문에 모든 인스턴스는 동일한 HMAC 키를 가져야 합니다. AEM 6.3부터는 주요 자료가 더 이상 저장소에 저장되지 않고 실제 파일 시스템에 저장됩니다. 이 점을 염두에 두고 키를 복제하는 가장 좋은 방법은 키를 복제할 대상 인스턴스의 파일 시스템에서 해당 키를 복제할 대상 인스턴스의 파일 시스템으로 복사하는 것입니다. 아래의 &quot;HMAC 키 복제&quot;에서 자세한 내용을 참조하십시오.
1. 캡슐화된 토큰을 활성화해야 합니다. 이 작업은 웹 콘솔을 통해 수행할 수 있습니다.

### HMAC 키 {#replicating-the-hmac-key} 복제

HMAC 키는 저장소에 `/etc/key`의 이진 속성으로 있습니다. 옆에 있는 **보기** 링크를 눌러 별도로 다운로드할 수 있습니다.

![chlimage_1-35](assets/chlimage_1-35a.png)

인스턴스 간에 키를 복제하려면 다음을 수행해야 합니다.

1. 복사할 주요 자료가 포함된 작성자 인스턴스인 AEM 인스턴스에 액세스합니다.
1. 로컬 파일 시스템에서 `com.adobe.granite.crypto.file` 번들을 찾습니다. 예를 들어 이 경로 아래에서 다음을 수행합니다.

   * &lt;author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21

   각 폴더 내의 `bundle.info` 파일은 번들 이름을 식별합니다.

1. 데이터 폴더로 이동합니다. 예:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. HMAC 및 마스터 파일을 복사합니다.
1. 그런 다음 HMAC 키를 복제할 대상 인스턴스로 이동하여 데이터 폴더로 이동합니다. 예:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 이전에 복사한 두 파일을 붙여넣습니다.
1. [대상 인스턴스가 이미 실행 ](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 중인 경우 Crypto Bundleb를 새로 고칩니다.

1. 키를 복제할 모든 인스턴스에 대해 위의 단계를 반복합니다.

#### 캡슐화된 토큰 {#enabling-the-encapsulated-token} 활성화

HMAC 키가 복제되면 웹 콘솔을 통해 캡슐화된 토큰을 활성화할 수 있습니다.

1. 브라우저를 `https://serveraddress:port/system/console/configMgr`으로 가리킵니다.
1. **Day CRX 토큰 인증 처리기**&#x200B;라는 항목을 찾아 클릭합니다.
1. 다음 창에서 **캡슐화된 토큰 지원 활성화** 상자에 확인 표시를 하고 **저장**&#x200B;을 누릅니다.

