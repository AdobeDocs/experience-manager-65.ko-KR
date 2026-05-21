---
title: AEM 6.5의 AI Assistant
description: AI 어시스턴트를 사용하면 Adobe Experience Manager에서 제공되는 솔루션에 대한 답변을 찾고 문제를 해결하는 데 도움이 됩니다.
solution: Experience Manager, Experience Manager 6.5
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
autotag-review: '2026-05-18T18:36:07.915Z'
TQID: 'https://experienceleague.adobe.com/dlFmrtn05S20z96wtAfkpGliITeVJhVkofqPix6QMxk'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1379
ht-degree: 93%

---

# AEM 6.5의 AI Assistant {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>Cloud Manager/Experience Hub를 사용하지 않는 AEM 6.5 및 AEM 6.5 LTS 고객은 Adobe 고객 성공 엔지니어에게 문의하여 AI 어시스턴트 액세스 권한을 요청해야 합니다.

AEM 6.5/AEM 6.5 LTS의 AI Assistant는 Adobe Experience Manager 관련 쿼리에 대한 답변 찾기를 간소화하도록 설계된 대화형 인터페이스를 제공합니다. AEM 제품 관련 질문에 대한 즉각적인 답변(*모든 사용자 사용 가능*)을 얻고 지원 티켓 생성을 자동화하는 데 도움이 됩니다(*지원 관리자 사용 가능*).

AI 어시스턴트는 다음 솔루션을 포함하여 AEM as a Cloud Service를 지원합니다.

* Experience Hub 개요 페이지
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


AEM에 직접 내장되어 있으며 AEM Experience Hub, Cloud Manager 및 Author UI에서 액세스할 수 있습니다.

다음 3분 25초 분량의 비디오는 AEM 내 AI 어시스턴트의 단계별 워크스루를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3475357/?learn=on&enablevpops)

## AEM 내 AI 어시스턴트 액세스{#get-access}

AEM 내 AI 어시스턴트에 액세스하려면 고객이 다음과 같은 정보를 보유하고 있어야 합니다.

* 제품 지식을 위한 AEM 내 AI 어시스턴트 사용 권한. 이 권한을 통해 AI 어시스턴트 채팅에서 제품 관련 질문을 할 수 있습니다. 이 권한을 활성화해야 합니다.
* **지원 관리자** 역할이 필요한 지원 티켓을 열 수 있는 권한.

>[!NOTE]
>
>AEM 내 AI 어시스턴트 요청은 Adobe IMS(Identity Management Services)를 통해 인증됩니다. 자세한 내용은 [Adobe Identity Management Services 개요](https://www.adobe.com/kr/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf)를 참조하십시오.

**AEM 내 AI 어시스턴트를 액세스하려면:**

1. 고객은 Adobe Experience Manager에서 다수의 AI 기반 및 에이전틱 기능에 액세스하려면 추가 계약을 체결해야 합니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

1. AEM 내 AI 어시스턴트를 사용하려면 AI 어시스턴트를 통해 제품 지식에 액세스할 수 있는 권한이 필요합니다. 이 권한은 기본적으로 켜져 있습니다.

   제품 정보에 액세스할 수 있는 사용자를 제어하려면 Adobe ID과 연결된 이메일 주소에서 [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com)으로 이메일을 보내십시오. Adobe가 사용자 수준 액세스 제어를 활성화할 수 있습니다. 활성화되면 관리자는 [AEM 내 AI 어시스턴트 구성](/help/ai-assistant-in-aem-admin.md)의 단계에 따라 사용자 수준 액세스 권한을 부여할 수 있습니다.


## 범위 {#scope}

AEM의 현재 AI Assistant 범위는 AEMr as a Cloud Service에 대한 제품 지식 질문 처리에 중점을 둡니다. 이 범위에는 주요 영역에 대한 포괄적인 지원이 포함됩니다. <!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **표면**: AEM Experience Hub, 작성자 UI, Cloud Manager에서 사용할 수 있습니다.
* **기능**: 문제 해결 및 지침, 지원 티켓 자동 생성 및 조회를 위한 제품 지식 및 첫 번째 중지.
* **값**: 시간을 절약하고 학습 속도와 가치 창출 시간을 단축하며, 지원 티켓을 수동으로 생성할 필요성을 줄이고, 지원 티켓 생성의 효율성을 향상시킵니다.

## 개인 정보, 보안 및 거버넌스{#privacy-security-governance}

AEM 내 AI 어시스턴트는 개인 정보, 보안, 거버넌스에 중점을 두고 설계되었습니다.

이 문서에서는 AEM 내 AI 어시스턴트에게 기대할 수 있는 신뢰 중심 기능에 대해 설명합니다.

* AEM 내 AI 어시스턴트는 교육 목적을 포함하여 개인 데이터를 사용하지 않습니다.
* AEM 내 AI 어시스턴트는 소비자 데이터에 액세스할 수 없습니다.
* AEM 내 AI 어시스턴트와 상호작용하려면 명시적인 권한이 필요합니다.
* 사용자가 제공한 프롬프트(질문, 쿼리 등)는 다른 고객과 공유되지 않습니다.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## 제품 지식과 자동화된 지원 티켓 생성을 위해 AEM 내 AI 어시스턴트에 대해 알아봅니다 {#ai-prod-insights}

제품 지식은 Adobe Experience League 설명서에서 파생된 개념과 주제를 포함합니다. 이 질문들은 다음과 같은 하위 그룹으로 분류될 수 있습니다.


| 제품 지식 | 모든 사용자 사용 가능<br>예 |
| :--- | :--- |
| 구체적인 학습 | <ul><li>범용 편집기란 무엇입니까?</li><li>Cloud Manager에서 프로그램을 만들려면 어떻게 해야 합니까?</li></ul> |
| 공개 검색 | <ul><li>범용 편집기는 어떻게 사용합니까?</li><li>한 환경에서 다른 환경으로 콘텐츠를 복사하는 방법이 있습니까?</li></ul> |
| 문제 해결 | <ul><li>범용 편집기에 액세스할 수 없는 이유는 무엇입니까?</li><li>내 파이프라인이 실패한 이유는 무엇입니까?</li></ul> |
| **티켓 만들기 지원** | **지원 관리자만 사용 가능&#x200B;**<br>**예** |
| AI 어시스턴트 채팅 기록 및 컨텍스트를 캡처하는 자동화된 지원 티켓 생성 | <ul><li>나를 위한 지원 티켓을 만드세요.</li></ul> |
| 지원 티켓 상태 가져오기 | <ul><li>내가 열어본 모든 지원 티켓을 보여 주세요.</li><li>티켓 “E-----------”의 상태를 보여 주세요</li></ul> |

{style="table-layout:auto"}


## 효과적인 질문을 작성하는 방법 {#ai-craft-questions}

AEM 내 AI 어시스턴트로부터 가장 정확한 답변을 받으려면 질문을 명확하고 맥락에 맞게 표현하는 것이 중요합니다. 다음 팁을 사용하여 쿼리가 명확하고 잘 구성되었는지 확인합니다.

* 과제나 질문을 간결하게 명확하게 표현합니다.
* 이해를 높이기 위해 모호한 표현이나 지나치게 복잡한 구문을 피합니다.
* 이 접근 방식은 AEM 내 AI 어시스턴트가 보다 정확하고 관련성 있는 답변을 제공하는 데 도움이 되므로 작업이나 질문에 대한 관련 컨텍스트를 포함합니다.
예를 들어 프롬프트에서 작업 중인 AEM 솔루션의 이름을 Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager 또는 Forms로 지정하는 데 도움이 됩니다.

### 지원되지 않는 질문의 예 {#ai-unsupported-questions}

| 영역 | 예 |
| --- | --- |
| 운영 인사이트 | <ul><li>내 테넌트에 개발 환경이 몇 개 있습니까?</li><li>마지막 프로덕션 파이프라인은 누가 시작했습니까?</li></ul> |
| 문제 해결 | <ul><li>프로덕션 파이프라인이 실패한 이유는 무엇입니까?</li></ul> |
| 작업 및 자동화 | <ul><li>나를 위해 개발 분기에서 코드 품질 파이프라인을 구성합니다.</li></ul> |


## AEM 내 AI 어시스턴트 사용 {#ai-use}

<!--
UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/ko/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md).
-->


### AEM 내 AI 어시스턴트 대화 시작

주제를 변경하려는 경우 AEM 내 AI 어시스턴트를 재설정하고 새 대화를 시작할 수 있습니다. 이 기능은 실패하거나 잘못된 정보를 제공하는 쿼리를 문제 해결할 때 특히 유용합니다.

**AEM 내 AI 어시스턴트 대화를 시작하려면:**

1. (Cloud Manager 페이지 또는 AEM 환경의 작성자 인스턴스의) AEM 사용자 인터페이스 오른쪽 상단 근처에서 **AI 어시스턴트** 아이콘을 클릭합니다.

   ![도구 모음의 AI 어시스턴트 아이콘](/help/assets/assets-ai/ai-assistant-icon.png)

1. 하단 근처에 있는 **AI 어시스턴트** 패널 텍스트 상자에 질문이나 프롬프트를 입력한 다음 `Enter`를 누르거나 ![보내기 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)을 클릭합니다.

   >[!NOTE]
   >
   >개인 데이터는 이 도구를 사용하는 데 불필요하므로 입력에 포함해서는 안 됩니다.

   ![AI 어시스턴트 패널 아래쪽에 있는 텍스트 상자](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. 새 대화(새 주제 또는 주제의 변경)를 시작하려면 ![자세히 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **새 대화 시작**&#x200B;을 클릭합니다.

   ![줄임표 아이콘을 사용하여 AI 어시스턴트에서 새 대화 시작](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### 카테고리별 프롬프트 검색

AEM 내 AI 어시스턴트에는 지원되는 주제와 카테고리를 탐색하는 데 도움이 되는 검색 기능이 포함되어 있습니다.

**카테고리별 프롬프트를 검색하려면:**

1. AI 어시스턴트 패널에서 ![학습 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)을 클릭하여 프롬프트 검색 패널을 켭니다.

   ![AI 어시스턴트에서 카테고리별 프롬프트를 탐색할 수 있는 패널](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *AI 어시스턴트에서 프롬프트 카테고리를 표시하는 패널.*

1. 관련 프롬프트 목록을 보려면 카테고리를 선택합니다.
1. AI 어시스턴트 답할 수 있는 질문 유형의 예를 보려면 프롬프트를 선택합니다.

1. 프롬프트 검색 패널을 숨기려면 ![학습 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)을 다시 클릭합니다.

### AEM 내 AI 어시스턴트에 대한 피드백 공유

사용자의 입력을 통해 Adobe는 AI 어시스턴트를 개선하여 성능과 정확성을 높일 수 있습니다.

다음 옵션을 통해 AEM 내 AI 어시스턴트와 사용자 경험에 대한 피드백을 공유할 수 있습니다.

![좋아요, 싫어요, 그리고 플래그 아이콘](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| 클릭 | 설명 |
| --- | --- |
| ![좋아요 아웃라인 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 무엇이 잘 진행되었는지 표시하고 긍정적인 피드백을 공유합니다. |
| ![싫어요 아웃라인 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 개선을 위한 제안을 입력합니다. 매일 검토되는 경험에 대한 구체적인 댓글을 추가합니다. |
| ![플래그 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | AEM 내 AI 어시스턴트와의 상호작용에 대한 문제를 보고하거나 자세한 피드백을 제공합니다. |

## AEM 내 AI 어시스턴트에 대해 자주 묻는 질문 {#ai-faq}

다음은 AI 어시스턴트에 대한 몇 가지 일반적인 질문에 대한 답변입니다.

* **AEM 내 AI 어시스턴트가 제공하는 정보는 실시간으로 제공됩니까?**\
  아니요. AI 어시스턴트는 Adobe Experience League 설명서에서 해당 콘텐츠를 제공합니다. 콘텐츠 업데이트가 응답에 반영하는 데 시간이 걸릴 수 있습니다.
* **AEM 내 AI 어시스턴트가 지원하는 Adobe 애플리케이션은 무엇입니까?**\
  현재 AI 비서는 사이트, Assets, 다이내믹 미디어, Cloud Manager, Forms 등 AEM as a Cloud Service에서 제품 지식 조회를 지원한다.
* **AEM 내 AI 어시스턴트의 기능은 무엇입니까?**\
  AEM의 AI Assistant는 Adobe 제품 지식과 관련된 질문에 답변할 수 있도록 설계되었습니다.
* **AEM 내 AI 어시스턴트가 교육 데이터에 개인 정보를 사용합니까?**\
  아니요. AEM 내 AI 어시스턴트는 교육 목적으로 개인 정보를 사용하지 않습니다. 이름이나 연락처 세부 정보를 포함하여 자신 또는 다른 사람에 대한 개인 정보를 AEM 내 AI 어시스턴트와 공유하지 마십시오.

<!--
IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

In addition to the general AI Assistant in AEM for product knowledge, AEM offers a specialized **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. This enhanced assistant can actively help you create and configure forms through natural language prompts and answer questions specific to forms.

### Key capabilities

The AEM Forms AI Assistant provides:

* **Form Creation**: Create new forms from scratch using natural language descriptions.
* **Design Import**: Convert existing designs (PDF, Figma, images) into functional AEM Forms. 
* **Form Configuration**: Add fields, panels, validation rules, and conditional logic.
* **Layout Management**: Organize form structure and optimize for different devices.
* **Integration Setup**: Configure form submissions and data handling.
* **Product Knowledge**: Answer questions about AEM Forms features and best practices.

### Where to access

The AEM Forms AI Assistant is available in the following:

* **Universal Editor**: For Edge Delivery Services forms with visual editing capabilities.
* **Adaptive Forms Editor**: For detailed form configuration and advanced features.
* **Forms Management UI**: For high-level form creation and management tasks.

### Getting started

>[!NOTE]
>
> The AEM Forms AI Assistant (Forms Experience Builder) is available under the private beta program. Send an email from your work address to [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) to request access.

To learn more about using the AEM Forms AI Assistant , see the [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md) documentation.

### Example Use Cases

* **"Create a customer feedback form with name, email, rating, and comments fields"**
* **"Convert this uploaded PDF application form into a digital adaptive form"**  
* **"Add conditional logic to show spouse information only when marital status is 'Married'"**
* **"Configure this form to submit data to the Customer Relationship Management system"**

This specialized AEM Forms AI Assistant represents the next evolution in form building, combining the power of AI with AEM's robust forms capabilities to streamline your form creation workflow.
-->
