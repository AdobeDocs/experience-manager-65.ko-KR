---
title: 데이터 보호 및 데이터 개인 정보 보호 규정 - Adobe Experience Manager 준비 완료
description: 다양한 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 지원에 대해 알아봅니다. 여기에는 EU GDPR(일반 데이터 보호 규정), 캘리포니아 소비자 개인 정보 보호법 및 새 AEM 프로젝트를 구현할 때 준수하는 방법이 포함되어 있습니다.
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 25%

---

# 데이터 보호 및 데이터 개인 정보 보호 규정에 대한 Adobe Experience Manager 준비 완료 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>이 문서의 콘텐츠는 법률적인 조언을 포함하지 않으며, 법률적인 조언을 대체하지 않습니다.
>
>데이터 보호 및 데이터 개인 정보 보호 규정에 대한 자세한 내용은 회사의 법무 부서에 문의하십시오.

>[!NOTE]
>
>개인 정보 보호 문제에 대한 Adobe의 대응 및 Adobe 고객으로서 사용자에게 미치는 영향에 대한 자세한 내용은 [Adobe 개인 정보 보호 센터](https://www.adobe.com/kr/privacy.html).

Adobe은 고객 개인 정보 보호 관리자 또는 AEM 관리자가 데이터 보호 및 데이터 개인 정보 보호 요청을 처리할 수 있도록 API와 함께 문서 및 절차를 제공합니다. 이것은 여러분이 이러한 규정을 준수하도록 도울 수 있습니다. 정리된 절차를 통해 고객은 수동으로 또는 외부 포털 또는 서비스에서 API를 호출하여 규정 준수 요청을 실행할 수 있습니다.

>[!CAUTION]
>
>여기에 설명된 세부 사항은 Adobe Experience Manager으로 제한됩니다.
>
>다른 Adobe 온디맨드 서비스의 데이터와 관련 개인 정보 보호 요청은 해당 서비스에 대해 조치를 취해야 합니다.
>
>자세한 내용은 [Adobe 개인 정보 보호 센터](https://www.adobe.com/kr/privacy.html).

## 소개 {#introduction}

Adobe Experience Manager 인스턴스와 이러한 인스턴스에서 실행되는 애플리케이션의 인스턴스는 Adobe 고객이 소유하고 관리합니다.

따라서 GDPR, CCPA 및 기타 데이터 보호 규정에 대한 책임은 고객에게 있습니다.

데이터 개인 정보 보호 및 보호에 대한 간략한 소개에는 다음과 같은 역할이 따라야 하는 새로운 규칙이 포함됩니다.

* 비즈니스 엔티티(CCPA) 및/또는 데이터 컨트롤러(GDPR)

* 서비스 공급자(CCPA) 및/또는 데이터 프로세서(GDPR)

이들 규정에서의 주요 프로비전은 다음과 같습니다.

1. 직접 또는 간접적으로 식별 가능한 데이터와 같이 모든 고유 ID를 포함하도록 개인 데이터의 정의 확장

2. 동의 요구 사항 강화

3. 삭제 권한(데이터 삭제)에 대한 집중 강화

4. 데이터 판매 옵트아웃

Adobe Experience Manager의 경우:

* 인스턴스 및 해당 인스턴스에서 실행되는 애플리케이션은 고객이 소유 및 운영합니다.

   * 고객은 비즈니스 엔터티 및 서비스 공급자, 데이터 컨트롤러, 데이터 프로세서 등의 규정 역할을 관리합니다.

   * 아래 다이어그램에 나와 있는 대로 Adobe Experience Platform Privacy Service은 AEM용 워크플로우의 일부가 아닙니다.

* AEM에는 고객의 개인정보 보호 관리자 및/또는 AEM 관리자가 수동으로 또는 가능한 경우 API를 통해 개인정보 보호 규정 요청을 실행하도록 하는 문서 및 절차가 포함되어 있습니다.

* 새 서비스나 UI는 추가되지 않았습니다.

   * 대신 개인정보 보호 규정 요청을 처리하는 고객 UI/포털에서 사용할 수 있도록 절차 및 API가 문서화되었습니다.

* AEM에는 개인 정보 요청 워크플로우를 지원하는 기본 도구 모음이 포함되어 있지 않습니다.

   * Adobe은 고객의 개인 정보 보호 관리자 및 AEM 관리자에 대한 설명서 및 절차를 제공하여 개인 정보 보호 규정 관련 요청을 수동으로 실행할 수 있도록 합니다.

Adobe은 Adobe Experience Manager에 대한 액세스, 삭제 및 옵트아웃과 관련된 개인 정보 보호 요청을 처리하는 절차를 제공합니다. 고객이 개발한 포털이나 스크립트에서 자동화를 지원하기 위해 호출할 수 있는 API가 있는 경우가 있습니다.

다음 다이어그램은 개인정보 보호 요청 워크플로의 형태를 보여 줍니다(Adobe Experience Manager 6.5를 사용하여 설명함).

![데이터 보호 및 개인정보 보호](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager 및 규정 준비 {#aem-and-regulatory-readiness}

AEM의 제품 영역에 대한 규정 설명서는 아래 섹션을 참조하십시오.

## AEM 기반 정보 {#aem-foundation}

자세한 내용은 [AEM Foundation에 대한 데이터 보호 및 개인 정보 보호 요청 처리](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM 총 사용량 통계 수집 선택 {#aem-opting-into-aggregate-usage-statistics-collection}

자세한 내용은 [집계된 사용 통계 수집](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

자세한 내용은 [AEM Sites - 데이터 보호 및 개인 정보 보호 준비 완료.](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

자세한 내용은 [AEM Commerce - 데이터 보호 및 개인 정보 보호 준비 완료](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

자세한 내용은 [AEM Mobile - 데이터 보호 및 개인 정보 보호 준비 완료](/help/mobile/aem-mobile-gdpr-compliance.md).

## Adobe Target 및 Adobe Analytics과 AEM 통합 {#aem-integration-with-adobe-target-adobe-analytics}

이러한 Adobe Experience Manager 통합은 데이터 보호 및 개인 정보 보호(예: GDPR 또는 CCPA) 지원 서비스와 함께 제공됩니다. 해당 통합과 관련하여 어떠한 Adobe Target 또는 Adobe Analytics의 개인 데이터도 AEM에 저장되지 않습니다.

자세한 내용은 다음을 참조하십시오.

* [Adobe Target - 개인정보 보호 개요](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Adobe Analytics 데이터 개인정보 보호 워크플로](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities은 데이터 주체에게 데이터 이동성, 액세스 권한 및 잊혀질 권리 등에 대해 탁월한 역량을 제공합니다 [기본 API](/help/communities/user-ugc-management-service.md). 이러한 API를 사용하면 사용자 생성 컨텐츠를 벌크 삭제 및 대량 내보낼 수 있으며, 작성 가능한 ID를 통해 식별된 사용자 계정을 비활성화할 수 있습니다. 그러나 사용자 계정의 영구 삭제는 CRXDE Lite에서 사용자 노드를 삭제함으로써 구현되므로 시스템에서 쉽게 옵트아웃할 필요가 있습니다.

또한 AEM Communities에서는 권한 있는 구성원이 사용자의 기여 및 세부 사항을 찾아 삭제할 수 있는 벌크 중재 콘솔 덕분에 디자인별 개인 정보를 제공합니다. 구성원 관리 콘솔을 사용하면 기여자를 금지하는 지점으로 제한할 수 있습니다. 또한 데이터 주체는 해당 사용자가 작성한 기여도를 삭제할 수 있도록 허용합니다.

## AEM Forms {#aem-forms}

AEM Forms에는 데이터를 캡처, 처리 및 저장하여 비즈니스 프로세스를 조정하고 디지털 트랜잭션을 완료하는 구성 요소 및 워크플로우가 포함되어 있습니다. 다른 구성 요소는 서로 다른 데이터 저장소를 사용하고 사용자 지정 데이터 스토어와의 통합을 허용합니다. 다음 설명서에서는 구성 요소에 대한 데이터 보호 및 개인 정보 보호(예: GDPR 또는 CCPA) 워크플로우를 지원하기 위해 사용자 데이터에 액세스 및 처리하는 절차 및 지침에 대해 설명합니다.

* [Forms 포털](/help/forms/using/forms-portal-handling-user-data.md)
* [서신 관리](/help/forms/using/correspondence-management-handling-user-data.md)
* [Adobe Sign과 통합](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi의 Forms 중심 워크플로우](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE 워크플로우](/help/forms/using/forms-workflow-jee-handling-user-data.md) (AEM Forms JEE만 해당)
* [문서 보안](/help/forms/using/document-security-handling-user-data.md) (AEM Forms JEE만 해당)
* [사용자 관리](/help/forms/using/user-management-handling-user-data.md) (AEM Forms JEE만 해당)
