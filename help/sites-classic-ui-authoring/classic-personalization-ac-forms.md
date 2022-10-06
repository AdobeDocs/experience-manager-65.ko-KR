---
title: AEM에서 Adobe Campaign 양식 작성
seo-title: Creating Adobe Campaign Forms in AEM
description: AEM에서는 웹 사이트에서 Adobe Campaign과 상호 작용하는 양식을 작성하고 사용할 수 있습니다. 특정 필드를 양식에 삽입하고 Adobe Campaign 데이터베이스에 매핑할 수 있습니다.
seo-description: AEM lets you create and use forms that interact with Adobe Campaign on your website. Specific fields can be inserted into your forms and mapped to the Adobe Campaign database.
uuid: 7b1028f3-268a-4d4d-bc9f-acd176f5ef3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 3086a8a1-8d2e-455a-a055-91b07d31ea65
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 62%

---

# AEM에서 Adobe Campaign 양식 작성{#creating-adobe-campaign-forms-in-aem}

AEM에서는 웹 사이트에서 Adobe Campaign과 상호 작용하는 양식을 작성하고 사용할 수 있습니다. 특정 필드를 양식에 삽입하고 Adobe Campaign 데이터베이스에 매핑할 수 있습니다.

데이터를 Adobe Campaign 데이터베이스에 통합하는 내내 새로운 연락처 가입, 가입 해지 및 사용자 프로필 데이터를 관리할 수 있습니다.

AEM에서 Adobe Campaign 양식을 사용하려면 이 문서에 설명된 다음 절차를 따라야 합니다.

1. 템플릿을 사용할 수 있도록 합니다.
1. 양식을 작성합니다.
1. 양식 컨텐츠를 편집합니다.

Adobe Campaign에 사용하는 세 가지 유형의 양식을 기본적으로 사용할 수 있습니다.

* 프로필 저장
* 서비스 가입
* 서비스 가입 해지

이러한 양식은 Adobe Campaign 프로필의 암호화된 기본 키를 허용하는 URL 매개 변수를 정의합니다. 양식은 연결된 Adobe Campaign 프로필의 데이터를 이 URL 매개 변수를 기반으로 업데이트합니다.

이러한 양식을 독립적으로 만들더라도 일반적인 사용 사례에서는 수신자가 링크를 열고 프로필 데이터를 조정(해당 프로필을 가입하든지, 가입 해지하든지 또는 업데이트하든지 간에)할 수 있도록 뉴스레터 컨텐츠 내에 양식 페이지를 연결하는 개인화된 링크를 생성합니다.

양식은 사용자를 기반으로 자동으로 업데이트됩니다. 자세한 내용은 [양식 컨텐츠 편집](#editing-form-content)을 참조하십시오.

## 템플릿을 사용할 수 있도록 설정 {#making-a-template-available}

Adobe Campaign에 사용되는 양식을 작성하려면 먼저 AEM 애플리케이션에서 다른 템플릿을 사용할 수 있도록 해야 합니다.

이렇게 하려면 다음을 참조하십시오. [템플릿 설명서](/help/sites-developing/page-templates-static.md#templateavailability).

먼저 작성 및 게시 인스턴스와 Adobe Campaign 간에 제대로 연결되었는지 확인하십시오. [Adobe Campaign Standard와 통합](/help/sites-administering/campaignstandard.md) 또는 [Adobe Campaign 6.1과 통합](/help/sites-administering/campaignonpremise.md)을 참조하십시오.

>[!NOTE]
>
>Adobe Campaign 6.1.x 또는 Adobe Campaign Standard를 각각 사용할 경우 페이지의 **jcr:content** 노드에 대한 **acMapping**&#x200B;속성이 **mapRecipient** 또는 **profile**&#x200B;로 설정되어 있는지 확인하십시오.

### 양식 만들기 {#creating-a-form}

1. siteadmin을 시작합니다.
1. 트리 구조를 스크롤하여 선택한 웹 사이트에서 양식을 작성하려는 위치로 이동합니다.
1. 선택 **새로 만들기** > **새 페이지...**.
1. 다음 중 하나를 선택합니다 **Adobe Campaign 프로필(AC 6.1)** 또는 **Adobe Campaign 프로필(ACS)** 템플릿을 사용하여 페이지 속성을 입력합니다.

   >[!NOTE]
   >
   >템플릿을 사용할 수 없는 경우 [템플릿 사용 가능](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) 섹션을 참조하십시오.

1. 클릭 **만들기** 양식을 만들려면

   ![chlimage_1-187](assets/chlimage_1-187.png)

   그런 다음, [양식의 컨텐츠를 편집 및 구성](#editing-form-content)할 수 있습니다.

## 양식 컨텐츠 편집 {#editing-form-content}

Adobe Campaign 전용 양식에는 특정 구성 요소가 있습니다. 이러한 구성 요소에는 양식의 각 필드를 Adobe Campaign 데이터베이스의 필드에 연결할 수 있는 선택 사항이 있습니다.

>[!NOTE]
>
>원하는 템플릿을 사용할 수 없는 경우 을 참조하십시오. [템플릿 사용 가능](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

이 섹션에서는 Adobe Campaign을 연결하는 특정 링크에 대해서만 자세히 설명합니다. Adobe Experience Manager에서 양식을 사용하는 방법에 대한 일반적인 개요에 대한 자세한 내용은 [편집 모드 구성 요소](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. 편집할 양식으로 이동합니다.
1. 도구 상자에서 **페이지** > **페이지 속성...** 그런 다음 **Cloud Services** 팝업 창의 탭입니다.
1. 다음을 클릭하여 Adobe Campaign 서비스 추가 **서비스 추가**&#x200B;그런 다음 서비스의 드롭다운 목록에서 Adobe Campaign 인스턴스에 해당하는 구성을 선택합니다. 이 구성은 인스턴스 간 연결을 설정할 때 수행됩니다. 자세한 내용은 [Adobe Campaign에 AEM 연결](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >필요한 경우, Adobe Campaign 서비스를 추가하려면 자물쇠 아이콘을 클릭하여 구성을 잠금 해제하십시오.

1. 을 사용하여 양식의 일반 매개 변수에 액세스합니다 **편집** 양식 시작 부분에 있는 단추입니다. 다음 **양식** 탭에서 양식의 유효성을 검사한 후 사용자를 리디렉션할 감사 인사 페이지를 선택할 수 있습니다.

   다음 **고급** 양식을 사용하면 양식의 유형을 선택할 수 있습니다. 다음 **게시 옵션** 필드에서는 다음 세 가지 유형의 Adobe Campaign 양식을 선택할 수 있습니다.

   * **Adobe Campaign: 프로필 저장**: Adobe Campaign(기본값)에서 수신자를 생성하거나 업데이트할 수 있습니다.
   * **Adobe Campaign: 서비스에 가입**: Adobe Campaign에서 수신자의 가입을 관리할 수 있습니다.
   * **Adobe Campaign: 서비스 가입 해지**: Adobe Campaign에서 수신자의 가입을 취소할 수 있습니다.

   다음 **작업 구성** 필드를 사용하면 수신자 프로필이 아직 없는 경우 Adobe Campaign 데이터베이스에서 수신자 프로필을 만들지 여부를 지정할 수 있습니다. 이렇게 하려면 **존재하지 않을 경우 사용자 만들기** 선택 사항입니다.

1. 도구 상자의 구성 요소를 양식에 드래그하여 놓아 선택한 구성 요소를 추가합니다. 사용 가능한 Adobe Campaign용 구성 요소에 대한 자세한 내용은 [Adobe 양식 구성 요소](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)를 참조하십시오.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 추가한 필드를 두 번 클릭하여 구성합니다. 다음 **Adobe Campaign** 탭에서 필드를 Adobe Campaign 수신자 테이블의 필드에 연결할 수 있습니다. 또한 필드가 이미 Adobe Campaign 데이터베이스에 있는 수신자를 인식할 수 있도록 해주는 조정 키의 일부인지 여부를 지정할 수도 있습니다.

   >[!CAUTION]
   >
   >다음 **요소 이름** 각 양식 필드에 대해 달라야 합니다. 필요한 경우 변경하십시오.
   >
   >각 양식에는 **암호화된 기본 키** 구성 요소를 사용하여 Adobe Campaign 데이터베이스에서 수신자를 올바르게 관리할 수 있습니다.

1. 을(를) 선택하여 페이지를 활성화합니다 **페이지** > **페이지 활성화** 도구 상자에 표시합니다. 사이트에서 페이지가 활성화됩니다. AEM 게시 인스턴스로 이동하여 이것을 확인할 수 있습니다. 양식의 유효성이 검증되면 Adobe Campaign 데이터베이스의 데이터가 업데이트됩니다.

## 양식 테스트 {#testing-a-form}

양식을 작성하고 양식 컨텐츠를 편집한 후 양식이 예상대로 작동하는지 수동으로 테스트할 수 있습니다.

>[!NOTE]
>
>다음을 수행해야 합니다. **암호화된 기본 키** 구성 요소를 생성하지 않습니다. [구성 요소]에서 해당 구성 요소만 표시되도록 Adobe Campaign을 선택합니다.
>
>이 절차에서는 epk(암호화된 기본 키) 번호를 수동으로 입력하지만 실제로는 사용자가 뉴스레터 내에서 이 페이지에 연결하는 링크를 가져오게 됩니다(프로필을 가입 해지하든지, 가입하든지 또는 업데이트하든지 간에). epk는 사용자를 기반으로 자동으로 업데이트됩니다.
>
>해당 링크를 만들려면 변수를 사용합니다 **기본 리소스 식별자**(Adobe Campaign Standard) 또는 **암호화된 식별자** (Adobe Campaign 6.1) (예: **텍스트 및 개인화(캠페인)** 구성 요소)가 있어야 합니다.

이렇게 하려면 Adobe Campaign 프로필의 EPK를 수동으로 가져온 다음, URL에 추가해야 합니다.

1. Adobe Campaign 프로필의 암호화된 기본 키(EPK)를 가져오려면 다음을 수행하십시오.

   * Adobe Campaign Standard에서 - 다음 위치로 이동합니다. **프로필 및 대상자** > **프로필**: 기존 프로필을 나열합니다. 표에 **기본 리소스 식별자** 열의 필드(클릭/탭하여 구성할 수 있음) **목록 구성**). 원하는 프로필의 기본 리소스 ID를 복사하십시오.
   * Adobe Campaign 6.11에서 **프로필 및 Target** >  **수신자**: 기존 프로필을 나열합니다. 표에 **암호화된 식별자** 열의 필드(항목을 마우스 오른쪽 단추로 클릭하고 선택하여 구성할 수 있습니다 **목록 구성...**). 원하는 프로필의 암호화된 ID를 복사하십시오.

1. AEM에서 게시 인스턴스의 양식 페이지를 열고 1단계의 EPK를 URL 매개 변수로 추가합니다. 양식을 작성할 때 이전에 EPK 구성 요소에서 정의한 이름과 동일한 이름(예: `?epk=...`)
1. 이제 연결된 Adobe Campaign 프로필과 연결된 데이터와 가입을 수정하는 데 이 양식을 사용할 수 있습니다. 일부 필드를 수정하고 양식을 제출한 후 적절한 데이터가 업데이트된 것을 Adobe Campaign 내에서 확인할 수 있습니다.

양식의 유효성이 검증되면 Adobe Campaign 데이터베이스의 데이터가 업데이트됩니다.
