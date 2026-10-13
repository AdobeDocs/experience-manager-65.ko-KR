---
title: AEM 6.5와 Adobe Campaign 통합
description: Adobe Campaign과의 통합을 위한 AEM 6.5의 지원에 대해 알아보십시오.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ab41e540-1d43-4fc2-99d4-621ff2290e77
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 12%
---

# AEM 6.5와 Adobe Campaign 통합{#integrating-with-adobe-campaign}

Adobe Campaign과의 통합을 위한 AEM 6.5의 지원에 대해 알아보십시오.

Adobe Campaign은 온라인과 오프라인의 모든 채널에서 캠페인을 개인화하고 게재할 수 있는 솔루션 세트입니다.

>[!NOTE]
>
>이 문서에서는 Adobe Campaign을 AEM 6.5, 온프레미스 또는 AMS 호스팅 AEM 솔루션과 통합하는 방법에 대해 설명합니다.
>
>Adobe Campaign과 AEM as a Cloud Service 기반 AEM 솔루션 통합에 대한 자세한 내용은 [이 문서를 참조하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/campaign.html?lang=ko)

## Adobe Campaign Classic과 통합 {#acc}

몇 가지 ACC(Adobe Campaign Classic) 버전이 있습니다. AEM과의 통합에 대한 지원은 구현한 ACC 버전과 AEM이 Adobe Manage Services(AMS)의 온프레미스에 설치되어 있는지에 따라 다릅니다.

| ACC 버전 | AEM 6.5 <br>온 프레미스와 통합 | AEM 6.5<br>AMS와 통합 |
|---|---|---|
| [v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ko) | 지원됨 | 지원됨 |
| [v8 클라이언트 콘솔](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ko) | 지원됨 | 지원됨 |

다음 설명서는 AEM을 Adobe Campaign Classic과 통합하는 방법을 설명합니다.

* [Adobe Campaign Classic과 통합](/help/sites-administering/campaignonpremise.md) - 통합 구성에 대한 단계별 세부 정보를 알아봅니다.

다음 추가 설명서에서는 통합을 사용하는 방법을 설명합니다.

* [이메일 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html?lang=ko) - AEM에서 Campaign 콘텐츠를 작성하는 데 사용할 수 있는 표준 이메일 구성 요소에 대해 알아봅니다.
* [Adobe Campaign Classic 통합 문제 해결](/help/sites-administering/troubleshooting-campaignintegration.md) - AEM-ACC 통합과 관련된 가장 일반적인 문제를 해결하는 방법에 대해 알아봅니다.

## Adobe Campaign Standard와 통합 {#acs}

ACS([Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ko))와 AEM의 통합은 AEM이 AMS(Adobe Manage Services)의 온-프레미스에 설치되어 있는지 여부에 따라 달라집니다.

| AEM 6.5 <br>온 프레미스와 통합 | AEM 6.5<br>AMS와 통합 |
|---|---|
| 지원됨 | 지원됨 |
| 지원됨 | 지원됨 |

다음 설명서는 AEM을 Adobe Campaign Standard과 통합하는 방법을 설명합니다.

* [Adobe Campaign Standard와 통합](/help/sites-administering/campaignstandard.md)

다음 추가 설명서에서는 통합을 사용하는 방법을 설명합니다.

* [이메일 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html?lang=ko)
