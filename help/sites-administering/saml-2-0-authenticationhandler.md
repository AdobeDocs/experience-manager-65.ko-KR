---
title: SAML 2.0 인증 핸들러
seo-title: SAML 2.0 Authentication Handler
description: AEM의 SAML 2.0 인증 핸들러에 대해 알아봅니다.
seo-description: Learn about the SAML 2.0 Authentication Handler in AEM.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---

# SAML 2.0 인증 핸들러{#saml-authentication-handler}

AEM은 와 함께 제공됩니다 [SAML](https://saml.xml.org/saml-specifications) 인증 처리기입니다. 이 처리기는 [SAML](https://saml.xml.org/saml-specifications) 2.0 인증 요청 프로토콜(Web-SSO 프로필) `HTTP POST` 바인딩.

다음을 지원합니다.

* 메시지 서명 및 암호화
* 사용자 자동 생성
* AEM의 기존 그룹과 그룹 동기화
* 서비스 공급자 및 ID 공급자가 인증을 시작했습니다.

이 처리기는 암호화된 SAML 응답 메시지를 사용자 노드에 저장합니다( `usernode/samlResponse`)를 사용하여 서드파티 서비스 제공업체와의 원활한 통신을 지원할 수 있습니다.

>[!NOTE]
>
>다음을 참조하십시오 [AEM과 SAML 통합 데모](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html).

## SAML 2.0 인증 핸들러 구성 {#configuring-the-saml-authentication-handler}

다음 [웹 콘솔](/help/sites-deploying/configuring-osgi.md) 에 대한 액세스 권한 제공 [SAML](https://saml.xml.org/saml-specifications) 2.0 인증 처리기 구성을 호출했습니다. **Adobe Granite SAML 2.0 Authentication Handler**. 다음 속성을 설정할 수 있습니다.

>[!NOTE]
>
>SAML 2.0 인증 핸들러는 기본적으로 비활성화되어 있습니다. 다음 속성 중 하나 이상을 설정하여 핸들러를 사용하도록 설정합니다.
>
>* ID 공급자 POST URL 또는 IDP URL.
>* 서비스 공급자 엔티티 ID.
>

>[!NOTE]
>
>SAML 어설션에 서명하고 선택적으로 암호화할 수 있습니다. 이 작업을 수행하려면 TrustStore에 ID 공급자의 공개 인증서 이상을 제공해야 합니다. 다음을 참조하십시오 [TrustStore에 IdP 인증서 추가](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) 섹션에 자세히 설명되어 있습니다.

**경로** Sling에서 이 인증 핸들러를 사용해야 하는 저장소 경로입니다. 비어 있는 경우 인증 핸들러가 비활성화됩니다.

**서비스 순위** 이 서비스를 호출하는 순서를 나타내는 OSGi 프레임워크 서비스 순위 값입니다. 값이 높을수록 우선 순위가 높은 정수 값입니다.

**IDP 인증서 별칭** 글로벌 Truststore에 있는 IdP 인증서 별칭. 이 속성이 비어 있으면 인증 핸들러가 비활성화됩니다. 설정 방법에 대해서는 아래의 &quot;AEM TrustStore에 IdP 인증서 추가&quot; 장을 참조하십시오.

**IDP URL** SAML 인증 요청을에 전송해야 하는 IDP의 URL. 이 속성이 비어 있으면 인증 핸들러가 비활성화됩니다.

>[!CAUTION]
>
>ID 공급자 호스트 이름을 **Apache Sling Referrer 필터** OSGi 구성. 다음을 참조하십시오. [웹 콘솔](/help/sites-deploying/configuring-osgi.md) 섹션에 자세히 설명되어 있습니다.

**서비스 공급자 엔티티 ID** ID 공급자로 이 서비스 공급자를 고유하게 식별하는 ID입니다. 이 속성이 비어 있으면 인증 핸들러가 비활성화됩니다.

**기본 리디렉션** 인증 성공 후 리디렉션할 기본 위치입니다.

>[!NOTE]
>
>이 위치는 `request-path` 쿠키가 설정되지 않았습니다. 유효한 로그인 토큰 없이 구성된 경로 아래에 있는 페이지를 요청하면 요청된 경로가 쿠키에 저장됩니다
>그리고 인증이 완료되면 브라우저가 이 위치로 다시 리디렉션됩니다.

**User-ID 속성** CRX 저장소에서 사용자를 인증하고 만드는 데 사용되는 사용자 ID가 포함된 속성의 이름입니다.

>[!NOTE]
>
>사용자 ID를 다음에서 가져오지 않습니다. `saml:Subject` SAML 어설션 노드(단, 해당 노드) `saml:Attribute`.

**암호화 사용** 이 인증 처리기가 암호화된 SAML 어설션을 예상하는지 여부입니다.

**CRX 사용자 자동 생성** 인증 성공 후 저장소에 존재하지 않는 사용자를 자동으로 만들지 여부.

>[!CAUTION]
>
>CRX 사용자 자동 생성을 비활성화하면 사용자를 수동으로 만들어야 합니다.

**그룹에 추가** 인증 성공 후 사용자를 CRX 그룹에 자동으로 추가해야 하는지 여부.

**그룹 멤버십** 이 사용자를 추가해야 하는 CRX 그룹 목록이 포함된 saml:Attribute의 이름입니다.

## AEM TrustStore에 IdP 인증서 추가 {#add-the-idp-certificate-to-the-aem-truststore}

SAML 어설션에 서명하고 선택적으로 암호화할 수 있습니다. 이 작업을 수행하려면 저장소에 IdP의 공개 인증서 이상을 제공해야 합니다. 이렇게 하려면 다음을 수행해야 합니다.

1. 다음으로 이동 *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*
1. 누르기 **[!UICONTROL TrustStore 링크 만들기]**
1. TrustStore의 암호를 입력하고 키를 누릅니다. **[!UICONTROL 저장]**.
1. 클릭 **[!UICONTROL TrustStore 관리]**.
1. IdP 인증서를 업로드합니다.
1. 인증서 별칭 을 확인합니다. 별칭은 입니다. **[!UICONTROL admin#1436172864930]** 아래 예제에서.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## AEM 키 저장소에 서비스 공급자 키 및 인증서 체인 추가 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>아래 단계는 필수입니다. 그렇지 않으면 다음 예외가 throw됩니다. `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 이동: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. 편집 `authentication-service` 사용자.
1. 다음을 클릭하여 KeyStore 만들기 **KeyStore 만들기** 아래에 **계정 설정**.

>[!NOTE]
>
>아래 단계는 핸들러가 메시지를 서명하거나 해독할 수 있어야 하는 경우에만 필요합니다.

1. AEM용 인증서/키 쌍을 만듭니다. openssl을 통해 생성하는 명령은 아래 예와 유사해야 합니다.

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. DER 인코딩을 사용하여 키를 PKCS#8 형식으로 변환합니다. AEM 키 저장소에서 필요한 형식입니다.

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. 을(를) 클릭하여 개인 키 파일 업로드 **개인 키 파일 선택**.
1. 다음을 클릭하여 인증서 파일 업로드 **인증서 체인 파일 선택**.
1. 아래 그림과 같이 별칭을 할당합니다.

   ![chlimage_1-373](assets/chlimage_1-373.png)

## SAML에 대한 로거 구성 {#configure-a-logger-for-saml}

SAML을 잘못 구성하여 발생할 수 있는 모든 문제를 디버깅하도록 로거를 설정할 수 있습니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 웹 콘솔로 이동 *http://localhost:4502/system/console/configMgr*
1. 라는 항목을 검색하고 클릭합니다. **Apache Sling 로깅 로거 구성**
1. 다음 구성으로 로거를 만듭니다.

   * **로그 수준:** 디버그
   * **로그 파일:** logs/saml.log
   * **로거:** com.adobe.granite.auth.saml
