---
title: 기본 구성 개념
description: 고유한 특정 요구 사항에 맞게 Adobe Experience Manager을 구성하는 방법에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '2093'
ht-degree: 0%

---

# 기본 구성 개념{#basic-configuration-concepts}

Adobe Experience Manager(AEM)는 &quot;즉시 실행&quot;할 수 있도록 하는 모든 매개 변수에 대한 기본 설정과 함께 설치됩니다. 하지만 고유한 특정 요구 사항에 맞게 AEM을 구성할 수 있습니다.

구성할 수 있는 AEM에는 다음과 같은 여러 측면이 있습니다.

* 일부 [일반적으로 모든 프로젝트 설치에 대해 구성됨](#primary-configuration-considerations) 및 을(를) 검토하여 프로젝트에 적용할 수 있는지 확인해야 합니다.
* [추가 구성](#further-configuration-considerations) 기능 또는 시스템 성능 및 안정성과 관련하여 필수적이지는 않지만 일반적일 수 있습니다.
* 다른 요소는 AEM의 특정 선택적 기능에 대해서만 필요합니다(해당 기능과 함께 설명됨).

특정 구성에 따라 다음 중 하나를 사용하여 변경할 수 있습니다.

* **Adobe CQ 웹 콘솔**

  OSGi 번들 및 서비스를 구성하는 표준 위치입니다.

  다음을 참조하십시오 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 추가 세부 정보 및 권장 사례를 확인하십시오.

* **저장소**

  OSGi 구성의 하위 집합은 저장소에서 사용할 수 있습니다. 이렇게 하면 저장소 콘텐츠를 복사하거나 복제하는 것과 동일한 구성이 다시 생성됩니다. 실행 모드에 따라 자체 구성을 저장소에 추가할 수도 있습니다.

  다음을 참조하십시오 [저장소의 OSGi 구성](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 특히 [저장소에 새 구성 추가](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) 을 참조하십시오.

* **파일 시스템**

  몇 가지 구성 파일이 파일 시스템 내에 있습니다.

* **AEM WCM**

  AEM WCM 자체 내에서 다양한 측면을 구성할 수 있으며, 많은 경우 [도구](/help/sites-administering/tools-consoles.md) 콘솔(예: 복제 에이전트)

>[!NOTE]
>
>Adobe Experience Manager을 사용하여 작업할 때 OSGi 서비스(콘솔 또는 저장소 노드)에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다.
>
>다음을 참조하십시오 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 전체 세부 정보.

>[!NOTE]
>
>AEM 구성은 간단합니다. 그러나 특정 변경 사항은 애플리케이션에 중요한 영향을 미칠 수 있습니다. 이러한 이유로 AEM 구성을 시작하기 전에 필요한 경험과 지식을 갖추고 있는지 확인하고 필요한 사항만 변경합니다. OSGi 콘솔을 통해 변경한 사항은 다음과 같습니다 **즉시** 실행 중인 시스템에 적용됩니다(다시 시작할 필요가 없음).

## 기본 구성 고려 사항 {#primary-configuration-considerations}

이 목록은 모든 새 프로젝트에 대해 일반적으로 구성되는 기본 영역을 자세히 설명합니다. 모두 필요한 것은 아니지만 목록을 읽고 검토하여 프로젝트에 적용할 수 있는 사항을 확인해야 합니다.

이 목록은 전체 세부 정보를 제공하는 페이지에 대한 링크와 함께 각 구성 측면에 대한 간단한 개요를 제공합니다.

### 보안 검사 목록 {#security-checklist}

몇 가지 주요 구성 문제가 다음에 나열됩니다. [보안 검사 목록](/help/sites-administering/security-checklist.md). 이 문서를 읽고 설치에 필요한 조치를 취했는지 확인하십시오.

### 기본 UI 구성 - 터치에 적합한 또는 클래식 {#configuring-the-default-ui-touch-optimized-or-classic}

AEM에서 사용할 수 있는 UI는 두 가지입니다.

* 터치에 적합한 UI
* 클래식 UI

을 사용하여 필요한 UI를 구성할 수 있습니다. [루트 매핑](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>UI 선택에 대한 자세한 내용은 [UI 선택](/help/sites-authoring/select-ui.md).

### IPv4 및 IPv6 {#ipv-and-ipv}

AEM의 모든 요소(예: 저장소 및 Dispatcher)는 IPv4 및 IPv6 네트워크 모두에 설치할 수 있습니다.

필요한 경우 네트워크 유형에 적합한 형식을 사용하여 IP 주소를 지정할 수 있으므로 특별한 구성이 필요하지 않으므로 원활한 작업이 가능합니다.

즉, IP 주소를 지정해야 하는 경우 다음 중에서 선택할 수 있습니다(필요에 따라).

* IPv6 주소

  예를 들어, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 주소

  예를 들어, `https://123.1.1.4:4502`

* 서버 이름

  예를 들어, `https://www.yourserver.com:4502`

* 의 기본 대/소문자 `localhost` 는 IPv4 및 IPv6 네트워크 설치 모두에 대해 해석됩니다.

  예를 들어, `http://localhost:4502`

### 버전 삭제 {#version-purging}

표준 설치에서 AEM은 사용자가 콘텐츠를 업데이트한 후 페이지를 활성화할 때마다 페이지 또는 노드 버전을 생성합니다. 를 사용하여 요청에 대한 추가 버전을 생성할 수도 있습니다. **버전 관리** 사이드 킥의 탭 이러한 모든 버전은 저장소에 저장되며 필요한 경우 복원할 수 있습니다.

이러한 버전은 삭제되지 않으므로 시간이 지남에 따라 저장소 크기가 커지므로 관리해야 합니다.

다음을 참조하십시오 [버전 삭제](/help/sites-deploying/version-purging.md) 특히 상세한 것은 [버전 관리자](/help/sites-deploying/version-purging.md#version-manager) 새 버전을 만들 때 이전 버전을 제거하도록 AEM을 구성하는 방법에 대한 자세한 내용을 보려면 여기를 클릭하십시오.

### 로깅 {#logging}

AEM에서는 다음을 구성할 수 있습니다.

* 중앙 로깅 서비스에 대한 전역 매개 변수
* 요청 데이터 로깅, 요청 정보에 대한 전문 로깅 구성
* 개별 서비스에 대한 특정 설정(예: 로그 메시지의 개별 로그 파일 및 형식)

다음을 참조하십시오 [로깅](/help/sites-deploying/configure-logging.md) 전체 세부 정보.

### 실행 모드 {#run-modes}

실행 모드를 사용하면 특정 목적을 위해 AEM 인스턴스를 조정할 수 있습니다. 예: 작성자 또는 게시, 테스트, 개발 또는 인트라넷 등.

이 작업은 각 실행 모드에 대한 구성 매개 변수의 컬렉션을 정의하여 수행됩니다. 기본 구성 매개변수 세트가 모든 실행 모드에 적용됩니다. 그런 다음 특정 환경의 목적에 맞게 추가 세트를 조정할 수 있습니다. 그런 다음 필요에 따라 적용됩니다.

모든 구성 설정은 하나의 저장소에 저장되며 **실행 모드**.

다음을 참조하십시오 [실행 모드](/help/sites-deploying/configure-runmodes.md) 전체 세부 정보.

### 단일 사인온 {#single-sign-on}

SSO(Single Sign-On)를 사용하면 인증 자격 증명(사용자 이름 및 암호 등)을 한 번 제공한 후 여러 시스템에 액세스할 수 있습니다. 별도의 시스템(신뢰할 수 있는 인증자라고도 함)이 인증을 수행하고 Experience Manager에게 사용자 자격 증명을 제공합니다. Experience Manager은 사용자에 대한 액세스 권한을 확인하고 적용합니다(즉, 사용자가 액세스할 수 있는 리소스를 결정합니다).

다음을 참조하십시오 [단일 사인온](/help/sites-deploying/single-sign-on.md) 을 참조하십시오.

### 리소스 매핑 {#resource-mapping}

리소스 매핑은 AEM의 리디렉션, vanity URL 및 가상 호스트를 정의하는 데 사용됩니다.

예를 들어 이러한 매핑을 사용하여 다음을 수행할 수 있습니다.

* 모든 요청 접두사로 사용 `/content` 따라서 웹 사이트 방문자에게 내부 구조가 숨겨집니다.
* 에 대한 모든 요청이 `/content/en/gateway` 웹 사이트의 페이지는 다음으로 리디렉션됩니다. `https://gbiv.com/`.

다음을 참조하십시오 [리소스 매핑](/help/sites-deploying/resource-mapping.md) 을 참조하십시오.

### 복제, 역복제 및 복제 에이전트 {#replication-reverse-replication-and-replication-agents}

복제 에이전트는 다음과 같은 작업에 사용되는 메커니즘으로 AEM에 중심적입니다.

* [게시(활성화)](/help/sites-authoring/publishing-pages.md) 작성자에서 게시 환경으로의 콘텐츠.
* Dispatcher 캐시에서 콘텐츠를 명시적으로 플러시합니다.
* 게시 환경의 사용자 입력(예: 양식 입력)을 작성 환경(작성 환경의 제어 아래)으로 반환합니다.

자세한 내용은 [복제](/help/sites-deploying/replication.md).

### OSGi 구성 설정 {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) 는 AEM의 기술 스택에 있는 기본 요소입니다. AEM의 복합 번들과 해당 구성을 제어하는 데 사용됩니다.

다음을 참조하십시오 [OSGi 구성 설정](/help/sites-deploying/osgi-configuration-settings.md) 프로젝트 구현과 관련된 다양한 번들 목록(번들에 따라 나열됨)입니다. 나열된 모든 설정을 조정할 필요는 없습니다. 일부 설정은 AEM 작동 방식을 이해하는 데 도움이 됩니다.

AEM을 사용하여 작업할 때 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 다음을 참조하십시오. [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 를 참조하십시오.

### LDAP 구성 {#configuring-ldap}

Active Directory와 같은 (중앙) LDAP 디렉터리에 저장된 사용자를 인증하려면 LDAP 인증이 필요합니다. 이렇게 하면 사용자 계정을 관리하는 데 필요한 수고를 줄일 수 있습니다.

LDAP 인증은 저장소 수준에서 발생하므로 저장소에서 직접 처리됩니다. 자세한 내용은 [AEM을 사용하여 LDAP 구성](/help/sites-administering/ldap-config.md).

AEM 내의 사용자 관리(액세스 권한 할당 포함)에 대해서는 다음을 참조하십시오. [사용자 관리 및 보안](/help/sites-administering/security.md).

### Dispatcher 구성 {#configuring-the-dispatcher}

Dispatcher는 캐싱, 로드 밸런싱 또는 둘 모두를 위한 Adobe Experience Manager의 도구입니다. 엔터프라이즈급 웹 서버와 함께 사용할 수 있습니다.

다음을 참조하십시오 [디스패처](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 특히 상세한 것은 [Dispatcher 구성](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html) 추가 구성 세부 정보.

### AEM LiveCycle 커넥터 구성 {#configuring-aem-livecycle-connector}

AEM Doc Services 및 AEM Doc Security가 출시되면서 AEM은 이제 LiveCycle Doc Services를 호출하여 XFA 양식을 렌더링하고 문서를 PDF으로 변환하며 문서를 정책으로 보호하는 기능을 갖게 되었습니다. 다음을 참조하십시오 [AEM LiveCycle 커넥터](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) 을 참조하십시오.

### 작업 오프로딩 및 토폴로지 관리 {#job-offloading-and-topology-administration}

[오프로드](/help/sites-deploying/offloading.md) 토폴로지의 Experience Manager 인스턴스 간에 처리 작업을 배포합니다. 오프로딩을 사용하면 특정 유형의 처리를 수행하기 위해 특정 Experience Manager 인스턴스를 사용할 수 있습니다. 특화된 처리를 통해 사용 가능한 서버 리소스의 사용을 극대화할 수 있습니다.

토폴로지는 오프로딩에 참여하는 느슨하게 결합된 Experience Manager 클러스터입니다. 클러스터는 하나 이상의 Experience Manager 서버 인스턴스로 구성됩니다(단일 인스턴스는 클러스터로 간주됨).

토폴로지 멤버십을 보거나 수정하는 방법에 대한 자세한 내용은 [토폴로지 관리](/help/sites-deploying/offloading.md#administering-topologies) 섹션.

### 시작 콘솔 구성 {#configuring-the-welcome-console}

클래식 UI의 시작 콘솔은 AEM 내의 다양한 콘솔 및 기능에 대한 링크 목록을 제공합니다.

표시되는 링크를 구성할 수 있습니다. 다음을 참조하십시오. [시작 콘솔 구성](/help/sites-developing/customizing-the-welcome-console.md) 을 참조하십시오.

### 성능을 위한 구성 {#configuring-for-performance}

[성능](/help/sites-deploying/configuring-performance.md) 는 프로젝트의 키입니다. AEM(및/또는 기본 저장소)의 특정 측면을 성능을 최적화하도록 구성할 수 있습니다.

다음을 참조하십시오 [성능을 위한 구성](/help/sites-deploying/configuring-performance.md#configuring-for-performance) 을 참조하십시오.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 공유 데이터 저장소 {#shared-data-store}

저장소 데이터 저장소는 저장소 트리 내에서 동일한 이진(예: 이미지)의 여러 인스턴스가 한 번만 저장되도록 큰 이진 저장을 별도의 영역에 적절한 저장소에서 오프로드하는 데 사용됩니다.

이 &quot;한 번 저장, 참조 여러 번&quot; 기능은 각 데이터 저장소를 동일한 공유 파일 시스템 위치를 참조하도록 구성하여 단일 저장소 트리뿐만 아니라 완전히 별도의 저장소를 제공하도록 확장할 수 있습니다.

이러한 데이터 저장소는 동일한 클러스터의 다른 노드, 동일한 설치의 다른 게시 및/또는 작성자 인스턴스 또는 다른 설치의 완전히 다른 인스턴스 간에 공유할 수 있습니다.

자세한 내용은 [데이터 저장소 및 노드 저장소 구성](/help/sites-deploying/data-store-config.md).

## 추가 구성 고려 사항 {#further-configuration-considerations}

### SSL을 통한 HTTP 활성화 {#enabling-http-over-ssl}

SSL을 통한 HTTP를 활성화하여 서버에 보다 안전한 연결을 사용할 수 있습니다.

다음을 참조하십시오 [SSL을 통한 HTTP 활성화](/help/sites-administering/ssl-by-default.md) 을 참조하십시오.

### AEM 포털 및 포틀릿 {#aem-portals-and-portlets}

포털은 개인화, SSO(Single Sign-On), 다양한 소스의 컨텐츠 통합을 제공하고 정보 시스템의 프레젠테이션 계층을 호스팅하는 웹 애플리케이션입니다. 포틀릿 구성 요소를 사용하여 페이지에 포틀릿을 포함할 수도 있습니다. CQ5 WCM에서 제공하는 콘텐츠에 액세스하려면 CQ5 포털 Director 포틀릿을 포털 서버에 연결할 수 있습니다. 포틀릿을 포털 페이지에 설치, 구성 및 추가하면 됩니다.

다음을 참조하십시오 [포털 및 포틀릿](/help/sites-administering/aem-as-portal.md) 을 참조하십시오.

### 정적 개체의 만료 {#expiration-of-static-objects}

정적 객체(예: 아이콘)는 변경되지 않습니다. 따라서 시스템이 (적절한 기간 동안) 만료되지 않고 불필요한 트래픽을 줄이도록 구성되어야 합니다.

다음을 참조하십시오 [정적 개체의 만료](/help/sites-deploying/expiration-static-objects.md) 을 참조하십시오.

### Java™ Process에서 FI 열기 {#open-files-in-the-java-process}

각 Java™ 프로세스는 파일에 액세스할 수 있습니다. 이렇게 하려면 시스템 리소스가 필요합니다. 이러한 이유로, 상한은 각 프로세스가 동시에 액세스할 수 있는 파일 수로 정의됩니다. 이를 초과하는 경우 예외 오류가 발생할 수 있습니다.

AEM 프로세스가 이 최대값을 초과하는 경우 &quot; `too many open files`&quot;이(가)에 표시됨 `error.log`.

이러한 예외를 방지하려면 다음을 수행합니다.

1. AEM 프로세스에서 사용 중인 열린 파일의 수를 확인합니다.

   이 검사는 인스턴스가 실행 중인 플랫폼에 따라 다릅니다. lsof(UNIX®) 또는 프로세스 탐색기(Windows)와 같은 유틸리티를 사용할 수 있습니다.

   이 값은 다음 작업을 위한 개발 및 테스트 중에 모니터링해야 합니다.

   * 파일이 필요에 따라 닫히고 있는지 확인합니다.
   * 필요한 최대값을 결정하기 위해(다양한 상황에서)

1. 허용되는 최대값을 설정하십시오.

   새 값은 현재 요구 사항과 향후 정점에 모두 적합해야 하므로 현재 요구 사항을 두 배로 늘리는 것이 좋습니다.

   기본적으로, `serverctl` 구성 `CQ_MAX_OPEN_FILES` 끝 `8192`: 대부분의 시나리오에 충분합니다.

### 리치 텍스트 편집기 구성 {#configuring-the-rich-text-editor}

다음 **리치 텍스트 편집기** (**RTE**)은 작성자에게 광범위한 기능을 제공합니다 [기능](/help/sites-authoring/rich-text-editor.md) 텍스트 컨텐츠를 편집합니다. WYSIWYG 경험을 위해 아이콘, 선택 상자 및 메뉴를 제공합니다.

다음을 참조하십시오 [리치 텍스트 편집기 구성](/help/sites-administering/rich-text-editor.md) 을 참조하십시오.

### 페이지 편집을 위해 실행 취소 구성 {#configuring-undo-for-page-editing}

페이지 편집을 위해 실행 취소 및 재실행 명령의 동작을 제어하는 몇 가지 속성이 있습니다. 구성할 수 있습니다. 다음을 참조하십시오. [페이지 편집을 위해 실행 취소 구성](/help/sites-administering/config-undo.md) 을 참조하십시오.

### 비디오 구성 요소 구성 {#configuring-the-video-component}

다음 [비디오 구성 요소](/help/sites-authoring/default-components-foundation.md#video) 사전 정의된 기본 비디오 요소를 페이지에 배치할 수 있습니다.

적절한 코드 변환이 일어나도록 하려면 관리자가 수행해야 합니다 [FFmpeg 설치](/help/sites-administering/config-video.md#install-ffmpeg) 별도로. 또한 다음과 같은 작업을 수행할 수 있습니다. [비디오 프로필 구성](/help/sites-administering/config-video.md#configure-video-profiles) html5 요소와 함께 사용됩니다.

### 보고서 구성 및 사용자 지정 {#configuring-and-customizing-reports}

인스턴스의 상태를 모니터링하고 분석하는 데 도움이 되도록 CQ는 개별 요구 사항에 맞게 구성할 수 있는 기본 보고서 선택을 제공합니다.

다음을 참조하십시오. [보고서 사용자 지정의 기본 사항](/help/sites-administering/reporting.md#the-basics-of-report-customization) 을 참조하십시오.

### 이메일 알림 구성 {#configuring-email-notification}

CQ는 다음과 같은 사용자에게 이메일 알림을 보냅니다.

* 페이지 이벤트(예: 수정 또는 복제)를 구독했습니다.
* 포럼 이벤트를 구독했습니다.
* 워크플로우에서 단계를 수행해야 합니다.

다음을 참조하십시오 [이메일 알림 구성](/help/sites-administering/notification.md) 을 참조하십시오.

### 페이지 노출 횟수 활성화 {#enabling-page-impressions}

페이지 노출 횟수는 **노출 횟수** 클래식 UI siteadmin 콘솔의 열입니다. 페이지 노출 횟수 캡처를 활성화하려면 다음을 구성합니다.

* 게시 인스턴스에서 다음을 수행합니다.

   * [일별 CQ WCM 페이지 통계](/help/sites-deploying/osgi-configuration-settings.md)

* 작성자 인스턴스에서 다음을 수행합니다.

   * [Adobe 페이지 노출 횟수 추적기](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>작성 환경에서 Adobe 페이지 노출 횟수 추적기를 구성하면 추적 서비스에 대한 익명 요청을 수행할 수 있습니다.
