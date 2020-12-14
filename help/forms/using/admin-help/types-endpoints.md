---
title: 끝점 유형
seo-title: 끝점 유형
description: 다양한 유형의 끝점에 대해 알아봅니다.
seo-description: 다양한 유형의 끝점에 대해 알아봅니다.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# 끝점 유형 {#types-of-endpoints}

서비스를 사용하려면 먼저 끝점을 구성하고 활성화해야 합니다. 끝점은 서비스를 호출할 방법을 지정합니다.

>[!NOTE]
>
>Workbench에서 끝점은 시작점이라고 합니다.

다음 유형의 끝점을 서비스에 추가할 수 있습니다. 일부 서비스에서는 모든 끝점을 지원하지 않습니다.

**이메일:** 사용자가 하나 이상의 첨부 파일이 있는 이메일 메시지를 지정된 이메일 계정으로 전송하여 서비스를 호출할 수 있습니다. 이메일 끝점을 구성하려면 먼저 필요한 이메일 계정을 구성해야 합니다. 자세한 내용은 전자 메일 끝점 구성을 참조하십시오.

**감시 폴더:** 정의된 간격으로 스캔되는 폴더에 파일을 가져와 서비스를 호출할 수 있습니다. (감시 폴더 끝점 구성을 참조하십시오.)

**TaskManager:** Workspace 사용자가 서비스를 호출할 수 있도록 합니다.

**Remoting:** Flex으로 작성한 응용 프로그램이 AEM Forms Remoting을 사용하여 서비스를 호출할 수 있도록 합니다(AEM 양식에서 더 이상 사용되지 않음). 활성화된 각 서비스에 대해 원격 끝점이 자동으로 만들어집니다. 끝점과 동일한 이름을 갖는 Flex 대상을 만들고 Flex 클라이언트는 이 대상을 가리키는 원격 개체를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

**SOAP:** AEM 양식 프로그래밍 API를 사용하여 개발된 클라이언트 응용 프로그램에서 SOAP 모드를 사용하여 서비스를 호출할 수 있습니다. 활성화된 각 서비스에 대해 SOAP 끝점이 자동으로 만들어집니다.

**참고**: *Adobe Acrobat 또는 Adobe Reader에서 문서를 보는 동안 SOAP 끝점을 사용하면 문서 보안 문서에서 보안을 제거할 수 있습니다. LCRM 문서에서 SOAP 끝점을 비활성화하는 방법에 대한 자세한 내용은 문서 보안 문서에 대한 SOAP 끝점 비활성화[를 참조하십시오.](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** AEM 양식 프로그래밍 API를 사용하여 개발한 클라이언트 응용 프로그램이 EJB(Enterprise JavaBeans) 모드를 사용하여 서비스를 호출할 수 있도록 합니다. 활성화된 각 서비스에 대해 EJB 끝점이 자동으로 생성됩니다.

**WSDL:** AEM 양식 프로그래밍 API를 사용하여 개발한 클라이언트 응용 프로그램이 WSDL(웹 서비스 정의 언어)을 사용하여 서비스를 호출할 수 있도록 합니다. 핵심 구성 페이지에는 AEM 양식에 포함된 모든 서비스에 대해 WSDL 생성을 활성화하는 옵션이 포함되어 있습니다. 자세한 내용은 일반 AEM 양식 설정 구성을 참조하십시오.

**REST:** Workbench에서 만든 프로세스를 구성하여 REST(Representational State Transfer) 요청을 통해 호출할 수 있습니다. REST 요청은 HTML 페이지에서 전송됩니다. 즉, REST 요청을 사용하여 웹 페이지에서 직접 AEM 양식 프로세스를 호출할 수 있습니다.

Email, TaskManager, Observed Folder 및 Remoting 끝점은 서비스의 특정 작업만 노출합니다. 이러한 끝점을 추가하려면 서비스를 호출할 메서드를 선택하고 구성 매개 변수를 설정하고 입력 및 출력 매개 변수 매핑을 지정하는 데 두 번째 구성 단계가 필요합니다.
