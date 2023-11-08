---
title: CSRF 보호 프레임워크
description: 프레임워크는 토큰을 사용하여 클라이언트 요청이 합법적임을 보장합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 5%

---

# CSRF 보호 프레임워크{#the-csrf-protection-framework}

Apache Sling Referrer Filter 외에도 Adobe은 이러한 유형의 공격으로부터 보호하기 위한 새로운 CSRF 보호 프레임워크를 제공합니다.

프레임워크는 토큰을 사용하여 클라이언트 요청이 합법적임을 보장합니다. 토큰은 양식을 클라이언트로 보낼 때 생성되며 양식을 다시 서버로 보낼 때 확인됩니다.

>[!NOTE]
>
>익명 사용자에 대한 게시 인스턴스에 토큰이 없습니다.

## 요구 사항 {#requirements}

### 종속성 {#dependencies}

를 사용하는 모든 구성 요소 `granite.jquery` 종속성은 CSRF 보호 프레임워크를 자동으로 활용할 수 있습니다. 그렇지 않은 경우 컴포넌트를 선언해야 합니다. `granite.csrf.standalone` 프레임워크를 사용하기 전에

### 암호화 키 복제 {#replicating-crypto-keys}

토큰을 사용하려면 HMAC 바이너리를 배포의 모든 인스턴스에 복제해야 합니다. 다음을 참조하십시오 [HMAC 키 복제](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) 을 참조하십시오.

>[!NOTE]
>
>필요한 사항도 만들어야 합니다 [디스패처 구성 변경 사항](https://helpx.adobe.com/kr/experience-manager/dispatcher/user-guide.html) CSRF 보호 프레임워크를 사용합니다.

>[!NOTE]
>
>웹 응용 프로그램에서 매니페스트 캐시를 사용하는 경우 &quot;**&amp;ast;**&#x200B;토큰이 CSRF 토큰 생성 호출을 오프라인으로 전환하지 않도록 매니페스트에 &quot;를 추가합니다. 자세한 내용은 다음을 참조하십시오. [링크](https://www.w3.org/TR/offline-webapps/).
>
>CSRF 공격 및 이를 완화하는 방법에 대한 자세한 내용은 다음을 참조하십시오. [사이트 간 요청 위조 OWASP 페이지](https://owasp.org/www-community/attacks/csrf).
