---
title: 엔드포인트 유형
description: 다양한 유형의 엔드포인트를 알아봅니다. 이메일, 감시 폴더 등 다양한 유형의 엔드포인트를 서비스에 추가할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '455'
ht-degree: 100%

---

# 엔드포인트 유형 {#types-of-endpoints}

서비스를 사용하려면 먼저 엔드포인트를 구성하고 활성화해야 합니다. 엔드포인트는 서비스를 호출하는 방법을 지정합니다.

>[!NOTE]
>
>워크벤치에서는 엔드포인트를 시작점이라고 합니다.

다음 유형의 엔드포인트를 서비스에 추가할 수 있습니다. 모든 서비스가 모든 엔드포인트를 지원하는 것은 아닙니다.

**이메일:** 사용자가 하나 이상의 첨부 파일이 포함된 이메일 메시지를 지정된 이메일 계정으로 보내 서비스를 호출할 수 있습니다. 이메일 엔드포인트를 구성하기 전에 필수 이메일 계정을 구성해야 합니다. (이메일 엔드포인트 구성을 참조하십시오.)

**감시 폴더:** 사용자가 폴더에 파일을 넣어 정의된 간격으로 스캔하는 서비스를 호출할 수 있습니다. (감시 폴더 엔드포인트 구성을 참조하십시오.)

**TaskManager:** Workspace 사용자가 서비스를 호출할 수 있습니다.

**Remoting:** Flex로 빌드된 애플리케이션에서 AEM Forms Remoting(AEM Forms에서는 더 이상 사용되지 않음)을 사용하여 서비스를 호출할 수 있습니다. 활성화된 각 서비스에 대해 Remoting 엔드포인트가 자동으로 생성됩니다. 엔드포인트와 이름이 동일한 Flex 대상이 생성되고 Flex 클라이언트는 이 대상을 가리키는 원격 오브젝트를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

**SOAP:** AEM Forms 프로그래밍 API를 사용하여 개발된 클라이언트 애플리케이션에서 SOAP 모드를 사용하여 서비스를 호출할 수 있습니다. 활성화된 각 서비스에 대해 SOAP 엔드포인트가 자동으로 생성됩니다.

**참고**: *Adobe Acrobat 또는 Adobe Reader에서 문서를 보는 동안 SOAP 엔드포인트를 사용하면 문서 보안 문서에서 보안이 제거될 수 있습니다. LCRM 문서에서 SOAP 엔드포인트를 비활성화하는 방법에 대한 자세한 내용은 [문서 보안 문서에 대한 SOAP 엔드포인트 비활성화](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*&#x200B;를 참조하십시오.

**EJB:** AEM Forms 프로그래밍 API를 사용하여 개발된 클라이언트 애플리케이션에서 EJB(Enterprise JavaBeans) 모드를 사용하여 서비스를 호출할 수 있습니다. 활성화된 각 서비스에 대해 EJB 엔드포인트가 자동으로 생성됩니다.

**WSDL:** AEM Forms 프로그래밍 API를 사용하여 개발된 클라이언트 애플리케이션에서 WSDL(Web Service Definition Language)을 사용하여 서비스를 호출할 수 있습니다. 핵심 구성 페이지에는 AEM Forms에 포함된 모든 서비스에 대해 WSDL 생성을 활성화하는 옵션이 있습니다. (일반 AEM Forms 설정 구성을 참조하십시오.)

**REST:** REST(Representational State Transfer) 요청을 통해 워크벤치에서 생성된 프로세스를 호출할 수 있도록 구성할 수 있습니다. REST 요청은 HTML 페이지에서 전송됩니다. 즉, REST 요청을 사용하여 웹 페이지에서 직접 AEM Forms 프로세스를 호출할 수 있습니다.

이메일, TaskManager, 감시 폴더, Remoting 엔드포인트는 서비스의 특정 작업만 노출합니다. 이러한 엔드포인트를 추가하려면 서비스를 호출할 메서드를 선택하고, 구성 매개변수를 설정하고, 입력 및 출력 매개변수 매핑을 지정하는 두 번째 구성 단계가 필요합니다.
