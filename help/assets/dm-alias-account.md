---
title: Dynamic Media 회사 별칭 계정 구성
description: Dynamic Media에서 회사 별칭 계정을 구성하는 방법을 알아봅니다.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

<!-- hide: yes
hidefromtoc: yes -->

# Dynamic Media 회사 별칭 계정 구성 정보 {#about-dm-alias-acct}

Dynamic Media URL 및 뷰어 포함 코드에 회사 계정 이름이 포함되어 있습니다. 이 계정 이름은 Dynamic Media 프로비저닝 시 생성되었습니다. 비즈니스에서 획득이나 리브랜딩을 받았거나, 더 기억에 남을 이름을 사용하고 싶은 시나리오가 있을 수 있습니다. 이러한 시나리오에서는 즉시 제공되는 모든 URL 및 뷰어 포함 코드에서 회사 계정 이름을 수동으로 업데이트하는 것이 쉽지 않습니다. 또한 기존 Dynamic Media 저장소에 영향을 주거나 라이브 컨텐츠에 영향을 줄 수 있습니다. 이 문제를 해결하려면 Dynamic Media 회사 별칭 계정을 구성할 수 있습니다.

Dynamic Media 회사 별칭 계정을 사용하면 사용자 인터페이스에 있는 즉시 사용 가능한 모든 Dynamic Media URL 및 뷰어 포함 코드가 리브랜딩과 같은 비즈니스 컨텍스트에 대한 업데이트를 반영하도록 할 수 있습니다. Dynamic Media URL 및 뷰어 포함 코드는 새 회사 계정 이름을 반영하므로 별칭 계정은 SEO(검색 엔진 최적화)에 긍정적인 영향을 줍니다.

Dynamic Media 회사 별칭 계정을 구성할 때는 다음 사항에 유의하십시오.

* 기존 Dynamic Media URL 또는 뷰어 포함 코드를 *live* 새 별칭 이름을 반영하려면 디지털 속성을 수동으로 업데이트해야 합니다. 그러나 원래 Dynamic Media 회사 이름의 모든 URL 또는 뷰어 포함 코드는 기존 또는 새 자산에 대해 계속 작동합니다.
* Dynamic Media 회사 별칭 계정 기능은 Experience Manager Assets 작성 모드 및 게재로 제한됩니다. 회사 별칭 이름이 Experience Manager Sites에서 작동하지 않습니다. WCM(Web Content Management) 구성 요소는 이 변경 사항에 대해 업데이트되지 않습니다. 이러한 구성 요소는 Dynamic Media 자산을 가져오기 위해 원래 Dynamic Media 회사 이름과 계속 작동합니다.
* 에서 회사 별칭 계정을 하나만 설정할 수 있습니다 **[!UICONTROL Dynamic Media 구성 편집]** 페이지. 그러나 지원 사례를 통해 회사 별칭 계정을 최대 여러 개 만들고 Dynamic Media URL 또는 뷰어 포함 코드에 필요한 별칭 이름을 수동으로 반영할 수 있습니다.
* 즉시 사용 가능한 [캐시 무효화](/help/assets/invalidate-cdn-cache-dynamic-media.md) Dynamic Media의 기능은 Cloud Services의 Dynamic Media 구성 페이지에 구성된 회사 및 회사 별칭 계정 모두로 URL을 무효화합니다.
* 에서 회사 별칭 계정을 구성할 때 **[!UICONTROL Dynamic Media 구성 편집]** 페이지, 캐시 무효화에 성공하려면 URL을 무효화해야 합니다. *둘 다* a **[!UICONTROL 회사]** 계정 및 **[!UICONTROL 회사 별칭]** 계정을 동시에 사용합니다.

참조 - [Cloud Services에서 Dynamic Media 구성 만들기](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Dynamic Media 회사 별칭 계정 구성 {#configure-dm-alias-account}

먼저 지원 사례를 제출하여 Dynamic Media 회사 별칭 계정 구성을 시작합니다. 이 단계는 필수입니다.

1. [Admin Console을 사용하여 지원 사례를 만듭니다](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. 지원 사례에 다음 정보를 제공하십시오.

   * 사용할 Dynamic Media 회사 별칭 이름입니다. 이름은 다음을 포함해야 합니다 *전용* 문자(대/소문자 혼합 허용), 숫자, 하이픈 및 밑줄
   * 지역
   * 선택 [규칙 세트](/help/assets/using-rulesets-to-transform-urls.md) 대체 Dynamic Media 회사 계정 이름을 통해 Dynamic Media 컨텐츠 제공을 위해 이전에 사용되고 있습니다.

1. Dynamic Media 별칭 계정이 지원에서 만든 후 Experience Manager as a Cloud Service 작성자 인스턴스에서 Experience Manager as a Cloud Service 로고를 선택하여 전역 탐색 콘솔에 액세스합니다.
1. 콘솔 왼쪽에서 도구 아이콘을 선택한 다음 로 이동합니다 **[!UICONTROL Cloud Services > Dynamic Media 구성]**.
1. Dynamic Media 구성 브라우저 페이지의 왼쪽 창에서 **[!UICONTROL 글로벌]** (폴더 아이콘을 의 왼쪽에 선택하지 마십시오.) **[!UICONTROL 글로벌]**). 그런 다음 을(를) 선택합니다 **[!UICONTROL 편집]**.

   ![Dynamic Media 회사 별칭 텍스트 필드](/help/assets/assets-dm/dm-company-alias.png)

1. 설정 **[!UICONTROL Dynamic Media 구성 편집]** 페이지, **[!UICONTROL 회사 별칭]** 텍스트 필드에 지원 사례에서 이전에 지정한 Dynamic Media 별칭 계정 이름을 입력합니다.
1. 페이지 오른쪽 상단에서 을 선택합니다 **[!UICONTROL 저장]**.
이제 Dynamic Media 회사 별칭 계정이 저장되고 활성화됩니다. 이제 기존 및 새 자산에 대한 모든 URL 및 뷰어 포함 코드가 새 회사 별칭 이름을 반영합니다.
