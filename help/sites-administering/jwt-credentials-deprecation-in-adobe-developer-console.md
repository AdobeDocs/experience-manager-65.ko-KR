---
title: Adobe Developer Console에서 JWT 자격 증명 사용 중단
description: AEM의 Adobe Developer Console에서 JWT 자격 증명 사용 중단이 미치는 영향에 대해 알아봅니다.
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 72%

---

# Adobe Developer Console에서 JWT 자격 증명 사용 중단 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud service는 자세한 내용을 보려면 [AEMaaCS 버전에 대해 비교 가능한 문서](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=ko)를 참조해야 합니다.

Adobe 고객은 [Adobe Developer Console](https://developer.adobe.com/console)을 사용하여 다양한 API에 액세스할 수 있는 자격 증명을 생성합니다. 고객은 OAuth 서버 간 자격 증명에서 단일 페이지 앱에 이르기까지 다양한 자격 증명 유형 중에서 선택합니다. 이러한 자격 증명 유형 중 하나인 서비스 계정(JWT) 자격 증명은 OAuth 서버 간 자격 증명이 마련되어 더 이상 사용되지 않습니다. 2024년 6월 3일 이후로 새 서비스 계정(JWT) 사용자 인증 정보를 생성할 수 없으며 기존 JWT 사용자 인증 정보는 2025년 1월 27일 이후에는 작동하지 않습니다. [사용 중단에 대해 살펴보십시오](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

이 문서에서는 Adobe Experience Manager(AEM) 6.5 고객이 사용 중단을 처리하는 방법에 대한 몇 가지 추가 컨텍스트를 제공합니다.

주요 해결 방법은 AEM이 이제 AEM에 대한 새 OAuth 서버 간 자격 증명을 지원한다는 것입니다. JWT 자격 증명을 마이그레이션하기 위한 지침이 포함된 이메일을 받으셨을 수 있습니다. 이제 이 마이그레이션을 수행할 수 있습니다.

아래 섹션에서는 고객이 서비스 계정(JWT) 자격 증명을 현재 AEM에서 지원되는 OAuth 서버 간 자격 증명으로 교체해야 하는(또는 경우에 따라 교체해서는 안 되는) 시나리오를 나열합니다. 자격 증명을 마이그레이션하는 [방법을 확인](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)하십시오.

## AEM을 다른 Adobe 솔루션과 통합 {#integrating-aem-with-other-adobe-solutions}

**조치**: 이제 AEM에서 OAuth 자격 증명을 지원하므로 구성을 마이그레이션합니다.

**관련 AEM 버전**: Adobe Managed Services(서비스 팩 21 이상).

AEM 고객은 AEM을 사용하여 다른 모든 Adobe 솔루션과의 통합을 구성합니다. 예를 들어 Adobe Target, Adobe Analytics 등이 있습니다.

![AEM을 다른 솔루션과 통합](/help/sites-administering/assets/jwt-deprecation.png)

다음 방법에 대한 자세한 내용은 [AEM용 IMS 통합 설정](/help/sites-administering/setting-up-ims-integrations-for-aem.md)을 참조하십시오.

* OAuth 자격 증명으로 구성 만들기
* OAuth 자격 증명을 사용하기 위해 JWT 자격 증명으로 만든 구성을 마이그레이션

## Cloud Manager API {#cloud-manager-apis}

**조치**: 언제 JWT에서 OAuth 자격 증명으로 마이그레이션할 수 있는지 확인합니다.

**관련 AEM 버전**: Adobe Managed Services(서비스 팩 21 이상).

고객은 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)를 호출할 수 있도록 Adobe Developer Console 프로젝트를 만듭니다. Adobe Developer 프로젝트의 자격 증명은 사용 중단된 JWT 자격 증명이 만료되는 2025년 1월 전에 OAuth 서버 간 자격 증명 유형으로 마이그레이션해야 합니다.
