---
title: SAML 2.0 인증 핸들러
seo-title: SAML 2.0 인증 핸들러
description: AEM의 SAML 2.0 인증 핸들러에 대해 알아봅니다.
seo-description: AEM의 SAML 2.0 인증 핸들러에 대해 알아봅니다.
uuid: 51f97315-350a-42a4-af2c-2de87307c6ad
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ed09b5d-5089-43d2-b9d5-e7db57be5c02
exl-id: 8e54bccf-0ff1-448d-a237-ec42fd3bfa23
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 1%

---

# SAML 2.0 인증 핸들러{#saml-authentication-handler}

AEM은 [SAML](http://saml.xml.org/saml-specifications) 인증 핸들러를 사용하여 제공됩니다. 이 처리기는 `HTTP POST` 바인딩을 사용하여 [SAML](http://saml.xml.org/saml-specifications) 2.0 인증 요청 프로토콜(Web-SSO 프로필)을 지원합니다.

다음을 지원합니다.

* 메시지 서명 및 암호화
* 사용자 자동 생성
* 그룹 동기화는 AEM에서 기존 그룹에 있습니다.
* 서비스 공급자 및 ID 공급자가 인증을 시작했습니다.

이 처리기는 타사 서비스 공급자와의 통신을 용이하게 하기 위해 사용자 노드( `usernode/samlResponse`)에 암호화된 SAML 응답 메시지를 저장합니다.

>[!NOTE]
>
>AEM 및 SAML 통합 [에 대한 데모를 참조하십시오.](https://helpx.adobe.com/experience-manager/kb/simple-saml-demo.html)
>
>최종 커뮤니티 문서를 읽으려면 다음을 클릭합니다.[SAML과 Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/aem63_saml.html) 통합

## SAML 2.0 인증 핸들러 구성 {#configuring-the-saml-authentication-handler}

[웹 콘솔](/help/sites-deploying/configuring-osgi.md)은 [SAML](http://saml.xml.org/saml-specifications) 2.0 인증 핸들러 구성(**Granite SAML 2.0 인증 핸들러** Adobe)에 대한 액세스 권한을 제공합니다. 다음 속성을 설정할 수 있습니다.

>[!NOTE]
>
>SAML 2.0 인증 핸들러는 기본적으로 비활성화되어 있습니다. 핸들러를 사용하려면 다음 속성 중 하나 이상을 설정해야 합니다.
>
>* ID 공급자 POST URL입니다.
>* 서비스 공급자 엔티티 ID입니다.

>



>[!NOTE]
>
>SAML 어설션은 서명되며 선택적으로 암호화할 수 있습니다. 이 작업을 수행하려면 TrustStore에서 Indentity Provider의 공개 인증서를 제공해야 합니다. 자세한 내용은 [TrustStore](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore) 섹션에 IdP 인증서 추가 를 참조하십시오.

**** Sling에서 이 인증 핸들러를 사용해야 하는 경로 저장소 경로입니다. 이 값이 비어 있으면 인증 처리기가 비활성화됩니다.

**서비스** 등급OSGi 프레임워크 서비스 등급 값에서 이 서비스를 호출할 순서를 나타냅니다. 높은 값이 높은 우선 순위를 지정하는 정수 값입니다.

**IDP 인증서** 별칭글로벌 truststore에서 IdP 인증서의 별칭입니다. 이 속성이 비어 있으면 인증 처리기가 비활성화됩니다. 설정 방법에 대해서는 아래의 &quot;AEM TrustStore에 IdP 인증서 추가&quot; 장을 참조하십시오.

**SAML** 인증 요청을 전송해야 하는 IDP의 ID 공급자 URL. 이 속성이 비어 있으면 인증 처리기가 비활성화됩니다.

>[!CAUTION]
>
>ID 공급자 호스트 이름을 **Apache Sling Referrer Filter** OSGi 구성에 추가해야 합니다. 자세한 내용은 [웹 콘솔](/help/sites-deploying/configuring-osgi.md) 섹션을 참조하십시오.

**ID 공급자** 로 이 서비스 공급자를 고유하게 식별하는 서비스 공급자 엔터티 ID입니다. 이 속성이 비어 있으면 인증 처리기가 비활성화됩니다.

**기본** 리디렉션인증 성공 후 리디렉션할 기본 위치입니다.

>[!NOTE]
>
>이 위치는 `request-path` 쿠키가 설정되지 않은 경우에만 사용됩니다. 유효한 로그인 토큰 없이 구성된 경로 아래의 페이지를 요청하면 요청된 경로가 쿠키에 저장됩니다
>그리고 인증 성공 후 브라우저가 이 위치로 다시 리디렉션됩니다.

**User-ID** 속성CRX 저장소에서 사용자를 인증하고 만드는 데 사용되는 사용자 ID가 들어 있는 속성의 이름입니다.

>[!NOTE]
>
>사용자 ID는 SAML 어설션의 `saml:Subject` 노드에서 가져오지 않고 이 `saml:Attribute`에서 가져옵니다.

**EncryptionEncryption** 이 인증 처리기에 암호화된 SAML 어설션이 필요한지 여부를 사용합니다.

**CRX 사용자 자동** 만들기인증 성공 후 저장소에서 존재하지 않는 사용자를 자동으로 만들지 여부를 선택합니다.

>[!CAUTION]
>
>CRX 사용자를 자동으로 만들 수 없게 설정된 경우 사용자를 수동으로 만들어야 합니다.

**그룹에** 추가인증 성공 후 사용자를 CRX 그룹에 자동으로 추가할지 여부를 지정합니다.

**그룹** 멤버십이 사용자가 추가되어야 하는 CRX 그룹 목록이 포함된 saml:Attribute의 이름입니다.

## AEM TrustStore {#add-the-idp-certificate-to-the-aem-truststore}에 IdP 인증서를 추가합니다.

SAML 어설션은 서명되며 선택적으로 암호화할 수 있습니다. 이를 수행하려면 저장소에 IdP의 공개 인증서를 제공해야 합니다. 이를 수행하려면 다음을 수행해야 합니다.

1. *http:/serveraddress:serverport/libs/granite/security/content/truststore.html*&#x200B;로 이동합니다.
1. **[!UICONTROL Create TrustStore 링크]** 키를 누릅니다
1. TrustStore의 암호를 입력하고 **[!UICONTROL Save]** 키를 누릅니다.
1. **[!UICONTROL Manage TrustStore]**&#x200B;를 클릭합니다.
1. IdP 인증서를 업로드합니다.
1. 인증서 별칭을 확인합니다. 별칭은 아래 예에서 **[!UICONTROL admin#1436172864930]**&#x200B;입니다.

   ![chlimage_1-372](assets/chlimage_1-372.png)

## 서비스 공급자 키 및 인증서 체인을 AEM 키 저장소 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}에 추가합니다.

>[!NOTE]
>
>아래 단계는 필수입니다. 그렇지 않으면 다음 예외가 발생합니다.`com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. 이동 위치:[http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html)
1. `authentication-service` 사용자를 편집합니다.
1. **계정 설정** 아래에 있는 **Create KeyStore**&#x200B;를 클릭하여 KeyStore를 만듭니다.

>[!NOTE]
>
>아래 단계는 처리기가 메시지를 서명하거나 해독할 수 있어야 하는 경우에만 필요합니다.

1. **개인 키 파일 선택**&#x200B;을 클릭하여 개인 키 파일을 업로드합니다. 키는 DER 인코딩이 있는 PKCS#8 형식이어야 합니다.
1. **인증서 체인 파일 선택**&#x200B;을 클릭하여 인증서 파일을 업로드합니다.
1. 아래와 같이 별칭을 할당합니다.

   ![chlimage_1-373](assets/chlimage_1-373.png)

## SAML {#configure-a-logger-for-saml}에 대한 로거 구성

SAML을 잘못 구성하여 발생할 수 있는 문제를 디버깅하기 위해 로거를 설정할 수 있습니다. 다음을 통해 이 작업을 수행할 수 있습니다.

1. 웹 콘솔로 이동(*http://localhost:4502/system/console/configMgr*)
1. **Apache Sling Logging Configuration** 이라는 항목을 검색하고 클릭합니다.
1. 다음 구성으로 로거를 만듭니다.

   * **로그 수준:** 디버그
   * **로그 파일:** logs/saml.log
   * **로거:** com.adobe.granite.auth.saml
