---
title: AEM 저장소 도구
seo-title: AEM Repo Tool
description: AEM Repo Tool은 FTP와 비슷한 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 콘텐츠를 전송하는 간단한 솔루션입니다. AEM Repo Tool은 Jackrabbit FileVault 도구와 유사하지만 더 빠르고, 종속성이 거의 없으며, 간단한 bash 스크립트입니다.
seo-description: The AEM Repo Tool is a simple solution to transfer JCR content between your local filesystem and the AEM server via the command line comparable to FTP. The AEM Repo Tool is similar to the Jackrabbit FileVault tool, but is faster, has minimal dependencies, and is a simple bash script.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# AEM 저장소 도구{#aem-repo-tool}

AEM Repo Tool은 FTP와 비슷한 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 콘텐츠를 전송하는 간단한 솔루션입니다. AEM Repo Tool 은 [Jackrabbit FileVault 도구](/help/sites-developing/ht-vlttool.md)는 빠르지만 최소한의 종속성과 간단한 bash 스크립트입니다.

이 도구는 개발자의 파일 전송을 단순화하고 IntelliJ 및 Eclipse에 통합하여 개발을 보다 효율적으로 수행할 수도 있습니다.

## 개요 {#overview}

의 주어진 경로에 대해 `jcr_root` 파일 시스템의 filevault 구조인 AEM Repo Tool은 전체 하위 트리에 대해 단일 필터로 패키지를 생성하고 서버에 푸시합니다(FTP와 유사). `put`), 는 서버에서 가져옵니다( `get`) 또는 차이점을 비교합니다( `status` 및 `diff`).

여러 필터 경로 또는 FileVault를 지원하지 않습니다. `filter.xml`.

>[!CAUTION]
>
>AEM Repo Tool은 항상 지정된 전체 파일 또는 디렉토리를 덮어씁니다.

## 다운로드 및 설명서 {#download-and-documentation}

다음 [AEM 보고 도구는 이 링크를 통해 GitHub에서 사용할 수 있습니다](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) 자세한 설치 및 사용 지침과 함께 제공됩니다.

AEM Repo Tool의 소스를 다운로드하려면 아래 연결된 GitHub 프로젝트를 참조하십시오.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 도구 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/tools)
* 다음으로 프로젝트 다운로드 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
