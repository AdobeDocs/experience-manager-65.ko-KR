---
title: AEM 6.5 Forms에서 적응형 Forms 핵심 구성 요소를 활성화하는 방법
seo-title: How to enable Adaptive Forms Core Components on AEM 6.5 Forms?
description: AEM 6.5 Forms 환경에서 적응형 Forms 핵심 구성 요소를 활성화하는 데 도움이 되는 단계별 안내서입니다.
seo-description: Step-by-Step guide to help you enable Adaptive Forms Core Components on an AEM 6.5 Forms environment.
keywords: 핵심 구성 요소, 핵심 구성 요소 적응형 Forms, 6.5의 핵심 구성 요소, AEM 6.5의 적응형 Forms 핵심 구성 요소, AEM 6.5의 AF 핵심 구성 요소, AEM 6.5 Forms 핵심 구성 요소 활성화
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 00f8b2c72aab37a57ab76e684f432250d2de3470
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 21%

---


# AEM 6.5 Forms에서 적응형 Forms 핵심 구성 요소 활성화 {#enable-adaptive-forms-core-components}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM 6.5 | 이 문서 |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |

**적용 대상:** ✅ 양식 핵심 구성 요소 ❎ 적응형 양식 기초 구성 요소

적응형 Forms 핵심 구성 요소를 활성화하면 만들기, 게시 및 전달을 시작할 수 있습니다 [적응형 Forms 기반의 핵심 구성 요소](create-an-adaptive-form-core-components.md) 및 [헤드리스 적응형 Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) AEM 6.5 Forms 환경에서.

AEM 6.5 Forms 환경에서 HAdapptive Forms 핵심 구성 요소를 활성화하려면 다음을 설정 및 배포합니다. [AEM Archetype 41 이상](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 모든 작성자 및 게시 인스턴스에 대한 기반 프로젝트(양식 옵션 활성화).

이 문서에서는 적응형 Forms 핵심 구성 요소를 활성화하기 위해 AEM 6.5 Forms 환경에서 AEM Archetype 41 이상 프로젝트를 설정하고 배포하는 방법에 대한 자세한 지침을 제공합니다.


## 사전 요구 사항 {#prerequisites}

AEM 6.5 Forms 환경에서 적응형 Forms 핵심 구성 요소를 활성화하기 전에:

* [AEM 6.5 Forms 서비스 팩 16(6.5.16.0) 이상으로 업그레이드](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* 의 최신 릴리스 설치 [Apache Maven](https://maven.apache.org/download.cgi).

* 일반 텍스트 편집기를 설치합니다. 예를 들어 Microsoft Visual Studio Code입니다.

## 최신 AEM Archetype 기반 프로젝트 생성 및 배포

AEM Archetype 41을 생성하려면 [나중에](https://github.com/adobe/aem-project-archetype) 를 기반으로 프로젝트를 제작하여 모든 작성자 및 게시 인스턴스에 배포합니다.

1. 컴퓨터에 로그인하여 AEM 6.5 Forms 인스턴스를 호스팅 및 실행합니다.
1. 명령 프롬프트 또는 터미널을 열고 다음 명령을 실행하여 AEM Archetype 프로젝트(양식 옵션 사용)를 생성합니다.

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux 또는 Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   위의 명령을 실행할 때는 다음 사항을 고려해야 합니다.

   * 의 값을 변경하지 마십시오. `aemVersion` 다음에서 속성 `6.5.15.0` 다른 것으로요

   * 설정 `archetypeVersion` 다음으로 속성: `41` 나중에 최신 버전은 의 시스템 요구 사항 섹션을 참조하십시오. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) 설명서를 참조하십시오.

   * 다음을 포함한 환경의 특정 값을 반영하도록 명령 업데이트 `appTitle`, `appId`, 및 `groupId`. 또한 의 값을 설정합니다.  `includeFormsenrollment` 다음으로 속성: `y`. Forms 포털을 사용하는 경우 `includeExamples=y` 선택 사항을 사용하여 프로젝트에 Forms 포털 핵심 구성 요소를 포함할 수 있습니다.


1. (Archetype 버전 41 기반 프로젝트만 해당) AEM Archetype 프로젝트가 생성되면 적응형 Forms 기반의 핵심 구성 요소에 대해 테마를 활성화합니다. 테마를 활성화하려면 다음을 수행하십시오.

   1. 를 엽니다. [AEM Archetype 프로젝트 폴더]/ui.apps/src/main/content/jcr_root/apps/__appId__&#x200B;편집용 /components/adaptiveForm/page/customheaderlibs.html:

   1. 21행에 다음 코드를 추가합니다.

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![21행에 위에서 언급한 코드를 추가합니다.](/help/forms/using/assets/code-to-enable-themes.png)

   1. 파일을 저장하고 닫습니다.

1. 최신 버전의 Forms 핵심 구성 요소를 포함하도록 프로젝트 업데이트:

   1. 를 엽니다. [AEM Archetype 프로젝트 폴더]/pom.xml을 참조하십시오.
   1. 버전 설정 `core.forms.components.version` 및 `core.forms.components.af.version` 끝 [최신 Forms 핵심 구성 요소](https://github.com/adobe/aem-core-forms-components/tree/release/650) 버전.

   1. 파일을 저장하고 닫습니다.


1. AEM Archetype 프로젝트가 정상적으로 생성되면 환경에 대한 배포 패키지를 빌드합니다. 패키지를 빌드하려면:

   1. AEM Archetype 프로젝트의 루트 디렉토리로 이동합니다.

   1. 다음 명령을 실행하여 환경에 맞는 AEM Archetype 프로젝트를 빌드합니다.

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   AEM Archetype 프로젝트가 성공적으로 빌드되면 AEM 패키지가 생성됩니다. 패키지는 다음 위치에서 찾을 수 있습니다. [AEM Archetype 프로젝트 폴더]\all\target\[appid].all-[버전].zip

1. 사용 [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en) 를 배포하려면 [AEM Archetype 프로젝트 폴더]\all\target\[appid].all-[버전].zip 패키지를 모든 Author 및 Publish 인스턴스에 추가합니다.

>[!NOTE]
>
>
>
> * 게시 인스턴스의 로그인 대화 상자에 액세스하는 데 문제가 있는 경우 패키지 관리자를 통해 패키지를 설치하려면 다음 URL을 사용해 보십시오. `http://[Publish Server URL]:[PORT]/system/console` 로그인합니다. 게시 인스턴스의 로그인 페이지에 액세스하여 설치 프로세스를 진행할 수 있습니다.
> * Archetype 프로젝트를 환경에 배포한 후 삭제하거나 삭제하지 마십시오. 사용자 정의 및 새로운 적응형 Forms 핵심 구성 요소 테마를 환경에 추가하려면 Archetype 프로젝트가 필요합니다.

사용자 환경에 대해 핵심 구성 요소가 활성화됩니다. 빈 적응형 양식 템플릿 및 Canvas 3.0 테마가 환경에 배포되어 다음과 같은 작업을 수행할 수 있습니다. [적응형 Forms 기반의 핵심 구성 요소 만들기](create-an-adaptive-form-core-components.md).

## 자주 묻는 질문

### 핵심 구성 요소란 무엇입니까?

[핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)는 AEM에서 개발 시간을 가속화고 웹 사이트의 유지 관리 비용을 절감할 수 있는 표준화된 웹 콘텐츠 관리(WCM) 구성 요소입니다.

### 핵심 구성 요소 활성화에 추가된 기능은 무엇입니까?


내 환경에 맞는 적응형 양식 핵심 구성 요소가 활성화되면 빈 핵심 구성 요소 기반 적응형 양식 템플릿 및 Canvas 3.0 테마가 해당 환경에 추가됩니다. 내 환경에 맞는 적응형 양식 핵심 구성 요소가 활성화되면 다음과 같은 작업을 수행할 수 있습니다.

* 핵심 구성 요소 기반 적응형 양식 만들기.
* 핵심 구성 요소 기반 적응형 양식 템플릿 만들기.
* 핵심 구성 요소 기반 적응형 양식 템플릿의 사용자 정의 테마 만들기.
* 모바일, 웹, 기본 앱 등 채널과 양식의 Headless 표현식이 필요한 서비스에 핵심 구성 요소 기반 적응형 양식의 JSON 표현식 제공.

## 다음 단계

* [핵심 구성 요소 기반 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md)
* [AEM Sites 페이지 또는 경험 조각에 적응형 양식 만들기 또는 추가](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [적응형 Forms 기반의 핵심 구성 요소에 대한 테마 만들기](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [적응형 Forms 기반의 핵심 구성 요소용 템플릿 만들기](template-editor.md)