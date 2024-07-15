---
title: Adobe Developer App Builder을 사용하여  [!DNL Adobe Experience Manager] 6.5를 확장합니다.
description: Adobe Developer App Builder을 사용하여  [!DNL Adobe Experience Manager] 6.5를 확장합니다.
exl-id: 8221c2db-82d4-43df-ad38-e8e7831541ac
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Adobe Developer App Builder을 사용하여 [!DNL Adobe Experience Manager] 확장 {#extend-using-app-builder}

## AEM용 App Builder 소개 {#project-appbuilder}

새로운 Adobe Developer App Builder은 개발자가 AEM 기능을 쉽게 확장할 수 있는 확장성 프레임워크를 제공합니다.

App Builder은 Adobe Experience Manager을 확장하는 사용자 지정 경험을 통합하고 만들기 위한 통합 타사 확장성 프레임워크를 제공합니다. Adobe의 인프라를 기반으로 구축된 이 완벽한 확장성 프레임워크를 통해 개발자는 맞춤형 마이크로서비스를 구축하고, Adobe 솔루션 및 나머지 IT 스택 전반에서 Adobe Experience Manager을 확장 및 통합할 수 있습니다.

App Builder은 고객이 다양한 사용 사례에서 Adobe Experience Manager을 쉽게 확장할 수 있는 방법을 제공합니다.

* 미들웨어 확장성 - 사용자 정의 커넥터를 빌드하는 Adobe 애플리케이션과 외부 시스템을 연결하거나 사전 설치된 통합 세트를 사용합니다.
* 핵심 서비스 확장성 - 사용자 정의 기능 및 비즈니스 논리를 통해 기본 동작을 확장하여 핵심 애플리케이션 기능을 확장합니다.
* 사용자 경험 확장성 - 핵심 경험을 확장하여 비즈니스 요구 사항을 지원하거나 고객별 디지털 속성, 상점 및 백오피스 앱을 빌드합니다.

App Builder은 2020년 여름부터 Adobe의 개발자 미리보기를 통해 기업 고객 및 파트너가 사용할 수 있습니다. App Builder의 GA(일반 공급)가 2021년 12월로 예정되어 있습니다. Adobe은 개발자가 Adobe의 [평가판 프로그램](https://developer.adobe.com/app-builder/trial/)을 통해 App Builder을 사용해 볼 수 있도록 환영합니다.

>[!NOTE]
>
>App Builder을 사용하려는 AEM as a Cloud Service 고객의 경우 [Adobe Developer App Builder을 사용하여 Adobe Experience Manager as a Cloud Service 확장](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html)을 참조하십시오.

## 아키텍처 {#architecture}

Adobe Developer App Builder은 기본 솔루션 대신 AEM과 같은 Adobe 클라우드 솔루션을 확장하기 위해 공통적이고, 일관되고, 표준화된 개발 플랫폼을 제공합니다.

* Adobe Developer Console — 사용자 정의 마이크로서비스 및 확장 개발을 위해 개발자가 플러그인 및 통합을 만드는 데 필요한 모든 도구 및 API에 액세스하는 동안 프로젝트를 구축하고 관리할 수 있도록 합니다.
* 개발자 도구 — 개발자가 사용자 정의 확장 및 통합을 쉽게 구축할 수 있도록 해주는 오픈 소스 도구, SDK 및 라이브러리입니다. React Spectrum(Adobe의 UI 툴킷)을 사용하여 모든 Adobe 앱에 대해 하나의 공통 UI를 가질 수 있습니다.
* 서비스 — Adobe의 서버리스 플랫폼에서 인프라를 호스팅하기 위한 I/O 런타임 및 이벤트 기반 통합을 위한 I/O 이벤트. Adobe은 또한 데이터 및 파일 저장을 위한 기본 지원을 제공합니다.
* Adobe Experience Cloud — 개발자는 Experience Cloud 조직 내에 게시할 확장 및 통합을 제출할 수 있습니다. 그런 다음 시스템 관리자는 이러한 확장을 검토, 관리 및 승인할 수 있습니다. 게시되면 사용자 지정 App Builder 확장 및 도구를 다른 Adobe Experience Cloud 앱과 함께 찾을 수 있습니다.

다음 다이어그램은 App Builder에 구축된 표준 애플리케이션이 이러한 기능을 사용하는 방법을 보여 줍니다.

![아키텍처](assets/appbuilder-architecture.jpg)

App Builder 아키텍처에 대한 자세한 내용은 [아키텍처 개요](https://developer.adobe.com/app-builder/docs/guides/)를 참조하십시오.

## App Builder 시작 {#additional-resources}

App Builder을 시작하는 데 도움이 되도록 다음 작업을 시작하는 데 도움이 되는 일련의 설명서가 만들어졌습니다.

* [App Builder 시작](https://developer.adobe.com/app-builder/docs/getting_started/)

## 설명서를 사용하여 학습 계속 {#appbuilder-documentation}

App Builder은 안내서를 포함하여 개발자를 위한 비디오 및 설명서와 사용자 정의 애플리케이션 개발을 시작하는 데 도움이 되는 참조 설명서를 제공합니다.

* [App Builder 설명서](https://developer.adobe.com/app-builder/docs/overview/)
* [App Builder 비디오](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## 샘플 애플리케이션 중 하나를 사용해 보십시오. {#appbuilder-codesamples}

개발을 시작할 준비가 되셨습니까? 다음은 빠르게 진행할 수 있는 샘플 애플리케이션입니다.

* Adobe Developer 웹 사이트의 [App Builder 코드 랩](https://developer.adobe.com/app-builder/docs/resources/)

