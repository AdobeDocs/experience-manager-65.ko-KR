---
title: AEM 개발 - 가이드라인 및 모범 사례
description: AEM에서 개발하기 위한 지침 및 모범 사례
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# AEM 개발 - 가이드라인 및 모범 사례{#aem-development-guidelines-and-best-practices}

## 템플릿 및 구성 요소 사용 지침 {#guidelines-for-using-templates-and-components}

Adobe Experience Manager(AEM) 구성 요소와 템플릿은 강력한 툴킷으로 구성됩니다. 개발자가 웹 사이트 비즈니스 사용자, 편집자 및 관리자에게 변화하는 비즈니스 요구 사항(콘텐츠 민첩성)에 맞게 웹 사이트를 조정할 수 있는 기능을 제공하는 데 사용할 수 있습니다. 사이트의 균일한 레이아웃을 유지하면서 이 모든 작업을 수행합니다(브랜드 보호).

웹 사이트 또는 웹 사이트 집합(예: 글로벌 기업의 지사)을 담당하는 사람의 일반적인 과제는 웹 사이트에 새로운 유형의 컨텐츠 프레젠테이션을 도입하는 것입니다.

이미 게시된 다른 문서에서 추출한 웹 사이트를 나열하는 뉴스 목록 페이지를 웹 사이트에 추가해야 한다고 가정해 보겠습니다. 페이지는 나머지 웹 사이트와 동일한 디자인 및 구조를 가져야 합니다.

이러한 문제에 접근하는 권장 방법은 다음과 같습니다.

* 페이지 유형을 만들 수 있도록 기존 템플릿을 재사용합니다. 템플릿은 페이지 구조(탐색 요소, 패널 등)를 대략적으로 정의하며, 이러한 구조는 디자인(CSS, 그래픽)에 따라 미세 조정됩니다.
* 새 페이지에서 단락 시스템(parsys/iparsys)을 사용합니다.
* 승인된 사람(일반적으로 관리자)만 변경할 수 있도록 단락 시스템의 디자인 모드에 대한 액세스 권한을 정의합니다.
* 주어진 단락 시스템에서 허용되는 구성 요소를 정의하여 편집자가 페이지에 필요한 구성 요소를 배치할 수 있도록 합니다. 이 경우 페이지의 하위 트리를 이동하고 사전 정의된 규칙에 따라 정보를 추출할 수 있는 목록 구성 요소일 수 있습니다.
* 편집자는 담당 페이지에서 허용된 구성 요소를 추가 및 구성하여 요청된 기능(정보)을 비즈니스에 제공합니다.

이는 이 접근 방식을 통해 웹 사이트의 기여 사용자 및 관리자가 개발 팀의 개입 없이 비즈니스 요구에 신속하게 대응할 수 있는 방법을 보여 줍니다. 템플릿 생성과 같은 대체 방법은 일반적으로 비용이 많이 드는 작업이므로 변경 관리 프로세스와 개발 팀의 참여가 필요합니다. 이 때문에 전체 프로세스가 더 길어지고 비용이 많이 듭니다.

따라서 AEM 기반 시스템의 개발자는 다음을 사용해야 합니다.

* 균일성과 브랜드 보호를 위한 템플릿 및 단락 시스템 디자인에 대한 액세스 제어
* 유연성을 위해 구성 옵션이 포함된 단락 시스템.

개발자를 위한 다음과 같은 일반 규칙은 대부분의 일반적인 프로젝트에서 사용할 수 있습니다.

* 웹 사이트에서 근본적으로 다른 페이지 구조의 수만큼 템플릿 수를 낮게 유지합니다.
* 사용자 지정 구성 요소에 필요한 유연성과 구성 기능을 제공합니다.
* AEM 단락 시스템(parsys 및 iparsys 구성 요소)의 강력한 기능과 유연성을 최대한 활용합니다.

### 구성 요소 및 기타 요소 맞춤화 {#customizing-components-and-other-elements}

자체 구성 요소를 만들거나 기존 구성 요소를 사용자 정의할 때 기존 정의를 재사용하는 것이 가장 쉽고 안전한 경우가 많습니다. 오류 처리기와 같은 동일한 원칙이 AEM 내의 다른 요소에도 적용됩니다.

이는 기존의 정의를 복사하고 오버레이하여 수행할 수 있다. 즉, 정의를 `/libs`에서 `/apps/<your-project>`(으)로 복사하는 것입니다. `/apps`의 이 새 정의는 요구 사항에 따라 업데이트할 수 있습니다.

>[!NOTE]
>
>자세한 내용은 [오버레이 사용](/help/sites-developing/overlays.md)을 참조하십시오.

예:

* [구성 요소 사용자 정의](/help/sites-developing/components.md)

  여기에는 구성 요소 정의 오버레이가 포함됩니다.

   * 기존 구성 요소를 복사하여 `/apps/<website-name>/components/<MyComponent>`에 구성 요소 폴더를 만듭니다.

      * 예를 들어 텍스트 구성 요소 사본을 사용자 정의하려면 다음을 수행합니다.

         * 변환 전: `/libs/foundation/components/text`
         * `/apps/myProject/components/text`에

* [오류 핸들러로 표시된 페이지 사용자 지정](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  이 경우 서블릿 오버레이가 포함됩니다.

   * 저장소에서 하나 이상의 기본 스크립트를 복사합니다.

      * 변환 전: `/libs/sling/servlet/errorhandler/`
      * `/apps/sling/servlet/errorhandler/`에

>[!CAUTION]
>
>**`/libs` 경로에서 아무 것도 변경하지 마십시오**.
>
>그 이유는 다음에 인스턴스를 업그레이드할 때 `/libs`의 콘텐츠가 덮어쓰기되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수도 있음).
>
>구성 및 기타 변경 사항의 경우:
>
>1. `/libs`의 항목을 `/apps`(으)로 복사
>1. `/apps` 내에서 변경

## JCR 쿼리를 사용해야 하는 경우와 사용하지 말아야 하는 경우 {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR 쿼리는 올바르게 사용할 경우 강력한 도구입니다. 적합한 용도:

* 콘텐츠에 대한 전체 텍스트 검색과 같은 실제 최종 사용자 쿼리
* 전체 저장소에서 구조화된 컨텐츠를 찾아야 하는 경우입니다.

  이러한 경우 필요한 경우에만 쿼리가 실행되도록 합니다. 예를 들어 구성 요소 활성화 또는 캐시 무효화 시(예를 들어 워크플로 단계, 콘텐츠 수정 시 트리거되는 이벤트 핸들러 및 필터와 반대로)

순수 렌더링 요청에 JCR 쿼리를 사용하지 마십시오. 예를 들어 JCR 쿼리는 다음에 적합하지 않습니다.

* 렌더링 탐색
* &quot;상위 10개 최신 뉴스 항목&quot; 개요 만들기
* 컨텐츠 항목의 수 표시

콘텐츠를 렌더링하려면 JCR 쿼리를 수행하는 대신 콘텐츠 트리에 대한 탐색 액세스를 사용하십시오.

>[!NOTE]
>
>[Query Builder](/help/sites-developing/querybuilder-api.md)를 사용하는 경우 Query Builder가 후드에서 JCR 쿼리를 생성하므로 JCR 쿼리를 사용합니다.
>

## 보안 고려 사항 {#security-considerations}

>[!NOTE]
>
>[보안 검사 목록](/help/sites-administering/security-checklist.md)을 참조하는 것도 좋습니다.

### JCR(저장소) 세션 {#jcr-repository-sessions}

관리 세션이 아닌 사용자 세션을 사용합니다. 즉, 다음을 사용해야 합니다.

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### XSS(크로스 사이트 스크립팅)에 대한 Protect {#protect-against-cross-site-scripting-xss}

XSS(크로스 사이트 스크립팅)를 사용하면 공격자가 다른 사용자가 본 웹 페이지에 코드를 삽입할 수 있습니다. 이 보안 취약성은 악의적인 웹 사용자가 액세스 제어를 우회하기 위해 악용될 수 있습니다.

AEM은 출력 시 사용자가 제공한 모든 콘텐츠를 필터링하는 원칙을 적용합니다. XSS 예방은 개발 및 테스트 모두에서 가장 높은 우선순위가 부여됩니다.

또한 Apache용 [mod_security](https://modsecurity.org)과(와) 같은 웹 응용 프로그램 방화벽은 배포 환경의 보안에 대한 신뢰할 수 있는 중앙 집중식 제어를 제공하고 이전에 탐지되지 않은 교차 사이트 스크립팅 공격으로부터 보호할 수 있습니다.

>[!CAUTION]
>
>AEM과 함께 제공된 예제 코드는 그 자체로 이러한 공격으로부터 보호되지 않을 수 있으며 일반적으로 웹 애플리케이션 방화벽에 의한 요청 필터링에 의존합니다.

XSS API 치트 시트 에는 XSS API를 사용하고 AEM 앱을 보다 안전하게 만들기 위해 알아야 하는 정보가 포함되어 있습니다. 여기에서 다운로드할 수 있습니다.

XSSAPI 치트 시트.

[파일 가져오기](assets/xss_cheat_sheet_2016.pdf)

### 기밀 정보에 대한 커뮤니케이션 보호 {#securing-communication-for-confidential-information}

모든 인터넷 응용 프로그램의 경우 기밀 정보를 전송할 때 다음을 확인하십시오

* 트래픽은 SSL을 통해 보호됩니다
* 해당되는 경우 HTTP POST이 사용됩니다

이는 시스템에 대해 기밀(예: 구성 또는 관리 액세스)인 정보와 해당 사용자에 대해 기밀(예: 개인 정보)인 정보에 적용됩니다

## 개별 개발 작업 {#distinct-development-tasks}

### 오류 페이지 사용자 지정 {#customizing-error-pages}

AEM에 대해 오류 페이지를 사용자 지정할 수 있습니다. 인스턴스가 내부 서버 오류에 대한 슬링 추적을 표시하지 않도록 하는 것이 좋습니다.

자세한 내용은 [오류 처리기에 표시된 오류 페이지 사용자 지정](/help/sites-developing/customizing-errorhandler-pages.md)을 참조하십시오.

### Java™ 프로세스에서 파일 열기 {#open-files-in-the-java-process}

AEM은 많은 파일에 액세스할 수 있으므로 AEM에 대해 [열린 Java™ 프로세스에 대한 파일 수](/help/sites-deploying/configuring.md#open-files-in-the-java-process)을 명시적으로 구성하는 것이 좋습니다.

이 문제를 최소화하려면 개발에서 열려 있는 파일이 가능할 때(의미 있게) 올바르게 닫혀 있는지 확인해야 합니다.
