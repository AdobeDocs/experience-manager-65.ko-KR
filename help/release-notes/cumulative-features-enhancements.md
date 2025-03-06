---
title: Adobe Experience Manager 6.5 릴리스의 누적 주요 기능 및 개선 사항.
description: 이전 8개의 서비스 팩 릴리스에서 Adobe Experience Manager 6.5에 포함된 주요 기능 및 개선 사항의 누적 목록입니다.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: 54b508809733ed86798558aee50f8c7b5de00af9
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 28%

---

# 누적 주요 기능 및 개선 사항

이전 8개의 서비스 팩 릴리스에 대한 Adobe Experience Manager 6.5의 주요 기능 및 개선 사항의 누적 목록입니다.

[Adobe Experience Manager 6.5 최신 서비스 팩 릴리스 정보](/help/release-notes/release-notes.md)도 참조하세요.

## AEM 6.5, 서비스 팩 18—2023년 12월 7일

* 사이트 페이지 편집기/이미지 구성 요소 사용자가 원격 Assets Cloud Service의 에셋을 참조할 수 있도록 했습니다. (SITES-13448, SITES-13433)
* 이제 AEM은 목록 보기에서 더 빠른 프로젝트 탐색을 위해 서버측 정렬을 지원합니다. 프로젝트 노드는 인터페이스에 표시되기 전에 사용자가 선택한 열을 기준으로 정렬됩니다.

### [!DNL Forms]

* **새로운 적응형 양식 핵심 구성 요소**: 양식의 확장성을 높이기 위해 세로 탭, 약관 및 확인란이 추가되었습니다.
   * **[확인란 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**: 이제 핵심 구성 요소를 기반으로 하는 적응형 양식에 확인란 구성 요소를 포함할 수 있습니다. 이를 통해 사용자는 특정 옵션을 선택하거나 선택 취소하는 이진 선택을 할 수 있습니다. 확인란은 일반적으로 클릭하거나 탭하여 두 가지 상태(선택됨 및 선택 취소됨) 사이를 전환할 수 있는 작은 상자 형태입니다. 확인란은 예/아니요 또는 참/거짓 선택을 표시하는 데 사용되는 일반적인 양식 요소입니다.

   * **[약관 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**: 이제 핵심 구성 요소를 기반으로 하는 적응형 양식에 약관 구성 요소를 포함함 수 있습니다. 이를 통해 Forms 작성자는 서비스, 제품 또는 플랫폼 사용과 관련된 약관, 조건 또는 법적 계약서를 사용자에게 제공하는 양식 내에서 특정 섹션을 소개할 수 있습니다. 이 구성 요소는 양식을 제출하면 동의하는 것으로 간주되는 규칙, 규정 및 의무에 대해 사용자에게 알리도록 설계되었습니다.

     ![세로 탭, 약관 및 확인란 구성 요소](/help/forms/using/assets/forms-components.png)

   * **[세로 탭 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**: 이제 핵심 구성 요소를 기반으로 하는 적응형 양식은 양식 콘텐츠를 세로 탭 목록으로 구성하여 체계적이고 탐색 가능한 레이아웃을 제공할 수 있습니다. 양식에서 세로 탭을 사용하면 특히 양식에 여러 섹션이나 복잡한 정보가 포함되어 있을 때 탐색을 단순화하고 양식 콘텐츠 구성을 개선하여 전반적인 사용자 경험을 향상시킬 수 있습니다.

* **[64비트 버전의 AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: 64비트 버전의 AEM Forms Designer은 향상된 성능, 확장성 및 메모리 관리를 제공하여 양식 생성 환경을 향상시킵니다. 64비트 아키텍처를 사용하면 더 크고 복잡한 프로젝트를 간단하게 처리하여 원활한 워크플로 디자인과 최적화된 효율성을 보장할 수 있습니다. 이 혁신적인 릴리스를 통해 양식 디자인 기능을 개선하고 AEM Forms Designer를 진전시킬 수 있습니다.

* **[적응형 Forms과 Microsoft® SharePoint 목록 연결](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**: AEM Forms에서는 양식 데이터를 SharePoint 목록에 직접 제출할 수 있는 기본 통합을 제공하므로 SharePoint의 목록 기능을 사용할 수 있습니다. Microsoft® SharePoint 목록을 양식 데이터 모델에 대한 데이터 소스로 구성하고 양식 데이터 모델을 사용하여 제출 제출 액션을 사용하여 적응형 양식을 SharePoint 목록과 연결할 수 있습니다.

* **[적응형 양식 조각에 대한 기록 문서 속성 구성 지원](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**: 이제 적응형 양식 편집기에서 적응형 양식 조각과 해당 필드를 쉽게 사용자 지정할 수 있습니다.

* **64비트 XMLFM**: XMLFM의 64비트 반복에서는 향상된 성능, 확장성 및 개선된 메모리 관리를 제공합니다. 서버측에 배포된 최초의 64비트 네이티브 서비스입니다. XMLFM 64비트는 32비트보다 더 큰 메모리 리소스에 액세스할 수 있는 고유한 기능을 활용함으로써 더 큰 렌더링 워크로드를 원활하게 처리할 수 있도록 지원합니다. 이 이정표는 성능 향상을 나타낼 뿐만 아니라 AEM Forms 서버 내의 기본 서비스 프레임워크에 대한 주요 개선 사항을 소개합니다. 이 업데이트는 AEM Forms 서버가 모든 64비트 기본 서비스를 원활하게 지원할 수 있도록 합니다.

## AEM 6.5, 서비스 팩 18—2023년 8월 24일

* Assets, Dynamic Media - [Dynamic Media의 비디오에 대한 다중 캡션 및 오디오 트랙 지원](/help/assets/video.md#about-msma) - 이제 기본 비디오에 다중 자막 및 다중 오디오 트랙을 쉽게 추가할 수 있습니다. 즉, 이러한 기능을 통해 글로벌 대상자는 비디오에 액세스할 수 있습니다. 여러 언어로 글로벌 대상자에게 게시된 하나의 기본 비디오를 사용자 정의하고 지역별 액세스 가능성 가이드라인을 준수할 수 있습니다. 작성자는 사용자 인터페이스의 단일 탭에서 자막 및 오디오 트랙을 관리할 수도 있습니다.
* Assets - 이제 검색 결과에서 에셋이 포함된 폴더 위치로 이동하여 다양한 에셋 관리 작업을 수행할 수 있습니다.
* 컨텐츠 조각의 Sites Polaris Picker가 성능이 향상되었습니다.
* 사이트 페이지 편집기/이미지 구성 요소 사용자가 원격 Assets Cloud Service의 에셋을 참조할 수 있도록 했습니다.
* 시스템에 많은 프로젝트가 있을 수 있는 목록 보기에서 프로젝트를 빠르게 찾기 위해 이제 Adobe에서 서버측 정렬을 지원합니다. 프로젝트 노드는 사용자 인터페이스에서 렌더링하기 전에 사용자가 선택한 열을 기반으로 백엔드에서 정렬됩니다.
* AEM 6.5.18.0은(는) MongoDB 5.0에서 6.0까지 지원합니다.

### [!DNL Forms]

* **[규칙 편집기에서 사용자 지정 오류 처리기를 사용하여 오류 처리 기능이 개선되었습니다](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html)** - 이제 외부 서비스에서 반환된 오류에 대한 응답으로 사용자 지정 함수(클라이언트 라이브러리 사용)를 호출할 수 있습니다. 또한 최종 사용자에게 맞춤 응답을 제공할 수 있습니다. 서비스에서 반환된 오류에 대해 특정 작업을 수행할 수도 있습니다. 예를 들어 특정 오류 코드에 대해 백엔드에서 사용자 지정 워크플로우를 호출하거나 서비스가 중단되었음을 고객에게 알릴 수 있습니다

* **[향상된 Adobe Sign 워크플로 단계](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step)** - AEM 워크플로의 Adobe Sign 워크플로 단계는 다음과 같은 향상된 기능을 통해 사용할 수 있습니다.

   * **Adobe Sign에 대한 정부 ID 기반 인증을 통해 향상된 보안** - Adobe Acrobat Sign의 정부 ID 기반 인증은 추가 인증 계층을 제공합니다. 사용자가 정부에서 발급한 신분증(운전면허증, 주민등록증, 여권)을 이용해 본인 인증을 할 수 있도록 했다. 신뢰할 수 있는 식별 문서를 사용하여 이 개선된 기능은 서명 프로세스에 신뢰도를 추가하여 보안, 규정 준수 및 사용자 유효성 검사 강화에 필요한 시나리오에 적합합니다.

   * **Adobe Sign 문서에 대한 감사 추적을 통해 투명성 향상** - 감사 추적 기능을 사용하여 Adobe Sign 문서의 라이프사이클에 대한 자세한 통찰력을 얻을 수 있습니다. 감사 추적을 사용하여 이제 문서와 관련된 모든 작업과 상호 작용에 대한 포괄적인 기록을 유지 관리할 수 있습니다. 여기에는 각 이벤트의 타임스탬프와 함께 문서를 조회하고, 편집하거나 서명한 사람 등과 같은 세부 정보가 포함됩니다. 이러한 개선된 기능은 규정 준수를 유지하고, 분쟁을 해결하고, 디지털 계약의 무결성을 보장하는 데 중요합니다.


   * **서명자 이상으로 계약 수신자의 역할 확장** - Adobe Acrobat Sign을 사용하면 계약 수신자의 역할을 서명자 이상으로 확장하여 워크플로 요구 사항에 보다 잘 부합하도록 할 수 있습니다. 활성화된 경우 계약의 각 수신자는 자신의 역할을 개별적으로 구성할 수 있으며 기본값은 서명자입니다.


* **[JEE의 AEM Forms 전체 설치 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)** - 서비스 팩은 다음을 포함한 여러 가지 새로운 소프트웨어 조합을 지원하는 JEE의 AEM Forms 전체 설치 관리자를 제공합니다.
   * Microsoft® 윈도우 서버 2022
   * Microsoft® Active Directory 2022
   * Windows Server 2022의 Oracle WebLogic 14C
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * MySQL JDBC Connector 8

JEE의 AEM 6.5 Forms 환경에 최신 소프트웨어를 설치하거나 사용할 계획이라면 Adobe은 JEE의 AEM 6.5.18.0 Forms 전체 설치 관리자를 사용하는 것이 좋습니다. 새로 추가되고 더 이상 사용되지 않는 소프트웨어의 전체 목록을 살펴보려면 JEE의 AEM Forms 또는 OSGi의 AEM Forms 설명서를 참조하십시오.

## AEM 6.5, 서비스 팩 17—2023년 5월 25일

* **검색 환경 개선 사항** - 이제 검색 결과에 표시되는 자산에 대해 다음 작업을 빠르게 수행할 수 있습니다.
   * 워크플로 만들기
   * 버전 만들기
   * 자산 연결 또는 연결 해제

  해당 작업을 수행하기 위해 자산 위치로 이동하여 자산 속성을 볼 필요가 없습니다.
* **Dynamic Media _스냅숏_**- 테스트 이미지 또는 Dynamic Media URL을 실험하여 다양한 이미지 수정자의 출력을 확인하고 Smart Imaging에서 파일 크기(WebP 및 AVIF 전달), 네트워크 대역폭 및 장치 픽셀 비율에 대해 최적화합니다. [Dynamic Media 스냅샷](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html)을 참조하십시오.
* **Dynamic Media를 사용한 DASH 스트리밍** - Dynamic Media 비디오 게재(CMAF가 활성화됨)에서 적응형 스트리밍을 위해 실행된 새 프로토콜(DASH - HTTP를 통한 동적 적응형 스트리밍). 현재 모든 지역에서 사용할 수 있습니다.
* **Experience Manager Sites 및 컨텐츠 조각과 Assets 차세대 Dynamic Media 통합** - 이제 Experience Manager Assets as a Cloud Service 차세대 Dynamic Media 사용자는 이러한 클라우드 호스팅 자산을 Experience Manager Sites 6.5의 온-프레미스 또는 Managed Services 인스턴스와 함께 작성 및 게재에 사용할 수 있습니다.

### [!DNL Forms]

* **[AEM 페이지 편집기 내 적응형 양식](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**: 이제 AEM 페이지 편집기를 사용하여 여러 양식을 빠르게 만들고 사이트 페이지에 추가할 수 있습니다. 이 기능을 통해 콘텐츠 작성자는 동적 비헤이비어, 유효성 검사, 데이터 통합, 기록 문서 생성 및 비즈니스 프로세스 자동화 등 적응형 양식 구성 요소의 기능을 사용하여 Sites 페이지에서 원활한 데이터 캡처 경험을 만들 수 있습니다. 다음과 같은 작업을 수행할 수 있습니다.
   * AEM Sites 편집기 또는 경험 조각에서 양식 구성 요소를 적응형 양식 컨테이너 구성 요소로 드래그 앤 드롭하여 적응형 양식을 만듭니다.
   * AEM Sites 편집기 내에서 적응형 양식 마법사를 사용하여 Sites 페이지와는 별개로 양식을 만들게 되면 여러 페이지에서 해당 양식을 자유롭게 재사용할 수 있습니다.
   * Sites 페이지에 여러 양식을 추가하여 사용자 경험을 간소화하고 더 많은 유연성을 제공합니다.
* **[Experience Manager Forms에서 reCAPTCHA Enterprise 지원](/help/forms/using/captcha-adaptive-forms.md)**: 기존 Google reCAPTCHA v2 지원에 더해 Experience Manager Forms에서 reCAPTCHA Enterprise에 대한 지원을 추가하여 사기 행위 및 스팸에 대한 보호 기능을 강화했습니다.
* **[Experience Manager Forms에서 정부용 Adobe Acrobat Sign 지원](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**: 이제 AEM Forms이 정부용 Adobe Acrobat Sign과 통합됩니다(FedRAMP 규격). 이 통합은 정부 관련 계정(정부 부서 및 기관)에 대한 적응형 양식 제출을 통해 전자 서명에 대한 고급 수준의 규정 준수 및 보안을 제공합니다. 공공기관용 Adobe Acrobat Sign과 통합하여 Adobe의 파트너와 공공기관 고객들은 가장 중요하고 민감한 비즈니스 라인에서 적응형 양식 전자 서명을 사용할 수 있습니다. 이 보안 계층이 추가되면 Adobe의 공공기관 고객들이 안심할 수 있도록 모든 전자 서명은 FedRAMP Moderate 규정을 완전히 준수해야 합니다.
* **데이터 교환을 위해 Experience Manager Forms과 Salesforce 통합 사용**: OAuth 2.0 클라이언트 자격 증명 흐름을 사용하여 Experience Manager Forms과 Salesforce 애플리케이션 간의 통합을 구성합니다. 이 기능을 통해 안전하고 직접적인 애플리케이션 인증 및 권한 부여가 가능하며 사용자 개입 없이 원활한 통신이 가능합니다.
* **워크플로 엔진의 최적화 및 향상된 기능**: 워크플로 인스턴스 수를 최소화하여 워크플로 엔진의 성능을 향상시킵니다. `COMPLETED` 및 `RUNNING` 상태 값 외에 워크플로에서는 `ABORTED`, `SUSPENDED` 및 `FAILED`의 세 가지 새 상태 값도 지원합니다.

## AEM 6.5, 서비스 팩 16—2023년 2월 23일

Dynamic Media 비디오 게재 시 적응형 비트율 스트리밍을 위해 새 프로토콜 DASH(HTTP를 통한 동적 적응형 스트리밍)가 시작되었습니다(CMAF [공통 미디어 애플리케이션 형식]이 활성화됨).

* 적응형 스트리밍(DASH/HLS)은 비디오에 대한 최종 사용자 시청 환경을 향상시킵니다.
* DASH는 응용 비디오 스트리밍에 대한 국제 표준 프로토콜로서 업계에서 널리 채택되고 있다.
* 현재 아시아 태평양 및 북미에서 이용 가능하며, 유럽-중동-아프리카에서 곧 출시될 예정입니다.

### [!DNL Forms]

* [Headless 적응형 Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)을(를) 사용하면 개발자는 기존의 그래픽 사용자 인터페이스가 아닌 API를 통해 액세스하고 상호 작용할 수 있는 대화형 양식을 만들고 게시하고 관리할 수 있습니다.

* [적응형 Forms 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features)는 Adobe Experience Manager WCM 핵심 구성 요소를 기반으로 구축된 24개의 오픈 소스 BEM 호환 구성 요소 세트입니다. 이러한 구성 요소는 오픈 소스이며 개발자가 조직의 특정 요구 사항에 맞게 이러한 구성 요소를 쉽게 사용자 정의하고 확장할 수 있는 기능을 제공합니다. [WCM 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html)를 사용자 지정할 수 있는 기존 기술을 가진 사용자는 이러한 구성 요소를 쉽게 사용자 지정하고 스타일을 지정할 수 있습니다.

* 이제 OSGi의 Reader 확장 서비스에서 PDF의 가져오기 및 내보내기 사용 권한을 활성화하여 Adobe Acrobat Reader에서 데이터를 가져오거나 내보낼 수 있는 별도의 옵션을 제공합니다.

## AEM 6.5, 서비스 팩 15—2022년 11월 24일

### [!DNL Forms]

* 이제 AEM Forms Designer을 [스페인어 로케일](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에서 사용할 수 있습니다.
* 이제 [OAuth2를 사용하여 Microsoft® Office 365 메일 서버 프로토콜(SMTP 및 IMAP)](/help/forms/using/oauth2-support-for-mail-service.md)을 인증할 수 있습니다.
* [서버에서 다시 유효성 검사](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) 속성을 true로 설정하여 서버측 기록 문서에서 제외할 숨겨진 필드를 식별할 수 있습니다.
* AEM Forms Designer에는 32비트 버전의 Visual C++ 2019 재배포 가능 패키지(x86)가 필요합니다.

## AEM 6.5, 서비스 팩 14 - 2022년 8월 25일

버그만 수정됩니다.

## AEM 6.5, 서비스 팩 13—2022년 5월 26일

* 적응형 양식에서 보이지 않는 CAPTCHA 사용: 이제 의심되는 활동이 있는 경우에만 보이지 않는 CAPTCHA를 사용하여 CAPTCHA 문제를 표시할 수 있습니다. 의심되는 활동이 없는 경우 CAPTCHA 문제가 표시되지 않습니다. 이는 확인란 요구 사항 없이 사람의 양식 완성을 평가하고, 맞춤화 노력을 줄이고, 최종 사용자 경험을 개선하는 데 도움이 됩니다.

* REST 끝점에 대한 양식 데이터 모델 사후 처리기에서 응답 헤더를 가져오는 지원이 추가되었습니다.

* 이제 적응형 양식 번역 파일을 생성할 때 생성된 XLIFF 파일과 동일한 텍스트 시퀀스가 해당 적응형 양식의 구성 요소 시퀀스와 동일합니다.

* 적응형 양식을 현지화하고 기본 언어의 텍스트를 조금만 변경해도 다른 모든 언어에 대한 전체 번역이 누락됩니다. [!DNL Experience Manager] 6.5.13.0에서 문제가 해결되었습니다.

* Forms의 접근성 개선:

   * 화면 판독기에 대한 지원을 추가하여 표의 헤더와 본문을 연속 및 연결 엔티티로 인식합니다. 이 기능은 화면 판독기가 표를 올바르게 탐색하는 데 도움이 됩니다. (NPR-37139)
   * 대화 상자가 열릴 때까지 HTML 작업 영역 탐색을 중단하도록 화면 판독기에 대한 지원을 추가했습니다.

## AEM 6.5, 서비스 팩 12—2022년 2월 24일

* 원격 DAM 및 Sites 배포 간의 연결을 구성한 후에는 Sites 배포에서 원격 DAM의 에셋을 사용할 수 있습니다. 이제 원격 DAM 에셋 또는 폴더에서의 작업을 업데이트하고, 삭제하고, 이름을 바꾸고, 이동할 수 있습니다. 업데이트는 약간의 지연과 함께 Sites 배포에서 자동으로 사용할 수 있습니다.
* 이제 블루프린트 구성 없이도 라이브 카피 소스를 여러 라이브 카피로 푸시-롤아웃할 수 있습니다.
* 이제 진행 중인 비동기 작업의 상태가 사용자 인터페이스에 표시되므로 사용자가 동일한 경로에서 여러 비동기 작업을 실수로 트리거하지 않도록 할 수 있습니다.
* Analytics 2.0 API에 대해 IMS 기반 인증 지원이 제공됩니다.
* JSON 오퍼 유형 경험 조각에 대한 API 지원.
* 이제 IMS의 오퍼 삭제 (경험 조각 API)에 대한 오퍼 요청이 제공됩니다.
* 내장된 저장소(Apache Jackrabbit Oak)는 여전히 1.22.9로 유지됩니다.
