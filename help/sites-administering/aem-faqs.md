---
title: AEM FAQ
description: 이러한 FAQ를 사용하여 AEM의 일반적인 워크플로 또는 문제를 이해, 구성 및 해결할 수 있습니다.
exl-id: 182c464a-ff7a-467b-9eb5-8ffac335a87a
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---

# AEM FAQ {#aem-faqs}

일부 AEM 문제 해결 및 구성 문제에 대한 답변을 이해할 수 있습니다.

## Sites {#sites}

### 바이너리 없는 배포를 구성하는 방법 {#how-do-i-configure-binary-less-distribution}

공유 데이터 저장소 배포에 대해 바이너리 없는 배포를 지원하며, 저장소 기반 배포 패키지 내보내기(팩터리 PID: `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) 패키지 빌더를 사용하는 에이전트가 포함됩니다.

바이너리 없음 모드가 활성화되면 배포된 콘텐츠 패키지에 실제 바이너리가 아닌 바이너리에 대한 참조가 포함됩니다.

#### 바이너리 없는 배포를 활성화하려면 어떻게 해야 합니까? {#how-do-i-enable-binary-less-distribution}

바이너리 없는 배포를 활성화하려면 공유 Blob 저장소를 사용하여 배포합니다.
에이전트가 사용 중인 팩터리 PID(`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*&#x200B;를 사용하여 OSGI 구성의 `useBinaryReferences` 속성을 확인하십시오.

#### AEM에서 콘텐츠 작성자용 언어 사본을 만드는 동안 권한을 활성화하는 방법 {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

언어 복사 기능을 만들려면 콘텐츠 작성자는 `/content/projects` 위치에서 권한이 필요합니다.

작성자가 프로젝트를 관리해야 하는 경우 해결 방법은 작성자를 `projects-administrators` 그룹에 추가하는 것입니다.

#### 프로젝트에 대한 언어 사본을 만드는 동안 형식을 변경하는 방법 {#how-to-change-the-format-while-creating-language-copy-for-a-project}

번역 프로젝트를 만들기 전에 언어 루트와 루트 내에 언어 사본을 만듭니다.

예를 들어,
`/content/geometrixx`에 이름이 `fr_LU`이고 제목이 프랑스어(룩셈부르크)인 언어 루트를 만듭니다. 이후에 참조 패널에서 페이지의 언어 사본을 만들고 `Create & Translate`의 `Create structure only` 옵션으로 이동합니다. 마지막으로 번역 프로젝트를 만든 다음 번역 작업에 언어 사본을 추가합니다.

자세한 내용은 아래의 추가 리소스를 참조하십시오.

* [번역을 위한 콘텐츠 준비](/help/sites-administering/tc-prep.md)
* [번역 프로젝트 관리](/help/sites-administering/tc-manage.md)

#### 로그인 시도 및 ACL 또는 권한 변경과 같은 AEM 기능을 감사하는 방법 {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM에서는 문제 해결 및 감사 향상을 위해 관리 변경 사항을 기록하는 기능을 도입했습니다. 기본적으로 정보는 `error.log` 파일에 기록됩니다. 모니터링을 더 쉽게 수행하려면 별도의 로그 파일로 리디렉션하는 것이 좋습니다.
출력을 별도의 로그 파일로 리디렉션하려면 [AEM에서 사용자 관리 작업을 감사하는 방법](/help/sites-administering/audit-user-management-operations.md)을 참조하십시오.

#### 기본적으로 SSL을 활성화하는 방법 {#how-to-enable-ssl-by-default}

Adobe Experience Manager(AEM) 6.4는 SSL 마법사와 함께 제공되며 Jetty 및 Granite Jetty SSL 지원을 구성할 수 있는 사용자 인터페이스를 제공합니다.

기본적으로 SSL을 사용하려면 [기본적으로 SSL](/help/sites-administering/ssl-by-default.md)을 참조하세요.

#### 모바일 앱, 이상적으로 React Native에서 AEM의 Content Services를 사용할 때 권장되는 아키텍처는 무엇입니까? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

컨텐츠 서비스는 Sling 모델을 기반으로 하며, AEM 개발자는 내보내는 각 구성 요소에 대해 Sling 모델 pojo를 제공해야 합니다.

React 애플리케이션에서 AEM Content Services를 사용하는 방법에 대한 자세한 내용은 [AEM Content Services 시작](https://helpx.adobe.com/kr/experience-manager/kt/sites/using/content-services-tutorial-use.html) 자습서를 참조하십시오.

또한 개발자가 구성 요소 트리를 내보내려는 경우 `ComponentExporter` 및 `ContainerExporter` 인터페이스를 구현하고 `ModelFactory`을(를) 사용하여 하위 구성 요소를 반복하고 모델 표현을 반환할 수도 있습니다. 아래 리소스를 참조하십시오.

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling :: Sling 모델](https://sling.apache.org/documentation/bundles/models.html)

#### AEM 6.4 설문 조사 팝업을 비활성화하는 방법 {#how-to-disable-aem-survey-pop-up}

Touch UI 또는 웹 콘솔을 사용하여 사용 통계 수집을 선택할 수 있습니다. 자세한 지침은 [집계된 사용 통계 수집으로 선택](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)을 참조하십시오.

#### AEM 6.4로 업그레이드하는 주요 기능을 강조 표시하는 훌륭한 리소스가 있습니까? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

최신 버전의 Adobe Experience Manager으로 업그레이드하는 것을 고려하는 고객을 위한 주요 기능에 대한 높은 수준의 분류를 설명하는 [AEM을 업그레이드해야 하는 이유 이해하기](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html)를 참조하십시오.

## 자산 {#assets}

### Assets 워크플로우가 MP4 파일을 업로드하는 동안 반복되는 이유는 무엇입니까(예: 드래그 앤 드롭 방법 사용)? {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

자산 노드에서 동영상 파일을 업로드할 때 삭제 권한이 없는 경우 청크 노드 삭제가 실패하고 업로드가 다시 시작됩니다.

#### 언어 사본을 만드는 동안 기본 구성에 대한 기본 설정은 무엇입니까? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

Touch UI를 통해 언어 사본을 만들 때(**참조** > **언어 사본 업데이트**), 새 DAM 폴더가 새 언어에 만들어지고 여기에서 자산이 참조됩니다.

기본 설정은 기본 구성에 대한 기본 설정입니다. 번역 구성에서 **페이지 Assets 번역** = **번역 안 함**을 설정할 수 있습니다.
AEM 6.4의 경우 **도구** > **Cloud Service** > **번역 클라우드 서비스**&#x200B;입니다.

#### AEM SegmentStore(AEM 6.3.1.1)의 기하급수적 증가를 유발하는 AEM 구성 요소를 비활성화하는 방법 {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

OSGi 구성 요소 비활성화기를 비활성화할 수 있습니다. 이 서비스를 사용하려면 [OSGi 구성 요소 사용 안 함](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html)을 참조하세요.

해결 방법으로, AEM을 다시 시작할 때마다 UI나 `curl` 명령(아래 예)을 통해 구성 요소를 수동으로 비활성화할 수도 있습니다.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### Admin Console을 사용자 지정하는 방법 {#how-to-customize-admin-consoles}

AEM은 작성 인스턴스의 콘솔 및 페이지 작성 기능을 사용자 지정할 수 있는 다양한 메커니즘을 제공합니다. 사용자 지정 콘솔을 만들고 콘솔의 기본 보기를 사용자 지정하는 방법에 대한 자세한 내용은 [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)을 참조하십시오.

#### CoralUI 2와 CoralUI 3 기반 구성 요소의 차이점은 무엇입니까? {#what-is-the-difference-between-coralui-and-coralui-based-components}

Granite UI Foundation의 새 Sling 구성 요소 집합이 Coral3에 대해 만들어지고 [/libs/granite/ui/components/coral/foundation 아래에 있습니다.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) CoralUI 2 기반 구성 요소 세트와 CoralUI 3 기반 구성 요소 세트가 있습니다. 새 세트는 이전 세트의 복사-붙여넣기가 아니라 정리됩니다(예: 스트리밍, 더 이상 사용되지 않는 기능 제거). 따라서 페이지는 CoralUI 3 기반 또는 CoralUI 2 기반 세트만 사용하는 것이 좋습니다.

자세한 내용은 [CoralUI 3 기반 마이그레이션 가이드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)를 참조하세요.

#### AEM Assets에서 검색 구성 요소를 사용자 지정하는 방법 {#how-to-customize-the-search-component-in-aem-assets}

검색 증가/순위 및 추가 구현 정보에 대한 자세한 내용은 [단순 검색 구현 안내서](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)를 참조하세요.

단순 검색 구현은 2017 Summit lab AEM Search Demystified의 자료입니다.

#### 고객이 Adobe 에셋 선택기에 액세스하여 이미지를 선택할 수 있도록 하는 워드 프레스에 대한 플러그인을 만들 수 있습니까? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

예, WordPress를 사용하는 고객은 Adobe 에셋 선택기를 사용하여 AEM Assets 서버에서 이미지를 선택하여 WordPress 사이트의 게시물에 추가할 수 있습니다.

자세한 내용은 [자산 선택기](../assets/search-assets.md#assetpicker)를 참조하세요.
