---
title: AEM FAQ
seo-title: AEM 6.4 FAQ
description: 이 FAQ를 사용하여 AEM의 일반적인 워크플로우 또는 문제를 이해, 구성 및 해결하십시오.
seo-description: 이 FAQ를 사용하여 AEM의 일반적인 워크플로우 또는 문제를 이해, 구성 및 해결하십시오.
uuid: 17d34923-f1ce-463b-8e9d-a713edcce51b
contentOwner: jsyal
discoiquuid: a3bb5695-6593-413d-9c2f-4c164e663b15
docset: aem65
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---


# AEM FAQ {#aem-faqs}

AEM 문제 해결 및 구성 문제에 대한 답변을 알 수 있습니다.

## 사이트 {#sites}

### 이진 없는 배포는 어떻게 구성합니까?{#how-do-i-configure-binary-less-distribution}

이진 없는 배포는 공유 데이터 저장소를 통한 배포에 대해 지원되며 저장소 기반 배포 패키지 내보내기(팩토리 PID:`org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`) 패키지 빌더.

이진 없는 모드가 활성화된 경우 배포된 컨텐츠 패키지에는 실제 바이너리가 아닌 바이너리에 대한 참조가 들어 있습니다.

#### 이진 없는 배포를 활성화하려면 어떻게 합니까?{#how-do-i-enable-binary-less-distribution}

바이너리 없는 배포를 활성화하려면 공유 Blob 저장소를 사용하여 배포하십시오.
에이전트가 사용 중인 팩토리 PID( `org.apache.sling.distribution.serialization.impl.vlt.VaultDistributionPackageBuilderFactory`*)*&#x200B;와 함께 OSGI 구성의 `useBinaryReferences` 속성을 확인합니다.

#### AEM 사이트 콘솔에서 페이지 계층을 탐색하는 동안 오류 메시지를 사용자 지정할 수 있는 방법은 무엇입니까?{#how-can-i-customize-the-error-messages-while-navigating-page-hierarchy-in-aem-sites-console}

개인 설정(JS가 축소되지 않음)이 있는 네트워크 패널(Chrome 브라우저)을 확인합니다.

`Initiator` 열을 보고 요청의 초기자가 무엇이었는지를 확인합니다. AJAX 호출이 수행되는 위치와 파일 번호를 제공합니다. 나중에 오류 처리 함수를 추적하고 요구 사항에 따라 오류 메시지를 변경할 수 있습니다.

#### AEM에서 컨텐츠 작성자용 언어 사본을 만드는 동안 권한을 활성화하는 방법?{#how-to-enable-permissions-while-creating-language-copy-for-content-authors-in-aem}

언어 복사 기능을 만들려면 컨텐츠 작성자가 `/content/projects` 위치에 권한이 있어야 합니다.

작성자가 프로젝트를 관리해야 하는 경우 해결 방법은 작성자를 `project-administrators` 그룹에 추가하는 것입니다.

#### 프로젝트에 대한 언어 사본을 만드는 동안 형식을 변경하는 방법은 무엇입니까?{#how-to-change-the-format-while-creating-language-copy-for-a-project}

번역 프로젝트를 만들기 전에 루트 안에 언어 루트 및 언어 사본을 만듭니다.

예를 들어
`/content/geometrixx`에 `fr_LU`(그리고 프랑스어(룩셈부르크)로 제목이 있는 언어 루트를 만듭니다. 그런 다음 참조 패널에서 페이지의 언어 사본을 만들고 `Create & Translate`의 `Create structure only` 옵션으로 이동합니다. 마지막으로 번역 프로젝트를 만든 다음 번역 작업에 언어 사본을 추가합니다.

자세한 내용은 아래 추가 리소스를 참조하십시오.

* [번역 내용 준비](/help/sites-administering/tc-prep.md)
* [번역 프로젝트 관리](/help/sites-administering/tc-manage.md)

#### 로그인 시도 및 ACL 또는 권한 변경과 같은 AEM 기능을 감사하는 방법은 무엇입니까?{#how-to-audit-aem-capabilities-such-as-login-attempts-and-acl-or-permission-changes}

AEM에서는 문제 해결 및 감사 개선을 위해 관리 변경 사항을 기록할 수 있는 기능을 도입했습니다. 기본적으로 정보는 `error.log` 파일에 기록됩니다. 모니터링을 쉽게 하려면 별도의 로그 파일로 리디렉션하는 것이 좋습니다.
출력을 별도의 로그 파일로 리디렉션하려면 AEM[에서 사용자 관리 작업을 감사하는 방법을 참조하십시오.](/help/sites-administering/audit-user-management-operations.md)

#### 기본적으로 SSL을 활성화하는 방법?{#how-to-enable-ssl-by-default}

AEM(Adobe Experience Manager) 6.4는 SSL 마법사와 함께 제공되며 Jetty 및 Granite Jetty SSL 지원을 구성하는 사용자 인터페이스를 제공합니다.

기본적으로 SSL을 활성화하려면 기본적으로 [SSL](/help/sites-administering/ssl-by-default.md)을 참조하십시오.

#### 모바일 앱에서 AEM 컨텐츠 서비스를 사용할 때 가장 적합한 아키텍처는 무엇입니까? 즉, React Native를 사용해야 합니다.{#what-is-the-recommended-architecture-when-using-aem-s-content-services-from-a-mobile-app-ideally-react-native}

컨텐트 서비스는 Sling 모델을 기반으로 하며 AEM 개발자는 내보낼 각 구성 요소에 대해 Sling 모델 도구를 제공해야 합니다.

반응형 애플리케이션에서 AEM 컨텐츠 서비스를 사용하는 방법을 이해하려면 [AEM Content Services 시작하기](https://helpx.adobe.com/kr/experience-manager/kt/sites/using/content-services-tutorial-use.html) 자습서를 참조하십시오.

또한 개발자가 구성 요소 트리를 내보내려는 경우 `ComponentExporter` 및 `ContainerExporter` 인터페이스를 구현하고 `ModelFactory`를 사용하여 하위 구성 요소를 반복하고 모델 표현을 반환할 수도 있습니다. 아래 리소스를 참조하십시오.

[1] [Adobe-Marketing-Cloud/aem-core-wcm-components](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/bundles/core/src/main/java/com/adobe/cq/wcm/core/components/internal/models/v1/PageImpl.java#L245)

[2] [Apache Sling:Sling Models](https://sling.apache.org/documentation/bundles/models.html)

#### AEM 6.4 설문 조사 팝업을 비활성화하는 방법?{#how-to-disable-aem-survey-pop-up}

터치 UI 또는 웹 콘솔을 사용하여 사용 통계 수집을 선택할 수 있습니다. 자세한 지침은 [집계된 사용 통계 컬렉션 선택](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)을 참조하십시오.

#### AEM 6.4로 업그레이드할 수 있는 주요 기능을 설명하는 유용한 리소스가 있습니까?{#is-there-a-good-resource-that-highlights-the-key-features-for-upgrading-to-aem}

최신 버전의 Adobe Experience Manager으로 업그레이드하는 것을 고려 중인 고객을 위한 주요 기능의 고급 분류를 설명하는 [AEM을 업그레이드해야 하는 이유 이해](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/upgrade-aem-article-understand.html)를 참조하십시오.

## 자산 {#assets}

### MP4 파일을 업로드하는 동안 에셋 작업 과정이 반복되는 이유는 무엇입니까(예: 드래그 앤 드롭 방식 사용)?{#why-the-assets-workflow-repeats-itself-while-uploading-mp-files-for-example-using-drag-and-drop-method}

사용자가 동영상 파일을 업로드할 때 자산 노드에서 삭제 권한이 없으면 삭제 청크 노드가 실패하여 업로드가 다시 시작됩니다.

#### AEM 6.4에서 한 번에 실행할 수 있는 디지털 자산의 최대 수는 얼마입니까?{#what-is-the-maximum-number-of-digital-assets-that-can-be-operated-with-aem-at-a-time}

Adobe Experience Manager(AEM) 6.5를 사용하면 현재 한 번에 최대 2GB의 자산을 업로드할 수 있습니다.

AEM 6.5로 실행할 수 있는 최대 자산 수에 대한 자세한 내용은 [자산 크기 조정 안내서](/help/assets/assets-sizing-guide.md)를 참조하십시오.

#### 언어 사본을 만드는 동안 OTB 구성에 대한 기본 설정은 무엇입니까?{#what-are-the-default-settings-for-ootb-configurations-while-creating-language-copy}

클래식 UI를 통해 언어 사본을 만들 때 자산은 새 언어 계층 아래로 이동되지 않고 언어 마스터에서 사용됩니다.

반면에 터치 UI를 통해 언어 사본을 만드는 경우(**참조** -> **언어 사본 업데이트**) 새 언어 아래에 새 DAM 폴더가 만들어지고 여기서 에셋이 참조됩니다.

OOTB 구성에 대한 기본 설정입니다. 번역 구성에서 **페이지 자산 번역** = **번역 안 함을 설정할 수 있습니다.**
AEM 6.4의 경우 **도구** > **Cloud Services** > **번역 클라우드 서비스**&#x200B;입니다.

#### AEM SegmentStore에 대해 기하급수적인 증가를 야기하는 AEM 구성 요소를 비활성화하는 방법(AEM 6.3.1.1)?{#how-to-disable-an-aem-component-causing-exponential-growth-for-the-aem-segmentstore-aem}

OSGi 구성 요소 비활성화 기능을 비활성화할 수 있습니다. 이 서비스를 사용하려면 [OSGi 구성 요소 비활성화](https://adobe-consulting-services.github.io/acs-aem-commons/features/osgi-disablers/component-disabler/index.html)를 참조하십시오.

해결 방법은 AEM을 다시 시작할 때마다 UI를 사용하거나 `curl` 명령(아래 예)을 통해 구성 요소를 수동으로 비활성화할 수도 있습니다.

`curl -u admin:$(pass CQ_Admin) 'https://localhost:4502/system/console/components/com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporter' --data 'action=disable'`

#### AEM 6.5 인스턴스로 자산 인사이트를 구성하는 방법?{#how-to-configure-asset-insights-with-aem-instance}

DTM(Adobe 활성화)을 통해 배포된 Experience Manager에 대한 자산 인사이트를 설정하고 구성하려면 AEM Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)을(를) 사용하여 [자산 인사이트 설정 방법을 참조하십시오.

#### 관리 콘솔을 사용자 지정하는 방법?{#how-to-customize-admin-consoles}

AEM에서는 작성 인스턴스의 콘솔 및 페이지 작성 기능을 사용자 정의할 수 있도록 하는 다양한 메커니즘을 제공합니다. 사용자 지정 콘솔을 만들고 콘솔에 대한 기본 보기를 사용자 지정하는 방법에 대해 알아보려면 [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md)을 참조하십시오.

#### CoralUI 2와 CoralUI 3 기반 구성 요소의 차이점은 무엇입니까?{#what-is-the-difference-between-coralui-and-coralui-based-components}

Granite UI Foundation의 새 Sling 구성 요소 세트는 Coral3용으로 만들어지며 [/libs/granite/ui/components/coral/foundation 아래에 있습니다.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/server.html) CoralUI 2 기반 구성 요소에 대한 세트 하나와 CoralUI 3 기반 구성 요소에 대한 세트 하나가 있습니다. 새 세트는 이전 세트의 복사하여 붙여넣은 것이 아니라 정리됩니다(예를 들어, 더 이상 사용되지 않는 기능 제거). 따라서 페이지는 CoralUI 3 기반 또는 CoralUI 2 기반 설정만 사용하는 것이 좋습니다.

자세한 내용은 [CoralUI 3 기반](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/legacy/coral2/migration.html)으로 마이그레이션 안내서를 참조하십시오.

#### AEM Assets에서 검색 구성 요소를 사용자 정의하는 방법{#how-to-customize-the-search-component-in-aem-assets}

검색 증폭/등급 및 추가 구현 정보에 대한 자세한 내용은 [단순 검색 구현 안내서](https://helpx.adobe.com/experience-manager/kt/sites/using/search-tutorial-develop.html)를 참조하십시오.

단순 검색 구현은 2017 Summit 랩 AEM Search Demified의 자료입니다.

#### AEM Assets과 AEM MediaLibrary의 차이점은 무엇입니까?{#what-is-the-difference-between-aem-assets-and-aem-medialibrary}

AEM Assets은 AEM Platform의 애플리케이션으로, 고객은 웹 기반 저장소에서 디지털 자산(이미지, 비디오, 문서 및 오디오 클립)을 관리할 수 있습니다. 반면 AEM Media Library는 이미지 및 기타 공유 리소스가 저장되는 AEM WCM 컨텐츠 저장소의 지정된 부분입니다.

자세한 내용은 [AEM Assets vs. AEM MediaLibrary](/help/assets/medialibrary.md)를 참조하십시오.

#### 고객이 Adobe 자산 선택기에 액세스하여 이미지를 선택할 수 있는 WordPress용 플러그인을 만들 수 있습니까?{#is-it-possible-to-build-plugin-for-wordpress-that-allows-a-customer-to-access-adobe-asset-picker-to-select-images}

예. WordPress를 사용하는 고객은 Adobe 자산 선택기를 사용하여 AEM Assets 서버에서 이미지를 선택하여 WordPress 사이트의 게시물에 추가할 수 있습니다.

자세한 내용은 [자산 선택기](../assets/search-assets.md#assetpicker)를 참조하십시오.

#### AEM Assets의 검색 패싯을 확장하여 추가 설명을 추가할 수 있습니까?{#is-it-possible-to-extend-the-search-facets-in-aem-assets-to-add-additional-predicates}

AEM(Adobe Experience Manager) 자산의 전사적 배포는 많은 자산을 저장할 수 있는 능력을 가지고 있습니다. 기본 양식에 설명을 추가하거나 선택한 패싯을 포함하는 사용자 지정 양식을 사용할 수 있습니다.

자세한 내용은 [검색 패싯](/help/assets/search-facets.md)을 참조하십시오.
