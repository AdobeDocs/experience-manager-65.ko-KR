---
title: 오류 처리기에 표시되는 페이지 사용자 지정
seo-title: 오류 처리기에 표시되는 페이지 사용자 지정
description: AEM에는 HTTP 오류 처리를 위한 표준 오류 처리기가 포함되어 있습니다.
seo-description: AEM에는 HTTP 오류 처리를 위한 표준 오류 처리기가 포함되어 있습니다.
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 오류 처리기에 표시되는 페이지 사용자 지정{#customizing-pages-shown-by-the-error-handler}

AEM에는 HTTP 오류 처리를 위한 표준 오류 처리기가 포함되어 있습니다.예를 들어 다음을 표시합니다.

![chlimage_1-67](assets/chlimage_1-67a.png)

시스템 제공 스크립트는 오류 코드에 응답하기 위해(아래 `/libs/sling/servlet/errorhandler`) 존재하며, 기본적으로 표준 CQ 인스턴스에서 다음을 사용할 수 있습니다.

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM은 Apache Sling을 기반으로 하므로 [Sling](https://sling.apache.org/site/errorhandling.html) 오류 처리에 대한 자세한 내용은 https://sling.apache.org/site/errorhandling.html을 참조하십시오.

>[!NOTE]
>
>작성자 인스턴스에서 CQ WCM [디버그](/help/sites-deploying/osgi-configuration-settings.md) 필터가 기본적으로 활성화되어 있습니다. 이렇게 하면 항상 응답 코드 200이 발생합니다. 기본 오류 처리기는 응답에 전체 스택 추적을 기록하여 응답합니다.
>
>게시 인스턴스에서 CQ WCM 디버그 필터는 *항상* 비활성화되어 있습니다(활성화된 것으로 구성된 경우에도).

## 오류 처리기에 표시되는 페이지 사용자 지정 방법 {#how-to-customize-pages-shown-by-the-error-handler}

오류가 발생할 때 오류 처리기가 표시하는 페이지를 사용자 지정하는 자체 스크립트를 개발할 수 있습니다. 사용자 정의된 페이지가 아래에 `/apps` 만들어지고 기본 페이지(아래 페이지)를 오버레이합니다 `/libs`.

>[!NOTE]
>
>자세한 [내용은 오버레이](/help/sites-developing/overlays.md) 사용을 참조하십시오.

1. 저장소에서 기본 스크립트를 복사합니다.

   * 시작 시간:`/libs/sling/servlet/errorhandler/`
   * 끝 `/apps/sling/servlet/errorhandler/`
   기본적으로 대상 경로가 없으므로 처음 만들 때는 대상 경로를 만들어야 합니다.

1. 다음으로 이동 `/apps/sling/servlet/errorhandler`. 여기에서 다음 중 하나를 수행할 수 있습니다.

   * 적절한 기존 스크립트를 편집하여 필요한 정보를 제공합니다.
   * 필요한 코드에 대한 새 스크립트를 만들고 편집합니다.

1. 변경 내용을 저장하고 테스트합니다.

>[!CAUTION]
>
>404.jsp 및 403.jsp 핸들러는 CQ5 인증을 위해 특별히 고안되었습니다.특히 이러한 오류가 발생하는 경우 시스템 로그인을 허용합니다.
>
>따라서, 이 두 처리기의 교체는 매우 조심해서 해야 한다.

### HTTP 500 오류에 대한 응답 사용자 지정 {#customizing-the-response-to-http-errors}

HTTP 500 오류는 서버측 예외에 의해 발생합니다.

* **[500 내부 서버](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**오류 서버에서 예기치 않은 조건이 발생하여 요청을 수행하지 못했습니다.

요청 처리 결과 예외가 발생하면 Apache Sling 프레임워크(AEM이 구축됨):

* 예외를 기록합니다.
* 반환:

   * http 응답 코드 500
   * 예외 스택 추적
   반응의 본문에.

오류 처리기가 [표시하는 페이지를](#how-to-customize-pages-shown-by-the-error-handler) 사용자 정의하여 `500.jsp` 스크립트를 만들 수 있습니다. 그러나 명시적으로 `HttpServletResponse.sendError(500)` 실행되는 경우에만 사용됩니다.예: 예외 포수

그렇지 않으면 응답 코드가 500으로 설정되지만 `500.jsp` 스크립트가 실행되지 않습니다.

500개의 오류를 처리하려면 오류 처리기 스크립트의 파일 이름이 예외 클래스(또는 수퍼 클래스)와 같아야 합니다. 이러한 모든 예외를 처리하려면 스크립트 `/apps/sling/servlet/errorhandler/Throwable.js`p 또는 `/apps/sling/servlet/errorhandler/Exception.jsp`을 만들 수 있습니다.

>[!CAUTION]
>
>작성자 인스턴스에서 CQ WCM [디버그](/help/sites-deploying/osgi-configuration-settings.md) 필터가 기본적으로 활성화되어 있습니다. 이렇게 하면 항상 응답 코드 200이 발생합니다. 기본 오류 처리기는 응답에 전체 스택 추적을 기록하여 응답합니다.
>
>사용자 지정 오류 처리기의 경우, 코드 500이 있는 응답이 필요하므로 CQ WCM [디버그 필터를 사용하지 않도록 설정해야](/help/sites-deploying/osgi-configuration-settings.md)합니다. 이렇게 하면 응답 코드 500이 반환되고, 이렇게 하면 올바른 Sling 오류 핸들러가 트리거됩니다.
>
>게시 인스턴스에서 CQ WCM 디버그 필터는 *항상* 비활성화되어 있습니다(활성화된 것으로 구성된 경우에도).

