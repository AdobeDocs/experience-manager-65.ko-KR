---
title: Salesforce와 통합
seo-title: Integrating with Salesforce
description: AEM과 Salesforce 통합에 대해 알아봅니다.
seo-description: Learn about integrating AEM with Salesforce.
uuid: 3d6a249d-082f-4a10-b255-96482ccd2c65
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bee7144e-4276-4e81-a3a0-5b7273af34fe
docset: aem65
exl-id: 0f3aaa0a-ccfb-4162-97a6-ee5485595d28
source-git-commit: 6f509ad2ae488d8baec790b7719305a5af49887c
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 3%

---


# Salesforce와 통합 {#integrating-with-salesforce}

Salesforce와 AEM을 통합하면 리드 관리 기능이 제공되며 Salesforce에서 제공하는 기존 기능을 활용합니다. Salesforce로 리드를 게시하고 Salesforce에서 직접 데이터에 액세스하는 구성 요소를 만들도록 AEM을 구성할 수 있습니다.

AEM과 Salesforce 간의 양방향 및 확장 가능한 통합을 통해 다음을 수행할 수 있습니다.

* 조직은 데이터를 완벽하게 사용하고 업데이트하여 고객 경험을 향상시킬 수 있습니다.
* 마케팅에서 판매 활동에 대한 참여
* Salesforce 데이터 저장소에서 데이터를 자동으로 전송 및 받을 조직입니다.

이 문서에서는 다음 사항에 대해 설명합니다.

* Salesforce Cloud Services 구성 방법(Salesforce와 통합하도록 AEM 구성)
* Client Context 및 개인화에 Salesforce 리드/연락처 정보를 사용하는 방법
* Salesforce 워크플로우 모델을 사용하여 AEM 사용자를 salesforce에 리드로 게시하는 방법
* Salesforce의 데이터를 표시하는 구성 요소를 만드는 방법

## Salesforce와 통합하도록 AEM 구성 {#configuring-aem-to-integrate-with-salesforce}

Salesforce와 통합하도록 AEM을 구성하려면 먼저 Salesforce에서 원격 액세스 애플리케이션을 구성해야 합니다. 그런 다음 이 원격 액세스 응용 프로그램을 가리키도록 salesforce 클라우드 서비스를 구성합니다.

>[!NOTE]
>
>Salesforce에서 무료 개발자 계정을 만들 수 있습니다.

Salesforce와 통합하도록 AEM을 구성하려면:

>[!CAUTION]
>
>을(를) 설치해야 합니다 [Salesforce Force API](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/com.adobe.cq.mcm.salesforce.content) 통합 패키지 를 사용하여 절차를 계속 진행할 수 있습니다. 패키지 작업 방법에 대한 자세한 내용은 [패키지 작업 방법](/help/sites-administering/package-manager.md#package-share) 페이지.

1. AEM에서 **Cloud Services**. 타사 서비스에서 **지금 구성** in **Salesforce**.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 예를 들어 새 구성을 만듭니다. **개발자**.

   >[!NOTE]
   >
   >새 구성은 새 페이지로 리디렉션됩니다. **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. Salesforce에서 원격 액세스 응용 프로그램을 만드는 동안 콜백 URL에서 지정해야 하는 것과 동일한 값입니다. 이러한 값은 일치해야 합니다.

1. salesforce 계정에 로그인합니다(또는 계정이 없는 경우 )에서 만듭니다. [https://developer.force.com](https://developer.force.com))
1. Salesforce에서 **만들기** > **앱** 에 대해 **연결된 앱** (이전 버전의 salesforce에서는 워크플로우가 **배포** > **원격 액세스**).
1. 클릭 **새로 만들기** Salesforce와 AEM에 연결

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 을(를) 입력합니다. **연결된 앱 이름**, **API 이름**, 및 **전자 메일 문의**. 을(를) 선택합니다 **OAuth 설정 활성화** 확인란을 선택하고 를 입력합니다. **콜백 URL** 및 OAuth 범위를 추가합니다(예: 전체 액세스). 콜백 URL은 다음과 유사합니다. `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   구성과 일치하도록 서버 이름/포트 번호 및 페이지 이름을 변경합니다.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 클릭 **저장** salesforce 구성을 저장합니다. Salesforce는 **소비자 키** 및 **소비자 비밀**: AEM 구성에 필요합니다.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >Salesforce의 원격 액세스 애플리케이션이 활성화될 때까지 몇 분(최대 15분)을 기다려야 할 수 있습니다.

1. AEM에서 **Cloud Services** 앞에서 만든 salesforce 구성으로 이동합니다(예: **개발자**). 클릭 **편집** salesforce.com에서 고객 키 및 고객 암호를 입력합니다.

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | 로그인 URL | Salesforce 인증 끝점입니다. 이 값은 사전 입력되어 대부분의 경우 제공됩니다. |
   |---|---|
   | 고객 키 | salesforce.com의 원격 액세스 응용 프로그램 등록 페이지에서 가져온 값을 입력합니다. |
   | 고객 비밀 | salesforce.com의 원격 액세스 응용 프로그램 등록 페이지에서 가져온 값을 입력합니다. |

1. 클릭 **Salesforce에 연결** 연결할 수 없습니다. Salesforce 요청은 구성이 salesforce에 연결되도록 허용합니다.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   AEM에서 성공적으로 연결되었다는 확인 대화 상자가 열립니다.

1. 웹 사이트의 루트 페이지로 이동하고 **페이지 속성**. 그런 다음 을(를) 선택합니다 **Cloud Services** 및 추가 **Salesforce** 올바른 구성을 선택합니다(예: **개발자**).

   ![chlimage_1-75](assets/chlimage_1-75.png)

   이제 워크플로우 모델을 사용하여 Salesforce에 리드를 게시하고 Salesforce에서 데이터에 액세스하는 구성 요소를 만들 수 있습니다.

## AEM 사용자를 Salesforce 리드로 내보내기 {#exporting-aem-users-as-salesforce-leads}

AEM 사용자를 Salesforce 리드로 내보내려면 리드를 Salesforce에 게시하도록 워크플로우를 구성해야 합니다.

AEM 사용자를 Salesforce 리드로 내보내려면

1. 의 Salesforce 워크플로우로 이동합니다. `http://localhost:4502/workflow` 워크플로우 마우스 오른쪽 단추 클릭 **Salesforce.com 내보내기** 및 **시작**.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 리드로 만들 AEM 사용자를 **페이로드** 이 워크플로우의 경우(홈 -> 사용자). 다음과 같은 정보가 포함되어 있으므로 사용자의 프로필 노드를 선택해야 합니다 **givenName**, **familyName** Salesforce 리드에 매핑되는 등 **FirstName** 및 **LastName** 필드.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >이 워크플로우를 시작하기 전에 AEM의 리드 노드가 Salesforce에 게시되기 전에 가져야 하는 특정 필수 필드가 있습니다. 이것들은 **givenName**, **familyName**, **회사**&#x200B;및 **이메일**. AEM 사용자와 Salesforce 리드 간의 전체 매핑 목록을 보려면 를 참조하십시오 [AEM 사용자와 Salesforce 리드 간의 구성 매핑.](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. **확인**&#x200B;을 클릭합니다. 사용자 정보는 salesforce.com으로 내보내집니다. salesforce.com에서 확인할 수 있습니다.

   >[!NOTE]
   >
   >오류 로그에 리드를 가져오는지 여부가 표시됩니다. 자세한 내용은 오류 로그를 확인하십시오.

### Salesforce.com 내보내기 워크플로우 구성 {#configuring-the-salesforce-com-export-workflow}

올바른 Salesforce.com 구성에 일치시키거나 다른 변경 작업을 수행하려면 Salesforce.com 내보내기 워크플로우를 구성해야 할 수 있습니다.

Salesforce.com 내보내기 워크플로우를 구성하려면 다음을 수행합니다.

1. 다음으로 이동 `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. Salesforce.com 내보내기 단계를 열고 **인수** 탭을 선택하고 올바른 구성을 선택한 다음 를 클릭합니다 **확인**. Salesforce에서 삭제된 리드를 워크플로우에서 다시 만들려면 확인란을 선택합니다.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 클릭 **저장** 변경 사항을 저장하려면 을 클릭합니다.

   ![chlimage_1-79](assets/chlimage_1-79.png)

### AEM 사용자와 Salesforce 리드 간의 구성 매핑 {#mapping-configuration-between-aem-user-and-salesforce-lead}

AEM 사용자와 Salesforce 리드 간의 현재 매핑 구성을 보거나 편집하려면 구성 관리자를 엽니다. `https://<hostname>:<port>/system/console/configMgr` 및 검색 **Salesforce 리드 매핑 구성**.

1. 구성 관리자를 열고 **웹 콘솔** 또는 `https://<hostname>:<port>/system/console/configMgr.`
1. 검색 대상 **Salesforce 리드 매핑 구성**.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 필요에 따라 매핑을 변경합니다. 기본 매핑은 패턴을 따릅니다 **aemUserAttribute=sfLeadAttribute**. 클릭 **저장** 변경 사항을 저장하려면 을 클릭합니다.

## Salesforce 클라이언트 컨텍스트 저장소 구성 {#configuring-salesforce-client-context-store}

Salesforce 클라이언트 컨텍스트 저장소는 AEM 내에서 이미 사용할 수 있는 정보보다 현재 로그인한 사용자에 대한 추가 정보를 표시합니다. Salesforce와의 연결에 따라 Salesforce에서 이 추가 정보를 가져옵니다.

이를 수행하려면 다음을 구성해야 합니다.

1. Salesforce 연결 구성 요소를 통해 AEM 사용자를 Salesforce ID에 연결합니다.
1. Salesforce 프로필 데이터 를 Client Context 페이지에 추가하여 보려는 속성을 구성합니다.
1. (선택 사항) Salesforce Client Context Store에서 데이터를 사용하는 세그먼트를 만듭니다.

### AEM 사용자를 Salesforce ID와 연결 {#linking-an-aem-user-with-a-salesforce-id}

Client Context에서 로드하려면 AEM 사용자를 Salesforce ID에 매핑해야 합니다. 실제 시나리오에서는 알려진 사용자 데이터를 기반으로 유효성 검사를 통해 연결됩니다. 데모 목적으로 이 절차에서는 **Salesforce 연결** 구성 요소.

1. AEM에서 웹 사이트로 이동하여 로그인한 다음, **Salesforce 연결** 구성 요소를 생성하지 않습니다.

   >[!NOTE]
   >
   >만약 **Salesforce 연결** 구성 요소를 사용할 수 없습니다. 다음 위치로 이동하십시오. **디자인** 을(를) 확인하고 선택하여 **편집** 보기.

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   구성 요소를 페이지로 끌면 해당 구성 요소가 표시됩니다 **Salesforce=Off에 연결**.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >이 구성 요소는 데모용으로만 사용됩니다. 실제 시나리오에서는 사용자를 리드와 연결/일치시키는 다른 프로세스가 있습니다.

1. 페이지에서 구성 요소를 드래그한 후 열어서 구성합니다. 구성, 연락처 유형, Salesforce 리드 또는 연락처를 선택하고 **확인**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM은 Salesforce 연락처 또는 리드와 사용자를 연결합니다.

   ![chlimage_1-83](assets/chlimage_1-83.png)

### Salesforce 데이터를 Client Context 추가 {#adding-salesforce-data-to-client-context}

Client Context에서 Salesforce에서 사용자 데이터를 로드하여 개인화에 사용할 수 있습니다.

1. 확장하려는 클라이언트 컨텍스트를 엽니다(예: `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. 을(를) 드래그합니다. **Salesforce 프로필 데이터** 구성 요소를 클라이언트 컨텍스트에 추가합니다.

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. 구성 요소를 두 번 클릭하여 엽니다. 선택 **항목 추가** 드롭다운 목록에서 속성을 선택합니다. 원하는 만큼 속성을 추가하고 을(를) 선택합니다 **확인**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. 이제 Salesforce의 Salesforce 관련 속성이 클라이언트 컨텍스트에 표시됩니다.

   ![chlimage_1-85](assets/chlimage_1-85.png)

### Salesforce Client Context Store의 데이터를 사용하여 세그먼트 작성 {#building-a-segment-using-data-from-salesforce-client-context-store}

Salesforce Client Context Store에서 데이터를 사용하는 세그먼트를 만들 수 있습니다. 이를 위해 진행되는 작업:

1. 다음 위치로 이동하여 AEM의 세그멘테이션으로 이동합니다 **도구** > **세그먼테이션** 또는 [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation).
1. Salesforce의 데이터를 포함하도록 세그먼트를 만들거나 업데이트합니다. 자세한 내용은 [세그먼테이션](/help/sites-administering/campaign-segmentation.md).

## 리드 검색 {#searching-leads}

AEM은 지정된 기준에 따라 Salesforce에서 리드를 검색하는 샘플 검색 구성 요소와 함께 제공됩니다. 이 구성 요소는 Salesforce REST API를 사용하여 salesforce 개체를 검색하는 방법을 보여줍니다. Salesforce 구성과 페이지를 연결하여 salesforce.com에 호출을 트리거해야 합니다.

>[!NOTE]
>
>Salesforce REST API를 사용하여 Salesforce 개체를 쿼리하는 방법을 보여주는 샘플 구성 요소입니다. 필요에 따라 더 복잡한 구성 요소를 만들려면 예를 사용하십시오.

이 구성 요소를 사용하려면

1. 이 구성을 사용할 페이지로 이동합니다. 페이지 속성을 열고 을 선택합니다 **Cloud Services.** 클릭 **서비스 추가** 을(를) 선택합니다. **Salesforce** 적절한 구성을 선택하고 **확인**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. Salesforce 검색 구성 요소를 페이지로 드래그합니다(활성화되어 있으면). 활성화하려면 디자인 모드로 이동하여 해당 영역에 추가합니다.

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. 검색 구성 요소를 열고 검색 매개 변수를 지정하고 **네.**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM에는 지정된 기준과 일치하는 검색 구성 요소에 지정된 리드가 표시됩니다.

   ![chlimage_1-87](assets/chlimage_1-87.png)
