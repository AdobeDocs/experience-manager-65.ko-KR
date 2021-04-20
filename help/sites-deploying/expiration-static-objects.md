---
title: 정적 개체 만료
seo-title: 정적 개체 만료
description: 정적인 객체가 만료되지 않도록 AEM을 구성하는 방법에 대해 알아보십시오(적절한 시간).
seo-description: 정적인 객체가 만료되지 않도록 AEM을 구성하는 방법에 대해 알아보십시오(적절한 시간).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# 정적 개체 만료{#expiration-of-static-objects}

정적 객체(예: 아이콘)는 변경되지 않습니다. 따라서 시스템이 적절한 기간 동안 만료되지 않도록 구성되어야 하므로 불필요한 트래픽이 줄어듭니다.

다음과 같은 영향을 줍니다.

* 서버 인프라에서 요청을 업로드합니다.
* 브라우저가 브라우저 캐시에서 개체를 캐시하여 페이지 로드 성능을 향상시킵니다.

만료는 파일의 &quot;만료&quot;에 대해 HTTP 표준으로 지정됩니다(예: [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; HTTP 1.1&quot;). 이 표준은 헤더를 사용하여 클라이언트가 오래된 것으로 간주될 때까지 객체를 캐시할 수 있습니다.이러한 객체는 원래 서버에 대한 상태 확인 없이 지정된 시간 동안 캐시됩니다.

>[!NOTE]
>
>이 구성은 Dispatcher와 완전히 분리되며(이 경우 작동하지 않음)
>
>Dispatcher의 목적은 AEM 앞에 데이터를 캐시하는 것입니다.

동적 파일이 아니며 시간이 지남에 따라 변경되지 않는 모든 파일은 캐싱될 수 있으며 캐시되어야 합니다. Apache HTTPD 서버에 대한 구성은 환경에 따라 다음 중 하나로 나타날 수 있습니다.

>[!CAUTION]
>
>객체가 최신 상태로 간주되는 기간을 정의할 때는 주의해야 합니다. *지정된 기간이 만료될 때까지 확인이 없으므로 클라이언트는 캐시에서 이전 컨텐츠를 제공할 수 있습니다.*

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

   이렇게 하면 중간 캐시(예: 브라우저 캐시)가 만료될 때까지 최대 1개월 동안 CSS, Javascript, PNG 및 GIF 파일을 저장할 수 있습니다. 즉, AEM 또는 웹 서버에서 요청할 필요는 없지만 브라우저 캐시에 저장할 수 있습니다.

   사이트의 다른 섹션은 언제든지 변경될 수 있으므로 작성 인스턴스에서 캐시되어서는 안 됩니다.

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

   이를 통해 중간 캐시(예: 브라우저 캐시)는 클라이언트 캐시에서 최대 하루 동안 CSS, Javascript, PNG 및 GIF 파일을 저장할 수 있습니다. 이 예제에서는 `/content` 및 `/etc/designs` 아래의 모든 항목에 대한 전역 설정을 표시하지만 보다 세분화된 설정을 만들어야 합니다.

   사이트가 업데이트되는 빈도에 따라 HTML 페이지 캐싱을 고려할 수도 있습니다. 적절한 기간은 1시간입니다.

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

정적 개체를 구성한 후에는 해당 개체를 포함하는 페이지를 선택하는 동안 `request.log`을 검색하여 정적 개체에 대해 요청이 수행되지 않고 있는지 확인합니다.
