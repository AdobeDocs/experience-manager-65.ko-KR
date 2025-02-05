---
title: AEM Forms 용어
description: AEM Forms 용어집은 Adobe Experience Manager Forms(AEM Forms)에서 사용되는 주요 용어, 정의 및 개념의 포괄적인 목록을 제공하여 사용자가 적응형 양식 및 관련 기능을 이해하고 작업할 수 있도록 지원합니다.
feature: Adaptive Forms
role: Admin, User, Developer
hidefromtoc: true
hide: true
source-git-commit: 37f471e09c13b7ab036ab1043d11dfed98da1d97
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 1%

---

# AEM Forms 용어

## [적응형 양식](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form)

사용자의 장치 및 입력을 기반으로 레이아웃과 프레젠테이션을 조정하여 다양한 플랫폼에서 사용자 경험을 향상시키는 동적이고 반응형 양식입니다. 조건부 논리, 동적 데이터 바인딩 및 규칙 기반 비헤이비어를 포함합니다.

## [적응형 양식 버전 관리](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/add-versioning-reviews-comments)

JCR 노드 버전 관리를 사용하여 저장소에서 여러 버전의 양식을 관리할 수 있습니다. 적응형 양식의 감사 추적 및 쉬운 롤백을 보장합니다.

## [Adobe Analytics Forms 통합](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation)

Adobe Analytics을 사용한 사용자 상호 작용(예: 필드 드롭오프, 섹션당 체류 시간)에 대한 자세한 통찰력을 제공하여 데이터 기반의 양식 디자인 최적화를 가능하게 합니다.

## [AEM Forms 추가 기능 패키지](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)

AEM(Adobe Experience Manager)에 패키지로 배포되는 응용 프로그램으로, AEM Sling 프레임워크에서 관리되는 서비스(API 공급자)와 서블릿 또는 JSP가 포함되어 있습니다.

## [JEE의 AEM Forms](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)

JEE(Java Enterprise Edition) 서버를 활용하는 AEM Forms의 배포 옵션으로, 엔터프라이즈급 확장성, 트랜잭션 관리 및 복잡한 엔터프라이즈 워크플로우에 대한 지원을 제공합니다.

## [OSGi의 AEM Forms](https://experienceleague.adobe.com/ko/docs/experience-manager-65/content/implementing/deploying/introduction/technical-requirements)

OSGi 환경의 AEM Forms은 AEM Forms 패키지가 배포된 표준 AEM Author 또는 AEM Publish입니다. 단일 서버 환경, 팜 및 클러스터된 설정에서 OSGi에서 AEM Forms을 실행할 수 있습니다. 클러스터 설정은 AEM 작성자 인스턴스에만 사용할 수 있습니다.

## [AEM Forms의 Adobe Sign](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms)

안전하고 원활한 디지털 서명 워크플로를 위한 RESTful 서비스. OAuth 기반 인증을 사용하여 AEM Forms과 통합되므로 자동화된 서명 수집과 실시간 추적이 가능합니다.

## [AEM Forms 문서 서비스 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services)

Forms 모바일 SDK과 같이 HTTP 기반 클라이언트의 원격 사용을 위해 AEM Forms 웹 계층에서 제공하는 API.PDF 문서의 생성, 어셈블리, 배포 및 보관, 디지털 서명 추가, Barcoded Forms의 디코딩을 가능하게 하는 AEM Forms 내의 기능입니다.

| **서비스 이름** | **설명** | **설명서 링크** |
|------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Forms 서비스** | 템플릿과 XML을 사용하여 PDF forms을 렌더링하고, 가져오기/내보내기를 위해 양식 데이터를 통합하고, 조각 기반 렌더링을 지원합니다. | [Forms 서비스 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **출력 서비스** | PDF, PCL 또는 PostScript과 같은 형식의 템플릿과 데이터를 병합하여 문서를 생성합니다. | [출력 서비스 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **어셈블러 서비스** | PDF 및 XDP 문서를 결합하고, 재정렬하고, 검증하고, 보완합니다. | [어셈블러 서비스 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/assembler-service) |
| **ConvertPDF 서비스** | PDF 문서를 PostScript 또는 PNG, JPEG 또는 TIFF과 같은 이미지 형식으로 변환합니다. | [ConvertPDF Service 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/using-convertpdf-service) |
| **바코드된 Forms 서비스** | TIFF 및 PDF 파일의 바코드에서 데이터를 추출하여 데이터 캡처 프로세스를 자동화합니다. | [바코드된 Forms 서비스 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/using-barcoded-forms-service) |
| **DocAssurance 서비스** | 문서 보안 정책을 암호화, 암호 해독, 디지털 서명 및 PDF에 적용합니다. | [DocAssurance 서비스 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services#doc-assurance-service) |
| **PDF Generator 서비스** | 기본 파일 형식(예: Microsoft Word, Excel)을 PDF 문서로 변환합니다. | [PDF Generator 서비스 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/aem-document-services-programmatically#pdfgeneratorservice) |

## [Forms as a Cloud Service 통신 API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction)

AEM Formsas a Cloud Service 는 양식 및 워크플로우 관리를 위한 고급 도구를 제공하며 원활한 디지털 양식 작성 및 개인화된 커뮤니케이션을 지원합니다. Cloud Communication API는 안전한 온디맨드 및 일괄 문서 생성, 조작, 유효성 검사 및 HTTP를 통한 외부 시스템과의 통합을 제공하여 효율적이고 안전한 작업을 보장합니다.

| **서비스 이름** | **설명** | **설명서 링크** |
|-------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **문서 생성** | 템플릿(XFA 또는 PDF)을 XML 데이터와 결합하여 PS, PCL, DPL, IPL 및 ZPL 형식과 같은 PDF 및 인쇄 형식의 문서를 생성합니다. | [문서 생성 설명서](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html#document-generation) |
| **문서 조작** | PDF 문서를 결합하고 재배열합니다. | [문서 조작 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation) |
| **문서 변환** | PDF을 PDF/A로 전환하고 PDF/A 준수 여부를 확인합니다. | [문서 변환 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-conversion) |
| **문서 Assurance** | 서명 필드 추가 또는 제거, 서명, 인증, 암호화, 암호 해독 및 사용 권한 PDF 문서에 적용. | [Assurance 문서](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#doc-assurance) |
| **디지털 서명** | 양식 및 문서의 보안 전자 서명을 위해 Adobe Sign을 통합합니다. | [디지털 서명 설명서](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html#digital-signatures) |


## [AEM Forms Workbench](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/install-workbench)

워크플로 제작, 편집 및 배포와 양식 중심의 비즈니스 프로세스 관리를 위한 데스크탑 애플리케이션입니다. 백엔드 서비스 및 시스템과 통합됩니다.

## [원형](https://experienceleague.adobe.com/ko/docs/experience-manager-core-components/using/developing/archetype/overview)

표준화, 빠른 설정 및 AEM 개발 모범 사례 준수를 용이하게 하는 사전 정의된 구조의 새 프로젝트를 생성하는 데 사용되는 AEM의 템플릿 또는 패턴입니다.

## [작성자 인스턴스](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

콘텐츠 작성자 및 관리자가 콘텐츠를 게시하기 전에 콘텐츠를 디자인하고 만들고 관리하는 환경입니다. 버전 관리, 미리보기 및 테스트를 지원합니다.

## [작성 프론트엔드](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

AEM Forms 내에서 양식을 작성 및 관리하기 위한 사용자 인터페이스입니다.

## [적응형 양식 블록](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-references/form-components)

관련 구성 요소 및 메타데이터를 논리적으로 그룹화하는 캡슐화 단위로, 동적 데이터 처리를 가능하게 하며, 여러 단계 형식으로 손쉽게 확장할 수 있습니다.

## [핵심 구성 요소](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction)

양식 필드, 레이아웃 컨테이너, 단추 및 기타 대화형 요소를 포함하여 양식을 작성할 수 있는 즉시 사용 가능한 빌딩 블록입니다.

## [서신 관리](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/letters-correspondences/cm-overview)

비즈니스에서 사전 정의된 템플릿, 규칙 및 데이터 소스를 사용하여 개인화된 서신을 만들고, 관리하고, 전달할 수 있는 모듈입니다. 편지 템플릿, 고객 커뮤니케이션 및 배치 생성을 포함합니다.

## [CRX(Content repository extreme)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-aem-forms-workspace/html-workspace-architecture)

정형 및 비정형 데이터를 저장하는 AEM의 내장 JCR(Java Content Repository). 컨텐츠, 템플릿 및 구성의 계층적 저장을 가능하게 합니다.

## [사용자 지정 구성 요소](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/customize-adaptive-forms-core-components)

Sling 모델, Sightly(HTL) 및 Java를 사용하여 개발된 AEM Forms 기능을 확장하는 맞춤형 구성 요소입니다. 일반적으로 고유한 비즈니스 논리 또는 고급 클라이언트측 상호 작용에 사용됩니다.

## [사용자 지정 XCI(XML 구성 정보)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/configure-forms/specifying-xci-configuration-options)

Adobe Experience Manager(AEM) Forms에서 관리자는 사용자 지정 XCI(XML 구성 정보) 파일을 사용하여 양식 및 문서에 대한 특정 렌더링 속성을 정의할 수 있습니다. 관리 콘솔에서 XCI 설정을 구성하면 사용자 지정 옵션으로 시스템 기본값을 대체할 수 있으므로 맞춤형 처리 및 양식 표시가 보장됩니다.

## [데이터 통합](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/form-data-model/data-integration)

데이터베이스, 웹 서비스 또는 REST API와 같은 외부 데이터 소스를 양식 및 워크플로우에 원활하게 통합하여 동적이고 개인화된 사용자 경험을 가능하게 합니다.

## [데이터 원본](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/form-data-model/configure-data-sources)

관계형 데이터베이스의 JDBC, 웹 서비스의 REST 끝점, SAP 시스템의 OData 등 외부 데이터를 양식에 통합하는 인터페이스입니다. AEM Forms 데이터 통합 프레임워크를 통해 관리됩니다.

## [문서 단편](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/letters-correspondences/lists)

일관성을 보장하기 위해 양식 또는 서신에 동적으로 포함될 수 있는 머리글, 바닥글, 면책조항 또는 조항과 같은 문서의 재사용 가능한 구성 요소입니다.

## [기록 문서(DoR)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms)

제출된 양식의 편집 불가능한 보관 버전(일반적으로 PDF 형식)을 생성하는 AEM Forms의 기능으로, 정확한 컨텐츠 및 레이아웃을 트랜잭션 기록으로 유지합니다.

## [Edge Delivery Services](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/edge-delivery/overview)

AEM Forms에 최적화된 컨텐츠 제공을 통해 작성자가 컨텐츠를 빠르게 업데이트하고 게시할 수 있는 양식, 테마 및 클라이언트 라이브러리와 같은 자산에 대한 지연 시간을 줄일 수 있습니다.

## [Forms 통합](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/form-data-model/data-integration)

OSGi 번들 및 커넥터를 사용하여 AEM Forms을 엔터프라이즈 시스템(예: SAP, Salesforce)에 연결하여 양방향 데이터 흐름 및 실시간 업데이트를 지원합니다.

## [양식 검토](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms)

관련자가 게시 전에 적응형 양식을 검토하고 주석을 추가하고 변경 사항을 승인할 수 있는 워크플로우 기반 기능입니다. AEM 받은 편지함 및 작업 관리를 사용합니다.

## [양식 데이터 모델(FDM)](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model)

적응형 양식을 백엔드 데이터 소스에 연결하여 RESTful 웹 서비스, SOAP 서비스 및 OData와의 통합을 가능하게 하는 표시 계층입니다. FDM을 사용하면 양식 작성자가 양식 필드를 백엔드 데이터 구조에 직접 매핑하여 외부 시스템과 사용자 입력을 원활하게 동기화할 수 있습니다.

## [양식 로컬라이제이션](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization)

여러 언어 및 지역 설정을 지원하기 위한 적응형 양식 프로세스를 통해 다양한 대상자가 양식에 액세스하고 사용자 친화적으로 사용할 수 있습니다.

## [양식 포털](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-forms-portal/creating-form-portal-page)

Forms 포털 구성 요소는 웹 개발자에게 Adobe Experience Manager(AEM)를 사용하여 작성된 웹 사이트에서 Forms 포털을 만들고 사용자 지정할 수 있는 구성 요소를 제공합니다. 이를 통해 사용자는 웹 및 모바일 플랫폼에서 양식을 효율적으로 검색, 액세스 및 제출할 수 있습니다.

## [양식 렌디션 및 제출 프론트엔드](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

사용자가 웹 브라우저를 통해 양식을 보고 제출할 수 있도록 해 주는 AEM Forms의 최종 사용자 인터페이스입니다.

## [양식 설정](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/html5-forms/formset-in-aem-forms)

사용자에게 단일 엔티티로 제시되도록 함께 그룹화된 관련 양식 컬렉션으로, 복잡한 데이터 수집 프로세스를 관리 가능한 섹션으로 분류할 수 있습니다.

## [Forms Designer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/installing-configuring-designer)

XDP 양식으로 양식 템플릿을 디자인하고 AEM Forms에서 사용하여 기록 문서를 생성하는 데 사용되는 독립 실행형 애플리케이션입니다.

## [Forms 중심 워크플로](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow)

문서 승인, 컨텐츠 게시 또는 사용자 알림과 같은 비즈니스 프로세스를 관리하는 AEM Forms의 자동화된 또는 수동 단계 세트입니다.

## [대화형 통신](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/getting-started/interactive-communications-overview)

고도로 개인화된 멀티채널 커뮤니케이션을 관리하기 위한 맞춤형 구현. CRM 또는 ERP 시스템과 같은 다양한 소스의 데이터를 결합하여 웹, 모바일, 이메일 및 인쇄와 같은 다양한 형식의 통신을 제공합니다.

## [JCR(Java Content Repository)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr)

컨텐츠, 구성 및 메타데이터를 AEM에 저장하는 계층형 표준 기반 저장소로, 정형 및 비정형 데이터 스토리지를 지원합니다.

## [편지](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/letters-correspondences/create-letter#create-a-letter-template)

AEM Forms 문서 서비스를 활용하여 고객 커뮤니케이션을 생성합니다. 편지는 XDP 템플릿, 데이터 모델 및 재사용 가능한 조각의 조합을 사용하여 생성되므로 대량 시나리오에서 확장성을 보장합니다.

## [AEM Forms의 메타데이터](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/manage-form-metadata)

메타데이터를 통해 효율적인 에셋 분류 및 검색 가능 AEM Forms에는 각 에셋 유형에 대해 사전 정의된 메타데이터가 포함되어 있으며 사용자 지정을 허용합니다. 또한 메타데이터를 원활하게 생성, 관리 및 교환할 수 있는 툴을 제공합니다.

## [PDF Generator](https://experienceleague.adobe.com/en/docs/experience-manager-learn/forms/document-services/using-pdfg-in-aem-forms)

다양한 파일 형식(예: Word, Excel, PowerPoint)을 PDF 문서로 변환하고 암호화, 워터마크 지정 및 병합과 같은 기능을 제공하는 AEM Forms의 도구입니다.

## [Publish 인스턴스](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

최종 사용자에게 라이브 컨텐츠를 제공하는 AEM의 환경입니다. 최적화된 성능으로 양식, 페이지 및 기타 디지털 경험을 제공합니다.

## [규칙 편집기](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components)

작성자가 코딩 전문 지식 없이도 가시성, 유효성 검사 및 데이터 미리 채우기와 같은 양식 필드에 대한 사용자 지정 규칙 및 논리를 정의할 수 있는 적응형 Forms의 시각적 도구입니다.

## [스크리블 서명](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble)

사용자가 마우스 또는 터치 지원 장치를 사용하여 양식에 직접 서명을 그려 양식에 전자 방식으로 서명할 수 있는 AEM Forms의 기능입니다.

## [AEM Forms에서 동작 제출](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/configuring-submit-actions)

양식 제출 시 실행되는 서버측 또는 클라이언트측 작업입니다. 예로는 REST API 호출, 워크플로우 호출 또는 JCR(Java Content Repository)에 데이터 쓰기가 있습니다.

## [테마](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components)

전처리기용으로 LESS/SASS를 활용하여 적응형 양식에 적용되는 CSS 기반 스타일 프레임워크. 테마는 브랜딩 지침 및 접근성 표준을 준수하도록 하며 테마를 사용자 정의하고 디자인 요소, 레이아웃, 색상, 타이포그래피 및 경우에 따라 기본 코드를 변경할 수 있습니다.

## [템플릿](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components)

구조 요소(필드, 레이아웃) 및 사전 구성된 스크립트로 구성된 적응형 양식의 블루프린트에서 새 템플릿을 만들고 사용자 지정하거나 기존 기본 템플릿을 사용할 수 있습니다.

## [웹 계층](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

일반 및 양식 서비스 위에 구축된 JSP 또는 서블릿을 포함하여 프론트엔드, 양식 렌디션 및 제출 프론트엔드, REST API 작성과 같은 기능을 제공합니다.

## [XDP(XML 데이터 패키지)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/get-xdp-pdf-documents-aem)

동적 콘텐츠와 상호 작용을 지원하면서 PDF 또는 HTML으로 렌더링할 수 있도록 양식을 디자인하고 구조화하기 위해 AEM Forms에서 사용되는 파일 형식입니다.

## [XFA(XML Forms 아키텍처)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-an-xfa-form-template)

대화형 및 동적 PDF forms을 만드는 레거시 기술입니다. XFA Forms를 사용하면 동적 레이아웃 조정, 스크립팅 및 백엔드 시스템과의 원활한 통합과 같은 고급 기능을 사용할 수 있습니다.

## [XML 또는 JSON 스키마](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-xml-or-json-schema)

양식 및 워크플로우에서 XML 또는 JSON 데이터의 형식 및 구성을 정의하는 데 사용되는 표준화된 구조입니다. 이러한 스키마는 일관된 데이터 처리를 보장하며 외부 시스템과의 상호 운용성을 가능하게 합니다.

<!--

## **Custom Properties**  

Developer-defined metadata attributes added to components or forms for advanced behaviors, accessed via Sling APIs or Groovy scripts for dynamic processing.

## **Embedding** 

Integrating adaptive forms into AEM Sites or external web pages using `<iframe>` or SPA (Single Page Application) models. Embedding supports seamless session handling and cross-origin resource sharing (CORS).

## **CDN (Content Delivery Network)**  

Distributed networks (e.g., Akamai) used for caching and delivering forms-related resources, ensuring high availability and faster load times for geographically distributed users.


## **Dispatcher**  

An AEM caching and load balancing tool configured to optimize delivery of adaptive forms. Its filter rules ensure secure access control while caching frequently accessed forms and assets.

## **Editors**  

Tools like the Adaptive Forms Editor, Theme Editor, and Rule Editor, enabling developers and content authors to customize forms and their behavior without extensive coding.

## **Responsive UI**  

An implementation of media queries and flexible grids, ensuring adaptive forms render seamlessly across various screen sizes and devices.

## **Custom Functions**  

JavaScript-based utilities or REST microservices that provide additional logic (e.g., complex field validation or data pre-population), extending the out-of-the-box capabilities of AEM Forms.

## **Package Manager**  

AEM's CRX Package Manager facilitates importing/exporting adaptive forms, data schemas, or configurations as .zip files, enabling modular deployment in distributed environments.

## **UE (User Experience)**  

Design principles and optimizations applied in AEM Forms to enhance usability, including accessibility features (ARIA roles, tab navigation) and intuitive layouts.

## **Forms Submission Services**

Back-end services for handling form submissions, integrating with the AEM Workflow engine, third-party APIs, or direct JCR persistence.


Foundation components
e-signing
adobe sign
letters
submit action
data sources
adaptive form block
edge delivery services
forms integration
custom component 
themes
template 
custom properties
embedding
CDN
Dispatcher
editors
responsive UI
custom functions
package manager
communication APIs
UE
Forms submission services
Form review
Forms Versioning
Adobe analytics forms integration specific

## **AEM Forms Foundation Components**  
Core reusable elements within AEM Forms, built on Granite UI, enabling developers to create complex forms. They provide robust features like data bindings, field validations, and support for multilingual content.


## **e-Signing**  
An implementation of digital signature standards (e.g., PKCS #7) within AEM Forms, integrated with Adobe Sign APIs to ensure secure and legally binding electronic signatures.

## Workspace

A browser-based interface for users to interact with AEM Forms workflows, tasks, and approvals.

## Sling

A REST-based web framework used in AEM to map request URLs to content resources, enabling efficient content rendering and delivery.

-->
