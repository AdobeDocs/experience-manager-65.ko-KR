---
title: AEM 개발 - 지침 및 우수 사례
seo-title: AEM 개발 - 지침 및 우수 사례
description: AEM에서 개발하기 위한 지침 및 우수 사례
seo-description: AEM에서 개발하기 위한 지침 및 우수 사례
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM 개발 - 지침 및 우수 사례{#aem-development-guidelines-and-best-practices}

## 템플릿 및 구성 요소 사용 지침 {#guidelines-for-using-templates-and-components}

AEM 구성 요소 및 템플릿은 매우 강력한 툴킷입니다. 개발자는 웹 사이트 비즈니스 사용자, 편집자 및 관리자에게 웹 사이트를 제공함으로써 변화하는 비즈니스 요구 사항(컨텐츠 민첩성)에 맞게 웹 사이트를 조정할 수 있는 기능을 제공하고 사이트(브랜드 보호)의 균일한 레이아웃을 유지할 수 있습니다.

웹 사이트 또는 웹 사이트(예: 글로벌 기업의 지사)를 담당하는 사람의 일반적인 과제는 웹 사이트에 새로운 유형의 컨텐츠 프레젠테이션을 도입하는 것입니다.

이미 게시된 다른 아티클의 추출을 나열하는 뉴스 목록 페이지를 웹 사이트에 추가해야 한다고 가정합니다. 페이지의 디자인 및 구조는 나머지 웹 사이트와 동일해야 합니다.

이러한 문제를 해결하는 권장 방법은 다음과 같습니다.

* 기존 템플릿을 재사용하여 새로운 유형의 페이지를 만듭니다. 템플릿은 페이지 구조(탐색 요소, 패널 등)를 대략적으로 정의하며, 디자인(CSS, 그래픽)에 따라 세부적으로 조정됩니다.
* 새 페이지에서 단락 시스템(parsys/iparsys)을 사용합니다.
* 단락 시스템의 디자인 모드에 대한 액세스 권한을 정의하여 권한이 있는 사람(일반적으로 관리자)만 변경할 수 있습니다.
* 편집자가 페이지에 필요한 구성 요소를 배치할 수 있도록 해당 단락 시스템에서 허용되는 구성 요소를 정의합니다. In our case it could be a list component, can traveling a subtree of pages and extract the information according to predefined rules.
* 편집자는 자신이 담당하는 페이지에 허용된 구성 요소를 추가하여 요청된 기능(정보)을 비즈니스에 전달합니다.

이 방법을 통해 웹 사이트의 기여 사용자 및 관리자가 개발 팀의 개입 없이도 비즈니스 요구 사항에 신속하게 대응할 수 있는 방법을 살펴볼 수 있습니다. 새 템플릿을 만드는 것과 같은 대체 방법은 일반적으로 비용이 많이 드는 작업이므로 변경 관리 프로세스와 개발 팀의 참여가 필요합니다. 이로 인해 전체 프로세스가 더 길어지고 비용이 많이 듭니다.

따라서 AEM 기반 시스템 개발자는 다음을 사용해야 합니다.

* 통일성과 브랜드 보호를 위한 단락 시스템 디자인의 템플릿과 액세스 제어
* 단락 시스템(유연한 구성 옵션 포함)

개발자를 위한 다음과 같은 일반적인 규칙은 대부분의 일반적인 프로젝트에서 의미가 있습니다.

* 템플릿 수를 웹 사이트에서 기본적으로 서로 다른 페이지 구조의 수만큼 낮게 유지합니다.
* 사용자 지정 구성 요소에 필요한 유연성과 구성 기능을 제공합니다.
* parsys 및 iparsys 구성 요소인 AEM 단락 시스템의 기능과 유연성을 극대화할 수 있습니다.

### 구성 요소 및 기타 요소 사용자 정의 {#customizing-components-and-other-elements}

고유한 구성 요소를 만들거나 기존 구성 요소를 사용자 정의할 때는 기존 정의를 다시 사용하는 것이 가장 쉽고 안전합니다. 동일한 원칙이 AEM 내의 다른 요소(예: 오류 처리기)에도 적용됩니다.

이 작업은 기존 정의를 복사하고 오버레이하여 수행할 수 있습니다. 즉, 정의를 에서 `/libs` 로 `/apps/<your-project>`복사합니다. 이 새로운 정의는, in, `/apps`your requirements에 따라 업데이트할 수 있습니다.

>[!NOTE]
>
>자세한 [내용은 오버레이](/help/sites-developing/overlays.md) 사용을 참조하십시오.

예:

* [구성 요소 사용자 정의](/help/sites-developing/components.md)

   이 문제는 구성 요소 정의를 오버레이하는 것과 관련이 있습니다.

   * 기존 구성 요소를 복사하여 에서 새 구성 요소 폴더를 `/apps/<website-name>/components/<MyComponent>` 만듭니다.

      * 예를 들어 텍스트 구성 요소 복사본을 사용자 정의하려면 다음을 수행합니다.

         * 시작 시간:`/libs/foundation/components/text`
         * 끝 `/apps/myProject/components/text`

* [오류 처리기에 표시되는 페이지 사용자 지정](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   이 사례에는 서블릿 오버레이가 포함됩니다.

   * 저장소에서 기본 스크립트를 복사합니다.

      * 시작 시간:`/libs/sling/servlet/errorhandler/`
      * 끝 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>패스에 있는 **어떤 것도 변경할 수** 없습니다 `/libs` .
>
>이는 다음에 인스턴스를 업그레이드할 때 의 컨텐츠를 `/libs` 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).
>
>구성 및 기타 변경 사항은 다음과 같습니다.
>
>1. 항목을 `/libs``/apps`
>1. 변경 `/apps`


## JCR 쿼리를 사용할 때와 사용하지 않을 때 {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR 쿼리는 올바르게 사용될 때 강력한 도구입니다. 이러한 요구 사항은 다음과 같습니다.

* 컨텐츠에 대한 전체 텍스트 검색과 같은 실제 최종 사용자 쿼리
* 구조화된 컨텐츠를 전체 저장소에서 찾아야 하는 경우입니다.

   이러한 경우 쿼리가 절대적으로 필요할 때만 실행되어야 합니다(예: 워크플로우 단계, 컨텐츠 수정, 필터 등에 대해 트리거되는 이벤트 핸들러 등).

JCR 쿼리는 순수한 렌더링 요청에 사용해서는 안 됩니다. 예를 들어 JCR 쿼리는

* 렌더링 탐색
* &quot;상위 10개의 최신 뉴스 항목&quot; 개요 만들기
* 콘텐트 항목 수 표시

컨텐츠를 렌더링하는 경우 JCR 쿼리를 수행하는 대신 컨텐츠 트리에 대한 탐색 액세스를 사용하십시오.

>[!NOTE]
>
>쿼리 빌더를 사용하는 [경우](/help/sites-developing/querybuilder-api.md)쿼리 빌더가 백그라운드에서 JCR 쿼리를 생성하기 때문에 JCR 쿼리를 사용합니다.


## 보안 고려 사항 {#security-considerations}

>[!NOTE]
>
>또한 [보안 체크리스트를](/help/sites-administering/security-checklist.md)참조할 수 있습니다.

### JCR(저장소) 세션 {#jcr-repository-sessions}

관리 세션이 아닌 사용자 세션을 사용해야 합니다. 즉, 다음을 사용해야 합니다.

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### XSS(교차 사이트 스크립팅)로부터 보호 {#protect-against-cross-site-scripting-xss}

XSS(교차 사이트 스크립팅)를 통해 공격자는 다른 사용자가 보는 웹 페이지에 코드를 삽입할 수 있습니다. 이 보안 취약점은 악의적인 웹 사용자가 액세스 제어를 우회하도록 악용될 수 있습니다.

AEM 파섹 XSS 방지는 개발 및 테스트 중 가장 높은 우선순위가 주어집니다.

또한 Apache용 [mod_security와 같은](https://modsecurity.org)웹 애플리케이션 방화벽은 배포 환경의 보안을 중앙에서 안전하게 제어하고 이전에 감지되지 않은 크로스 사이트 스크립팅 공격으로부터 보호할 수 있습니다.

>[!CAUTION]
>
>AEM과 함께 제공된 예제 코드는 이러한 공격으로부터 자체적으로 보호되지 않을 수 있으며 일반적으로 웹 애플리케이션 방화벽에 의한 요청 필터링에 의존합니다.

XSS API 요약서에는 XSS API를 사용하고 AEM 앱을 보다 안전하게 만들기 위해 알아야 하는 정보가 포함되어 있습니다. 여기에서 다운로드할 수 있습니다.

XSSAPI 요약서

[파일 가져오기](assets/xss_cheat_sheet_2016.pdf)

### 기밀 정보를 위한 커뮤니케이션 보안 {#securing-communication-for-confidential-information}

모든 인터넷 응용 프로그램에 대해 기밀 정보를 전송할 때는

* 트래픽은 SSL을 통해 보호됩니다.
* HTTP POST는 해당되는 경우 사용됩니다.

이는 구성 또는 관리 액세스와 같이 시스템에 기밀이 되는 정보와 사용자의 개인 정보(예: 개인 정보)에 적용됩니다.

## 개별 개발 작업 {#distinct-development-tasks}

### 오류 페이지 사용자 지정 {#customizing-error-pages}

AEM에 대해 오류 페이지를 사용자 지정할 수 있습니다. 인스턴스가 내부 서버 오류에 대한 슬링 추적을 표시하지 않도록 하는 것이 좋습니다.

자세한 [내용은 오류 처리기에서 표시되는 오류 페이지 사용자](/help/sites-developing/customizing-errorhandler-pages.md) 지정을 참조하십시오.

### Java 프로세스에서 파일 열기 {#open-files-in-the-java-process}

AEM은 많은 수의 파일에 액세스할 수 있으므로 Java 프로세스에 [](/help/sites-deploying/configuring.md#open-files-in-the-java-process) 대해 열려 있는 파일 수를 AEM에 대해 명시적으로 구성하는 것이 좋습니다.

이러한 문제를 최소화하려면 열려 있는 파일이 가능한 한 빨리 올바르게 닫혀 있어야 합니다.
