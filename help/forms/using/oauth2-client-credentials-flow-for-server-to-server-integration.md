---
title: OAuth 2.0 클라이언트 자격 증명 플로우를 사용하여 AEM Forms과 Salesforce 통합
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: OAuth 2.0 클라이언트 자격 증명 플로우를 사용하여 AEM Forms과 Salesforce 통합을 통합하는 절차
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
exl-id: 31f2ccf8-1f4f-4d88-8c5f-ef1b7d1bfb4f
source-git-commit: f11bb43d914a43431cab408ca77690b6ba528a06
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 5%

---

# OAuth 2.0 클라이언트 자격 증명 플로우를 사용한 Salesforce 통합  {#configure-salesforce-with-ouath-2.0-client-credential}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM 6.5 | 이 문서 |

OAuth 2.0 클라이언트 자격 증명을 사용하여 AEM Forms을 Salesforce 애플리케이션과 통합할 수 있습니다. OAuth 2.0 클라이언트 자격 증명은 사용자 개입 없이 직접 통신하는 표준 및 보안 방법입니다.

![AEM Forms과 Salesforce 애플리케이션 간의 통신을 설정하는 동안 발생하는 워크플로우](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms은 Salesforce 연결 애플리케이션에 정의된 클라이언트 자격 증명(소비자 키 및 소비자 암호)을 교환하여 액세스 토큰을 얻습니다.

인증 코드 흐름 인증보다 인증에 OAuth 2.0 클라이언트 자격 증명을 사용하면 다음과 같은 여러 가지 이점이 있습니다.

* OAuth 2.0 클라이언트 자격 증명 인증은 사용자당 5개 이상의 연결을 허용합니다.
* AEM 데이터 소스 구성은 AEM 사용자에 대한 비활성화, 액세스 변경, 암호 업데이트 시 계속 작동합니다.

## 사전 요구 사항 {#prerequisites}

Salesforce 애플리케이션과 AEM 환경 간의 통신을 설정하기 전에

* 만들기 [Salesforce가 앱을 OAuth 2.0 클라이언트 자격 증명 흐름과 연결함](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) 및 를 조직의 API 전용 사용자로, 앱에 대한 소비자 키와 소비자 암호를 받습니다.

* Swagger 파일이 조직의 API와 일치하도록 적절히 구성되었는지 확인합니다. 또는 다음을 선택할 수 있습니다 [Swagger 파일 만들기](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) 처음부터 AEM 환경에서의 활용에 맞춰 설계되었습니다.
>[!NOTE]
>
> AEM 6.5는 Swagger 2.0 파일 사양만 지원합니다.

+++

## 클라이언트 자격 증명 흐름으로 Salesforce를 구성하는 단계 {#steps-to-create-aem-datasource-configuration}

1.  작성자 인스턴스에 로그인합니다. 
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
