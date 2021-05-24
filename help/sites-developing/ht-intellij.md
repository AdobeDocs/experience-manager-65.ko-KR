---
title: IntelliJ IDEA를 사용하여 AEM 프로젝트를 개발하는 방법
seo-title: IntelliJ IDEA를 사용하여 AEM 프로젝트를 개발하는 방법
description: IntelliJ IDEA를 사용하여 AEM 프로젝트 개발
seo-description: IntelliJ IDEA를 사용하여 AEM 프로젝트 개발
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 4%

---

# IntelliJ IDEA를 사용하여 AEM 프로젝트를 개발하는 방법{#how-to-develop-aem-projects-using-intellij-idea}

## 개요 {#overview}

IntelliJ에서 AEM 개발을 시작하려면 다음 단계가 필요합니다.

각 설명은 이 방법 설명서의 나머지 부분에서 더 자세히 설명합니다.

* IntelliJ 설치
* Maven을 기반으로 AEM 프로젝트 설정
* Maven POM에서 IntelliJ에 대한 JSP 지원 준비
* Maven 프로젝트를 IntelliJ로 가져오기

>[!NOTE]
>
>이 안내서는 IntelliJ IDEA Ultimate Edition 12.1.4 및 AEM 5.6.1을 기반으로 합니다.

### IntelliJ IDEA {#install-intellij-idea} 설치

JetBrain](https://www.jetbrains.com/idea/download/index.html)의 다운로드 페이지에서 IntelliJ IDEA를 다운로드합니다.[

그런 다음 해당 페이지의 설치 지침을 따릅니다.

### Maven {#set-up-your-aem-project-based-on-maven}을 기반으로 AEM 프로젝트 설정

그런 다음 Apache Maven](/help/sites-developing/ht-projects-maven.md)을 사용하여 AEM 프로젝트를 작성하는 방법[에 설명된 대로 Maven을 사용하여 프로젝트를 설정하십시오.

IntelliJ IDEA에서 AEM 프로젝트 작업을 시작하려면 [5분 후에 시작하기](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)의 기본 설정이 충분합니다.

### IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}에 대한 JSP 지원 준비

IntelliJ IDEA는 JSP 작업(예:

* 태그 라이브러리 자동 완성
* `<cq:defineObjects />` 및 `<sling:defineObjects />`에 의해 정의된 개체 인식

이를 수행하려면 [Apache Maven](/help/sites-developing/ht-projects-maven.md)을 사용하여 AEM 프로젝트를 작성하는 방법[JSP에서 작업하는 방법](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)의 지침을 따르십시오.

### Maven 프로젝트 가져오기 {#import-the-maven-project}

1. IntelliJ IDEA에서 **가져오기** 대화 상자를 엽니다.

   * 아직 열려 있는 프로젝트가 없는 경우 시작 화면에서 **프로젝트 가져오기** 선택
   * 기본 메뉴에서 **파일 -> 프로젝트 가져오기** 선택

1. 가져오기 대화 상자에서 프로젝트의 POM 파일을 선택합니다.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 아래 대화 상자에 표시된 대로 기본 설정을 계속 진행합니다.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. **다음** 및 **완료**&#x200B;를 클릭하여 다음 대화 상자를 계속 진행합니다.
1. 이제 IntelliJ IDEA를 사용하여 AEM 개발을 사용하도록 설정되었습니다

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### IntelliJ IDEA {#debugging-jsps-with-intellij-idea}로 JSP 디버깅

IntelliJ IDEA를 사용하여 JSP를 디버깅하는 데 다음 단계가 필요합니다

* 프로젝트에서 웹 패싯 설정
* JSR45 지원 플러그인 설치
* 디버그 프로필 구성
* 디버그 모드에 대한 AEM 구성

#### 프로젝트 {#set-up-a-web-facet-in-the-project}에서 웹 패싯 설정

IntelliJ IDEA는 디버깅할 JSP를 찾을 위치를 이해해야 합니다. IDEA가 `content-package-maven-plugin` 설정을 해석할 수 없으므로 수동으로 구성해야 합니다.

1. **파일 -> 프로젝트 구조**&#x200B;로 이동합니다.
1. **Content** 모듈을 선택합니다
1. 모듈 목록 위에 있는 **+** 를 클릭하고 **웹**&#x200B;을 선택합니다.
1. 웹 리소스 디렉터리로 아래 스크린샷에 표시된 대로 프로젝트의 `content/src/main/content/jcr_root subdirectory`을 선택합니다.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### JSR45 지원 플러그인 {#install-the-jsr-support-plugin} 설치

1. IntelliJ IDEA 설정의 **Plugins** 창으로 이동합니다
1. **JSR45 통합** 플러그인으로 이동하고 그 옆에 있는 확인란을 선택합니다
1. **적용** 클릭
1. 요청 시 IntelliJ IDEA를 다시 시작합니다.

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 디버그 프로필 구성 {#configure-a-debug-profile}

1. **실행 -> 구성 편집**&#x200B;으로 이동합니다.
1. **+**&#x200B;를 누르고 **JSR45 Remote**&#x200B;를 선택합니다.
1. 구성 대화 상자에서 **응용 프로그램 서버** 옆에 있는 **구성**&#x200B;을 선택하고 일반 서버를 구성합니다
1. 디버깅을 시작할 때 브라우저를 열려면 시작 페이지를 적절한 URL로 설정합니다
1. vlt autosync를 사용하는 경우 시작 전 **작업을 모두 제거하거나, 그렇지 않은 경우 적절한 Maven 작업을 구성하십시오**
1. **시작/연결** 창에서 필요한 경우 포트를 조정합니다
1. IntelliJ IDEA에서 제안하는 명령줄 인수를 복사합니다.

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 디버그 모드 {#configure-aem-for-debug-mode}에 대해 AEM 구성

IntelliJ IDEA에서 제안하는 JVM 옵션을 사용하여 AEM을 시작하는 것이 필요한 마지막 단계입니다.

이렇게 하려면 AEM jar 파일을 직접 시작하고 다음 명령줄을 사용하여 이러한 옵션을 추가하면 됩니다.

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart-5.6.1.jar`

아래 표시된 대로 `crx-quickstart/bin/start`에서 이러한 옵션을 시작 스크립트에 추가할 수도 있습니다.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 디버깅 시작 {#start-debugging}

이제 AEM에서 JSP를 디버깅하도록 설정되어 있습니다.

1. **실행 -> 디버그 -> 디버그 프로필을 선택합니다.**
1. 구성 요소 코드에서 중단점 설정
1. 브라우저에서 페이지에 액세스

![chlimage_1-52](assets/chlimage_1-52a.png)

### IntelliJ IDEA {#debugging-bundles-with-intellij-idea}를 사용하여 번들 디버깅

번들의 코드는 표준 일반 원격 디버그 연결을 사용하여 디버깅할 수 있습니다. 원격 디버깅](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html)에서 [Jetbrain 설명서를 따를 수 있습니다.
