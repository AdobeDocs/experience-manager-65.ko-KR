---
title: 엔드포인트 유형
description: 다양한 유형의 엔드포인트에 대해 알아봅니다. 이메일, 감시 폴더 등과 같은 다양한 유형의 엔드포인트를 서비스에 추가할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 엔드포인트 유형 {#types-of-endpoints}

서비스를 사용하려면 먼저 끝점을 구성하고 활성화해야 합니다. 끝점은 서비스 호출 방법을 지정합니다.

>[!NOTE]
>
>Workbench에서 끝점을 시작점이라고 합니다.

서비스에 다음 유형의 끝점을 추가할 수 있습니다. 모든 서비스가 모든 끝점을 지원하는 것은 아닙니다.

**이메일:** 사용자가 하나 이상의 첨부 파일이 있는 이메일 메시지를 지정된 이메일 계정으로 전송하여 서비스를 호출할 수 있습니다. 이메일 엔드포인트를 구성하기 전에 필요한 이메일 계정을 구성해야 합니다. (이메일 엔드포인트 구성 참조)

**감시 폴더:** 사용자가 정의된 간격으로 스캔되는 폴더에 파일을 배치하여 서비스를 호출할 수 있습니다. 자세한 내용은 감시 폴더 엔드포인트 구성 을 참조하십시오.

**작업 관리자:** 작업 영역 사용자가 서비스를 호출할 수 있습니다.

**원격:** Flex으로 구축된 응용 프로그램에서 (AEM Forms의 경우 더 이상 사용되지 않음) AEM Forms Remoting을 사용하여 서비스를 호출할 수 있도록 합니다. 원격 끝점은 활성화된 각 서비스에 대해 자동으로 만들어집니다. 끝점과 이름이 같은 Flex 대상이 만들어지고 Flex 클라이언트는 이 대상을 가리키는 원격 개체를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

**SOAP:** AEM Forms 프로그래밍 API를 사용하여 개발된 클라이언트 응용 프로그램에서 SOAP 모드를 사용하여 서비스를 호출할 수 있도록 합니다. SOAP 끝점은 활성화된 각 서비스에 대해 자동으로 만들어집니다.

**참고**: *Adobe Acrobat 또는 Adobe Reader에서 문서를 보는 동안 SOAP 끝점을 사용하면 문서 보안 문서에서 보안을 제거할 수 있습니다. LCRM 문서에서 SOAP Enpoints를 비활성화하는 방법에 대한 자세한 내용은 [문서 보안 문서에 대한 SOAP 끝점 비활성화](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** AEM Forms 프로그래밍 API를 사용하여 개발된 클라이언트 애플리케이션이 EJB(Enterprise JavaBeans) 모드를 사용하여 서비스를 호출할 수 있도록 합니다. EJB 끝점은 활성화된 각 서비스에 대해 자동으로 만들어집니다.

**WSDL:** AEM Forms 프로그래밍 API를 사용하여 개발된 클라이언트 응용 프로그램이 WSDL(Web Service Definition Language)을 사용하여 서비스를 호출할 수 있도록 합니다. 코어 구성 페이지에는 AEM 양식의 일부인 모든 서비스에 대해 WSDL 생성을 활성화하는 옵션이 포함되어 있습니다. 자세한 내용은 일반 AEM 양식 설정 구성 을 참조하십시오.

**REST:** Workbench에서 생성된 프로세스는 REST(표현 상태 전송) 요청을 통해 호출할 수 있도록 구성할 수 있습니다. REST 요청은 HTML 페이지에서 전송됩니다. 즉, REST 요청을 사용하여 웹 페이지에서 직접 AEM Forms 프로세스를 호출할 수 있습니다.

이메일, 작업 관리자, 감시 폴더 및 원격 끝점은 서비스의 특정 작업만 표시합니다. 이러한 끝점을 추가하려면 서비스를 호출할 방법을 선택하고, 구성 매개 변수를 설정하고, 입력 및 출력 매개 변수 매핑을 지정하는 두 번째 구성 단계가 필요합니다.
