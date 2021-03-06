---
title: AEM Repo Tool
seo-title: AEM 보고 도구
description: AEM Repo Tool 은 FTP와 비교할 수 있는 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 컨텐츠를 전송하는 간단한 솔루션입니다. AEM Repo Tool은 Jackrabbit FileVault 도구와 유사하지만 더 빨라지고, 최소한의 종속성과 간단한 Bash 스크립트입니다.
seo-description: AEM Repo Tool 은 FTP와 비교할 수 있는 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 컨텐츠를 전송하는 간단한 솔루션입니다. AEM Repo Tool은 Jackrabbit FileVault 도구와 유사하지만 더 빨라지고, 최소한의 종속성과 간단한 Bash 스크립트입니다.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 2%

---

# AEM Repo Tool{#aem-repo-tool}

AEM Repo Tool 은 FTP와 비교할 수 있는 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 컨텐츠를 전송하는 간단한 솔루션입니다. AEM Repo Tool은 [Jackrabbit FileVault 도구](/help/sites-developing/ht-vlttool.md)와 유사하지만, 속도가 빠르며, 종속성이 최소화되며, 간단한 Bash 스크립트입니다.

이 도구를 사용하면 개발자를 위한 파일 전송을 간소화할 수 있고 IntelliJ 및 Eclipse에 통합하여 개발 효율을 높일 수 있습니다.

## 개요 {#overview}

파일 시스템의 `jcr_root` 파일 구조 내의 지정된 경로에 대해 AEM Repo Tool은 전체 하위 트리에 대한 단일 필터가 있는 패키지를 만들어 서버(FTP `put`과 유사)에 푸시하거나, 서버( `get`)에서 가져오거나( `status` 및 `diff`)를 비교합니다.

이 도구는 여러 필터 경로나 FileVault의 `filter.xml`를 지원하지 않습니다.

>[!CAUTION]
>
>AEM Repo Tool은 항상 지정된 전체 파일 또는 디렉토리를 덮어씁니다.

## 다운로드 및 설명서 {#download-and-documentation}

[AEM Repo Tool은 세부 설치 및 사용 지침과 함께 이 링크](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)를 통해 GitHub에서 사용할 수 있습니다.

AEM Repo Tool의 소스를 다운로드하려면 아래에 연결된 GitHub 프로젝트를 참조하십시오.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 도구 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/tools)
* 프로젝트를 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)로 다운로드합니다
