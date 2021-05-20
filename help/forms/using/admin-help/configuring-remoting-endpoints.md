---
title: 원격 끝점 구성
seo-title: 원격 끝점 구성
description: 원격 끝점을 구성하는 방법을 알아봅니다.
seo-description: 원격 끝점을 구성하는 방법을 알아봅니다.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 원격 끝점 구성 중 {#configuring-remoting-endpoints}

원격 끝점을 사용하면 Flex으로 빌드된 응용 프로그램이 AEM Forms에서 사용되지 않는 AEM Forms Remoting을 사용하여 서비스를 호출할 수 있습니다. 활성화된 각 서비스에 대해 원격 끝점이 자동으로 만들어집니다. 종단점과 동일한 이름을 갖는 Flex 대상이 생성되며 Flex 클라이언트는 해당 대상을 가리키는 원격 개체를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

## 원격 끝점 설정 {#remoting-endpoint-settings}

**Flex 클라이언트 인증 방법:** 호출된 서비스가 보안 기능을 사용할 수 있고, 호출된 작업이 익명 호출을 지원하지 않으며, 클라이언트가 없거나 잘못된 자격 증명을 전달하면 서버가 클라이언트로 다시 보내는 응답 유형을 결정합니다.
