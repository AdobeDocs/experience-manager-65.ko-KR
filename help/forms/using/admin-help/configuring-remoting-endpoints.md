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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '139'
ht-degree: 100%

---

# Remoting 엔드포인트 구성 {#configuring-remoting-endpoints}

Remoting 엔드포인트를 사용하면 Flex로 빌드된 애플리케이션에서 AEM Forms Remoting(AEM Forms에서는 더 이상 사용되지 않음)을 사용하여 서비스를 호출할 수 있습니다. 활성화된 각 서비스에 대해 Remoting 엔드포인트가 자동으로 생성됩니다. 엔드포인트와 이름이 동일한 Flex 대상이 생성되고 Flex 클라이언트는 이 대상을 가리키는 원격 오브젝트를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

## Remoting 엔드포인트 설정 {#remoting-endpoint-settings}

**Flex 클라이언트 인증 방법:** 호출된 서비스에 보안이 활성화되어 있고, 호출된 작업이 익명 호출을 지원하지 않으며, 클라이언트가 자격 증명을 전달하지 않거나 잘못된 자격 증명을 전달하는 경우 서버에서 클라이언트에 다시 보내는 응답 유형을 결정합니다.
