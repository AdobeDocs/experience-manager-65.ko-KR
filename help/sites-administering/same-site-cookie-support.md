---
title: AEM 6.5와 동일한 사이트 쿠키 지원
description: AEM 6.5와 동일한 사이트 쿠키 지원
topic-tags: security
translation-type: tm+mt
source-git-commit: ac2f3d69fd20d7779120a194c698d6f0dd6e6a84
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# AEM 6.5에 대한 동일한 사이트 쿠키 지원 {#same-site-cookie-support-for-aem-65}

버전 80, Chrome 이상 버전의 Safari에서는 쿠키 보안을 위한 새로운 모델을 도입했습니다. 이 모드는 `SameSite`이라는 설정을 통해 제3자 사이트에 쿠키의 가용성에 대한 보안 제어를 도입하도록 설계되었습니다. 자세한 내용은 이 [article](https://web.dev/samesite-cookies-explained/)을 참조하십시오.

이 설정의 기본값(`SameSite=Lax`)으로 인해 AEM 인스턴스 또는 서비스 간 인증이 작동하지 않을 수 있습니다. 이러한 서비스의 도메인 또는 URL 구조가 이 쿠키 정책의 제한 사항에 해당되지 않을 수 있기 때문입니다.

이 문제를 해결하려면 로그인 토큰에 대해 SameSite 쿠키 속성을 `None`으로 설정해야 합니다.

다음 단계에 따라 이 작업을 수행할 수 있습니다.

1. `http://serveraddress:serverport/system/console/configMgr`의 웹 콘솔로 이동
1. **Adobe Granite Token 인증 처리기**&#x200B;를 검색하고 클릭합니다.
1. 아래 이미지에 표시된 것처럼 로그인 토큰 쿠키&#x200B;**에 대한** SameSite 특성을 `None`로 설정합니다.
   ![사마새](assets/samesite1.png)
1. 저장을 클릭합니다
1. 이 설정이 업데이트되고 사용자가 로그아웃되어 다시 로그인하면 `login-token` 쿠키는 `None` 속성 집합을 가지며 교차 사이트 요청에 포함됩니다.
