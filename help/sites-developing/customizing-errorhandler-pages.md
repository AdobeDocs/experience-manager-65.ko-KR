---
title: 오류 핸들러로 표시된 페이지 사용자 지정
seo-title: Customizing Pages shown by the Error Handler
description: AEM에는 HTTP 오류를 처리할 수 있는 표준 오류 핸들러가 포함되어 있습니다
seo-description: AEM comes with a standard error handler for handling HTTP errors
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 5%

---

# 오류 핸들러로 표시된 페이지 사용자 지정{#customizing-pages-shown-by-the-error-handler}

AEM에는 HTTP 오류를 처리하기 위한 표준 오류 처리기가 함께 제공됩니다. 예를 들면 다음과 같습니다.

![chlimage_1-67](assets/chlimage_1-67a.png)

시스템에서 제공한 스크립트가 있습니다( 아래). `/libs/sling/servlet/errorhandler`) 오류 코드에 응답하려면 기본적으로 표준 CQ 인스턴스에서 다음 작업을 사용할 수 있습니다.

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM은 Apache Sling을 기반으로 하므로 다음을 참조하십시오. [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) 슬링 오류 처리에 대한 자세한 내용을 보려면 를 참조하십시오.

>[!NOTE]
>
>작성자 인스턴스에서 [CQ WCM 디버그 필터](/help/sites-deploying/osgi-configuration-settings.md) 은 기본적으로 활성화되어 있습니다. 따라서 항상 응답 코드 200이 생성됩니다. 기본 오류 처리기는 전체 스택 추적을 응답에 기록하여 응답합니다.
>
>게시 인스턴스에서 CQ WCM 디버그 필터는 *항상* 비활성화됨(활성화됨으로 구성된 경우에도).

## 오류 핸들러로 표시된 페이지를 사용자 지정하는 방법 {#how-to-customize-pages-shown-by-the-error-handler}

자체 스크립트를 개발하여 오류가 발생했을 때 오류 핸들러에서 표시하는 페이지를 사용자 지정할 수 있습니다. 맞춤화된 페이지는 아래에 생성됩니다. `/apps` 및 기본 페이지 오버레이(아래) `/libs`).

>[!NOTE]
>
>다음을 참조하십시오 [오버레이 사용](/help/sites-developing/overlays.md) 을 참조하십시오.

1. 저장소에서 기본 스크립트를 복사합니다.

   * 변환 전: `/libs/sling/servlet/errorhandler/`
   * 끝 `/apps/sling/servlet/errorhandler/`

   기본적으로 대상 경로가 없으므로 처음 이 작업을 수행할 때 대상 경로를 만들어야 합니다.

1. 다음으로 이동 `/apps/sling/servlet/errorhandler`. 다음 중 하나를 수행할 수 있습니다.

   * 필요한 정보를 제공하도록 적절한 기존 스크립트를 편집합니다.
   * 필요한 코드에 대한 새 스크립트를 만들고 편집합니다.

1. 변경 사항을 저장하고 테스트합니다.

>[!CAUTION]
>
>404.jsp 및 403.jsp 핸들러는 특히 이러한 오류가 발생하는 경우 시스템 로그인을 허용하도록 CQ5 인증을 지원하도록 특별히 설계되었습니다.
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

작성자: [오류 핸들러로 표시된 페이지 사용자 지정](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 스크립트를 만들 수 있습니다. 그러나 다음과 같은 경우에만 사용됩니다 `HttpServletResponse.sendError(500)` 는 명시적으로 실행됩니다(예: 예외 캐쳐에서).

그렇지 않으면 응답 코드가 500으로 설정되지만 `500.jsp` 스크립트가 실행되지 않습니다.

500 오류를 처리하려면 오류 처리기 스크립트의 파일 이름이 예외 클래스(또는 슈퍼클래스)와 같아야 합니다. 이러한 모든 예외를 처리하기 위해 스크립트를 만들 수 있습니다 `/apps/sling/servlet/errorhandler/Throwable.js`p 또는 `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>작성자 인스턴스에서 [CQ WCM 디버그 필터](/help/sites-deploying/osgi-configuration-settings.md) 은 기본적으로 활성화되어 있습니다. 따라서 항상 응답 코드 200이 생성됩니다. 기본 오류 처리기는 전체 스택 추적을 응답에 기록하여 응답합니다.
>
>사용자 지정 오류 처리기의 경우 코드 500이 있는 응답이 필요하므로 [CQ WCM 디버그 필터를 비활성화해야 합니다.](/help/sites-deploying/osgi-configuration-settings.md). 이는 응답 코드(500)가 반환되는 것을 보장하며, 이는 결국 올바른 Sling 오류-핸들러를 트리거한다.
>
>게시 인스턴스에서 CQ WCM 디버그 필터는 *항상* 비활성화됨(활성화됨으로 구성된 경우에도).
