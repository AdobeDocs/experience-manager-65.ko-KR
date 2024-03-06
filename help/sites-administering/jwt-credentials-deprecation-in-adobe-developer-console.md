---
title: Adobe Developer Console에서 JWT 자격 증명 사용 중단
description: AEM의 Adobe Developer Console에서 JWT 자격 증명 사용 중단이 미치는 영향에 대해 알아봅니다.
source-git-commit: 72974d27fecbd9c242f66e203b02463c22b93108
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 80%

---


# Adobe Developer Console에서 JWT 자격 증명 사용 중단 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service는 다음을 참조해야 합니다. [이 문서](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) 추가 정보.

Adobe 고객은 [Adobe Developer Console](https://developer.adobe.com/console)을 사용하여 다양한 API에 액세스할 수 있는 자격 증명을 생성합니다. 고객은 OAuth 서버 간 자격 증명에서 단일 페이지 앱에 이르기까지 다양한 자격 증명 유형 중에서 선택합니다. 이러한 자격 증명 유형 중 하나인 서비스 계정(JWT) 자격 증명은 OAuth 서버 간 자격 증명이 마련되어 더 이상 사용되지 않습니다. 2024년 5월 1일 이후에는 새 서비스 계정(JWT) 사용자 인증 정보를 생성할 수 없으며 기존 JWT 사용자 인증 정보는 2025년 1월 1일 이후에는 작동하지 않습니다. [사용 중단에 대해 살펴보십시오](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

이 문서에서는 AEM 6.5 고객이 사용 중단을 처리하는 방법에 대한 몇 가지 추가 컨텍스트를 제공합니다.

중요한 점은 AEM 기능이 아직 새로운 OAuth 서버 간 자격 증명을 지원하지 않는다는 것입니다. 최신 서비스 팩 20 이하를 실행하는 경우 AEM 6.5용 특수 호환성 패키지를 통해 2024년 4월 중순까지 지원이 제공될 예정입니다(서비스 팩 21 이상에는 자동으로 포함됨). JWT 자격 증명을 마이그레이션하기 위한 지침이 포함된 이메일을 받았을 수 있지만, AEM이 새로운 OAuth 서버 간 자격 증명 유형을 지원할 때까지 자격 증명 마이그레이션을 유보할 수 있습니다.

아래 섹션에서는 AEM이 4월 중반에 지원하면 고객이 서비스 계정(JWT) 자격 증명을 OAuth 서버 간 자격 증명으로 교체해야 하는(또는 경우에 따라 교체해서는 안 되는) 시나리오를 나열합니다. [향후 자격 증명을 교체하는 방법](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)을 읽어보십시오.

## AEM을 다른 Adobe 솔루션과 통합 {#integrating-aem-with-other-adobe-solutions}

**작업**: AEM에서 지원하는 2024년 4월 중반 이후까지 마이그레이션을 유보하십시오.

**관련 AEM 버전**: Adobe Managed Services(서비스 팩 20 이하).


AEM 고객은 AEM Author UI를 사용하여 다른 모든 Adobe 솔루션과의 통합을 구성합니다. 예를 들어 Adobe Target, Adobe Analytics, Adobe Launch, AFCS 등이 있습니다.

![AEM을 다른 솔루션과 통합](/help/sites-administering/assets/jwt-deprecation.png)

예를 들어 Adobe Target과의 통합을 구성하기 위한 [지침](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=ko)은 다음과 같습니다. [AEM에서 IMS 구성 완료](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) 섹션의 API 키는 AEM이 4월 중반에 해당 자격 증명을 지원하면 OAuth 서버 간 자격 증명 유형으로 마이그레이션됩니다. 해당 지침은 새로운 OAuth 서버 간 자격 증명을 적용하는 데 도움이 되도록 4월 중반에 업데이트될 예정입니다.

## Cloud Manager API {#cloud-manager-apis}

**작업**: AEM에서 지원하는 2024년 4월 중반 이후까지 마이그레이션을 유보하십시오.

**관련 AEM 버전**: Adobe Managed Services(서비스 팩 20 이하).

고객은 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)를 호출할 수 있도록 Adobe Developer Console 프로젝트를 만듭니다. AEM 및 Cloud Manager가 지원하면 Adobe Developer 프로젝트의 자격 증명은 OAuth 서버 간 자격 증명 유형으로 마이그레이션되어야 합니다.
