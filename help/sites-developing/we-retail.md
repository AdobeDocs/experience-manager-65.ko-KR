---
title: We.Retail 참조 구현
seo-title: We.Retail 참조 구현
description: We.Retail은 참조 구현의 기술 미리 보기로서 AEM에서 온라인 상태 설정 방법을 보여 줍니다
seo-description: We.Retail은 참조 구현의 기술 미리 보기로서 AEM에서 온라인 상태 설정 방법을 보여 줍니다
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# We.Retail 참조 구현{#we-retail-reference-implementation}

## 소개 {#introduction}

We.Retail은 Adobe Experience Manager를 사용하여 온라인 입지를 설정하는 권장 방법을 보여주는 참조 구현 및 샘플 컨텐츠입니다.

We.Retail에서는 HTL, 반응형 레이아웃, 편집 가능한 템플릿, 핵심 구성 요소 등과 같은 최신 AEM 기술을 사용합니다.

리테일 세로로 표시되지만 사이트가 세로로 설정되는 방식은 세로로 적용할 수 있으며 제품 카탈로그 및 장바구니 기능만 소매용으로 적용됩니다.

## 기능 {#features}

AEM의 표준 참조 구현인 We.Retail은 AEM의 가장 강력한 기능 중 일부를 보여줍니다.

| **기능** | **설명** | **관심?** |
|---|---|---|
| [사이트 구조 글로벌라이제이션](/help/sites-administering/tc-bp.md) | We.Retail에는 국가 특정 사이트에 실시간으로 복사되는 언어 마스터가 포함되어 있습니다. | [사용해 보세요!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [반응형 레이아웃](/help/sites-authoring/responsive-layout.md) | 모든 페이지는 화면 및 디바이스 크기에 맞게 동적으로 조정되는 반응형 레이아웃을 제공합니다. | [사용해 보세요!](/help/sites-developing/we-retail-responsive-layout.md) |
| [편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md) | 모든 페이지는 편집 가능한 템플릿을 기반으로 하므로 개발자가 아닌 사용자가 템플릿을 조정하고 사용자 정의할 수 있습니다. | [사용해 보세요!](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML Template Language](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) | 모든 구성 요소는 HTL을 기반으로 합니다. |  |
| [eCommerce 기능](/help/sites-developing/ecommerce.md) | 제품 카탈로그 기능 |  |
| [커뮤니티 사이트](/help/communities/overview.md) | 방문자가 커뮤니티 토론에 참여하거나 블로그 등을 읽을 수 있도록 허용 |  |
| [코어 구성 요소](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) | 모든 구성 요소는 새로운 핵심 구성 요소를 기반으로 하며 보다 유용하고 사용자가 즉시 구성할 수 있습니다 | [사용해 보세요!](/help/sites-developing/we-retail-core-components.md) |
| [컨텐츠 조각](/help/assets/content-fragments.md) | We.Retail 경험 섹션에서는 컨텐츠 조각을 통해 컨텐츠를 재사용할 수 있는 강력한 기능을 보여줍니다. | [시험해 보세요!](/help/sites-developing/we-retail-content-fragments.md) |
| [경험 조각](/help/sites-authoring/experience-fragments.md) | 경험 조각은 페이지 내에서 참조할 수 있는 컨텐츠 및 레이아웃을 포함한 하나 이상의 구성 요소 그룹입니다. | [시험해 보세요!](/help/sites-developing/we-retail-experience-fragments.md) |

## 시작하기 {#getting-started}

We.Retail은 AEM 파섹 사용하려면 샘플 컨텐츠가 비활성화되지 않도록 AEM을 평소대로 [간단히](/help/sites-deploying/deploy.md#getting-started)시작합니다.

>[!CAUTION]
>
>We.Retail은 프로덕션 인스턴스에 설치하면 안 됩니다. 프로덕션 인스턴스는 `nosamplecontent` 런타임 [모드에서](/help/sites-deploying/configure-runmodes.md)시작해야 합니다.

>[!CAUTION]
>
>We.Retail은 최신 AEM 기술을 기반으로 하므로 [클래식 UI 저작을](/help/sites-classic-ui-authoring/home.md)지원하지 않습니다.

### 최신 버전 {#latest-version}

We.Retail은 AEM 릴리스와 함께 배포되지만, 컨텐츠 및 해당 기능에 대한 업데이트는 릴리스 이후에 제공될 수 있습니다. 따라서 GitHub에서 최신 릴리스를 [다운로드한 다음](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) AEM 인스턴스에 패키지로 [업로드](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system)[및](/help/sites-administering/package-manager.md#installing-packages) 설치할수 있습니다.

### 첫 단계 {#first-steps}

1. AEM이 시작되면(및/또는 We.Retail이 설치됨) 사이트 **We.** Retail을 [사이트 콘솔에서](/help/sites-authoring/basic-handling.md#global-navigation)사용할 수 있습니다.
1. 예를 들어 다음 페이지를 열 수 있으며 아래 [부록에](#appendix) 표시된 것처럼 보입니다.

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail 및 Geometrixx {#we-retail-geometrixx}

Geometrixx 및 그 많은 화면은 이전 버전의 AEM에서 샘플 컨텐츠로 제공되었습니다. 버전 6.3 이후 We.Retail은 AEM과 함께 제공되는 샘플 컨텐츠였으며 새로운 표준 참조 구현 역할을 합니다.

We.Retail은 보다 기술적으로 강력하며 최신 AEM 기술을 활용하여 유연하고 확장 가능하며 제품의 최신 기능을 보여줍니다.

### 기능 비교 {#feature-comparison}

다음 표는 Geometrixx와 비교하여 We.Retail에서 사용할 수 있는 주요 기능에 대한 개요를 제공합니다.

* **사용 가능한** 것은 기능의 예가 샘플 컨텐츠에 있음을 의미합니다.
* **사용할 수** 없음을 의미하는 것은 기능의 예를 샘플 컨텐츠에서 사용할 수 없지만 기능 자체가 아니라는 것을 의미하지는 않습니다.

| **기능** | **We.Retail** | **Geometrixx** |
|---|---|---|
| 사이트 구조 글로벌라이제이션 | 언어 마스터가 국가별 사이트에 라이브로 복사 | 사용할 수 없음 |
| 컨텐츠 조각 | 사용 가능 | 사용할 수 없음 |
| 경험 조각 | 사용 가능 | 사용할 수 없음 |
| 응답형 레이아웃 | 모든 페이지 | Geometrixx Media만 해당 |
| 편집 가능한 템플릿 | 모든 페이지 | 사용할 수 없음 |
| HTL | 모든 구성 요소 | 제한적 |
| 타깃팅 | 모든 페이지 | Geometrixx Outdoors만 해당 |
| 스크린 | 사용 가능 | 사용할 수 없음 |
| 모바일 | 사용할 수 없음 | 사용 가능 |
| 원고 | 사용할 수 없음 | 사용 가능 |
| Carousel, 다운로드, 차트 구성 요소 | 사용할 수 없음 | 사용 가능 |
| 열 컨트롤 | 레이아웃 컨테이너로 대체 | 사용 가능 |
| 양식 | 사용할 수 없음 | 사용 가능 |
| 캠페인 | 이메일 샘플 없음 | 사용 가능 |

>[!NOTE]
>
>이 목록은 완성에 중점을 두지만 완전한 것으로 간주해서는 안 됩니다.

## Contribute {#contribute}

We.Retail은 오픈 소스 프로젝트로 릴리스되었으며 소스 코드의 최신 버전은 GitHub에서 다운로드할 수 있습니다.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-sample-we-retail 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

최신 릴리스는 설치 가능한 패키지로 [직접](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) 다운로드할 수도 있습니다.

문제가 발생하면 GitHub 문제를 [보고하십시오](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

자유롭게 포크를 하거나 [당기기 요청에](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)참여하십시오.

## 미리 보기 {#preview}

We.Retail 시작 페이지 미리 보기:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)

