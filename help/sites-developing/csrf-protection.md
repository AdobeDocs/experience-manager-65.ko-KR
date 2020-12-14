---
title: CSRF 보호 프레임워크
seo-title: CSRF 보호 프레임워크
description: 프레임워크에서 토큰을 사용하여 클라이언트 요청이 합법적임을 보장합니다.
seo-description: 프레임워크에서 토큰을 사용하여 클라이언트 요청이 합법적임을 보장합니다.
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
translation-type: tm+mt
source-git-commit: c83c77c5c313099944dd73c8cbe63d429d84a518
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 6%

---


# CSRF 보호 프레임워크{#the-csrf-protection-framework}

Apache Sling Referrer Filter 외에도 Adobe은 이러한 유형의 공격으로부터 보호하기 위해 새로운 CSRF Protection Framework를 제공합니다.

프레임워크에서는 토큰을 사용하여 클라이언트 요청이 합법적임을 보장합니다. 양식이 클라이언트에 전송될 때 토큰이 생성되고 양식이 다시 서버로 전송될 때 유효성이 확인됩니다.

>[!NOTE]
>
>익명 사용자를 위한 게시 인스턴스에 토큰이 없습니다.

## 요구 사항 {#requirements}

### 종속성 {#dependencies}

`granite.jquery` 종속성을 사용하는 모든 구성 요소는 자동으로 CSRF Protection Framework를 통해 혜택을 받습니다. 구성 요소의 경우 이 경우가 아니면 프레임워크를 사용하기 전에 `granite.csrf.standalone`에 대한 종속성을 선언해야 합니다.

### 암호화 키 복제 중 {#replicating-crypto-keys}

토큰을 사용하려면 `/etc/keys/hmac` 바이너리를 배포의 모든 인스턴스에 복제해야 합니다. HMAC 키를 모든 인스턴스에 복사하는 편리한 방법은 키가 포함된 패키지를 만들어 모든 인스턴스에 패키지 관리자를 통해 설치하는 것입니다.

>[!NOTE]
>
>CSRF 보호 프레임워크를 사용하려면 필요한 [Dispatcher 구성을 변경](https://helpx.adobe.com/kr/experience-manager/dispatcher/user-guide.html)해야 합니다.

>[!NOTE]
>
>웹 응용 프로그램에서 매니페스트 캐시를 사용하는 경우 토큰이 CSRF 토큰 생성 호출을 오프라인으로 사용하지 않도록 하려면 매니페스트에 &quot;**&amp;ast;**&quot;을 추가해야 합니다. 자세한 내용은 이 [link](https://www.w3.org/TR/offline-webapps/)을 참조하십시오.
>
>CSRF 공격 및 이를 완화하는 방법에 대한 자세한 내용은 [교차 사이트 요청 위조 OWASP 페이지](https://owasp.org/www-community/attacks/csrf)를 참조하십시오.
