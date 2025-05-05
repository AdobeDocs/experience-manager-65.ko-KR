---
title: 데이터 소스 구성
description: 양식 데이터 모델을 만들 수 있도록 다양한 유형의 데이터 소스를 구성하는 방법에 대해 알아봅니다.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
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

데이터 통합은 OAuth2.0([인증 코드](https://oauth.net/2/grant-types/authorization-code/), [클라이언트 자격 증명](https://oauth.net/2/grant-types/client-credentials/)), 기본 인증 및 API 키 인증 유형을 즉시 사용할 수 있도록 지원하며, 이를 통해 웹 서비스에 액세스하기 위한 사용자 지정 인증을 구현할 수 있습니다. RESTful, SOAP 기반 및 OData 서비스가 AEM Cloud Service에 구성되어 있는 반면, 관계형 데이터베이스에 대한 JDBC와 AEM 사용자 프로필에 대한 커넥터는 AEM 웹 콘솔에 구성되어 있습니다.

## 관계형 데이터베이스 구성 {#configure-relational-database}

AEM 웹 콘솔 구성을 사용하여 관계형 데이터베이스를 구성할 수 있습니다. 다음 작업을 수행합니다.

1. `https://server:host/system/console/configMgr`의 AEM 웹 콘솔로 이동합니다.
1. **[!UICONTROL Apache Sling 연결의 풀링된 데이터 소스]** 구성을 찾습니다. 을(를) 선택하여 편집 모드로 구성을 엽니다.
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
   > 1. https://&#39;[server]:[port]&#39;/system/console/crypto로 이동합니다.
   > 1. **[!UICONTROL 일반 텍스트]** 필드에서 암호화할 암호 또는 문자열을 지정하고 **[!UICONTROL Protect]**&#x200B;을(를) 선택합니다.
   >
   >암호화된 텍스트는 구성에 지정할 수 있는 보호된 텍스트 필드에 나타납니다.

1. **[!UICONTROL Test on Borrow]** 또는 **[!UICONTROL Test on Return]**&#x200B;을(를) 사용하여 개체를 풀과 풀에서 각각 빌리거나 반환하기 전에 유효성을 검사하도록 지정합니다.
1. **[!UICONTROL 유효성 검사 쿼리]** 필드에 SQL SELECT 쿼리를 지정하여 풀로부터의 연결을 검증하십시오. 쿼리는 하나 이상의 행을 반환해야 합니다. 데이터베이스를 기반으로 다음 중 하나를 지정합니다.

   * 1(MySQL 및 MS SQL) 선택
   * 이중 (Oracle)에서 1 선택

1. **[!UICONTROL 저장]**&#x200B;을 선택하여 구성을 저장합니다.

   >[!NOTE]
   >
   > Forms 데이터 모델에 관계형 데이터베이스에 대해 예약된 키워드인 개체가 포함된 경우, 이로 인해 데이터 추가, 업데이트 또는 검색 문제가 발생할 수 있습니다. 따라서 양식 데이터 모델에서 이러한 개체를 사용하지 마십시오.

## AEM 사용자 프로필 구성 {#configure-aem-user-profile}

AEM 웹 콘솔에서 사용자 프로필 커넥터 구성을 사용하여 AEM 사용자 프로필을 구성할 수 있습니다. 다음 작업을 수행합니다.

1. https://&#39;[server]:[port]의 system/console/configMgr에서 AEM 웹 콘솔로 이동합니다.
1. **[!UICONTROL AEM Forms 데이터 통합 - 사용자 프로필 커넥터 구성]**&#x200B;을 찾아 편집 모드에서 구성을 열도록 선택합니다.
1. 사용자 프로필 커넥터 구성 대화 상자에서 사용자 프로필 속성을 추가, 제거 또는 업데이트할 수 있습니다. 지정된 속성은 양식 데이터 모델에서 사용할 수 있습니다. 사용자 프로필 속성을 지정하려면 다음 형식을 사용하십시오.

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   예:

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >위의 예에서 **&#42;**&#x200B;은(는) CRXDE 구조의 AEM 사용자 프로필에 있는 `profile/empLocation/` 노드 아래의 모든 노드를 나타냅니다. 즉, 양식 데이터 모델은 `profile/empLocation/` 노드 아래의 모든 노드에 있는 `string` 유형의 `city` 속성에 액세스할 수 있습니다. 그러나 지정된 속성이 포함된 노드는 일관된 구조를 따라야 합니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택하여 구성을 저장합니다.

## 클라우드 서비스 구성을 위한 폴더 구성 {#cloud-folder}

>[!NOTE]
>
>RESTful, SOAP 및 OData 서비스에 대한 클라우드 서비스를 구성하려면 클라우드 서비스 폴더에 대한 구성이 필요합니다.

AEM의 모든 클라우드 서비스 구성은 AEM 저장소의 `/conf` 폴더에 통합됩니다. 기본적으로 `conf` 폴더에는 클라우드 서비스 구성을 만들 수 있는 `global` 폴더가 있습니다. 그러나 클라우드 구성에 대해서는 수동으로 활성화해야 합니다. `conf`에서 추가 폴더를 만들어 클라우드 서비스 구성을 만들고 구성할 수도 있습니다.

클라우드 서비스 구성에 대한 폴더를 구성하려면 다음을 수행합니다.

1. **[!UICONTROL 도구 > 일반 > 구성 브라우저]**&#x200B;로 이동합니다.
   * 자세한 내용은 [구성 브라우저](/help/sites-administering/configurations.md) 설명서를 참조하십시오.
1. 클라우드 구성에 대한 전역 폴더를 활성화하려면 다음을 수행하거나 클라우드 서비스 구성에 대한 다른 폴더를 만들고 구성하려면 이 단계를 건너뜁니다.

   1. **[!UICONTROL 구성 브라우저]**&#x200B;에서 `global` 폴더를 선택하고 **[!UICONTROL 속성]**&#x200B;을 선택합니다.

   1. **[!UICONTROL 구성 속성]** 대화 상자에서 **[!UICONTROL 클라우드 구성]**&#x200B;을 사용하도록 설정합니다.

   1. 구성을 저장하고 대화 상자를 종료하려면 **[!UICONTROL 저장 및 닫기]**&#x200B;를 선택하십시오.

1. **[!UICONTROL 구성 브라우저]**&#x200B;에서 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL 구성 만들기]** 대화 상자에서 폴더의 제목을 지정하고 **[!UICONTROL 클라우드 구성]**&#x200B;을 사용하도록 설정합니다.
1. 클라우드 서비스 구성에 사용할 수 있는 폴더를 만들려면 **[!UICONTROL 만들기]**&#x200B;를 선택하십시오.

## RESTful 웹 서비스 구성 {#configure-restful-web-services}

RESTful 웹 서비스는 Swagger 정의 파일에서 JSON 또는 YAML 형식의 [Swagger 사양](https://swagger.io/specification/)을 사용하여 설명할 수 있습니다. AEM Cloud Services에서 RESTful 웹 서비스를 구성하려면 파일 시스템에 Swagger 파일이 있거나 파일이 호스팅되는 URL이 있는지 확인합니다.

RESTful 서비스를 구성하려면 다음을 수행합니다.

1. **[!UICONTROL 도구 > Cloud Service > 데이터 원본]**(으)로 이동합니다. 클라우드 구성을 만들 폴더를 선택하려면 를 선택합니다.

   클라우드 서비스 구성을 위한 폴더를 만들고 구성하는 방법에 대한 자세한 내용은 [클라우드 서비스 구성을 위한 폴더 구성](../../forms/using/configure-data-sources.md#cloud-folder)을 참조하십시오.

1. **[!UICONTROL 만들기]**&#x200B;를 선택하여 **[!UICONTROL 데이터 Source 구성 만들기 마법사]**&#x200B;를 엽니다. 구성의 이름 및 제목(선택 사항)을 지정하고, **[!UICONTROL 서비스 유형]** 드롭다운에서 **[!UICONTROL RESTful 서비스]**&#x200B;를 선택하고, 선택 사항으로 구성의 썸네일 이미지를 검색하여 선택한 후 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. RESTful 서비스에 대해 다음 세부 정보를 지정합니다.

   * Swagger Source 드롭다운에서 URL 또는 파일 을 선택한 다음 그에 따라 Swagger 정의 파일에 Swagger URL 을 지정하거나 로컬 파일 시스템에서 Swagger 파일을 업로드합니다.
   * Swagger Source 입력을 기반으로 다음 필드는 값으로 미리 채워집니다.

      * 체계: REST API에서 사용하는 전송 프로토콜입니다. 드롭다운 목록에 표시되는 구성표 유형의 수는 Swagger 소스에 정의된 구성표에 따라 다릅니다.
      * 호스트: REST API를 제공하는 호스트의 도메인 이름 또는 IP 주소입니다. 필수 필드입니다.
      * 기본 경로: 모든 API 경로의 URL 접두어. 선택 필드입니다.\
        필요한 경우 이러한 필드에 대해 미리 채워진 값을 편집합니다.

   * 인증 유형(없음, OAuth2.0([인증 코드](https://oauth.net/2/grant-types/authorization-code/), [클라이언트 자격 증명](https://oauth.net/2/grant-types/client-credentials/)), 기본 인증, API 키, 사용자 지정 인증 또는 상호 인증)을 선택하여 RESTful 서비스에 액세스하고 그에 따라 인증에 대한 세부 정보를 제공합니다.

   인증 유형으로 **[!UICONTROL API 키]**&#x200B;을(를) 선택한 경우 API 키 값을 지정하십시오. API 키는 요청 헤더 또는 쿼리 매개 변수로 전송될 수 있습니다. **[!UICONTROL 위치]** 드롭다운 목록에서 이러한 옵션 중 하나를 선택하고 **[!UICONTROL 매개 변수 이름]** 필드에 헤더 이름 또는 쿼리 매개 변수를 적절하게 지정합니다.

   인증 유형으로 **[!UICONTROL 상호 인증]**&#x200B;을 선택한 경우 [RESTful 및 SOAP 웹 서비스에 대한 인증서 기반 상호 인증](#mutual-authentication)을 참조하십시오.

1. RESTful 서비스에 대한 클라우드 구성을 만들려면 **[!UICONTROL 만들기]**&#x200B;를 선택하십시오.

### 성능을 최적화하기 위한 양식 데이터 모델 HTTP 클라이언트 구성 {#fdm-http-client-configuration}

데이터 소스로 RESTful 웹 서비스와 통합할 때 [!DNL Experience Manager Forms] 양식 데이터 모델에 성능 최적화를 위한 HTTP 클라이언트 구성이 포함됩니다.
양식 데이터 모델 HTTP 클라이언트를 구성하려면 다음 단계를 수행하십시오.

1. [!DNL Experience Manager Forms] 작성자 인스턴스에 관리자로 로그인하고 [!DNL Experience Manager] 웹 콘솔 번들로 이동합니다. 기본 URL은 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)입니다.

1. REST 데이터 원본에 대한 **[!UICONTROL 양식 데이터 모델 Http 클라이언트 구성]**&#x200B;을 선택하십시오.

1. [!UICONTROL REST 데이터 원본에 대한 양식 데이터 모델 Http 클라이언트 구성] 대화 상자에서 다음을 수행합니다.

   * **[!UICONTROL 총 연결 제한]** 필드에 양식 데이터 모델과 RESTful 웹 서비스 간 허용되는 최대 연결 수를 지정하십시오. 기본값은 20개 연결입니다.

   * **[!UICONTROL 경로별 연결 제한]** 필드에 각 경로에 대해 허용되는 최대 연결 수를 지정합니다. 기본값은 2개 연결입니다.

   * **[!UICONTROL 활성 상태 유지]** 필드에 영구 HTTP 연결이 활성 상태로 유지되는 기간을 지정하십시오. 기본값은 15초입니다.

   * **[!UICONTROL 연결 시간 초과]** 필드에 [!DNL Experience Manager Forms] 서버가 연결을 설정할 때까지 기다리는 기간을 지정합니다. 기본값은 10초입니다.

   * **[!UICONTROL 소켓 시간 제한]** 필드에 두 데이터 패킷 간 비활성 최대 기간을 지정합니다. 기본값은 30초입니다.

## SOAP 웹 서비스 구성 {#configure-soap-web-services}

SOAP 기반 웹 서비스는 [WSDL(Web Services Description Language) 사양](https://www.w3.org/TR/wsdl)을 사용하여 설명합니다. AEM 클라우드 서비스에서 SOAP 기반 웹 서비스를 구성하려면 웹 서비스에 대한 WSDL URL이 있는지 확인하고 다음을 수행합니다.

1. **[!UICONTROL 도구 > Cloud Service > 데이터 원본]**(으)로 이동합니다. 클라우드 구성을 만들 폴더를 선택하려면 를 선택합니다.

   클라우드 서비스 구성을 위한 폴더를 만들고 구성하는 방법에 대한 자세한 내용은 [클라우드 서비스 구성을 위한 폴더 구성](../../forms/using/configure-data-sources.md#cloud-folder)을 참조하십시오.

1. **[!UICONTROL 만들기]**&#x200B;를 선택하여 **[!UICONTROL 데이터 Source 구성 만들기 마법사]**&#x200B;를 엽니다. 구성의 이름 및 제목(선택 사항)을 지정하고, **[!UICONTROL 서비스 유형]** 드롭다운에서 **[!UICONTROL SOAP 웹 서비스]**&#x200B;를 선택하고, 선택 사항으로 구성의 썸네일 이미지를 찾아 선택한 후 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. SOAP 웹 서비스에 대해 다음을 지정합니다.

   * 웹 서비스용 WSDL URL입니다.
   * 서비스 엔드포인트. WSDL에 언급된 서비스 끝점을 재정의하려면 이 필드에 값을 지정하십시오.
   * 인증 유형(없음, OAuth2.0([인증 코드](https://oauth.net/2/grant-types/authorization-code/), [클라이언트 자격 증명](https://oauth.net/2/grant-types/client-credentials/)), 기본 인증, 사용자 지정 인증, X509 토큰 또는 상호 인증)을 선택하여 SOAP 서비스에 액세스하고 그에 따라 인증에 대한 세부 정보를 제공합니다.

     인증 유형으로 **[!UICONTROL X509 토큰]**&#x200B;을(를) 선택한 경우 X509 인증서를 구성하십시오. 자세한 내용은 [인증서 설정](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)을 참조하세요.
**[!UICONTROL 키 별칭]** 필드에 X509 인증서에 대한 KeyStore 별칭을 지정하십시오. 인증 요청이 유효한 상태로 유지될 때까지 **[!UICONTROL Time To Live]** 필드에 시간을 초 단위로 지정합니다. 메시지 본문 또는 타임스탬프 헤더 또는 둘 다에 서명하려면 선택합니다(선택적).

     인증 유형으로 **[!UICONTROL 상호 인증]**&#x200B;을 선택한 경우 [RESTful 및 SOAP 웹 서비스에 대한 인증서 기반 상호 인증](#mutual-authentication)을 참조하십시오.

1. SOAP 웹 서비스에 대한 클라우드 구성을 만들려면 **[!UICONTROL 만들기]**&#x200B;를 선택하십시오.

## OData 서비스 구성 {#config-odata}

OData 서비스는 서비스 루트 URL로 식별됩니다. AEM Cloud Services에서 OData 서비스를 구성하려면 서비스에 대한 서비스 루트 URL이 있는지 확인하고 다음을 수행합니다.

>[!NOTE]
>
>양식 데이터 모델이 [OData 버전 4](https://www.odata.org/documentation/)을(를) 지원합니다.
>온라인 또는 온-프레미스에서 Microsoft Dynamics 365를 구성하는 방법에 대한 단계별 안내서는 [Microsoft Dynamics OData 구성](/help/forms/using/ms-dynamics-odata-configuration.md)을 참조하십시오.

1. **[!UICONTROL 도구 > Cloud Service > 데이터 원본]**(으)로 이동합니다. 클라우드 구성을 만들 폴더를 선택하려면 를 선택합니다.

   클라우드 서비스 구성을 위한 폴더를 만들고 구성하는 방법에 대한 자세한 내용은 [클라우드 서비스 구성을 위한 폴더 구성](../../forms/using/configure-data-sources.md#cloud-folder)을 참조하십시오.

1. **[!UICONTROL 만들기]**&#x200B;를 선택하여 **[!UICONTROL 데이터 Source 구성 만들기 마법사]**&#x200B;를 엽니다. 구성의 이름 및 제목(선택 사항)을 지정하고, **[!UICONTROL 서비스 유형]** 드롭다운에서 **[!UICONTROL 데이터 서비스]**&#x200B;를 선택하고, 선택 사항으로 구성의 썸네일 이미지를 찾아 선택한 후 **[!UICONTROL 다음]**&#x200B;을 선택합니다.
1. OData 서비스에 대해 다음 세부 정보를 지정합니다.

   * 구성할 OData 서비스의 서비스 루트 URL입니다.
   * 인증 유형(없음, OAuth2.0([인증 코드](https://oauth.net/2/grant-types/authorization-code/), [클라이언트 자격 증명](https://oauth.net/2/grant-types/client-credentials/)), 기본 인증 또는 사용자 지정 인증)을 선택하여 OData 서비스에 액세스하고 그에 따라 인증에 대한 세부 정보를 제공합니다.

   >[!NOTE]
   >
   >OData 끝점을 서비스 루트로 사용하여 Microsoft Dynamics 서비스와 연결하려면 OAuth 2.0 인증 유형을 선택하십시오.

1. OData 서비스에 대한 클라우드 구성을 만들려면 **만들기**&#x200B;를 선택하십시오.

## RESTful 및 SOAP 웹 서비스를 위한 인증서 기반 상호 인증 {#mutual-authentication}

양식 데이터 모델에 대해 상호 인증을 활성화하면 데이터를 공유하기 전에 양식 데이터 모델을 실행하는 AEM 서버와 데이터 소스 모두 서로의 ID를 인증합니다. REST 및 SOAP 기반 연결(데이터 소스)에 상호 인증을 사용할 수 있습니다. AEM Forms 환경에서 양식 데이터 모델에 대한 상호 인증을 구성하려면 다음 작업을 수행하십시오.

1. 개인 키(인증서)를 [!DNL AEM Forms] 서버에 업로드합니다. 개인 키를 업로드하려면:
   1. [!DNL AEM Forms] 서버에 관리자로 로그인합니다.
   1. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**(으)로 이동합니다. `fd-cloudservice` 사용자를 선택하고 **[!UICONTROL 속성]**&#x200B;을 선택합니다.
   1. **[!UICONTROL 키 저장소]** 탭을 열고 **[!UICONTROL KeyStore 파일에서 개인 키 추가]** 옵션을 확장하고 KeyStore 파일을 업로드한 다음 별칭, 암호를 지정하고 **[!UICONTROL 제출]**&#x200B;을 선택합니다. 인증서가 업로드되었습니다.  개인 키 별칭은 인증서에 언급되어 있으며 인증서를 만드는 동안 설정됩니다.
1. 글로벌 Trust Store에 트러스트 인증서를 업로드합니다. 인증서를 업로드하려면:
   1. **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 신뢰 저장소]**&#x200B;로 이동합니다.
   1. **[!UICONTROL CER 파일에서 인증서 추가]** 옵션을 확장하고 **[!UICONTROL 인증서 파일 선택]**&#x200B;을 선택하고 인증서를 업로드한 다음 **[!UICONTROL 제출]**&#x200B;을 선택합니다.
1. [SOAP](#configure-soap-web-services) 또는 [RESTful](#configure-restful-web-services) 웹 서비스를 데이터 소스로 구성하고 인증 유형으로 **[!UICONTROL 상호 인증]**&#x200B;을(를) 선택하십시오. `fd-cloudservice` 사용자에 대해 여러 개의 자체 서명된 인증서를 구성하는 경우 인증서에 대한 키 별칭 이름을 지정하십시오.

## 다음 단계 {#next-steps}

데이터 소스를 구성했습니다. 그런 다음 양식 데이터 모델을 만들거나 데이터 소스 없이 이미 양식 데이터 모델을 만든 경우 구성한 데이터 소스와 연결할 수 있습니다. 자세한 내용은 [양식 데이터 모델 만들기](/help/forms/using/create-form-data-models.md)를 참조하십시오.
