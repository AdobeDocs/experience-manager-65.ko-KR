---
title: Dispatcher for Communities 구성
seo-title: Dispatcher for Communities 구성
description: AEM Communities용 디스패처 구성
seo-description: AEM Communities용 디스패처 구성
uuid: c17daca9-3244-4b10-9d4e-2e95df633dd9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 23745dd3-1424-4d22-8456-d2dbd42467f4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Dispatcher for Communities 구성 {#configuring-dispatcher-for-communities}

## AEM Communities {#aem-communities}

AEM Communities의 경우 [커뮤니티 사이트에서](overview.md#community-sites)제대로 작동하도록 디스패처를 구성해야 합니다. 커뮤니티 활성화 및 소셜 로그인과 같은 기능을 포함할 때는 추가 구성이 필요합니다.

특정 배포 및 사이트 디자인에 필요한 사항 살펴보기

* Contact [Customer Care](https://helpx.adobe.com/marketing-cloud/contact-support.html)

기본 Dispatcher [설명서를](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)참조하십시오.

## 발송자 캐싱 {#dispatcher-caching}

### 개요 {#overview}

AEM Communities용 디스패처 캐싱은 디스패처가 완전히 캐시된 버전의 커뮤니티 사이트 페이지를 제공하는 기능입니다.

현재, 커뮤니티 사이트를 탐색하거나 검색 결과로 커뮤니티 페이지에 도착하는 사용자와 페이지를 인덱싱하는 검색 엔진 등 익명의 사이트 방문자만 지원됩니다. 이러한 이점은 익명의 사용자와 검색 엔진이 향상된 성능을 경험할 수 있다는 것입니다.

로그인된 멤버의 경우 디스패처는 캐시를 건너뛰고 모든 페이지가 동적으로 생성되어 배달되도록 요청을 게시자에게 직접 전달합니다.

디스패처 캐싱을 지원하도록 구성되면 디스패처가 캐시된 페이지가 최신 상태인지 확인하기 위해 TTL 기반 &quot;최대 기간&quot; 만료가 헤더에 추가됩니다.

### 요구 사항 {#requirements}

* Dispatcher 버전 4.1.2 이상( [최신 버전의](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html) Dispatcher 설치 참조)
* [ACS AEM Commons 패키지](https://adobe-consulting-services.github.io/acs-aem-commons/)

   * 버전 3.3.2 이상
   * `ACS AEM Commons - Dispatcher Cache Control Header - Max Age` OSGi 구성

### 구성 {#configuration}

OSGi 구성 **ACS AEM Commons - Dispatcher Cache Control Header - Max** Age는 지정된 경로 아래에 표시되는 캐시된 페이지의 만료를 설정합니다.

* 웹 [콘솔에서](../../help/sites-deploying/configuring-osgi.md)

   * 예: [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* 찾기 `ACS AEM Commons - Dispatcher Cache Control Header - Max Age`
* &#39;+&#39; 아이콘을 선택하여 새 연결 구성을 만듭니다.

![chlimage_1-339](assets/chlimage_1-339.png)

* **필터 패턴**
   *(필수)* 커뮤니티 페이지에 대한 하나 이상의 경로. 예, `/content/sites/engage/(.*)`.

* **캐시 제어 최대 페이지**
   *(필수)* 캐시 컨트롤 헤더에 추가할 최대 페이지(초)입니다. 값은 0보다 커야 합니다.

## 발송자 클라이언트 헤더 {#dispatcher-client-headers}

의 /clientheaders 섹션에서 `dispatcher.any`특정 헤더 세트를 나열하는 경우 활성 기능이 `"CSRF-Token"` 제대로 작동하려면 반드시 포함해야 [](enablement.md) 합니다.

## 발송자 필터 {#dispatcher-filters}

파일의 /filter 섹션은 컨텐츠에 대한 액세스 `dispatcher.any` - /filter [](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#filter)구성에 설명되어 있습니다.

이 섹션에서는 Communities 기능의 적절한 기능을 위해 필요한 항목에 대해 설명합니다.

필터 속성 이름은 필터 패턴을 적용할 순서를 나타내기 위해 네 자리 숫자를 사용하는 규칙을 따릅니다. 여러 필터 패턴이 요청에 적용되면 마지막으로 적용된 필터 패턴이 적용됩니다. 따라서 첫 번째 필터 패턴은 다음 패턴이 제어된 방식으로 액세스를 복원하는 등 모든 것을 거부하는 데 종종 사용됩니다.

다음 샘플에서는 특정 dispatcher.any 파일에 맞게 수정해야 하는 속성 이름을 사용합니다.

참고 항목

* [Dispatcher 보안 검사 목록](https://helpx.adobe.com/experience-manager/dispatcher/using/security-checklist.html)

>[!NOTE]
>
>**속성 이름 예**
>표시된 모든 속성 이름(예: **0050** 및 **0170**)은 기존 발송자.임의의 구성 파일에 맞게 조정되어야 합니다.

다음 항목은 /filter 섹션의 끝에, 특히 모든 거부 항목 뒤에 추가해야 합니다.

```shell
# design and template assets
/0050 { /type "allow" /glob "GET /etc/designs/*" }

# collected JS/CSS from the components and design
/0051 { /type "allow" /glob "GET /etc/clientlibs/*" }

# foundation search component - write stats
/0052 { /type "allow" /glob "GET /bin/statistics/tracker/*" }

# allow users to edit profile page
/0054 { /type "allow" /glob "* /home/users/*/*/profile.form.html*" }

# all profile data
/0057 { /type "allow" /glob "GET /home/users/*/profile/*" }

# required for social "Sign In" link.
/0059 { /type "allow" /glob "GET /etc/clientcontext/*" }

# required for "Sign Out" operation
/0063 { /type "allow" /glob "* /system/sling/logout*" }

# enable Facebook and Twitter signin
/0064 { /type "allow" /glob "GET /etc/cloudservices/*" }

# enable personalization
/0062 { /type "allow" /url "/libs/cq/personalization/*" }

# for Enablement features
/0170 { /type "allow" /url "/libs/granite/csrf/token.json*" }
/0171 { /type "allow" /glob "POST /content/sites/*/resources/en/*" }
/0172 { /type "allow" /glob "GET /content/communities/enablement/reports/*" }
/0173 { /type "allow" /glob "GET /content/sites/*" }
/0174 { /type "allow" /glob "GET /content/communities/scorm/*" }
/0175 { /type "allow" /url "GET /content/sites/*" }
/0176 { /type "allow" /url "GET /libs/granite/security/userinfo.json"}
/0177 { /type "allow" /url "GET /libs/granite/security/currentuser.json" }

# Enable CSRF token otherwise nothings works.
/5001 { /type "allow" /glob "GET /libs/granite/csrf/token.json *"}
# Allow SCF User Model to bootstrap as it depends on the granite user
/5002 { /type "allow" /glob "GET /libs/granite/security/currentuser.json*" }

# Allow Communities Site Logout button work
/5003 { /type "allow" /glob "GET /system/sling/logout.html*" }

# Allow i18n to load correctly
/5004 { /type "allow" /glob "GET /libs/cq/i18n/dict.en.json *" }

# Allow social json get pattern.
/6002 { /type "allow" /glob "GET *.social.*.json*" }

# Allow loading of templates
/6003 { /type "allow" /glob "GET /services/social/templates*" }

# Allow SCF User model to check moderator rules
/6005 { /type "allow" /glob "GET /services/social/getLoggedInUser?moderatorCheck=*" }

# Allow CKEditor to load which uses a query pattern not sufficed by regular glob above.
/6006 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
/6007 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

# Allow Fonts from Communities to load
/6050 { /type "allow" /glob "GET *.woff *" }
/6051 { /type "allow" /glob "GET *.ttf *" }

# Enable CQ Security checkpoint for component guide.
/7001 { /type "allow" /glob "GET /libs/cq/security/userinfo.json?cq_ck=*"
```

## 발송자 규칙 {#dispatcher-rules}

의 규칙 섹션은 요청된 URL을 기반으로 캐시해야 하는 응답을 `dispatcher.any` 정의합니다. Communities의 경우 규칙 섹션을 사용하여 캐시해서는 안 되는 항목을 정의합니다.

```shell
# Never cache the client-side .social.json calls
/0001 { /type "deny" /glob "*.social.json*" }

# Never cache the user-specific .json requests
/0002 { /type "deny" /glob "/libs/granite/csrf/token.json*" }
/0003 { /type "deny" /glob "/libs/granite/security/currentuser.json*" }
/0004 { /type "deny" /glob "/libs/granite/security/userinfo.json*" }

# Never cache the private community groups pages in case - add your own deny rules in there
/0005 { /type "deny" /glob "/content/*/groups/*" }

# Never cache the assignments page in case the Enablement feature is in use - add your own deny rules in there
/0006 { /type "deny" /glob "/content/*/assignments/*" }

# Never cache user generated content
/0208 { /type "deny" /glob "/content/usergenerated/*" }
```

## 문제 해결 {#troubleshooting}

특히 액세스를 거부할 규칙을 추가할 때 이전 규칙의 영향을 고려하지 않고 필터 규칙을 삽입하는 것이 문제의 주요 원인입니다.

첫 번째 필터 패턴은 모든 것을 거부하는 데 사용되므로 다음의 필터가 제어된 방식으로 액세스를 복원합니다. 여러 필터가 한 요청에 적용되면 마지막으로 적용되는 필터가 적용됩니다.

## Sample dispatcher.any {#sample-dispatcher-any}

다음은 커뮤니티 /filters 및 /rules를 포함하는 샘플 `dispatcher.any` 파일입니다.

```shell
# Each farm configures a set of load balanced renders (i.e. remote servers)
/farms
  {
  # First farm entry
  /website
    {
    # Request headers that should be forwarded to the remote server.
    /clientheaders
      {
      # Forward all request headers that are end-to-end. If you want
      # to forward a specific set of headers, you'll have to list
      # them here.
      "*"
      }

    # Hostname globbing for farm selection (virtual domain addressing)
    /virtualhosts
      {
      # Entries will be compared against the "Host" request header
      # and an optional request URL prefix.
      #
      # Examples:
      #
      #   www.company.com
      #   intranet.*
      #   myhost:8888/mysite
      "*"
      }

    # The load will be balanced among these render instances
    /renders
      {
      /rend01
        {
        # Hostname or IP of the render
        /hostname "127.0.0.1"
        # Port of the render
        /port "4503"
        # Connect timeout in milliseconds, 0 to wait indefinitely
        # /timeout "0"
        }
      }

    # The filter section defines the requests that should be handled by the dispatcher.
    #
    # Entries can be either specified using globs, or elements of the request line:
    #
    # (1) globs will be compared against the entire request line, e.g.:
    #
    #     /0001 { /type "deny" /glob "* /index.html *" }
    #
    #   matches request "GET /index.html HTTP/1.1" but not "GET /index.html?a=b HTTP/1.1".
    #
    # (2) method/url/query/protocol will be compared againts the respective elements of
    #   the request line, e.g.:
    #
    #     /0001 { /type "deny" /method "GET" /url "/index.html" }
    #
    #   matches both "GET /index.html" and "GET /index.html?a=b HTTP/1.1".
    #
    # Note: specifying elements of the request line is the preferred method.
    /filter
      {
      # Deny everything first and then allow specific entries
      /0001 { /type "deny" /glob "*" }

      # Open consoles
#     /0011 { /type "allow" /url "/admin/*"  }  # allow servlet engine admin
#     /0012 { /type "allow" /url "/crx/*"    }  # allow content repository
#     /0013 { /type "allow" /url "/system/*" }  # allow OSGi console

      # Allow non-public content directories
#     /0021 { /type "allow" /url "/apps/*"   }  # allow apps access
#     /0022 { /type "allow" /url "/bin/*"    }
      /0023 { /type "allow" /url "/content*" }  # disable this rule to allow mapped content only

#     /0024 { /type "allow" /url "/libs/*"   }
#     /0025 { /type "deny"  /url "/libs/shindig/proxy*" } # if you enable /libs close access to proxy

#     /0026 { /type "allow" /url "/home/*"   }
#     /0027 { /type "allow" /url "/tmp/*"    }
#     /0028 { /type "allow" /url "/var/*"    }

      # Enable specific mime types in non-public content directories
      /0041 { /type "allow" /url "*.css"   }  # enable css
      /0042 { /type "allow" /url "*.gif"   }  # enable gifs
      /0043 { /type "allow" /url "*.ico"   }  # enable icos
      /0044 { /type "allow" /url "*.js"    }  # enable javascript
      /0045 { /type "allow" /url "*.png"   }  # enable png
      /0046 { /type "allow" /url "*.swf"   }  # enable flash
      /0047 { /type "allow" /url "*.jpg"   }  # enable jpg
      /0048 { /type "allow" /url "*.jpeg"  }  # enable jpeg

      # Deny content grabbing
      /0081 { /type "deny"  /url "*.infinity.json" }
      /0082 { /type "deny"  /url "*.tidy.json"     }
      /0083 { /type "deny"  /url "*.sysview.xml"   }
      /0084 { /type "deny"  /url "*.docview.json"  }
      /0085 { /type "deny"  /url "*.docview.xml"  }

      /0086 { /type "deny"  /url "*.*[0-9].json" }
#     /0087 { /type "allow" /method "GET" /url "*.1.json" }  # allow one-level json requests

      # Deny query
   /0090 { /type "deny"  /url "*.query.json" }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
   #######################################
   /0050 { /type "allow" /glob "GET /etc/designs/*" }
   /0051 { /type "allow" /glob "GET /etc/clientlibs/*" }
   /0052 { /type "allow" /glob "GET /bin/statistics/tracker/*" }
   /0054 { /type "allow" /glob "* /home/users/*/*/profile.form.html*" }
   /0057 { /type "allow" /glob "GET /home/users/*/profile/*" }
   /0059 { /type "allow" /glob "GET /etc/clientcontext/*" }
   /0063 { /type "allow" /glob "* /system/sling/logout*" }
   /0064 { /type "allow" /glob "GET /etc/cloudservices/*" }
   /0062 { /type "allow" /url "/libs/cq/personalization/*"  }  # enable personalization

   # For Enablement features
   /0170 { /type "allow" /url "/libs/granite/csrf/token.json*" }
   /0171 { /type "allow" /glob "POST /content/sites/*/resources/en/*" }
   /0172 { /type "allow" /glob "GET /content/communities/enablement/reports/*" }
   /0173 { /type "allow" /glob "GET /content/sites/*" }
   /0174 { /type "allow" /glob "GET /content/communities/scorm/*" }
   /0175 { /type "allow" /url "GET /content/sites/*" }
   /0176 { /type "allow" /url "GET /libs/granite/security/userinfo.json"}
   /0177 { /type "allow" /url "GET /libs/granite/security/currentuser.json" }

      # Enable CSRF token otherwise nothings works.
   /5001 { /type "allow" /glob "GET /libs/granite/csrf/token.json *"}

   # Allow SCF User Model to bootstrap as it depends on the granite user
   /5002 { /type "allow" /glob "GET /libs/granite/security/currentuser.json*" }

      # Allow Communities Site Logout button work
      /5003 { /type "allow" /glob "GET /system/sling/logout.html*" }

   # Allow i18n to load correctly
   /5004 { /type "allow" /glob "GET /libs/cq/i18n/dict.en.json *" }

   # Allow social json get pattern.
   /6002 { /type "allow" /glob "GET *.social.*.json*" }

   # Allow loading of templates
   /6003 { /type "allow" /glob "GET /services/social/templates*" }

   # Allow SCF User model to check moderator rules
   /6005 { /type "allow" /glob "GET /services/social/getLoggedInUser?moderatorCheck=*" }

   # Allow CKEditor to load which uses a query pattern not sufficed by regular glob above.
   /6006 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.js?t=*" }
   /6007 { /type "allow" /glob "GET /etc/clientlibs/social/thirdparty/ckeditor/*.css?t=*" }

   # Allow Fonts from Communities to load
   /6050 { /type "allow" /glob "GET *.woff *" }
   /6051 { /type "allow" /glob "GET *.ttf *" }

      # Enable CQ Security checkpoint for component guide.
   /7001 { /type "allow" /glob "GET /libs/cq/security/userinfo.json?cq_ck=*"}

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
   #######################################

      }

    # The cache section regulates what responses will be cached and where.
    /cache
      {
      # The docroot must be equal to the document root of the webserver. The
      # dispatcher will store files relative to this directory and subsequent
      # requests may be "declined" by the dispatcher, allowing the webserver
      # to deliver them just like static files.
      /docroot "/opt/dispatcher"

      # Sets the level upto which files named ".stat" will be created in the
      # document root of the webserver. When an activation request for some
      # page is received, only files within the same subtree are affected
      # by the invalidation.
      #/statfileslevel "0"

      # Flag indicating whether to cache responses to requests that contain
      # authorization information.
      /allowAuthorized "1"

      # Flag indicating whether the dispatcher should serve stale content if
      # no remote server is available.
      #/serveStaleOnError "0"

      # The rules section defines what responses should be cached based on
      # the requested URL. Please note that only the following requests can
      # lead to cacheable responses:
      #
      # - HTTP method is GET
      # - URL has an extension
      # - Request has no query string
      # - Request has no "Authorization" header (unless allowAuthorized is 1)
      /rules
        {
        /0000
          {
          # the globbing pattern to be compared against the url
          # example: * -> everything
          #        : /foo/bar.* -> only the /foo/bar documents
          #        : /foo/bar/* -> all pages below /foo/bar
          #        : /foo/bar[./]* -> all pages below and /foo/bar itself
          #        : *.html        -> all .html files
          /glob "*"
          /type "allow"
          }

      #######################################
      ## BEGIN: AEM COMMUNITITES ADDITIONS
     #######################################

   # Never cache the client-side .social.json calls
   /0001 { /type "deny" /glob "*.social.json*" }

   # Never cache the user-specific .json requests
   /0002 { /type "deny" /glob "/libs/granite/csrf/token.json*" }
   /0003 { /type "deny" /glob "/libs/granite/security/currentuser.json*" }
   /0004 { /type "deny" /glob "/libs/granite/security/userinfo.json*" }

   # Never cache the private community groups pages in case - add your own deny rules in there
   /0005 { /type "deny" /glob "/content/*/groups/*" }

   # Never cache the assignments page in case the enablement feature is in use - add your own deny rules in there
   /0006 { /type "deny" /glob "/content/*/assignments/*" }

      #######################################
      ## END: AEM COMMUNITITES ADDITIONS
      #######################################

        }

      # The invalidate section defines the pages that are "invalidated" after
      # any activation. Please note that the activated page itself and all
      # related documents are flushed on an modification. For example: if the
      # page /foo/bar is activated, all /foo/bar.* files are removed from the
      # cache.
      /invalidate
        {
        /0000
          {
          /glob "*"
          /type "deny"
          }
        /0001
          {
          # Consider all HTML files stale after an activation.
          /glob "*.html"
          /type "allow"
          }
        /0002
          {
          /glob "/etc/segmentation.segment.js"
          /type "allow"
          }
        /0003
          {
          /glob "*/analytics.sitecatalyst.js"
          /type "allow"
          }
        }

      # The allowedClients section restricts the client IP addresses that are
      # allowed to issue activation requests.
      /allowedClients
        {
        # Uncomment the following to restrict activation requests to originate
        # from "localhost" only.
        #
        #/0000
        #  {
        #  /glob "*"
        #  /type "deny"
        #  }
        #/0001
        #  {
        #  /glob "127.0.0.1"
        #  /type "allow"
        #  }
        }

      # The ignoreUrlParams section contains query string parameter names that
      # should be ignored when determining whether some request's output can be
      # cached or delivered from cache.
      #
      # In this example configuration, the "q" parameter will be ignored.
      #/ignoreUrlParams
      #  {
      #  /0001 { /glob "*" /type "deny" }
      #  /0002 { /glob "q" /type "allow" }
      #  }

    /enableTTL "1"

      }

    # The statistics sections dictates how the load should be balanced among the
    # renders according to the media-type.
    /statistics
      {
      /categories
        {
        /html
          {
          /glob "*.html"
          }
        /others
          {
          /glob "*"
          }
        }
      }
    }
  }
```

