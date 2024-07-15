---
title: AEM 6.5 Forms에서 적응형 Forms 핵심 구성 요소를 활성화하는 방법
description: AEM 6.5 Forms 환경에서 적응형 Forms 핵심 구성 요소를 활성화하는 데 도움이 되는 단계별 안내서입니다.
keywords: 핵심 구성 요소, 핵심 구성 요소 적응형 Forms, 6.5의 핵심 구성 요소, AEM 6.5의 적응형 Forms 핵심 구성 요소, AEM 6.5의 AF 핵심 구성 요소, AEM 6.5 Forms 핵심 구성 요소 활성화
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 11%

---

# AEM 6.5 Forms에서 적응형 Forms 핵심 구성 요소 활성화 {#enable-adaptive-forms-core-components}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html) |
| AEM 6.5 | 이 문서 |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

적응형 Forms 핵심 구성 요소를 활성화하면 AEM 6.5 Forms 환경에서 [적응형 Forms을 기반으로 한 핵심 구성 요소](create-an-adaptive-form-core-components.md) 및 [헤드리스 적응형 Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)를 만들고, 게시하고, 제공할 수 있습니다.

AEM 6.5 Forms 환경에서 적응형 Forms 핵심 구성 요소를 활성화하려면 모든 작성자 및 Publish 인스턴스에서 [AEM Archetype 41 이상](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 기반 프로젝트(양식 옵션 사용)를 설정하고 배포합니다.

이 문서에서는 적응형 Forms 핵심 구성 요소를 활성화하기 위해 AEM 6.5 Forms 환경에서 AEM Archetype 41 이상 프로젝트를 설정하고 배포하는 방법에 대한 자세한 지침을 제공합니다. Forms 핵심 구성 요소를 활성화하기 위해 아래 목록에서 **AEM 6.5** 호환 버전을 참조할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

AEM 6.5 Forms 환경에서 적응형 Forms 핵심 구성 요소를 활성화하기 전에:

* [AEM 6.5 Forms 서비스 팩 16(6.5.16.0) 이상으로 업그레이드](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* [Apache Maven](https://maven.apache.org/download.cgi)의 최신 릴리스를 설치하십시오.

* 일반 텍스트 편집기를 설치합니다. 예를 들어 Microsoft Visual Studio Code입니다.

## 최신 AEM Archetype 기반 프로젝트 생성 및 배포

AEM Archetype 41 또는 [이후](https://github.com/adobe/aem-project-archetype) 기반 프로젝트를 만들고 모든 작성자 및 Publish 인스턴스에 배포하려면 다음을 수행하십시오.

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

   * `aemVersion` 속성의 값을 `6.5.15.0`에서 다른 값으로 변경하지 마십시오.

   * `archetypeVersion` 속성을 `41` 이상으로 설정하십시오. 최신 버전은 [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) 설명서의 시스템 요구 사항 섹션을 참조하십시오.

   * `appTitle`, `appId` 및 `groupId`을(를) 포함하여 환경에 대한 특정 값을 반영하도록 명령을 업데이트합니다. 또한 `includeFormsenrollment` 속성의 값을 `y`(으)로 설정하십시오. Forms 포털을 사용하는 경우 `includeExamples=y` 옵션을 설정하여 프로젝트에 Forms 포털 핵심 구성 요소를 포함하십시오.


1. (Archetype 버전 41 기반 프로젝트만 해당) AEM Archetype 프로젝트가 생성되면 적응형 Forms 기반의 핵심 구성 요소에 대해 테마를 활성화합니다. 테마를 활성화하려면 다음을 수행하십시오.

   1. 편집할 [AEM Archetype 프로젝트 폴더]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html을 엽니다.

   1. 21행에 다음 코드를 추가합니다.

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![위에 언급된 코드를 21행에 추가](/help/forms/using/assets/code-to-enable-themes.png)

   1. 파일을 저장하고 닫습니다.

1. 최신 버전의 Forms 핵심 구성 요소를 포함하도록 프로젝트 업데이트:

   1. 편집할 [AEM Archetype 프로젝트 폴더]/pom.xml을 엽니다.
   1. `core.forms.components.version` 및 `core.forms.components.af.version`의 버전을 [최신 Forms 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history) 버전으로 설정하고, 두 구성 요소의 버전이 표에 언급된 **Forms 핵심 구성 요소**&#x200B;와(과) 동일한지 확인하고, [WCM 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/versions.html)에 지정된 대로 `core.wcm.components.version`의 버전을 설정하십시오.

      >[!WARNING]
      >
      >* 버전 45의 Archetype 프로젝트를 만들 때 `[AEM Archetype Project Folder]/pom.xml`은(는) 처음에 양식 핵심 구성 요소 버전을 1.1.28로 설정합니다. Archetype 프로젝트를 빌드하거나 배포하기 전에 Forms 핵심 구성 요소 버전을 1.1.26으로 업데이트합니다. [AEM 6.5 Forms 버전 내역](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history)에서 최신 버전을 찾을 수 있습니다.

      >[!NOTE]
      >
      >* 다른 토폴로지를 설정하는 경우 제출, 미리 채우기 및 기타 URL을 Dispatcher 레이어의 허용 목록에 추가하다에 추가해야 합니다.

   1. 파일을 저장하고 닫습니다.


1. AEM Archetype 프로젝트가 정상적으로 생성되면 환경에 대한 배포 패키지를 빌드합니다. 패키지를 빌드하려면:

   1. AEM Archetype 프로젝트의 루트 디렉토리로 이동합니다.

   1. 다음 명령을 실행하여 환경에 맞는 AEM Archetype 프로젝트를 빌드합니다.

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   AEM Archetype 프로젝트가 성공적으로 빌드되면 AEM 패키지가 생성됩니다. 패키지는 [AEM Archetype 프로젝트 폴더]\all\target\[appid].all-[버전].zip에서 찾을 수 있습니다.

1. [패키지 관리자](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en)를 사용하여 모든 작성자 및 Publish 인스턴스에 [AEM Archetype 프로젝트 폴더]\all\target\[appid].all-[버전].zip 패키지를 배포하십시오.

>[!NOTE]
>
>
>
> * 게시 인스턴스의 로그인 대화 상자에 액세스하는 데 문제가 있는 경우 패키지 관리자를 통해 패키지를 설치하려면 URL `http://[Publish Server URL]:[PORT]/system/console`을(를) 사용하여 로그인하십시오. 이렇게 하면 Publish 인스턴스의 로그인 페이지에 액세스할 수 있으므로 설치 프로세스를 계속 진행할 수 있습니다.
> * Archetype 프로젝트를 환경에 배포한 후 삭제하거나 삭제하지 마십시오. 사용자 정의 및 새로운 적응형 Forms 핵심 구성 요소 테마를 환경에 추가하려면 Archetype 프로젝트가 필요합니다.

사용자 환경에 대해 핵심 구성 요소가 활성화됩니다. 빈 적응형 양식 템플릿 기반 핵심 구성 요소와 Canvas 3.0 테마가 환경에 배포되어 [적응형 Forms 기반 핵심 구성 요소를 만들 수 있습니다](create-an-adaptive-form-core-components.md).

## 자주 묻는 질문

### 핵심 구성 요소란 무엇입니까?

[핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko-KR)는 AEM에서 개발 시간을 가속화고 웹 사이트의 유지 관리 비용을 절감할 수 있는 표준화된 웹 콘텐츠 관리(WCM) 구성 요소입니다.

### 핵심 구성 요소 활성화에 추가된 기능은 무엇입니까?


내 환경에 맞는 적응형 양식 핵심 구성 요소가 활성화되면 빈 핵심 구성 요소 기반 적응형 양식 템플릿 및 Canvas 3.0 테마가 해당 환경에 추가됩니다. 내 환경에 맞는 적응형 양식 핵심 구성 요소가 활성화되면 다음과 같은 작업을 수행할 수 있습니다.

* 적응형 Forms 기반의 핵심 구성 요소 만들기
* 적응형 양식 템플릿을 기반으로 핵심 구성 요소를 만듭니다.
* 적응형 양식 템플릿을 기반으로 핵심 구성 요소에 대한 사용자 지정 테마를 만듭니다.
* 모바일, 웹, 기본 앱 및 양식의 Headless 표시가 필요한 서비스와 같은 채널에 핵심 구성 요소 기반 적응형 양식의 JSON 표시를 제공합니다.

## 다음 단계

* [핵심 구성 요소 기반 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md)
* [AEM Sites 페이지 또는 경험 조각에 적응형 양식 만들기 또는 추가](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [적응형 Forms 기반의 핵심 구성 요소에 대한 테마 만들기](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [적응형 Forms 기반의 핵심 구성 요소용 템플릿 만들기](template-editor.md)
