---
title: IntelliJ IDEA를 사용하여 AEM 프로젝트를 개발하는 방법
description: IntelliJ IDEA를 사용하여 Adobe Experience Manager 프로젝트를 개발하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 2%

---

# IntelliJ IDEA를 사용하여 AEM 프로젝트를 개발하는 방법{#how-to-develop-aem-projects-using-intellij-idea}

## 개요 {#overview}

IntelliJ에서 AEM 개발을 시작하려면 다음 단계가 필요합니다.

각 단계는 이 주제의 나머지 부분에서 더 자세히 설명합니다.

* IntelliJ 설치
* Maven을 기반으로 AEM 프로젝트 설정
* Maven POM에서 IntelliJ에 대한 JSP 지원 준비
* Maven 프로젝트를 IntelliJ로 가져오기

>[!NOTE]
>
>이 안내서는 IntelliJ IDEA Ultimate Edition 12.1.4 및 AEM 5.6.1을 기반으로 합니다.

### IntelliJ IDEA 설치 {#install-intellij-idea}

에서 IntelliJ IDEA 다운로드 [jetBrains의 다운로드 페이지](https://www.jetbrains.com/idea/download/).

그런 다음 해당 페이지의 설치 지침을 따릅니다.

### Maven을 기반으로 AEM 프로젝트 설정 {#set-up-your-aem-project-based-on-maven}

다음에에 설명된 대로 Maven을 사용하여 프로젝트를 설정합니다. [Apache Maven을 사용한 AEM 프로젝트 빌드 방법](/help/sites-developing/ht-projects-maven.md).

IntelliJ IDEA에서 AEM 프로젝트 작업을 시작하려면 [5분 후 시작](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) 충분합니다.

### IntelliJ IDEA에 대한 JSP 지원 준비 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA는 JSP 작업을 지원할 수도 있습니다. 예를 들면 다음과 같습니다.

* 태그 라이브러리 자동 완성
* 에 의해 정의된 오브젝트 인식 `<cq:defineObjects />` 및 `<sling:defineObjects />`

이를 위해 의 지침을 따르십시오. [JSP에서 사용 방법](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) 위치: [Apache Maven을 사용한 AEM 프로젝트 빌드 방법](/help/sites-developing/ht-projects-maven.md).

### Maven 프로젝트 가져오기 {#import-the-maven-project}

1. 를 엽니다. **가져오기** IntelliJ IDEA의 대화 상자

   * 선택 **프로젝트 가져오기** 아직 열려 있는 프로젝트가 없는 경우 시작 화면에서 다음을 수행하십시오
   * 선택 **파일 > 프로젝트 가져오기** 메인 메뉴에서

1. 가져오기 대화 상자에서 프로젝트의 POM 파일을 선택합니다.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 아래 대화 상자에 표시된 대로 기본 설정을 계속 진행합니다.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 다음을 클릭하여 다음 대화 상자를 계속 진행합니다. **다음** 및 **완료**.
1. 이제 IntelliJ IDEA를 사용하여 AEM 개발에 대해 설정되었습니다.

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### IntelliJ IDEA를 사용하여 JSP 디버깅 {#debugging-jsps-with-intellij-idea}

IntelliJ IDEA로 JSP를 디버깅하려면 다음 단계가 필요합니다

* 프로젝트에서 웹 Facet 설정
* JSR45 지원 플러그인 설치
* 디버그 프로필 구성
* 디버그 모드에 대한 AEM 구성

#### 프로젝트에서 웹 Facet 설정 {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA는 디버깅을 위해 JSP를 찾을 위치를 이해해야 합니다. IDEA는 `content-package-maven-plugin` 수동으로 구성해야 합니다.

1. 다음으로 이동 **파일 > 프로젝트 구조**
1. 다음 항목 선택 **콘텐츠** 모듈
1. 클릭 **+** 모듈 목록 위에 있는 을 선택합니다. **웹**
1. 웹 리소스 디렉토리로 `content/src/main/content/jcr_root subdirectory` 아래 스크린샷에 표시된 대로 프로젝트 내에서 작동합니다.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### JSR45 지원 플러그인 설치 {#install-the-jsr-support-plugin}

1. 로 이동 **플러그인** IntelliJ IDEA 설정의 창
1. 다음 위치로 이동 **JSR45 통합** 플러그인을 선택하고 옆에 있는 확인란을 선택합니다.
1. 클릭 **적용**
1. 요청하면 IntelliJ IDEA 다시 시작

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 디버그 프로필 구성 {#configure-a-debug-profile}

1. 다음으로 이동 **실행 > 구성 편집**
1. 다음을 누르세요. **+** 및 선택 **JSR45 원격**
1. 구성 대화 상자에서 **구성** 다음에 **응용 프로그램 서버** 일반 서버 구성
1. 디버깅을 시작할 때 브라우저를 열려면 시작 페이지를 적절한 URL로 설정하십시오
1. 모두 제거 **실행 전** vlt 자동 동기화를 사용하는 경우 작업을 수행하거나 그렇지 않은 경우 적절한 Maven 작업을 구성합니다.
1. 다음에서 **시작/연결** 필요한 경우 창에서 포트를 조정합니다.
1. IntelliJ IDEA에서 제안하는 명령줄 인수 복사

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 디버그 모드에 대한 AEM 구성 {#configure-aem-for-debug-mode}

필요한 마지막 단계는 IntelliJ IDEA에서 제안한 JVM 옵션으로 AEM을 시작하는 것입니다.

AEM jar 파일을 직접 시작하고 다음 명령줄을 사용하여 이러한 옵션을 추가합니다.

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

에서 시작 스크립트에 이러한 옵션을 추가할 수도 있습니다. `crx-quickstart/bin/start` 아래와 같이 표시됩니다.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 디버깅 시작 {#start-debugging}

이제 AEM에서 JSP를 디버깅하도록 모두 설정되었습니다.

1. 선택 **실행 > 디버그 > 디버그 프로필**
1. 구성 요소 코드에서 중단점 설정
1. 브라우저에서 페이지에 액세스

![chlimage_1-52](assets/chlimage_1-52a.png)

### IntelliJ IDEA를 사용하여 번들 디버깅 {#debugging-bundles-with-intellij-idea}

표준 일반 원격 디버그 연결을 사용하여 번들의 코드를 디버깅할 수 있습니다. 다음 단계를 따를 수 있습니다. [원격 디버깅에 대한 Jetbrain 설명서](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
