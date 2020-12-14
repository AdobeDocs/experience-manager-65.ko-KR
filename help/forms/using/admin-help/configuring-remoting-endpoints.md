---
title: 원격 끝점 구성
seo-title: 원격 끝점 구성
description: 원격 끝점을 구성하는 방법에 대해 알아봅니다.
seo-description: 원격 끝점을 구성하는 방법에 대해 알아봅니다.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# 원격 끝점 구성 중 {#configuring-remoting-endpoints}

원격 끝점은 Flex으로 빌드된 응용 프로그램이 AEM 양식 Remoting을 사용하여 서비스를 호출할 수 있도록 합니다(AEM 양식에 대해 더 이상 사용되지 않음). 활성화된 각 서비스에 대해 원격 끝점이 자동으로 만들어집니다. 끝점과 동일한 이름을 갖는 Flex 대상을 만들고 Flex 클라이언트는 이 대상을 가리키는 원격 개체를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

## 원격 끝점 설정 {#remoting-endpoint-settings}

**Flex 클라이언트 인증 방법:** 호출된 서비스가 보안을 사용하도록 설정했을 때 서버가 클라이언트에 다시 보내는 응답 유형을 결정합니다. 호출된 작업은 익명 호출을 지원하지 않으며 클라이언트는 no 또는 invalid 자격 증명을 전달합니다.
