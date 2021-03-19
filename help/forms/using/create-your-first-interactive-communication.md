---
title: 자습서 - 간단한 대화형 커뮤니케이션 만들기
seo-title: 간단한 인터랙티브 커뮤니케이션 제작
description: 간단한 인터랙티브 커뮤니케이션 제작
seo-description: 간단한 인터랙티브 커뮤니케이션 제작
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
feature: 대화형 통신
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# 자습서:첫 번째 대화형 통신 만들기 {#tutorial-create-your-first-interactive-communication}

간단한 인터랙티브 커뮤니케이션 제작

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Interactive Communications는 비즈니스 서신, 문서, 명세서, 마케팅 이메일, 청구서 및 환영 키트와 같은 안전하고 개인화된 인터랙티브한 통신의 작성, 조합 및 전달을 중앙 집중화하고 관리합니다. 인터랙티브 커뮤니케이션은인쇄 및 웹. 인쇄 채널은 PDF 및 종이 커뮤니케이션을 만드는 데 사용되는 반면 웹 채널은 온라인 경험을 전달하는 데 사용됩니다.

이 자습서는 인터랙티브 커뮤니케이션을 만들기 위한 엔드 투 엔드 프레임워크를 제공합니다. 이 자습서는 사용 사례와 여러 안내선으로 구성됩니다. 각 안내서는 인터랙티브 커뮤니케이션을 만들기 위한 구성 요소로 사용되는 기능을 만드는 데 도움이 됩니다.

다음 이미지는 대화형 통신을 만드는 데 필요한 구성 요소를 보여 줍니다.

![workflow](assets/workflow.gif)

이 튜토리얼의 끝에서 다음 작업을 수행할 수 있습니다.

* 구성 요소(양식 데이터 모델, 문서 조각 및 템플릿) 만들기
* 대화형 통신 만들기
* 인터랙티브 커뮤니케이션 테스트 및 게시

## 사용 사례 {#use-case}

여정은 사용 사례를 배움으로써 시작됩니다.

통신 사업자는 고객에게 이메일로 매월 청구서를 보낸다. 그 법안은 상호 작용 통신이다. 이메일에는 다음이 포함됩니다.

* 이 자습서에서 인쇄 채널이라고 하는 암호로 보호된 PDF입니다. 고객 세부 사항, 청구 세부 사항, 비용 요약, 요금 지불 편리한 모드 및 사용 세부 사항이 포함되어 있습니다.
* 이 자습서에서 웹 채널이라고 하는 BOM의 웹 버전에 대한 링크입니다. PDF 버전에 포함된 세부 사항 외에도 웹 버전의 이 청구서는 Adobe Target을 기반으로 사용 세부 사항과 개인화된 제안을 그래픽으로 표시합니다. 웹 버전에는 온라인 결제 양식도 포함되어 있습니다. IC를 종료하지 않고도 온라인 결제를 할 수 있습니다.
* 온라인 스토리지, 음악 구독, 주문형 비디오 구독 등 부가가치 서비스에 대한 링크입니다.

## 전제 조건 {#prerequisites}

* AEM 작성자 인스턴스를 설정합니다.
* 작성자 인스턴스에 [AEM Forms add-on](/help/forms/using/installing-configuring-aem-forms-osgi.md)을(를) 설치합니다.
* MYSQL 데이터베이스 설정
* 데이터베이스 공급자로부터 JDBC 데이터베이스 드라이버(JAR 파일)를 가져옵니다. 자습서의 예는 MySQL 데이터베이스를 기반으로 하며 Oracle의 [MySQL JDBC 데이터베이스 드라이버](https://dev.mysql.com/downloads/connector/j/5.1.html)를 사용합니다.

## 1단계:대화형 통신 계획 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

대화형 통신을 계획하는 첫 번째 단계는 대화형 커뮤니케이션의 내용을 마무리하는 것입니다. 컨텐츠가 완료되면 분석을 통해 인터랙티브 커뮤니케이션을 만드는 데 필요한 다양한 자산 유형을 식별해야 합니다.

**목표:**

다음과 같은 데이터 입력 모드를 사용하여 인터랙티브 커뮤니케이션의 구조를 만들려면:

* 정적 텍스트
* 양식 데이터 모델
* 에이전트 UI
* 조건부 데이터
* 이미지

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/planning-interactive-communications.md)

## 2단계:양식 데이터 모델 {#step-create-form-data-model} 만들기

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

양식 데이터 모델을 사용하면 인터랙티브 커뮤니케이션을 서로 다른 데이터 소스에 연결할 수 있습니다. 예를 들어 AEM 사용자 프로필, RESTful 웹 서비스, SOAP 기반 웹 서비스, OData 서비스 및 관계형 데이터베이스를 들 수 있습니다. 양식 데이터 모델은 연결된 데이터 소스에서 사용할 수 있는 비즈니스 조직 및 서비스의 통합된 데이터 표현 스키마입니다. 대화형 통신과 함께 양식 데이터 모델을 사용하여 연결된 데이터 소스에서 데이터를 검색할 수 있습니다. 양식 데이터 모델에 대한 자세한 내용은 [AEM Forms 데이터 통합](/help/forms/using/data-integration.md)을 참조하십시오.

**목표:**

* 데이터베이스 인스턴스(MySQL 데이터베이스)를 데이터 소스로 구성
* MySQL 데이터베이스를 데이터 소스로 사용하여 양식 데이터 모델 만들기
* 양식 데이터 모델에 데이터 모델 개체 추가
* 양식 데이터 모델에 대한 읽기 및 쓰기 서비스 구성
* 데이터 모델 개체 간 연결 만들기
* 자동으로 생성된 샘플 데이터 보기
* 샘플 데이터 편집
* 테스트 데이터를 사용하여 양식 데이터 모델 및 구성된 서비스 테스트

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-form-data-model0.md)

## 3단계:문서 조각 만들기 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

문서 조각은 인터랙티브 커뮤니케이션을 구성하는 데 사용되는 통신 구성 요소의 재사용 가능한 구성 요소입니다. 문서 조각은 다음과 같은 유형입니다.텍스트, 목록 및 조건을 참조하십시오.

**목표:**

* 문서 조각 만들기
* 변수 만들기
* 규칙 만들기 및 적용

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-document-fragments.md)

## 4단계:템플릿 만들기 {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

대화형 통신을 만들려면 인쇄 및 웹 채널용 AEM 서버에서 사용할 수 있는 템플릿이 있어야 합니다.

인쇄 채널의 템플릿은 Adobe Forms Designer에서 만들고 AEM 서버에 업로드됩니다. 그런 다음 대화형 통신을 만드는 동안 이러한 템플릿을 사용할 수 있습니다.

웹 채널의 템플릿은 AEM에서 만듭니다. 템플릿 작성자 및 관리자는 웹 템플릿을 만들고 편집하고 활성화할 수 있습니다. 만들어진 후 활성화하면 이러한 템플릿을 대화형 통신을 만드는 동안 사용할 수 있습니다.

**목표:**

* Adobe Forms Designer를 사용하여 인쇄 채널용 XDP 템플릿 만들기
* AEM Forms 서버에 XDP 템플릿 업로드
* 웹 채널에 대한 템플릿 만들기 및 활성화

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-templates-print-web.md)

## 5단계:대화형 통신 만들기 {#step-create-an-interactive-communication}

![09style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

양식 데이터 모델, 문서 조각 및 웹 버전에 대한 템플릿과 같은 구성 요소를 모두 만들고 나면 대화형 통신을 만들기 시작할 수 있습니다.

인터랙티브 커뮤니케이션은 다음 두 채널을 통해 전달할 수 있습니다.인쇄 및 웹. 또한 인쇄 채널을 마스터로 사용하여 대화형 통신을 만들 수도 있습니다. 웹 채널에 대한 마스터 옵션으로 인쇄하면 웹 채널의 컨텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생됩니다.

**목표:**

* 인쇄 채널용 대화형 통신 만들기
* 웹 채널을 위한 대화형 통신 만들기
* 인쇄물로 인쇄 및 웹 인터랙티브 커뮤니케이션 기본 제작
* 웹 버전의 인터랙티브 커뮤니케이션에서 동적 표 만들기
* 웹 버전의 인터랙티브 커뮤니케이션으로 차트 만들기
* 웹 버전의 인터랙티브 커뮤니케이션에서 하이퍼링크 만들기

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-interactive-communication0.md)

## 6단계:대화형 통신 테스트 {#step-test-your-interactive-communication}

![11 test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

인터랙티브 커뮤니케이션을 만든 후에는 변경 내용을 모두 테스트하는 것이 중요합니다. 인터랙티브 커뮤니케이션의 모든 필드를 테스트하는 것은 지루합니다. AEM Forms은 웹 브라우저에서 대화형 통신 테스트를 자동화하는 SDK(Calvin SDK)를 제공합니다.

**목표:**

* 테스트 세트 만들기
* 테스트 케이스 만들기
* 테스트 케이스 실행

## 7단계:대화형 통신 게시 {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

인쇄 및 웹 채널을 사용하여 인터랙티브 커뮤니케이션을 만들고 테스트하고 나면 이러한 자산을 게시할 수 있습니다. 이 자습서에서 설명하는 사용 사례는 이러한 자산을 이메일 클라이언트와 통합하는 데 중점을 둡니다. 이메일 클라이언트는 Interactive Communications를 여러 이메일 주소로 전송하는 다리 역할을 합니다.

**목표:**

* 고객에게 커뮤니케이션을 보낼 수 있도록 이메일 클라이언트와 인터랙티브 커뮤니케이션 통합
* PDF 문서를 첨부 파일로 포함(인쇄 채널에서 만든 대화형 통신)
* 웹 버전의 대화형 통신에 대한 링크 포함

