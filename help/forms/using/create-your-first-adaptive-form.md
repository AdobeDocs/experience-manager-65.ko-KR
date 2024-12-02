---
title: '자습서: 첫 번째 적응형 양식 만들기'
description: 비즈니스 클래스, 대화형 및 반응형 양식을 만드는 방법을 알아봅니다.
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 6%

---

# 자습서: 첫 번째 적응형 양식 만들기 {#tutorial-create-your-first-adaptive-form}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html) |
| AEM 6.5 | 이 문서 |


![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## 소개 {#introduction}

등록을 단순화하고 참여를 늘리며 반환 시간을 단축하는 모바일 친화적인 **양식 경험**&#x200B;을 찾고 계십니까? **적응형 양식**&#x200B;이 귀하에게 적합합니다. 적응형 양식은 모바일, 자동화 및 분석 친화적 양식 경험을 제공합니다. 반응형 및 대화형 양식을 손쉽게 제작하고, 자동화된 프로세스를 사용하여 관리 및 반복 작업을 줄이고, 데이터 분석을 사용하여 고객의 양식 사용 경험을 개선하고 개인화할 수 있습니다.

이 튜토리얼에서는 적응형 양식을 만들기 위한 전체적인 프레임워크를 제공합니다. 자습서는 사용 사례와 여러 안내서로 구성됩니다. 각 안내서는 이 자습서에서 만든 적응형 양식에 새로운 기능을 학습하고 추가하는 데 도움이 됩니다. 모든 안내서 다음에 작업 적응형 양식이 있습니다. 적응형 양식 만들기 안내서를 사용할 수 있습니다. 다음 안내서가 곧 제공될 예정입니다. 이 자습서를 마치면 다음을 수행할 수 있습니다.

* 적응형 양식 및 양식 데이터 모델 만들기
* 적응형 양식에 스타일을 지정합니다.
* 적응형 양식 규칙 편집기를 사용하여 비즈니스 규칙을 작성하십시오.
* 적응형 양식을 테스트하고 게시합니다.

![적응형 양식 워크플로 만들기](assets/create-daptive-form-workflow.png)

여정은 사용 사례 학습부터 시작합니다.

웹 사이트에서는 다양한 고객을 위한 다양한 제품을 제공합니다. 고객은 포털을 탐색하고 제품을 선택하고 주문합니다. 모든 고객은 계정을 만들고 배송 및 청구 주소를 제공합니다. 기존 고객인 Sara Rose는 자신의 배송 주소를 웹사이트에 추가하려고 합니다. 웹사이트는 배송 주소를 추가하고 업데이트할 수 있는 온라인 양식을 제공합니다.

웹 사이트는 AEM(Adobe Experience Manager)에서 실행되고 데이터 캡처 및 처리에 AEM [!DNL Forms]을(를) 사용합니다. 주소 추가 및 업데이트 양식은 적응형 양식입니다. 웹 사이트는 고객 세부 정보를 데이터베이스에 저장합니다. 주소 추가 및 업데이트 양식을 사용하여 사용 가능한 주소를 검색하고 표시합니다. 또한 적응형 양식을 사용하여 업데이트된 새 주소를 수락합니다.

### 전제 조건 {#prerequisite}

* [AEM 작성자 인스턴스 설정](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html#author-and-publish-installs)
* 작성자 인스턴스에 [AEM Forms 추가 기능](../../forms/using/installing-configuring-aem-forms-osgi.md)을(를) 설치합니다.
* 데이터베이스 공급자로부터 JDBC 데이터베이스 드라이버(JAR 파일)를 가져옵니다. 자습서의 예제는 [!DNL MySQL] 데이터베이스를 기반으로 하며 [!DNL Oracle's] [MySQL JDBC 데이터베이스 드라이버](https://dev.mysql.com/downloads/connector/j/5.1.html)를 사용합니다.

* 아래 필드가 표시된 고객 데이터를 포함하는 데이터베이스를 설정합니다. 적응형 양식을 만드는 데 데이터베이스가 반드시 필요한 것은 아닙니다. 이 자습서에서는 데이터베이스를 사용하여 AEM [!DNL Forms]의 양식 데이터 모델 및 지속성 기능을 표시합니다.

![adaptiveformdata](assets/adaptiveformdata.png)

## 1단계: 적응형 양식 만들기 {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

적응형 양식은 새로운 세대의 매력적인 반응형 동적 적응형 양식입니다. 적응형 양식을 사용하여 개인화되고 타겟팅된 경험을 제공할 수 있습니다. AEM [!DNL Forms]에서는 적응형 양식을 만들 수 있는 드래그 앤 드롭 WYSIWYG 편집기를 제공합니다. 적응형 양식에 대한 자세한 내용은 [적응형 양식 작성 소개](../../forms/using/introduction-forms-authoring.md)를 참조하십시오.

목표:

* 고객이 배송 주소를 추가할 수 있도록 하는 적응형 양식을 만듭니다.
* 적응형 양식의 레이아웃 필드를 통해 고객의 정보를 표시하고 수락합니다.
* 제출 액션을 만들어 양식 콘텐츠가 포함된 이메일을 보냅니다.
* 적응형 양식을 미리 보고 제출합니다.

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## 2단계: 양식 데이터 모델 만들기 {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

양식 데이터 모델을 사용하면 적응형 양식을 개별 데이터 소스에 연결할 수 있습니다. 예를 들어 AEM 사용자 프로필, RESTful 웹 서비스, SOAP 기반 웹 서비스, OData 서비스 및 관계형 데이터베이스가 있습니다. 양식 데이터 모델은 연결된 데이터 소스에서 사용할 수 있는 비즈니스 엔터티 및 서비스의 통합 데이터 표시 스키마입니다. 양식 데이터 모델을 적응형 양식과 함께 사용하여 데이터를 검색, 업데이트, 삭제 및 연결된 데이터 소스에 추가할 수 있습니다.

목표:

* 웹 사이트의 데이터베이스 인스턴스([!DNL MySQL] 데이터베이스)를 데이터 원본으로 구성합니다.
* [!DNL MySQL] 데이터베이스를 데이터 원본으로 사용하여 양식 데이터 모델을 만듭니다.
* 데이터 모델을 형성할 수 있도록 데이터 모델 개체를 추가합니다.
* 양식 데이터 모델에 대한 읽기 및 쓰기 서비스를 구성합니다.
* 테스트 데이터를 사용하여 양식 데이터 모델 및 구성된 서비스를 테스트합니다.

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 3단계: 적응형 양식 필드에 규칙 적용 {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

적응형 양식은 적응형 양식 오브젝트에 대한 규칙을 작성할 편집기를 제공합니다. 이러한 규칙은 양식에 대한 사전 설정 조건, 사용자 입력 및 사용자 작업을 기반으로 양식 개체에서 트리거하는 작업을 정의합니다. 정확도를 보장하고 양식 작성 시간을 단축하는 데 도움이 됩니다.

목표:

* 적응형 양식 필드에 규칙을 만들어 적용합니다.
* 규칙을 사용하여 양식 데이터 모델 서비스를 트리거하여 데이터베이스에 데이터를 업데이트합니다.

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 4단계: 적응형 양식 스타일 지정 {#step-style-your-adaptive-form}

![적응형 양식 스타일 지정](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

적응형 양식에서는 테마와 적응형 양식용 테마를 만들 수 있는 [편집기](../../forms/using/themes.md)를 제공합니다. 테마에는 구성 요소 및 패널의 스타일 지정 세부 정보가 포함되어 있으며 다른 양식에서 테마를 다시 사용할 수 있습니다. 스타일에는 배경색, 상태 색상, 투명도, 정렬과 크기와 같은 속성이 포함됩니다. 테마를 양식에 적용하면 지정된 스타일이 양식의 해당 구성 요소를 반영합니다. 적응형 양식은 양식별 스타일에 대한 인라인 스타일링도 지원합니다.

목표:

* 적응형 양식에 즉시 사용 가능한 테마를 적용합니다.
* 테마 편집기를 사용하여 적응형 양식에 대한 테마를 만듭니다.
* 사용자 지정 테마에서 Web Fonts을 사용합니다.

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 5단계: 적응형 양식 Publish {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

[Forms 포털](../../forms/using/introduction-publishing-forms.md)을 사용하여 적응형 양식을 독립 실행형 양식(단일 페이지 애플리케이션)으로 게시하거나, AEM [Sites 페이지](/help/forms/using/embed-adaptive-form-aem-sites.md)에 포함하거나, AEM [!DNL Site]에 나열할 수 있습니다.

목표:

* 적응형 양식을 AEM 페이지로 Publish.
* AEM [!DNL Sites] 페이지에 적응형 양식을 포함하십시오.
* 적응형 양식을 외부 웹 페이지(AEM 외부에 호스트된 비 AEM 웹 페이지)에 임베드합니다.

[![안내서 참조](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
