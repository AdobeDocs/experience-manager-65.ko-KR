---
title: 맞춤형 HTTP 헤더
description: 사용자 지정 HTTP 헤더 구성
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 3%

---

# 맞춤형 HTTP 헤더 {#custom-http-headers}

## 개요 {#overview}

백엔드를 보다 세밀하게 제어하기 위해 작성자는 CIF에서 이미 보낸 사용자 지정 HTTP 헤더와 함께 상거래 엔진으로 전송될 사용자 지정 HTTP 헤더를 구성할 수 있습니다. 일반적인 사용 사례에는 HTTP 헤더를 사용하여 상거래 백엔드의 응답을 제어할 수 있는 다중 저장소 설정이 포함됩니다.

>[!NOTE]
>
>개발자는 항상 GraphQL 클라이언트 구성을 사용하여 사용자 지정 HTTP 헤더를 구성할 수 있습니다.

## 구성 {#configuration}

사용자 지정 HTTP 헤더를 구성하려면 먼저 사용자 지정 HTTP 헤더를 정의해야 합니다. 먼저 사용자 지정 HTTP 헤더를 `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` OSGi 구성을 사용한 서비스 구성.

프로젝트의 Cloud Service 구성 페이지에서 HTTP 헤더 값을 구성할 수 있습니다.

1. 도구 -> Cloud Services -> CIF 구성의 Cloud Service 구성 페이지로 이동합니다.
1. 기존 구성을 열거나 새 구성을 만듭니다
1. &quot;고급&quot; 탭으로 이동하여 &quot;사용자 지정 HTTP 헤더&quot; 다중 필드를 찾습니다. 앞에서 정의한 헤더를 선택하고 값을 지정할 수 있습니다.

위의 클라우드 서비스 구성을 사용하는 구성 요소는 모든 GraphQL 요청을 통해 이러한 HTTP 헤더를 전송합니다.

## 제한 사항 {#restrictions}

서비스를 통해 표준 헤더 이름을 포함하여 모든 헤더 이름을 정의할 수 있지만 에서는 구성할 수 없습니다. 즉, 이 기능을 사용하여 표준 HTTP 헤더를 재정의할 수 없습니다. 제한된 헤더 이름 목록을 찾을 수 있습니다. [여기](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). 이 헤더 외에 사용할 수 없는 헤더가 두 개 더 있습니다.

* &quot;스토어&quot; - CIF가 Adobe Commerce 스토어를 식별하는 데 사용합니다
* &quot;Preview-Version&quot; - CIF에서 준비된 제품을 검색하는 데 사용됩니다.
