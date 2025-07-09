---
title: Adobe Experience Manager 6.5 릴리스의 누적 주요 기능 및 개선 사항.
description: 이전 8개의 서비스 팩 릴리스에서 Adobe Experience Manager 6.5에 포함된 주요 기능 및 개선 사항의 누적 목록입니다.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: eef3ad559612c338de0c4232aadc4133c910aaf8
workflow-type: tm+mt
source-wordcount: '3109'
ht-degree: 13%

---

# 누적 주요 기능 및 개선 사항

이전 8개의 서비스 팩 릴리스에 대한 Adobe Experience Manager 6.5의 주요 기능 및 개선 사항의 누적 목록입니다.

[Adobe Experience Manager 6.5 최신 서비스 팩 릴리스 정보](/help/release-notes/release-notes.md)도 참조하세요.


## AEM 6.5, 서비스 팩 23—2025년 5월 22일

### Forms {#forms-sp23}

* [정적 PDF에서 혼합 텍스트 스타일을 사용하는 액세스 가능한 하이퍼링크](https://helpx.adobe.com/kr/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf): 이제 정적 PDF에서 혼합 텍스트 스타일을 포함하는 하이퍼링크에 액세스 가능한 단일 요소로 태그가 지정됩니다. 이러한 향상된 기능은 태그 트리 구조를 단순화하고, 화면 판독기 탐색을 개선하며, 향상된 접근성 규정 준수를 지원합니다.

* [지원되는 플랫폼 매트릭스를 업데이트했습니다](/help/forms/using/aem-forms-jee-supported-platforms.md)

  최신 버전에서는 지원되는 플랫폼 매트릭스에 대한 업데이트를 도입하여 최신 기술과의 호환성을 보장합니다.

   * IBM® Content Manager 클라이언트 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC 드라이버 12.8

   * Red Hat® Enterprise Linux® 9(커널 4.x, 64비트)

* [파일 첨부 파일 구성 요소 강화](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment): 이제 보안 조치로서 구성 요소가 허용된 파일 형식 검사를 무시하는 수정된 확장자를 가진 파일 제출을 방지합니다. 이러한 파일은 제출 중에 차단되어 유효한 파일 형식만 허용됩니다.

## AEM 6.5, 서비스 팩 22—2024년 11월 21일

### Sites {#sites}

[이제 기능 팩의 응용 프로그램에서 Headless 사용 사례를 위해 AEM 6.5에서 유니버설 편집기](/help/sites-developing/universal-editor/introduction.md)를 사용할 수 있습니다.

### [!DNL Assets]

이제 IPTC 탭에서 [!UICONTROL 대체 텍스트] 및 [!UICONTROL 확장 설명] 텍스트 필드를 지원합니다. (Assets-34918)

### Forms {#forms-sp22}

#### AEM Forms의 새로운 GA 기능 {#ga-aem-forms-sp22}

* [대화형 통신 일괄 처리 API](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel)에서 글꼴 임베딩을 사용할 수 있도록 지원이 추가되었습니다. 이제 대화형 통신에는 일괄 처리 API를 통해 생성된 PDF에 Adobe Ming 및 Adobe Myungjo 글꼴을 포함할 수 있는 지원이 포함됩니다. 이러한 향상된 기능을 통해 글꼴 하위 집합을 사용하는 경우에도 생성된 문서에서 정확한 텍스트 렌더링이 보장되므로 PDF 출력에서 다국어 콘텐츠에 대한 지원이 향상됩니다.

* [PDF 접근성을 위한 목차 API](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) - 이제 OSGi의 AEM Forms에서 새로운 TOC Tag API를 지원하여 접근성 표준을 위한 PDF을 향상시킵니다. 보조 기술을 사용하는 사용자가 PDF에 보다 쉽게 액세스할 수 있도록 해줍니다.

* [조각 XDP 확인](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository) - 이제 OSGi의 AEM Forms이 기본 XDP에서 참조되고 AEM CRX 저장소에 저장된 조각 XDP를 확인합니다.

* [PDF/A 규정 준수 개선 사항](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) - 이제 사용자는 PDF를 보관용으로 PDF/A 형식(1a, 2a, 3a)으로 변환할 수 있으며 접근성을 보장하고 이러한 표준 준수를 확인할 수 있습니다.

* **정적 PDF 문서의 글꼴 자동 크기 조정 지원** - AEM Forms Designer, OutputService 및 FormsService는 이제 정적 PDF의 글꼴 자동 크기 조정을 지원합니다. 텍스트, 숫자, 암호 또는 날짜/시간 필드에 대해 글꼴 크기를 0으로 설정하면 필드의 전체 크기를 변경하지 않고 글꼴 크기가 이러한 필드 내에서 자동으로 조정됩니다. 기능을 사용하려면 사용자가 사용자 지정 XCI에 플래그를 전달합니다. `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`.

#### AEM Forms의 새로운 Beta 기능 {#beta-aem-forms-sp22}

Beta 기능은 혁신적인 최신 기술에 독점적으로 액세스하고 개발 환경을 개선할 수 있는 특별한 기회를 제공합니다. 환경에 Beta 기능을 활성화하는 데 관심이 있습니까? 관심 있는 기능 목록과 함께 공식 주소에서 aem-forms-ea@adobe.com으로 이메일을 보내십시오.

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) 및 [Cloudflare Turnstille CAPTCHA 서비스](/help/forms/using/integrate-adaptive-forms-turnstile.md): AEM Forms에서는 다음 Captcha 서비스를 지원합니다.
   * Captcha는 확인란 위젯으로 사용자에게 도전하여 봇, 스팸 및 자동 남용으로부터 양식을 보호합니다. 인간 사용자만 진행하도록 보장해 온라인 거래에 대한 보안을 강화한다.
   * Cloudflare Turnstile은 자동화된 봇, 악의적인 공격, 스팸 및 원치 않는 자동화된 트래픽으로부터 양식을 보호하기 위한 보안 조치를 제공합니다. 양식 제출을 허용하기 전에 양식 제출에 대한 확인란을 표시하여 사람인지 확인합니다.

* 적응형 양식 버전 관리:
   * [적응형 양식의 여러 버전 만들기](/help/forms/using/add-versioning-reviews-comments.md) - 이제 사용자가 기존 양식의 변형을 쉽게 관리할 수 있습니다. 이 프로세스는 간소화된 단일 워크플로우 내에서 버전 제어를 단순화하고 양식 최적화를 위한 비교를 용이하게 합니다.
   * [적응형 Forms 비교](/help/forms/using/compare-forms-core-components.md): 이제 사용자는 두 양식을 쉽게 비교하여 차이점을 식별할 수 있습니다. 팀원이 수정본을 비교하고 변경 사항을 효율적으로 논의할 수 있도록 하여 원활한 공동 작업을 촉진합니다.

## AEM 6.5, 서비스 팩 21—2024년 6월 6일

### [!DNL Assets]

#### 개선 사항

이제 IPTC 탭에서 [!UICONTROL 대체 텍스트] 및 [!UICONTROL 확장 설명] 텍스트 필드를 지원합니다. (Assets-34918)

#### 접근성

* 에셋의 처리 상태가 실패 또는 메타데이터 실패인 경우 이제 캡션 및 오디오 트랙 UI가 제대로 작동합니다. (Assets-37281)
* 이제 에셋 메타데이터를 저장하고 편집하려고 하면 언어 이름이 표시됩니다. (Assets-37281)

### [!DNL Forms]

* **Oauth 자격 증명 지원**: 기존 서비스 계정(JWT) 자격 증명을 대체하면서 서버 간 인증에 사용할 수 있는 새롭고 쉬운 자격 증명입니다. (NPR-41994)
* [AEM Forms의 규칙 편집기 개선 사항](/help/forms/using/rule-editor-core-components.md):
   * `When-then-else` 기능을 사용하여 중첩된 조건을 구현할 수 있도록 지원합니다.
   * 필드를 포함한 패널 및 양식의 유효성을 검사하거나 재설정합니다.
   * 사용자 지정 함수 내에서 let 및 arrow 함수(ES10 지원)와 같은 최신 JavaScript 기능을 지원합니다.
* [PDF 접근성을 위한 AutoTag API](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services): 이제 OSGi의 AEM Forms에서 태그: 단락 및 목록을 추가하여 접근성 표준을 위한 PDF을 개선하기 위해 새로운 AutoTag API를 지원합니다. 보조 기술을 사용하는 사용자가 PDF에 보다 쉽게 액세스할 수 있도록 해줍니다.
* **16비트 PNG 지원**: 이제 PDF Generator의 ImageToPdf 서비스에서 16비트 색상 깊이의 PNG 변환을 지원합니다.
* **XDP의 개별 텍스트 블록에 아티팩트 적용**: 이제 Forms Designer을 사용하여 사용자가 XDP 파일의 개별 텍스트 블록에 대한 설정을 구성할 수 있습니다. 이 기능을 사용하면 결과 PDF에서 아티팩트로 처리되는 요소를 제어할 수 있습니다. 머리글 및 바닥글과 같은 이러한 요소는 보조 기술에 액세스할 수 있습니다. 주요 기능에는 텍스트 블록을 아티팩트로 표시하고 이러한 설정을 XDP 메타데이터에 포함시키는 작업이 포함됩니다. Forms 출력 서비스는 PDF 생성 중에 이러한 설정을 적용하여 적절한 PDF/UA 태깅을 보장합니다.
* **AEM Forms Designer이 `GB18030:2022` standard로 인증되었습니다**: 이제 `GB18030:2022` 인증을 통해 Forms Designer에서 편집 가능한 모든 필드와 대화 상자에 중국어 문자를 입력할 수 있는 중국어 유니코드 문자 집합을 지원합니다.
* [JEE Server에서 WebToPDF 경로 지원](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings) 이제 PDF Generator 서비스를 사용하여 HTML 파일을 JEE의 PDF 문서로 변환하는 WebToPDF 경로를 지원합니다. 이 지원은 기존 Webkit 및 WebCapture(Windows에만 해당) 경로에 추가됩니다. WebToPDF 경로는 OSGi에서 이미 사용할 수 있고 JEE로 확장되어 있습니다. 이제 JEE 및 OSGi 플랫폼 모두에서 PDF Generator 서비스는 서로 다른 운영 체제에서 다음 경로를 지원합니다.
   * **Windows**: Webkit, WebCapture, WebToPDF
   * **Linux®**: Webkit, WebToPDF


## AEM 6.5, 서비스 팩 20—2024년 2월 22일

### [!DNL Assets]

* Dynamic Media는 이제 Apple iOS/iPadOS에 대해 무손실 HEIC 이미지 형식을 지원합니다. Dynamic Media 이미지 제공 및 렌더링 API에서 [fmt](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt)을(를) 참조하십시오.
* 이제 MSM(Multisite Manager)은 경험 조각을 라이브 카피로 효율적으로 대량 롤아웃하기 위해 폴더 및 하위 폴더를 포함한 경험 조각 구조를 지원합니다.

### [!DNL Forms]

* **JEE의 AEM Forms에서 트랜잭션 보고**: JEE의 AEM Forms에 트랜잭션 보고 기능이 도입되었습니다. 변환, 변환 및 제출과 같은 문서 트랜잭션을 종합적으로 기록할 수 있습니다. 이러한 향상된 기능은 효율성을 향상시키고 기록 보관을 용이하게 합니다. 이 기능은 기본적으로 비활성화되어 있습니다. 관리자 UI에서 활성화할 수 있습니다.
* **ECDSA를 지원하는 향상된 보안**: 이제 AEM Forms은 JEE 및 OSGi 스택 모두에서 ECDSA(Elliptic Curve Digital Signature Algorithm)를 강력하게 지원합니다. 이제 사용자는 강화된 보안을 통해 PDF 문서에 서명, 인증 및 확인할 수 있습니다. 지원되는 EC 곡선 알고리즘은 다음과 같습니다.
   * SHA256 다이제스트 알고리즘을 사용한 ECDSA 타원 곡선 P256
   * SHA384 다이제스트 알고리즘을 사용한 ECDSA 타원 곡선 P384
   * SHA512 다이제스트 알고리즘을 사용한 ECDSA 타원 곡선 P512
* **Forms Designer용 Windows 11과의 원활한 호환성**: AEM Forms Designer은 이제 Windows 11을 지원하므로 원활한 설치 및 작업이 가능합니다. 사용자는 Forms Designer을 다시 설치하거나 호환성 문제에 대한 걱정 없이 Windows 11로 자신 있게 업그레이드할 수 있으므로 워크플로우가 중단되지 않습니다.
* **AEM Forms Designer에서 사용자 지정 &quot;캡션&quot; 역할을 사용하여 접근성을 개선했습니다**: 이제 AEM Forms Designer에는 &quot;캡션&quot;이라는 사용자 지정 접근성 역할이 포함되어 사용자가 개인화된 캡션 요소로 XDP를 만들 수 있습니다. 이 기능을 사용하면 사용자가 사용자 정의 캡션을 문서 디자인에 통합하여 포괄성과 사용자 경험을 향상시킬 수 있으므로 접근성을 향상시킬 수 있습니다.

## AEM 6.5, 서비스 팩 19—2023년 12월 7일

* 사이트 페이지 편집기/이미지 구성 요소 사용자가 원격 Assets Cloud Service의 에셋을 참조할 수 있도록 했습니다. (SITES-13448, SITES-13433)
* 이제 AEM은 목록 보기에서 보다 빠른 프로젝트 탐색을 위해 서버측 정렬을 지원합니다. 프로젝트 노드는 인터페이스에 표시되기 전에 사용자가 선택한 열을 기준으로 정렬됩니다.

### [!DNL Forms]

* **새로운 적응형 양식 핵심 구성 요소**: 양식의 확장성을 높이기 위해 세로 탭, 약관 및 확인란이 추가되었습니다.
   * **[확인란 구성 요소](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)**: 이제 핵심 구성 요소를 기반으로 하는 적응형 양식에 확인란 구성 요소를 포함할 수 있습니다. 이를 통해 사용자는 특정 옵션을 선택하거나 선택 취소하는 이진 선택을 할 수 있습니다. 확인란은 일반적으로 클릭하거나 탭하여 두 가지 상태(선택됨 및 선택 취소됨) 사이를 전환할 수 있는 작은 상자 형태입니다. 확인란은 예/아니요 또는 참/거짓 선택을 표시하는 데 사용되는 일반적인 양식 요소입니다.

   * **[약관 구성 요소](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)**: 이제 핵심 구성 요소 기반 적응형 Forms에 약관 구성 요소가 포함됩니다. 양식 작성자는 이 섹션을 추가하여 사용자에게 서비스, 제품 또는 플랫폼에 대한 약관, 조건 또는 법적 계약을 표시합니다. 이 구성 요소는 양식을 제출하면 동의하는 것으로 간주되는 규칙, 규정 및 의무에 대해 사용자에게 알리도록 설계되었습니다.

     ![세로 탭, 약관 및 확인란 구성 요소](/help/forms/using/assets/forms-components.png)

   * **[세로 탭 구성 요소](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)**: 이제 핵심 구성 요소를 기반으로 하는 적응형 양식은 양식 콘텐츠를 세로 탭 목록으로 구성하여 체계적이고 탐색 가능한 레이아웃을 제공할 수 있습니다. 양식의 세로 탭은 탐색을 단순화하고 콘텐츠를 구성하여 사용자 경험을 향상시킵니다. 이 변수는 양식에 여러 섹션이나 복잡한 정보가 포함되어 있을 때 특히 유용합니다.

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

* **[규칙 편집기에서 사용자 지정 오류 처리기를 사용하여 오류 처리 기능이 개선되었습니다](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)** - 이제 외부 서비스에서 반환된 오류에 대한 응답으로 사용자 지정 함수(클라이언트 라이브러리 사용)를 호출할 수 있습니다. 또한 최종 사용자에게 맞춤 응답을 제공할 수 있습니다. 서비스에서 반환된 오류에 대해 특정 작업을 수행할 수도 있습니다. 예를 들어 특정 오류 코드에 대해 백엔드에서 사용자 지정 워크플로우를 호출하거나 서비스가 중단되었음을 고객에게 알릴 수 있습니다

* **[향상된 Adobe Sign 워크플로 단계](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)** - AEM 워크플로의 Adobe Sign 워크플로 단계는 다음과 같은 향상된 기능을 통해 사용할 수 있습니다.

   * **Adobe Sign에 대한 정부 ID 기반 인증을 통해 보안이 강화되었습니다** - Adobe Acrobat Sign의 정부 ID 기반 인증은 추가 인증 계층을 제공합니다. 사용자가 정부에서 발급한 신분증(운전면허증, 주민등록증, 여권)을 이용해 본인 인증을 할 수 있도록 했다. 신뢰할 수 있는 식별 문서를 사용하여 이 개선된 기능은 서명 프로세스에 신뢰도를 추가하여 보안, 규정 준수 및 사용자 유효성 검사 강화에 필요한 시나리오에 적합합니다.

   * **Adobe Sign 문서에 대한 감사 추적을 사용하여 투명성 향상** - Adobe Sign 문서의 라이프사이클에 대한 자세한 통찰력을 얻으려면 감사 추적 기능을 사용하십시오. 이제 감사 추적을 사용하여 문서와 관련된 모든 작업 및 상호 작용에 대한 포괄적인 레코드를 유지 관리할 수 있습니다. 이러한 작업과 상호 작용에는 각 이벤트에 대한 타임스탬프와 함께 문서를 보고, 편집하고, 서명한 사람이 포함됩니다. 이러한 개선된 기능은 규정 준수를 유지하고, 분쟁을 해결하고, 디지털 계약의 무결성을 보장하는 데 중요합니다.


   * **서명자 이상으로 계약 수신자의 역할 확장** - Adobe Acrobat Sign을 사용하면 계약 수신자의 역할을 서명자 이상으로 확장하여 워크플로 요구 사항에 보다 잘 부합하도록 할 수 있습니다. 활성화된 경우 계약의 각 수신자는 자신의 역할을 개별적으로 구성할 수 있으며 기본값은 서명자입니다.


* **[JEE의 AEM Forms 전체 설치 관리자](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)** - 서비스 팩은 다음을 포함한 여러 가지 새로운 소프트웨어 조합을 지원하는 JEE의 AEM Forms 전체 설치 관리자를 제공합니다.
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

* **Dynamic Media _스냅숏_**&#x200B;을(를) 사용하면 테스트 이미지 또는 Dynamic Media URL을 사용하여 WebP 또는 AVIF 출력, 대역폭 인식 압축 및 장치 픽셀 비율 비율과 같은 이미지 수정자 및 스마트 이미징 최적화를 미리 볼 수 있습니다. 그런 다음 각 설정이 품질 및 파일 크기에 미치는 영향을 즉시 비교할 수 있습니다.
[Dynamic Media 스냅샷](https://experienceleague.adobe.com/ko/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot)을 참조하십시오.
* **Dynamic Media를 사용한 DASH 스트리밍** - Dynamic Media 비디오 게재(CMAF가 활성화됨)에서 적응형 스트리밍을 위해 새로운 프로토콜(DASH - HTTP를 통한 동적 적응형 스트리밍)이 시작되었습니다. 현재 모든 지역에서 사용할 수 있습니다.
* **Experience Manager Sites 및 컨텐츠 조각과 Assets 차세대 Dynamic Media 통합** - 사용자는 이제 Experience Manager Sites 6.5에서 클라우드 호스팅 자산을 사용할 수 있습니다. 온프레미스 또는 Managed Services 인스턴스에서 이러한 에셋을 작성하고 전달할 수 있습니다.

### [!DNL Forms]

* **[AEM 페이지 편집기 내의 적응형 Forms](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** - 이제 AEM 페이지 편집기를 사용하여 여러 양식을 만들어 사이트 페이지에 빠르게 추가할 수 있습니다. 이 기능을 통해 콘텐츠 작성자는 동적 비헤이비어, 유효성 검사, 데이터 통합, 기록 문서 생성 및 비즈니스 프로세스 자동화 등 적응형 양식 구성 요소의 기능을 사용하여 Sites 페이지에서 원활한 데이터 캡처 경험을 만들 수 있습니다. 다음과 같은 작업을 수행할 수 있습니다.
   * 양식 구성 요소를 AEM Sites 편집기 또는 경험 조각의 적응형 Forms 컨테이너 구성 요소로 끌어다 놓아 적응형 양식을 만드십시오.
   * AEM Sites 편집기 내의 적응형 Forms 마법사를 사용하여 모든 Sites 페이지와 독립적인 양식을 만들 수 있으므로 여러 페이지에서 이러한 양식을 자유롭게 재사용할 수 있습니다.
   * Sites 페이지에 여러 양식을 추가하여 사용자 경험을 간소화하고 더 많은 유연성을 제공합니다.
* **[Experience Manager Forms에서 reCAPTCHA Enterprise 지원](/help/forms/using/captcha-adaptive-forms.md)** - Experience Manager Forms에서 reCAPTCHA Enterprise 지원이 추가되었습니다. 이 기능은 기존 Google reCAPTCHA v2 지원 외에도 사기 활동 및 스팸에 대한 향상된 보호 기능을 제공합니다.
* **[Experience Manager Forms과 정부용 Adobe Acrobat Sign에 대한 지원이 추가되었습니다](/help/forms/using/adobe-sign-integration-adaptive-forms.md)** - 이제 AEM Forms을 정부용 Adobe Acrobat Sign과 통합(FedRAMP 규격)합니다. 이 통합은 정부 관련 계정(정부 부서 및 기관)에 대한 적응형 양식 제출을 통해 전자 서명에 대한 고급 수준의 규정 준수 및 보안을 제공합니다. Adobe Acrobat Sign for Government와의 통합을 통해 Adobe 파트너 및 정부 고객은 적응형 Forms에서 전자 서명을 사용하여 가장 미션 크리티컬하고 민감한 비즈니스 라인 중 일부를 수행할 수 있습니다. 이 보안 계층이 추가되면 Adobe의 공공기관 고객들이 안심할 수 있도록 모든 전자 서명은 FedRAMP Moderate 규정을 완전히 준수해야 합니다.
* **데이터 교환을 위해 Experience Manager Forms과 Salesforce 통합 사용** - OAuth 2.0 클라이언트 자격 증명 흐름을 사용하여 Experience Manager Forms과 Salesforce 애플리케이션 간의 통합을 구성합니다. 이 기능을 통해 안전하고 직접적인 애플리케이션 인증 및 권한 부여가 가능하며 사용자 개입 없이 원활한 통신이 가능합니다.
* **워크플로 엔진의 최적화 및 향상된 기능**: 워크플로 인스턴스 수를 최소화하여 워크플로 엔진의 성능을 향상시킵니다. `COMPLETED` 및 `RUNNING` 상태 값 외에 워크플로에서는 `ABORTED`, `SUSPENDED` 및 `FAILED`의 세 가지 새 상태 값도 지원합니다.

## AEM 6.5, 서비스 팩 16—2023년 2월 23일

Dynamic Media 비디오 게재 시 적응형 비트율 스트리밍을 위해 새 프로토콜 DASH(HTTP를 통한 동적 적응형 스트리밍)가 시작되었습니다(CMAF [공통 미디어 애플리케이션 형식]이 활성화됨).

* 적응형 스트리밍(DASH/HLS)은 비디오에 대한 최종 사용자 시청 환경을 향상시킵니다.
* DASH는 응용 비디오 스트리밍에 대한 국제 표준 프로토콜로서 업계에서 널리 채택되고 있다.
* 현재 아시아 태평양 및 북미에서 이용 가능하며, 유럽-중동-아프리카에서 곧 출시될 예정입니다.

### [!DNL Forms]

* [Headless 적응형 Forms](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/overview)을(를) 사용하면 개발자는 기존의 그래픽 사용자 인터페이스가 아닌 API를 통해 액세스하고 상호 작용할 수 있는 대화형 양식을 만들고 게시하고 관리할 수 있습니다.

* [적응형 Forms 핵심 구성 요소](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#features)는 Adobe Experience Manager WCM 핵심 구성 요소를 기반으로 구축된 24개의 오픈 소스 BEM 호환 구성 요소 세트입니다. 이러한 구성 요소는 오픈 소스이며 개발자가 조직의 특정 요구 사항에 맞게 이러한 구성 요소를 쉽게 사용자 정의하고 확장할 수 있는 기능을 제공합니다. [WCM 핵심 구성 요소](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/get-started/authoring)를 사용자 지정할 수 있는 기존 기술을 가진 사용자는 이러한 구성 요소를 쉽게 사용자 지정하고 스타일을 지정할 수 있습니다.

* 이제 OSGi의 Reader 확장 서비스에서 PDF의 가져오기 및 내보내기 사용 권한을 활성화하여 Adobe Acrobat Reader에서 데이터를 가져오거나 내보낼 수 있는 별도의 옵션을 제공합니다.
