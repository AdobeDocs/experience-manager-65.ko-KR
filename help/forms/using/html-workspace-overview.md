---
title: AEM Forms 작업 영역 작업
seo-title: AEM Forms 작업 영역 작업
description: 프로세스 워크플로우에 대한 빠른 개요를 통해 AEM Forms 작업 영역을 시작합니다.
seo-description: 프로세스 워크플로우에 대한 빠른 개요를 통해 AEM Forms 작업 영역을 시작합니다.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
translation-type: tm+mt
source-git-commit: 21efe30c6a69d04c737bc523aeaab504db8f605b

---


# Working with AEM Forms workspace{#working-with-aem-forms-workspace}

## 소개 {#introduction}

AEM Forms 작업 영역은 AEM Forms의 일부입니다. 작업 공간에서는 PDF 양식 외에도 HTML 양식을 쉽게 변환할 수 있습니다. 이제 모바일 인터페이스 및 웹 애플리케이션에서 비즈니스 프로세스에 관여할 수 있습니다.

또한 AEM Forms 작업 영역은 표준 HTML 및 JavaScript™ 개발 방법을 사용하여 사용자 정의할 수 있습니다. 다른 웹 애플리케이션과 손쉽게 통합되는 구성 요소 기반의 소프트웨어입니다.

자세한 내용은 AEM [Forms 작업 영역](/help/forms/using/introduction-html-workspace.md)소개를 참조하십시오.

## 친숙한 방법 {#getting-familiar}

양식 애플리케이션을 만들어 비즈니스 프로세스를 자동화하는 종단 간 프로세스에 익숙해지려면 이 연습을 따르십시오. 이 연습 후에 워크벤치, 디자이너 및 AEM Forms 작업 영역을 사용하여 애플리케이션을 만들고, 관리하고 테스트할 수 있습니다. 구현에 대한 자세한 내용은 첫 [번째 AEM Forms 애플리케이션 만들기를 참조하십시오](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## 기능 개요 {#functional-overview}

AEM Forms 작업 영역을 사용하여 다음 작업을 수행할 수 있습니다.

**비즈니스 프로세스 시작:** AEM Forms 작업 영역은 조직에서 디자인하고 설정한 프로세스에 따라 분류합니다. 자주 사용하는 카테고리를 즐겨찾기에 추가하여 카테고리에 빠르게 액세스할 수 있습니다. 프로세스를 시작하면 일반적으로 양식을 작성하여 양식 워크플로우가 제어하는 비즈니스 프로세스를 시작합니다. 자세한 내용은 프로세스 [시작을 참조하십시오](/help/forms/using/starting-processes.md).

**작업 보기 및 실행:** 할 일 목록을 볼 때 자신에게 할당된 업무 프로세스, 또는 사용자가 속한 그룹 또는 다른 사용자의 공유 작업에서 작업이 표시됩니다. 필요에 따라 작업을 열고 계속 작업하고 완료할 수 있습니다. 일반적으로 작업을 완료하는 데는 정보 제공, 양식 승인 또는 양식 거부가 포함됩니다. 자세한 내용은 할 일 [목록](/help/forms/using/todo-lists.md)작업을 참조하십시오.

**작업**&#x200B;추적:작업을 추적하려면 AEM Forms 작업 영역의 추적 탭을 사용합니다. 시작하거나 참여한 활성 또는 완료된 프로세스를 검색할 수 있습니다. 프로세스의 일부인 작업, 할당 및 양식을 볼 수 있습니다. 이전에 시작한 프로세스의 양식 데이터를 사용하여 새 프로세스를 시작할 수도 있습니다. 자세한 내용은 추적 [프로세스를](/help/forms/using/tracking-processes.md)참조하십시오.

## AEM Forms 작업 영역의 새로운 기능 {#new-offering-of-aem-forms-workspace}

**작업의**&#x200B;일괄 승인 지원:

동일한 유형의 여러 작업을 승인할 수 있습니다. 승인을 위해 하나의 작업을 선택하면 동일한 프로세스, 동일한 작업 이름 및 동일한 경로 옵션이 있는 작업만 활성화됩니다. 구현 [세부 사항은 할 일 목록](/help/forms/using/todo-lists.md) 작업을 참조하십시오.

## Flex 작업 공간에서 AEM Forms 작업 영역으로 마이그레이션 {#migrating-from-flex-workspace-to-aem-forms-workspace}

AEM Forms 고객은 Flex 작업 영역을 지원하지 않습니다. Flex 작업 영역을 사용하는 모든 고객은 AEM Forms 작업 영역으로 이동해야 합니다.

AEM Forms 작업 영역에서 기본 렌더링 및 제출 서비스는 XDP 양식과 연결된 기본 작업 프로필에서 변경되었으며 새 서비스가 도입되었습니다. 자세한 내용은 새로운 [렌더링 및 제출 서비스를](/help/forms/using/new-render-submit-service.md)참조하십시오. XDP 양식과 연동되는 기존 프로세스를 마이그레이션하여 이러한 서비스를 이용하려면 [다음 단계를](new-render-submit-service.md)따르십시오.

**AEM Forms 작업 영역을 사용하여 Flex 작업 영역 사용자 정의 매핑**

두 작업 영역에서 다양한 유형의 사용자 정의 간의 매핑은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>사용자 정의 유형 </strong></td>
   <td><strong>사용자 정의 적용 </strong></td>
   <td><strong>해당 AEM Forms 작업 영역 사용자 정의 시나리오</strong></td>
  </tr>
  <tr>
   <td>로컬라이제이션 사용자 정의</td>
   <td>
    <ol>
     <li>작업 영역의 로케일 변경</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">AEM Forms 작업 영역 로케일 변경</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>테마 맞춤화</td>
   <td>
    <ol>
     <li>이미지 바꾸기</li>
     <li>색상 수정</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">조직 로고 변경</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">색상 구성표 변경</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>레이아웃 사용자 정의</td>
   <td>
    <ol>
     <li>작업 영역 사용자 인터페이스 간소화<br /> </li>
     <li>새 로그인 화면 만들기</li>
     <li>사용자 지정 승인 컨테이너 만들기</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">재사용 가능한 구성 요소 작업</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">새 로그인 화면 만들기</a></li>
     <li>승인 컨테이너는 더 이상 사용되지 않습니다.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

AEM Forms 작업 영역에서 사용할 수 없는 Flex 작업 영역의 일부 기능은 다음과 같습니다.메시지 및 알림, 시작 페이지, 승인 컨테이너 및 열 머리글 관리 옵션 전체 목록은 AEM Forms 작업 [영역에서](/help/forms/using/features-flex-workspace-available-html.md)사용할 수 없는 Flex 작업 영역의 기능을 참조하십시오.

## AEM Forms 작업 영역으로 개발 {#developing-with-aem-forms-workspace}

### 아키텍처 {#architecture}

AEM Forms 작업 영역은 CRX™에서 호스팅되는 HTML 및 JavaScript™ 기반의 웹 애플리케이션입니다. 브라우저에서 작업 영역 URL을 열면 CRX™ 리소스에 액세스되고 응용 프로그램이 브라우저에서 HTML 페이지로 렌더링됩니다. JavaScript 라이브러리와 사용자 지정 JavaScript 코드는 사용자 인터페이스, 사용자 상호 작용 및 AEM Forms 서버와의 통신과 같은 애플리케이션의 내부 및 외부 동작을 관리합니다. 자세한 내용은 AEM Forms 작업 영역 [아키텍처를](/help/forms/using/html-workspace-architecture.md)참조하십시오.

### AEM Forms 작업 영역 사용자 정의 {#aem-forms-workspace-customization}

AEM Forms 작업 영역은 사용자 인터페이스의 레이아웃, 모양, 기능 등을 업데이트하기 위해 다양한 사용자 지정을 지원합니다. 사용자 지정에는 다음 중 하나 이상을 업데이트하는 작업이 포함됩니다.

* 유저 인터페이스의 모양
* 의미 체계 사용자 지정을 사용한 기능
* 다른 웹 애플리케이션에서 HTML 구성 요소 재사용

사용자 [지정](introduction-customizing-html-workspace.md#types-of-customizations) 아티클에서는 이러한 사용자 정의 유형에 대해 설명합니다.

### Set up the developer environment {#set-up-the-developer-environment}

AEM Forms 작업 영역 결과물에는 CRX에 배포된 CRX 패키지, 전체 소스 코드, 타사 JavaScript 라이브러리가 포함된 SDK 아카이브, AEM Forms 작업 영역의 스크립트 빌드가 포함됩니다. 개발자 환경을 설정하여 위에 언급된 사용자 지정을 수행합니다. 자세한 내용은 AEM Forms [작업 영역 코드](introduction-customizing-html-workspace.md#building-html-workspace-code)작성을 참조하십시오.

인터페이스 및 핵심 기능(예: 글꼴, 색상 구성표, 로고, 로그인 화면, 오류 대화 상자, 타사 애플리케이션과의 통합, 타사 애플리케이션에서 구성 요소 재사용)의 주요 부분을 사용자 정의할 수 있습니다. 작업 요약 페이지에 표시되는 컨텐츠를 향상시키고 작업 경로 작업에 대한 이미지를 보여주며 AEM Forms 작업 영역 응용 프로그램을 만드는 하위 수준 백본 모델 및 보기를 수정할 수도 있습니다.

### XDP 양식의 HTML 렌더링 {#html-rendering-of-xdp-forms}

기본적으로 새로운 프로세스의 경우 XDP 양식이 데스크탑에서 PDF 형식으로 렌더링되고 태블릿에서 HTML 형식으로 렌더링됩니다. XDP 양식을 항상 HTML 형식으로 렌더링할 수 있습니다. 자세한 내용은 새로운 렌더링 [및 제출 서비스를 참조하십시오](/help/forms/using/new-render-submit-service.md).

[모바일 양식](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) 기능을 사용하면 [XDP 양식의 HTML 변환을](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html)사용할 수 있습니다. 기본적으로 &#39;새 HTML 양식 렌더링&#39;은 변경할 수 있는 `default.html` 프로파일을 사용합니다. XDP 양식을 HTML 형식으로 렌더링하기 전에 발생하는 사용자 지정 변경 사항을 추가할 수도 있습니다.

## AEM Forms 작업 영역 앱 {#aem-forms-workspace-app}

모바일 장치에서 비즈니스 프로세스를 작업하려면 AEM Forms의 AEM Forms 작업 영역 앱 솔루션을 사용할 수 있습니다. 자세한 내용은 AEM Forms 작업 [영역 앱 개요를](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html)참조하십시오.
