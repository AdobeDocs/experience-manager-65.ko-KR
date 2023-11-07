---
title: AEM FAQ
description: 이러한 FAQ를 사용하여 AEM의 일반적인 워크플로 또는 문제를 이해, 구성 및 해결할 수 있습니다.
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 1%

---

# AEM FAQ {#aem-faqs}

일부 AEM 문제 해결 및 구성 문제에 대한 답변을 이해할 수 있습니다.

## Sites {#sites}

### 바이너리 없는 배포를 구성하는 방법 {#how-do-i-configure-binary-less-distribution}

공유 데이터 저장소 배포에 대해 바이너리 없는 배포가 지원되며 저장소 기반 배포 패키지 내보내기(팩토리 PID: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) 패키지 빌더.

바이너리 없음 모드가 활성화되면 배포된 콘텐츠 패키지에 실제 바이너리가 아닌 바이너리에 대한 참조가 포함됩니다.

#### 바이너리 없는 배포를 활성화하려면 어떻게 해야 합니까? {#how-do-i-enable-binary-less-distribution}

바이너리 없는 배포를 활성화하려면 공유 Blob 저장소를 사용하여 배포합니다.
다음 확인: `useBinaryReferences` 공장 PID가 있는 OSGI 구성의 속성( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)* 에이전트에서 사용 중입니다.

#### AEM Sites 콘솔에서 페이지 계층 구조를 탐색하는 동안 오류 메시지를 사용자 정의하려면 어떻게 해야 합니까? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

개인 설정(JS가 축소되지 않은 경우)이 있는 Chrome 브라우저의 네트워크 패널을 확인하십시오.

보기 `Initiator` 요청 개시자를 결정하는 열입니다. AJAX 호출이 수행되는 위치의 파일 및 줄 번호를 제공합니다. 나중에 오류 처리 함수를 추적하고 요구 사항에 따라 오류 메시지를 변경할 수 있습니다.

#### AEM에서 콘텐츠 작성자용 언어 사본을 만드는 동안 권한을 활성화하는 방법 {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

언어 복사 기능을 만들려면 콘텐츠 작성자는 다음 위치에서 권한이 필요합니다. `/content/projects` 위치.

작성자가 프로젝트도 관리해야 하는 경우 해결 방법은 작성자를에 추가하는 것입니다. `projects-administrators` 그룹입니다.

#### 프로젝트에 대한 언어 사본을 만드는 동안 형식을 변경하는 방법 {#how-to-change-the-format-while-creating-language-copy-for-a-project}

번역 프로젝트를 만들기 전에 언어 루트와 루트 내에 언어 사본을 만듭니다.

예를 들어 다음 위치에 언어 루트 만들기 `/content/geometrixx` (으)로 이름 포함 `fr_LU` (프랑스어(룩셈부르크)로 제목). 그런 다음 참조 패널에서 페이지의 언어 사본을 만들고 다음으로 이동합니다. `Create structure only` 의 옵션 `Create & Translate`. 마지막으로 번역 프로젝트를 만든 다음 번역 작업에 언어 사본을 추가합니다.

자세한 내용은 아래의 추가 리소스를 참조하십시오.

* [번역을 위한 콘텐츠 준비](/help/sites-administering/tc-prep.md)
* [번역 프로젝트 관리](/help/sites-administering/tc-manage.md)

#### 로그인 시도 및 ACL 또는 권한 변경과 같은 AEM 기능을 감사하는 방법 {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM에서는 문제 해결 및 감사 향상을 위해 관리 변경 사항을 기록하는 기능을 도입했습니다. 기본적으로 정보는 `error.log` 파일. 모니터링을 더 쉽게 수행하려면 별도의 로그 파일로 리디렉션하는 것이 좋습니다.
출력을 별도의 로그 파일로 리디렉션하려면 다음을 참조하십시오 [AEM에서 사용자 관리 작업을 감사하는 방법](/help/sites-administering/audit-user-management-operations.md).

#### 기본적으로 SSL을 활성화하는 방법 {#how-to-enable-ssl-by-default}

Adobe Experience Manager(AEM) 6.4는 SSL 마법사와 함께 제공되며 Jetty 및 Granite Jetty SSL 지원을 구성할 수 있는 사용자 인터페이스를 제공합니다.

기본적으로 SSL을 활성화하려면 다음을 참조하십시오 [기본적으로 SSL](/help/sites-administering/ssl-by-default.md).

#### 모바일 앱에서 AEM Content Services를 사용할 때 권장되는 아키텍처인 React Native는 무엇입니까? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

컨텐츠 서비스는 Sling 모델을 기반으로 하며, AEM 개발자는 내보내는 각 구성 요소에 대해 Sling 모델 pojo를 제공해야 합니다.

React 애플리케이션에서 AEM 콘텐츠 서비스를 사용하는 방법을 이해하려면 다음을 참조하십시오. [AEM Content Services 시작](https://helpx.adobe.com/kr/experience-manager/kt/sites/using/content-services-tutorial-use.html) 튜토리얼.

또한 개발자가 구성 요소 트리를 내보내려는 경우 `ComponentExporter` 및 `ContainerExporter` 인터페이스 및 사용 `ModelFactory` 를 클릭하여 하위 컴포넌트를 반복하고 해당 모델 표현을 반환합니다. 아래 리소스를 참조하십시오.

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Sling 모델](https://sling.apache.org/documentation/bundles/models.html)

#### AEM 6.4 설문 조사 팝업을 비활성화하는 방법 {#how-to-disable-aem-survey-pop-up}

Touch UI 또는 웹 콘솔을 사용하여 사용 통계 수집을 선택할 수 있습니다. 자세한 지침은 [집계된 사용 통계 수집으로 선택](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

#### AEM 6.4로 업그레이드하는 주요 기능을 강조 표시하는 훌륭한 리소스가 있습니까? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

다음을 참조하십시오 [AEM 업그레이드 이유 이해하기](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) 최신 버전의 Adobe Experience Manager으로 업그레이드하는 것을 고려하는 고객을 위한 주요 기능에 대한 높은 수준의 분류를 설명합니다.

## 자산 {#assets}

### MP4 파일을 업로드하는 동안 자산 워크플로우가 반복되는 이유는 무엇입니까(예: 드래그 앤 드롭 방법 사용)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

자산 노드에서 동영상 파일을 업로드할 때 삭제 권한이 없는 경우 청크 노드 삭제가 실패하고 업로드가 다시 시작됩니다.

#### 언어 사본을 만드는 동안 OOTB 구성에 대한 기본 설정은 무엇입니까? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Touch UI를 통해 언어 사본을 만들 때(**참조** -> **언어 사본 업데이트**) 새 언어 아래에 새 DAM 폴더가 생성되고 여기에서 에셋이 참조됩니다.

OOTB 구성의 기본 설정입니다. 다음을 설정할 수 있습니다. **페이지 에셋 번역** = **번역 안 함** 번역 구성에서.
AEM 6.4의 경우 **도구** > **Cloud Service** > **번역 클라우드 서비스**.

#### AEM SegmentStore(AEM 6.3.1.1)의 기하급수적 증가를 유발하는 AEM 구성 요소를 비활성화하는 방법 {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

OSGi 구성 요소 비활성화기를 비활성화할 수 있습니다. 이 서비스를 사용하려면 다음을 참조하십시오 [OSGi 구성 요소 비활성화](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

해결 방법으로, UI 또는 를 통해 구성 요소를 수동으로 비활성화할 수도 있습니다. `curl` AEM 명령(아래 예)을 실행하십시오.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Admin Console을 사용자 지정하는 방법 {#how-to-customize-admin-consoles}

AEM은 작성 인스턴스의 콘솔 및 페이지 작성 기능을 사용자 지정할 수 있는 다양한 메커니즘을 제공합니다. 사용자 지정 콘솔을 만들고 콘솔의 기본 보기를 사용자 지정하는 방법에 대한 자세한 내용은 [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md).

#### CoralUI 2와 CoralUI 3 기반 구성 요소의 차이점은 무엇입니까? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Granite UI Foundation의 새 슬링 구성 요소 세트는 Coral3용으로 만들어졌으며 아래에 있습니다. [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) CoralUI 2 기반 구성 요소에 대한 세트와 CoralUI 3 기반 구성 요소에 대한 세트가 있습니다. 새 세트는 이전 세트의 복사-붙여넣기가 아니라 정리됩니다(예: 스트리밍, 더 이상 사용되지 않는 기능 제거). 따라서 페이지는 CoralUI 3 기반 또는 CoralUI 2 기반 세트만 사용하는 것이 좋습니다.

자세한 내용은 [CoralUI 3 기반으로 마이그레이션 안내서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html).

#### AEM Assets에서 검색 구성 요소를 사용자 지정하는 방법 {#how-to-customize-the-search-component-in-aem-assets}

검색 증가/순위 및 추가 구현 정보에 대한 자세한 내용은 을 참조하십시오. [단순 검색 구현 안내서](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html).

단순 검색 구현은 2017 Summit lab AEM Search Demystified의 자료입니다.

#### 고객이 Adobe 에셋 선택기에 액세스하여 이미지를 선택할 수 있도록 하는 워드 프레스에 대한 플러그인을 만들 수 있습니까? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

예, WordPress를 사용하는 고객은 Adobe 에셋 선택기를 사용하여 AEM Assets 서버에서 이미지를 선택하여 WordPress 사이트의 게시물에 추가할 수 있습니다.

을(를) 참조하십시오 [자산 선택기](../assets/search-assets.md#assetpicker) 추가 정보.
