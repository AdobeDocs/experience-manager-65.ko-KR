---
title: Edge Delivery Services 사용
description: Edge Delivery Services 사용
source-git-commit: 0c0e14ec3d022b7e9efd17edf2997990f5ac3dc2
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---

# Edge Delivery Services 사용 {#usingedge}

Edge Delivery를 통해 작성자가 콘텐츠를 빠르게 업데이트하고 게시할 수 있으며 새로운 사이트를 빠르게 시작할 수 있는 신속한 개발 환경을 구축할 수 있습니다. 이를 위해 동일한 웹 사이트에서 여러 컨텐츠 소스로 작업할 수 있으며 선택한 소스에 관계없이 게시가 원활하고 간소화됩니다. 따라서 콘텐츠를 인터넷에서 실시간으로 보려면 편집부터 표시까지 불과 몇 초 밖에 걸리지 않습니다.

## 작성 {#authoring-edge}

Edge Delivery를 통해 쉽고 빠르고 유연하게 작성할 수 있습니다. Edge Delivery Services 컨텍스트 내에서 작성하려면 두 개의 서로 다른 경로를 사용할 수 있습니다.

* 문서 기반 작성(Microsoft Word 또는 Google 문서) - [자세한 내용은 이 링크 를 참조하십시오](https://www.hlx.live/docs/authoring).
* 페이지 편집기/범용 편집기 - Adobe 영업 담당자에게 문의하십시오.

문서 기반 작성의 경우 Microsoft Word 및 Google Docs와 같은 다양한 소스를 사용하여 작업할 수 있습니다. 이러한 소스의 문서는 웹 사이트의 페이지가 됩니다. 제목, 목록, 이미지, 글꼴 요소, 비디오 모두 초기 소스에서 웹 사이트로 전송할 수 있습니다. SEO 용도로 메타데이터를 추가하거나 블록을 사용하여 구조화된 컨텐츠로 작업하고 기능을 추가할 수 있습니다.

## 게시 {#publishing-edge}

Edge Delivery를 통해 콘텐츠 소스에 관계없이 콘텐츠 게시가 원활하게 수행됩니다. 프로세스는 다음과 같습니다. [사이드 킥 확장](#using-sidekick) 게시 메커니즘을 트리거하면 몇 초 후에 웹 사이트에서 콘텐츠를 라이브로 사용할 수 있습니다.

## Edge Delivery Services 및 GitHub {#github-edge}

Edge Delivery는 GitHub를 활용하므로 고객은 GitHub 저장소에서 직접 코드를 관리하고 배포할 수 있습니다. 예를 들어 GitHub에서 CSS와 JavaScript를 사용하여 Google 문서 또는 Microsoft Word로 콘텐츠를 작성하고 사이트의 기능을 개발할 수 있습니다. 웹 사이트는 콘텐츠 미리보기에서 프로덕션에 이르기까지 각 분기에 대해 자동으로 만들어집니다. GitHub 저장소에 입력하는 모든 리소스는 빌드 프로세스 없이 웹 사이트에서 사용할 수 있습니다.

## Sidekick 사용 {#using-sidekick}

AEM 사이드 킥은 컨텐츠를 쉽게 편집하고, 미리 보고, 게시할 수 있도록 컨텍스트 인식 옵션이 있는 도구 모음을 제공합니다. 다음 이후 [설치](https://www.hlx.live/docs/sidekick-extension) AEM 사이드 킥 확장은 프로젝트 환경 또는 콘텐츠를 편집할 때(예: Google 문서에서) 사용할 수 있습니다. 환경에 따라 미리 보기, 다시 로드, 편집 및 게시 등 여러 작업을 사용할 수 있습니다. 미리보기에서 프로덕션으로 또는 그 반대로 사이드 킥을 사용할 때 환경을 전환할 수도 있습니다.

**게시하려면**&#x200B;를 클릭하고 미리 보기 페이지에서 사이드 킥을 연 다음 게시 작업을 사용합니다. 게시 를 클릭하면 페이지의 현재 미리보기 버전을 라이브 및 프로덕션 환경에서 사용할 수 있습니다.

## 문서 기반 작성과 AEM Assets 통합 {#integrate-assets-edge}

Edge Delivery를 사용하면 Microsoft Word 또는 AEM Assets 문서에서 문서를 작성하는 동안 Google 저장소에서 사용할 수 있는 이미지를 사용할 수 있습니다.

문서 내에서 이미지를 사용하는 옵션은 다음 경우에만 사용할 수 있습니다. [AEM Assets 사이드 킥 플러그인 구성](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin).

AEM Assets용 사이드 킥 플러그인은 다음에 대한 액세스를 지원합니다.

* AEM Assets as a Cloud Service

* AEM Assets Essentials

AEM Assets 사이드 킥 플러그인을 구성한 후 다음을 수행할 수 있습니다. [Google 문서 또는 Microsoft Word 문서에서 이미지 사용 시작](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## 추가 읽기 {#further-reading}

자세한 내용은 다음 페이지를 참조하십시오.

* Edge 전달을 시작하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [빌드](https://www.hlx.live/docs/#build) 섹션 을 참조하십시오.
* Edge Delivery를 사용하여 콘텐츠를 작성 및 게시하는 방법을 이해하려면 다음을 참조하십시오. [섹션 게시](https://www.hlx.live/docs/authoring).
* 사이드 킥 확장을 사용하는 방법을 이해하려면 를 참조하십시오. [사이드 킥 사용](https://www.hlx.live/docs/sidekick) 페이지를 가리키도록 업데이트하는 중입니다.
* AEM 작성에 대해서는 [작성 개념 페이지](/help/sites-authoring/author.md))
