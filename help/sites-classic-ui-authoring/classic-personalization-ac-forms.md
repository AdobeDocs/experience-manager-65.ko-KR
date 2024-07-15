---
title: AEM에서 Adobe Campaign Forms 만들기
description: AEM을 사용하면 웹 사이트에서 Adobe Campaign과 상호 작용하는 양식을 만들고 사용할 수 있습니다. 특정 필드를 양식에 삽입하여 Adobe Campaign 데이터베이스에 매핑할 수 있습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3f9ed24e-c54b-4bd4-9212-eabc67bb540e
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# AEM에서 Adobe Campaign Forms 만들기{#creating-adobe-campaign-forms-in-aem}

AEM을 사용하면 웹 사이트에서 Adobe Campaign과 상호 작용하는 양식을 만들고 사용할 수 있습니다. 특정 필드를 양식에 삽입하여 Adobe Campaign 데이터베이스에 매핑할 수 있습니다.

새 연락처 구독, 구독 취소 및 사용자 프로필 데이터를 관리하면서 Adobe Campaign 데이터베이스에 데이터를 통합할 수 있습니다.

AEM에서 Adobe Campaign 양식을 사용하려면 이 문서에 설명된 다음 단계를 수행해야 합니다.

1. 템플릿을 사용할 수 있도록 설정
1. 양식을 만듭니다.
1. 양식 콘텐츠를 편집합니다.

기본적으로 Adobe Campaign에 해당하는 세 가지 유형의 양식을 사용할 수 있습니다.

* 프로필 저장
* 서비스 구독
* 서비스 구독 취소

이러한 양식은 Adobe Campaign 프로필의 암호화된 기본 키를 수락하는 URL 매개 변수를 정의합니다. 이 URL 매개 변수를 기반으로 양식은 연결된 Adobe Campaign 프로필의 데이터를 업데이트합니다.

이러한 양식을 독립적으로 생성하지만 일반적인 사용 사례에서는 뉴스레터 콘텐츠 내의 양식 페이지에 대한 개인화된 링크를 생성하여 수신자가 링크를 열고 프로필 데이터(구독 취소, 구독 또는 프로필 업데이트)를 조정할 수 있도록 합니다.

사용자를 기반으로 양식이 자동으로 업데이트됩니다. 자세한 내용은 [양식 콘텐츠 편집](#editing-form-content)을 참조하십시오.

## 템플릿 사용 가능 {#making-a-template-available}

Adobe Campaign에 고유한 양식을 만들려면 먼저 AEM 애플리케이션에서 다른 템플릿을 사용할 수 있도록 해야 합니다.

이렇게 하려면 [템플릿 설명서](/help/sites-developing/page-templates-static.md#templateavailability)를 참조하세요.

먼저 작성자 및 게시 인스턴스 간에 연결이 작동하고 Adobe Campaign이 작동하는지 확인합니다. [Adobe Campaign Standard과 통합](/help/sites-administering/campaignstandard.md) 또는 [Adobe Campaign 6.1과 통합](/help/sites-administering/campaignonpremise.md)을 참조하십시오.

>[!NOTE]
>
>Adobe Campaign 6.1.x 또는 Adobe Campaign Standard을 사용할 때 각각 페이지의 **jcr:content** 노드에 있는 **acMapping** 속성이 **mapRecipient** 또는 **profile**(으)로 설정되어 있는지 확인하십시오
>

### 양식 만들기 {#creating-a-form}

1. siteadmin에서 시작합니다.
1. 트리 구조를 스크롤하여 선택한 웹 사이트에서 양식을 작성하고자 하는 위치로 이동합니다.
1. **새로 만들기** > **새 페이지...**&#x200B;을 선택합니다.
1. **Adobe Campaign 프로필(AC 6.1)** 또는 **Adobe Campaign 프로필(ACS)** 템플릿을 선택하고 페이지 속성을 입력하십시오.

   >[!NOTE]
   >
   >템플릿을 사용할 수 없는 경우 [사용 가능한 템플릿 만들기](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate) 섹션을 참조하십시오.

1. 양식을 만들려면 **만들기**&#x200B;를 클릭하십시오.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   그런 다음 [양식의 콘텐츠를 편집하고 구성](#editing-form-content)할 수 있습니다.

## 양식 콘텐츠 편집 {#editing-form-content}

Adobe Campaign 전용 Forms에는 특정 구성 요소가 있습니다. 이러한 구성 요소에는 양식의 각 필드를 Adobe Campaign 데이터베이스의 필드에 연결할 수 있는 옵션이 있습니다.

>[!NOTE]
>
>원하는 템플릿을 사용할 수 없는 경우 [사용할 수 있는 템플릿 만들기](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate)를 참조하십시오.

이 섹션에서는 Adobe Campaign에 대한 특정 링크만 자세히 설명합니다. Adobe Experience Manager에서 양식을 사용하는 방법에 대한 보다 일반적인 개요는 [편집 모드 구성 요소](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)를 참조하십시오.

1. 편집할 양식으로 이동합니다.
1. 도구 상자에서 **페이지** > **페이지 속성...**&#x200B;을 선택한 다음 팝업 창의 **Cloud Service** 탭으로 이동합니다.
1. **서비스 추가**&#x200B;를 클릭한 다음 서비스의 드롭다운 목록에서 Adobe Campaign 인스턴스에 해당하는 구성을 선택하여 Adobe Campaign 서비스를 추가하십시오. 이 구성은 인스턴스 간 연결을 설정할 때 수행됩니다. 자세한 내용은 [Adobe Campaign에 AEM 연결](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign)을 참조하십시오.

   >[!NOTE]
   >
   >필요한 경우 자물쇠 아이콘을 클릭하여 구성의 잠금을 해제하여 Adobe Campaign 서비스를 추가할 수 있습니다.

1. 양식 시작 부분에 있는 **편집** 단추를 사용하여 양식의 일반 매개 변수에 액세스합니다. **양식** 탭에서는 양식의 유효성을 검사한 후 사용자가 리디렉션될 감사 페이지를 선택할 수 있습니다.

   **고급** 양식을 사용하여 양식 유형을 선택할 수 있습니다. **Post 옵션** 필드에서는 다음 세 가지 유형의 Adobe Campaign 양식 중에서 선택할 수 있습니다.

   * **Adobe Campaign: 프로필 저장**: Adobe Campaign에서 받는 사람을 만들거나 업데이트할 수 있습니다(기본값).
   * **Adobe Campaign: 서비스에 가입**: Adobe Campaign에서 받는 사람의 구독을 관리할 수 있습니다.
   * **Adobe Campaign: 서비스에서 구독 취소**: Adobe Campaign에서 받는 사람의 구독을 취소할 수 있습니다.

   **작업 구성** 필드를 사용하면 아직 존재하지 않는 경우 Adobe Campaign 데이터베이스에 수신자 프로필을 만들지 여부를 지정할 수 있습니다. 이렇게 하려면 **존재하지 않을 경우 사용자 만들기** 옵션을 선택하십시오.

1. 도구 상자에서 선택한 구성 요소를 끌어 폼에 놓아 추가합니다. 사용 가능한 Adobe Campaign 관련 구성 요소에 대한 자세한 내용은 [Adobe 양식 구성 요소](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)를 참조하십시오.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. 추가된 필드를 두 번 클릭하여 구성합니다. **Adobe Campaign** 탭에서는 필드를 Adobe Campaign 수신자 테이블의 필드에 연결할 수 있습니다. 필드가 Adobe Campaign 데이터베이스에 이미 있는 수신자를 인식할 수 있도록 하는 조정 키의 일부인지 여부를 지정할 수도 있습니다.

   >[!CAUTION]
   >
   >**요소 이름**&#x200B;은(는) 각 양식 필드에 대해 달라야 합니다. 필요한 경우 변경합니다.
   >
   >Adobe Campaign 데이터베이스에서 받는 사람을 올바르게 관리하려면 각 양식에 **암호화된 기본 키** 구성 요소가 있어야 합니다.

1. 도구 상자에서 **페이지** > **페이지 활성화**&#x200B;를 선택하여 페이지를 활성화합니다. 페이지가 사이트에서 활성화됩니다. AEM 게시 인스턴스로 이동하여 볼 수 있습니다. 양식의 유효성을 검사하면 Adobe Campaign 데이터베이스의 데이터가 업데이트됩니다.

## 양식 테스트 {#testing-a-form}

양식을 만들고 양식 콘텐츠를 편집한 후 양식이 예상대로 작동하는지 수동으로 테스트할 수 있습니다.

>[!NOTE]
>
>각 양식에 **암호화된 기본 키** 구성 요소가 있어야 합니다. 구성 요소에서 Adobe Campaign을 선택하여 해당 구성 요소만 표시합니다.
>
>이 절차에서는 epk 번호를 수동으로 입력하더라도, 실제로 사용자는 뉴스레터 내에서 이 페이지에 대한 링크(구독 취소, 구독 또는 프로필 업데이트 여부)를 받게 됩니다. 사용자에 따라 epk가 자동으로 업데이트됩니다.
>
>해당 링크를 만들려면 변수 **기본 리소스 식별자**(Adobe Campaign Standard) 또는 **암호화된 식별자**(Adobe Campaign 6.1)(예: **텍스트 및 Personalization(캠페인)** 구성 요소에서)를 사용합니다. 이 구성 요소는 Adobe Campaign의 epk로 연결됩니다.

이렇게 하려면 Adobe Campaign 프로필의 EPK를 수동으로 가져온 다음 URL에 추가해야 합니다.

1. Adobe Campaign 프로필의 암호화된 기본 키(EPK)를 가져오려면 다음을 수행하십시오.

   * Adobe Campaign Standard에서 - 기존 프로필을 나열하는 **프로필 및 대상자** > **프로필**(으)로 이동합니다. 테이블에 열에 **기본 리소스 식별자** 필드가 표시되는지 확인하십시오(**목록 구성**&#x200B;을(를) 클릭/탭하여 구성할 수 있음). 원하는 프로필의 기본 리소스 식별자를 복사합니다.
   * Adobe Campaign 6.11에서 기존 프로필을 나열하는 **프로필 및 대상** > **수신자**(으)로 이동합니다. 테이블에 열에 **암호화된 식별자** 필드가 표시되는지 확인합니다. 항목을 마우스 오른쪽 단추로 클릭하고 **목록 구성...**&#x200B;을 선택하여 구성할 수 있습니다. 원하는 프로필의 암호화된 식별자를 복사합니다.

1. AEM에서 게시 인스턴스의 양식 페이지를 열고 1단계의 EPK를 URL 매개 변수로 추가합니다. 양식을 작성할 때 EPK 구성 요소에 이전에 정의한 것과 동일한 이름을 사용합니다(예: `?epk=...`).
1. 이제 양식을 사용하여 연결된 Adobe Campaign 프로필과 연결된 데이터 및 구독을 수정할 수 있습니다. 일부 필드를 수정하고 양식을 제출한 후 Adobe Campaign 내에서 적절한 데이터가 업데이트되었는지 확인할 수 있습니다.

양식의 유효성을 검사하면 Adobe Campaign 데이터베이스의 데이터가 업데이트됩니다.
