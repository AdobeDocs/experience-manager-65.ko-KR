---
title: OAuth 2.0 클라이언트 자격 증명 플로우를 사용하여 AEM Forms과 Salesforce 통합
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: OAuth 2.0 클라이언트 자격 증명 플로우를 사용하여 AEM Forms과 Salesforce 통합을 통합하는 절차
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
exl-id: 31f2ccf8-1f4f-4d88-8c5f-ef1b7d1bfb4f
source-git-commit: 91683330024fbf1059715447073f35cecde45b0a
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---

# OAuth 2.0 클라이언트 자격 증명 플로우를 사용한 Salesforce 통합  {#configure-salesforce-with-ouath-2.0-client-credential}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html) |
| AEM 6.5 | 이 문서 |


AEM Forms을 Salesforce 애플리케이션과 통합하기 위해 OAuth 2.0 클라이언트 자격 증명 플로우가 사용됩니다. 사용자 관여 없이 직접 의사소통을 할 수 있는 표준화되고 안전한 방법이다. 이 흐름에서 클라이언트 애플리케이션(AEM Form)은 Salesforce 연결 애플리케이션에 정의된 클라이언트 자격 증명을 교환하여 액세스 토큰을 얻습니다. 필수 클라이언트 자격 증명에는 소비자 키 및 소비자 암호가 포함됩니다.

## OAuth 2.0 클라이언트 자격 증명 플로우를 사용하여 Salesforce를 AEM Forms과 통합할 때의 이점 {#advantages-of-integrating-saleforce-aemforms}

AEM Forms에서는 OAuth 2.0 클라이언트 자격 증명 흐름 외에 인증 코드 흐름과 Salesforce 통합을 지원합니다. OAuth 2.0 인증 코드 흐름에서 클라이언트 애플리케이션(AEM Forms)은 Salesforce 사용자를 대신하여 리소스 액세스 권한을 획득하므로 몇 가지 제한 사항이 있습니다.

* 사용자당 최대 5개의 연결이 허용됩니다. 추가 연결은 이전 연결을 자동으로 취소합니다.
* 사용자가 비활성화되거나, 액세스할 수 없거나, 암호를 업데이트하면 AEM 데이터 소스 구성이 작동하지 않습니다.

## 사전 요구 사항 {#prerequisites}

Salesforce와 AEM 환경 간에 데이터를 검색하고 가져오려면 추가 작업을 진행하기 전에 특정 사전 요구 사항이 필요합니다.

+++ **클라이언트 자격 증명 흐름 및 API 전용 사용자로 Saleforce 연결 애플리케이션 설정**

OAuth 2.0 클라이언트 자격 증명 흐름과 조직에 대한 API 전용 사용자로 Salesforce에 연결된 앱을 만들어야 합니다. 자세한 단계는 이 문서를 참조하십시오 [서버 간 통합을 위한 OAuth 2.0 클라이언트 자격 증명 흐름](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5). 이러한 단계는 소비자 키와 소비자 암호를 얻는 데 도움이 됩니다.

>[!NOTE]
>
> AEM 데이터 소스 구성을 만드는 동안 소비자 키와 소비자 암호를 필수 항목으로 적어 두십시오.

+++

+++ **Swagger 파일 만들기**

Swagger는 RESTful API를 개발하고 설명하는 규칙, 사양 및 도구의 오픈 소스 세트입니다. [Swagger 파일 만들기](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) AEM Forms과 Salesforce를 통합하기 전에

>[!NOTE]
>
> AEM 6.5는 Swagger 2.0 파일 사양만 지원합니다.

+++

## 클라이언트 자격 증명 흐름으로 Salesforce를 구성하는 단계 {#steps-to-create-aem-datasource-configuration}

1. 작성자 인스턴스에 로그인합니다.
1. 다음으로 이동 **[!UICONTROL 도구]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 데이터 소스]**.
1. 구성 폴더를 선택합니다.
1. 클릭 **[!UICONTROL 만들기]** 및 **[!UICONTROL 데이터 소스 구성 만들기]** 가 표시됩니다.
1. 다음을 지정합니다. **[!UICONTROL 제목]** 및 선택 **[!UICONTROL 서비스 유형]** 다음으로: **[!UICONTROL RESTful 서비스]**.
1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 다음 항목 선택 **[!UICONTROL Swagger 소스]** 다음으로: **[!UICONTROL 파일].**
   >[!NOTE]
   >
   > Swagger 파일을 선택하면 스키마, 호스트 이름 및 기본 경로가 자동으로 채워집니다.

1. 를 클릭하여 로컬 컴퓨터에서 생성된 Swagger 파일을 업로드합니다. **[!UICONTROL 찾아보기]**.
1. 다음 항목 선택 **[!UICONTROL 인증 유형]** 다음으로: **[!UICONTROL OAuth 2.0]** 및 **[!UICONTROL 인증 설정]** 패널이 나타납니다.
1. 다음 항목 선택 **[!UICONTROL 권한 유형]** 다음으로: **[!UICONTROL 클라이언트 자격 증명]**.
1. 다음을 지정합니다. **[!UICONTROL 클라이언트 ID]** 및 **[!UICONTROL 클라이언트 암호]** salesforce 연결 앱에서 가져왔습니다.
1. 다음을 지정합니다. **[!UICONTROL 토큰 URL 액세스]** 형식
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > 각 조직에는 고유한 도메인 이름이 있습니다.

1. 클릭 **[!UICONTROL 연결 테스트]**.
1. 연결이 성공하면 **[!UICONTROL 만들기]** 단추를 클릭합니다.

이제 다음을 수행할 수 있습니다. [양식 데이터 모델 만들기](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) 를 사용하여 구성된 데이터 소스를 적응형 Forms과 통합합니다.
