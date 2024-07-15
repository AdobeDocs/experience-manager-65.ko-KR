---
title: 원격 끝점 구성
description: 원격 끝점을 구성하는 방법에 대해 알아봅니다. 이 문서에서는 AEM Forms Remoting을 사용하여 Flex으로 빌드된 응용 프로그램에서 서비스를 호출할 수 있도록 설정하는 방법에 대해 설명합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# 원격 끝점 구성 {#configuring-remoting-endpoints}

원격 끝점을 사용하면 Flex으로 빌드된 응용 프로그램에서 (AEM Forms의 경우 더 이상 사용되지 않음) AEM Forms Remoting을 사용하여 서비스를 호출할 수 있습니다. 원격 끝점은 활성화된 각 서비스에 대해 자동으로 만들어집니다. 끝점과 이름이 같은 Flex 대상이 만들어지고 Flex 클라이언트는 이 대상을 가리키는 원격 개체를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

## 원격 끝점 설정 {#remoting-endpoint-settings}

**Flex 클라이언트 인증 방법:** 호출된 서비스가 보안을 사용하도록 설정되어 있고 호출된 작업이 익명 호출을 지원하지 않으며 클라이언트가 no 또는 invalid 자격 증명을 전달할 때 서버가 클라이언트로 다시 보내는 응답 형식을 결정합니다.
