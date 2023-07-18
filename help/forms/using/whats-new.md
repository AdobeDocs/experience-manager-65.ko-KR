---
title: 새로운 기능 요약 | AEM 6.5 Forms
seo-title: New features summary | AEM 6.5 Forms
description: 세계에서 가장 진보된 디지털 경험 관리 솔루션의 양식 및 문서에 대한 최신 기능과 개선 사항입니다.
seo-description: Latest features and improvements to forms and documents of world’s most advanced digital experience management solution.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 1%

---

# 새로운 기능 요약 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## 거래 보고서 {#transaction-reports}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/latest-innovations.html) |
| AEM 6.5 | 이 문서 |


트랜잭션 보고서를 사용하면 제출된 양식, 처리된 문서 및 렌더링된 문서의 수를 캡처하고 추적할 수 있습니다. 이러한 거래를 추적하는 목적은 제품 사용과 하드웨어 및 소프트웨어에 대한 투자 재조정에 대한 정보에 입각한 결정을 내리는 것입니다. 트랜잭션의 몇 가지 예는 다음과 같습니다.

* 적응형 양식, HTML5 양식 또는 양식 세트 제출
* 대화형 통신의 인쇄 또는 웹 버전 렌디션
* 한 파일 형식에서 다른 파일 형식으로 문서 변환

트랜잭션 보고서 구성 및 사용에 대한 자세한 내용은 [거래 보고서 개요](../../forms/using/transaction-reports-overview.md).

![샘플 거래 보고서](assets/surface_transaction_reporting.png)

## 대화형 통신 {#interactive-communications}

**데이터 표시 패턴 정의**

이제 대화형 통신 작성자가 다음을 정의할 수 있습니다. [데이터 표시 패턴](create-interactive-communication.md#datadisplaypatterns) 필드, 변수 및 양식 데이터 모델 요소의 경우. 예: 날짜, 통화 또는 전화 형식

**새로운 유형의 차트 사용**

이제 를 추가할 수 있습니다. [여러 시리즈가 포함된 Quadrant 차트 및 차트](../../forms/using/chart-component-interactive-communications.md) (대화형 통신).

**테이블의 열 정렬**

이제 다음을 수행할 수 있습니다. [테이블의 열 정렬](../../forms/using/create-interactive-communication.md#sortcolumns) ( 대화형 통신). 테이블 열을 정적 텍스트 또는 데이터 모델 개체와 바인딩하고 정렬할 수 있습니다.

**웹 채널에서 새 구성 요소 사용**

이제 Button 및 Separator 구성 요소를 웹 채널에 추가할 수 있습니다. 자세한 내용은 [웹 채널에 Button 구성 요소 추가](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) 및 [웹 채널의 분리자 구성 요소](../../forms/using/create-interactive-communication.md#separatorcomponent).

**구성 요소 크기를 조정하는 레이아웃 모드**

이제 다음으로 전환할 수 있습니다. [레이아웃 모드](../../forms/using/resize-using-layout-mode.md) WYSIWYG 인터페이스를 사용하여 웹 채널에서 구성 요소의 크기를 조정할 수 있습니다.

**유용성 개선**

대화형 통신 작성자는 이제 서신을 작성하는 동안 사용하기 쉬운 다양한 작업을 활용할 수 있습니다. 작업 목록에는 다음이 포함됩니다.

* [인쇄 및 웹 채널에서 실행 취소-재실행 작업 수행](../../forms/using/create-interactive-communication.md#undoredoactions)
* [@ 기호를 사용하여 문서 조각에 변수 추가](../../forms/using/texts-interactive-communications.md#searchvariables)
* [@ 기호를 사용하여 문서 조각에 데이터 모델 요소 추가](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [기존 대화형 통신에 웹 채널 삭제 또는 추가](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [드래그 앤 드롭 작업을 사용하여 필드 및 변수와 데이터 소스 요소 바인딩](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [대화형 통신을 작성하는 동안 바인딩되지 않은 필드 및 변수 강조 표시](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [웹 채널에서 상속된 구성 요소에 대해 복사, 그룹 등의 추가 작업을 수행합니다](../../forms/using/create-interactive-communication.md#componenttoolbar)

**동기화 프로세스 개선**

인쇄 채널을 사용하여 자동 생성된 웹 채널 레이아웃에는 몇 가지 개선 사항이 있습니다.

![대화형 통신 차트](assets/interactive-communication-charts.png)

## 적응형 양식 {#adaptive-forms}

### 적응형 Forms에서 Adobe Sign 클라우드 기반 디지털 서명 사용 {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[클라우드 기반 디지털 서명](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 또는 원격 서명은 데스크탑, 모바일 및 웹에서 작동하는 새로운 세대의 디지털 서명으로, 서명자 인증을 위한 최고 수준의 규정 준수 및 보증을 충족합니다. 이제 다음을 수행할 수 있습니다. [적응형 양식에 서명](../../forms/using/working-with-adobe-sign.md) (클라우드 기반 디지털 서명 사용)

#### AEM Sites 단일 페이지 애플리케이션에 적응형 양식 또는 대화형 통신 포함 {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms을 사용하면 다음 작업을 수행할 수 있습니다. [적응형 양식을 매끄럽게 임베드](../../forms/using/embed-adaptive-form-aem-sites-spa.md) 또는 AEM Sites 단일 페이지 애플리케이션(SPA)의 대화형 통신 임베드된 적응형 양식 및 대화형 커뮤니케이션은 완전히 기능하며 사용자는 페이지를 종료하지 않고 양식을 작성하고 제출할 수 있습니다. 사용자가 웹 페이지의 다른 요소 컨텍스트에 남아 있으면서 적응형 양식 또는 대화형 통신과 동시에 상호 작용하는 데 도움이 됩니다.

#### 적응형 양식 표의 열 정렬 {#sort-columns-of-adaptive-form-tables}

다음을 수행할 수 있습니다. [적응형 양식 표의 모든 열 정렬](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) 오름차순 또는 내림차순으로 정렬합니다. 정적 텍스트, 데이터 모델 개체 속성 또는 정적 텍스트와 데이터 모델 개체 속성의 조합으로 테이블 열에 정렬을 적용할 수 있습니다.

#### 적응형 Forms 템플릿의 가용성을 특정 경로로 제한 {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

적응형 양식에 cq:allowedPaths 속성에 대한 지원이 추가되었습니다. 속성 [적응형 Forms 템플릿의 가용성을 특정 경로로 제한합니다](creating-adaptive-form.md#adaptive-form-templates).

#### 적응형 양식에 동적으로 확인란 추가 {#add-check-boxes-to-the-adaptive-form-dynamically}

이제 규칙을 정의하여 다음을 수행할 수 있습니다. [적응형 양식에 동적으로 확인란 추가](../../forms/using/rule-editor.md#setpropertyrule) 사용자 지정 함수, 양식 개체 또는 개체 속성을 기반으로 합니다.

## AEM 워크플로우 {#aem-workflows}

### AEM 워크플로우에서 변수 사용 {#use-variables-in-aem-workflows}

변수를 사용하면 런타임 시 워크플로 단계 간에 메타데이터를 유지하고 전달할 수 있습니다. 다양한 유형의 데이터를 저장하기 위해 다양한 유형의 변수를 만들 수 있습니다. 예: 정수, 문자열, 문서 또는 양식 데이터 모델 인스턴스 일반적으로 변수 또는 변수 컬렉션은 보유하고 있는 값을 기반으로 결정을 내려야 하거나 나중에 프로세스에서 필요한 정보를 저장해야 할 때 사용합니다.

변수는 의 확장입니다. [메타데이터 맵](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 이전 버전에서 사용할 수 있는 인터페이스입니다. 메타데이터 값을 검색하고 업데이트하는 데 사용되는 사용자 지정 ECMAScript 코드를 개발하는 데 드는 시간을 절약하는 데 도움이 됩니다. 메타데이터를 조작하기 위해 MetaDataMap 인터페이스와 ECMAScript 코드를 계속 사용합니다. MetaDataMap 및 ECMAScript에 대해 변수를 사용하면 다음과 같은 몇 가지 이점이 있습니다.

* 사용자 지정 코드에 의존하지 않고 워크플로우 전반에 걸쳐 변수에 저장된 값을 동적으로 저장, 업데이트 및 사용
* 제출된 양식의 양식 데이터 모델 및 데이터 파일(XML/JSON )에 직접 값을 검색하고 업데이트합니다
* 전체 문서를 변수에 저장하여 문서 처리 수행

이동 단계 또는 분할 단계 및 모든 AEM Forms 워크플로 단계는 변수를 지원합니다. MetaDataMap 인터페이스를 사용하여 변수에 대한 기본 지원이 없는 워크플로 단계의 변수에 액세스할 수 있습니다. 자세한 내용은 [AEM 워크플로의 변수](../../forms/using/variable-in-aem-workflows.md).

![워크플로우에서에 대한 변수 설정](assets/variable.png)

#### 다른 적응형 Forms과 함께 워크플로우 사용  {#use-a-workflow-with-different-adaptive-forms}

다음을 수행할 수 있습니다. [할당 작업에 대한 적응형 양식 지정](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) 런타임에 양식 중심 워크플로의 기록 문서 단계. 이를 통해 워크플로우가 다양한 적응형 Forms에서 작업할 수 있습니다. 워크플로우를 디자인하는 동안 적응형 양식을 선택하는 방법을 결정할 수 있습니다. 적응형 양식은 절대 경로에 위치하거나, 워크플로우에 페이로드로 제출하거나, 변수를 사용하여 계산된 경로에서 사용할 수 있습니다.

#### 양식 중심 워크플로우 단계의 향상된 로깅 기능 사용 {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

양식 중심 워크플로우 단계의 로깅 기능은 표준화되었습니다. 이제 모든 양식 중심의 워크플로우 단계에서 유사하게 표준화된 로그가 생성됩니다. 디버깅 속도를 개선하는 데 도움이 됩니다.

## 데이터 통합 {#data-integration}

이제 다음을 수행할 수 있습니다.

* [입력 데이터 유효성 검사](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) 제약 조건 목록을 기반으로 합니다. 유효한 데이터만 데이터 소스에 제출되도록 합니다.
* [기본 끝점 재정의](../../forms/using/configure-data-sources.md#configure-soap-web-services) wsdl(웹 서비스 설명 언어) 파일에서 정의됩니다.

* [기본값 재정의](../../forms/using/configure-data-sources.md#configure-restful-web-services) [스키마, 호스트 및 기본 경로](../../forms/using/configure-data-sources.md#configure-restful-web-services) Swagger 정의 파일에 정의되어 있습니다.

## 플랫폼 및 보안 업데이트 {#platform-and-security-updates}

### 주요 플랫폼 업데이트 {#major-platform-updates}

AEM Forms은 지원되는 운영 체제, 애플리케이션 서버, 데이터베이스, 데이터베이스 드라이버, JDK, LDAP 서버 및 이메일 서버의 조합을 사용하여 설정할 수 있습니다. 다음은 의 주요 변경 사항입니다 [지원되는 플랫폼](../../forms/using/aem-forms-jee-supported-platforms.md):

<table>
 <tbody>
  <tr>
   <td>구성 요소</td>
   <td>지원 제거됨</td>
  </tr>
  <tr>
   <td>운영 체제</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>애플리케이션 서버<br /> </td>
   <td>
    <ul>
    <li>WebSphere Liberty 프로필</li>
    <li>Oracle WebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>데이터베이스</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>ORACLE RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP 서버</td>
   <td>
    <ul>
     <li>Microsoft Active Directory</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>이메일 서버</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>커넥터</td>
   <td>
    <ul>
     <li>Microsoft Sharepoint 2013용 커넥터</li>
     <li>EMC Documentum 7.0용 커넥터</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms 앱<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1 지원</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42; 다른 플랫폼으로 마이그레이션하는 방법에 대한 자세한 내용은 Adobe 지원 센터에 문의하십시오

#### 새로운 HTML5 기반 UI {#new-html-based-uis}

Adobe Flash Player의 계획된 EOL 및 Flash 기반 컨텐츠를 개방형 표준으로 마이그레이션하는 전반적인 방향에 따라 AEM 6.5 Forms은 JEE 관리 콘솔의 AEM Forms에 대한 상태 모니터, 프로세스 관리, Reader 확장 및 범주 관리 UI의 Flash 기반 UI를 HTML5 기반 UI로 대체했습니다.

#### 보안 개선 사항 {#security-improvements}

* JEE 관리 콘솔 UI의 AEM 6.5 Forms은 이제 Apache Struts 2.5를 기반으로 합니다.
* AEM 6.5 Forms은 이제 jQuery를 3.2.1 및 jQuery UI 1.12.1에 사용합니다. 다음을 참조하십시오. [업그레이드 설명서](/help/forms/home.md) 를 참조하십시오.

#### 액세스 가능성 향상 {#accessibility-improvements}

AEM 6.5 Forms은 AEM Forms 작업 영역의 접근성을 개선했습니다.
