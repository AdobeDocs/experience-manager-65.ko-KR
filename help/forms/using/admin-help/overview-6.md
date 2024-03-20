---
title: SSL 구성 개요
description: SSL을 구성하여 통신 보안을 강화하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# SSL 구성 개요 {#overview-of-configuring-ssl}

SSL(Secure Sockets Layer) 자격 증명을 생성하고 애플리케이션 서버에서 SSL을 구성하여 애플리케이션 서버와의 통신 보안을 강화할 수 있습니다.

보안 제품으로서, Rights Management은 SSL을 구성해야 합니다. SSL 인증서를 구성할 때는 RSA 키만 사용해야 합니다. DSA 키가 있는 SSL 인증서는 지원되지 않습니다.

제공된 정보는 턴키, 자동 및 수동 설치에 적용됩니다. 이 섹션에서는 SSL 구성 방법의 예를 제공합니다. 네트워크나 조직에 더 적합한 다른 방법을 사용할 수도 있습니다.

>[!NOTE]
>
>애플리케이션 서버에서 SSL을 구성하기 전에 AEM Forms 모듈의 설치, 구성 및 배포를 완료하고 제품이 올바르게 실행되고 있는지 확인하는 것이 좋습니다.

>[!NOTE]
>
>SSL 보안 인증서 및 자격 증명을 생성할 때 애플리케이션 서버를 실행하는 데 사용한 것과 동일한 사용자 계정 권한을 사용합니다. 응용 프로그램 서버가 다른 사용자 권한을 사용하여 실행되는 경우 ContentRootURI가 https를 가리키면 양식이 PDForm 표현물에 대해 제대로 렌더링되지 않을 수 있습니다.

SSL을 사용할 수 있는 LDAP 서버가 있는 경우 사용할 수 있도록 사용자 관리를 구성합니다. (참조: [SSL 사용 LDAP 서버에 대한 사용자 관리 구성](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
