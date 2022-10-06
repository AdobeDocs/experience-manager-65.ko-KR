---
title: AEM 개발 - 지침 및 우수 사례
seo-title: AEM Development - Guidelines and Best Practices
description: AEM 개발 지침 및 우수 사례
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 1%

---

# AEM 개발 - 지침 및 우수 사례{#aem-development-guidelines-and-best-practices}

## 템플릿 및 구성 요소 사용 지침 {#guidelines-for-using-templates-and-components}

AEM 구성 요소 및 템플릿은 매우 강력한 툴킷입니다. 개발자가 균일한 사이트 레이아웃(브랜드 보호)을 유지하면서 웹 사이트 비즈니스 사용자, 편집자 및 관리자에게 웹 사이트를 변화하는 비즈니스 요구(컨텐츠 민첩성)에 맞게 조정할 수 있는 기능을 제공하는 데 사용할 수 있습니다.

웹 사이트 또는 웹 사이트 세트(예: 글로벌 기업의 지사에서)를 담당하는 사람에게 일반적인 과제는 웹 사이트에 새로운 유형의 컨텐츠 프레젠테이션을 도입하는 것입니다.

이미 게시된 다른 문서의 추출물을 나열하는 웹 사이트에 뉴스 목록 페이지를 추가해야 한다고 가정합니다. 페이지의 디자인과 구조는 나머지 웹 사이트와 동일해야 합니다.

이러한 문제를 해결하는 데 권장되는 방법은 다음과 같습니다.

* 기존 템플릿을 재사용하여 새 유형의 페이지를 만듭니다. 템플릿은 페이지 구조(탐색 요소, 패널 등)를 대략적으로 정의하며, 해당 디자인(CSS, 그래픽)에 의해 추가로 세밀하게 조정됩니다.
* 새 페이지에서 단락 시스템(parsys/iparsys)을 사용합니다.
* 단락 시스템의 디자인 모드에 대한 액세스 권한을 정의하면 권한이 있는 사람(일반적으로 관리자)만 이 액세스 권한을 변경할 수 있습니다.
* 편집기에서 페이지에 필요한 구성 요소를 배치할 수 있도록 지정된 단락 시스템에서 허용되는 구성 요소를 정의합니다. 이 경우 목록 구성 요소일 수 있으며, 이 구성 요소는 페이지의 하위 트리를 트래버스하고 사전 정의된 규칙에 따라 정보를 추출할 수 있습니다.
* 편집자는 허용된 구성 요소를 담당 페이지에서 추가하여 구성하여 요청된 기능(정보)을 비즈니스에 전달합니다.

이러한 접근 방식을 통해 웹 사이트의 기여 사용자 및 관리자가 개발 팀에 관여하지 않고도 비즈니스 요구 사항에 신속하게 대응할 수 있는 방법을 보여줍니다. 새 템플릿을 만드는 것과 같은 다른 방법은 일반적으로 비용이 많이 드는 작업이므로 변경 관리 프로세스와 개발 팀의 참여가 필요합니다. 이렇게 하면 전체 프로세스가 보다 길고 비용이 많이 듭니다.

따라서 AEM 기반 시스템 개발자는 다음을 사용해야 합니다.

* 균일성 및 브랜드 보호를 위한 단락 시스템 디자인의 템플릿 및 액세스 제어
* 단락 시스템에는 유연성을 위한 구성 옵션이 포함되어 있습니다.

개발자를 위한 다음과 같은 일반적인 규칙은 대부분의 일반 프로젝트에서 적용됩니다.

* 템플릿 수를 웹 사이트에서 기본적으로 다른 페이지 구조의 수와 마찬가지로 낮게 유지합니다.
* 사용자 정의 구성 요소에 필요한 유연성과 구성 기능을 제공합니다.
* AEM 단락 시스템(parsys 및 iparsys 구성 요소)의 힘과 유연성을 극대화합니다.

### 구성 요소 및 기타 요소 사용자 지정 {#customizing-components-and-other-elements}

자체 구성 요소를 만들거나 기존 구성 요소를 사용자 지정할 때 기존 정의를 다시 사용하는 것이 가장 쉽고 안전합니다. 동일한 원칙은 AEM 내의 다른 요소(예: 오류 처리기)에도 적용됩니다.

기존 정의를 복사하고 오버레이하여 수행할 수 있습니다. 즉, 정의 복사 `/libs` to `/apps/<your-project>`. 이 새로운 정의인 `/apps`은 요구 사항에 따라 업데이트할 수 있습니다.

>[!NOTE]
>
>자세한 내용은 [오버레이 사용](/help/sites-developing/overlays.md) 자세한 내용

예:

* [구성 요소 사용자 지정](/help/sites-developing/components.md)

   구성 요소 정의를 오버레이하는 것과 관련되어 있습니다.

   * 에서 새 구성 요소 폴더를 만듭니다 `/apps/<website-name>/components/<MyComponent>` 기존 구성 요소를 복사하여

      * 예를 들어, 텍스트 구성 요소 복사본을 사용자 지정하는 방법은 다음과 같습니다.

         * 변환 전: `/libs/foundation/components/text`
         * 끝 `/apps/myProject/components/text`

* [오류 핸들러로 표시된 페이지 사용자 지정](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   이 경우 서블릿 오버레이가 포함됩니다.

   * 저장소에서 기본 스크립트를 복사합니다.

      * 변환 전: `/libs/sling/servlet/errorhandler/`
      * 끝 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>사용자 **필수가 아니어야 합니다.** 에서 변경 `/libs` 경로.
>
>왜냐하면 `/libs` 는 다음에 인스턴스를 업그레이드할 때 덮어쓰여지며, 핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있습니다.
>
>구성 및 기타 변경 사항에 대해서는
>
>1. 의 항목 복사 `/libs` to `/apps`
>1. 내에서 변경 `/apps`


## JCR 쿼리를 사용해야 하는 경우 및 사용하지 않아야 하는 경우 {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR 쿼리는 올바르게 사용할 때 강력한 도구입니다. 다음 경우에 적합합니다.

* 전체 텍스트 검색과 같이 컨텐츠에 대한 실제 최종 사용자 쿼리
* 구조화된 컨텐츠를 전체 저장소에서 찾아야 하는 경우가 있습니다.

   이러한 경우 쿼리가 절대적으로 필요한 경우에만 실행되는지 확인하십시오. 예를 들어, 구성 요소 활성화 또는 캐시 무효화(예: 컨텐츠 수정, 필터 등에 대해 트리거하는 워크플로우 단계, 이벤트 핸들러 등)가 아니라

JCR 쿼리는 순수 렌더링 요청에 사용해서는 안 됩니다. 예를 들어 JCR 쿼리는

* 렌더링 탐색
* 상위 10개의 최신 뉴스 항목 만들기 개요
* 콘텐츠 항목 수 표시

컨텐츠를 렌더링하려면 JCR 쿼리를 수행하지 않고 컨텐츠 트리에 대한 탐색 액세스를 사용합니다.

>[!NOTE]
>
>를 사용하는 경우 [Query Builder](/help/sites-developing/querybuilder-api.md)쿼리 빌더가 후드 아래에 JCR 쿼리를 생성하므로 JCR 쿼리를 사용합니다.

## 보안 고려 사항 {#security-considerations}

>[!NOTE]
>
>또한, [보안 검사 목록](/help/sites-administering/security-checklist.md).

### JCR(저장소) 세션 {#jcr-repository-sessions}

관리 세션이 아니라 사용자 세션을 사용해야 합니다. 즉, 다음을 사용해야 합니다.

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### XSS(교차 사이트 스크립팅)에 대한 Protect {#protect-against-cross-site-scripting-xss}

XSS(교차 사이트 스크립팅)를 사용하면 공격자가 다른 사용자가 보는 웹 페이지에 코드를 삽입할 수 있습니다. 이 보안 취약성은 악의적인 웹 사용자가 액세스 제어를 무시하기 위해 사용할 수 있습니다.

AEM은 사용자가 제공한 모든 컨텐츠를 출력 시 필터링하는 원칙을 적용합니다. XSS 방지는 개발 및 테스트 중에 가장 높은 우선 순위가 지정됩니다.

또한 다음과 같은 웹 애플리케이션 방화벽도 [Apache용 mod_security](https://modsecurity.org)를 사용하면 배포 환경의 보안을 중앙 집중식으로 안정적으로 제어할 수 있으며 이전에 감지되지 않은 교차 사이트 스크립팅 공격으로부터 보호할 수 있습니다.

>[!CAUTION]
>
>AEM과 함께 제공되는 예제 코드는 이러한 공격으로부터 자체 보호되지 않을 수 있으며 일반적으로 웹 애플리케이션 방화벽에 의한 요청 필터링에 의존합니다.

XSS API 치트 시트에는 XSS API를 사용하고 AEM 앱을 보다 안전하게 만들기 위해 알아야 하는 정보가 포함되어 있습니다. 여기에서 다운로드할 수 있습니다.

XSSAPI 치트 시트.

[파일 가져오기](assets/xss_cheat_sheet_2016.pdf)

### 기밀 정보를 위한 통신 보안 {#securing-communication-for-confidential-information}

모든 인터넷 응용 프로그램에 대해 기밀 정보를 전송할 때는 반드시

* 트래픽은 SSL을 통해 보안됩니다
* HTTP POST은 해당하는 경우 사용됩니다

이는 시스템에 기밀이 되는 정보(예: 구성 또는 관리 액세스)뿐만 아니라 사용자에게 기밀이 되는 정보(예: 개인 세부 정보)에도 적용됩니다

## 개별 개발 작업 {#distinct-development-tasks}

### 오류 페이지 사용자 지정 {#customizing-error-pages}

AEM에 대해 오류 페이지를 사용자 지정할 수 있습니다. 인스턴스가 내부 서버 오류에 대한 슬링 추적을 표시하지 않도록 하는 것이 좋습니다.

자세한 내용은 [오류 핸들러로 표시된 오류 페이지 사용자 지정](/help/sites-developing/customizing-errorhandler-pages.md) 자세한 내용

### Java 프로세스에서 파일 열기 {#open-files-in-the-java-process}

AEM은 많은 수의 파일에 액세스할 수 있으므로 [Java 프로세스에 대한 파일 열기](/help/sites-deploying/configuring.md#open-files-in-the-java-process) AEM에 대해 명시적으로 구성됩니다.

이 문제 개발을 최소화하려면 열려 있는 파일이 가능한 한 빨리(의미 있게) 올바르게 닫혀 있어야 합니다.
