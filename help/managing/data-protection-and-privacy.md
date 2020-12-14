---
title: 데이터 보호 및 데이터 개인 정보 보호 규정 - Adobe Experience Manager 준비 사항
seo-title: 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 준비 사항;GDPR, CPA 등
description: '다양한 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 지원에 대해 알아봅니다.여기에는 EU 개인 정보 보호 규정(GDPR), 캘리포니아 개인 정보 보호 법 및 새로운 AEM 프로젝트 구현 시 준수되는 방법이 포함되어 있습니다. '
seo-description: '다양한 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 지원에 대해 알아봅니다.여기에는 EU 개인 정보 보호 규정(GDPR), 캘리포니아 개인 정보 보호 법 및 새로운 AEM 프로젝트 구현 시 준수되는 방법이 포함되어 있습니다. '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---


# 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 준비 사항 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>이 문서의 내용이 법률적 조언을 의미하지 않으며 법적 조언을 대체하기 위한 것이 아니다.
>
>데이터 보호 및 데이터 개인 정보 보호 규정에 대한 정보는 회사의 법무팀에 문의하십시오.

>[!NOTE]
>
>개인정보 보호 문제에 대한 Adobe의 응답과 Adobe 고객으로서 사용자에게 의미하는 바를 자세히 알아보려면 [Adobe의 개인 정보 보호 센터](https://www.adobe.com/privacy.html)를 참조하십시오.

Adobe은 고객 개인 정보 관리자 또는 AEM 관리자가 데이터 보호 및 데이터 개인 정보 보호 요청을 처리하고 adobe 고객이 이러한 규정을 준수하도록 지원하기 위해 API와 함께 설명서 및 절차를 제공합니다. 문서화된 절차를 통해 고객은 수동으로 또는 외부 포털 또는 서비스에서 API를 호출하여 규정 요청을 실행할 수 있습니다.

>[!CAUTION]
>
>여기에 설명된 세부 사항은 Adobe Experience Manager으로 제한됩니다.
>
>다른 Adobe 온디맨드 서비스의 데이터와 관련 개인 정보 보호 요청은 해당 서비스에 대해 조치를 취해야 합니다.
>
>자세한 내용은 [Adobe의 개인 정보 보호 센터](https://www.adobe.com/privacy.html)를 참조하십시오.

## 소개 {#introduction}

Adobe Experience Manager 인스턴스와 그 인스턴스에서 실행되는 애플리케이션은 Adobe 고객이 소유하고 운영하는 애플리케이션입니다.

그 결과 GDPR, CPA 등 데이터 보호 규정이 고객의 책임입니다.

매우 간단한 소개로서, 데이터 개인 정보 보호 및 보호에 대한 규정에는

* CPA(Business Entities) 및/또는 GDPR(Data Controllers)

* CPA(Service Providers) 및/또는 데이터 프로세서(GDPR)

이러한 규정의 주요 내용은 다음과 같습니다.

1. 모든 고유 ID를 포함하도록 개인 데이터의 확장된 정의를 직접 및 간접적으로 식별할 수 있는 데이터에서 사용할 수 있습니다.

2. 동의 요건 강화

3. 삭제 권한에 대한 집중(데이터 삭제)

4. 데이터 판매 거부.

Adobe Experience Manager의 경우:

* 인스턴스 및 해당 인스턴스에서 실행되는 응용 프로그램은 고객이 소유하며 관리합니다.

   * 즉, 비즈니스 엔티티 및 서비스 제공업체, 데이터 컨트롤러, 데이터 프로세서 등의 규정 역할을 효율적으로 관리하게 됩니다.

   * 아래 다이어그램과 같이 Adobe Experience Platform Privacy Service은 AEM용 워크플로우에 포함되지 않습니다.

* AEM에는 고객의 개인정보 보호 관리자 및/또는 AEM 관리자가 개인정보 보호 규정 요청을 실행하는 데 필요한 문서 및 절차가 포함되어 있습니다.수동으로 또는 API를 통해(있는 경우).

* 새 서비스 또는 UI가 추가되지 않았습니다.

   * 대신 개인 정보 보호 규정 요청을 처리하는 고객 UI/포털에서 사용하기 위해 절차 및 API를 문서화합니다.

* AEM은 개인 정보 요청 워크플로우를 지원하기 위해 특별히 마련된 도구를 포함하지 않습니다.

   * Adobe은 고객의 개인 정보 관리자 및/또는 AEM 관리자에 대한 문서 및 절차를 제공하여 고객이 개인 정보 보호 규정과 관련된 요청을 수동으로 실행할 수 있도록 합니다.

Adobe은 Adobe Experience Manager에 대한 액세스, 삭제 및 옵트아웃과 관련된 개인정보 보호 요청을 처리하는 절차를 제공합니다. 일부 경우, 고객 개발 포털이나 자동화 지원에 도움이 되는 스크립트에서 호출할 수 있는 API가 있습니다.

다음 다이어그램은 개인 정보 요청 워크플로우의 모양을 보여줍니다(Adobe Experience Manager 6.5 사용 그림).

![데이터 보호 및 개인 정보 보호](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager 및 규정 준비 {#aem-and-regulatory-readiness}

AEM의 제품 영역에 대한 규정 설명서는 아래 섹션을 참조하십시오.

## AEM 기반 정보 {#aem-foundation}

AEM Foundation에 대한 [데이터 보호 및 개인 정보 보호 요청 처리를 참조하십시오](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM 집계 사용 통계 수집 동의 {#aem-opting-into-aggregate-usage-statistics-collection}

[집계된 사용 통계 컬렉션](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)을 참조하십시오.

## AEM Sites {#aem-sites}

[AEM Sites - 데이터 보호 및 개인 정보 보호 준비를 참조하십시오.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

[AEM Commerce - 데이터 보호 및 개인 정보 보호 준비](/help/sites-administering/gdpr-compliance-commerce.md)를 참조하십시오.

## AEM Mobile {#aem-mobile}

[AEM Mobile - 데이터 보호 및 개인 정보 보호 준비](/help/mobile/aem-mobile-gdpr-compliance.md)를 참조하십시오.

## ADOBE TARGET 및 Adobe Analytics와의 AEM 통합 {#aem-integration-with-adobe-target-adobe-analytics}

이러한 Adobe Experience Manager 통합은 데이터 보호 및 개인 정보 보호(예: GDPR 또는 CPA) 전용 서비스와 통합되어 있습니다. 통합과 관련하여 Adobe Target 또는 Adobe Analytics의 개인 데이터는 AEM에 저장되지 않습니다.
자세한 내용은 다음을 참조하십시오.

* [Adobe Target - 개인 정보 개요](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics 데이터 개인 정보 보호 워크플로우](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities은 데이터 주체에게 데이터 이식성, 액세스 권한 및 바로 사용 가능한 APIs[를 통해 잊어버릴 권리가 있음을 알려줍니다. ](/help/communities/user-ugc-management-service.md) 이러한 API를 사용하면 사용자 생성 컨텐츠의 벌크 삭제 및 일괄 내보내기를 수행할 수 있으며 인증 가능 ID를 통해 식별된 사용자 계정을 비활성화할 수 있습니다. 그러나 사용자 계정의 영구 삭제는 CRXDE Lite에서 사용자 노드를 삭제하여 시스템에서 손쉽게 옵트아웃할 필요가 있음을 해결합니다.

또한, AEM Communities은 권한 있는 구성원이 사용자의 기여도와 세부 사항을 찾아서 삭제할 수 있는 벌크 중재 콘솔로 인해 개인 정보를 디자인함으로써 개인 정보를 제공합니다. 멤버 관리 콘솔에서는 기고자를 금지하는 지점으로 제한할 수 있습니다. 또한 데이터 주체가 작성된 기여도를 삭제할 수 있도록 허용합니다.

## AEM Forms {#aem-forms}

AEM Forms에는 데이터를 캡처, 처리 및 저장하여 비즈니스 프로세스를 조정하고 디지털 거래를 완료하는 구성 요소 및 워크플로우가 포함되어 있습니다. 다른 구성 요소는 서로 다른 데이터 저장소를 사용하고 사용자 지정 데이터 저장소와의 통합을 허용합니다. 다음 설명서는 구성 요소의 데이터 보호 및 개인 정보 보호(예: GDPR 또는 CCPA) 워크플로우를 지원하기 위해 사용자 데이터에 액세스하고 이를 처리하기 위한 절차와 지침을 설명합니다.

* [Forms 포털](/help/forms/using/forms-portal-handling-user-data.md)
* [서신 관리](/help/forms/using/correspondence-management-handling-user-data.md)
* [Adobe Sign과 통합](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi 기반의 Forms 워크플로우](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE 워크플로우](/help/forms/using/forms-workflow-jee-handling-user-data.md) (AEM Forms JEE만 해당)
* [문서 보안](/help/forms/using/document-security-handling-user-data.md) (AEM Forms JEE만 해당)
* [사용자 관리](/help/forms/using/user-management-handling-user-data.md) (AEM Forms JEE만 해당)
