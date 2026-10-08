---
title: AEM Forms의 데이터 유지
description: Adobe Experience Manager(AEM) Forms이 기본적으로 통과 서버 역할을 하고 양식 최종 사용자 데이터를 저장하지 않으므로 데이터 개인 정보를 지원하는 방법에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin, User
solution: Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ca1448119778a2bcfeca7189aab5b360d992d99d
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%
---
# AEM Forms의 데이터 유지 {#data-retention-in-aem-forms}

AEM Forms은 양식 데이터를 저장합니까? 기본적으로 아니요. Adobe Experience Manager(AEM) Forms은 적응형 Forms을 통해 캡처된 데이터를 위한 통과 서버 역할을 하며, 최종 사용자 데이터를 AEM 저장소에 저장하지 않습니다. 대신 서버는 제출된 데이터를 사용자가 소유 및 구성하는 대상에 전달합니다. 이 기본 동작은 데이터 개인정보 보호 및 규정 준수 목표를 충족하는 데 도움이 되며 OSGi의 AEM Forms과 JEE의 AEM Forms에 모두 적용됩니다.

AEM Forms은 확장 가능한 플랫폼이므로 AEM을 사용자 지정하여 이 기본 동작을 변경할 수 있습니다. 사용자 정의가 적응형 양식을 통해 제출된 데이터를 AEM 저장소에 저장하거나 AEM 로그에 작성하는 경우, 이러한 데이터가 프로덕션 및 스테이징 시스템에 유지되지 않도록 해야 합니다.

## 기본 기능을 갖춘 기본 비헤이비어 {#default-behavior}

즉시 사용 가능한 적응형 Forms 기능을 사용하면 AEM Forms은 최종 사용자 데이터를 저장하지 않습니다. 서버는 제출된 데이터를 사용자가 소유 및 구성하는 대상에 직접 전달합니다.

양식을 소유한 대상에 연결하는 기본 제공 메커니즘에는 양식 데이터 모델(FDM), 기본 제공 커넥터 및 제출 작업이 포함됩니다. 이렇게 하면 각각 자신이 소유 및 구성한 위치로 데이터를 보내므로 AEM 저장소에 보존되지 않습니다. 양식은 규칙 또는 제출 작업에서 REST API와 같은 외부 또는 서드파티 서비스를 호출하고 AEM의 데이터를 지속하지 않고 데이터를 해당 서비스에 전달할 수도 있습니다.

승인 단계와 관련된 장기 프로세스가 있는 AEM Workflow를 사용하는 경우, AEM Forms은 메모리 및 임시 저장소에 데이터를 보관하여 작업을 완료할 수 있습니다. 이 데이터가 AEM에 저장되지 않도록 하는 방법에 대한 자세한 내용은 [장기 워크플로우 프로세스의 데이터](#long-lived-workflow-processes) 섹션을 참조하십시오.

Forms 포털 제출 액션은 적응형 Forms을 통해 캡처하거나 제출한 데이터를 유지하지만 데이터는 AEM 저장소나 로그가 아닌 사용자가 제공하고 소유한 저장소 위치에 저장됩니다. 자세한 내용은 [Forms 포털에서 저장한 데이터 보안 제출 작업](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-saved-by-forms-portal-submit-action)을 참조하십시오.

## 전송 중인 데이터 {#data-in-transit}

AEM Forms은 기본적으로 최종 사용자 데이터를 저장하지 않지만 최종 사용자인 AEM Forms과 사용자가 구성하는 대상 간에 데이터가 계속 이동합니다. 전송 중 데이터가 암호화되도록 TLS(전송 계층 보안)를 사용하여 이 트래픽을 보호합니다.

브라우저와 AEM 간의 연결을 보호하려면 AEM 인스턴스에서 HTTPS를 활성화합니다. 단계는 [기본적으로 SSL/TLS](/help/sites-administering/ssl-by-default.md)를 참조하십시오.

또한 AEM Forms이 데이터를 보내는 엔드포인트(예: 클라우드 구성, 제출 작업 URL 및 양식 데이터 모델 데이터 소스)가 보안 HTTPS 엔드포인트를 사용하는지 확인하십시오. AEM Forms은 통과하는 데이터를 저장하지 않으므로 사용하지 않는 암호화는 해당 데이터에 적용되지 않습니다. 연결 보안에 대한 자세한 지침은 [보안 전송 계층](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-transport-layer)을 참조하세요.

## 외부 데이터 저장소에 대한 양식 데이터 모델 {#form-data-model}

데이터 저장소에 데이터를 읽고 쓰려면 양식 데이터 모델(FDM)을 사용합니다. FDM은 소유하거나 관리하는 데이터 소스(예: 데이터베이스 또는 RESTful 웹 서비스)에 양식을 연결하는 데 권장되는 메커니즘입니다.

자세한 내용은 [AEM Forms 데이터 통합 소개](/help/forms/using/data-integration.md)를 참조하십시오. FDM이 처리하는 데이터 보안에 대한 자세한 내용은 [양식 데이터 모델(FDM)로 처리되는 데이터 보안](/help/forms/using/hardening-securing-aem-forms-environment.md#secure-data-handled-by-form-data-model-fdm)을 참조하십시오.

## 오래 지속되는 워크플로우 프로세스의 데이터 {#long-lived-workflow-processes}

수명이 긴 워크플로 프로세스를 사용하는 경우 AEM은 워크플로 페이로드의 일부로 데이터를 일시적으로 저장할 수 있습니다. 이 페이로드를 전달하는 워크플로우 변수는 AEM 저장소의 워크플로우 인스턴스 메타데이터에 저장되며, 적응형 양식을 작성하는 동안 최종 사용자가 제공하는 PII(개인 식별 정보) 또는 SPD(중요한 개인 데이터)를 포함할 수 있습니다.

이 데이터를 AEM이 아닌 Azure Blob 저장소와 같이 소유 및 관리하는 저장소에 보관하려면 AEM의 데이터 외부화 기능을 사용하십시오. 변수를 외부화할 때 데이터는 AEM 저장소에 저장되지 않고 대신 자체 데이터 저장소에 저장됩니다.

데이터를 외부화하는 단계는 [중요 데이터를 워크플로우 변수에 매개 변수화하고 외부 데이터 저장소에 저장](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)을 참조하십시오.

## 사용자 지정 및 로깅 {#customization-and-logging}

AEM은 사용자 정의 가능한 솔루션입니다. AEM을 사용자 지정하는 경우 사용자 지정에 AEM 저장소 또는 로그에 데이터가 저장되지 않도록 하십시오.

기본 기능을 사용하면 AEM Forms은 최종 사용자 데이터를 로그에 쓰지 않습니다.

사용자 지정 코드는 로그에 데이터를 쓸 수 있습니다. 개발 중에 추적 또는 로깅을 추가하는 경우 스테이징 및 프로덕션 환경에 코드를 배포하기 전에 로그에 전송된 추적 및 데이터를 제거합니다.

## AEM Forms 데이터 유지에 대한 FAQ {#faq}

**AEM Forms에서 양식 데이터를 저장합니까?**

아니요. 기본적으로 Adobe Experience Manager(AEM) Forms은 적응형 Forms을 통해 캡처된 데이터에 대한 통과 서버 역할을 하며 최종 사용자 데이터를 AEM 저장소에 저장하지 않습니다. 서버는 제출된 데이터를 양식 데이터 모델 데이터 소스, 제출 액션 대상 또는 외부 API와 같이 사용자가 소유 및 구성하는 대상에 전달합니다. 이 기본 동작은 OSGi의 AEM Forms과 JEE의 AEM Forms 모두에 적용됩니다.

**적응형 양식 데이터는 어디에 저장되어 있습니까?**

제출된 적응형 양식 데이터는 Adobe Experience Manager(AEM) 저장소가 아닌 사용자가 소유 및 구성하는 대상에 저장됩니다. 양식 데이터 모델(FDM), 커넥터 및 제출 작업과 같은 기본 메커니즘으로 인해 데이터가 고유한 위치로 전송됩니다. 양식은 AEM에서 지속하지 않고 REST API와 같은 외부 서비스로 데이터를 전달할 수도 있습니다. 또한 Forms 포털 제출 액션은 제공하고 소유한 저장소 위치에 데이터를 저장합니다.

**오래 지속되는 워크플로우에서 양식 데이터를 저장합니까?**

Adobe Experience Manager(AEM) Forms의 장기 워크플로 프로세스는 AEM 저장소의 워크플로 인스턴스 메타데이터에 저장된 워크플로 페이로드의 일부로 데이터를 임시 저장할 수 있습니다. 이 데이터를 AEM이 아닌 Azure Blob 저장소와 같이 소유 및 관리하는 저장소에 보관하려면 워크플로우 변수에 대해 [AEM 데이터 외부화 기능](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)을 사용하십시오.

**AEM Forms에서 로그에 데이터를 기록합니까?**

아니요. 기본 기능을 사용하면 Adobe Experience Manager(AEM) Forms은 최종 사용자 데이터를 로그에 기록하지 않습니다. AEM은 사용자 지정 가능한 플랫폼이므로 사용자 지정 코드는 데이터를 로그에 쓸 수 있습니다. 개발 중에 추적 또는 로깅을 추가하는 경우 스테이징 및 프로덕션 환경에 배포하기 전에 이러한 추적 및 기록된 데이터를 제거합니다. 사용자 지정은 AEM 저장소 또는 로그에 데이터를 저장하지 않아야 합니다.

**전송 중인 데이터는 어떻게 보호됩니까?**

전송 중인 데이터는 Adobe Experience Manager(AEM) Forms에서 전송 계층 보안(TLS)으로 보호됩니다. AEM 인스턴스에서 HTTPS를 활성화하여 브라우저와 AEM 간의 연결을 보호합니다. 또한 AEM Forms이 데이터를 보내는 엔드포인트(예: 클라우드 구성, 제출 액션 URL 및 양식 데이터 모델 데이터 소스)에서 보안 HTTPS 엔드포인트를 사용하도록 하십시오. AEM Forms은 전달하는 데이터를 저장하지 않으므로 사용하지 않는 암호화는 해당 데이터에 적용되지 않습니다.

## 관련 리소스 {#related-resources}

* [AEM Forms 데이터 통합 소개](/help/forms/using/data-integration.md)
* [중요한 데이터를 워크플로우 변수에 매개 변수화하고 외부 데이터 저장소에 저장](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)
* [제출 작업 구성](/help/forms/using/configuring-submit-actions.md)
* [OSGi 환경에서 AEM Forms 강화 및 보호](/help/forms/using/hardening-securing-aem-forms-environment.md)
