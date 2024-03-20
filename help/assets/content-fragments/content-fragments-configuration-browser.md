---
title: 콘텐츠 조각 - 구성 브라우저
description: 구성 브라우저에서 특정 콘텐츠 조각 기능을 활성화하여 Adobe Experience Manager의 강력한 Headless 게재 기능을 사용하는 방법에 대해 알아봅니다.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 49%

---

# 콘텐츠 조각 - 구성 브라우저{#content-fragments-configuration-browser}

구성 브라우저에서 특정 콘텐츠 조각 기능을 활성화하여 Adobe Experience Manager(AEM)의 강력한 Headless 게재 기능을 사용하는 방법에 대해 알아봅니다.

## 인스턴스에 대해 콘텐츠 조각 기능 활성화 {#enable-content-fragment-functionality-instance}

콘텐츠 조각을 사용하기 전에 **구성 브라우저** 다음을 활성화하려면:

* **콘텐츠 조각 모델** - 필수
* **GraphQL 지속 쿼리** - 선택 사항

>[!CAUTION]
>
>**콘텐츠 조각 모델**&#x200B;을 활성화하지 않는 경우
>
>* 모델을 만들 때 **만들기** 옵션을 사용할 수 없습니다.
>* 다음을 수행할 수 없음 [사이트 구성을 선택하여 관련 끝점을 생성합니다.](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint).

콘텐츠 조각 기능을 활성화하려면 다음 작업을 수행해야 합니다.

* 구성 브라우저를 통해 콘텐츠 조각 기능 사용 활성화
* 자산 폴더에 구성 적용

### 구성 브라우저에서 콘텐츠 조각 기능 활성화 {#enable-content-fragment-functionality-in-configuration-browser}

종료 [특정 콘텐츠 조각 기능 사용](#creating-a-content-fragment-model), 본인 **필수** 먼저 다음을 통해 활성화합니다. **구성 브라우저**:

>[!NOTE]
>
>자세한 내용은 [구성 브라우저:](/help/sites-administering/configurations.md#using-configuration-browser).

1. **도구**, **일반**&#x200B;으로 이동한 다음 **구성 브라우저**&#x200B;를 엽니다.

1. **만들기**&#x200B;를 사용하여 대화 상자를 열고 여기에서

   1. **제목**&#x200B;을 지정합니다.
   1. 사용을 활성화하려면 다음을 선택합니다.
      * **콘텐츠 조각 모델**
      * **GraphQL 지속 쿼리**

      ![구성 정의](assets/cfm-conf-01.png)

1. **만들기**&#x200B;를 선택하여 정의를 저장합니다.

<!-- 1. Select the location appropriate to your website. -->

### 자산 폴더에 구성 적용 {#apply-the-configuration-to-your-assets-folder}

구성 시 **글로벌** 가 콘텐츠 조각 기능에 대해 활성화된 후 모든 에셋 폴더에 적용됩니다.

비교 가능한 자산 폴더와 함께 다른 구성(전역 제외)을 사용하려면 연결을 정의해야 합니다. This is done by selecting the appropriate **Configuration** in the **Cloud Services** tab of the **Folder Properties** of the appropriate folder.

![구성 적용](assets/cfm-conf-02.png)
