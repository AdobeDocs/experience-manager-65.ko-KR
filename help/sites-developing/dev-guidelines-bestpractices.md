---
title: AEM 개발 - 지침 및 우수 사례
seo-title: AEM 개발 - 지침 및 우수 사례
description: AEM 개발 지침 및 모범 사례
seo-description: AEM 개발 지침 및 모범 사례
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 2%

---


# AEM 개발 - 지침 및 우수 사례{#aem-development-guidelines-and-best-practices}

## 템플릿 및 구성 요소 사용 지침 {#guidelines-for-using-templates-and-components}

AEM 구성 요소 및 템플릿은 매우 강력한 툴킷입니다. 개발자는 웹 사이트 비즈니스 사용자, 편집자 및 관리자에게 웹 사이트를 변화하는 비즈니스 요구 사항(컨텐츠 민첩성)에 맞게 조정하고 사이트의 동일한 레이아웃(브랜드 보호)을 유지하는 기능을 제공할 수 있습니다.

웹 사이트 또는 웹 사이트(예: 글로벌 기업의 지사)를 담당하는 사람의 일반적인 과제는 웹 사이트에 새로운 유형의 컨텐츠 프레젠테이션을 도입하는 것입니다.

이미 게시된 다른 아티클에서 추출되는 뉴스 목록 페이지를 웹 사이트에 추가해야 한다고 가정합니다. 페이지의 디자인과 구조는 다른 웹 사이트의 디자인과 동일해야 합니다.

이러한 문제를 해결하는 권장되는 방법은 다음과 같습니다.

* 기존 템플릿을 재사용하여 새로운 유형의 페이지를 만듭니다. 템플릿은 페이지 구조(탐색 요소, 패널 등)를 대략적으로 정의하며, 이 구조는 해당 디자인(CSS, 그래픽)에 의해 세밀하게 조정됩니다.
* 새 페이지에서 단락 시스템(parsys/iparsys)을 사용합니다.
* 권한이 있는 사람(일반적으로 관리자)만 단락 시스템의 디자인 모드에 대한 액세스 권한을 정의할 수 있습니다.
* 편집자가 페이지에 필요한 구성 요소를 배치할 수 있도록 해당 단락 시스템에서 허용되는 구성 요소를 정의합니다. In our case it could be a list component, can traveling a subtree of pages and extract the information according to predefined rules.
* 편집자는 자신이 담당하는 페이지에 허용된 구성 요소를 추가하여 요청된 기능(정보)을 비즈니스에 전달합니다.

이 접근 방식을 통해 웹 사이트의 기여 사용자 및 관리자가 개발 팀의 참여 없이 비즈니스 요구 사항에 신속하게 응답할 수 있는 방법을 설명합니다. 새 템플릿을 만드는 것과 같은 대체 방법은 일반적으로 비용이 많이 드는 작업이므로 변경 관리 프로세스와 개발 팀의 참여가 필요합니다. 따라서 전체 프로세스가 보다 길어지고 비용이 많이 소요됩니다.

따라서 AEM 기반 시스템의 개발자는 다음을 사용해야 합니다.

* 균일성과 브랜드 보호를 위한 단락 시스템 디자인의 템플릿과 액세스 제어
* 단락 시스템(유연성을 위한 구성 옵션 포함)

개발자를 위한 다음과 같은 일반 규칙은 대부분의 일반적인 프로젝트에서 유용합니다.

* 웹 사이트에서 기본적으로 서로 다른 페이지 구조의 수와 마찬가지로 템플릿 수를 낮게 유지합니다.
* 사용자 지정 구성 요소에 필요한 유연성과 구성 기능을 제공합니다.
* AEM 단락 시스템인 parsys 및 iparsys 구성 요소의 기능과 유연성을 극대화할 수 있습니다.

### 구성 요소 및 기타 요소 사용자 지정 {#customizing-components-and-other-elements}

고유한 구성 요소를 만들거나 기존 구성 요소를 사용자 지정하는 경우 기존 정의를 다시 사용하는 것이 가장 쉽고 안전합니다. 같은 원칙은 AEM 내의 다른 요소(예: 오류 처리기)에도 적용됩니다.

기존 정의를 복사하고 오버레이하여 수행할 수 있습니다. 즉, 정의를 `/libs`에서 `/apps/<your-project>`로 복사합니다. 이 새 정의는 `/apps`에서 사용자의 요구 사항에 따라 업데이트할 수 있습니다.

>[!NOTE]
>
>자세한 내용은 [Overlays](/help/sites-developing/overlays.md) 사용을 참조하십시오.

예:

* [구성 요소 사용자 정의](/help/sites-developing/components.md)

   여기에는 구성 요소 정의 오버레이가 포함됩니다.

   * 기존 구성 요소를 복사하여 `/apps/<website-name>/components/<MyComponent>`에 새 구성 요소 폴더를 만듭니다.

      * 예를 들어 텍스트 구성 요소 복사본을 사용자 정의하려면

         * 변환 전: `/libs/foundation/components/text`
         * 끝 `/apps/myProject/components/text`

* [오류 처리기에 표시되는 페이지 사용자 지정](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   이 사례에는 서블릿 오버레이가 포함됩니다.

   * 저장소에서 기본 스크립트를 복사합니다.

      * 변환 전: `/libs/sling/servlet/errorhandler/`
      * 끝 `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**은(는) `/libs` 경로에서 아무 것도 변경하지 않아야 합니다.**
>
>이는 다음 번에 인스턴스를 업그레이드할 때 `/libs`의 콘텐트가 덮어쓰기되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓰기 될 수 있음).
>
>구성 및 기타 변경 사항:
>
>1. `/libs`의 항목을 `/apps`에 복사
>1. `/apps` 내에서 변경


## JCR 쿼리를 사용할 때와 이 쿼리를 사용하지 않을 때는 {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR 쿼리는 올바르게 사용할 때 강력한 도구입니다. 적합한 용도:

* 전체 텍스트가 컨텐츠에서 검색되는 것과 같은 실제 최종 사용자 쿼리
* 구조화된 컨텐츠를 전체 저장소에서 찾아야 하는 경우가 있습니다.

   이러한 경우 쿼리가 절대적으로 필요할 때만 실행되도록 하십시오. 예를 들어 구성 요소 활성화 또는 캐시 무효화(예: 워크플로우 단계, 컨텐츠 수정, 필터 등에 대해 트리거되는 이벤트 핸들러).

JCR 쿼리는 순수한 렌더링 요청에 사용해서는 안 됩니다. 예를 들어 JCR 쿼리는

* 렌더링 탐색
* &quot;상위 10개의 최신 뉴스 항목 만들기&quot; 개요
* 콘텐트 항목 수 표시

컨텐츠를 렌더링하는 경우 JCR 쿼리를 수행하는 대신 컨텐츠 트리에 대한 탐색 액세스를 사용하십시오.

>[!NOTE]
>
>[Query Builder](/help/sites-developing/querybuilder-api.md)를 사용하는 경우 쿼리 빌더가 백그라운드에서 JCR 쿼리를 생성하기 때문에 JCR 쿼리를 사용합니다.


## 보안 고려 사항 {#security-considerations}

>[!NOTE]
>
>또한 [보안 검사 목록](/help/sites-administering/security-checklist.md)을 참조할 수 있습니다.

### JCR(저장소) 세션 {#jcr-repository-sessions}

관리 세션이 아닌 사용자 세션을 사용해야 합니다. 즉, 다음을 사용해야 합니다.

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### 크로스 사이트 스크립팅(XSS)에 대한 Protect {#protect-against-cross-site-scripting-xss}

XSS(교차 사이트 스크립팅)를 통해 공격자는 다른 사용자가 보는 웹 페이지에 코드를 삽입할 수 있습니다. 이 보안 취약점은 악성 웹 사용자가 액세스 제어를 우회하도록 악용할 수 있습니다.

AEM은 출력 시 사용자가 제공한 모든 컨텐츠를 필터링하는 원칙을 적용합니다. XSS 예방은 개발 및 테스트 과정에서 가장 우선순위가 높습니다.

또한 Apache](https://modsecurity.org)용 [mod_security와 같은 웹 응용 프로그램 방화벽은 배포 환경의 보안을 중앙에서 안정적으로 제어하고 이전에 감지되지 않은 교차 사이트 스크립팅 공격으로부터 보호할 수 있습니다.

>[!CAUTION]
>
>AEM과 함께 제공되는 예제 코드는 이러한 공격으로부터 자체적으로 보호되지 않을 수 있으며 일반적으로 웹 응용 프로그램 방화벽에 의한 요청 필터링에 의존합니다.

XSS API 요약서에는 XSS API를 사용하고 AEM 앱을 보다 안전하게 만들기 위해 알아야 하는 정보가 포함되어 있습니다. 여기에서 다운로드할 수 있습니다.

XSSAPI 요약서

[파일 가져오기](assets/xss_cheat_sheet_2016.pdf)

### 기밀 정보에 대한 통신 보호 {#securing-communication-for-confidential-information}

인터넷 응용 프로그램의 경우 기밀 정보를 전송할 때

* 트래픽은 SSL을 통해 보호됩니다.
* HTTP POST은 해당되는 경우 사용됩니다.

이는 시스템에 기밀인 정보(구성 또는 관리 액세스 등)와 사용자에게 기밀 정보를 제공하는 경우에 적용됩니다(개인 정보 등)

## 개별 개발 작업 {#distinct-development-tasks}

### 오류 페이지 사용자 지정 {#customizing-error-pages}

오류 페이지는 AEM용으로 사용자 지정할 수 있습니다. 인스턴스가 내부 서버 오류에 대한 슬링 추적을 표시하지 않도록 하는 것이 좋습니다.

자세한 내용은 오류 처리기](/help/sites-developing/customizing-errorhandler-pages.md)에 표시된 오류 페이지 사용자 지정을 참조하십시오.[

### Java 프로세스에서 파일 열기 {#open-files-in-the-java-process}

AEM은 많은 수의 파일에 액세스할 수 있으므로 AEM용으로 Java 프로세스에 대해 [열린 파일 수를 명시적으로 구성하는 것이 좋습니다.](/help/sites-deploying/configuring.md#open-files-in-the-java-process)

이 문제를 최소화하려면 열려 있는 파일이 가능한 한(의미 있게) 올바르게 닫혀 있어야 합니다.
