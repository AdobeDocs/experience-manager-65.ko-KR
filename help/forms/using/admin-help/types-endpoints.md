---
title: 끝점 유형
seo-title: Types of endpoints
description: 다양한 유형의 엔드포인트에 대해 알아봅니다.
seo-description: Learn about the different types of endpoints.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 끝점 유형 {#types-of-endpoints}

서비스를 사용하려면 엔드포인트를 구성하고 활성화해야 합니다. 끝점은 서비스를 호출하는 방법을 지정합니다.

>[!NOTE]
>
>Workbench에서 끝점은 시작점이라고 합니다.

다음 유형의 끝점을 서비스에 추가할 수 있습니다. 일부 서비스에서는 모든 끝점을 지원하지 않습니다.

**이메일:** 사용자가 하나 이상의 파일 첨부 파일이 있는 전자 메일 메시지를 지정된 전자 메일 계정에 전송하여 서비스를 호출할 수 있습니다. 이메일 끝점을 구성하려면 먼저 필요한 이메일 계정을 구성해야 합니다. 자세한 내용은 전자 메일 엔드포인트 구성을 참조하십시오.

**감시 폴더:** 정의된 간격으로 스캔되는 폴더에 파일을 배치하여 서비스를 호출할 수 있도록 합니다. 감시 폴더 엔드포인트 구성을 참조하십시오.

**작업 관리자:** Workspace 사용자가 서비스를 호출할 수 있도록 합니다.

**원격:** Flex으로 빌드된 애플리케이션에서 AEM Forms Remoting을 사용하여 서비스를 호출할 수 있도록 설정합니다(AEM Forms에서는 더 이상 사용되지 않음). 활성화된 각 서비스에 대해 원격 끝점이 자동으로 만들어집니다. 종단점과 동일한 이름을 갖는 Flex 대상이 생성되며 Flex 클라이언트는 해당 대상을 가리키는 원격 개체를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

**SOAP:** AEM Forms 프로그래밍 API를 사용하여 개발된 클라이언트 응용 프로그램에서 SOAP 모드를 사용하여 서비스를 호출할 수 있도록 합니다. 활성화된 각 서비스에 대해 SOAP 엔드포인트가 자동으로 만들어집니다.

**참고**: *Adobe Acrobat 또는 Adobe Reader에서 문서를 보는 동안 SOAP 종단점을 사용하는 경우 문서 보안 문서에서 보안을 제거할 수 있습니다. LCRM 문서에서 SOAP 끝점을 비활성화하는 방법에 대한 자세한 내용은 다음을 참조하십시오 [문서 보안 문서에 대한 SOAP 끝점을 사용하지 않습니다.](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** AEM Forms 프로그래밍 API를 사용하여 개발된 클라이언트 응용 프로그램에서 EJB(Enterprise JavaBeans) 모드를 사용하여 서비스를 호출할 수 있습니다. 활성화된 각 서비스에 대해 EJB 엔드포인트가 자동으로 생성됩니다.

**WSDL:** AEM Forms 프로그래밍 API를 사용하여 개발된 클라이언트 응용 프로그램에서 WSDL(웹 서비스 정의 언어)을 사용하여 서비스를 호출할 수 있습니다. 핵심 구성 페이지에는 AEM Forms의 일부인 모든 서비스에 대해 WSDL을 생성할 수 있도록 하는 옵션이 포함되어 있습니다. 자세한 내용은 일반 AEM 양식 설정 구성을 참조하십시오.

**REST:** Workbench에서 만든 프로세스는 REST(대리 상태 전송) 요청을 통해 호출할 수 있도록 구성할 수 있습니다. REST 요청은 HTML 페이지에서 전송됩니다. 즉, REST 요청을 사용하여 웹 페이지에서 직접 AEM Forms 프로세스를 호출할 수 있습니다.

전자 메일, TaskManager, 감시 폴더 및 원격 끝점은 서비스의 특정 작업만 노출합니다. 이러한 끝점을 추가하면 서비스를 호출할 메서드를 선택하고, 구성 매개 변수를 설정하고, 입력 및 출력 매개 변수 매핑을 지정하는 두 번째 구성 단계가 필요합니다.
