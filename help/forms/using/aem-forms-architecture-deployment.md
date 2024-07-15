---
title: AEM Forms의 아키텍처 및 배포 토폴로지
description: 신규 및 기존 AEM 고객과 LiveCycle ES4에서 AEM Forms으로 업그레이드하는 고객을 위한 AEM Forms 및 권장 토폴로지에 대한 아키텍처 세부 정보.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2469'
ht-degree: 0%

---

# AEM Forms의 아키텍처 및 배포 토폴로지 {#architecture-and-deployment-topologies-for-aem-forms}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html) |
| AEM 6.5 | 이 문서 |

## 아키텍처 {#architecture}

AEM Forms은 AEM as a AEM 패키지에 배포된 애플리케이션입니다. 이 패키지를 AEM Forms 추가 기능 패키지라고 합니다. AEM Forms 추가 기능 패키지에는 AEM OSGi 컨테이너에 배포되는 서비스(API 공급자)와 AEM Sling 프레임워크에서 관리하는 서블릿 또는 JSP(프론트엔드 및 REST API 기능 모두 제공)가 모두 포함되어 있습니다. 다음 다이어그램은 이 설정을 보여 줍니다.

![아키텍처](assets/architecture.png)

AEM Forms용 아키텍처에는 다음 구성 요소가 포함되어 있습니다.

* **핵심 AEM 서비스:** AEM에서 배포된 응용 프로그램에 제공하는 기본 서비스입니다. 이러한 서비스에는 JCR 규격 콘텐츠 저장소, OSGI 서비스 컨테이너, 워크플로 엔진, 신뢰 저장소, 키 저장소 등이 포함됩니다. 이러한 서비스는 AEM Forms 애플리케이션에서 사용할 수 있지만 AEM Forms 패키지에서 제공되지 않습니다. 이러한 서비스는 전체 AEM 스택에서 필수적인 부분이며 다양한 AEM Forms 구성 요소가 이러한 서비스를 사용합니다.
* **Forms 서비스:** PDF 문서 만들기, 조합, 배포, 보관, 디지털 서명을 추가하여 문서에 대한 액세스를 제한하고 바코드 형식을 디코딩하는 등 양식 관련 기능을 제공합니다. 이러한 서비스는 AEM에 공동 배포된 사용자 지정 코드에서 공개적으로 사용할 수 있습니다.
* **웹 계층:** 다음 기능을 제공하는 일반 및 양식 서비스를 통해 빌드된 JSP 또는 서블릿입니다.

   * **작성 프론트엔드**: 양식을 작성 및 관리하기 위한 양식 작성 및 양식 관리 사용자 인터페이스입니다.
   * **양식 렌디션 및 제출 프론트엔드**: AEM Forms의 최종 사용자(예: 정부 웹 사이트에 액세스하는 사용자)가 사용할 최종 사용자 대면 인터페이스입니다. 이렇게 하면 양식 렌디션(웹 브라우저에 양식 표시) 및 제출 기능이 제공됩니다.
   * **REST API**: JSP 및 서블릿은 forms mobile SDK와 같은 HTTP 기반 클라이언트의 원격 사용을 위해 양식 서비스의 하위 집합을 내보냅니다.

**OSGi의 AEM Forms:** OSGi 환경의 AEM Forms은 AEM Forms 패키지가 배포된 표준 AEM 작성자 또는 AEM Publish입니다. [단일 서버 환경, 팜 및 클러스터된 설정](/help/sites-deploying/recommended-deploys.md)에서 OSGi에서 AEM Forms을 실행할 수 있습니다. 클러스터 설정은 AEM 작성자 인스턴스에만 사용할 수 있습니다.

JEE의 **AEM Forms:** JEE의 AEM Forms은 JEE 스택에서 실행 중인 AEM Forms 서버입니다. 애플리케이션 서버에서 실행되는 단일 JEE 스택에 AEM Forms 추가 기능 패키지 및 추가 AEM Forms JEE 기능이 공동 배포된 AEM Author가 포함되어 있습니다. 단일 서버 및 클러스터된 설정에서 JEE에서 AEM Forms을 실행할 수 있습니다. AEM Forms on JEE는 문서 보안, 프로세스 관리를 실행하고 AEM Forms으로 업그레이드하는 LiveCycle 고객을 위해서만 필요합니다. 다음은 JEE에서 AEM Forms을 사용하는 몇 가지 추가 시나리오입니다.

* **HTML 작업 영역 지원(HTML 작업 영역을 사용하는 고객):** JEE의 AEM Forms은 처리 인스턴스로 SSO(Single Sign-On)를 활성화하고, 처리 인스턴스에서 렌더링된 특정 자산을 제공하고, HTML 작업 영역에서 렌더링된 양식의 제출을 처리합니다.
* **고급 추가 양식/대화형 통신 데이터 처리**: 고급 프로세스 관리 기능이 필요한 복잡한 사용 사례에서 양식/대화형 통신 데이터를 추가 처리(및 결과를 적절한 데이터 저장소에 저장)하는 데 JEE의 AEM Forms을 활용할 수 있습니다.

AEM Forms on JEE에는 AEM 구성 요소에 다음과 같은 지원 서비스도 포함되어 있습니다.

* **통합 사용자 관리:** JEE의 AEM Forms 사용자를 OSGi 사용자의 AEM 양식으로 인식할 수 있도록 하고, OSGi와 JEE 사용자 모두에 대해 SSO를 사용하도록 설정합니다. OSGi의 AEM Forms와 JEE의 AEM Forms 간에 단일 사인온이 필요한 시나리오(예: 작업 영역 HTML)에 필요합니다.
* JEE의 **자산 호스팅:** AEM Forms은 OSGi에서 AEM Forms에 렌더링된 자산(예: HTML 5 양식)을 제공할 수 있습니다.

AEM Forms 작성 사용자 인터페이스는 DOR(Document of Record), PDF forms 및 HTML5 Forms 작성을 지원하지 않습니다. 이러한 에셋은 독립 실행형 Forms Designer 애플리케이션을 사용하여 설계되었으며 AEM Forms Manager에 개별적으로 업로드되었습니다. 또는 JEE의 AEM Forms에 대해 양식을 애플리케이션(AEM Forms Workbench에서) 자산으로 디자인하고 JEE 서버의 AEM Forms에 배포할 수 있습니다.

OSGi의 AEM Forms과 JEE의 AEM Forms은 모두 워크플로우 기능을 가지고 있습니다. JEE에 AEM Forms의 본격적인 프로세스 관리 기능을 설치하지 않고도 OSGi의 AEM Forms에서 다양한 작업을 위한 기본 워크플로우를 빠르게 빌드하고 배포할 수 있습니다. OSGi의 AEM Forms에서 양식 중심 워크플로의 [기능과 JEE의 AEM Forms에서 프로세스 관리 기능](capabilities-osgi-jee-workflows.md)에는 약간의 차이가 있습니다. OSGi의 AEM Forms에서 양식 중심의 워크플로우를 개발 및 관리하는 경우 익숙한 AEM Workflow 및 AEM Inbox 기능을 사용합니다.

## 용어 {#terminologies}

다음 이미지에는 일반적인 AEM Forms 배포에 사용되는 다양한 AEM Form 서버 구성 및 해당 구성 요소가 표시됩니다.

![aem_forms_-_recommenddedtopology](assets/aem_forms_-_recommendedtopology.png)

**작성자:** 작성자 인스턴스는 표준 작성자 실행 모드에서 실행되는 AEM Forms 서버입니다. JEE의 AEM Forms 또는 OSGi 환경의 AEM Forms일 수 있습니다. 내부 사용자, 양식 및 대화형 통신 디자이너, 개발자를 위한 것입니다. 이를 통해 다음과 같은 기능을 사용할 수 있습니다.

* **양식 및 대화형 통신 작성 및 관리:** 디자이너와 개발자는 적응형 양식 및 대화형 통신을 만들고 편집할 수 있으며, 외부에서 만든 다른 형식의 양식(예: Forms Designer Adobe에서 만든 양식)을 업로드하고 Forms Manager 콘솔을 사용하여 이러한 에셋을 관리할 수 있습니다.
* 작성자 인스턴스에 호스팅된 **양식 및 대화형 통신 게시:** Assets을 게시 인스턴스에 게시하여 런타임 작업을 수행할 수 있습니다. 자산 게시는 AEM의 복제 기능을 사용합니다. Adobe은 게시된 양식을 처리 인스턴스로 수동으로 푸시하도록 모든 작성자 인스턴스에 복제 에이전트를 구성하고, 수신된 양식을 게시 인스턴스로 자동으로 복제하도록 *수신 시* 트리거를 사용하도록 설정한 처리 인스턴스에 다른 복제 에이전트를 구성할 것을 권장합니다.

**Publish:** 게시 인스턴스는 표준 Publish 실행 모드에서 실행되는 AEM Forms 서버입니다. Publish 인스턴스는 양식 기반 애플리케이션의 최종 사용자(예: 공개 웹 사이트에 액세스하고 양식을 제출하는 사용자)를 위한 것입니다. 이를 통해 다음과 같은 기능을 사용할 수 있습니다.

* 최종 사용자를 위한 Forms 렌더링 및 제출.
* 최종 기록 시스템에서 추가 처리 및 저장을 위해 원시 제출된 양식 데이터를 처리 인스턴스로 전송. AEM Forms에서 제공하는 기본 구현은 AEM의 역방향 복제 기능을 사용하여 이를 달성합니다. 양식 데이터를 로컬로 먼저 저장하는 대신 처리 서버로 직접 푸시하는 대체 구현도 사용할 수 있습니다(후자는 역방향 복제를 활성화하기 위한 전제 조건). 게시 인스턴스에 잠재적으로 민감한 데이터를 저장하는 것에 대한 우려가 있는 고객은 이 [대체 구현](/help/forms/using/configuring-draft-submission-storage.md)을 시작할 수 있습니다. 처리 인스턴스는 일반적으로 더 안전한 영역에 있기 때문입니다.
* 대화형 통신 및 편지 렌더링 및 제출: 대화형 통신 및 편지가 게시 인스턴스에 렌더링되고 해당 데이터가 저장 및 사후 처리를 위해 처리 인스턴스에 제출됩니다. 데이터는 게시 인스턴스에 로컬로 저장하고 나중에 처리 인스턴스(기본 옵션)에 역복제하거나 게시 인스턴스에 저장하지 않고 처리 인스턴스로 직접 푸시할 수 있습니다. 후자의 구현은 보안을 중요하게 생각하는 고객에게 유용합니다.

**처리 중:** forms-manager 그룹에 할당된 사용자가 없는 작성자 실행 모드에서 실행 중인 AEM Forms 인스턴스입니다. JEE에 AEM Forms을 배포하거나 OSGi에 AEM Forms을 처리 인스턴스로 배포할 수 있습니다. 양식 작성 및 관리 활동이 처리 인스턴스에서 수행되지 않고 작성자 인스턴스에서만 발생하도록 사용자에게 할당되지 않습니다. 처리 인스턴스는 다음 기능을 활성화합니다.

* **Publish 인스턴스에서 도착하는 원시 양식 데이터 처리:** 이는 주로 데이터가 도착할 때 트리거되는 AEM 워크플로를 통해 처리 인스턴스에서 수행됩니다. 워크플로에서는 기본 제공되는 양식 데이터 모델 단계를 사용하여 데이터 또는 문서를 적절한 데이터 저장소에 보관할 수 있습니다.
* **양식 데이터의 보안 저장소**: 처리에서는 사용자로부터 격리된 원시 양식 데이터에 대해 방화벽 뒤에 저장소를 제공합니다. 작성자 인스턴스의 양식 디자이너와 Publish 인스턴스의 최종 사용자 모두 이 저장소에 액세스할 수 없습니다.

  >[!NOTE]
  >
  >Adobe은 AEM 저장소를 사용하는 대신 서드파티 데이터 저장소를 사용하여 최종 처리된 데이터를 저장하는 것을 권장합니다.

* **Publish 인스턴스에서 도착하는 서신 데이터의 저장 및 사후 처리:** AEM 워크플로에서는 해당 문자 정의의 선택적 사후 처리를 수행합니다. 이러한 워크플로우는 최종 처리된 데이터를 적합한 외부 데이터 저장소에 저장할 수 있습니다.

* **HTML Workspace 호스팅**: 처리 인스턴스는 Workspace HTML의 프론트엔드를 호스팅합니다. HTML 작업 영역에서는 검토 및 승인 프로세스에 연결된 작업/그룹 지정에 대한 UI를 제공합니다.

다음과 같은 이유로 처리 인스턴스가 작성자 실행 모드에서 실행되도록 구성됩니다.

* Publish 인스턴스에서 원시 양식 데이터를 역복제할 수 있습니다. 기본 데이터 스토리지 핸들러에는 역방향 복제 기능이 필요합니다.
* Publish 인스턴스에서 도착하는 원시 양식 데이터를 처리하는 기본 수단인 AEM 워크플로우는 작성자 스타일 시스템에서 실행하는 것이 좋습니다.

## JEE의 AEM Forms에 대한 샘플 물리적 토폴로지 {#sample-physical-topologies-for-aem-forms-on-jee}

아래에 권장되는 AEM Forms on JEE 토폴로지는 주로 LiveCycle 또는 JEE의 이전 버전의 AEM Forms에서 업그레이드하는 고객을 위한 것입니다. Adobe은 새로 설치하기 위해 OSGi에서 AEM Forms을 사용하는 것을 권장합니다. Document Security 및 프로세스 관리 기능을 사용하는 경우에만 JEE에 AEM Forms을 새로 설치하는 것이 좋습니다.

### 문서 서비스 또는 문서 보안 기능을 사용하기 위한 토폴로지 {#topology-for-using-document-services-or-document-security-capabilities}

document services 또는 document security 기능만 사용하려는 AEM Forms 고객은 아래에 표시된 것과 유사한 토폴로지를 가질 수 있습니다. 이 토폴로지에서는 AEM Forms의 단일 인스턴스를 사용하는 것이 좋습니다. 필요한 경우 AEM Forms 서버의 클러스터 또는 팜을 만들 수도 있습니다. 대부분의 사용자가 프로그래밍 방식으로 AEM Forms 서버의 기능에 액세스하고 사용자 인터페이스를 통한 개입이 최소인 경우 이 토폴로지를 사용하는 것이 좋습니다. 토폴로지는 문서 서비스의 일괄 처리 작업에 유용합니다. 예를 들어 출력 서비스를 사용하여 매일 편집할 수 없는 수백 개의 PDF 문서를 만들 수 있습니다.

AEM Forms을 사용하면 단일 서버에서 모든 기능을 설정하고 실행할 수 있지만 프로덕션 환경에서는 특정 기능에 대해 용량 계획, 로드 밸런싱 및 전용 서버 설정을 수행해야 합니다. 예를 들어, PDF Generator 서비스를 사용하는 환경에서 하루에 수천 페이지를 변환하고 디지털 서명을 추가하여 문서에 대한 액세스를 제한하는 경우 PDF Generator 서비스와 디지털 서명 기능에 대해 별도의 AEM Forms 서버를 설정합니다. 최적의 성능을 제공하고 서로 독립적으로 서버를 확장할 수 있습니다.

![기본 기능](assets/basic-features.png)

### AEM Forms 프로세스 관리 사용을 위한 토폴로지 {#topology-for-using-aem-forms-process-management}

예를 들어 AEM Forms 프로세스 관리 기능을 사용하려는 AEM Forms 고객은 Workspace HTML 와 유사한 토폴로지를 사용할 수 있습니다. JEE의 AEM Forms 서버는 단일 서버 또는 클러스터 구성에 있을 수 있습니다.

LiveCycle ES4에서 업그레이드하는 경우, 이 토폴로지는 JEE의 AEM Forms에 AEM 작성자 기본 제공 기능을 추가하는 것을 제외하고 LiveCycle에 이미 있는 기능과 밀접하게 미러링합니다. 또한 업그레이드를 수행하는 고객의 클러스터링 요구 사항에는 변화가 없습니다. 클러스터된 환경에서 AEM Forms을 사용하는 경우 AEM 6.5 Forms에서 계속 사용할 수 있습니다. HTML Workspace을 사용하기 위해 JEE의 AEM Forms을 새로 설치하려면 JEE 환경에 내장된 AEM 작성자 인스턴스를 실행하는 것이 추가 요구 사항입니다.

양식 데이터 저장소는 양식 및 대화형 통신의 최종 처리 데이터를 저장하는 데 사용되는 타사 데이터 저장소입니다. 이는 토폴로지에서 선택적 요소입니다. 필요한 경우 처리 인스턴스를 설정하고 해당 저장소를 최종 기록 시스템 시스템으로 사용하도록 선택할 수도 있습니다.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

사후 처리, 적응형 양식, HTML 5 양식 및 대화형 통신 기능을 사용하지 않고 프로세스 관리 기능 (AEM Forms HTML Workspace)에 JEE Server의 를 사용하려는 고객에게 토폴로지를 권장합니다.

### 적응형 양식, HTML 5 양식, 대화형 통신 기능 사용을 위한 토폴로지 {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

적응형 양식, HTML5 Forms, PDF forms 등과 같은 AEM Forms 데이터 캡처 기능을 사용할 예정인 AEM Forms 고객은 아래에 표시된 것과 유사한 토폴로지를 가질 수 있습니다. 이 토폴로지는 AEM Forms의 대화형 통신 기능을 사용하는 데에도 권장됩니다.

![forms-osgi-modules를 사용하는 토폴로지](assets/topology-for-using-forms-osgi-modules.png)

위에서 제안한 토폴로지에 다음과 같은 변경/사용자 지정을 수행할 수 있습니다.

* Workspace 및 AEM Forms 앱 HTML을 사용하려면 AEM 작성자 또는 처리 인스턴스가 필요합니다. 추가 외부 AEM 작성자 서버를 설정하는 대신 JEE 서버의 AEM Forms에 내장된 AEM 작성자 인스턴스를 사용할 수 있습니다.
* AEM 작성자 또는 처리 인스턴스는 OSGi의 Forms 중심 워크플로우, 적응형 양식, 양식 포털 및 대화형 통신에만 필요합니다.
* 대화형 통신 에이전트 UI는 일반적으로 조직 내에서 실행됩니다. 따라서 에이전트 UI용 게시 서버를 개인 네트워크 내에 유지할 수 있습니다.
* JEE 서버의 AEM Forms에 내장된 OSGi 인스턴스의 AEM Forms에서도 OSGi 및 감시 폴더에서 Forms 중심 워크플로우를 실행할 수 있습니다.

## OSGi에서 AEM Forms을 사용하기 위한 샘플 물리적 토폴로지 {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### 데이터 캡처, 대화형 통신, OSGi 기능의 양식 중심 워크플로우를 위한 토폴로지 {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

적응형 양식, HTML5 Forms, PDF forms 등과 같은 AEM Forms 데이터 캡처 기능을 사용할 예정인 AEM Forms 고객은 아래에 표시된 것과 유사한 토폴로지를 가질 수 있습니다. 이 토폴로지는 대화형 통신 및 OSGi의 Forms 중심 워크플로 기능을 사용하는 데에도 권장됩니다. 예를 들어, 비즈니스 프로세스 워크플로에 AEM 받은 편지함 및 AEM Forms 앱을 사용하는 경우입니다.

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### 오프라인 일괄 처리를 위해 감시 폴더 기능을 사용하기 위한 토폴로지 {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

일괄 처리에 감시 폴더를 사용할 예정인 AEM Forms 고객은 아래에 표시된 토폴로지와 유사한 토폴로지를 사용할 수 있습니다. 토폴로지에 클러스터된 환경이 표시되지만 로드에 따라 단일 인스턴스 또는 AEM Forms 서버 팜을 사용하기로 결정합니다. 타사 데이터 소스는 자체 레코드 시스템입니다. 감시 폴더의 입력 소스 역할을 합니다. 또한 토폴로지는 인쇄된 파일 형태로 출력을 표시합니다. 출력 컨텐츠를 파일 시스템에 저장하고, 이메일을 통해 전송하고, 다른 사용자 지정 방법을 사용하여 출력을 사용할 수도 있습니다.

![watched-folders를 통한 오프라인 일괄 처리](assets/offline-batch-processing-via-watched-folders.png)

### 오프라인 API 기반 처리를 위해 문서 서비스 기능을 사용하기 위한 토폴로지 {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

document services 기능만 사용하려는 AEM Forms 고객은 아래에 표시된 것과 유사한 토폴로지를 가질 수 있습니다. 이 토폴로지에서는 OSGi 서버에서 AEM Forms 클러스터를 사용하는 것이 좋습니다. 대부분의 사용자가 프로그래밍 방식으로(API 사용) AEM Forms 서버의 기능에 액세스하고 사용자 인터페이스를 통해 개입하는 것이 최소인 경우 이 토폴로지를 사용하는 것이 좋습니다. 이 토폴로지는 여러 소프트웨어 클라이언트 시나리오에서 매우 유용합니다. 예를 들어 여러 클라이언트가 PDF Generator 서비스를 사용하여 요청 시 PDF 문서를 만드는 경우

AEM Forms을 사용하면 단일 서버에서 모든 기능을 설정하고 실행할 수 있지만 프로덕션 환경에서는 특정 기능에 대해 용량 계획, 로드 밸런싱 및 전용 서버 설정을 수행해야 합니다. 예를 들어, PDF Generator 서비스를 사용하여 하루에 수천 페이지의 데이터를 변환하고 여러 적응형 양식을 사용하여 데이터를 캡처하는 환경의 경우, PDF Generator 서비스 및 적응형 양식 기능을 위해 별도의 AEM Forms 서버를 설정하십시오. 최적의 성능을 제공하고 서로 독립적으로 서버를 확장할 수 있습니다.

![오프라인 API 기반 처리](assets/offline-api-based-processing.png)
