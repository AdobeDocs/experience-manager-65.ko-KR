---
title: 데이터 소스 구성
seo-title: 데이터 소스 구성
description: 다양한 유형의 데이터 소스를 구성하고 이를 활용하여 양식 데이터 모델을 만드는 방법을 살펴볼 수 있습니다.
seo-description: 다양한 유형의 데이터 소스를 구성하고 이를 활용하여 양식 데이터 모델을 만드는 방법을 살펴볼 수 있습니다.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 0%

---


# 데이터 소스 구성{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms 데이터 통합을 사용하면 서로 다른 데이터 소스를 구성하고 연결할 수 있습니다. 기본적으로 지원되는 유형은 다음과 같습니다. 그러나 사용자 정의가 거의 이루어지지 않는 경우 다른 데이터 소스도 통합할 수 있습니다.

* 관계형 데이터베이스 - MySQL, Microsoft SQL Server, IBM DB2 및 Oracle RDBMS
* AEM 사용자 프로필
* RESTful 웹 서비스
* SOAP 기반의 웹 서비스
* OData 서비스

데이터 통합은 즉시 사용 가능한 OAuth2.0, 기본 인증 및 API 키 인증 유형을 지원하며, 웹 서비스에 액세스하기 위한 사용자 정의 인증을 구현할 수 있습니다. RESTful, SOAP 기반 및 OData 서비스는 AEM Cloud Services에서 구성되지만 관계형 데이터베이스의 JDBC 및 AEM 사용자 프로필의 커넥터는 AEM 웹 콘솔에서 구성됩니다.

## 관계형 데이터베이스 구성 {#configure-relational-database}

AEM 웹 콘솔 구성을 사용하여 관계형 데이터베이스를 구성할 수 있습니다. 다음을 수행합니다.

1. AEM 웹 콘솔(https://server:host/system/console/configMgr)으로 이동합니다.
1. Apache Sling **[!UICONTROL 연결 풀링된 DataSource 구성을]** 찾습니다. 을 눌러 편집 모드에서 구성을 엽니다.
1. 구성 대화 상자에서 구성할 데이터베이스의 세부 정보(예:

   * 데이터 원본 이름
   * 데이터 원본 이름을 저장하는 데이터 원본 서비스 속성
   * JDBC 드라이버용 Java 클래스 이름
   * JDBC 연결 URI
   * JDBC 드라이버와의 연결을 설정하는 사용자 이름 및 암호

   >[!NOTE]
   >
   >데이터 소스를 구성하기 전에 암호와 같은 중요한 정보를 암호화해야 합니다. 암호화하려면:
   >
   >    
   >    
   >    1. https://&#39;[server]:[port]&#39;/system/console/crypto로 이동합니다.
   >    1. 일반 **[!UICONTROL 텍스트]** 필드에서 암호나 암호화할 문자열을 지정하고 **[!UICONTROL Protect을]**&#x200B;누릅니다.

   >    
   >    
   >    
   >암호화된 텍스트는 구성에서 지정할 수 있는 보호된 텍스트 필드에 나타납니다.

1. [ **[!UICONTROL 반환]** 시 차입 **[!UICONTROL 또는]** 테스트]를 활성화하여 개체가 대출 또는 풀로부터 반환되기 전에 확인되도록 지정합니다.
1. [유효성 검사 쿼리] **[!UICONTROL 필드에 SQL SELECT]** 쿼리를 지정하여 풀의 연결을 확인합니다. 쿼리는 하나 이상의 행을 반환해야 합니다. 데이터베이스를 기준으로 다음 중 하나를 지정합니다.

   * 1을 선택합니다(MySQL 및 MS SQL).
   * 이중 SELECT 1(Oracle)

1. 저장을 **[!UICONTROL 눌러]** 구성을 저장합니다.

## AEM 사용자 프로필 구성 {#configure-aem-user-profile}

AEM 웹 콘솔의 사용자 프로필 커넥터 구성을 사용하여 AEM 사용자 프로필을 구성할 수 있습니다. 다음을 수행합니다.

1. https://&#39;[server]:[port]&#39;system/console/configMgr의 AEM 웹 콘솔로 이동합니다.
1. AEM Forms **[!UICONTROL 데이터 통합 - 사용자 프로필 커넥터 구성을]** 찾고 탭하여 편집 모드에서 구성을 엽니다.
1. 사용자 프로필 커넥터 구성 대화 상자에서 사용자 프로필 속성을 추가, 제거 또는 업데이트할 수 있습니다. 지정한 속성은 양식 데이터 모델에서 사용할 수 있습니다. 다음 형식을 사용하여 사용자 프로필 속성을 지정합니다.

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   예:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >위 ***** 예제의 경우 CRXDE 구조의 AEM 사용자 프로필에서 노드 아래에 있는 `profile/empLocation/` 모든 노드를 나타냅니다. 즉, 양식 데이터 모델은 노드 아래의 임의 노드에 `city` 있는 유형 `string` 의 속성에 액세스할 수 `profile/empLocation/` 있습니다. 그러나 지정된 속성을 포함하는 노드는 일관된 구조를 따라야 합니다.

1. 저장을 **[!UICONTROL 눌러]** 구성을 저장합니다.

## 클라우드 서비스 구성을 위한 폴더 구성 {#cloud-folder}

>[!NOTE]
클라우드 서비스 폴더의 구성은 RESTful, SOAP 및 OData 서비스에 대한 클라우드 서비스를 구성하는 데 필요합니다.

AEM의 모든 클라우드 서비스 구성은 AEM 저장소의 `/conf` 폴더에 통합됩니다. 기본적으로 `conf` 폴더에는 클라우드 서비스 구성을 만들 수 있는 `global` 폴더가 포함되어 있습니다. 하지만 클라우드 구성에 대해 수동으로 활성화해야 합니다. 클라우드 서비스 구성을 만들고 구성하기 위해 추가 폴더 `conf` 를 만들 수도 있습니다.

클라우드 서비스 구성을 위한 폴더를 구성하려면:

1. 도구 > **[!UICONTROL 일반 > 구성 브라우저로 이동합니다]**.
   * See the [Configuration Browser](/help/sites-administering/configurations.md) documentation for more information.
1. 클라우드 구성에 대한 글로벌 폴더를 활성화하거나 이 단계를 건너뛰어 클라우드 서비스 구성에 대한 다른 폴더를 만들고 구성하려면 다음을 수행하십시오.

   1. 구성 **[!UICONTROL 브라우저에서]**&#x200B;폴더를 `global` 선택하고 속성 **[!UICONTROL 을]**&#x200B;누릅니다.

   1. 구성 **[!UICONTROL 속성]** 대화 상자에서 **[!UICONTROL 클라우드 구성을 활성화합니다]**.

   1. 저장 **[!UICONTROL 및 닫기를]** 눌러 구성을 저장하고 대화 상자를 종료합니다.

1. 구성 **[!UICONTROL 브라우저에서 만들기를]**&#x200B;누릅니다 ****.
1. 구성 **[!UICONTROL 만들기]** 대화 상자에서 폴더 제목을 지정하고 **[!UICONTROL 클라우드 구성을 활성화합니다]**.
1. 만들기 **[!UICONTROL 를]** 눌러 클라우드 서비스 구성에 대해 활성화된 폴더를 만듭니다.

## RESTful 웹 서비스 구성 {#configure-restful-web-services}

RESTful 웹 서비스는 JSON 또는 YAML 포맷의 [Swagger 사양을](https://swagger.io/specification/) 사용하여 Swagger 정의 파일에 설명할 수 있습니다. AEM Cloud 서비스에서 RESTful 웹 서비스를 구성하려면 파일 시스템에 Swagger 파일 또는 파일이 호스팅된 URL이 있는지 확인하십시오.

RESTful 서비스를 구성하려면 다음을 수행합니다.

1. 도구 > **[!UICONTROL Cloud Services > 데이터 소스로 이동합니다]**. 클라우드 구성을 만들 폴더를 눌러 선택합니다.

   클라우드 [서비스 구성을 위한 폴더 만들기 및 구성에 대한 자세한 내용은 클라우드 서비스](../../forms/using/configure-data-sources.md#cloud-folder) 구성을 위한 폴더 구성을 참조하십시오.

1. 만들기를 **[!UICONTROL 눌러]** 데이터 소스 **[!UICONTROL 구성 만들기 마법사를 엽니다]**. 구성에 대한 이름과 제목을 지정하고, **[!UICONTROL 서비스 유형]** 드롭다운에서 RESTful 서비스 **[!UICONTROL 를 선택하고, 필요에 따라 구성에 대한 축소판 이미지를 찾아 선택한 다음]** 다음을 누릅니다 ****.
1. RESTful 서비스에 대해 다음 세부 사항을 지정합니다.

   * Swagger 소스 드롭다운에서 URL 또는 파일을 선택한 다음 Swagger URL을 Swagger 정의 파일로 지정하거나 로컬 파일 시스템에서 Swagger 파일을 업로드합니다.
   * Swagger 소스 입력을 기준으로 다음 필드는 값으로 미리 채워집니다.

      * 구성표:REST API에서 사용하는 전송 프로토콜입니다. 드롭다운 목록에 표시되는 체계 유형의 수는 Swagger 소스에 정의된 구성에 따라 다릅니다.
      * 호스트:REST API를 제공하는 호스트의 도메인 이름 또는 IP 주소. 필수 필드입니다.
      * 기본 경로:모든 API 경로의 URL 접두사입니다. 선택 필드입니다.\
         필요한 경우 이러한 필드에 대해 미리 채워진 값을 편집합니다.
   * RESTful 서비스에 액세스하려면 인증 유형(없음, OAuth 2.0, 기본 인증, API 키, 사용자 정의 인증 또는 상호 인증)을 선택하고 그에 따라 인증에 대한 세부 정보를 제공합니다.

   인증 유형으로 **[!UICONTROL API 키를]** 선택한 경우 API 키 값을 지정합니다. API 키는 요청 헤더 또는 쿼리 매개 변수로 보낼 수 있습니다. 위치 **[!UICONTROL 드롭다운 목록에서]** 이러한 옵션 중 하나를 선택하고 그에 따라 매개 변수 이름 **[!UICONTROL 필드에 헤더 또는 쿼리 매개 변수의 이름을]** 지정합니다.

   인증 유형으로 [ **[!UICONTROL 상호 인증]** ]을 선택한 경우 RESTful 및 SOAP 웹 서비스에 대한 [인증서 기반 상호 인증을 참조하십시오](#mutual-authentication).

1. 만들기 **[!UICONTROL 를]** 눌러 RESTful 서비스에 대한 클라우드 구성을 만듭니다.

## SOAP 웹 서비스 구성 {#configure-soap-web-services}

SOAP 기반 웹 서비스는 WSDL( [Web Services Description Language) 사양을 사용하여 설명합니다](https://www.w3.org/TR/wsdl). AEM Cloud 서비스에서 SOAP 기반 웹 서비스를 구성하려면 웹 서비스에 대한 WSDL URL이 있는지 확인하고 다음을 수행하십시오.

1. 도구 > **[!UICONTROL Cloud Services > 데이터 소스로 이동합니다]**. 클라우드 구성을 만들 폴더를 눌러 선택합니다.

   클라우드 [서비스 구성을 위한 폴더 만들기 및 구성에 대한 자세한 내용은 클라우드 서비스](../../forms/using/configure-data-sources.md#cloud-folder) 구성을 위한 폴더 구성을 참조하십시오.

1. 만들기를 **[!UICONTROL 눌러]** 데이터 소스 **[!UICONTROL 구성 만들기 마법사를 엽니다]**. 구성에 대한 이름과 제목을 지정하고, **[!UICONTROL 서비스 유형]** 드롭다운에서 **[!UICONTROL SOAP 웹 서비스]** 를 선택하고, 필요에 따라 구성에 대한 축소판 이미지를 찾아 선택한 다음 **[!UICONTROL 다음을 누릅니다]**.
1. SOAP 웹 서비스에 대해 다음을 지정합니다.

   * 웹 서비스용 WSDL URL.
   * 서비스 엔드포인트. WSDL에 언급된 서비스 끝점을 재정의하려면 이 필드에 값을 지정합니다.
   * SOAP 서비스에 액세스하려면 인증 유형(없음, OAuth 2.0, 기본 인증, 사용자 정의 인증, X509 토큰 또는 상호 인증)을 선택하고 그에 따라 인증에 대한 세부 정보를 제공합니다.

      인증 유형으로 **[!UICONTROL X509 토큰을]** 선택한 경우 X509 인증서를 구성합니다. 자세한 내용은 인증서 [설정을 참조하십시오](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
키 별칭 **** 필드에서 X509 인증서에 대한 키 저장소 별칭을 지정합니다. 인증 요청이 유효한 상태로 유지될 때까지 [ **[!UICONTROL 라이브할 시간] 필드에 시간(초)을]** 지정합니다. 메시지 본문이나 타임스탬프 헤더 또는 둘 다에 서명하도록 선택합니다(선택 사항).

      인증 유형으로 [ **[!UICONTROL 상호 인증]** ]을 선택한 경우 RESTful 및 SOAP 웹 서비스에 대한 [인증서 기반 상호 인증을 참조하십시오](#mutual-authentication).

1. 만들기 **[!UICONTROL 를]** 눌러 SOAP 웹 서비스에 대한 클라우드 구성을 만듭니다.

## OData 서비스 구성 {#config-odata}

OData 서비스는 서비스 루트 URL로 식별됩니다. AEM 클라우드 서비스에서 OData 서비스를 구성하려면 서비스에 대한 서비스 루트 URL이 있는지 확인하고 다음을 수행하십시오.

>[!NOTE]
Microsoft Dynamics 365, 온라인 또는 온-프레미스를 구성하는 단계별 지침은 [Microsoft Dynamics OData 구성을 참조하십시오](/help/forms/using/ms-dynamics-odata-configuration.md).

1. 도구 > **[!UICONTROL Cloud Services > 데이터 소스로 이동합니다]**. 클라우드 구성을 만들 폴더를 눌러 선택합니다.

   클라우드 [서비스 구성을 위한 폴더 만들기 및 구성에 대한 자세한 내용은 클라우드 서비스](../../forms/using/configure-data-sources.md#cloud-folder) 구성을 위한 폴더 구성을 참조하십시오.

1. 만들기를 **[!UICONTROL 눌러]** 데이터 소스 **[!UICONTROL 구성 만들기 마법사를 엽니다]**. 구성에 대한 이름 및 제목을 지정하고, **[!UICONTROL 서비스 유형]** 드롭다운에서 OData 서비스 **[!UICONTROL 를 선택하고, 필요에 따라 구성에 대한 축소판 이미지를 찾아 선택한 다음]** 다음을 **[!UICONTROL 누릅니다]**.
1. OData 서비스에 대해 다음 세부 사항을 지정합니다.

   * 구성할 OData 서비스의 서비스 루트 URL.
   * OData 서비스에 액세스하려면 인증 유형(없음, OAuth 2.0, 기본 인증 또는 사용자 정의 인증)을 선택하고 그에 따라 인증에 대한 세부 정보를 제공합니다.

   >[!NOTE]
   OData 끝점을 서비스 루트로 사용하여 Microsoft Dynamics 서비스에 연결하려면 OAuth 2.0 인증 유형을 선택해야 합니다.

1. 만들기 **를** 눌러 OData 서비스에 대한 클라우드 구성을 만듭니다.

## RESTful 및 SOAP 웹 서비스를 위한 인증서 기반의 상호 인증 {#mutual-authentication}

양식 데이터 모델에 대해 상호 인증을 활성화하면 양식 데이터 모델을 실행하는 데이터 소스 및 AEM Server가 모두 데이터를 공유하기 전에 서로의 ID를 인증합니다. REST 및 SOAP 기반 연결(데이터 소스)에 상호 인증을 사용할 수 있습니다. AEM Forms 환경에서 양식 데이터 모델에 대한 상호 인증을 구성하려면:

1. 개인 키(인증서)를 [!DNL AEM Forms] 서버에 업로드합니다. 개인 키를 업로드하려면:
   1. 관리자로 [!DNL AEM Forms] 서버에 로그인합니다.
   1. 도구 **[!UICONTROL > 보안]** **** > **[!UICONTROL 사용자로]**&#x200B;이동합니다. 사용자를 `fd-cloudservice` 선택하고 속성 **[!UICONTROL 을 누릅니다]**.
   1. Keystore **[!UICONTROL 탭을 열고 KeyStore 파일]** 에서 개인 키 **[!UICONTROL 추가 옵션을 확장한 다음 KeyStore 파일을]** 업로드하고 별칭, 암호를 지정하고 **[!UICONTROL 제출을 누릅니다]**. 인증서가 업로드됩니다.  개인 키 별칭은 인증서를 만드는 동안 인증서에 언급되고 설정됩니다.
1. Global Trust Store에 트러스트 인증서를 업로드합니다. 인증서를 업로드하려면:
   1. 도구 **[!UICONTROL > 보안]** **** > **[!UICONTROL Trust Store]**&#x200B;로 이동합니다.
   1. CER 파일에서 **[!UICONTROL 인증서]** 추가 옵션을 확장하고 **[!UICONTROL 인증서 파일]**&#x200B;선택을 탭하고 인증서를 업로드한 다음 **[!UICONTROL 제출을]**&#x200B;누릅니다.
1. 데이터 소스로 [SOAP](#configure-soap-web-services) 또는 [RESTful](#configure-restful-web-services)**[!UICONTROL 웹 서비스를 구성하고]** 상호 인증을인증 유형으로선택합니다. 사용자에 대해 자체 서명된 여러 인증서를 구성하는 경우 `fd-cloudservice` 인증서에 대한 키 별칭 이름을 지정합니다.

## 다음 단계 {#next-steps}

데이터 소스를 구성했습니다. 양식 데이터 모델을 만들거나 데이터 소스 없이 양식 데이터 모델을 이미 만든 경우 방금 구성한 데이터 소스와 연결할 수 있습니다. 자세한 내용은 [양식 데이터 모델](/help/forms/using/create-form-data-models.md) 만들기를 참조하십시오.
