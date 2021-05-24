---
title: 정적 개체 만료
seo-title: 정적 개체 만료
description: 정적 개체가 적절한 기간 동안 만료되지 않도록 AEM을 구성하는 방법을 알아봅니다.
seo-description: 정적 개체가 적절한 기간 동안 만료되지 않도록 AEM을 구성하는 방법을 알아봅니다.
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: 구성
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# 정적 개체 만료{#expiration-of-static-objects}

정적 개체(예: 아이콘)는 변경되지 않습니다. 따라서 시스템이 적절한 시간 동안 만료되지 않고 불필요한 트래픽을 줄이도록 구성해야 합니다.

이 기능은 다음과 같은 영향을 줍니다.

* 서버 인프라의 요청을 오프로드합니다.
* 브라우저가 브라우저 캐시에서 개체를 캐시할 때 페이지 로드 성능을 향상시킵니다.

만료는 HTTP 표준에서 파일의 &quot;만료&quot;에 대해 지정합니다(예를 들어, [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Hypertext Transfer Protocol — HTTP 1.1&quot; 장 14.21을 참조하십시오). 이 표준은 헤더를 사용하여 클라이언트가 오래된 것으로 간주될 때까지 개체를 캐시할 수 있습니다.이러한 객체는 원래 서버에 상태 검사를 수행하지 않고 지정된 시간 동안 캐시됩니다.

>[!NOTE]
>
>이 구성은 Dispatcher와 완전히 별개입니다(및 에서는 작동하지 않음).
>
>Dispatcher의 목적은 AEM 앞에 데이터를 캐시하는 것입니다.

동적 파일이 아니며 시간이 지남에 따라 변경되지 않는 모든 파일은 캐싱될 수 있으며 캐시되어야 합니다. Apache HTTPD 서버의 구성은 환경에 따라 다음 중 하나로 표시될 수 있습니다.

>[!CAUTION]
>
>객체가 최신 상태로 간주되는 기간을 정의할 때는 주의해야 합니다. 지정된 기간이 만료될 때까지 *확인이 없으므로 클라이언트가 캐시에서 이전 콘텐츠를 제공할 수 있습니다.*

1. **작성자 인스턴스의 경우:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   이렇게 하면 중간 캐시(예: 브라우저 캐시)가 만료될 때까지 최대 1개월 동안 CSS, Javascript, PNG 및 GIF 파일을 저장할 수 있습니다. 즉, AEM 또는 웹 서버에서 요청할 필요가 없지만 브라우저 캐시에 남아 있을 수 있습니다.

   언제든지 변경될 수 있으므로 사이트의 다른 섹션은 작성자 인스턴스에 캐시되지 않아야 합니다.

1. **게시 인스턴스의 경우:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   이렇게 하면 중간 캐시(예: 브라우저 캐시)가 클라이언트 캐시에서 최대 하루 동안 CSS, Javascript, PNG 및 GIF 파일을 저장할 수 있습니다. 이 예에서는 `/content` 및 `/etc/designs` 아래의 모든 항목에 대한 전역 설정을 설명하지만, 보다 세부적인 설정을 만들어야 합니다.

   사이트 업데이트 빈도에 따라 HTML 페이지 캐싱을 고려할 수도 있습니다. 합리적인 기간은 1시간입니다.

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

정적 개체를 구성한 후 해당 개체를 포함하는 페이지를 선택하는 동안 `request.log`을 검색하여 정적 개체에 대해 아무런(불필요한) 요청이 수행되지 않는지 확인합니다.
