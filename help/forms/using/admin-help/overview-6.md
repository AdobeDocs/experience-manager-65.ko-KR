---
title: SSL 구성 개요
seo-title: SSL 구성 개요
description: SSL을 구성하여 통신 보안을 강화하는 방법에 대해 알아봅니다.
seo-description: SSL을 구성하여 통신 보안을 강화하는 방법에 대해 알아봅니다.
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# SSL 구성 개요 {#overview-of-configuring-ssl}

SSL(Secure Sockets Layer) 자격 증명을 만들고 응용 프로그램 서버에 SSL을 구성하여 응용 프로그램 서버와의 통신 보안을 강화할 수 있습니다.

보안 제품으로서 Rights Management는 SSL을 구성해야 합니다. SSL 인증서를 구성할 때 RSA 키만 사용하는지 확인하십시오. DSA 키가 있는 SSL 인증서는 지원되지 않습니다.

제공된 정보는 턴키, 자동 및 수동 설치에 적용됩니다. SSL을 구성하는 방법의 예를 제공합니다. 네트워크 또는 조직에 더 적합한 다른 방법을 사용할 수도 있습니다.

>[!NOTE]
>
>AEM 양식 모듈의 설치, 구성 및 배포를 완료하고 응용 프로그램 서버에서 SSL을 구성하기 전에 제품이 올바르게 실행되는지 확인하는 것이 좋습니다.

>[!NOTE]
>
>SSL 보안 인증서 및 자격 증명을 만들 때 응용 프로그램 서버를 실행하는 데 사용한 것과 동일한 사용자 계정 권한을 사용합니다. 다른 사용자 권한을 사용하여 응용 프로그램 서버를 실행하는 경우 ContentRootURI가 https를 가리키는 경우 PDForm 변환에 대해 양식이 제대로 렌더링되지 않을 수 있습니다.

SSL이 활성화된 LDAP 서버가 있는 경우 사용자 관리를 구성하여 사용합니다. SSL [사용 LDAP 서버에](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)대한 사용자 관리 구성을 참조하십시오.
