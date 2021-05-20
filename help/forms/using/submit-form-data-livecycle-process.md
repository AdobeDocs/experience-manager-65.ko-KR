---
title: JEE 프로세스에서 AEM Forms에 양식 데이터를 제출하도록 AEM Forms 구성
seo-title: JEE 프로세스에서 AEM Forms에 양식 데이터를 제출하도록 AEM Forms 구성
description: AEM Forms을 사용하면 적응형 양식을 JEE 프로세스의 AEM Forms과 통합하여 양식 데이터를 처리할 수 있습니다.
seo-description: AEM Forms을 사용하면 적응형 양식을 JEE 프로세스의 AEM Forms과 통합하여 양식 데이터를 처리할 수 있습니다.
uuid: 71a894d7-7c0a-43a6-afe5-40c4a15c66d6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: ff97424d-b384-4149-9a3c-b4f00aaa1def
docset: aem65
role: Administrator
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# JEE 프로세스{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}에서 AEM Forms에 양식 데이터를 제출하도록 AEM Forms 구성

적응형 양식은 추가적인 처리를 위해 JEE 프로세스에서 AEM Forms에 데이터 제출을 지원합니다. 이를 통해 제출된 양식에서 사용할 수 있는 데이터로 JEE 프로세스에서 AEM Forms을 트리거할 수 있습니다. AEM Forms 인스턴스가 JEE 프로세스에서 AEM Forms에 적응형 양식을 제출할 수 있도록 하려면 다음 단계를 수행하십시오.

## AEM Forms 서버 구성 {#configure-your-aem-forms-server}

AEM Forms 서버가 JEE 서버의 AEM Forms에 데이터를 제출하도록 하려면 다음 단계를 수행하십시오.

1. https://[*host*]:[*port*]/system/console/configMgr의 AEM 웹 구성 콘솔로 이동합니다.

1. **Adobe LiveCycle 클라이언트 SDK 구성** 구성 요소를 찾아 클릭합니다.
1. JEE 서버의 AEM Forms 구성 서버 URL, 사용자 이름 및 암호를 편집하려면 을(를) 클릭합니다.
1. 설정을 검토하고 **저장**&#x200B;을 클릭합니다.

![Adobe LiveCycle 클라이언트 SDK 구성](assets/clientsdkconfiguration.jpg)

## 프로세스 필드 {#map-data-with-process-fields}에 데이터 매핑

AEM Forms이 구성되면 제출된 양식의 데이터 XML 및 첨부 파일을 JEE 프로세스의 AEM Forms 필드에 매핑합니다. 이를 위해 진행되는 작업:

1. AEM 웹 구성 콘솔에서 **가이드 LiveCycle 프로세스 로케이터 및 Invoker** 구성을 편집하려면 클릭합니다.
1. 다음 매개 변수를 지정합니다.

   * **데이터 xml 매개 변수의 이름** (필수):제출된 데이터를 처리해야 하는 JEE 프로세스에서 AEM Forms의 XML 속성 파일을 지정합니다. 기본값은 **dataxml**&#x200B;입니다.

   * **첨부 파일 매개 변수의 이름** (선택 사항):JEE의 AEM Forms 프로세스에서 처리해야 하는 문서 객체 목록을 지정합니다. 기본값은 **fileAttachmentsList**&#x200B;입니다.

1. 설정을 검토하고 **저장**&#x200B;을 클릭합니다.

![가이드 LiveCycle 프로세스 로케이터 및 인포커](assets/test3.jpg)

구성된 경우, Submit to Forms Workflow 제출 작업은 지정된 데이터 xml 매개 변수를 포함하는 JEE 서버 프로세스의 AEM Forms을 나열합니다.
