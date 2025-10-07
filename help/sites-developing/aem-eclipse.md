---
title: Eclipse용 AEM 개발자 도구
description: Adobe Experience Manager의 Eclipse 개발자 도구에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 5bd621b14e3bcd21431c1df5629fe4669b14052c
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 2%

---


# Eclipse용 AEM 개발자 도구 {#aem-developer-tools-for-eclipse}

![Eclipse용 Experience Manager 개발자 도구 로고](assets/eclipse-logo.png)

## 개요 {#overview}

_Eclipse용 Experience Manager 개발자 도구_&#x200B;는 Apache 라이선스 2에 따라 릴리스된 [Apache Sling용 Eclipse 플러그인](https://sling.apache.org/documentation/development/ide-tooling.html)을 기반으로 하는 Eclipse 플러그인입니다.

AEM 개발을 보다 쉽게 만드는 몇 가지 기능을 제공합니다.

* Eclipse Server Connector를 통해 AEM 인스턴스와 원활하게 통합
* 콘텐츠 및 OSGi 번들 모두에 대한 동기화
* 코드 핫 스왑 기능으로 디버깅 지원
* 특정 프로젝트 만들기 마법사를 통한 AEM 프로젝트의 간단한 Bootstrap
* JCR 속성의 간편한 편집

## 요구 사항 {#requirements}

AEM 개발자 도구를 사용하기 전에 다음을 수행해야 합니다.

* Enterprise Java 및 웹 개발자용 [Eclipse IDE를 다운로드하여 설치합니다.](https://www.eclipse.org/downloads/packages/)
   * AEM Developer Tools for Eclipse 버전 1.4.0은 Eclipse 2022-12(4.26) 이상과 호환되며, 실행하려면 Java 17 이상이 필요합니다.
* `eclipse.ini`Eclipse FAQ[에 설명된 대로 &#x200B;](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F) 구성 파일을 편집하여 1GB 이상의 힙 메모리가 있는지 확인하도록 Eclipse 설치를 구성합니다.

>[!NOTE]
>
>macOS에서 **Eclipse.app**&#x200B;을(를) 마우스 오른쪽 단추로 클릭한 다음 **패키지 내용 표시**&#x200B;를 선택하여 `eclipse.ini`을(를) 찾아야 합니다.

## Eclipse용 AEM 개발자 도구를 설치하는 방법 {#how-to-install-the-aem-developer-tools-for-eclipse}

위의 [요구 사항](#requirements)을 충족하면 다음과 같이 개발자 도구 플러그인을 설치할 수 있습니다.

1. [AEM 개발자 도구 웹 사이트를 엽니다.](https://eclipse.adobe.com/)

1. **설치 링크**&#x200B;를 복사합니다.

   * 또는 설치 링크를 사용하는 대신 아카이브를 다운로드할 수 있습니다.
   * 이 방법을 사용하면 오프라인 설치가 허용되지만 자동 업데이트 알림은 수신되지 않습니다.

1. Eclipse에서 **도움말** 메뉴를 엽니다.
1. **새 소프트웨어 설치**&#x200B;를 클릭합니다.
1. **추가...**&#x200B;를 클릭합니다.
1. **이름** 필드에 `AEM Developer Tools`을(를) 입력하십시오.
1. **위치** 필드에서 설치 URL을 복사합니다.
1. **추가**&#x200B;를 클릭합니다.
1. **AEM** 및 **Sling** 플러그인을 모두 확인하세요.
1. **다음**&#x200B;을 클릭합니다.
1. **설치 세부 정보** 창에서 설치할 항목을 검토하고 **다음**&#x200B;을 다시 클릭합니다.
1. 사용권 계약에 동의하고 **마침**&#x200B;을 클릭합니다.
1. 표시되는 **신뢰 기관** 대화 상자에서 기관/사이트 `https://eclipse.adobe.com`을(를) 선택하고 **선택한 신뢰**&#x200B;를 클릭합니다.
1. 표시되는 **아티팩트 신뢰** 대화 상자에서 코드 서명자를 선택하고 **선택한 신뢰**&#x200B;를 클릭합니다.
1. Eclipse를 다시 시작하려면 **RestartNow**&#x200B;를 클릭하십시오.

## AEM 관점 {#the-aem-perspective}

Eclipse에서 **관점**&#x200B;은(는) 창 내에서 사용할 수 있는 작업 및 보기를 결정하고 Eclipse의 리소스와 작업 중심의 상호 작용을 가능하게 합니다. 관점에 대한 자세한 내용은 [Eclipse 설명서](https://help.eclipse.org/latest/index.jsp)를 참조하십시오.

_Eclipse용 Experience Manager 개발 도구_&#x200B;는 AEM 프로젝트 및 인스턴스를 완벽하게 제어할 수 있는 AEM 관점을 제공합니다. AEM 관점을 열려면:

1. Eclipse 메뉴 모음에서 **창** > **관점** > **관점 열기** > **기타**&#x200B;를 선택합니다.
1. 대화 상자에서 **AEM**&#x200B;을 선택하고 **열기**&#x200B;를 클릭합니다.

![Eclipse의 AEM 관점](assets/eclipse-aem-perspective.png)

## 샘플 다중 모듈 프로젝트 {#sample-multi-module-project}

_Eclipse용 Experience Manager 개발자 도구_&#x200B;에는 Eclipse의 프로젝트 설정을 빠르게 시작하는 데 도움이 되는 샘플 다중 모듈 프로젝트가 포함되어 있습니다. 또한 [AEM Project Archetype.](https://github.com/adobe/aem-project-archetype)을(를) 활용하여 여러 AEM 기능에 대한 모범 사례 가이드 역할을 합니다.

다음 단계에 따라 샘플 프로젝트를 만듭니다.

1. **파일** > **새로 만들기** > **프로젝트** 메뉴에서 **AEM** 섹션으로 이동하여 **AEM 샘플 다중 모듈 프로젝트**&#x200B;를 선택합니다.

   ![AEM 샘플 다중 모듈 프로젝트](assets/aem-sample-project.png)

1. **다음**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >[m2eclipse](https://eclipse.dev/m2e/)에서 Archetype 카탈로그를 스캔해야 하므로 이 단계는 잠시 걸릴 수 있습니다.

1. `com.adobe.aem : aem-project-archetype : <highest-number>`Archetype **드롭다운에서**&#x200B;을(를) 자동으로 선택해야 합니다. 원하는 경우 이전 버전을 선택합니다. **다음**&#x200B;을 클릭합니다.

   ![Archetype 버전 선택](assets/select-archetype.png)

1. 샘플 프로젝트에 대해 다음 필드를 제공합니다.

   * **이름**
   * **그룹 ID**
   * **아티팩트 Id**
   * **appId** - 이 값을 설정하려면 **고급** 옵션을 확장해야 할 수 있습니다.
   * **appTitle** - 이 값을 설정하려면 **고급** 옵션을 확장해야 할 수 있습니다.
   * **패키지** - 이 값을 설정하려면 **고급** 옵션을 확장해야 할 수 있습니다.

   ![Archetype 속성 정의](assets/archetype-properties.png)

1. **다음**&#x200B;을 클릭합니다.

1. **새 서버 설정**&#x200B;을 선택하고 서버 이름과 필요한 연결 세부 정보를 제공하여 Eclipse가 연결할 AEM 서버를 구성합니다.

   ![AEM 서버에 연결](assets/connect-server.png)

   * 디버거 기능을 사용하려면 `-agentlib` 매개 변수를 제공하여 디버그 모드에서 AEM을 시작해야 합니다. 예:

   ```text
   $ java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar aem-author-p4502.jar
   ```

   >[!TIP]
   >
   >로컬 AEM SDK에서 실행 중인 프로젝트를 디버깅하는 방법에 대한 자세한 내용은 문서 [AEM SDK 원격 디버깅](https://experienceleague.adobe.com/ko/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-sdk/remote-debugging)을 참조하십시오.

1. **마침**&#x200B;을 클릭합니다.

프로젝트 구조가 생성됩니다. 프로젝트에 필요한 아티팩트를 다운로드하는 데 잠시 시간이 걸릴 수 있습니다.

>[!NOTE]
>
>새로 설치할 때 또는 Maven 종속 항목을 이전에 다운로드하지 않은 경우 Eclipse에서 프로젝트가 오류와 함께 생성되었다고 보고할 수 있습니다. 이 경우 [잘못된 프로젝트 정의 해결](#resolving-invalid-project-definition) 섹션에 설명된 절차를 따르십시오.

## 기존 프로젝트를 가져오는 방법 {#how-to-import-existing-projects}

**새 프로젝트** 기능을 사용하여 기본 프로젝트 구조를 만듭니다.

1. 지침을 따라 문제를 적절하게 분리하여 기본 프로젝트 구조를 만드는 [샘플 다중 모듈 프로젝트](#sample-multi-module-project)을(를) 만듭니다.

   * `PROJECT.ui.apps` 및 `/apps` 콘텐츠에 대한 `/etc`
   * 작성된 `PROJECT.ui.content`에 대한 `/content`
   * Java 번들에 대한 `PROJECT.core`
   * 통합 테스트용 `PROJECT.it.launcher` 및 `PROJECT.it.tests`

1. `PROJECT.ui.apps` 프로젝트의 콘텐츠를 패키지의 `apps` 및 `etc` 폴더로 바꿉니다.

   1. **프로젝트 탐색기** 패널에서 `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`을(를) 확장합니다.
   1. `apps` 폴더를 마우스 오른쪽 단추로 클릭하고 **다음에서 표시** > **시스템 탐색기**&#x200B;를 선택합니다.
   1. `apps` 및 `etc` 폴더를 삭제하십시오.
   1. 동일한 위치에 콘텐츠 패키지의 `apps` 및 `etc` 폴더를 배치합니다.
   1. Eclipse에서 `PROJECT.ui.apps` 프로젝트를 마우스 오른쪽 단추로 클릭하고 **새로 고침**&#x200B;을 선택합니다.

1. 그런 다음 `PROJECT.ui.content`에 대해 동일한 작업을 수행하고 해당 콘텐츠 폴더를 패키지 중 하나로 바꿉니다.

   1. **프로젝트 탐색기** 패널에서 `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`을(를) 확장합니다.
   1. 더 깊은 콘텐츠 폴더를 마우스 오른쪽 단추로 클릭하고 **다음에서 표시** > **시스템 탐색기**&#x200B;를 선택합니다.
   1. 콘텐츠 폴더를 삭제합니다.
   1. 동일한 위치에 콘텐츠 패키지의 콘텐츠 폴더를 배치합니다.
   1. Eclipse에서 `PROJECT.ui.content` 프로젝트를 마우스 오른쪽 단추로 클릭하고 **새로 고침**&#x200B;을 선택합니다.

1. 콘텐츠 패키지의 `filter.xml` 파일을 별도의 텍스트/코드 편집기에서 열어 콘텐츠 패키지의 콘텐츠에 일치하도록 이 두 프로젝트의 `META-INF/vault/filter.xml` 파일을 업데이트합니다.

   * 다음은 `filter.xml` 파일이 표시되는 모습의 예입니다.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. 두 개의 프로젝트로 분할된 패키지의 컨텐츠에 대해서는 이러한 필터 규칙을 두 개로 분할하고 두 프로젝트의 `filter.xml` 파일도 그에 따라 업데이트해야 합니다.

   1. Eclipse에서 `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`을 엽니다.
   1. `<workspaceFilter>` 요소의 콘텐츠를 `/apps` 및 `/etc`(으)로 시작하는 패키지의 규칙으로 바꿉니다.
      * 예:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. `PROJECT.ui.content/src/main/content/META-INF/filter.xml`을(를) 엽니다.
   1. 규칙을 `/content`(으)로 시작하는 패키지로 바꾸십시오.
      * 예:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. 모든 변경 사항을 저장해야 합니다. 이제 새로운 콘텐츠를 AEM 인스턴스와 동기화할 수 있습니다.

1. **서버** 패널에서 연결이 시작되었는지 확인하고, 시작해서는 안 됩니다.

1. **정리 및 게시** 아이콘을 클릭합니다.

완료되면 인스턴스에서 패키지를 실행해야 합니다. 저장 시 모든 변경 사항이 자동으로 인스턴스에 동기화됩니다.

프로젝트에서 패키지를 다시 빌드하려면 `PROJECT.ui.apps` 또는 `PROJECT.ui.content`을(를) 마우스 오른쪽 단추로 클릭하고 **다음 계정으로 실행** > **Maven 설치**&#x200B;를 선택합니다.

이제 패키지 내부에 대상 폴더를 만들었습니다(예: `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## 문제 해결 {#troubleshooting}

### 잘못된 프로젝트 정의 해결 중 {#resolving-invalid-project-definition}

잘못된 종속성 및 프로젝트 정의를 해결하려면 다음과 같이 진행합니다.

1. 생성된 모든 프로젝트를 선택합니다.
1. 마우스 오른쪽 버튼을 클릭합니다.
1. 컨텍스트 메뉴에서 **Maven** > **프로젝트 업데이트**&#x200B;를 선택합니다.
1. **스냅숏/릴리스의 강제 업데이트**&#x200B;를 확인하세요.
1. **확인**&#x200B;을 클릭합니다.

Eclipse는 필요한 종속성을 다운로드합니다. 잠시 기다려 주십시오.

## 추가 정보 {#more-information}

Eclipse용 공식 Apache Sling IDE 툴링 웹 사이트는 유용한 추가 정보를 제공합니다.

* [**Eclipse용 Apache Sling IDE 도구** 사용 안내서](https://sling.apache.org/documentation/development/ide-tooling.html)는 AEM 개발 도구에서 지원하는 전체 개념, 서버 통합 및 배포 기능을 안내합니다.
* [Apache Sling IDE 도구 문제 해결](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [알려진 문제 목록](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

다음의 공식 [Eclipse](https://www.eclipse.org/) 설명서는 환경을 설정하는 데 도움이 될 수 있습니다.

* [Eclipse 시작](https://eclipseide.org/getting-started/)
* [Eclipse Luna 도움말 시스템](https://help.eclipse.org/latest/index.jsp)
* [Maven 통합(m2eclipse)](https://www.eclipse.org/m2e/)
