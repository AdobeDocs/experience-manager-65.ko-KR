---
title: Edge Delivery Services 사용
description: Edge Delivery Services 사용
exl-id: 6c9178b0-c8f3-4fc7-8614-8e71ffc2f0b8
source-git-commit: d2c0dea636280c28e1d5a76d1c5375f21b6eb111
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 95%

---

# Edge Delivery Services 사용 {#usingedge}

Edge Delivery를 사용하면 작성자가 콘텐츠를 빠르게 업데이트 및 게시하고 새 사이트를 신속하게 시작할 수 있는 빠른 개발 환경을 제작할 수 있습니다. 이를 위해 동일한 웹 사이트에서 여러 콘텐츠 소스로 작업하고, 선택한 소스에 관계없이 게시를 간소화할 수 있습니다. 따라서 인터넷에서 라이브로 콘텐츠를 편집하고 보는 데까지 단 몇 초밖에 걸리지 않습니다.

## 작성 {#authoring-edge}

Edge Delivery를 사용하여 쉽고, 빠르고, 유연하게 콘텐츠를 작성할 수 있습니다. 두 가지 다른 경로를 선택하여 Edge Delivery Services 컨텍스트 내에서 콘텐츠를 작성할 수 있습니다.

* 문서 기반 작성(예: Microsoft Word 또는 Google Docs) - [자세한 내용은 이 링크 참조](https://www.hlx.live/docs/authoring).
* 페이지 편집기/Universal Editor - Adobe 영업 담당자에게 문의하십시오.

문서 기반 작성은 Microsoft Word 및 Google Docs와 같은 다양한 소스에서 작업할 수 있습니다. 이러한 소스의 문서는 웹 사이트의 페이지가 됩니다. 제목, 목록, 이미지, 글꼴 요소 및 비디오는 모두 초기 소스에서 내 웹 사이트로 전송할 수 있습니다. SEO 용도로 메타데이터를 추가하거나 블록을 사용하여 구조화된 콘텐츠로 작업하고 기능을 추가할 수 있습니다.

## 게시 {#publishing-edge}

Edge Delivery를 사용하여 콘텐츠 소스에 관계없이 원활하게 콘텐츠를 게시합니다. 프로세스는 다음과 같습니다. [Sidekick 확장 기능](#using-sidekick)을 사용하여 게시 메커니즘을 트리거하면 단 몇 초 만에 콘텐츠를 웹 사이트에 라이브로 제공할 수 있습니다.

## Edge Delivery Services 및 GitHub {#github-edge}

Edge Delivery는 GitHub를 사용하므로 고객은 GitHub 저장소에서 바로 코드를 관리 및 배포할 수 있습니다. 예를 들어 Google Docs 또는 Microsoft Word에서 콘텐츠를 작성할 수 있고, GitHub의 CSS 및 JavaScript를 사용하여 사이트 기능을 개발할 수 있습니다. 콘텐츠 미리보기부터 프로덕션까지 각 분기별로 웹 사이트가 자동으로 생성됩니다. GitHub 저장소에 저장된 모든 리소스는 빌드 프로세스 없이 웹 사이트에서 제공됩니다.

## Sidekick 사용 {#using-sidekick}

AEM Sidekick은 콘텐츠를 쉽게 편집하고, 미리 보고, 게시할 수 있도록 컨텍스트 인식 옵션이 포함된 도구 모음을 제공합니다. AEM Sidekick 확장 기능이 [설치](https://www.hlx.live/docs/sidekick-extension)되면 프로젝트 환경에서나 콘텐츠 편집 시(예: Google Docs에서) 사용할 수 있습니다. 환경에 따라 미리보기, 다시 로드, 편집 및 게시와 같은 몇 가지 액션이 제공됩니다. 미리보기부터 프로덕션까지 Sidekick을 사용하는 경우 환경을 전환할 수도 있으며, 그 반대의 경우도 마찬가지입니다.

**게시하려면** 미리보기 페이지에서 Sidekick을 열고 게시 액션을 사용합니다. 게시를 클릭하면 페이지의 현재 미리보기 버전이 라이브 및 프로덕션 환경에서 제공됩니다.

## AEM Assets를 문서 기반 작성과 통합 {#integrate-assets-edge}

Edge Delivery를 사용하면 Microsoft Word 또는 Google Docs에서 문서를 작성하는 동안 AEM Assets 저장소에서 제공되는 이미지를 사용할 수 있습니다.

문서 내에서 이미지를 사용하는 옵션은 [AEM Assets Sidekick 플러그인을 구성](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin)한 이후에만 제공됩니다.

AEM Assets용 Sidekick 플러그인은 다음에 대한 액세스 권한을 지원합니다.

* AEM Assets as a Cloud Service

* AEM Assets 기본 사항

AEM Assets Sidekick 플러그인을 구성한 후에는 [Microsoft Word 또는 Google Docs 문서 내에서 이미지 사용을 시작](https://www.hlx.live/docs/aem-assets-sidekick-plugin)할 수 있습니다.

## 추가 참조 {#further-reading}

자세한 내용은 다음 페이지를 참조하십시오.

* Edge Delivery를 시작하는 방법에 대한 자세한 내용은 Edge Delivery 설명서의 [빌드](https://www.hlx.live/docs/#build) 섹션을 참조하십시오.
* Edge Delivery를 사용하여 콘텐츠를 작성 및 게시하는 방법을 이해하려면 [게시 섹션](https://www.hlx.live/docs/authoring)을 참조하십시오.
* Sidekick 확장 기능을 사용하는 방법을 이해하려면 [Sidekick 사용](https://www.hlx.live/docs/sidekick) 페이지를 참조하십시오.
* AEM 작성에 대해서는 [작성 개념 페이지](/help/sites-authoring/author.md))
