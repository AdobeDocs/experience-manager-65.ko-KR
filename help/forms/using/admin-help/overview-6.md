---
title: SSL 구성 개요
description: SSL을 구성하여 통신 보안을 강화하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 100%
---
# SSL 구성 개요 {#overview-of-configuring-ssl}

애플리케이션 서버에서 SSL(Secure Sockets Layer) 자격 증명을 만들고 SSL을 구성하여 애플리케이션 서버와의 통신 보안을 강화할 수 있습니다.

보안 제품인 Rights Management를 사용하려면 SSL 구성이 필요합니다. SSL 인증서를 구성할 때 RSA 키만 사용해야 합니다. DSA 키가 포함된 SSL 인증서는 지원되지 않습니다.

제공된 정보는 턴키, 자동 및 수동 설치에 적용됩니다. SSL을 구성하는 방법에 대한 예를 제공합니다. 네트워크나 조직에 더 적합한 다른 방법을 사용할 수도 있습니다.

>[!NOTE]
>
>애플리케이션 서버에서 SSL을 구성하기 전에 AEM Forms 모듈의 설치, 구성 및 배포를 완료하고 제품이 올바르게 실행되는지 확인하는 것이 좋습니다.

>[!NOTE]
>
>SSL 보안 인증서와 자격 증명을 만들 때는 애플리케이션 서버를 실행하는 데 사용한 것과 동일한 사용자 계정 권한을 사용하십시오. 다른 사용자 권한을 사용하여 애플리케이션 서버를 실행하는 경우 ContentRootURI가 https를 가리킬 때 PDFForm 렌디션에 대한 양식이 제대로 렌더링되지 않을 수 있습니다.

SSL이 활성화된 LDAP 서버가 있는 경우 사용자 관리가 해당 서버와 함께 작동하도록 구성하십시오. ([SSL이 활성화된 LDAP 서버에 대한 사용자 관리 구성](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)을 참조하십시오.)
