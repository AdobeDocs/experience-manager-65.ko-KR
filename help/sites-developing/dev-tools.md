---
title: 개발 도구
description: JCR, Apache Sling 또는 Adobe Experience Manager 애플리케이션을 개발하기 위해 몇 가지 도구 세트를 사용할 수 있습니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
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
source-wordcount: '394'
ht-degree: 17%
---
# 개발 도구{#development-tools}

JCR, Apache Sling 또는 Adobe Experience Manager(AEM) 애플리케이션을 개발하기 위해 다음 도구 세트를 사용할 수 있습니다.

* [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 및 WebDAV로 구성된 한 집합입니다. CRXDE Lite은 CRX/AEM에 내장되어 있으며, 이를 통해 브라우저에서 표준 개발 작업을 수행할 수 있습니다. CRXDE Lite을 사용하면 SVN에 로그인하고 통합하는 동안 파일(.jsp 및 .java 등), 폴더, 템플릿, 구성 요소, 대화 상자, 노드, 속성 및 번들을 만들고 편집할 수 있습니다.

  CRXDE Lite/AEM 서버에 직접 액세스할 수 없는 경우, 기본 제공 구성 요소 및 Java™ 번들을 확장 또는 수정하여 애플리케이션을 개발하는 경우 또는 전용 디버거, 코드 완성 및 구문 강조 표시가 필요하지 않은 경우 CRX을 사용하는 것이 좋습니다.

* 한 세트는 다음과 같이 구성됩니다.
  * 통합 개발 환경. 예: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) 또는 [IntelliJ](/help/sites-developing/ht-intellij.md).
  * 빌드 도구입니다. 예: [Apache Maven](/help/sites-developing/ht-projects-maven.md).
  * Adobe에서 개발하여 저장소를 파일 시스템(버전 제어 시스템)에 매핑하는 FileVault 예: Subversion.
  * 버그 추적기 시스템. 예를 들어, Jira입니다.
  * 중앙 종속성 관리 시스템입니다. 예: Apache Archiva.
  * 빌드 자동화 시스템. 예를 들어 Apache Continuum입니다.

  이 설정을 사용하면 애플리케이션(콘텐츠, 코드, 구성)을 모든 개발 환경 및 프로세스에 완전히 통합할 수 있습니다. 이전에 언급된 모든 개발 도구가 파일에서 작동할 수 있으므로 서로 다른 요소 간의 링크는 FileVault를 통한 저장소의 파일 시스템 표현입니다.

## 통합 개발 환경을 위한 확장 {#extensions-for-integrated-development-environments}

Adobe은 다음 확장을 릴리스했습니다.

* [AEM Eclipse 확장](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets 확장](/help/sites-developing/aem-brackets.md)

### 기타 도구 {#other-tools}

AEM은 개발을 용이하게 하는 기타 도구와 함께 제공됩니다.

* [대화 상자 편집기](/help/sites-developing/dialog-editor.md)
* [번역기를 사용하여 사전 관리](/help/sites-developing/i18n-translator.md)
* [Maven을 사용한 패키지 관리](/help/sites-developing/vlt-mavenplugin.md)
* [Eclipse를 사용하여 AEM 프로젝트를 개발하는 방법](/help/sites-developing/howto-projects-eclipse.md)
* [Apache Maven을 사용하여 AEM 프로젝트를 작성하는 방법](/help/sites-developing/ht-projects-maven.md)
* [IntelliJ IDEA를 사용하여 AEM 프로젝트를 개발하는 방법](/help/sites-developing/ht-intellij.md)
* [VLT 도구 사용 방법](/help/sites-developing/ht-vlttool.md)
* [프록시 서버 도구 사용 방법](/help/sites-developing/ht-proxy-server.md)
* [AEM 현대화 도구](/help/sites-developing/modernization-tools.md)
* [AEM 저장소 도구](/help/sites-developing/aem-repo-tool.md)

새 프로젝트를 쉽게 만들 수 있는 도구:

* [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
* [AEM 레이저본스 틀](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>다음 튜토리얼은 새 AEM 프로젝트를 시작하는 데 도움이 될 수 있습니다.
>[AEM Sites 1부 시작 - 프로젝트 설정](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
