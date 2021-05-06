---
title: RemotePage 구성 요소
description: RemotePage 구성 요소는 AEM 내에서 원격 반응 SPA을 편집하기 위한 사용자 지정 페이지 구성 요소입니다.
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
translation-type: tm+mt
source-git-commit: a92358d187aa78e05dd9b5a7bd4ae14bf0972f62
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# RemotePage 구성 요소 {#remote-page-component}

외부 SPA과 AEM 간에 어떤 통합 수준을 원하는지 결정할 때 AEM 내에서 SPA을 보고 편집할 수 있어야 하는 것이 일반적입니다. RemotePage 구성 요소는 이 목적을 위해 사용자 지정 페이지 구성 요소입니다.

## 개요 {#overview}

RemotePage 구성 요소는 애플리케이션에서 생성된 `asset-manifest.json`에서 필요한 모든 에셋을 가져오고 AEM 내에서 SPA을 렌더링하는 데 사용합니다.

* RemotePage를 사용하면 SPA의 스크립트 및 스타일 시트를 AEM 페이지 구성 요소 본문에 삽입할 수 있습니다.
* 가상 프런트 엔드 구성 요소를 사용하면 AEM SPA 편집기에서 섹션을 편집 가능한 것으로 표시할 수 있습니다.
* 서로 다른 도메인에 호스팅된 SPA을 AEM에서 편집할 수 있습니다.

AEM에서 편집 가능한 외부 SPA에 대한 자세한 내용은 SPA에서 외부을 편집하는 문서 [AEM 내 외부 편집을 참조하십시오.](spa-edit-external.md)

## 요구 사항 {#requirements}

* 개발 시 CORS 활성화
* 페이지 속성에서 원격 URL 구성
* AEM에서 SPA 렌더링
* 웹 응용 프로그램은 다음 중 하나와 같은 번들러 자산 매니페스트를 사용하고 로드할 모든 CSS 및 JS 파일을 진입점 속성에 나열하는 도메인 루트에 asset-manifest.json 파일을 노출해야 합니다.
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

   ![시작 지점](assets/asset-manifest-entrypoints.png)

* 응용 프로그램은 본문 요소 아래의 `<div id="root"></div>`에서 시작할 수 있어야 합니다. 앱이 인스턴스화되기 위해 다른 마크업이 필요한 경우 `sling:resourceSuperType="spa-project-core/components/remotepage`이(가) 있는 프록시 구성 요소의 HTL 스크립트에서 적절히 조정되어야 합니다.

## 제한 사항 {#limitations}

* RemotePage 구성 요소의 현재 구현은 원격 응답 애플리케이션만 지원합니다.
* AEM에서 원격 렌더링을 수행할 때 애플리케이션의 루트 HTML 파일과 루트 DOM 노드의 인라인 CSS에 정의된 내부 CSS를 사용할 수 없습니다.

## 기술 세부 정보 {#technical-details}

나머지 AEM SPA 프로젝트와 마찬가지로 RemotePage 구성 요소는 오픈 소스입니다. RemotePage 구성 요소에 대한 전체 기술 세부 정보는 [GitHub 리포지토리를 참조하십시오.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
