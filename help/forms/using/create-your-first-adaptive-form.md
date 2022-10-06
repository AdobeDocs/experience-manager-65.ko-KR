---
title: "자습서: 첫 번째 적응형 양식 만들기"
seo-title: "Tutorial: Create your first adaptive form"
description: 비즈니스 클래스, 대화형 및 반응형 양식을 만드는 방법을 알아봅니다.
seo-description: Learn to create business class, interactive, and responsive forms.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
source-git-commit: 471d7f48dc4653000b4852dbbeb886b05e28e644
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# 자습서: 첫 번째 적응형 양식 만들기 {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## 소개 {#introduction}

모바일 친화적 제품을 찾고 계십니까 **양식 경험** 등록을 단순화하고 참여를 늘리고 전환 시간을 줄일 수 있습니다. **적응형 양식** 딱 맞네요. 적응형 양식은 모바일, 자동화 및 분석에 적합한 양식 경험을 제공합니다. 실제로 반응형 및 대화형 양식을 손쉽게 작성하고, 자동화된 프로세스를 사용하여 관리 및 반복 작업을 줄이고, 데이터 분석을 사용하여 고객이 보유한 경험을 개선하거나 개인화할 수 있습니다.

이 자습서에서는 적응형 양식을 만드는 종단 간 프레임워크를 제공합니다. 이 자습서는 사용 사례와 여러 안내서로 구성되어 있습니다. 각 안내서는 이 자습서에서 만든 적응형 양식에 새 기능을 학습하고 추가하는 데 도움이 됩니다. 모든 안내서 뒤에 작업 적응형 양식이 있습니다. 적응형 양식 만들기 안내서를 사용할 수 있습니다. 후속 가이드가 곧 제공될 예정입니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* 적응형 양식 및 양식 데이터 모델을 만듭니다.
* 적응형 양식의 스타일을 지정합니다.
* 적응형 양식 규칙 편집기를 사용하여 비즈니스 규칙을 작성할 수 있습니다.
* 적응형 양식을 테스트하고 게시합니다.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

여정은 사용 사례를 학습하여 시작됩니다.

웹 사이트에서는 다양한 고객을 위한 다양한 제품을 제공합니다. 고객이 포털을 탐색하고 제품을 선택하고 순서를 지정합니다. 모든 고객은 계정을 만들고 배송 및 청구 주소를 제공합니다. 기존 고객인 새라 로즈는 자신의 배송 주소를 웹사이트에 추가하길 기대하고 있다. 웹 사이트에서는 배송 주소를 추가하고 업데이트하는 온라인 양식을 제공합니다.

웹 사이트는 Adobe Experience Manager(AEM)에서 실행되며 AEM을 사용합니다 [!DNL Forms] 데이터 캡처 및 처리용. 주소 추가 및 업데이트 양식은 적응형 양식입니다. 웹 사이트는 고객 세부 사항을 데이터베이스에 저장합니다. 주소 추가 및 업데이트 양식을 사용하여 사용 가능한 주소를 검색하고 표시합니다. 또한 적응형 양식을 사용하여 업데이트되고 새 주소를 수락합니다.

### 전제 조건 {#prerequisite}

* AEM 작성자 인스턴스를 설정합니다.
* 설치 [AEM Forms 추가 기능](../../forms/using/installing-configuring-aem-forms-osgi.md) 작성자 인스턴스에서 사용됩니다.
* 데이터베이스 공급자에서 JDBC 데이터베이스 드라이버(JAR 파일)를 가져옵니다. 자습서의 예는 를 기반으로 합니다 [!DNL MySQL] 데이터베이스 및 사용 [!DNL Oracle's] [MySQL JDBC 데이터베이스 드라이버](https://dev.mysql.com/downloads/connector/j/5.1.html).

* 아래 필드가 표시된 고객 데이터가 포함된 데이터베이스를 설정합니다. 적응형 양식을 만드는 데에는 데이터베이스가 필요하지 않습니다. 이 자습서에서는 데이터베이스를 사용하여 AEM의 양식 데이터 모델 및 지속성 기능을 표시합니다 [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## 1단계: 적응형 양식 만들기 {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

적응형 양식은 자연에서 새로운 세대, 매력적인 반응형, 동적 및 적응형입니다. 적응형 양식을 사용하여 개인화된 및 타깃팅된 경험을 제공할 수 있습니다. AEM [!DNL Forms] 끌어서 놓기 WYSIWYG 편집기를 제공하여 적응형 양식을 만듭니다. 적응형 양식에 대한 자세한 내용은 [적응형 양식 작성 소개](../../forms/using/introduction-forms-authoring.md).

목표:

* 고객이 배송 주소를 추가할 수 있도록 하는 적응형 양식을 만듭니다
* 고객의 정보를 표시하고 수락하는 적응형 양식의 레이아웃 필드
* 양식 컨텐츠가 포함된 이메일을 전송하기 위한 제출 작업 만들기
* 적응형 양식 미리 보기 및 제출

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## 2단계: 양식 데이터 모델 만들기 {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

양식 데이터 모델을 사용하면 적응형 양식을 서로 다른 데이터 소스에 연결할 수 있습니다. 예를 들어 AEM 사용자 프로필, RESTful 웹 서비스, SOAP 기반 웹 서비스, OData 서비스 및 관계형 데이터베이스가 있습니다. 양식 데이터 모델은 연결된 데이터 소스에서 사용할 수 있는 비즈니스 엔티티 및 서비스의 통합 데이터 표현 스키마입니다. 적응형 양식과 함께 양식 데이터 모델을 사용하여 연결된 데이터 소스를 검색, 업데이트, 삭제 및 추가할 수 있습니다.

목표:

* 웹 사이트의 데이터베이스 인스턴스 구성([!DNL MySQL] 데이터베이스) 데이터 소스
* 을 사용하여 양식 데이터 모델 만들기 [!DNL MySQL] 데이터 소스로 데이터베이스
* 양식 데이터 모델에 데이터 모델 개체 추가
* 양식 데이터 모델에 대한 읽기 및 쓰기 서비스 구성
* 테스트 데이터로 양식 데이터 모델 및 구성된 서비스 테스트

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 3단계: 적응형 양식 필드에 규칙 적용 {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

적응형 양식은 적응형 양식 개체에 대한 규칙을 작성하는 편집기를 제공합니다. 이러한 규칙은 양식의 사전 설정된 조건, 사용자 입력 및 사용자 작업을 기반으로 양식 개체에 대해 트리거할 작업을 정의합니다. 정확성을 보장하고 양식 채우기 경험을 빠르게 할 수 있습니다.

목표:

* 적응형 양식 필드에 규칙 만들기 및 적용
* 규칙을 사용하여 데이터 모델 서비스를 트리거하여 데이터를 데이터베이스로 업데이트

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 4단계: 적응형 양식 스타일 지정 {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

적응형 양식은 테마 및 [편집기](../../forms/using/themes.md) 적응형 양식의 테마를 만들기 위해 다음을 수행하십시오. 테마 에는 구성 요소 및 패널에 대한 스타일 지정 세부 사항이 포함되어 있으며 다른 양식에서 테마를 다시 사용할 수 있습니다. 스타일은 배경색, 상태 색상, 투명도, 정렬 및 크기와 같은 속성을 포함합니다. 양식에 테마를 적용하면 지정된 스타일이 양식의 해당 구성 요소에 반영됩니다. 적용형 양식은 양식에 대한 인라인 스타일링을 지원합니다.

목표:

* 즉시 사용 가능한 테마를 적응형 양식에 적용
* 테마 편집기를 사용하여 적응형 양식의 테마 만들기
* 사용자 정의 테마에 웹 글꼴 사용

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 5단계: 적응형 양식 게시 {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

적응형 양식을 독립형 양식(단일 페이지 애플리케이션)으로 게시하고 AEM에 포함할 수 있습니다 [사이트 페이지](/help/forms/using/embed-adaptive-form-aem-sites.md), 또는 AEM의 목록 [!DNL Site] 사용 [Forms 포털](../../forms/using/introduction-publishing-forms.md).

목표:

* 적응형 양식을 AEM 페이지로 게시
* AEM에 적응형 양식 포함 [!DNL Sites] 페이지
* 외부 웹 페이지에 적응형 양식 포함(AEM 외부에서 호스팅된 AEM이 아닌 웹 페이지)

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
