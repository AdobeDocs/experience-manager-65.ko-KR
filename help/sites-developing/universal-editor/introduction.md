---
title: 범용 편집기
description: 범용 편집기의 유연성과 AEM 6.5를 사용하여 Headless 경험을 제공하는 데 어떻게 도움이 되는지 알아봅니다.
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: d3dd827e93549c558284be1c1991b4e003c9e0e8
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 1%

---


# 범용 편집기 {#universal-editor}

범용 편집기의 유연성과 AEM 6.5를 사용하여 Headless 경험을 제공하는 데 어떻게 도움이 되는지 알아봅니다.

## 개요 {#overview}

범용 편집기는 Adobe Experience Manager Sites의 일부인 다목적 비주얼 편집기입니다. 이를 통해 작성자는 Headless 경험에 대한 간단한(WYSIWYG) 편집을 수행할 수 있습니다.

* 작성자는 모든 형태의 AEM Headless 콘텐츠에 대해 동일한 일관된 시각적 편집을 지원하므로 유니버설 편집기의 유연성이 향상됩니다.
* 개발자는 구현의 진정한 분리를 지원하므로 유니버설 편집기의 다기능성을 활용할 수 있습니다. 이를 통해 개발자는 SDK 또는 기술의 제약 없이 원하는 프레임워크나 아키텍처를 거의 활용할 수 있습니다.

자세한 내용은 범용 편집기에서 [AEM as a Cloud Service 설명서](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)를 참조하세요.

## 아키텍처 {#architecture}

범용 편집기는 AEM과 함께 작동하여 headless로 콘텐츠를 작성하는 서비스입니다.

* 유니버설 편집기는 `https://experience.adobe.com/#/aem/editor/canvas`에서 호스팅되며 AEM 6.5에서 렌더링한 페이지를 편집할 수 있습니다.
* AEM 페이지는 AEM 작성자 인스턴스에서 Dispatcher를 통해 유니버설 편집기에서 읽습니다.
* Dispatcher과 동일한 호스트에서 실행되는 범용 편집기 서비스는 변경 사항을 AEM 작성자 인스턴스에 다시 기록합니다.

![유니버설 편집기를 사용한 작성자 흐름](assets/author-flow.png)

## 요구 사항 {#requirements}

유니버설 편집기는 다음에서 지원합니다.

* AEM 6.5(서비스 팩 21 또는 22 + 기능 팩 추가)
   * 온-프레미스 및 AMS 호스팅이 모두 지원됩니다.
* [AEM as a Cloud Service](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)&#x200B;(릴리스 `2023.8.13099` 이상)

이 문서는 범용 편집기의 AEM 6.5 지원에 중점을 둡니다.

## 설정 {#setup}

범용 편집기를 테스트하려면 다음 작업을 수행해야 합니다.

1. [AEM 작성 인스턴스를 업데이트하고 구성합니다.](#update-configure-aem)
1. [로컬 유니버설 편집기 서비스를 설정합니다.](#set-up-ue)
1. [Universal Editor Service를 허용하도록 Dispatcher를 조정합니다.](#update-dispatcher)

설정이 완료되면 응용 프로그램을 [유니버설 편집기를 사용하도록 계측할 수 있습니다.](#instrumentation)

### AEM 업데이트 {#update-aem}

AEM 6.5와 함께 범용 편집기를 사용하려면 서비스 팩 21 또는 22와 AEM용 기능 팩이 필요합니다.

#### 최신 서비스 팩 적용 {#latest}

AEM 6.5용 서비스 팩 21 또는 22 이상을 실행 중인지 확인하십시오. [소프트웨어 배포](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)에서 최신 서비스 팩을 다운로드할 수 있습니다.

#### 범용 편집기 기능 팩 설치 {#feature-pack}

**AEM용 유니버설 편집기 기능 팩 6.5** [소프트웨어 배포에 사용 가능](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)을(를) 설치합니다.

이미 서비스 팩 23 이상을 실행 중인 경우 기능 팩이 필요하지 않습니다.

### 서비스 구성 {#configure-services}

기능 팩은 추가 구성이 필요한 많은 새 패키지를 설치합니다.

#### `login-token` 쿠키에 대해 SameSite 특성을 설정합니다. {#samesite-attribute}

1. 구성 관리자를 엽니다.
   * `http://<host>:<port>/system/console/configMgr`
1. 목록에서 **Adobe Granite 토큰 인증 처리기**&#x200B;를 찾은 다음 **구성 값 변경**&#x200B;을 클릭합니다.
1. 대화 상자에서 로그인 토큰 쿠키&#x200B;**(`token.samesite.cookie.attr`) 값의** SameSite 특성을 `Partitioned`(으)로 변경합니다.
1. **저장**&#x200B;을 클릭합니다.

#### `SAMEORIGIN` 헤더 X-Frame 옵션을 제거합니다. {#sameorigin}

1. 구성 관리자를 엽니다.
   * `http://<host>:<port>/system/console/configMgr`
1. 목록에서 **Apache Sling 주 서블릿**&#x200B;을(를) 찾은 다음 **구성 값 편집**&#x200B;을(를) 클릭합니다.
1. **추가 응답 헤더** 특성(`sling.additional.response.headers`)이 있는 경우 `X-Frame-Options=SAMEORIGIN` 값을 삭제합니다.
1. **저장**&#x200B;을 클릭합니다.

#### Adobe Granite 쿼리 매개 변수 인증 핸들러를 구성합니다. {#query-parameter}

1. 구성 관리자를 엽니다.
   * `http://<host>:<port>/system/console/configMgr`
1. 목록에서 **Adobe Granite 쿼리 매개 변수 인증 처리기**&#x200B;를 찾은 다음 **구성 값 편집**&#x200B;을 클릭합니다.
1. **경로** 필드(`path`)에서 `/`을(를) 추가하여 활성화하십시오.
   * 값이 비어 있으면 인증 처리기가 비활성화됩니다.
1. **저장**&#x200B;을 클릭합니다.

#### 범용 편집기를 열 콘텐츠 경로 또는 `sling:resourceTypes`을(를) 정의합니다. {#paths}

1. 구성 관리자를 엽니다.
   * `http://<host>:<port>/system/console/configMgr`
1. 목록에서 **유니버설 편집기 URL 서비스**&#x200B;를 찾은 다음 **구성 값 편집**&#x200B;을 클릭합니다.
1. 범용 편집기를 열 콘텐츠 경로 또는 `sling:resourceTypes`을(를) 정의합니다.
   * **유니버설 편집기 열기 매핑** 필드에서 유니버설 편집기를 열 경로를 제공합니다.
   * **범용 편집기에서 여는 Sling:resourceTypes** 필드에 유니버설 편집기에서 직접 여는 리소스 목록을 제공합니다.
1. **저장**&#x200B;을 클릭합니다.
1. [외부화 구성](/help/sites-developing/externalizer.md)을 확인하고 최소한 다음 예제와 같이 로컬, 작성자 및 게시 환경이 설정되어 있는지 확인하십시오.

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

이러한 구성 단계가 완료되면 AEM에서 다음 순서로 페이지용 범용 편집기를 엽니다.

1. AEM이 `Universal Editor Opening Mapping`에서 매핑을 확인하고 콘텐츠가 정의된 경로에 있는 경우 유니버설 편집기가 열립니다.
1. `Universal Editor Opening Mapping`에 정의된 경로에 없는 콘텐츠의 경우, AEM은 콘텐츠의 `resourceType`이(가) 유니버설 편집기에서 열어야 하는 **Sling:resourceTypes에 정의된 유형과 일치하는지 확인**&#x200B;하고, 콘텐츠가 그러한 유형 중 하나와 일치하면 `${author}${path}.html`에 유니버설 편집기가 열립니다.
1. 그렇지 않으면 AEM에서 페이지 편집기가 열립니다.

`Universal Editor Opening Mapping`에서 매핑을 정의하는 데 다음 변수를 사용할 수 있습니다.

* `path`: 열 리소스의 콘텐츠 경로
* `localhost`: 스키마 없이 `localhost`에 대한 외부화 항목(예: `localhost:4502`)
* `author`: 스키마 없는 작성자에 대한 외부화 항목(예: `localhost:4502`)
* `publish`: 스키마 없이 게시하기 위한 외부화 항목(예: `localhost:4503`)
* `preview`: 스키마 없이 미리 보기하기 위한 외부화 항목(예: `localhost:4504`)
* `env`: 정의된 Sling 실행 모드를 기반으로 하는 `prod`, `stage`, `dev`
* `token`: `QueryTokenAuthenticationHandler`에 필요한 쿼리 토큰

예제 매핑:

* AEM 작성자의 `/content/foo`에서 모든 페이지를 엽니다.
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * `https://localhost:4502/content/foo/x.html?login-token=<token>`을(를) 엽니다.
* 원격 NextJS 서버에서 `/content/bar`의 모든 페이지를 열어 모든 변수를 정보로 제공
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`을(를) 엽니다.

### 범용 편집기 서비스 설정 {#set-up-ue}

AEM이 업데이트 및 구성되면 고유한 로컬 개발 및 테스트를 위해 로컬 유니버설 편집기 서비스를 설정할 수 있습니다.

1. Node.js 버전 >=20을 설치합니다.
1. [Software Distribution](https://experienceleague.adobe.com/en/docs/experience-cloud/software-distribution/home)에서 최신 유니버설 편집기 서비스 다운로드 및 압축 풀기
1. 환경 변수 또는 `.env` 파일을 통해 유니버설 편집기 서비스를 구성하십시오.
   * [자세한 내용은 AEM as a Cloud Service 유니버설 편집기 설명서를 참조하세요.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * 내부 IP 재작성이 필요한 경우 `UES_MAPPING` 옵션을 사용해야 할 수 있습니다.
1. `universal-editor-service.cjs` 실행

### Dispatcher 업데이트 {#update-dispatcher}

AEM이 구성되어 있고 로컬 유니버설 편집기 서비스가 실행 중인 경우 Dispatcher에서 새 서비스 [에 대한 역방향 프록시를 허용해야 합니다.](https://experienceleague.adobe.com/ko/docs/experience-manager-dispatcher/using/dispatcher)

1. 역방향 프록시를 포함하도록 작성자 인스턴스의 vhost 파일을 조정합니다.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080이 기본 포트입니다. [내 `.env` 파일,](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)에서 `UES_PORT` 매개 변수를 사용하여 이 값을 변경한 경우 여기에서 포트 값을 적절하게 조정해야 합니다.

1. Apache를 다시 시작합니다.

## 앱 계기 {#instrumentation}

AEM이 업데이트되고 로컬 유니버설 편집기 서비스가 실행되면 유니버설 편집기를 사용하여 headless 콘텐츠 편집을 시작할 수 있습니다.

그러나 범용 편집기를 사용하려면 앱을 계측해야 합니다. 여기에는 콘텐츠를 지속하는 방법과 위치를 편집기에 지시하는 메타 태그가 포함됩니다. 이 계기에 대한 자세한 내용은 [AEM as a Cloud Service용 유니버설 편집기 설명서](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)를 참조하세요.

AEM as a Cloud Service을 사용하는 범용 편집기에 대한 설명서를 참조할 때 AEM 6.5에서 사용할 때 다음 변경 사항이 적용됩니다.

* 메타 태그의 프로토콜은 `aem` 대신 `aem65`이어야 합니다.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* 범용 편집기 서비스 끝점은 메타 태그를 통해 알려야 합니다.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* 구성 요소 정의의 `plugins` 섹션에서 `aem` 대신 `aem65`을(를) 사용해야 합니다.

>[!TIP]
>
>범용 편집기를 시작하는 개발자를 위한 포괄적인 안내서는 이 섹션에서 언급한 대로 AEM 6.5 지원에 필요한 변경 사항을 염두에 두고 AEM as a Cloud Service 설명서의 [AEM 개발자를 위한 범용 편집기 개요](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) 문서를 참조하십시오.

## AEM 6.5와 AEM as a Cloud Service의 차이점 {#differences}

AEM 6.5의 유니버설 편집기는 UI 및 대부분의 설정을 포함하여 AEM as a Cloud Service과 동일하게 작동합니다. 그러나 주의해야 할 차이점이 있습니다.

* 6.5의 유니버설 편집기는 Headless 사용 사례만 지원합니다.
* 유니버설 편집기의 설정이 6.5마다 약간 다릅니다([현재 문서의 ](#setup)에 설명된 대로).
* 6.5의 유니버설 편집기는 AEM as a Cloud Service과 다른 에셋 선택기와 콘텐츠 조각 선택기를 사용합니다.
