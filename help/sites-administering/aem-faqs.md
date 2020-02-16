---
title: AEM FAQ
seo-title: AEM 6.4 FAQ
description: 이러한 FAQ를 사용하여 AEM 파섹
seo-description: 이러한 FAQ를 사용하여 AEM 파섹
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
translation-type: tm+mt
source-git-commit: bc042696506bf1691c2eeffc6ab941be85fa274c

---


# AEM FAQ {#aem-faqs}

일부 AEM 문제 해결 및 구성 문제에 대한 답변을 알아봅니다.

## 사이트 {#sites}

### 바이너리 없는 배포는 어떻게 구성합니까? {#how-do-i-configure-binary-less-distribution}

바이너리 없는 배포는 공유 데이터 저장소를 통한 배포에 대해 지원되며 저장소 기반 배포 패키지 내보내기(출하 시 PID:) `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`패키지 빌더

바이너리 없는 모드가 활성화된 경우 배포된 컨텐츠 패키지에는 실제 바이너리가 아닌 바이너리에 대한 참조가 들어 있습니다.

#### 바이너리 없는 배포를 활성화하려면 어떻게 해야 합니까? {#how-do-i-enable-binary-less-distribution}

바이너리 없는 배포를 활성화하려면 공유 Blob 저장소를 사용하여 배포하십시오.
에이전트가 사용 중인 팩토리 PID( `useBinaryReferences` ) `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`**를 사용하여 OSGI 구성의 속성을 확인합니다.

#### AEM 사이트 콘솔에서 페이지 계층 구조를 탐색하는 동안 오류 메시지를 사용자 정의하려면 어떻게 합니까? {#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

개인 설정(JS가 축소되지 않은 경우) 네트워크 패널(Chrome 브라우저의)을 확인합니다.

요청 시작자가 무엇이었는지를 판별하려면 `Initiator` 열을 확인합니다. AJAX를 호출하는 위치의 파일 및 행 번호를 제공합니다. 나중에 오류 처리 기능을 추적하고 요구 사항에 따라 오류 메시지를 변경할 수 있습니다.

#### AEM에서 컨텐츠 작성자용 언어 사본을 만드는 동안 권한을 활성화하는 방법? {#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

언어 복사 기능을 만들려면 컨텐츠 작성자가 `/content/projects` 위치에서 권한을 필요로 합니다.

작성자도 프로젝트를 관리해야 하는 경우 `project-administrators` 그룹에 작성자를 추가하는 것이 해결 방법입니다.

#### 프로젝트의 언어 사본을 만드는 동안 형식을 변경하는 방법? {#how-to-change-the-format-while-creating-language-copy-for-a-project}

번역 프로젝트를 만들기 전에 루트 내에 언어 루트 및 언어 사본을 만듭니다.

예를 들어, Create a language root at `/content/geometrixx` name as `fr_LU` (and title as French (Luxembourg)). 그런 다음 참조 패널에서 페이지의 언어 사본을 만들고 의 `Create structure only` 옵션으로 이동합니다 `Create & Translate`. 마지막으로 번역 프로젝트를 만든 다음 번역 작업에 언어 사본을 추가합니다.

자세한 내용은 아래 추가 리소스를 참조하십시오.

* [번역 컨텐츠 준비](/help/sites-administering/tc-prep.md)
* [번역 프로젝트 관리](/help/sites-administering/tc-manage.md)

#### 로그인 시도 및 ACL 또는 권한 변경과 같은 AEM 기능을 감사하는 방법? {#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM에서는 더 나은 문제 해결 및 감사를 위해 관리 변경 사항을 기록하는 기능을 도입했습니다. 기본적으로 정보는 `error.log` 파일에 기록됩니다. 모니터링을 보다 쉽게 하려면 별도의 로그 파일로 리디렉션하는 것이 좋습니다.
출력을 별도의 로그 파일로 리디렉션하려면 AEM에서 [사용자 관리 작업을 감사하는 방법을 참조하십시오](/help/sites-administering/audit-user-management-operations.md).

#### 기본적으로 SSL을 활성화하는 방법? {#how-to-enable-ssl-by-default}

AEM(Adobe Experience Manager) 6.4는 SSL 마법사와 함께 제공되며 Jetty 및 Granite Jetty SSL 지원을 구성할 수 있는 사용자 인터페이스를 제공합니다.

기본적으로 SSL을 활성화하려면 [기본적으로](/help/sites-administering/ssl-by-default.md)SSL을 참조하십시오.

#### 모바일 앱에서 AEM의 컨텐츠 서비스를 사용할 때 가장 적합한 아키텍처인 React Native는 무엇입니까? {#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

컨텐츠 서비스는 Sling 모델을 기반으로 하며 AEM 개발자는 내보내기한 각 구성 요소에 대해 Sling 모델 도구를 제공해야 합니다.

React 애플리케이션에서 AEM 컨텐츠 서비스를 사용하는 방법에 대한 자세한 내용은 AEM Content [Services 시작하기 자습서를](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html) 참조하십시오.

또한 개발자가 구성 요소 트리를 내보내려는 경우 `ComponentExporter` 및 인터페이스를 구현하고 하위 구성 요소를 반복 사용하고 모델 표현을 반환할 `ContainerExporter` `ModelFactory` 수 있습니다. 아래 리소스를 참조하십시오.

[1][Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] Apache [Sling ::Sling Models](https://sling.apache.org/documentation/bundles/models.html)

#### AEM 6.4 설문 조사 팝업을 비활성화하는 방법? {#how-to-disable-aem-survey-pop-up}

터치 UI 또는 웹 콘솔을 사용하여 사용 통계 수집을 선택할 수 있습니다. 자세한 지침은 집계된 [사용 통계 수집](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)선택을 참조하십시오.

#### AEM 6.4로 업그레이드하기 위한 주요 기능을 설명하는 유용한 리소스가 있습니까? {#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

최신 버전의 Adobe [Experience Manager로](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html) 업그레이드를 고려 중인 고객의 주요 기능 상세 분류에 대해 설명하는 AEM 업그레이드해야 하는 이유 이해를 참조하십시오.

## 자산 {#assets}

### MP4 파일을 업로드하는 동안 에셋 워크플로우가 반복되는 이유(예: 드래그 앤 드롭 방식 사용) {#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

사용자가 동영상 파일을 업로드해도 자산 노드에서 삭제 권한이 없으면 청크 삭제 노드가 실패하여 업로드가 다시 시작됩니다.

#### AEM 6.4에서 한 번에 실행할 수 있는 디지털 자산의 최대 수는 무엇입니까? {#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Adobe Experience Manager(AEM) 6.5에서는 현재 한 번에 최대 2GB의 자산을 업로드할 수 있습니다.

AEM 6.5에서 작동할 수 있는 자산의 최대 수에 대한 자세한 내용은 자산 [크기 조정 가이드를](/help/assets/assets-sizing-guide.md)참조하십시오.

#### 언어 사본을 만드는 동안 OOTB 구성에 대한 기본 설정은 무엇입니까? {#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

클래식 UI를 통해 언어 사본을 만들 때, 자산은 새 언어 계층 아래로 이동되지 않고 언어 마스터에서 사용됩니다.

반면에 터치 UI를 통해 언어 사본을 만드는 경우(**참조** -> **언어 사본 업데이트**)새 언어 아래에 새 DAM 폴더가 생성되며 에셋이 여기에서 참조됩니다.

OOTB 구성에 대한 기본 설정입니다. 페이지 자산 **번역** = 번역 **구성에서 번역** 안 함을 설정할 수 있습니다.
AEM 6.4의 경우, **도구** > **클라우드 서비스** > **번역**&#x200B;클라우드서비스.

#### AEM SegmentStore(AEM 6.3.1.1)에 대해 기하급수적인 증가를 초래하는 AEM 구성 요소를 비활성화하는 방법? {#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

OSGi 구성 요소 비활성화 기능을 비활성화할 수 있습니다. 이 서비스를 사용하려면 OSGi 구성 요소 [비활성화 를 참조하십시오](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html).

AEM을 다시 시작할 때마다 UI나 `curl` 명령(예: 아래)을 통해 구성 요소를 수동으로 비활성화할 수도 있습니다.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### AEM 6.5 인스턴스로 자산 통찰력을 구성하는 방법? {#how-to-configure-asset-insights-with-aem-instance}

DTM(Adobe Activation)을 통해 배포된 Experience Manager에 대한 자산 통찰력을 설정하고 구성하려면 AEM [자산과 자산 인사이트 설정을 참조하십시오](https://helpx.adobe.com/experience-manager/kt/assets/using/asset-insights-tutorial-setup.html).

#### 관리 콘솔을 사용자 지정하는 방법 {#how-to-customize-admin-consoles}

AEM 파섹 사용자 정의 콘솔을 만들고 콘솔에 대한 기본 보기를 사용자 지정하는 방법에 대해 알아보려면 콘솔 사용자 [지정을 참조하십시오](/help/sites-developing/customizing-consoles-touch.md).

#### CoralUI 2와 CoralUI 3 기반 구성 요소의 차이점은 무엇입니까? {#what-is-the-difference-between-coralui-and-coralui-based-components}

[MOCK] A new set of Sling components of Granal UI Foundation is created for Coral3, and is located under [/libs/granite/ui/components/coral/foundation.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) CoralUI 2 기반 구성 요소에 대한 세트 하나와 CoralUI 3 기반 구성 요소에 대한 세트 하나가 있습니다. 새 세트는 이전 세트의 복사하여 붙여넣기만 하는 것이 아니라 정리됩니다(예: 능률화, 사용되지 않는 기능 제거). 따라서 페이지는 CoralUI 3 기반 또는 CoralUI 2 기반 세트만 사용하는 것이 좋습니다.

자세한 내용은 CoralUI 3 [기반의](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)마이그레이션 안내서를 참조하십시오.

#### AEM 자산에서 검색 구성 요소를 사용자 지정하는 방법? {#how-to-customize-the-search-component-in-aem-assets}

검색 증폭/등급 및 추가 구현 정보에 대한 자세한 내용은 간단한 [검색 구현 안내서를](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)참조하십시오.

단순 검색 구현은 2017 Summit Lab AEM Search Demided의 자료입니다.

#### AEM Assets와 AEM MediaLibrary의 차이점은 무엇입니까? {#what-is-the-difference-between-aem-assets-and-aem-medialibrary}

AEM Assets는 고객이 웹 기반 저장소에서 디지털 자산(이미지, 비디오, 문서 및 오디오 클립)을 관리할 수 있도록 해주는 AEM Platform의 애플리케이션이지만 AEM Media Library는 이미지 및 기타 공유 리소스가 저장되는 AEM WCM 컨텐츠 저장소의 지정된 일부입니다.

자세한 내용은 [AEM Assets와 AEM MediaLibrary를](/help/assets/medialibrary.md) 참조하십시오.

#### 고객이 Adobe 자산 선택기에 액세스하여 이미지를 선택할 수 있는 WordPress용 플러그인을 만들 수 있습니까? {#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

예. WordPress를 사용하는 고객은 Adobe Asset Picker를 사용하여 AEM Assets 서버에서 이미지를 선택하여 WordPress 사이트의 게시물에 추가할 수 있습니다.

자세한 내용은 [자산](../assets/search-assets.md#assetselector) 선택기를 참조하십시오.

#### AEM 자산에서 검색 패싯을 확장하여 추가 조건자를 추가할 수 있습니까? {#is-it-possible-to-extend-the-search-facets-in-aem-assets-to-add-additional-predicates}

AEM(Adobe Experience Manager) 자산의 전사적 배포는 많은 자산을 저장할 수 있는 능력을 가지고 있습니다. 기본 양식에 조건자를 추가하거나 원하는 단면화를 포함하는 사용자 지정 양식을 사용할 수 있습니다.

자세한 내용은 [검색 패싯](/help/assets/search-facets.md) 을 참조하십시오.
