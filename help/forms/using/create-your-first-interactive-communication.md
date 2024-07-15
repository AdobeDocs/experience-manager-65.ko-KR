---
title: 자습서 - 첫 번째 대화형 통신 만들기
description: 첫 번째 대화형 커뮤니케이션을 만드는 방법을 알아봅니다.
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
feature: Interactive Communication
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# 자습서: 첫 번째 대화형 통신 만들기 {#tutorial-create-your-first-interactive-communication}

첫 번째 대화형 커뮤니케이션을 만드는 방법을 알아봅니다.

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Interactive Communications는 비즈니스 서신, 문서, 명세서, 마케팅 메일, 청구서 및 환영 키트와 같은 안전하고 개인화된 인터랙티브한 통신의 작성, 수집 및 전달을 중앙 집중화하여 관리합니다. 대화형 커뮤니케이션은 인쇄와 웹의 두 가지 채널을 사용하여 제공할 수 있습니다. 인쇄 채널은 PDF 및 종이 문서 통신을 만드는 데 사용되며 웹 채널은 온라인 경험을 전달하는 데 사용됩니다.

이 자습서에서는 대화형 통신을 만드는 통합 프레임워크를 제공합니다. 자습서는 사용 사례와 여러 안내서로 구성됩니다. 각 안내서는 대화형 커뮤니케이션을 만들기 위한 빌딩 블록으로 사용되는 기능을 만드는 데 도움이 됩니다.

다음 이미지는 대화형 통신을 만드는 데 필요한 구성 요소를 보여 줍니다.

![워크플로](assets/workflow.gif)

이 자습서를 마치면 다음을 수행할 수 있습니다.

* 빌딩 블록 작성(양식 데이터 모델, 문서 단편 및 템플릿)
* 대화형 통신 만들기
* 대화형 통신 테스트 및 게시

## 사용 사례 {#use-case}

여정은 사용 사례 학습부터 시작합니다.

통신사는 매달 요금을 이메일로 고객들에게 보낸다. 그 청구서는 쌍방향 통신이다. 이메일에는 다음이 포함됩니다.

* 암호로 보호된 PDF. 이 자습서에서는 인쇄 채널이라고도 합니다. 고객 세부 정보, 청구서 세부 정보, 요금 요약, 청구서 결제 시 편리한 모드, 사용 세부 정보 등이 포함됩니다.
* 이 자습서에서 웹 채널이라고 하는 BOM의 웹 버전에 대한 링크입니다. 청구서의 웹 버전은 PDF 버전에서 다루는 세부 정보 외에도 Adobe Target을 기반으로 하는 사용 세부 정보 및 개인화된 오퍼를 그래픽으로 표시합니다. 웹 버전에는 온라인 결제 양식도 포함되어 있습니다. IC를 벗어나지 않고도 온라인 결제가 가능하도록 돕는다.
* 온라인 스토리지, 음악 구독 및 온디맨드 비디오 구독과 같은 부가 가치 서비스에 대한 링크.

## 사전 요구 사항 {#prerequisites}

* AEM 작성자 인스턴스를 설정합니다.
* 작성자 인스턴스에 [AEM Forms 추가 기능](/help/forms/using/installing-configuring-aem-forms-osgi.md) 설치
* MYSQL 데이터베이스 설정
* 데이터베이스 공급자로부터 JDBC 데이터베이스 드라이버(JAR 파일)를 가져옵니다. 자습서의 예는 MySQL 데이터베이스를 기반으로 하며 Oracle의 [MySQL JDBC 데이터베이스 드라이버](https://dev.mysql.com/downloads/connector/j/5.1.html)를 사용합니다.

## 1단계: 대화형 통신 계획 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

대화형 통신을 계획하는 첫 번째 단계는 대화형 통신의 내용을 완료하는 것입니다. 콘텐츠가 완료되면 이를 분석하여 대화형 커뮤니케이션을 만드는 데 필요한 다양한 에셋 유형을 식별해야 합니다.

**목표:**

다음 데이터 입력 모드를 사용하여 대화형 커뮤니케이션에 대한 구조를 생성하려면 다음을 수행합니다.

* 정적 텍스트
* 양식 데이터 모델
* 에이전트 UI
* 조건부 데이터
* 이미지

[](/help/forms/using/planning-interactive-communications.md)

## 2단계: 양식 데이터 모델 만들기 {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

양식 데이터 모델을 사용하면 대화형 통신을 개별 데이터 소스에 연결할 수 있습니다. 예를 들어 AEM 사용자 프로필, RESTful 웹 서비스, SOAP 기반 웹 서비스, OData 서비스 및 관계형 데이터베이스가 있습니다. 양식 데이터 모델은 연결된 데이터 소스에서 사용할 수 있는 비즈니스 엔터티 및 서비스의 통합 데이터 표시 스키마입니다. 양식 데이터 모델을 대화형 통신과 함께 사용하여 연결된 데이터 소스에서 데이터를 검색할 수 있습니다. 양식 데이터 모델에 대한 자세한 내용은 [AEM Forms 데이터 통합](/help/forms/using/data-integration.md)을 참조하십시오.

**목표:**

* 데이터베이스 인스턴스(MySQL 데이터베이스)를 데이터 소스로 구성
* MySQL 데이터베이스를 데이터 소스로 사용하여 양식 데이터 모델 만들기
* 양식 데이터 모델에 데이터 모델 개체 추가
* 양식 데이터 모델에 대한 읽기 및 쓰기 서비스 구성
* 데이터 모델 개체 간 연결 만들기
* 자동 생성된 샘플 데이터 보기
* 샘플 데이터 편집
* 테스트 데이터를 사용하여 양식 데이터 모델 및 구성된 서비스 테스트

[](/help/forms/using/create-form-data-model0.md)

## 3단계: 문서 단편 만들기 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

문서 조각은 대화형 통신을 구성하는 데 사용되는 서신의 재사용 가능한 구성 요소입니다. 문서 조각은 텍스트, 목록 및 조건 유형입니다.

**목표:**

* 문서 단편 만들기
* 변수 만들기
* 규칙 만들기 및 적용

[](/help/forms/using/create-document-fragments.md)

## 4단계: 템플릿 만들기 {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

대화형 통신을 만들려면 인쇄 및 웹 채널에 대해 AEM 서버에서 사용할 수 있는 템플릿이 있어야 합니다.

인쇄 채널의 템플릿은 Forms Designer Adobe에서 만들어 AEM 서버에 업로드됩니다. 그런 다음 대화형 통신을 만드는 동안 이러한 템플릿을 사용할 수 있습니다.

웹 채널에 대한 템플릿은 AEM에서 만들어집니다. 템플릿 작성자 및 관리자는 웹 템플릿을 만들고 편집하고 활성화할 수 있습니다. 이러한 템플릿을 만들고 활성화하면 대화형 통신을 만드는 동안 사용할 수 있습니다.

**목표:**

* Forms Designer Adobe을 사용하여 인쇄 채널용 XDP 템플릿 만들기
* AEM Forms 서버에 XDP 템플릿 업로드
* 웹 채널에 대한 템플릿 만들기 및 활성화

[](/help/forms/using/create-templates-print-web.md)

## 5단계: 대화형 통신 만들기 {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

양식 데이터 모델, 문서 단편 및 웹 버전에 대한 템플릿과 같은 모든 구성 요소를 만들면 대화형 커뮤니케이션을 만들 수 있습니다.

대화형 커뮤니케이션은 인쇄와 웹의 두 가지 채널을 통해 전달될 수 있습니다. 또한 인쇄 채널을 마스터로 하는 대화형 통신을 만들 수도 있습니다. 웹 채널에 대한 마스터 옵션으로 인쇄를 사용하면 웹 채널의 콘텐츠, 상속 및 데이터 바인딩이 인쇄 채널에서 파생됩니다.

**목표:**

* 인쇄 채널용 대화형 통신 만들기
* 웹 채널용 대화형 통신 만들기
* 인쇄를 기본으로 사용하여 인쇄 및 웹 대화형 통신 만들기
* 대화형 통신의 웹 버전에서 동적 테이블 만들기
* 대화형 통신의 웹 버전에서 차트 만들기
* 대화형 통신의 웹 버전에서 하이퍼링크 만들기

[](/help/forms/using/create-interactive-communication0.md)

## 6단계: 대화형 통신 Publish {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

인쇄 및 웹 채널을 사용하여 대화형 커뮤니케이션을 만들고 테스트하면 이러한 에셋을 게시할 수 있습니다. 이 자습서에 설명된 사용 사례는 이러한 에셋을 이메일 클라이언트와 통합하는 데 중점을 둡니다. 이메일 클라이언트는 대화형 커뮤니케이션을 여러 이메일 주소로 전송하는 브리지 역할을 합니다.

**목표:**

* 대화형 커뮤니케이션을 이메일 클라이언트와 통합하여 고객에게 커뮤니케이션을 보낼 수 있습니다.
* PDF 문서를 첨부 파일로 포함(인쇄 채널에서 생성된 대화형 통신)
* 대화형 통신의 웹 버전에 대한 링크 포함
