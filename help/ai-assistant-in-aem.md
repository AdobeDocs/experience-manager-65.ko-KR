---
title: AEM 6.5의 AI Assistant
description: AI 어시스턴트를 사용하면 Adobe Experience Manager에서 제공되는 솔루션에 대한 답변을 찾고 문제를 해결하는 데 도움이 됩니다.
solution: Experience Manager, Experience Manager 6.5
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
source-git-commit: c98a66a4b4be23145334b339a793ded1716e9889
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 4%

---

# AEM 6.5의 AI Assistant {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>Cloud Manager/Experience Hub을 사용하지 않는 AEM 6.5 및 AEM 6.5 LTS 고객은 Adobe 고객 성공 엔지니어에게 연락하여 AI Assistant에 대한 액세스를 요청해야 합니다.

AEM 6.5/AEM 6.5 LTS의 AI Assistant는 Adobe Experience Manager 관련 쿼리에 대한 답변 찾기를 간소화하도록 설계된 대화형 인터페이스를 제공합니다. AEM 제품 관련 질문에 대한 즉각적인 답변을 얻고(*모든 사용자가 사용할 수 있음*) 지원 티켓 생성을 자동화할 수 있습니다(*지원 관리자가 사용할 수 있음*).

AI Assistant는 다음 솔루션을 포함하여 AEM as a Cloud Service을 지원합니다.

* Experience Hub 개요 페이지
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


AEM에 직접 내장되어 있으며 AEM Experience Hub, Cloud Manager 및 Author UI에서 액세스할 수 있습니다.

다음 3분 39초 길이의 비디오에서는 AEM의 AI Assistant에 대한 단계별 연습을 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3470362?learn=on&captions=kor)

## AEM에서 AI Assistant 액세스{#get-access}

AEM의 AI Assistant에 대한 액세스 권한을 사용자에게 부여하려면 Adobe 관리자가 **Adobe Admin Console**&#x200B;에서 액세스 권한이 필요한 프로필에 대해 다음과 같은 사용자 지정 권한을 구성해야 합니다.

* **AI Assistant 액세스** - 제품 지식을 위해 AEM의 AI Assistant를 사용할 수 있는 권한으로, 사용자가 AI Assistant 채팅에서 제품 관련 질문을 할 수 있습니다. 이 권한을 활성화해야 합니다.
* **지원 액세스** - **지원 관리자** 역할이 필요한 지원 티켓을 열 수 있는 권한도 사용자에게 있어야 합니다.

AEM의 AI Assistant 요청은 Adobe Identity Management Services(IMS)를 통해 인증됩니다. 자세한 내용은 [Adobe Identity Management 서비스 개요](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf)를 참조하십시오.

**AEM에서 AI Assistant에 액세스하려면:**

1. 고객은 Adobe Experience Manager에서 AI가 제공하는 대부분의 아젠틱 기능에 액세스하려면 추가 계약을 체결해야 합니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

<!-- OLD STEP 1 [Customers must sign the Gen AI rider with Adobe](https://fieldreadiness-adobe.highspot.com/items/665f831c9f831b011aeda057#1). 

    The GenAI Rider is a legal agreement between a customer and Adobe, required to use most AI and agentic capabilities. Contact Adobe Customer Care to learn more. -->

1. AEM 관리자는 해당 조직에서 사용할 AI Assistant를 구성합니다. [AEM에서 AI Assistant 구성](/help/ai-assistant-in-aem-admin.md)을 참조하십시오.

<!--
>[!IMPORTANT]
>Be sure you have reviewed and submitted the user agreement so Adobe can enable the AI Assistant feature for you to test out and participate in the private beta program.
>
>For any questions, send an email to [Grp-AEMAIASSISTANT@adobe.com](mailto:Grp-AEMAIASSISTANT@adobe.com) from your email address associated with your Adobe ID. -->

## 범위 {#scope}

AEM에 있는 AI Assistant의 현재 범위는 AEMr as a Cloud Service에 대한 제품 지식 질문 해결에 중점을 둡니다. 이 범위에는 주요 영역에 대한 포괄적인 지원이 포함됩니다. <!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **표면**: AEM Experience Hub, 작성자 UI, Cloud Manager에서 사용할 수 있습니다.
* **기능**: 문제 해결 및 지침, 지원 티켓 자동 생성 및 조회를 위한 제품 지식 및 첫 번째 중지.
* **값**: 시간을 절약하고, 학습 및 가치 창출 시간을 가속화하며, 지원 티켓을 수동으로 만들어야 하는 필요성을 줄이고, 지원 티켓을 만드는 효율성을 향상시킵니다.

## 개인 정보, 보안 및 거버넌스{#privacy-security-governance}

AEM의 AI Assistant는 개인 정보 보호, 보안 및 거버넌스에 중점을 두고 설계되었습니다.

이 문서에서는 AEM의 AI Assistant에서 기대할 수 있는 신뢰 중심 기능에 대해 간략히 설명합니다.

* AEM의 AI Assistant는 교육 목적을 포함하여 개인 데이터를 사용하지 않습니다.
* AEM의 AI 도우미는 소비자 데이터에 액세스할 수 없습니다.
* AEM에서 AI Assistant와 상호 작용하려면 명시적 권한이 필요합니다.
* 사용자가 제공한 프롬프트(질문, 쿼리 등)는 다른 고객과 공유되지 않습니다.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## 제품 지식 및 자동화된 지원 티켓 생성을 위해 AEM의 AI Assistant에 대해 알아봅니다 {#ai-prod-insights}

제품 지식은 Adobe Experience League 설명서에서 파생된 개념과 주제를 포함합니다. 이러한 질문은 다음과 같은 하위 그룹으로 분류될 수 있습니다.


| 제품 지식 | 모든 사용자가 사용할 수 있음<br>예 |
| :--- | :--- |
| 뾰족한 학습 | <ul><li>유니버설 편집기란?</li><li>Cloud Manager에서 프로그램을 만들려면 어떻게 해야 합니까?</li></ul> |
| 검색 열기 | <ul><li>범용 편집기는 어떻게 사용합니까?</li><li>한 환경에서 다른 환경으로 콘텐츠를 복사하는 방법이 있습니까?</li></ul> |
| 문제 해결 | <ul><li>유니버설 편집기에 액세스할 수 없는 이유는 무엇입니까?</li><li>내 파이프라인이 실패한 이유는 무엇입니까?</li></ul> |
| **티켓 만들기 지원** | **지원 관리자만 사용 가능&#x200B;**<br>**예** |
| AI Assistant 채팅 내역 및 컨텍스트를 캡처하는 자동화된 지원 티켓 작성 | <ul><li>지원 티켓을 만드십시오.</li></ul> |
| 지원 티켓 상태 가져오기 | <ul><li>제가 열어 본 응원 티켓을 모두 보여주세요.</li><li>티켓 &quot;E-----------&quot; 상태 표시</li></ul> |

{style="table-layout:auto"}


## 효과적인 질문을 작성하는 방법 {#ai-craft-questions}

AEM의 AI Assistant로부터 가장 정확한 응답을 받으려면 명확성과 문맥으로 질문을 구문 분석하는 것이 중요합니다. 다음 팁을 사용하여 쿼리가 명확하고 잘 구성되어 있는지 확인하십시오.

* 과제나 질문을 간결하게 명확히 진술하라.
* 애매한 문구나 지나치게 복잡한 구문을 방지하여 이해도를 높입니다.
* 이 접근 방식은 AEM의 AI Assistant가 보다 정확하고 적절한 답변을 제공하는 데 도움이 되므로 작업 또는 질문에 대한 관련 컨텍스트를 포함합니다.
예를 들어 프롬프트에서 작업 중인 AEM 솔루션의 이름을 Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager 또는 Forms으로 지정하는 데 도움이 됩니다.

### 지원되지 않는 질문의 예 {#ai-unsupported-questions}

| 영역 | 예 |
| --- | --- |
| Operational insights | <ul><li>내 테넌트에 개발 환경이 몇 개 있습니까?</li><li>마지막 프로덕션 파이프라인은 누가 시작했습니까?</li></ul> |
| 문제 해결 | <ul><li>프로덕션 파이프라인이 실패한 이유는 무엇입니까?</li></ul> |
| 작업 및 자동화 | <ul><li>나를 위해 개발 분기에서 코드 품질 파이프라인을 구성합니다.</li></ul> |


## AEM에서 AI Assistant 사용 {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use the AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in the AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/ko/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### AEM 대화에서 AI 도우미 시작

주제를 변경하려는 경우 AEM에서 AI 도우미를 재설정하고 새 대화를 시작할 수 있습니다. 이 기능은 특히 실패한 쿼리의 문제를 해결하거나 잘못된 정보를 제공할 때 유용합니다.

**AEM 대화에서 AI 도우미를 시작하려면:**

1. AEM 사용자 인터페이스(Cloud Manager 페이지 또는 AEM 환경의 작성자 인스턴스)의 오른쪽 상단 모서리 근처에서 **AI Assistant** 아이콘을 클릭합니다.

   도구 모음의 ![AI 길잡이 아이콘](/help/assets/assets-ai/ai-assistant-icon.png)

1. 아래쪽 근처에 있는 **AI Assistant** 패널 텍스트 상자에 질문이나 프롬프트를 입력한 다음 `Enter`을 누르거나 ![보내기 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg)을 클릭합니다.

   >[!NOTE]
   >
   >개인 데이터는 이 도구를 사용하는 데 필요하지 않으므로 입력에 포함되지 않아야 합니다.

   ![AI Assistant 패널 아래쪽에 있는 텍스트 상자](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. 새 대화(새 주제 또는 주제의 변경)를 시작하려면 ![추가 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **새 대화 시작**&#x200B;을 클릭하세요.

   ![줄임표 아이콘을 사용하여 AI Assistant에서 새 대화를 시작하십시오](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### 카테고리별 프롬프트 검색

AEM의 AI 도우미에는 지원되는 주제와 범주를 탐색하는 데 도움이 되는 검색 기능이 포함되어 있습니다.

**카테고리별로 프롬프트를 검색하려면:**

1. AI Assistant 패널에서 ![학습 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)을 클릭하여 프롬프트 검색 패널을 켭니다.

   AI Assistant에서 카테고리별 프롬프트를 탐색할 수 있는 ![패널](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *AI Assistant에서 프롬프트 범주를 표시하는 패널.*

1. 관련 프롬프트 목록을 보려면 카테고리를 선택하십시오.
1. AI Assistant가 답할 수 있는 질문 유형의 예를 보려면 프롬프트를 선택합니다.

1. 프롬프트 검색 패널을 숨기려면 ![학습 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg)을 다시 클릭합니다.

### AEM의 AI Assistant에 대한 피드백 공유

사용자의 입력을 통해 Adobe은 AI Assistant를 개선하여 성능과 정확성을 높일 수 있습니다.

다음 옵션을 통해 AEM의 AI Assistant와 사용자 경험에 대한 피드백을 공유할 수 있습니다.

![엄지손가락 위로, 엄지손가락 아래로 및 플래그 아이콘](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| 클릭 | 설명 |
| --- | --- |
| ![Thumbs 위쪽 아웃라인 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | 무엇이 잘 진행되었는지 나타내고 긍정적인 피드백을 공유하십시오. |
| ![Thumbs down outine 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | 개선을 위한 제안을 제공합니다. 매일 검토되는 경험에 대한 특정 주석을 추가합니다. |
| ![플래그 아이콘](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | AEM의 AI Assistant와의 상호 작용에 대한 우려를 보고하거나 자세한 피드백을 제공합니다. |

## AEM의 AI Assistant에 대해 자주 묻는 질문 {#ai-faq}

다음은 AI Assistant에 대한 몇 가지 일반적인 질문에 대한 답변입니다.

* **AEM의 AI 도우미가 제공하는 정보가 실시간으로 제공됩니까?**\
  아니요. AI Assistant는 Adobe Experience League 설명서에서 해당 콘텐츠를 소스화합니다. 콘텐츠에 대한 업데이트가 응답에 반영되는 데 시간이 걸릴 수 있습니다.
* **AEM의 AI 도우미가 지원하는 Adobe 애플리케이션은 무엇입니까?**\
  현재 AI 비서는 사이트, Assets, 다이내믹 미디어, Cloud Manager, Forms 등 AEM as a Cloud Service에서 제품 지식 조회를 지원한다.
* **AEM에서 AI Assistant의 기능은 무엇입니까?**\
  AEM의 AI Assistant는 Adobe 제품 지식과 관련된 질문에 답변할 수 있도록 설계되었습니다.
* **AEM의 AI 도우미가 교육 데이터에 개인 정보를 사용합니까?**\
  아니요. AEM의 AI Assistant는 교육 목적으로 개인 정보를 사용하지 않습니다. 이름이나 연락처 세부 정보를 포함하여 자신 또는 다른 사람에 대한 개인 정보를 AEM의 AI 어시스턴트와 공유하지 마십시오.

<!-- IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

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
