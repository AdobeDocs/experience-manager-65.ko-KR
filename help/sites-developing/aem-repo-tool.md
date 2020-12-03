---
title: AEM Repo Tool
seo-title: AEM 보고서 도구
description: AEM 보고서 도구는 FTP와 비교할 수 있는 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 컨텐츠를 전송하는 간단한 솔루션입니다. AEM Repo Tool은 Jackrabbit FileVault 도구와 유사하지만 더 빨라지고, 의존성이 거의 없으며, 간단한 배쉬 스크립트입니다.
seo-description: AEM 보고서 도구는 FTP와 비교할 수 있는 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 컨텐츠를 전송하는 간단한 솔루션입니다. AEM Repo Tool은 Jackrabbit FileVault 도구와 유사하지만 더 빨라지고, 의존성이 거의 없으며, 간단한 배쉬 스크립트입니다.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 2%

---


# AEM Repo Tool{#aem-repo-tool}

AEM 보고서 도구는 FTP와 비교할 수 있는 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 컨텐츠를 전송하는 간단한 솔루션입니다. AEM Repo 도구는 [Jackrabbit FileVault 도구](/help/sites-developing/ht-vlttool.md)와 비슷하지만, 더 빨라지고, 최소 종속성을 가지며, 간단한 배시 스크립트입니다.

이 툴을 사용하면 개발자를 위한 파일 전송을 간소화할 수 있고 IntelliJ 및 Eclipse에 통합하여 개발 효율성을 높일 수 있습니다.

## 개요 {#overview}

파일 시스템의 `jcr_root` 파일 구조 내의 지정된 경로에 대해 AEM Repo Tool은 전체 하위 트리에 대해 단일 필터가 있는 패키지를 생성하여 서버로 푸시합니다(FTP `put`과 유사). 서버에서 해당 패키지를 가져오거나 ( `status` 및 `diff`) 차이점을 비교합니다.`get`

도구는 여러 필터 경로 또는 FileVault의 `filter.xml`를 지원하지 않습니다.

>[!CAUTION]
>
>AEM 보고서 도구는 지정된 전체 파일 또는 디렉토리를 항상 덮어씁니다.

## 다운로드 및 설명서 {#download-and-documentation}

[AEM 보고서 도구는 자세한 설치 및 사용 지침과 함께 이 링크](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)를 통해 GitHub에서 사용할 수 있습니다.

AEM 보고서 툴의 소스를 다운로드하려면 아래 링크된 GitHub 프로젝트를 참조하십시오.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 툴 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/tools)
* 프로젝트를 ZIP 파일](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)으로 다운로드합니다.[

