---
title: JEE의 AEM Forms 프로세스에 데이터를 제출하도록 AEM Forms 구성
description: 양식 데이터 처리를 위해 JEE 프로세스의 AEM Forms과 적응형 양식을 통합합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin, User, Developer
exl-id: 025a3314-8b9d-48e1-a74f-ea0c933e21e3
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# JEE 프로세스에서 AEM 양식에 양식 데이터를 제출하도록 AEM Forms 구성{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

적응형 양식은 추가 처리를 위해 JEE의 AEM Forms 프로세스에 데이터 제출을 지원합니다. 제출된 양식에서 사용할 수 있는 데이터로 JEE의 AEM Forms 프로세스를 트리거할 수 있습니다. AEM Forms 인스턴스를 활성화하여 적응형 양식을 JEE의 AEM Forms 프로세스에 제출할 수 있도록 다음 단계를 수행하십시오.

## AEM Forms 서버 구성 {#configure-your-aem-forms-server}

AEM Forms 서버가 JEE 서버의 AEM Forms에 데이터를 제출할 수 있도록 다음 단계를 수행하십시오.

1. https://에서 AEM 웹 구성 콘솔로 이동합니다.[*호스트*]:[*포트*]/system/console/configMgr.

1. 을(를) 찾아 클릭합니다 **Adobe LiveCycle 클라이언트 SDK 구성** 구성 요소.
1. 를 클릭하여 JEE 서버의 AEM Forms에 대한 구성 서버 URL, 사용자 이름 및 암호를 편집합니다.
1. 설정을 검토하고 다음을 클릭합니다. **저장**.

![Adobe LiveCycle 클라이언트 SDK 구성](assets/clientsdkconfiguration.jpg)

## 프로세스 필드를 사용하여 데이터 매핑 {#map-data-with-process-fields}

AEM Forms을 구성한 후 제출된 양식의 데이터 XML 및 첨부 파일을 JEE의 AEM Forms 프로세스에 있는 필드에 매핑합니다. 다음 작업을 수행합니다.

1. AEM 웹 구성 콘솔에서 을 클릭하여 **안내 LiveCycle 프로세스 보관처 및 호출기** 구성.
1. 다음 매개 변수를 지정합니다.

   * **데이터 xml 매개 변수의 이름** (필수): 제출된 데이터를 처리해야 하는 AEM Forms on JEE 프로세스의 XML 속성 파일을 지정합니다. 기본값은 입니다. **dataxml**.

   * **첨부 파일 매개 변수 이름** (선택 사항): JEE의 AEM Forms 프로세스에서 처리해야 하는 문서 객체 목록을 지정합니다. 기본값은 입니다. **첨부 파일 목록**.

1. 설정을 검토하고 다음을 클릭합니다. **저장**.

![안내 LiveCycle 프로세스 보관처 및 호출기](assets/test3.jpg)

구성된 경우 Forms Workflow에 제출 액션은 지정된 데이터 xml 매개 변수를 포함하는 JEE의 AEM Forms 서버 프로세스를 나열합니다.
