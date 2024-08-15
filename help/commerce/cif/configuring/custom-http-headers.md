---
title: 사용자 정의 HTTP 헤더
description: Adobe Experience Manager Commerce에서 사용자 지정 HTTP 헤더를 구성하는 방법에 대해 알아봅니다.
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---

# 사용자 정의 HTTP 헤더 {#custom-http-headers}

## 개요 {#overview}

백엔드를 더 세밀하게 제어하기 위해 작성자는 CIF에서 이미 보낸 헤더와 함께 상거래 엔진으로 전송할 사용자 지정 HTTP 헤더를 구성할 수 있습니다. 일반적인 사용 사례에는 HTTP 헤더를 사용하여 상거래 백 엔드의 응답을 제어할 수 있는 다중 저장소 설정이 포함됩니다.

>[!NOTE]
>
>개발자는 항상 GraphQL 클라이언트 구성을 사용하여 사용자 지정 HTTP 헤더를 구성할 수 있습니다.
>

## 구성 {#configuration}

사용자 지정 HTTP 헤더를 구성하려면 먼저 헤더를 정의해야 합니다. 사용자 지정 HTTP 헤더는 먼저 OSGi 구성을 사용하여 `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` 서비스 구성에 추가하여 정의해야 합니다.

프로젝트의 [Cloud Service 구성] 페이지에서 HTTP 헤더 값을 구성할 수 있습니다.

1. 도구 > Cloud Services > CIF 구성의 Cloud Service 구성 페이지로 이동합니다.
1. 기존 구성을 열거나 만듭니다.
1. &quot;고급&quot; 탭으로 이동하여 &quot;사용자 지정 HTTP 헤더&quot; 다중 필드를 찾습니다. 앞에서 정의한 헤더를 선택하고 값을 할당할 수 있습니다.

위의 클라우드 서비스 구성을 사용하는 구성 요소는 모든 GraphQL 요청과 함께 이러한 HTTP 헤더를 전송합니다.

## 제한 사항 {#restrictions}

서비스를 통해 표준 헤더 이름을 비롯한 모든 헤더 이름을 정의할 수 있지만, 구성할 때는 사용할 수 없습니다. 즉, 이 기능을 사용하여 표준 HTTP 헤더를 재정의할 수 없습니다. 제한된 헤더 이름 목록은 [mdn 웹 문서 - HTTP 헤더](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)에서 찾을 수 있습니다. 이들 외에도 사용할 수 없는 두 개의 헤더가 더 있습니다.

* &quot;Store&quot; - CIF에서 Adobe Commerce 스토어를 식별하는 데 사용됨
* &quot;Preview-Version&quot; - CIF에서 스테이징된 제품을 검색하는 데 사용
