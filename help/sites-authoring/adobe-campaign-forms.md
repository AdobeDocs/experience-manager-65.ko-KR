---
title: Adobe Experience Manager에서 Adobe Campaign Forms 만들기
description: Adobe Experience Manager을 사용하면 웹 사이트에서 Adobe Campaign과 상호 작용하는 양식을 만들고 사용할 수 있습니다
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: 7d60673e-484a-4447-83cf-d62a0d7ad745
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 389d5fa8de320a7237fc8290992a33743b15db99
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 1%

---

# AEM에서 Adobe Campaign Forms 만들기 {#creating-adobe-campaign-forms-in-aem}

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

이렇게 하려면 [템플릿 설명서](/help/sites-developing/templates.md#template-availability)를 참조하세요.

## 양식 만들기 {#creating-a-form}

먼저 작성자 및 게시 인스턴스 간에 연결이 작동하고 Adobe Campaign이 작동하는지 확인합니다. [Adobe Campaign Standard과 통합](/help/sites-administering/campaignstandard.md) 또는 [Adobe Campaign Classic과 통합](/help/sites-administering/campaignonpremise.md)을 참조하십시오.

>[!NOTE]
>
>Adobe Campaign Classic 또는 Adobe Campaign Standard을 사용할 때 각각 페이지의 **jcr** 노드에 있는 **acMapping:content** 속성이 **mapRecipient** 또는 **profile**(으)로 설정되어 있는지 확인하십시오
>

1. AEM의 Sites에서 페이지를 만들려는 위치로 이동합니다.
1. 페이지를 만들고 **Adobe Campaign Classic 프로필**&#x200B;또는&#x200B;**Adobe Campaign Standard 프로필**&#x200B;을 선택한 후 **다음**&#x200B;을 클릭하세요.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >원하는 서식 파일을 사용할 수 없는 경우 [서식 파일 사용 가능](/help/sites-developing/templates.md#template-availability)을 참조하세요.

1. **이름** 필드에 페이지 이름을 추가합니다. 유효한 JCR 이름이어야 합니다.
1. **제목** 필드에 제목을 입력하고 **만들기**&#x200B;를 클릭합니다.
1. 페이지를 열고 **속성 열기**&#x200B;를 선택한 다음 Cloud Services에서 Adobe Campaign 구성을 추가하고 확인 표시를 선택하여 변경 내용을 저장합니다.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. 페이지의 **양식 시작** 구성 요소에서 양식 유형을 선택합니다. **구독, 구독 취소,**&#x200B;또는&#x200B;**프로필 저장**. 양식당 한 가지 유형만 사용할 수 있습니다. 이제 [양식의 콘텐츠를 편집](#editing-form-content)할 수 있습니다.

## 양식 콘텐츠 편집 {#editing-form-content}

Adobe Campaign 전용 Forms에는 특정 구성 요소가 있습니다. 이러한 구성 요소에는 양식의 각 필드를 Adobe Campaign 데이터베이스의 필드에 연결할 수 있는 옵션이 있습니다.

>[!NOTE]
>
>원하는 템플릿을 사용할 수 없는 경우 [사용할 수 있는 템플릿 만들기](/help/sites-authoring/campaign.md)를 참조하십시오.

이 섹션에서는 Adobe Campaign에 대한 특정 링크만 자세히 설명합니다. Adobe Experience Manager에서 양식을 사용하는 방법에 대한 보다 일반적인 개요는 [편집 모드 구성 요소](/help/sites-authoring/default-components-foundation.md)를 참조하십시오.

1. **속성 열기**&#x200B;를 선택하고 Cloud Services에서 Adobe Campaign 구성을 추가하고 확인 표시를 선택하여 변경 내용을 저장합니다.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 페이지의 **양식 시작** 구성 요소에서 구성 아이콘을 클릭합니다.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. **고급** 탭을 클릭하고 양식 유형(**구독, 구독 취소,** 또는 **프로필 저장**)을 선택한 다음 **확인을 클릭합니다.** 양식당 하나의 형식만 사용할 수 있습니다.

   * **Adobe Campaign: 프로필 저장**: Adobe Campaign에서 받는 사람을 만들거나 업데이트할 수 있습니다(기본값).
   * **Adobe Campaign: 서비스에 가입**: Adobe Campaign에서 받는 사람의 구독을 관리할 수 있습니다.
   * **Adobe Campaign: 서비스에서 구독 취소**: Adobe Campaign에서 받는 사람의 구독을 취소할 수 있습니다.

1. 각 양식에 **암호화된 기본 키** 구성 요소가 있어야 합니다. 이 구성 요소는 Adobe Campaign 프로필의 암호화된 기본 키를 수락하는 데 사용되는 URL 매개 변수를 정의합니다. 구성 요소에서 Adobe Campaign을 선택하여 해당 구성 요소만 표시합니다.
1. 구성 요소 **암호화된 기본 키**&#x200B;를 폼(아무 곳에나)으로 드래그하고 **구성** 아이콘을 클릭합니다. **Adobe Campaign** 탭에서 URL 매개 변수의 이름을 지정합니다. 확인 표시를 클릭하여 변경 사항을 저장합니다.

   이 양식에 대해 생성된 링크는 이 URL 매개 변수를 사용하고, Adobe Campaign 프로필의 암호화된 기본 키를 할당해야 합니다. 암호화된 기본 키는 적절한 URL(백분율)로 인코딩되어야 합니다.

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. 텍스트 필드, 날짜 필드, 확인란 필드, 옵션 필드 등과 같은 구성 요소를 양식에 필요에 따라 추가합니다. 각 구성 요소에 대한 자세한 내용은 [Adobe Campaign 양식 구성 요소](/help/sites-authoring/adobe-campaign-components.md)를 참조하십시오.
1. 구성 아이콘을 클릭하여 구성 요소를 엽니다. 예를 들어 **텍스트 필드(캠페인)** 구성 요소에서 제목과 텍스트를 변경합니다.

   양식 필드를 Adobe Campaign 메타데이터 변수에 매핑하려면 **Adobe Campaign**&#x200B;을(를) 클릭하십시오. 양식을 제출하면 매핑된 필드가 Adobe Campaign에서 업데이트됩니다. 변수 선택기에서 형식이 일치하는 필드만 사용할 수 있습니다(예: 텍스트 필드의 문자열 변수).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >[https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)의 지침을 따라 받는 사람 테이블에 표시되는 필드를 추가/제거할 수 있습니다.

1. **페이지 게시**&#x200B;를 클릭합니다. 페이지가 사이트에서 활성화됩니다. AEM 게시 인스턴스로 이동하여 볼 수 있습니다. [양식을 테스트](#testing-a-form)할 수도 있습니다.

   >[!CAUTION]
   >
   >게시할 때 양식을 사용하려면 Cloud Service의 익명 사용자에게 읽기 권한을 제공해야 합니다. 그러나 익명 사용자에게 읽기 권한을 제공할 때 발생할 수 있는 보안 문제에 유의하고 Dispatcher 구성 등을 통해 이를 완화해야 합니다.

## 양식 테스트 {#testing-a-form}

양식을 만들고 양식 콘텐츠를 편집한 후 양식이 예상대로 작동하는지 수동으로 테스트할 수 있습니다.

>[!NOTE]
>
>각 양식에 **암호화된 기본 키** 구성 요소가 있어야 합니다. 구성 요소에서 Adobe Campaign을 선택하여 해당 구성 요소만 표시합니다.
>
>이 절차에서는 epk 번호를 수동으로 입력하더라도, 실제로 사용자는 뉴스레터 내에서 이 페이지에 대한 링크(구독 취소, 구독 또는 프로필 업데이트 여부)를 받게 됩니다. 사용자에 따라 epk가 자동으로 업데이트됩니다.
>
>해당 링크를 만들려면 변수 **기본 리소스 식별자**(Adobe Campaign Standard) 또는 **암호화된 식별자**(Adobe Campaign Classic)(예: **텍스트 및 Personalization(캠페인)** 구성 요소에서)를 사용합니다. 이 구성 요소는 Adobe Campaign의 epk로 연결됩니다.

이렇게 하려면 Adobe Campaign 프로필의 EPK를 수동으로 가져온 다음 URL에 추가해야 합니다.

1. Adobe Campaign 프로필의 암호화된 기본 키(EPK)를 가져오려면 다음을 수행하십시오.

   * Adobe Campaign Standard에서 - 기존 프로필을 나열하는 **프로필 및 대상자** > **프로필**(으)로 이동합니다. 테이블에 열에 **기본 리소스 식별자** 필드가 표시되는지 확인하십시오(**목록 구성**&#x200B;을(를) 클릭/탭하여 구성할 수 있음). 원하는 프로필의 기본 리소스 식별자를 복사합니다.
   * Adobe Campaign Classic에서 기존 프로필을 나열하는 **프로필 및 대상** > **수신자**(으)로 이동합니다. 테이블에 열에 **암호화된 식별자** 필드가 표시되는지 확인합니다. 항목을 마우스 오른쪽 단추로 클릭하고 **목록 구성...**&#x200B;을 선택하여 구성할 수 있습니다. 원하는 프로필의 암호화된 식별자를 복사합니다.

1. AEM에서 게시 인스턴스의 양식 페이지를 열고 1단계의 EPK를 URL 매개 변수로 추가합니다. 양식을 작성할 때 EPK 구성 요소에 이전에 정의한 것과 동일한 이름을 사용합니다(예: `?epk=...`).
1. 이제 양식을 사용하여 연결된 Adobe Campaign 프로필과 연결된 데이터 및 구독을 수정할 수 있습니다. 일부 필드를 수정하고 양식을 제출한 후 Adobe Campaign 내에서 적절한 데이터가 업데이트되었는지 확인할 수 있습니다.

양식의 유효성을 검사하면 Adobe Campaign 데이터베이스의 데이터가 업데이트됩니다.
