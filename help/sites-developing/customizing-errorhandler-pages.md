---
title: 오류 핸들러로 표시된 페이지 사용자 지정
description: Adobe Experience Manager에는 HTTP 오류를 처리하기 위한 표준 오류 핸들러가 포함되어 있습니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# 오류 핸들러로 표시된 페이지 사용자 지정{#customizing-pages-shown-by-the-error-handler}

Adobe Experience Manager(AEM)에는 HTTP 오류를 처리하기 위한 표준 오류 처리기가 함께 제공됩니다. 예를 들면 다음과 같습니다.

![chlimage_1-67](assets/chlimage_1-67a.png)

오류 코드에 응답하기 위해 시스템에서 제공한 스크립트가 `/libs/sling/servlet/errorhandler` 아래에 있습니다. 기본적으로 표준 CQ 인스턴스에서 다음 스크립트를 사용할 수 있습니다.

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM은 Apache Sling을 기반으로 합니다. 따라서 Sling 오류 처리에 대한 자세한 내용은 [오류 처리](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)를 참조하십시오.

>[!NOTE]
>
>작성자 인스턴스에서 [CQ WCM 디버그 필터](/help/sites-deploying/osgi-configuration-settings.md)를 기본적으로 사용합니다. 따라서 항상 응답 코드 200이 생성됩니다. 기본 오류 처리기는 전체 스택 추적을 응답에 기록하여 응답합니다.
>
>게시 인스턴스에서 CQ WCM 디버그 필터가 *항상* 비활성화되었습니다(활성화됨으로 구성된 경우에도).

## 오류 핸들러로 표시된 페이지를 사용자 지정하는 방법 {#how-to-customize-pages-shown-by-the-error-handler}

자체 스크립트를 개발하여 오류가 발생했을 때 오류 핸들러에서 표시하는 페이지를 사용자 지정할 수 있습니다. 사용자 지정된 페이지가 `/apps` 아래에 만들어지고 `/libs` 아래에 있는 기본 페이지를 오버레이합니다.

>[!NOTE]
>
>자세한 내용은 [오버레이 사용](/help/sites-developing/overlays.md)을 참조하십시오.

1. 저장소에서 기본 스크립트를 복사합니다.

   * 변환 전: `/libs/sling/servlet/errorhandler/`
   * `/apps/sling/servlet/errorhandler/`에

   기본적으로 대상 경로가 존재하지 않으므로 처음 이 작업을 수행할 때 대상 경로를 만들어야 합니다.

1. `/apps/sling/servlet/errorhandler`(으)로 이동하여 다음 중 하나를 수행합니다.

   * 필요한 정보를 제공할 수 있도록 적절한 기존 스크립트를 편집합니다.
   * 필요한 코드에 대한 새 스크립트를 만들고 편집합니다.

1. 변경 사항을 저장하고 테스트합니다.

>[!CAUTION]
>
>404.jsp 및 403.jsp 핸들러는 CQ5 인증을 지원하도록 설계되었습니다. 특히 이러한 오류가 있는 경우 시스템 로그인을 허용합니다.
>
>따라서 이 두 처리기의 교체는 신중을 기해야 한다.

### HTTP 500 오류에 대한 응답 사용자 지정 {#customizing-the-response-to-http-errors}

HTTP 500 오류는 서버측 예외로 인해 발생합니다.

* **[500 내부 서버 오류](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
서버에서 예기치 않은 상태가 발생하여 요청을 수행할 수 없습니다.

요청 처리로 인해 예외가 발생하면 (AEM이 빌드된) Apache Sling 프레임워크가

* 예외를 기록합니다.
* 반환:

   * http 응답 코드 500
   * 예외 스택 추적

  를 입력합니다.

[오류 처리기로 표시된 페이지를 사용자 지정](#how-to-customize-pages-shown-by-the-error-handler)하면 `500.jsp` 스크립트를 만들 수 있습니다. 그러나 `HttpServletResponse.sendError(500)`이(가) 예외 캐쳐에서 명시적으로 실행되는 경우에만 사용됩니다.

그렇지 않으면 응답 코드가 500으로 설정되어 있지만 `500.jsp` 스크립트가 실행되지 않습니다.

500 오류를 처리하려면 오류 처리기 스크립트의 파일 이름이 예외 클래스(또는 슈퍼클래스)와 같아야 합니다. 이러한 모든 예외를 처리하기 위해 `/apps/sling/servlet/errorhandler/Throwable.js`p 또는 `/apps/sling/servlet/errorhandler/Exception.jsp` 스크립트를 만들 수 있습니다.

>[!CAUTION]
>
>작성자 인스턴스에서 [CQ WCM 디버그 필터](/help/sites-deploying/osgi-configuration-settings.md)를 기본적으로 사용합니다. 따라서 항상 응답 코드 200이 생성됩니다. 기본 오류 처리기는 전체 스택 추적을 응답에 기록하여 응답합니다.
>
>사용자 지정 오류 처리기의 경우 코드 500을 사용한 응답이 필요하므로 [CQ WCM 디버그 필터를 사용하지 않도록 설정해야 합니다](/help/sites-deploying/osgi-configuration-settings.md). 이는 응답 코드(500)가 반환되는 것을 보장하며, 이는 결국 올바른 Sling 오류-핸들러를 트리거한다.
>
>게시 인스턴스에서 CQ WCM 디버그 필터가 *항상* 비활성화되었습니다(활성화됨으로 구성된 경우에도).
