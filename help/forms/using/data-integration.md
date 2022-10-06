---
title: AEM Forms 데이터 통합
seo-title: AEM Forms Data Integration
description: 데이터 통합을 사용하면 AEM Forms을 서로 다른 데이터 소스와 통합하고 양식 데이터 모델을 만들어 적응형 양식 및 대화형 커뮤니케이션을 만들고 사용할 수 있습니다.
seo-description: Data Integration lets you integrate AEM Forms with disparate data sources and create form data model to create and work with adaptive forms and interactive communications.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
feature: Form Data Model
exl-id: dd1146e4-952d-4dfa-8084-46c6096c4177
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# [!DNL AEM Forms] 데이터 통합 {#aem-forms-data-integration}

![](do-not-localize/data-integeration.png)

엔터프라이즈 인프라스트럭처에는 데이터베이스, 웹 서비스, REST 서비스, OData 서비스, CRM 솔루션과 같은 다양한 백엔드 시스템 또는 데이터 소스가 포함됩니다. 즉, 기업 애플리케이션에 데이터를 제공하는 정보 시스템을 구축하여 일상적인 비즈니스를 수행할 수 있습니다. 반면 애플리케이션은 데이터를 캡처하여 다시 전송하여 데이터 소스를 업데이트합니다.

[!DNL AEM Forms] 적응형 양식 및 대화형 커뮤니케이션과 같은 애플리케이션을 사용하려면 양식을 렌더링하고 대화형 커뮤니케이션을 만드는 동안 고객 데이터를 가져오기 위해 데이터 소스와 통합되어야 합니다. 적응형 양식의 사용자 입력을 기반으로 데이터 소스에서 데이터를 가져오는 경우의 사용 사례가 있습니다. 또한 제출된 적응형 양식 데이터를 다시 작성하여 각 데이터 소스를 업데이트할 수 있습니다.

분산 모듈식 시스템에는 자체 이점이 있지만 데이터 소스 간에 데이터 연결을 통합하고 생성하는 것이 당면 과제입니다. 데이터 통합은 비즈니스 데이터를 교환하기 위해 애플리케이션과 연결된 서로 다른 데이터 소스를 통해 기능적이고 효율적인 엔터프라이즈 인프라의 핵심입니다.

## 데이터 통합 개요 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] 데이터 통합을 통해 서로 다른 데이터 소스를 구성하고 [!DNL AEM Forms]. 또한 직관적인 사용자 인터페이스를 통해 연결된 데이터 소스 간에 비즈니스 엔티티와 서비스의 통합 데이터 표현 스키마를 생성할 수 있습니다. 통합 표현은 JSON 스키마 확장인 양식 데이터 모델이라고 합니다. 양식 데이터 모델의 엔티티를 데이터 모델 개체라고 합니다. 양식 데이터 모델을 사용하면 다음 작업을 수행할 수 있습니다.

* 연결된 데이터 소스에서 데이터 모델 개체, 속성 및 서비스에 액세스합니다.
* 사용자 정의 데이터 모델 개체 및 속성 만들기
* 데이터 소스 내 및 여러 데이터 모델 개체 간의 연결을 만듭니다.
* 데이터 모델 개체 서비스를 호출하여 데이터 소스와 데이터 소스의 데이터를 쿼리하거나 씁니다.

양식 데이터 모델을 만들면 다음과 같은 다양한 적응형 양식 및 대화형 커뮤니케이션 워크플로우에서 사용할 수 있습니다.

* 양식 데이터 모델을 기반으로 적응형 양식 및 인터랙티브 커뮤니케이션 제작
* 구성된 데이터 소스에서 적응형 양식 및 대화형 커뮤니케이션 미리 채우기
* 적응형 양식 규칙을 사용하여 데이터 소스 서비스/작업 호출
* 제출된 적응형 양식 데이터를 데이터 소스에 쓰기

## 데이터 통합 시작 {#get-started-with-data-integration}

데이터 통합을 구현하는 첫 번째 단계는 적응형 양식 및 대화형 커뮤니케이션 사용 사례에서 활용할 정보를 저장하는 데이터 소스를 식별하고 구성하는 것입니다. 그런 다음 하나 이상의 데이터 소스에서 데이터 모델 개체, 속성 및 서비스를 사용하는 양식 데이터 모델을 만듭니다. 적응형 양식 필드 또는 대화형 커뮤니케이션의 자리 표시자가 각 데이터 소스 속성에 바인딩되는 양식 데이터 모델을 기반으로 적응형 양식 및 대화형 커뮤니케이션을 만들 수 있습니다.

[!DNL AEM Forms] 또한 데이터 소스와 관계없이 양식 데이터 모델을 만들고 나중에 데이터 모델의 데이터 모델 개체 및 속성을 데이터 소스와 연결하거나 바인딩할 수 있습니다. 양식 데이터 모델에서 작업하는 동안 데이터 소스에 대한 종속성이 제거됩니다.

데이터 통합을 시작, 이해 및 구현하려면 다음 사항을 검토하십시오.

* [데이터 소스 구성](../../forms/using/configure-data-sources.md)
* [양식 데이터 모델 만들기](../../forms/using/create-form-data-models.md)
* [양식 데이터 모델 작업](../../forms/using/work-with-form-data-model.md)
* [양식 데이터 모델 사용](../../forms/using/using-form-data-model.md)
