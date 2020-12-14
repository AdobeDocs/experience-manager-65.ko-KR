---
title: AEM Brackets 확장
seo-title: AEM Brackets 확장
description: 'null'
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 3%

---


# AEM Brackets 확장{#aem-brackets-extension}

## 개요 {#overview}

AEM Brackets Extension은 AEM 구성 요소 및 클라이언트 라이브러리를 편집하는 매끄러운 워크플로우를 제공하고 코드 편집기 내에서 Photoshop 파일 및 레이어에 액세스할 수 있는 [Brackets](https://brackets.io/) 코드 편집기의 강력한 기능을 활용합니다. 익스텐션에서 제공되는 간편한 동기화(Maven 또는 File Vault 필요 없음)는 개발자의 효율성을 높여주며, AEM에 대한 지식이 제한된 프런트 엔드 개발자도 프로젝트에 참여할 수 있도록 도와줍니다. 또한 이 익스텐션은 구성 요소 개발을 더 쉽고 안전하게 하기 위해 JSP의 복잡성을 없애고 HTL(HTML Template Language)[에 대한 일부 지원을 제공합니다.](https://docs.adobe.com/content/help/ko-KR/experience-manager-htl/using/overview.html)

![chlimage_1-53](assets/chlimage_1-53a.png)

### 기능 {#features}

AEM Brackets Extension의 주요 기능은 다음과 같습니다.

* 변경된 파일을 AEM 개발 인스턴스로 자동으로 동기화할 수 있습니다.
* 파일과 폴더의 수동 양방향 동기화
* 프로젝트의 전체 컨텐츠 패키지 동기화.
* 표현식 및 `data-sly-*` 블록 문에 대한 HTL 코드 완성

또한 Brackets에는 AEM 글꼴 엔드 개발자에게 유용한 다양한 기능이 포함되어 있습니다.

* 레이어, 측정, 색상, 글꼴, 텍스트 등과 같은 PSD 파일에서 정보를 추출하는 Photoshop 파일 지원
* PSD의 코드 힌트 기능을 사용하여 코드에 추출된 정보를 손쉽게 재사용할 수 있습니다.
* LESS 및 SCSS와 같은 CSS 프리프로세서 지원
* 또한 보다 구체적인 요구 사항을 충족하는 수백 개의 익스텐션을 추가할 수 있습니다.

## 설치 {#installation}

### Brackets {#brackets}

AEM Brackets Extension은 Brackets 버전 1.0 이상을 지원합니다.

[brackets.io](https://brackets.io/)에서 최신 Brackets 버전을 다운로드합니다.

### 확장 {#the-extension}

확장 프로그램을 설치하려면 다음과 같이 하십시오.

1. 대괄호를 엽니다. **파일** 메뉴에서 **Extension Manager...**
1. 검색 표시줄에 **AEM**&#x200B;을 입력하고 **AEM Brackets 확장**&#x200B;을 찾습니다.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. **설치**&#x200B;를 클릭합니다.
1. 설치가 완료된 후 대화 상자와 Extension Manager을 닫습니다.

## 시작하기 {#getting-started}

### Content-Package 프로젝트 {#the-content-package-project}

확장자가 설치된 후 Brackets로 파일 시스템에서 content-package 폴더를 열어 AEM 구성 요소 개발을 시작할 수 있습니다.

프로젝트에 적어도 다음이 포함되어야 합니다.

1. `jcr_root` 폴더(예:`myproject/jcr_root`)

1. `filter.xml` 파일(예:`myproject/META-INF/vault/filter.xml`);`filter.xml` 파일 구조에 대한 자세한 내용은 [작업 공간 필터 정의](https://jackrabbit.apache.org/filevault/filter.html)를 참조하십시오.

Brackets&#39; **파일** 메뉴에서 **폴더 열기...**&#x200B;를 선택하고 `jcr_root` 폴더 또는 상위 프로젝트 폴더를 선택합니다.

>[!NOTE]
>
>컨텐츠 패키지가 있는 프로젝트가 없는 경우 [HTL TodoMVC 예제](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc)를 사용해 볼 수 있습니다. GitHub에서 **ZIP 다운로드**&#x200B;를 클릭하고 로컬에서 파일을 추출합니다. 위의 지시에 따라 대괄호로 `jcr_root` 폴더를 엽니다. 그런 다음 아래 절차에 따라 **프로젝트 설정**&#x200B;을 설정하고, 전체 컨텐츠-패키지 동기화 섹션에 자세히 설명된 대로 **콘텐츠 패키지 내보내기**&#x200B;를 수행하여 전체 패키지를 AEM 개발 인스턴스에 업로드합니다.
>
>이러한 단계 후에 AEM 개발 인스턴스에서 `/content/todo.html` URL에 액세스할 수 있어야 하며 Brackets에서 코드 수정을 시작하고 웹 브라우저에서 새로 고친 후 변경 내용이 AEM 서버에 즉시 동기화되는 방법을 확인할 수 있습니다.

### 프로젝트 설정 {#project-settings}

AEM 개발 인스턴스와 컨텐츠를 동기화하려면 프로젝트 설정을 정의해야 합니다. 이 작업은 **AEM** 메뉴로 이동하고 **프로젝트 설정..**

![chlimage_1-55](assets/chlimage_1-55a.png)

프로젝트 설정을 사용하면 다음을 정의할 수 있습니다.

1. 서버 URL(예:`http://localhost:4502`)
1. 유효한 HTTPS 인증서가 없는 서버를 허용할지 여부(필요하지 않은 경우 선택 취소)
1. 컨텐츠를 동기화하는 데 사용되는 사용자 이름(예:`admin`)
1. 사용자의 암호(예:`admin`)

## 콘텐트 동기화 중 {#synchronizing-content}

AEM Brackets Extension은 `filter.xml`에 정의된 필터링 규칙에서 허용하는 파일 및 폴더에 대해 다음과 같은 유형의 컨텐츠 동기화를 제공합니다.

### 변경된 파일의 자동 동기화 {#automated-synchronization-of-changed-files}

이렇게 하면 Brackets의 변경 사항만 AEM 인스턴스로 동기화되지만 다른 방법은 동기화되지 않습니다.

### 수동 양방향 동기화 {#manual-bidirectional-synchronization}

프로젝트 탐색기에서 파일 또는 폴더를 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴를 열고 **서버로 내보내기** 또는 **서버에서 가져오기** 옵션에 액세스할 수 있습니다.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>선택한 항목이 `jcr_root` 폴더 외부에 있으면 **서버로 내보내기** 및 **서버에서 가져오기** 컨텍스트 메뉴 항목이 비활성화됩니다.

### 전체 컨텐츠 패키지 동기화 {#full-content-package-synchronization}

**AEM** 메뉴에서 **콘텐츠 패키지 내보내기** 또는 **콘텐츠 패키지 가져오기** 옵션을 사용하면 전체 프로젝트를 서버와 동기화할 수 있습니다.

![chlimage_1-57](assets/chlimage_1-57a.png)

### 동기화 상태 {#synchronization-status}

AEM Brackets Extension은 마지막 동기화 상태를 나타내는 Brackets 창 오른쪽의 도구 모음에 알림 아이콘을 제공합니다.

* 녹색 - 모든 파일이 성공적으로 동기화되었습니다.
* blue - 동기화 작업이 진행 중입니다.
* 노란색 - 일부 파일이 동기화되지 않았습니다.
* red - 파일 중 동기화되지 않은 파일

알림 아이콘을 클릭하면 동기화된 각 파일의 모든 상태가 나열된 동기화 상태 보고서 대화 상자가 열립니다.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>사용된 동기화 방법에 상관없이 `filter.xml`의 필터링 규칙에 의해 포함됨으로 표시된 컨텐츠만 동기화됩니다.
>
>또한 `.vltignore` 파일은 저장소에서 컨텐츠를 동기화하거나 동기화하지 않고 저장소에서 컨텐츠를 제외하는 데 지원됩니다.

## HTL 코드 편집 {#editing-htl-code}

AEM Brackets Extension에는 HTL 특성 및 표현식 작성을 용이하게 하는 자동 완성 기능도 포함되어 있습니다.

### 속성 자동 완성 {#attribute-auto-completion}

1. HTML 특성에 `sly`을 입력합니다. 특성이 `data-sly-`에 자동으로 완성됩니다.
1. 드롭다운 목록에서 HTL 속성을 선택합니다.

### 표현식 자동 완성 {#expression-auto-completion}

표현식 `${}` 내에서 일반적인 변수 이름은 자동으로 완료됩니다.

## 추가 정보 {#more-information}

AEM Brackets Extension은 Apache License 버전 2.0의 [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) 조직이 GitHub에서 호스팅하는 오픈 소스 프로젝트입니다.

* 코드 저장소:[https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache License, 버전 2.0:[https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets 코드 편집기는 또한 [Adobe Systems Incorporated](https://github.com/adobe) 조직이 GitHub에서 호스팅하는 오픈 소스 프로젝트입니다.

* 코드 저장소:[https://github.com/adobe/brackets](https://github.com/adobe/brackets)

마음껏 기부하세요!
