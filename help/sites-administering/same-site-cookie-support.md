---
title: AEM 6.5에 대한 Same Site 쿠키 지원
description: AEM 6.5에 대한 Same Site 쿠키 지원에 대해 알아봅니다.
topic-tags: security
exl-id: e1616385-0855-4f70-b787-b01701929bbc
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 74%

---

# AEM 6.5에 대한 Same Site 쿠키 지원 {#same-site-cookie-support-for-aem-65}

버전 80부터 Chrome과 이후 Safari에 쿠키 보안을 위한 새로운 모델이 도입되었습니다. 이 모드는 라는 설정을 통해 서드파티 사이트에 대한 쿠키 가용성의 보안 제어를 도입하기 위해 설계되었습니다. `SameSite`. 자세한 내용은 이 [문서](https://web.dev/samesite-cookies-explained/)를 참조하십시오.

이 설정의 기본값(`SameSite=Lax`)으로 인해 AEM 인스턴스 또는 서비스 간 인증이 제대로 작동하지 않을 수 있습니다. 이들 서비스의 도메인 또는 URL 구조가 이 쿠키 정책의 제한 조건에 해당하지 않을 수 있기 때문입니다.

이 문제를 해결하려면 다음을 설정해야 합니다 `SameSite` 에 대한 쿠키 속성 `None` 로그인 토큰에 사용됩니다.

>[!CAUTION]
>
>다음 `SameSite=None` 설정은 프로토콜이 보안(HTTPS)인 경우에만 적용됩니다.
>
>프로토콜이 안전하지 않은 경우(HTTP) 설정이 무시되고 서버에 다음 경고 메시지가 표시됩니다.
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

아래 단계에 따라 설정을 추가할 수 있습니다.

1. `http://serveraddress:serverport/system/console/configMgr`의 웹 콘솔로 이동합니다.
1. **Adobe Granite 토큰 인증 핸들러**&#x200B;를 검색하여 클릭합니다.
1. 아래 이미지에 표시된 대로 **로그인 토큰 쿠키에 대한 SameSite 속성**&#x200B;을 `None`으로 설정합니다.
   ![samesite](assets/samesite1.png)
1. 저장을 클릭합니다.
1. 이 설정이 업데이트되고 사용자가 로그아웃 후 다시 로그인하면 `login-token` 쿠키가 `None` 속성으로 설정되고 크로스 사이트 요청에 포함됩니다.
