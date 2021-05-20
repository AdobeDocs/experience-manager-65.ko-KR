---
title: 데이터 보호 및 데이터 개인 정보 보호 규정 - Adobe Experience Manager 준비 완료
seo-title: 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 준비 완료GDPR, CCPA 등
description: '다양한 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 지원에 대해 알아봅니다.에는 유럽 연합 개인 정보 보호 규정(GDPR), 캘리포니아 소비자 개인 정보 보호법 및 새 AEM 프로젝트를 구현할 때 준수하는 방법이 포함되어 있습니다. '
seo-description: '다양한 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 지원에 대해 알아봅니다.에는 유럽 연합 개인 정보 보호 규정(GDPR), 캘리포니아 소비자 개인 정보 보호법 및 새 AEM 프로젝트를 구현할 때 준수하는 방법이 포함되어 있습니다. '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 1%

---

# 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 준비 완료 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>이 문서의 컨텐츠는 법률적인 조언을 구성하지 않으며 법률적인 조언을 대체하지 않습니다.
>
>데이터 보호 및 데이터 개인 정보 보호 규정에 대한 자세한 내용은 회사의 법무 부서에 문의하십시오.

>[!NOTE]
>
>개인 정보 보호 문제에 대한 Adobe의 응답 및 Adobe 고객으로서 사용자에게 의미하는 바에 대한 자세한 내용은 [Adobe의 개인 정보 센터](https://www.adobe.com/privacy.html)를 참조하십시오.

Adobe은 고객 개인 정보 보호 관리자 또는 AEM 관리자가 데이터 보호 및 데이터 개인 정보 보호 요청을 처리하고 고객이 이러한 규정을 준수하도록 지원하는 API와 함께 문서 및 절차를 제공합니다. 정리된 절차를 통해 고객은 수동으로 또는 외부 포털 또는 서비스에서 API를 호출하여 규정 요청을 실행할 수 있습니다.

>[!CAUTION]
>
>여기에 설명된 세부 사항은 Adobe Experience Manager으로 제한됩니다.
>
>다른 Adobe 온디맨드 서비스의 데이터와 관련 개인 정보 보호 요청은 해당 서비스에 대해 조치를 취해야 합니다.
>
>자세한 내용은 [Adobe의 개인 정보 보호 센터](https://www.adobe.com/privacy.html)를 참조하십시오.

## 소개 {#introduction}

Adobe Experience Manager의 인스턴스와 이러한 인스턴스에서 실행되는 애플리케이션의 인스턴스는 Adobe 고객이 소유하고 관리합니다.

따라서 GDPR, CCPA 등과 같은 데이터 보호 규정은 고객의 책임입니다.

매우 간략하게 소개되는 데이터 개인 정보 보호 및 보호에 대한 규정에는 다음과 같은 역할이 따라야 하는 새로운 규칙이 포함됩니다.

* CCPA(Business Entity) 및/또는 GDPR(데이터 통제자)

* CCPA(서비스 공급자) 및/또는 GDPR(데이터 프로세서)

이러한 규정의 주요 내용은 다음과 같습니다.

1. 모든 고유 ID를 포함하도록 개인 데이터의 확장된 정의를 직접 및 간접적으로 식별 가능한 데이터에서 사용할 수 있습니다.

2. 강화된 동의 요구 사항.

3. 삭제 권한 (데이터 삭제)에 중점을 둡니다.

4. 데이터 판매 거부.

Adobe Experience Manager의 경우:

* 인스턴스 및 이 인스턴스에서 실행되는 응용 프로그램은 고객이 소유하여 운영하고 있습니다.

   * 이는 고객이 비즈니스 엔터티 및 서비스 공급자, 데이터 컨트롤러, 데이터 프로세서 등 규정 역할을 관리함을 효과적으로 의미합니다.

   * 아래 다이어그램에 나와 있는 대로 Adobe Experience Platform Privacy Service은 AEM용 워크플로우의 일부가 아닙니다.

* AEM에는 고객의 개인 정보 보호 관리자 및/또는 AEM 관리자가 개인 정보 보호 규정 요청을 실행하기 위한 설명서 및 절차가 포함되어 있습니다.수동으로 또는 API를 통해 가능한 경우 선택할 수 있습니다.

* 새 서비스 또는 UI가 추가되지 않았습니다.

   * 대신 개인 정보 보호 규정 요청을 처리하는 고객 UI/포털에서 사용하기 위해 절차 및 API를 문서화합니다.

* AEM에는 개인 정보 요청 워크플로우를 지원하는 기본 도구 모음이 포함되지 않습니다.

   * Adobe은 고객의 개인 정보 보호 관리자 및/또는 AEM 관리자에 대한 설명서 및 절차를 제공하며, 이 절차를 통해 개인 정보 보호 규정과 관련된 요청을 수동으로 실행할 수 있습니다.

Adobe은 Adobe Experience Manager에 대한 액세스, 삭제 및 옵트아웃과 관련된 개인 정보 보호 요청을 처리하는 절차를 제공하고 있습니다. 경우에 따라 고객이 개발한 포털이나 스크립트에서 자동화를 지원하기 위해 호출할 수 있는 API가 있습니다.

다음 다이어그램은 개인 정보 보호 요청 워크플로우의 모양을 보여줍니다(Adobe Experience Manager 6.5 사용 그림).

![데이터 보호 및 개인 정보](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager 및 규정 준비 {#aem-and-regulatory-readiness}

AEM 제품 영역에 대한 규정 설명서는 아래 섹션을 참조하십시오.

## AEM 기반 정보 {#aem-foundation}

AEM Foundation](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)에 대한 데이터 보호 및 개인 정보 보호 요청 처리 를 참조하십시오.[

## AEM 총 사용량 통계 수집 선택 {#aem-opting-into-aggregate-usage-statistics-collection}

[집계된 사용 통계 컬렉션](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)을 참조하십시오.

## AEM Sites {#aem-sites}

[AEM Sites - 데이터 보호 및 개인 정보 보호 준비를 참조하십시오.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

[AEM Commerce - 데이터 보호 및 개인 정보 보호 준비](/help/sites-administering/gdpr-compliance-commerce.md)를 참조하십시오.

## AEM Mobile {#aem-mobile}

[AEM Mobile - 데이터 보호 및 개인 정보 보호 준비](/help/mobile/aem-mobile-gdpr-compliance.md)를 참조하십시오.

## Adobe Target 및 Adobe Analytics과 AEM 통합 {#aem-integration-with-adobe-target-adobe-analytics}

이러한 Adobe Experience Manager 통합은 데이터 보호 및 개인 정보 보호(예: GDPR 또는 CCPA) 지원 서비스와 함께 제공됩니다. Adobe Target 또는 Adobe Analytics의 개인 데이터는 통합과 관련하여 AEM에 저장되지 않습니다.
자세한 내용은 다음을 참조하십시오.

* [Adobe Target - 개인 정보 보호 개요](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics 데이터 개인 정보 보호 워크플로우](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities은 데이터 주체에게 데이터 이동성, 액세스 권한 및 [기본 제공 API](/help/communities/user-ugc-management-service.md)를 통해 잊혀질 권리 등을 제공합니다. 이러한 API를 사용하면 사용자 생성 컨텐츠를 벌크 삭제 및 대량 내보낼 수 있으며, 작성 가능한 ID를 통해 식별된 사용자 계정을 비활성화할 수 있습니다. 그러나 사용자 계정의 영구 삭제는 CRXDE Lite에서 사용자 노드를 삭제함으로써 구현되므로 시스템에서 쉽게 옵트아웃할 필요가 있습니다.

또한 AEM Communities에서는 권한 있는 구성원이 사용자의 기여 및 세부 사항을 찾아 삭제할 수 있는 벌크 중재 콘솔로 인해 디자인별 개인 정보를 제공합니다. 구성원 관리 콘솔을 사용하면 기여자를 금지하는 지점으로 제한할 수 있습니다. 또한 데이터 주체는 해당 사용자가 작성한 기여도를 삭제할 수 있도록 허용합니다.

## AEM Forms {#aem-forms}

AEM Forms에는 데이터를 캡처, 처리 및 저장하여 비즈니스 프로세스를 조정하고 디지털 트랜잭션을 완료하는 구성 요소 및 워크플로우가 포함되어 있습니다. 다른 구성 요소는 서로 다른 데이터 저장소를 사용하고 사용자 지정 데이터 스토어와의 통합을 허용합니다. 다음 설명서에서는 구성 요소에 대한 데이터 보호 및 개인 정보 보호(예: GDPR 또는 CCPA) 워크플로우를 지원하기 위해 사용자 데이터에 액세스 및 처리하는 절차 및 지침에 대해 설명합니다.

* [Forms 포털](/help/forms/using/forms-portal-handling-user-data.md)
* [서신 관리](/help/forms/using/correspondence-management-handling-user-data.md)
* [Adobe Sign과 통합](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi의 Forms 중심 워크플로우](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE 워크플로우](/help/forms/using/forms-workflow-jee-handling-user-data.md) (AEM Forms JEE만 해당)
* [문서 보안](/help/forms/using/document-security-handling-user-data.md) (AEM Forms JEE만 해당)
* [사용자 관리](/help/forms/using/user-management-handling-user-data.md) (AEM Forms JEE만 해당)
