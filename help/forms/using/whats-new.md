---
title: 새로운 기능 요약 | AEM 6.5 Forms
seo-title: 새로운 기능 요약 | AEM 6.5 Forms
description: 세계 최고의 고급 디지털 경험 관리 솔루션의 양식 및 문서에 대한 최신 기능과 향상된 기능
seo-description: 세계 최고의 고급 디지털 경험 관리 솔루션의 양식 및 문서에 대한 최신 기능과 향상된 기능
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
translation-type: tm+mt
source-git-commit: a417094c1d7b28ec54a6e84303d7a9747bb0c510
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 1%

---


# 새로운 기능 요약 | AEM 6.5 Forms{#new-features-summary-aem-forms}

## 트랜잭션 보고서 {#transaction-reports}

거래 보고서를 사용하면 제출된 양식, 처리된 문서 및 렌더링된 문서의 수를 캡처하고 추적할 수 있습니다. 이러한 거래를 추적하는 목적은 제품 사용에 대해 현명한 의사 결정을 내리고 하드웨어 및 소프트웨어에 대한 투자를 재조정하는 것입니다. 거래의 일부 예는 다음과 같습니다.

* 적응형 양식, HTML5 양식 또는 양식 세트 제출
* 인터랙티브한 커뮤니케이션의 인쇄 또는 웹 버전 변환
* 한 파일 형식에서 다른 파일 형식으로 문서 변환

거래 보고서 구성 및 사용에 대한 자세한 내용은 [거래 보고서 개요](../../forms/using/transaction-reports-overview.md)를 참조하십시오.

![샘플 트랜잭션 보고서](assets/surface_transaction_reporting.png)

## 대화형 통신 {#interactive-communications}

**데이터 표시 패턴 정의**

이제 대화형 통신 작성자는 필드, 변수 및 양식 데이터 모델 요소에 대해 [데이터 표시 패턴](create-interactive-communication.md#datadisplaypatterns)을 정의할 수 있습니다. 예를 들어 날짜, 통화 또는 전화 형식 등이 있습니다.

**새로운 유형의 차트 사용**

이제 Interactive Communications에 [Quadrant 차트와 여러 시리즈](../../forms/using/chart-component-interactive-communications.md)의 차트를 추가할 수 있습니다.

**표의 열 정렬**

이제 대화형 통신에서 [표 열 정렬(](../../forms/using/create-interactive-communication.md#sortcolumns))할 수 있습니다. 정적 텍스트 또는 데이터 모델 개체를 사용하여 표 열을 바인딩하고 정렬할 수 있습니다.

**웹 채널에서 새로운 구성 요소 사용**

이제 웹 채널에 단추 및 구분 문자 구성 요소를 추가할 수 있습니다. 자세한 내용은 웹 채널에 [단추 구성 요소 추가](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) 및 웹 채널](../../forms/using/create-interactive-communication.md#separatorcomponent)의 [구분 문자 구성 요소를 참조하십시오.

**구성 요소의 크기를 조정할 수 있는 레이아웃 모드**

이제 [레이아웃 모드](../../forms/using/resize-using-layout-mode.md)로 전환하여 WYSIWYG 인터페이스를 사용하여 웹 채널에서 구성 요소의 크기를 조정할 수 있습니다.

**향상된 유용성**

이제 인터랙티브 커뮤니케이션 작성자는 커뮤니케이션을 제작하면서 다양한 편리한 작업을 활용할 수 있습니다. 작업 목록은 다음과 같습니다.

* [인쇄 및 웹 채널에서 실행 취소/다시 실행 작업 수행](../../forms/using/create-interactive-communication.md#undoredoactions)
* [@ 기호를 사용하여 문서 조각에 변수 추가](../../forms/using/texts-interactive-communications.md#searchvariables)
* [@ 기호를 사용하여 문서 조각에 데이터 모델 요소 추가](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [기존 대화형 통신에 웹 채널 삭제 또는 추가](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [드래그 앤 드롭 작업을 사용하여 데이터 소스 요소를 필드 및 변수로 바인딩](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [인터랙티브 커뮤니케이션을 작성하는 동안 언바운드 필드 및 변수 강조 표시](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [웹 채널에서 상속된 구성 요소에 대해 복사, 그룹 등과 같은 추가 작업 수행](../../forms/using/create-interactive-communication.md#componenttoolbar)

**향상된 동기화 프로세스**

인쇄 채널을 사용하여 자동으로 생성된 웹 채널 레이아웃에서는 몇 가지 향상된 기능이 있습니다.

![인터랙티브 커뮤니케이션 차트](assets/interactive-communication-charts.png)

## 적응형 양식 {#adaptive-forms}

### 적응형 Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}에서 Adobe Sign의 클라우드 기반 디지털 서명 사용

[클라우드 기반의 디지털 ](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 서명 또는 원격 서명은 데스크탑, 모바일 및 웹에서 사용할 수 있는 차세대 디지털 서명이며, 최고 수준의 규정 준수 및 서명자 인증을 보장할 수 있습니다. 이제 [클라우드 기반 디지털 서명을 사용하여 응용 양식](../../forms/using/working-with-adobe-sign.md)에 서명할 수 있습니다.

#### AEM Sites 단일 페이지 응용 프로그램에 응용 양식 또는 대화형 통신 포함 {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms을 사용하면 AEM Sites 단일 페이지 애플리케이션(SPA)에 응용 양식[ 또는 대화형 통신을 완벽하게 포함할 수 있습니다. ](../../forms/using/embed-adaptive-form-aem-sites-spa.md) 포함된 적응형 양식 및 인터랙티브 커뮤니케이션은 모든 기능을 제공하므로 사용자는 페이지를 나가지 않고도 양식을 작성하고 제출할 수 있습니다. 사용자가 웹 페이지의 다른 요소 컨텍스트에서 벗어나지 않고 적응형 양식 또는 대화형 통신과 동시에 상호 작용할 수 있도록 해줍니다.

#### 응용 양식 테이블 열 정렬 {#sort-columns-of-adaptive-form-tables}

[응용 양식 테이블](../../forms/using/adaptive-forms-tables.md#sortcolumnstable)의 열을 오름차순 또는 내림차순으로 정렬할 수 있습니다. 정적 텍스트, 데이터 모델 개체 속성 또는 정적 텍스트 및 데이터 모델 개체 속성의 조합으로 표 열에 정렬을 적용할 수 있습니다.

#### 응용 Forms 템플릿의 가용성을 특정 경로 {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}로 제한

적응형 양식에서 cq:allowedPaths 속성에 대한 지원을 추가했습니다. 속성 [은 응용 Forms 템플릿의 가용성을 특정 경로](creating-adaptive-form.md#adaptive-form-templates)로 제한합니다.

#### 적응형 양식에 동적으로 {#add-check-boxes-to-the-adaptive-form-dynamically} 확인란을 추가합니다.

이제 사용자 지정 함수, 양식 개체 또는 개체 속성에 따라 확인란을 동적으로[에 추가하는 규칙을 정의할 수 있습니다.](../../forms/using/rule-editor.md#setpropertyrule)

## AEM 워크플로우 {#aem-workflows}

### AEM 워크플로우에서 변수 사용 {#use-variables-in-aem-workflows}

변수를 사용하면 런타임 시 워크플로우 단계에서 메타데이터를 저장하고 전달할 수 있습니다. 다양한 유형의 데이터를 저장하기 위해 다양한 유형의 변수를 만들 수 있습니다. 예: 정수, 문자열, 문서 또는 양식 데이터 모델 인스턴스. 일반적으로, 보유 중인 값을 기반으로 하거나 나중에 프로세스에서 필요한 정보를 저장하기 위해 필요한 경우 변수 또는 변수 모음을 사용합니다.

변수는 이전 버전에서 사용할 수 있는 [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 인터페이스의 확장입니다. 메타데이터 값을 검색하고 업데이트하는 데 사용되는 사용자 정의 ECMAScript 코드를 개발하는 데 소요되는 시간을 절약할 수 있습니다. MetaDataMap 인터페이스 및 ECMAScript 코드를 사용하여 메타데이터를 조작합니다. MetaDataMap 및 ECMAScript를 통해 변수를 사용하면 다음과 같은 이점이 있습니다.

* 사용자 지정 코드에 의존하지 않고 워크플로우 전반에 걸쳐 변수에 저장된 값을 동적으로 저장, 업데이트 및 사용
* 값을 검색하고 제출된 양식의 양식 데이터 모델 및 데이터 파일(XML/JSON)에 직접 업데이트
* 전체 문서를 변수에 저장하여 문서 처리 수행

이동 단계, OR 분할 단계 및 모든 AEM Forms 워크플로우 단계는 변수를 지원합니다. MetaDataMap 인터페이스를 사용하여 변수에 대한 기본 지원이 없는 워크플로우 단계의 변수에 액세스할 수 있습니다. 자세한 내용은 AEM Workflows](../../forms/using/variable-in-aem-workflows.md)의 [변수를 참조하십시오.

![워크플로우에서 변수 설정](assets/variable.png)

#### 다른 응용 Forms {#use-a-workflow-with-different-adaptive-forms}의 워크플로우 사용

[할당 작업](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step)에 대해 응용 양식을 지정하고 런타임 시 양식 중심 워크플로의 기록 단계 문서를 지정할 수 있습니다. 이를 통해 다양한 적응형 Forms을 사용하여 워크플로우를 진행할 수 있습니다. 워크플로우를 디자인하는 동안 적응형 양식을 선택하는 방법을 결정할 수 있습니다. 응용 양식은 절대 경로에 위치하거나, 워크플로우에 페이로드로 제출하거나, 변수를 사용하여 계산된 경로에 사용할 수 있습니다.

#### 양식 중심의 워크플로우 단계의 향상된 로깅 기능 사용 {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

양식 중심의 워크플로우 단계의 로깅 기능은 표준화되어 있습니다. 이제 모든 양식 중심의 워크플로우 단계에서는 유사한 표준화된 로그를 생성합니다. 디버깅 속도를 향상시킬 수 있습니다.

## 데이터 통합 {#data-integration}

이제 다음을 수행할 수 있습니다.

* [제약 조건 목록에 ](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) 있는 입력 데이터베이스의 유효성을 확인합니다. 유효한 데이터만 데이터 소스에 전송되도록 합니다.
* [WSDL(](../../forms/using/configure-data-sources.md#configure-soap-web-services) Web Services 설명 언어) 파일에 정의된 기본 끝점을 재정의합니다.

* [Swagger ](../../forms/using/configure-data-sources.md#configure-restful-web-services) [정의 파일에 정의된 기본 ](../../forms/using/configure-data-sources.md#configure-restful-web-services) 스키마, 호스트 및 기본 경로 무시

## 플랫폼 및 보안 업데이트 {#platform-and-security-updates}

### 주요 플랫폼 업데이트 {#major-platform-updates}

AEM Forms은 지원되는 운영 체제, 애플리케이션 서버, 데이터베이스, 데이터베이스 드라이버, JDK, LDAP 서버 및 이메일 서버를 조합하여 설정할 수 있습니다. 다음은 [지원되는 플랫폼](../../forms/using/aem-forms-jee-supported-platforms.md)의 주요 변경 사항입니다.

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
   <td>응용 프로그램 서버<br /> </td>
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
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP 서버</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
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
     <li>Connector for EMC Documentum 7.0</li>
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

* 다른 플랫폼으로 마이그레이션하는 방법에 대한 자세한 내용은 Adobe 지원 센터에 문의하십시오.

#### 새 HTML5 기반 UI {#new-html-based-uis}

Adobe Flash Player의 예정된 EOL과 개방형 표준으로 Flash 기반 컨텐츠를 마이그레이션하는 전반적인 방향에 따라 AEM 6.5 Forms은 JEE 관리 콘솔에서 AEM Forms의 Flash 기반 UI, 프로세스 관리, Reader 확장 및 카테고리 관리 UI를 HTML5 기반 UI로 대체했습니다.

#### 보안 개선 사항 {#security-improvements}

* JEE 관리 콘솔 UI의 AEM 6.5 Forms은 이제 Apache Struts 2.5를 기반으로 합니다.
* AEM 6.5 Forms은 이제 jQuery를 3.2.1 및 jQuery UI 1.12.1로 사용합니다. 변경 영향을 받으려면 [업그레이드 설명서](/help/forms/home.md)를 참조하십시오.

#### 액세스 가능성 향상 {#accessibility-improvements}

AEM 6.5 Forms은 AEM Forms 작업 공간의 접근성을 개선했습니다.
