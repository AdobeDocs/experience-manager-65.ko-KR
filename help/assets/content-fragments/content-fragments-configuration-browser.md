---
title: 컨텐츠 조각 - 구성 브라우저
description: AEM의 강력한 헤드리스 게재 기능을 활용하기 위해 구성 브라우저에서 특정 컨텐츠 조각 기능을 활성화하는 방법을 알아봅니다.
feature: Content Fragments
role: User
exl-id: a9990b0c-56c7-4e61-bae9-98e19a7f364e
source-git-commit: 8dc8eff86ff25534a578dd227033aa185853d930
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 31%

---

# 컨텐츠 조각 - 구성 브라우저{#content-fragments-configuration-browser}

AEM의 강력한 헤드리스 게재 기능을 활용하기 위해 구성 브라우저에서 특정 컨텐츠 조각 기능을 활성화하는 방법을 알아봅니다.

## 인스턴스용 콘텐츠 조각 기능 활성화 {#enable-content-fragment-functionality-instance}

컨텐츠 조각을 사용하기 전에 **구성 브라우저** 를 사용하려면 다음을 수행하십시오.

* **컨텐츠 조각 모델** - 필수
* **GraphQL 영구 쿼리** - 선택 사항

>[!CAUTION]
>
>활성화하지 않은 경우 **컨텐츠 조각 모델**:
>
>* a **만들기** 새 모델을 만드는 데에는 옵션을 사용할 수 없습니다.
>* 당신은 [사이트 구성을 선택하여 관련 끝점을 만듭니다](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint).


컨텐츠 조각 기능을 활성화하려면 필요한 단계가 있습니다.

* 구성 브라우저를 통해 컨텐츠 조각 기능을 사용할 수 있도록 설정
* 자산 폴더에 구성 적용

### 구성 브라우저에서 컨텐츠 조각 기능 활성화 {#enable-content-fragment-functionality-in-configuration-browser}

종료 [특정 컨텐츠 조각 기능 사용](#creating-a-content-fragment-model) you **반드시** 먼저 을 통해 활성화합니다 **구성 브라우저**:

>[!NOTE]
>
>자세한 내용은 [구성 브라우저:](/help/sites-administering/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>하위 구성(구성 내에 중첩된 구성)은 컨텐츠 조각에서 사용할 수 있지만 GraphQL 쿼리에 사용할 수 없습니다.

1. **도구**, **일반**&#x200B;으로 이동한 후 **Configuration Browser**&#x200B;를 엽니다.

1. **만들기**&#x200B;를 사용하여 대화 상자를 열고 여기에서

   1. **제목**&#x200B;을 지정합니다.
   1. 사용을 활성화하려면 를 선택합니다
      * **콘텐츠 조각 모델**
      * **GraphQL 지속 쿼리**

      ![구성 정의](assets/cfm-conf-01.png)


1. **만들기**&#x200B;를 선택하여 정의를 저장합니다.

<!-- 1. Select the location appropriate to your website. -->

### 자산 폴더에 구성 적용 {#apply-the-configuration-to-your-assets-folder}

구성 시 **글로벌** 컨텐츠 조각 기능에 대해 활성화되어 있으면 모든 자산 폴더에 적용됩니다.

비교 가능한 자산 폴더와 함께 다른 구성(즉, 전역 제외)을 사용하려면 연결을 정의해야 합니다. This is done by selecting the appropriate **Configuration** in the **Cloud Services** tab of the **Folder Properties** of the appropriate folder.

![구성 적용](assets/cfm-conf-02.png)
