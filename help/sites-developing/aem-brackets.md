---
title: AEM Brackets 확장
seo-title: AEM Brackets Extension
description: AEM Brackets 확장
seo-description: null
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 3%

---

# AEM Brackets 확장{#aem-brackets-extension}

## 개요 {#overview}

AEM Brackets 확장은 AEM 구성 요소와 클라이언트 라이브러리를 편집하는 원활한 워크플로우를 제공하고 의 기능을 활용합니다 [대괄호](https://brackets.io/) 코드 편집기: 코드 편집기 내에서 Photoshop 파일 및 레이어에 대한 액세스 권한을 제공합니다. 확장에서 제공하는 간편한 동기화(Maven 또는 File Vault 필요 없음)는 개발자 효율성을 높이고 제한된 AEM 지식을 갖춘 프런트 엔드 개발자도 프로젝트에 참여할 수 있도록 지원합니다. 이 확장은 또한 [HTL(HTML 템플릿 언어)](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)에서는 구성 요소를 보다 쉽고 안전하게 개발할 수 있도록 JSP의 복잡성을 줄입니다.

![chlimage_1-53](assets/chlimage_1-53a.png)

### 기능 {#features}

AEM Brackets 확장의 주요 기능은 다음과 같습니다.

* AEM 개발 인스턴스에 변경된 파일의 자동 동기화
* 파일 및 폴더의 수동 양방향 동기화
* 프로젝트의 전체 컨텐츠 패키지 동기화.
* 표현식 및 `data-sly-*` 차단 문.

또한 Brackets에는 AEM 글꼴 엔드 개발자에게 유용한 여러 기능이 포함되어 있습니다.

* Photoshop 파일은 레이어, 측정, 색상, 글꼴, 텍스트 등과 같은 PSD 파일에서 정보를 추출하도록 지원합니다.
* 코드에서 추출된 정보를 쉽게 재사용할 수 있도록 PSD의 코드 힌트입니다.
* LESS 및 SCSS와 같은 CSS 전처리기 지원.
* 그리고 보다 구체적인 요구 사항을 지원하는 수백 개의 추가 확장.

## 설치 {#installation}

### 대괄호 {#brackets}

AEM Brackets 확장은 Brackets 버전 1.0 이상을 지원합니다.

에서 최신 Brackets 버전을 다운로드합니다. [brackets.io](https://brackets.io/).

### 확장 {#the-extension}

확장을 설치하려면 다음 절차를 수행하십시오.

1. 대괄호를 엽니다. 메뉴에서 **파일**, 선택 **Extension Manager...**
1. Enter 키 **AEM** 검색 창에서 **AEM Brackets 확장**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 클릭 **설치**.
1. 설치가 완료된 후 대화 상자 및 Extension Manager을 닫습니다.

## 시작하기 {#getting-started}

### 컨텐츠 패키지 프로젝트 {#the-content-package-project}

확장이 설치되면 Brackets 를 사용하여 파일 시스템에서 컨텐츠 패키지 폴더를 열어 AEM 구성 요소 개발을 시작할 수 있습니다.

프로젝트에는 적어도 다음이 포함되어야 합니다.

1. a `jcr_root` 폴더(예: `myproject/jcr_root`)

1. a `filter.xml` 파일(예: `myproject/META-INF/vault/filter.xml`); 의 구조에 대한 자세한 내용은 `filter.xml` 파일을 참조하십시오. [작업 공간 필터 정의](https://jackrabbit.apache.org/filevault/filter.html).

대괄호 **파일** 메뉴, 선택 **폴더 열기...** 다음 중 하나를 선택합니다. `jcr_root` 폴더 또는 상위 프로젝트 폴더가 표시됩니다.

>[!NOTE]
>
>컨텐츠 패키지가 있는 자체 프로젝트가 없는 경우, [HTL TodoMVC 예](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). GitHub에서 **ZIP 다운로드**&#x200B;를 추출하여 로컬에서 파일을 추출하고 위의 지시에 따라 `jcr_root` Brackets 폴더 그런 다음 아래 단계에 따라 **프로젝트 설정**&#x200B;를 수행한 다음, 마지막으로 다음을 수행하여 전체 패키지를 AEM 개발 인스턴스에 업로드합니다. **컨텐츠 패키지 내보내기** 가 전체 컨텐츠 패키지 동기화 섹션에 자세히 설명되어 있는 대로
>
>이 단계를 수행한 후에는 `/content/todo.html` AEM 개발 인스턴스의 URL을 생성하고 Brackets에서 코드 수정을 시작하고 웹 브라우저에서 새로 고침을 수행한 후 변경 사항이 AEM 서버에 즉시 동기화되는 방법을 볼 수 있습니다.

### 프로젝트 설정 {#project-settings}

AEM 개발 인스턴스와 컨텐츠를 동기화하려면 프로젝트 설정을 정의해야 합니다. 이 작업은 로 이동하여 수행할 수 있습니다 **AEM** 메뉴 및 선택 **프로젝트 설정...**

![chlimage_1-55](assets/chlimage_1-55a.png)

프로젝트 설정에서 다음을 정의할 수 있습니다.

1. 서버 URL(예: `http://localhost:4502`)
1. 유효한 HTTPS 인증서가 없는 서버를 허용할지 여부(필요하지 않은 경우 선택 해제)
1. 컨텐츠 동기화에 사용되는 사용자 이름(예: `admin`)
1. 사용자의 암호(예: `admin`)

## 컨텐츠 동기화 {#synchronizing-content}

AEM Brackets 확장에서는 `filter.xml`:

### 변경된 파일의 자동 동기화 {#automated-synchronization-of-changed-files}

이렇게 하면 Brackets에서 AEM 인스턴스로 변경 사항만 동기화되지만 다른 방법으로는 동기화되지 않습니다.

### 수동 양방향 동기화 {#manual-bidirectional-synchronization}

프로젝트 탐색기에서 파일이나 폴더를 마우스 오른쪽 단추로 클릭하고 **서버로 내보내기** 또는 **서버에서 가져오기** 옵션에 액세스할 수 있습니다.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>선택한 항목이 `jcr_root` 폴더, **서버로 내보내기** 및 **서버에서 가져오기** 상황별 메뉴 항목을 사용할 수 없습니다.

### 전체 컨텐츠 패키지 동기화 {#full-content-package-synchronization}

에서 **AEM** 메뉴, **컨텐츠 패키지 내보내기** 또는 **컨텐츠 패키지 가져오기** 옵션을 사용하면 전체 프로젝트를 서버와 동기화할 수 있습니다.

![chlimage_1-57](assets/chlimage_1-57a.png)

### 동기화 상태 {#synchronization-status}

AEM Brackets Extension은 마지막 동기화 상태를 나타내는 Brackets 창 오른쪽 도구 모음에 알림 아이콘을 제공합니다.

* 녹색 - 모든 파일이 동기화되었습니다.
* 파란색 - 동기화 작업이 진행 중입니다.
* 노란색 - 일부 파일이 동기화되지 않았습니다.
* 빨간색 - 어떤 파일도 동기화되지 않았습니다.

알림 아이콘을 클릭하면 동기화된 각 파일의 모든 상태를 나열하는 동기화 상태 보고서 대화 상자가 열립니다.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>필터링 규칙에 따라 포함된 것으로 표시된 콘텐츠만 `filter.xml` 은 사용된 동기화 방법과 관계없이 동기화됩니다.
>
>또한, `.vltignore` 파일은 컨텐츠가 저장소에서 동기화되거나 동기화되지 않도록 제외하도록 지원됩니다.

## HTL 코드 편집 {#editing-htl-code}

AEM Brackets 확장에서는 HTL 속성 및 표현식의 작성을 용이하게 하기 위한 일부 자동 완성 기능을 제공합니다.

### 속성 자동 완성 {#attribute-auto-completion}

1. HTML 속성에서 다음을 입력합니다 `sly`. 속성은 자동으로 다음으로 완료됩니다. `data-sly-`.
1. 드롭다운 목록에서 HTL 속성을 선택합니다.

### 표현식 자동 완성 {#expression-auto-completion}

표현식 내에서 `${}`를 입력하면 일반적인 변수 이름이 자동으로 완료됩니다.

## 추가 정보 {#more-information}

AEM Brackets 확장은 오픈 소스 프로젝트로서, [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) 조직, Apache 라이센스 아래 버전 2.0:

* 코드 저장소: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache 라이센스, 버전 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

괄호 코드 편집기는 또한 [Adobe Systems Incorporated](https://github.com/adobe) 조직:

* 코드 저장소: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

자유롭게 기여하십시오!
