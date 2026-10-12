---
title: Remoting 엔드포인트 구성
description: Remoting 엔드포인트를 구성하는 방법을 알아봅니다. 이 문서에서는 Flex로 빌드된 애플리케이션에서 AEM Forms Remoting을 사용하여 서비스를 호출하도록 하는 방법을 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
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
source-wordcount: '139'
ht-degree: 100%
---
# Remoting 엔드포인트 구성 {#configuring-remoting-endpoints}

Remoting 엔드포인트를 사용하면 Flex로 빌드된 애플리케이션에서 AEM Forms Remoting(AEM Forms에서는 더 이상 사용되지 않음)을 사용하여 서비스를 호출할 수 있습니다. 활성화된 각 서비스에 대해 Remoting 엔드포인트가 자동으로 생성됩니다. 엔드포인트와 이름이 동일한 Flex 대상이 생성되고 Flex 클라이언트는 이 대상을 가리키는 원격 오브젝트를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

## Remoting 엔드포인트 설정 {#remoting-endpoint-settings}

**Flex 클라이언트 인증 방법:** 호출된 서비스에 보안이 활성화되어 있고, 호출된 작업이 익명 호출을 지원하지 않으며, 클라이언트가 자격 증명을 전달하지 않거나 잘못된 자격 증명을 전달하는 경우 서버에서 클라이언트에 다시 보내는 응답 유형을 결정합니다.
