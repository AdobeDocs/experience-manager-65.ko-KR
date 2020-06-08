---
title: SAML 2.0 인증 처리기
seo-title: SAML 2.0 인증 처리기
description: AEM의 SAML 2.0 인증 핸들러에 대해 알아봅니다.
seo-description: AEM의 SAML 2.0 인증 핸들러에 대해 알아봅니다.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
translation-type: tm+mt
source-git-commit: d559a15e3c1c65c39e38935691835146f54a356e
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# SAML 2.0 인증 처리기{#saml-authentication-handler}

AEM은 [SAML](http://saml.xml.org/saml-specifications) 인증 핸들러와 함께 제공됩니다. 이 처리기는 바인딩을 사용하여 [SAML](http://saml.xml.org/saml-specifications) 2.0 인증 요청 프로토콜(Web-SSO 프로필)을 `HTTP POST` 지원합니다.

다음을 지원합니다.

* 메시지 서명 및 암호화
* 자동 사용자 생성
* AEM에서 기존 그룹에 동기화
* 서비스 제공자 및 ID 공급자가 인증을 시작했습니다.

이 처리기는 타사 서비스 제공자와의 통신을 용이하게 하기 위해 사용자 노드( `usernode/samlResponse`)에 암호화된 SAML 응답 메시지를 저장합니다.

>[!NOTE]
>
>AEM [및 SAML 통합에 대한 데모를 참조하십시오](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html).
>
>엔드 투 엔드 커뮤니티 아티클을 읽으려면 다음을 클릭합니다. [Adobe Experience Manager와 SAML 통합](https://helpx.adobe.com/experience-manager/using/aem63_saml.html).

## SAML 2.0 인증 처리기 구성 {#configuring-the-saml-authentication-handler}

웹 [콘솔에서는](/help/sites-deploying/configuring-osgi.md) [Adobe Granite SAML](http://saml.xml.org/saml-specifications) 2.0 Authentication Handler라는 **SAML** 2.0 인증 처리기 구성에 대한 액세스 권한을 제공합니다. 다음 속성을 설정할 수 있습니다.

>[!NOTE]
>
>SAML 2.0 인증 핸들러는 기본적으로 비활성화되어 있습니다. 핸들러를 활성화하려면 다음 속성 중 적어도 하나를 설정해야 합니다.
>
>* ID 공급자 게시물 URL.
>* 서비스 공급자 엔티티 ID.

>



>[!NOTE]
>
>SAML 어설션은 서명되며 선택적으로 암호화될 수 있습니다. 이를 수행하려면 TrustStore에서 Indentity Provider의 공개 인증서를 제공해야 합니다. 자세한 [내용은 TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) 섹션에 IdP 인증서 추가를 참조하십시오.

**Sling에서 이 인증 처리기를 사용해야 하는 경로** 저장소 경로입니다. 이 값이 비어 있으면 인증 처리기가 비활성화됩니다.

**서비스 등급** OSGi Framework 서비스 등급 값으로 이 서비스를 호출할 순서를 나타냅니다. 높은 값이 높은 우선 순위를 지정하는 정수 값입니다.

**IDP 인증서 별칭** 전역 truststore에 있는 IdP 인증서의 별칭입니다. 이 속성이 비어 있으면 인증 처리기가 비활성화됩니다. 설정하는 방법은 아래의 &quot;AEM TrustStore에 IdP 인증서 추가&quot; 장을 참조하십시오.

**SAML 인증 요청을 보내야 하는 IDP의 ID 공급자 URL** URL. 이 속성이 비어 있으면 인증 처리기가 비활성화됩니다.

>[!CAUTION]
>
>ID 공급자 호스트 이름은 **Apache Sling Referrer 필터 OSGi 구성에** 추가해야 합니다. 자세한 내용은 [웹 콘솔](/help/sites-deploying/configuring-osgi.md) 섹션을 참조하십시오.

**ID 공급자로 이 서비스 공급자를 고유하게 식별하는 서비스 공급자 엔티티 ID** ID. 이 속성이 비어 있으면 인증 처리기가 비활성화됩니다.

**기본 리디렉션** 성공적인 인증 후 리디렉션할 기본 위치입니다.

>[!NOTE]
>
>이 위치는 쿠키가 설정되지 않은 경우에만 `request-path` 사용됩니다. 유효한 로그인 토큰이 없는 구성된 경로 아래에 페이지를 요청하면 요청된 경로가 쿠키에 저장됩니다
>그리고 인증 성공 후 브라우저가 이 위치로 다시 리디렉션됩니다.

**사용자-ID 속성** CRX 저장소에서 사용자를 인증하고 만드는 데 사용되는 사용자 ID가 포함된 속성의 이름입니다.

>[!NOTE]
>
>사용자 ID는 SAML 어설션의 노드 `saml:Subject` 에서 가져오지 않고 여기에서 가져올 수 있습니다 `saml:Attribute`.

**암호화** 사용 이 인증 처리기에 암호화된 SAML 어설션이 필요한지 여부를 확인하십시오.

**CRX 사용자** 자동 생성 인증 성공 후 저장소에 존재하지 않는 사용자를 자동으로 만들지 여부를 나타냅니다.

>[!CAUTION]
>
>CRX 사용자를 자동으로 만들 수 없는 경우 사용자를 수동으로 만들어야 합니다.

**그룹에** 추가 인증 성공 후 사용자를 CRX 그룹에 자동으로 추가할지 여부

**그룹 구성원** 이 사용자가 추가되어야 하는 CRX 그룹 목록이 포함된 saml:Attribute의 이름입니다.

## AEM TrustStore에 IdP 인증서 추가 {#add-the-idp-certificate-to-the-aem-truststore}

SAML 어설션은 서명되며 선택적으로 암호화될 수 있습니다. 이를 수행하려면 보관소에 IdP의 공용 인증서를 제공해야 합니다. 이를 위해서는 다음을 수행해야 합니다.

1. http:/serveraddress:serverport/libs/granite/security/content/truststore.html으로 *이동*
1. TrustStore **[!UICONTROL 만들기 링크를 누릅니다.]**
1. TrustStore의 암호를 입력하고 **[!UICONTROL 저장을 누릅니다]**.
1. TrustStore **[!UICONTROL 관리를 클릭합니다]**.
1. IdP 인증서를 업로드합니다.
1. 인증서 별칭에 주목하십시오. 별칭은 아래 **[!UICONTROL 예에서 admin#1436172864930입니다]** .

   ![chlimage_1-372](assets/chlimage_1-372.png)

## AEM 키 저장소에 서비스 공급자 키 및 인증서 체인 추가 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>아래 단계는 필수입니다. 그렇지 않으면 다음 예외가 발생합니다. `com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 이동: [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. 사용자를 `authentication-service` 편집합니다.
1. 계정 설정에서 **키 스토어** 만들기를 클릭하여 **키 스토어**&#x200B;만들기를만듭니다.

>[!NOTE]
>
>아래 단계는 핸들러가 메시지를 서명하거나 해독할 수 있어야 하는 경우에만 필요합니다.

1. 개인 키 파일 선택을 클릭하여 **개인 키 파일을 업로드합니다**. 키는 DER 인코딩이 있는 PKCS#8 형식이어야 합니다.
1. 인증서 체인 파일 선택을 클릭하여 **인증서 파일을 업로드합니다**.
1. 아래와 같이 별칭을 지정합니다.

   ![chlimage_1-373](assets/chlimage_1-373.png)

## SAML용 로거 구성 {#configure-a-logger-for-saml}

SAML을 잘못 구성하여 발생할 수 있는 모든 문제를 디버깅하기 위해 로거를 설정할 수 있습니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 웹 콘솔(http://localhost:4502/system/console/configMgr)으로 *이동*
1. Apache Sling Logging **Logger Configuration이라는 항목을 검색하여 클릭합니다.**
1. 다음과 같은 구성으로 로거를 만듭니다.

   * **로그 수준:** 디버그
   * **로그 파일:** logs/saml.log
   * **로거:** com.adobe.granite.auth.saml

