---
title: AEM 저장소 도구
description: AEM Repo Tool은 FTP와 비슷한 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 콘텐츠를 전송하는 간단한 솔루션입니다. AEM Repo Tool은 Jackrabbit FileVault 도구와 유사하지만 더 빠르고, 종속성이 거의 없으며, 간단한 bash 스크립트입니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%
---
# AEM 저장소 도구{#aem-repo-tool}

AEM Repo Tool은 FTP와 비슷한 명령줄을 통해 로컬 파일 시스템과 AEM 서버 간에 JCR 콘텐츠를 전송하는 간단한 솔루션입니다. AEM Repo Tool은 [Jackrabbit FileVault 도구](/help/sites-developing/ht-vlttool.md)와 유사하지만 더 빠르며 종속성이 거의 없으며 간단한 bash 스크립트입니다.

이 도구는 개발자의 파일 전송을 단순화하고 IntelliJ 및 Eclipse에 통합하여 개발을 보다 효율적으로 수행할 수도 있습니다.

## 개요 {#overview}

파일 시스템의 `jcr_root` Filevault 구조 내에 지정된 경로에 대해 AEM Repo Tool은 전체 하위 트리에 대해 단일 필터를 사용하여 패키지를 만들고 이를 서버로 푸시하고(FTP `put`과(와) 서버(`get`)에서 가져오거나 차이점(`status` 및 `diff`)을 비교합니다.

여러 필터 경로 또는 FileVault의 `filter.xml`을(를) 지원하지 않습니다.

>[!CAUTION]
>
>AEM Repo Tool은 항상 지정된 전체 파일 또는 디렉토리를 덮어씁니다.

## 다운로드 및 설명서 {#download-and-documentation}

[AEM 보고 도구는 자세한 설치 및 사용 지침과 함께 이 링크](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)를 통해 GitHub에서 사용할 수 있습니다.

AEM Repo Tool의 소스를 다운로드하려면 아래 연결된 GitHub 프로젝트를 참조하십시오.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 도구 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/tools)
* 프로젝트를 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)&#x200B;(으)로 다운로드
