---
title: AEM Forms 작업 영역 작업
description: 프로세스 워크플로에 대한 이 빠른 개요를 통해 AEM Forms 작업 영역을 시작하십시오.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# AEM Forms 작업 영역 작업{#working-with-aem-forms-workspace}

## 소개 {#introduction}

AEM Forms workspace 는 AEM Forms의 일부입니다. 작업 영역은 PDF forms 외에도 HTML Forms의 렌디션을 용이하게 합니다. 이제 모바일 인터페이스 및 웹 애플리케이션에서 비즈니스 프로세스에 참여할 수 있습니다.

또한 AEM Forms 작업 영역은 표준 HTML 및 JavaScript™ 개발 방법론을 사용하여 사용자 지정할 수 있습니다. 다른 웹 애플리케이션과 쉽게 통합되는 구성 요소 기반 소프트웨어입니다.

자세한 내용은 [AEM Forms 작업 영역 소개](/help/forms/using/introduction-html-workspace.md).

## 친숙해지기 {#getting-familiar}

비즈니스 프로세스를 자동화하는 Forms 응용 프로그램을 만드는 전체 프로세스에 익숙해지려면 연습에 따르십시오. 이 연습을 따라 Workbench, Designer 및 AEM Forms 작업 영역을 사용하여 응용 프로그램을 만들고 관리하고 테스트할 수 있습니다. 구현에 대한 자세한 내용은 [첫 번째 AEM Forms 애플리케이션 만들기](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## 기능 개요 {#functional-overview}

AEM Forms 작업 영역을 사용하여 다음 작업을 수행할 수 있습니다.

**비즈니스 프로세스 시작:** AEM Forms workspace는 조직이 디자인하고 설정한 대로 프로세스를 분류합니다. 자주 사용되는 카테고리를 즐겨찾기에 추가하여 카테고리에 빠르게 액세스할 수 있습니다. 프로세스를 시작할 때 일반적으로 양식을 작성하여 워크플로 컨트롤을 구성하는 비즈니스 프로세스를 시작합니다. 자세한 내용은 [시작 프로세스](/help/forms/using/starting-processes.md).

**작업 보기 및 조치:** 할 일 목록을 볼 때 자신에게 할당되거나 자신이 속한 그룹에 할당되거나 다른 사용자의 공유 작업인 비즈니스 프로세스의 작업이 표시됩니다. 필요에 따라 작업을 열고, 작업하고, 완료할 수 있습니다. 일반적으로 작업 완료에는 정보 제공, 양식 승인 또는 양식 거부가 포함됩니다. 자세한 내용은 [할 일 목록 작업](/help/forms/using/todo-lists.md).

**작업 추적**: 작업을 추적하려면 AEM Forms 작업 공간의 추적 탭을 사용합니다. 시작하거나 참여한 활성 또는 완료된 프로세스를 검색할 수 있습니다. 프로세스에 포함된 작업, 할당 및 양식을 볼 수 있습니다. 이전에 시작한 프로세스의 양식 데이터를 사용하여 새 프로세스를 시작할 수도 있습니다. 자세한 내용은 [추적 프로세스](/help/forms/using/tracking-processes.md).

## AEM Forms 작업 영역의 새로운 기능 {#new-offering-of-aem-forms-workspace}

**작업의 일괄 승인 지원**:

동일한 유형의 여러 작업을 승인할 수 있습니다. 승인을 위해 하나의 작업을 선택하면 프로세스가 같고 작업 이름이 같고 경로 옵션이 같은 작업만 활성화됩니다. 다음을 참조하십시오 [할 일 목록 작업](/help/forms/using/todo-lists.md) 구현 세부 사항.

## Flex Workspace에서 AEM Forms Workspace로 마이그레이션 {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace는 AEM Forms 고객에게 지원되지 않습니다. Flex 작업 영역을 사용하는 모든 고객은 AEM Forms 작업 영역으로 이동해야 합니다.

AEM Forms 작업 영역에서 XDP 양식과 연결된 기본 작업 프로필의 기본 렌더링 및 제출 서비스가 변경되고 새 서비스가 도입되었습니다. 자세한 내용은 [새로운 렌더링 및 제출 서비스](/help/forms/using/new-render-submit-service.md). XDP 양식에서 작동하는 기존 프로세스를 마이그레이션하고 이러한 서비스를 사용하려면 다음을 수행할 수 있습니다. [다음 단계](new-render-submit-service.md).

**AEM Forms Workspace를 사용하여 Flex Workspace 사용자 지정 매핑**

두 작업 영역의 다양한 사용자 지정 유형 간의 매핑은 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>사용자 지정 유형 </strong></td>
   <td><strong>다루어진 사용자 정의 </strong></td>
   <td><strong>해당 AEM Forms 작업 영역 사용자 지정 시나리오</strong></td>
  </tr>
  <tr>
   <td>로컬라이제이션 맞춤화</td>
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
   <td>레이아웃 사용자 지정</td>
   <td>
    <ol>
     <li>작업 공간 사용자 인터페이스 단순화<br /> </li>
     <li>새 로그인 화면 만들기</li>
     <li>사용자 지정 승인 컨테이너 만들기</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">재사용 가능한 구성 요소 작업</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">로그인 화면 만들기</a></li>
     <li>승인 컨테이너는 더 이상 사용되지 않습니다.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

AEM Forms Workspace에서 사용할 수 없는 Flex Workspace의 기능 중 일부는 메시지 및 알림, 시작 페이지, 승인 컨테이너 및 열 머리글을 관리하는 옵션이 있습니다. 전체 목록이 필요하면 를 참조하십시오. [Flex 작업 영역의 기능을 AEM Forms 작업 영역에서 사용할 수 없음](/help/forms/using/features-flex-workspace-available-html.md).

## AEM Forms 작업 영역을 사용하여 개발 {#developing-with-aem-forms-workspace}

### 아키텍처 {#architecture}

AEM Forms workspace 는 CRX™에서 호스팅되는 HTML 및 JavaScript™ 기반 웹 애플리케이션입니다. 작업 공간 URL이 브라우저에서 열리면 CRX™ 리소스에 액세스되고, 애플리케이션이 브라우저에서 HTML 페이지로 렌더링됩니다. JavaScript 라이브러리 및 사용자 지정 JavaScript 코드는 사용자 인터페이스, 사용자 상호 작용 및 AEM Forms 서버와의 통신과 같은 애플리케이션의 내부 및 외부 동작을 관리합니다. 자세한 내용은 AEM Forms 작업 영역 을 참조하십시오. [아키텍처](/help/forms/using/html-workspace-architecture.md).

### AEM Forms 작업 공간 사용자 정의 {#aem-forms-workspace-customization}

AEM Forms 작업 영역은 사용자 인터페이스의 레이아웃, 모양, 기능 등을 업데이트하는 다양한 사용자 지정을 지원합니다. 맞춤화에는 다음 중 하나 이상을 업데이트하는 작업이 포함됩니다.

* 사용자 인터페이스의 모양새
* 의미 체계 사용자 지정을 사용한 기능
* 다른 웹 애플리케이션에서 HTML 구성 요소 재사용

다음 [사용자 지정](introduction-customizing-html-workspace.md#types-of-customizations) 이 문서에서는 이러한 사용자 지정 유형에 대해 설명합니다.

### 개발자 환경 설정 {#set-up-the-developer-environment}

AEM Forms 작업 공간 결과물에는 CRX에 배포된 CRX 패키지, 전체 소스 코드가 포함된 SDK 아카이브, 타사 JavaScript 라이브러리 및 AEM Forms 작업 공간의 빌드 스크립트가 포함됩니다. 위에서 언급한 맞춤화를 수행하도록 개발자 환경을 설정하는 데 사용합니다. 자세한 내용은 [AEM Forms 작업 공간 코드 작성](introduction-customizing-html-workspace.md#building-html-workspace-code).

인터페이스 및 핵심 기능의 주요 부분(글꼴, 색 구성표, 로고, 로그인 화면, 오류 대화 상자, 타사 응용 프로그램과의 통합 및 타사 응용 프로그램의 구성 요소 재사용)을 사용자 지정할 수 있습니다. 또한 [작업 요약] 페이지에 표시되는 내용을 향상시키고, 작업 경로 작업에 대한 이미지를 표시하고, AEM Forms 작업 영역 응용 프로그램을 생성하는 낮은 수준의 백본 모델 및 보기를 수정할 수 있습니다.

### XDP Forms의 HTML 렌더링 {#html-rendering-of-xdp-forms}

기본적으로 새 프로세스의 경우 XDP 양식은 데스크탑에서 PDF 형식으로 렌더링되고 태블릿에서 HTML 형식으로 렌더링됩니다. XDP 양식을 항상 HTML 형식으로 렌더링할 수 있습니다. 자세한 내용은 [새로운 렌더링 및 제출 서비스](/help/forms/using/new-render-submit-service.md).

[모바일 Forms](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) 과 호환되는 기능 [프로필](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html): XDP 양식의 HTML 렌디션을 활성화합니다. 기본적으로 &#39;새 HTML 양식 렌더링&#39;은 `default.html` 변경할 수 있는 프로필. XDP 양식을 HTML 형식으로 렌더링하기 전에 발생하는 사용자 지정 변경 사항을 추가할 수도 있습니다.

## AEM Forms 작업 영역 앱 {#aem-forms-workspace-app}

모바일 디바이스에서 비즈니스 프로세스를 작업하려면 AEM Forms의 AEM Forms 작업 영역 앱 서비스를 사용하면 됩니다. 자세한 내용은 [AEM Forms 작업 영역 앱 개요](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
