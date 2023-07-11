---
title: AEM Forms 데이터 통합
seo-title: AEM Forms Data Integration
description: 데이터 통합을 통해 AEM Forms을 다양한 데이터 소스와 통합하고 양식 데이터 모델을 만들어 적응형 양식 및 대화형 커뮤니케이션을 만들고 작업할 수 있습니다.
seo-description: Data Integration lets you integrate AEM Forms with disparate data sources and create form data model to create and work with adaptive forms and interactive communications.
uuid: 01df045e-1b26-437c-9674-fd223ecd5097
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: e397c6ce-d73f-4183-8445-1897a8906960
docset: aem65
feature: Form Data Model
exl-id: dd1146e4-952d-4dfa-8084-46c6096c4177
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# [!DNL AEM Forms] 데이터 통합 {#aem-forms-data-integration}

![영웅 이미지](do-not-localize/data-integration.png)

엔터프라이즈 인프라스트럭처에는 데이터베이스, 웹 서비스, REST 서비스, OData 서비스, CRM 솔루션과 같이 서로 다른 백엔드 시스템 또는 데이터 소스가 포함됩니다. 이를 통합하여 엔터프라이즈 애플리케이션에 데이터를 제공하여 일상적인 업무를 수행하는 정보 시스템을 구축합니다. 반면에 애플리케이션은 데이터를 캡처하여 데이터 소스를 업데이트하기 위해 다시 전송합니다.

[!DNL AEM Forms] 적응형 양식 및 대화형 통신과 같은 애플리케이션을 사용하려면 양식을 렌더링하고 대화형 통신을 만드는 동안 고객 데이터를 가져오기 위해 데이터 소스와의 통합이 필요합니다. 적응형 양식의 사용자 입력을 기반으로 데이터 소스에서 데이터를 가져오는 사용 사례가 있습니다. 또한 제출된 적응형 양식 데이터를 다시 작성해 각 데이터 소스를 업데이트할 수 있습니다.

분산형 모듈식 시스템에는 고유한 이점이 있지만 데이터 소스 간에 데이터 연관성을 통합하고 만드는 것이 과제입니다. 데이터 통합은 비즈니스 데이터 교환을 위해 애플리케이션에 연결된 서로 다른 데이터 소스를 사용하는 기능적이고 효율적인 엔터프라이즈 인프라의 핵심입니다.

## 데이터 통합 개요 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] 데이터 통합을 통해 다양한 데이터 소스를 구성하고 와 연결할 수 있습니다. [!DNL AEM Forms]. 연결된 데이터 소스 전반에 걸쳐 비즈니스 엔티티 및 서비스의 통합 데이터 표현 스키마를 생성할 수 있는 직관적인 사용자 인터페이스를 제공합니다. 통합 표현을 양식 데이터 모델, JSON 스키마 확장이라고 합니다. 양식 데이터 모델의 엔티티를 데이터 모델 개체라고 합니다. 양식 데이터 모델을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* 연결된 데이터 소스에서 데이터 모델 개체, 속성 및 서비스에 액세스합니다.
* 사용자 지정 데이터 모델 개체 및 속성 만들기
* 데이터 소스 내 및 여러 데이터 모델 개체 간의 연결을 만듭니다.
* 데이터 모델 개체 서비스를 호출하여 데이터 소스에서 데이터를 쿼리하거나 씁니다.

양식 데이터 모델을 만들면 다음과 같은 다양한 적응형 양식 및 대화형 통신 워크플로우에서 사용할 수 있습니다.

* 양식 데이터 모델을 기반으로 적응형 양식 및 대화형 커뮤니케이션 만들기
* 구성된 데이터 소스에서 적응형 양식 및 대화형 통신 미리 채우기
* 적응형 양식 규칙을 사용하여 데이터 소스 서비스/작업 호출
* 제출된 적응형 양식 데이터를 데이터 소스에 쓰기

## 데이터 통합 시작 {#get-started-with-data-integration}

데이터 통합을 구현하는 첫 번째 단계는 적응형 양식 및 대화형 통신 사용 사례에서 활용할 정보를 저장하는 데이터 소스를 식별하고 구성하는 것입니다. 그런 다음 하나 이상의 데이터 소스에서 데이터 모델 개체, 속성 및 서비스를 사용하는 양식 데이터 모델을 만듭니다. 대화형 커뮤니케이션의 적응형 양식 필드 또는 자리 표시자가 각 데이터 소스 속성에 바인딩되는 양식 데이터 모델을 기반으로 적응형 양식 및 대화형 커뮤니케이션을 만들 수 있습니다.

[!DNL AEM Forms] 또한 데이터 소스와 독립적인 양식 데이터 모델을 만들고 나중에 양식 데이터 모델의 데이터 모델 개체 및 속성을 데이터 소스와 연결하거나 바인딩할 수 있습니다. 양식 데이터 모델을 사용하는 동안 데이터 소스에 대한 종속성을 제거합니다.

데이터 통합을 시작, 이해 및 구현하려면 다음을 검토하십시오.

* [데이터 소스 구성](../../forms/using/configure-data-sources.md)
* [양식 데이터 모델 만들기](../../forms/using/create-form-data-models.md)
* [양식 데이터 모델 작업](../../forms/using/work-with-form-data-model.md)
* [양식 데이터 모델 사용](../../forms/using/using-form-data-model.md)
