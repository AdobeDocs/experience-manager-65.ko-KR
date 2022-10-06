---
title: 개발 도구
seo-title: Development Tools
description: JCR, Apache Sling 또는 AEM 애플리케이션을 개발하려면 많은 도구 세트를 사용할 수 있습니다
seo-description: To develop your JCR, Apache Sling or AEM applications, a number of tool sets are available
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 17%

---

# 개발 도구{#development-tools}

JCR, Apache Sling 또는 AEM 애플리케이션을 개발하려면 다음 도구 세트를 사용할 수 있습니다.

* 한 세트로 구성되어 있습니다 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 및 WebDAV를 참조하십시오. CRXDE Lite은 CRX/AEM에 포함되어 있으며 브라우저에서 표준 개발 작업을 수행할 수 있습니다. CRXDE Lite을 사용하여 SVN과 로그인하고 통합할 때 파일(예: .jsp 및 .java), 폴더, 템플릿, 구성 요소, 대화 상자, 노드, 속성 및 번들을 만들고 편집할 수 있습니다.

   CRX/AEM 서버에 직접 액세스할 수 없는 경우, 기본 구성 요소 및 Java 번들을 확장 또는 수정하여 애플리케이션을 개발하거나 전용 디버거, 코드 완료 및 구문 강조 표시가 필요하지 않은 경우 CRXDE Lite을 사용하는 것이 좋습니다.

* 통합 개발 환경으로 구성된 한 세트(예: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) 또는 [IntelliJ](/help/sites-developing/ht-intellij.md)), 빌드 도구(예: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault는 Adobe이 리포지토리를 파일 시스템에 매핑하기 위해 개발한(예: Subversion), 버그 추적기 시스템(예: 중앙 종속성 관리 시스템인 Jira(예: Apache Archiva) 및 빌드 자동화 시스템(예: Apache Continuum).

   이 설정을 사용하면 응용 프로그램(컨텐츠, 코드, 구성)을 모든 개발 환경과 프로세스에 완전히 통합할 수 있습니다.위의 모든 개발 도구가 파일을 사용하여 작업할 수 있으므로 다른 요소 간의 링크는 FileVault를 통해 저장소의 파일 시스템 표현입니다.

## 통합 개발 환경을 위한 확장 {#extensions-for-integrated-development-environments}

Adobe에서 다음 확장을 릴리스했습니다.

* [AEM Eclipse 확장](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets 확장](/help/sites-developing/aem-brackets.md)
* [AEM IntelliJ 확장](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf) (헤드와이어에서)

### 기타 도구 {#other-tools}

AEM은 개발을 용이하게 하는 다른 도구와 함께 제공됩니다.

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

새로운 프로젝트 작성을 용이하게 하는 도구:

* [AEM Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Lazybones 템플릿](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>새 AEM 프로젝트를 시작하기 위해 다음 자습서가 유용할 수 있습니다.
>[AEM Sites 시작하기 1부 - 프로젝트 설정](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
