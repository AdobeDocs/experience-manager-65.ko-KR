---
title: 기본 구성 개념
seo-title: 기본 구성 개념
description: AEM 구성 방법을 알아봅니다.
seo-description: AEM 구성 방법을 알아봅니다.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
translation-type: tm+mt
source-git-commit: 8f35717324cd2c1524fb2cf931b3ce21be05729a
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 1%

---


# 기본 구성 개념{#basic-configuration-concepts}

AEM(Adobe Experience Manager)은 &quot;즉시 실행&quot;할 수 있는 모든 매개 변수에 대한 기본 설정과 함께 설치됩니다. 그러나 특정 요구 사항에 맞게 AEM을 구성할 수 있습니다.

AEM에는 다음과 같은 다양한 측면을 구성할 수 있습니다.

* 일부 프로젝트는 [일반적으로 모든 프로젝트 설치](#primary-configuration-considerations)에 대해 구성되며 프로젝트에 해당 사항이 적용되는지 여부를 확인하기 위해 검토해야 합니다.
* [추가 구성](#further-configuration-considerations) 은 반드시 필요하지 않지만 일반적일 수 있습니다.기능 또는 시스템 성능 및 안정성과 관련된 것입니다.
* AEM의 특정 옵션 기능에만 필요한 경우도 있습니다(해당 기능과 함께 문서화되어 있음).

특정 구성에 따라 다음 중 하나를 사용하여 변경할 수 있습니다.

* **Adobe CQ 웹 콘솔**

   OSGi 번들 및 서비스를 구성하기 위한 표준 위치입니다.

   자세한 내용 및 권장 방법은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성을 참조하십시오.

* **저장소**

   저장소에서 OSGi 구성의 하위 세트를 사용할 수 있습니다. 이렇게 하면 저장소 내용을 복사 또는 복제하면 동일한 구성이 다시 만들어집니다. 또한 실행 모드에 따라 고유한 구성을 저장소에 추가할 수도 있습니다.

   자세한 내용은 [저장소](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)의 OSGi 구성 및 특히 [저장소](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)에 새 구성 추가를 참조하십시오.

* **파일 시스템**

   파일 시스템에 몇 개의 구성 파일이 있습니다.

* **AEM WCM**

   AEM WCM 자체에서 다양한 측면을 구성할 수 있으며, 많은 기능이 [도구](/help/sites-administering/tools-consoles.md) 콘솔을 사용합니다.예: 복제 에이전트.

>[!NOTE]
>
>Adobe Experience Manager을 사용하여 작업할 때 OSGi 서비스(콘솔 또는 저장소 노드)에 대한 구성 설정을 관리하는 방법은 여러 가지가 있습니다.
>
>자세한 내용은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성을 참조하십시오.

>[!NOTE]
>
>AEM 구성은 간단하지만 다음을 인지해야 합니다.
>
>특정 변경 사항은 응용 프로그램에 큰 영향을 줄 수 있습니다. 따라서 AEM 구성을 시작하기 전에 필요한 경험과 지식이 있는지 확인하고 필요한 변경 사항만 적용해야 합니다. OSGi 콘솔을 통해 수행한 모든 변경 사항은 **즉시**&#x200B;실행 중인 시스템에 적용됩니다(다시 시작할 필요 없음).

## 기본 구성 고려 사항 {#primary-configuration-considerations}

이 목록은 모든 새 프로젝트에 대해 일반적으로 구성된 기본 영역을 자세히 설명합니다. 모든 것이 필요한 것은 아니지만 프로젝트에 적용되는 사항을 확인하려면 목록을 읽고 검토해야 합니다.

이 목록은 전체 세부 정보를 제공하는 페이지에 대한 링크와 함께 각 구성 측면에 대한 간단한 개요를 제공합니다.

### Security 검사 목록 {#security-checklist}

[보안 검사 목록](/help/sites-administering/security-checklist.md)에 몇 가지 주요 구성 문제가 나열되어 있습니다. 이 내용을 읽고 설치에 필요한 조치를 취하십시오.

### 기본 UI 구성 - 터치에 적합한 또는 클래식 {#configuring-the-default-ui-touch-optimized-or-classic}

AEM에서 사용할 수 있는 UI는 두 가지가 있습니다.

* 터치에 적합한 UI
* 클래식 UI

[루트 매핑](/help/sites-deploying/osgi-configuration-settings.md)을(를) 사용하여 필요한 UI를 구성할 수 있습니다.

>[!NOTE]
>
>UI 선택에 대한 자세한 내용은 [UI 선택](/help/sites-authoring/select-ui.md)을 참조하십시오.

### IPv4 및 IPv6 {#ipv-and-ipv}

AEM의 모든 요소(예: 저장소, 디스패처 등)는 IPv4 및 IPv6 네트워크 모두에 설치할 수 있습니다.

특별한 구성이 필요하지 않으므로 작업이 완벽합니다. 필요할 경우 네트워크 유형에 적합한 형식을 사용하여 IP 주소를 간단히 지정할 수 있습니다.

즉, IP 주소를 지정해야 할 경우 다음 중에서 선택할 수 있습니다(필요에 따라).

* IPv6 주소

   예 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 주소

   예 `https://123.1.1.4:4502`

* 서버 이름

   예, `https://www.yourserver.com:4502`

* `localhost`의 기본 사례는 IPv4 및 IPv6 네트워크 설치에 대해 해석됩니다.

   예, `http://localhost:4502`

### 버전 제거 {#version-purging}

표준 설치 AEM에서는 페이지를 활성화할 때마다(컨텐츠를 업데이트한 후) 페이지 또는 노드의 새 버전을 만듭니다. 사이드 킥의 **버전 매기기** 탭을 사용하여 요청 시 추가 버전을 만들 수도 있습니다. 이러한 모든 버전은 저장소에 저장되며 필요한 경우 복원할 수 있습니다.

이러한 버전은 삭제되지 않으므로 저장소 크기가 시간이 지남에 따라 증가하므로 관리해야 합니다.

새 버전이 만들어질 때 이전 버전을 제거하도록 AEM을 구성하는 방법에 대한 자세한 내용은 [버전 삭제](/help/sites-deploying/version-purging.md), 특히 [버전 관리자](/help/sites-deploying/version-purging.md#version-manager)를 참조하십시오.

### 로깅 {#logging}

AEM은 다음과 같은 구성 가능성을 제공합니다.

* 중앙 로깅 서비스에 대한 전역 매개 변수
* 요청 데이터 로깅;요청 정보에 대한 전문 로깅 구성
* 개별 서비스에 대한 특정 설정;예를 들어 개별 로그 파일과 로그 메시지의 형식

자세한 내용은 [로깅](/help/sites-deploying/configure-logging.md)을 참조하십시오.

### 실행 모드 {#run-modes}

실행 모드를 사용하면 특정 목적을 위해 AEM 인스턴스를 조정할 수 있습니다.작성자 또는 게시, 테스트, 개발 또는 인트라넷 등의 작업을 할 수 있습니다.

이 작업은 각 실행 모드에 대한 구성 매개 변수의 컬렉션을 정의하여 수행합니다. 구성 매개 변수의 기본 세트가 모든 실행 모드에 적용되면 특정 환경의 목적에 맞게 추가 세트를 조정할 수 있습니다. 그런 다음 필요에 따라 적용됩니다.

모든 구성 설정은 하나의 저장소에 저장되고 **실행 모드**&#x200B;를 설정하여 활성화됩니다.

자세한 내용은 [실행 모드](/help/sites-deploying/configure-runmodes.md)를 참조하십시오.

### {#single-sign-on}의 단일 서명

SSO(Single Sign On)를 통해 사용자는 인증 자격 증명(예: 사용자 이름 및 암호)을 한 번 제공한 후 여러 시스템에 액세스할 수 있습니다. 별도의 시스템(신뢰할 수 있는 인증자)은 인증을 수행하고 사용자 자격 증명을 사용하여 Experience Manager을 제공합니다. Experience Manager은 사용자에 대한 액세스 권한을 확인하고 적용합니다(즉, 사용자가 액세스할 수 있는 리소스를 결정합니다).

자세한 내용은 [단일 사인온](/help/sites-deploying/single-sign-on.md)을 참조하십시오.

### 리소스 매핑 {#resource-mapping}

리소스 매핑은 AEM용 리디렉션, 별칭 URL 및 가상 호스트를 정의하는 데 사용됩니다.

예를 들어 다음 매핑을 사용할 수 있습니다.

* 웹 사이트 방문자가 내부 구조를 보이지 않도록 모든 요청에 `/content`을(를) 접두어로 사용합니다.
* 웹 사이트의 `/content/en/gateway` 페이지에 대한 모든 요청이 `https://gbiv.com/`로 리디렉션되도록 리디렉션을 정의합니다.

자세한 내용은 [리소스 매핑](/help/sites-deploying/resource-mapping.md)을 참조하십시오.

### 복제, 역 복제 및 복제 에이전트 {#replication-reverse-replication-and-replication-agents}

복제 에이전트는 다음과 같은 메커니즘으로 AEM의 중앙 역할을 합니다.

* [작성자의 ](/help/sites-authoring/publishing-pages.md) 컨텐츠를 게시 환경에 게시(활성화)합니다.
* Dispatcher 캐시에서 컨텐츠를 명시적으로 플러시합니다.
* 작성 환경의 제어하에 제작 환경에서 사용자 입력(예: 양식 입력)을 작성 환경으로 반환합니다.

자세한 내용은 [복제](/help/sites-deploying/replication.md)를 참조하십시오.

### OSGi 구성 설정 {#osgi-configuration-settings}

[OSG](https://www.osgi.org/) 는 AEM의 기술 스택에서 기본적인 요소입니다. AEM의 합성 번들과 그 구성을 제어하는 데 사용됩니다.

프로젝트 구현과 관련된 다양한 번들(번들에 따라 나열됨) 목록은 [OSGi 구성 설정](/help/sites-deploying/osgi-configuration-settings.md)을 참조하십시오. 나열된 모든 설정을 조정할 필요는 없으며 AEM 작동 방식을 이해하는 데 도움이 되는 몇 가지 설정이 언급됩니다.

AEM으로 작업할 때 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 여러 가지가 있습니다.자세한 내용 및 권장 방법은 [OSGi](/help/sites-deploying/configuring-osgi.md) 구성을 참조하십시오.

### LDAP {#configuring-ldap} 구성

Active Directory와 같은 (중앙) LDAP 디렉토리에 저장된 사용자를 인증하려면 LDAP 인증이 필요합니다. 이렇게 하면 사용자 계정을 관리하는 데 필요한 노력을 줄일 수 있습니다.

LDAP 인증은 저장소 수준에서 수행되므로 저장소에서 직접 처리됩니다. 자세한 내용은 [AEM](/help/sites-administering/ldap-config.md)과 함께 LDAP 구성을 참조하십시오.

AEM 내 사용자 관리(액세스 권한 할당 포함)의 경우 [사용자 관리 및 보안](/help/sites-administering/security.md)을 참조하십시오.

### 디스패처 {#configuring-the-dispatcher} 구성

Dispatcher는 엔터프라이즈급 웹 서버와 함께 사용할 수 있는 Adobe Experience Manager의 캐싱 및/또는 로드 밸런싱 도구입니다.

자세한 구성 정보는 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), 특히 [Dispatcher](https://helpx.adobe.com/kr/experience-manager/dispatcher/using/dispatcher-configuration.html을 참조하십시오.) 구성을 참조하십시오.

### AEM LiveCycle 커넥터 구성 중 {#configuring-aem-livecycle-connector}

AEM Doc Services 및 AEM Doc Security가 출시되면 LiveCycle 문서 서비스를 호출하여 XFA 양식을 렌더링하고 문서를 PDF로 변환하며 문서를 보호하는 정책을 수행할 수 있습니다. 자세한 내용은 [AEM LiveCycle 커넥터](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html)를 참조하십시오.

### 작업 오프로딩 및 토폴로지 관리 {#job-offloading-and-topology-administration}

[오프로드토폴로지](/help/sites-deploying/offloading.md) 의 Experience Manager 인스턴스 중 처리 작업을 배포합니다. 오프로드를 사용하면 특정 유형의 처리를 수행하기 위해 특정 Experience Manager 인스턴스를 사용할 수 있습니다. 전문화된 처리를 통해 사용 가능한 서버 리소스의 사용을 극대화할 수 있습니다.

토폴로지는 오프로딩에 참여하는 느슨하게 연결된 Experience Manager 클러스터입니다. 클러스터는 하나 이상의 Experience Manager 서버 인스턴스로 구성됩니다(단일 인스턴스가 클러스터로 간주됨).

토폴로지 멤버십을 보거나 수정하는 방법에 대한 자세한 내용은 [토폴로지 관리](/help/sites-deploying/offloading.md#administering-topologies) 섹션을 참조하십시오.

### 시작 콘솔 구성 {#configuring-the-welcome-console}

클래식 UI의 시작 콘솔은 AEM 내의 다양한 콘솔 및 기능에 대한 링크 목록을 제공합니다.

표시되는 링크를 구성할 수 있습니다. 자세한 내용은 [시작 콘솔 구성](/help/sites-developing/customizing-the-welcome-console.md)을 참조하십시오.

### 성능 구성 {#configuring-for-performance}

[성능](/help/sites-deploying/configuring-performance.md) 은 프로젝트에 중요합니다. AEM(및/또는 기본 저장소)의 특정 측면을 성능 최적화를 위해 구성할 수 있습니다.

자세한 내용은 [성능 구성](/help/sites-deploying/configuring-performance.md#configuring-for-performance)을 참조하십시오.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 공유 데이터 저장소 {#shared-data-store}

저장소 데이터 저장소는 대용량 바이너리의 저장 공간을 저장소에서 별도의 영역으로 오프로드하여 저장소 트리 내에 있는 동일한 이진(예: 이미지)의 여러 인스턴스가 한 번만 저장되도록 하는 데 사용됩니다.

이 &quot;한 번 저장, 여러 번 참조&quot; 기능을 확장하여 하나의 저장소 트리뿐만 아니라 완전히 분리된 저장소를 제공할 수 있습니다. 각 저장소의 데이터 저장소를 구성하여 동일한 공유 파일 시스템 위치를 참조합니다.

이러한 데이터 저장소는 동일한 클러스터의 서로 다른 노드 간에 공유되거나, 동일한 설치에서 서로 다른 게시 및/또는 작성자 인스턴스 간에 공유되거나, 심지어 다른 설치에서 완전히 별개의 인스턴스로 공유될 수 있습니다.

자세한 내용은 [데이터 저장소 및 노드 저장소 구성](/help/sites-deploying/data-store-config.md)을 참조하십시오.

## 추가 구성 고려 사항 {#further-configuration-considerations}

### SSL {#enabling-http-over-ssl}을 통해 HTTP 활성화

SSL을 통해 HTTP를 활성화하여 서버에 더 많은 보안 연결을 적용할 수 있습니다.

자세한 내용은 [SSL을 통해 HTTP 활성화](/help/sites-administering/ssl-by-default.md)를 참조하십시오.

### AEM 포털 및 포틀릿 {#aem-portals-and-portlets}

포털은 개인화, Single Sign On, 다양한 소스의 컨텐츠 통합, 정보 시스템의 프레젠테이션 레이어를 호스팅하는 웹 애플리케이션입니다. 포틀릿 구성 요소를 사용하여 페이지에 포틀릿을 포함할 수도 있습니다. CQ5 WCM에서 제공하는 컨텐츠에 액세스하려면 포털 서버에 CQ5 Portal Director 포틀릿을 설치할 수 있습니다. 포틀릿을 설치, 구성 및 포털 페이지에 추가하여 이 작업을 수행할 수 있습니다.

자세한 내용은 [포털 및 포틀릿](/help/sites-administering/aem-as-portal.md)을 참조하십시오.

### 정적 개체 만료 {#expiration-of-static-objects}

정적 객체(예: 아이콘)는 변경되지 않습니다. 따라서 시스템이 적절한 기간 동안 만료되지 않도록 구성되어야 하므로 불필요한 트래픽이 줄어듭니다.

자세한 내용은 [정적 개체 만료](/help/sites-deploying/expiration-static-objects.md)를 참조하십시오.

### Java 프로세스 {#open-files-in-the-java-process}에서 FI 열기

각 Java 프로세스는 파일에 액세스할 수 있습니다. 시스템 리소스가 필요합니다. 따라서 각 프로세스에서 동시에 액세스할 수 있는 파일 수에 대한 상한값이 정의됩니다. 이 값이 초과되면 예외 오류가 발생할 수 있습니다.

AEM 프로세스가 이 최대값을 초과하는 경우 &quot; `too many open files`&quot; 메시지가 `error.log`에 표시됩니다.

이러한 예외를 피하려면 다음을 수행해야 합니다.

1. AEM 프로세스에서 사용 중인 열린 파일 수를 확인합니다.

   이 확인 방법은 인스턴스가 실행 중인 플랫폼에 따라 다릅니다. lsof(Unix) 또는 프로세스 탐색기(Windows)와 같은 유틸리티를 사용할 수 있습니다.

   개발 및 테스트 중에 이 값을 모니터링하여 다음을 수행해야 합니다.

   * 필요에 따라 파일을 닫는지 확인
   * 필요한 최대 값을 결정하기 위해(다양한 상황에서)

1. 허용되는 최대 수를 설정합니다.

   새 값은 현재 필요와 미래의 최고점에 모두 충족해야 하므로 현재 요구 사항을 두 배로 늘리는 것이 좋습니다.

   기본적으로 `serverctl`은 `CQ_MAX_OPEN_FILES`을(를) `8192`;(으)로 구성합니다.대부분의 시나리오에 충분해야 합니다.

### 리치 텍스트 편집기 구성 {#configuring-the-rich-text-editor}

**리치 텍스트 편집기**(**RTE**)는 작성자에게 텍스트 내용을 편집하기 위한 [기능](/help/sites-authoring/rich-text-editor.md)의 광범위한 범위를 제공합니다.WYSIWYG 경험에 대한 아이콘, 선택 상자 및 메뉴를 제공합니다.

자세한 내용은 [리치 텍스트 편집기 구성](/help/sites-administering/rich-text-editor.md)을 참조하십시오.

### 페이지 편집에 대한 실행 취소 구성 {#configuring-undo-for-page-editing}

페이지 편집을 위한 실행 취소 및 다시 실행 명령의 동작을 제어하는 여러 속성이 있습니다. 이러한 구성 요소를 구성할 수 있습니다. 자세한 내용은 [페이지 편집에 대한 실행 취소 구성](/help/sites-administering/config-undo.md)을 참조하십시오.

### 비디오 구성 요소 {#configuring-the-video-component} 구성

[비디오 구성 요소](/help/sites-authoring/default-components-foundation.md#video)를 사용하면 사전 정의된 기본 비디오 요소를 페이지에 배치할 수 있습니다.

변환이 올바르게 수행되려면 관리자가 별도로 [FFmpeg를 설치](/help/sites-administering/config-video.md#install-ffmpeg)해야 합니다. 또한 HTML5 요소와 함께 사용하기 위해 [비디오 프로필](/help/sites-administering/config-video.md#configure-video-profiles)을 구성할 수도 있습니다.

### 보고서 구성 및 사용자 지정 {#configuring-and-customizing-reports}

인스턴스 상태를 모니터링하고 분석하는 데 도움이 되도록 CQ에서는 개별 요구 사항에 맞게 구성할 수 있는 기본 보고서 선택을 제공합니다.

자세한 내용은 [보고서 사용자 지정 기본 사항](/help/sites-administering/reporting.md#the-basics-of-report-customization)을 참조하십시오.

### 이메일 알림 구성 {#configuring-email-notification}

CQ는 다음과 같은 사용자에게 이메일 알림을 보냅니다.

* 페이지 이벤트(예: 수정 또는 복제)에 가입했습니다.
* 포럼 이벤트에 가입했습니다.
* 워크플로우에서 단계를 수행해야 합니다.

자세한 내용은 [이메일 알림 구성](/help/sites-administering/notification.md)을 참조하십시오.

### 페이지 노출 횟수 {#enabling-page-impressions} 활성화

페이지 노출 횟수는 클래식 UI siteadmin 콘솔의 **노출 횟수** 열에 표시됩니다. 페이지 노출 횟수를 캡처하려면 다음을 구성해야 합니다.

* 게시 인스턴스에서:

   * [일 CQ WCM 페이지 통계](/help/sites-deploying/osgi-configuration-settings.md)

* 작성 인스턴스에서:

   * [Adobe 페이지 노출 횟수 추적](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>작성 환경에 대한 Adobe 페이지 노출 횟수 추적기를 구성하면 추적 서비스에 대한 익명의 요청이 허용됩니다.

