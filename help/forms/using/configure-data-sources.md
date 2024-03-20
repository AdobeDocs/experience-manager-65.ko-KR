---
title: 데이터 소스 구성
description: 양식 데이터 모델을 만들 수 있도록 다양한 유형의 데이터 소스를 구성하는 방법에 대해 알아봅니다.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 1%

---

# 데이터 소스 구성{#configure-data-sources}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html) |
| AEM 6.5 | 이 문서 |


![데이터 통합](do-not-localize/data-integeration.png)

AEM Forms 데이터 통합을 통해 서로 다른 데이터 소스를 구성하고 연결할 수 있습니다. 기본적으로 지원되는 유형은 다음과 같습니다. 하지만 사용자 정의가 거의 없으므로 다른 데이터 소스도 통합할 수 있습니다.

* 관계형 데이터베이스 - MySQL, Microsoft SQL Server, IBM DB2, Oracle RDBMS, postgreSQL 및 Sybase
* AEM 사용자 프로필
* RESTful 웹 서비스
* SOAP 기반 웹 서비스
* OData 서비스

데이터 통합은 OAuth2.0([인증 코드](https://oauth.net/2/grant-types/authorization-code/), [클라이언트 자격 증명](https://oauth.net/2/grant-types/client-credentials/)), 기본 인증 및 API 키 인증 유형은 즉시 사용할 수 있으며 웹 서비스에 액세스하기 위해 사용자 지정 인증을 구현할 수 있습니다. RESTful, SOAP 기반 및 OData 서비스는 AEM Cloud Service에 구성되어 있지만, 관계형 데이터베이스에 대한 JDBC 및 AEM 사용자 프로필에 대한 커넥터는 AEM 웹 콘솔에 구성되어 있습니다.

## 관계형 데이터베이스 구성 {#configure-relational-database}

AEM 웹 콘솔 구성을 사용하여 관계형 데이터베이스를 구성할 수 있습니다. 다음 작업을 수행합니다.

1. 다음 위치에서 AEM 웹 콘솔로 이동 `https://server:host/system/console/configMgr`.
1. 다음을 찾습니다. **[!UICONTROL Apache Sling 연결의 풀링된 데이터 소스]** 구성. 을(를) 선택하여 편집 모드로 구성을 엽니다.
1. 구성 대화 상자에서 다음과 같이 구성할 데이터베이스에 대한 세부 정보를 지정합니다.

   * 데이터 소스 이름
   * 데이터 소스 이름을 저장하는 데이터 소스 서비스 속성
   * JDBC 드라이버의 Java 클래스 이름
   * JDBC 연결 URI
   * JDBC 드라이버와의 연결을 설정하는 사용자 이름 및 암호

   >[!NOTE]
   >
   >데이터 소스를 구성하기 전에 암호와 같은 중요한 정보를 암호화해야 합니다. 암호화하려면:
   >
   > 1. https://&#39;으로 이동[server]:[포트]&#39;/system/console/crypto.
   > 1. 다음에서 **[!UICONTROL 일반 텍스트]** 필드, 암호화할 암호 또는 문자열을 지정하고 선택 **[!UICONTROL Protect]**.
   >
   >암호화된 텍스트는 구성에 지정할 수 있는 보호된 텍스트 필드에 나타납니다.

1. 사용 **[!UICONTROL 차입 시 테스트]** 또는 **[!UICONTROL 반환 시 테스트]** 를 사용하여 객체를 풀에서 및 로 각각 대여하거나 반환하기 전에 검증되도록 지정할 수 있습니다.
1. 다음에서 SQL SELECT 쿼리를 지정합니다 **[!UICONTROL 유효성 검사 쿼리]** 풀에서 연결의 유효성을 검사하는 필드입니다. 쿼리는 하나 이상의 행을 반환해야 합니다. 데이터베이스를 기반으로 다음 중 하나를 지정합니다.

   * 1(MySQL 및 MS SQL) 선택
   * 이중 (Oracle)에서 1 선택

1. 선택 **[!UICONTROL 저장]** 구성을 저장합니다.

   >[!NOTE]
   >
   > Forms 데이터 모델에 관계형 데이터베이스에 대해 예약된 키워드인 개체가 포함된 경우, 이로 인해 데이터 추가, 업데이트 또는 검색 문제가 발생할 수 있습니다. 따라서 양식 데이터 모델에서 이러한 개체를 사용하지 마십시오.

## AEM 사용자 프로필 구성 {#configure-aem-user-profile}

AEM 웹 콘솔에서 사용자 프로필 커넥터 구성을 사용하여 AEM 사용자 프로필을 구성할 수 있습니다. 다음 작업을 수행합니다.

1. https://&#39;에서 AEM 웹 콘솔로 이동합니다.[server]:[포트]&#39;system/console/configMgr.
1. 다음을 찾습니다. **[!UICONTROL AEM Forms 데이터 통합 - 사용자 프로필 커넥터 구성]** 을(를) 선택하고 을(를) 선택하여 편집 모드로 구성을 엽니다.
1. 사용자 프로필 커넥터 구성 대화 상자에서 사용자 프로필 속성을 추가, 제거 또는 업데이트할 수 있습니다. 지정된 속성은 양식 데이터 모델에서 사용할 수 있습니다. 사용자 프로필 속성을 지정하려면 다음 형식을 사용하십시오.

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   예:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >다음 **&#42;** 위의 예에서는 아래의 모든 노드를 나타냅니다. `profile/empLocation/` crxde 구조의 AEM 사용자 프로필에 있는 노드 즉, 양식 데이터 모델이 `city` 유형의 속성 `string` 의 모든 노드에 있음 `profile/empLocation/` 노드. 그러나 지정된 속성이 포함된 노드는 일관된 구조를 따라야 합니다.

1. 선택 **[!UICONTROL 저장]** 구성을 저장합니다.

## 클라우드 서비스 구성을 위한 폴더 구성 {#cloud-folder}

>[!NOTE]
>
RESTful, SOAP 및 OData 서비스에 대한 클라우드 서비스를 구성하려면 클라우드 서비스 폴더에 대한 구성이 필요합니다.

AEM의 모든 클라우드 서비스 구성은 `/conf` 폴더를 AEM 리포지토리에 추가합니다. 기본적으로 `conf` 폴더에는 `global` 클라우드 서비스 구성을 만들 수 있는 폴더입니다. 그러나 클라우드 구성에 대해서는 수동으로 활성화해야 합니다. 에서 추가 폴더를 만들 수도 있습니다. `conf` 클라우드 서비스 구성을 만들고 구성합니다.

클라우드 서비스 구성에 대한 폴더를 구성하려면 다음을 수행합니다.

1. **[!UICONTROL 도구 > 일반 > 구성 브라우저]**&#x200B;로 이동합니다.
   * 다음을 참조하십시오. [구성 브라우저](/help/sites-administering/configurations.md) 설명서 를 참조하십시오.
1. 클라우드 구성에 대한 전역 폴더를 활성화하려면 다음을 수행하거나 클라우드 서비스 구성에 대한 다른 폴더를 만들고 구성하려면 이 단계를 건너뜁니다.

   1. 다음에서 **[!UICONTROL 구성 브라우저]**&#x200B;를 선택하고 `global` 폴더 및 선택 **[!UICONTROL 속성]**.

   1. 다음에서 **[!UICONTROL 구성 속성]** 대화 상자, 활성화 **[!UICONTROL 클라우드 구성]**.

   1. 선택 **[!UICONTROL 저장 및 닫기]** 구성을 저장하고 대화 상자를 종료합니다.

1. 다음에서 **[!UICONTROL 구성 브라우저]**, 선택 **[!UICONTROL 만들기]**.
1. 다음에서 **[!UICONTROL 구성 만들기]** 대화 상자에서 폴더의 제목을 지정하고 활성화합니다. **[!UICONTROL 클라우드 구성]**.
1. 선택 **[!UICONTROL 만들기]** 을 클릭하여 클라우드 서비스 구성에 대해 활성화된 폴더를 만듭니다.

## RESTful 웹 서비스 구성 {#configure-restful-web-services}

RESTful 웹 서비스는 [Swagger 사양](https://swagger.io/specification/) Swagger 정의 파일의 JSON 또는 YAML 형식에서. AEM Cloud Services에서 RESTful 웹 서비스를 구성하려면 파일 시스템에 Swagger 파일이 있거나 파일이 호스팅되는 URL이 있는지 확인합니다.

RESTful 서비스를 구성하려면 다음을 수행합니다.

1. 다음으로 이동 **[!UICONTROL 도구 > Cloud Service > 데이터 소스]**. 클라우드 구성을 만들 폴더를 선택하려면 를 선택합니다.

   다음을 참조하십시오 [클라우드 서비스 구성을 위한 폴더 구성](../../forms/using/configure-data-sources.md#cloud-folder) 클라우드 서비스 구성을 위한 폴더 만들기 및 구성에 대한 정보를 제공합니다.

1. 선택 **[!UICONTROL 만들기]** 을(를) 열려면 **[!UICONTROL 데이터 소스 구성 만들기 마법사]**. 구성의 이름 및 제목(선택 사항)을 지정하고 다음을 선택합니다. **[!UICONTROL RESTful 서비스]** 다음에서 **[!UICONTROL 서비스 유형]** 드롭다운에서 필요한 경우 구성에 대한 썸네일 이미지를 검색하여 선택하고 **[!UICONTROL 다음]**.
1. RESTful 서비스에 대해 다음 세부 정보를 지정합니다.

   * Swagger 소스 드롭다운에서 URL 또는 파일 을 선택한 다음 그에 따라 Swagger 정의 파일에 Swagger URL 을 지정하거나 로컬 파일 시스템에서 Swagger 파일을 업로드합니다.
   * Swagger 소스 입력을 기반으로 다음 필드는 값으로 미리 채워집니다.

      * 체계: REST API에서 사용하는 전송 프로토콜입니다. 드롭다운 목록에 표시되는 구성표 유형의 수는 Swagger 소스에 정의된 구성표에 따라 다릅니다.
      * 호스트: REST API를 제공하는 호스트의 도메인 이름 또는 IP 주소입니다. 필수 필드입니다.
      * 기본 경로: 모든 API 경로의 URL 접두어. 선택 필드입니다.\
        필요한 경우 이러한 필드에 대해 미리 채워진 값을 편집합니다.

   * 인증 유형 선택 — 없음, OAuth2.0([인증 코드](https://oauth.net/2/grant-types/authorization-code/), [클라이언트 자격 증명](https://oauth.net/2/grant-types/client-credentials/)), 기본 인증, API 키, 사용자 지정 인증 또는 상호 인증 - RESTful 서비스에 액세스하여 인증에 대한 세부 정보를 제공합니다.

   다음을 선택하는 경우 **[!UICONTROL API 키]** 인증 유형으로 API 키 값을 지정합니다. API 키는 요청 헤더 또는 쿼리 매개 변수로 전송될 수 있습니다. 다음에서 다음 옵션 중 하나를 선택합니다 **[!UICONTROL 위치]** 드롭다운 목록을 나열하고 헤더 이름 또는 쿼리 매개 변수를 **[!UICONTROL 매개 변수 이름]** 필드입니다.

   다음을 선택하는 경우 **[!UICONTROL 상호 인증]** 인증 유형으로 다음을 참조하십시오. [RESTful 및 SOAP 웹 서비스를 위한 인증서 기반 상호 인증](#mutual-authentication).

1. 선택 **[!UICONTROL 만들기]** RESTful 서비스에 대한 클라우드 구성을 만듭니다.

### 성능을 최적화하기 위한 양식 데이터 모델 HTTP 클라이언트 구성 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 데이터 소스로 RESTful 웹 서비스와 통합할 때 양식 데이터 모델에 성능 최적화를 위한 HTTP 클라이언트 구성이 포함됩니다.
양식 데이터 모델 HTTP 클라이언트를 구성하려면 다음 단계를 수행하십시오.

1. 에 로그인 [!DNL Experience Manager Forms] 작성자 인스턴스 관리자 권한으로 [!DNL Experience Manager] 웹 콘솔 번들. 기본 URL은 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. 선택 **[!UICONTROL REST 데이터 소스에 대한 양식 데이터 모델 Http 클라이언트 구성]**.

1. 다음에서 [!UICONTROL REST 데이터 소스에 대한 양식 데이터 모델 Http 클라이언트 구성] 대화 상자:

   * 양식 데이터 모델과 RESTful 웹 서비스 간에 허용되는 최대 연결 수를 지정합니다. **[!UICONTROL 총 연결 제한]** 필드. 기본값은 20개 연결입니다.

   * 의 각 경로에 대해 허용되는 최대 연결 수를 지정합니다. **[!UICONTROL 경로당 연결 제한]** 필드. 기본값은 2개 연결입니다.

   * 지속 HTTP 연결이 활성 상태로 유지되는 기간을 **[!UICONTROL Keep alive]** 필드. 기본값은 15초입니다.

   * 기간을 지정하십시오. [!DNL Experience Manager Forms] 서버가 다음 위치에서 연결이 설정될 때까지 기다립니다. **[!UICONTROL 연결 시간 초과]** 필드. 기본값은 10초입니다.

   * 에 있는 두 데이터 패킷 간의 비활성 최대 기간을 지정합니다. **[!UICONTROL 소켓 시간 제한]** 필드. 기본값은 30초입니다.

## SOAP 웹 서비스 구성 {#configure-soap-web-services}

SOAP 기반 웹 서비스는 다음을 사용하여 설명합니다. [WSDL(웹 서비스 설명 언어) 사양](https://www.w3.org/TR/wsdl). AEM 클라우드 서비스에서 SOAP 기반 웹 서비스를 구성하려면 웹 서비스에 대한 WSDL URL이 있는지 확인하고 다음을 수행합니다.

1. 다음으로 이동 **[!UICONTROL 도구 > Cloud Service > 데이터 소스]**. 클라우드 구성을 만들 폴더를 선택하려면 를 선택합니다.

   다음을 참조하십시오 [클라우드 서비스 구성을 위한 폴더 구성](../../forms/using/configure-data-sources.md#cloud-folder) 클라우드 서비스 구성을 위한 폴더 만들기 및 구성에 대한 정보를 제공합니다.

1. 선택 **[!UICONTROL 만들기]** 을(를) 열려면 **[!UICONTROL 데이터 소스 구성 만들기 마법사]**. 구성의 이름 및 제목(선택 사항)을 지정하고 다음을 선택합니다. **[!UICONTROL SOAP 웹 서비스]** 다음에서 **[!UICONTROL 서비스 유형]** 드롭다운에서 필요한 경우 구성에 대한 썸네일 이미지를 검색하여 선택하고 **[!UICONTROL 다음]**.
1. SOAP 웹 서비스에 대해 다음을 지정하십시오.

   * 웹 서비스용 WSDL URL입니다.
   * 서비스 엔드포인트. WSDL에 언급된 서비스 끝점을 재정의하려면 이 필드에 값을 지정하십시오.
   * 인증 유형 선택 — 없음, OAuth2.0([인증 코드](https://oauth.net/2/grant-types/authorization-code/), [클라이언트 자격 증명](https://oauth.net/2/grant-types/client-credentials/)), 기본 인증, 사용자 지정 인증, X509 토큰 또는 상호 인증 — SOAP 서비스에 액세스하여 인증에 대한 세부 정보를 제공합니다.

     다음을 선택하는 경우 **[!UICONTROL X509 토큰]** 인증 유형으로 X509 인증서를 구성합니다. 자세한 내용은 [인증서 설정](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
에서 X509 인증서에 대한 KeyStore 별칭을 지정합니다. **[!UICONTROL 키 별칭]** 필드. 인증 요청이 유효한 상태로 유지될 때까지의 시간(초)을 **[!UICONTROL TTL(Time to Live)]** 필드. 메시지 본문 또는 타임스탬프 헤더 또는 둘 다에 서명하려면 선택합니다(선택적).

     다음을 선택하는 경우 **[!UICONTROL 상호 인증]** 인증 유형으로 다음을 참조하십시오. [RESTful 및 SOAP 웹 서비스를 위한 인증서 기반 상호 인증](#mutual-authentication).

1. 선택 **[!UICONTROL 만들기]** 를 클릭하여 SOAP 웹 서비스에 대한 클라우드 구성을 만듭니다.

## OData 서비스 구성 {#config-odata}

OData 서비스는 서비스 루트 URL로 식별됩니다. AEM Cloud Services에서 OData 서비스를 구성하려면 서비스에 대한 서비스 루트 URL이 있는지 확인하고 다음을 수행합니다.

>[!NOTE]
>
양식 데이터 모델 지원 [OData 버전 4](https://www.odata.org/documentation/).
온라인 또는 온프레미스에서 Microsoft Dynamics 365를 구성하는 방법에 대한 단계별 안내서는 다음을 참조하십시오. [Microsoft Dynamics OData 구성](/help/forms/using/ms-dynamics-odata-configuration.md).

1. 다음으로 이동 **[!UICONTROL 도구 > Cloud Service > 데이터 소스]**. 클라우드 구성을 만들 폴더를 선택하려면 를 선택합니다.

   다음을 참조하십시오 [클라우드 서비스 구성을 위한 폴더 구성](../../forms/using/configure-data-sources.md#cloud-folder) 클라우드 서비스 구성을 위한 폴더 만들기 및 구성에 대한 정보를 제공합니다.

1. 선택 **[!UICONTROL 만들기]** 을(를) 열려면 **[!UICONTROL 데이터 소스 구성 만들기 마법사]**. 구성의 이름 및 제목(선택 사항)을 지정하고 다음을 선택합니다. **[!UICONTROL OData 서비스]** 다음에서 **[!UICONTROL 서비스 유형]** 드롭다운에서 필요한 경우 구성에 대한 썸네일 이미지를 검색하여 선택하고 **[!UICONTROL 다음]**.
1. OData 서비스에 대해 다음 세부 정보를 지정합니다.

   * 구성할 OData 서비스의 서비스 루트 URL입니다.
   * 인증 유형 선택 — 없음, OAuth2.0([인증 코드](https://oauth.net/2/grant-types/authorization-code/), [클라이언트 자격 증명](https://oauth.net/2/grant-types/client-credentials/)), 기본 인증 또는 사용자 지정 인증 - OData 서비스에 액세스하여 인증에 대한 세부 정보를 제공합니다.

   >[!NOTE]
   >
   OData 끝점을 서비스 루트로 사용하여 Microsoft Dynamics 서비스와 연결하려면 OAuth 2.0 인증 유형을 선택하십시오.

1. 선택 **만들기** 를 클릭하여 OData 서비스에 대한 클라우드 구성을 만듭니다.

## RESTful 및 SOAP 웹 서비스를 위한 인증서 기반 상호 인증 {#mutual-authentication}

양식 데이터 모델에 대해 상호 인증을 활성화하면 데이터를 공유하기 전에 양식 데이터 모델을 실행하는 AEM 서버와 데이터 소스 모두 서로의 ID를 인증합니다. REST 및 SOAP 기반 연결(데이터 소스)에 대해 상호 인증을 사용할 수 있습니다. AEM Forms 환경에서 양식 데이터 모델에 대한 상호 인증을 구성하려면 다음 작업을 수행하십시오.

1. 개인 키(인증서)를에 업로드 [!DNL AEM Forms] 서버입니다. 개인 키를 업로드하려면:
   1. 에 로그인 [!DNL AEM Forms] 관리자인 서버입니다.
   1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**. 다음 항목 선택 `fd-cloudservice` 사용자 및 선택 **[!UICONTROL 속성]**.
   1. 를 엽니다. **[!UICONTROL 키 저장소]** 탭을 확장하고 **[!UICONTROL KeyStore 파일의 개인 키 추가]** 옵션을 선택하고 KeyStore 파일을 업로드한 다음 별칭, 암호를 지정하고 **[!UICONTROL 제출]**. 인증서가 업로드되었습니다.  개인 키 별칭은 인증서에 언급되어 있으며 인증서를 만드는 동안 설정됩니다.
1. 글로벌 Trust Store에 트러스트 인증서를 업로드합니다. 인증서를 업로드하려면:
   1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL Trust Store]**.
   1. 확장 **[!UICONTROL CER 파일에서 인증서 추가]** 옵션, 선택 **[!UICONTROL 인증서 파일 선택]**&#x200B;를 클릭하고 인증서를 업로드한 다음 을 선택합니다 **[!UICONTROL 제출]**.
1. 구성 [SOAP](#configure-soap-web-services) 또는 [RESTful](#configure-restful-web-services) 웹 서비스를 데이터 소스로 사용하고 선택 **[!UICONTROL 상호 인증]** 를 인증 유형으로 사용하십시오. 에 대해 여러 자체 서명된 인증서를 구성하는 경우 `fd-cloudservice` 사용자, 인증서의 키 별칭 이름을 지정합니다.

## 다음 단계 {#next-steps}

데이터 소스를 구성했습니다. 그런 다음 양식 데이터 모델을 만들거나 데이터 소스 없이 이미 양식 데이터 모델을 만든 경우 구성한 데이터 소스와 연결할 수 있습니다. 다음을 참조하십시오 [양식 데이터 모델 만들기](/help/forms/using/create-form-data-models.md) 을 참조하십시오.
