---
title: 범용 편집기
description: 범용 편집기의 유연성과 AEM 6.5를 활용하여 헤드리스 경험을 강화하는 방법을 알아봅니다.
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: 9f91063e51aa599ef48967f832aa359ecf100fc2
workflow-type: ht
source-wordcount: '1183'
ht-degree: 100%

---


# 범용 편집기 {#universal-editor}

범용 편집기의 유연성과 AEM 6.5를 활용하여 헤드리스 경험을 강화하는 방법을 알아봅니다.

## 개요 {#overview}

범용 편집기는 Adobe Experience Manager Sites에 포함된 다용도 시각적 편집기입니다. 작성자는 모든 헤드리스 경험에 대한 WYSIWYG(what-you-see-is-what-you-get) 편집을 수행할 수 있습니다.

* 작성자는 범용 편집기의 유연성을 활용하여 모든 형태의 AEM 헤드리스 콘텐츠에 대해 동일하고 일관된 시각적 편집 경험을 누릴 수 있습니다.
* 개발자는 범용 편집기의 다목적성을 활용하여 구현을 완전히 분리할 수 있습니다. 이를 통해 개발자는 SDK나 기술 제한 없이 사실상 원하는 모든 프레임워크 또는 아키텍처를 활용할 수 있습니다.

자세한 내용은 [범용 편집기의 AEM as a Cloud Service 설명서](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)를 참조하십시오.

## 아키텍처 {#architecture}

범용 편집기는 AEM과 함께 작동하면서 헤드리스 방식으로 콘텐츠를 작성하는 서비스입니다.

* 범용 편집기는 `https://experience.adobe.com/#/aem/editor/canvas`에서 호스팅되며 AEM 6.5에서 렌더링된 페이지를 편집할 수 있습니다.
* AEM 페이지는 AEM 작성자 인스턴스의 Dispatcher를 통해 범용 편집기에서 읽습니다.
* Dispatcher와 동일한 호스트에서 실행되는 범용 편집기 서비스는 변경 사항을 AEM 작성자 인스턴스에 다시 기록합니다.

![범용 편집기를 사용한 작성자 흐름](assets/author-flow.png)

## 요구 사항 {#requirements}

범용 편집기는 다음 환경에서 지원됩니다.

* AEM 6.5
   * 온프레미스 및 AMS 호스팅이 모두 지원됩니다.
* [AEM 6.5 LTS](https://experienceleague.adobe.com/ko/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * 온프레미스 및 AMS 호스팅이 모두 지원됩니다.
* [AEM as a Cloud Service](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)

이 문서는 AEM 6.5의 범용 편집기 지원에 중점을 두고 있습니다. AEM 6.5에서 범용 편집기를 사용하려면 다음이 필요합니다.

* 서비스 팩 23 이상이 포함된 AEM 6.5
   * 서비스 팩 21과 22도 [기능 팩](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)과 함께 지원됩니다.
* 올바르게 구성된 Dispatcher

## 설정 {#setup}

범용 편집기를 테스트하려면 다음 단계를 완료해야 합니다.

1. [로컬 범용 편집기 서비스를 설정합니다.](#set-up-ue)
1. [Dispatcher를 조정하여 범용 편집기 서비스를 허용합니다.](#update-dispatcher)

설정을 완료하면 [범용 편집기를 사용하도록 애플리케이션을 계측](#instrumentation)할 수 있습니다.

### 서비스 구성 {#configure-services}

범용 편집기는 추가 구성이 필요한 여러 패키지를 활용합니다.

#### `login-token` 쿠키의 SameSite 속성을 설정합니다. {#samesite-attribute}

1. 구성 관리자를 엽니다.
   * `http://<host>:<port>/system/console/configMgr`
1. 목록에서 **Adobe Granite 토큰 인증 핸들러**&#x200B;를 찾고 **구성 값 변경**&#x200B;을 클릭합니다.
1. 대화 상자에서 **login-token 쿠키의 SameSite 속성**(`token.samesite.cookie.attr`) 값을 `Partitioned`로 변경합니다.
1. **저장**&#x200B;을 클릭합니다.

#### `SAMEORIGIN` 헤더 X-Frame option을 제거합니다. {#sameorigin}

1. 구성 관리자를 엽니다.
   * `http://<host>:<port>/system/console/configMgr`
1. 목록에서 **Apache Sling Main Servlet**&#x200B;을 찾고 **구성 값 편집**&#x200B;을 클릭합니다.
1. **추가 응답 헤더** 속성(`sling.additional.response.headers`)에서 `X-Frame-Options=SAMEORIGIN` 값이 있으면 삭제합니다.
1. **저장**&#x200B;을 클릭합니다.

#### Adobe Granite 쿼리 매개변수 인증 핸들러를 구성합니다. {#query-parameter}

1. 구성 관리자를 엽니다.
   * `http://<host>:<port>/system/console/configMgr`
1. 목록에서 **Adobe Granite 쿼리 매개변수 인증 핸들러**&#x200B;를 찾고 **구성 값 편집**&#x200B;을 클릭합니다.
1. **경로** 필드(`path`)에서 `/`를 추가하여 활성화합니다.
   * 값이 비어 있으면 인증 핸들러가 비활성화됩니다.
1. **저장**&#x200B;을 클릭합니다.

#### 범용 편집기를 여는 콘텐츠 경로 또는 `sling:resourceTypes`를 정의합니다. {#paths}

1. 구성 관리자를 엽니다.
   * `http://<host>:<port>/system/console/configMgr`
1. 목록에서 **범용 편집기 URL 서비스**&#x200B;를 찾아 **구성 값 편집**&#x200B;을 클릭합니다.
1. 범용 편집기를 여는 콘텐츠 경로 또는 `sling:resourceTypes`를 정의합니다.
   * **범용 편집기 열기 매핑** 필드에서 범용 편집기를 여는 경로를 제공합니다.
   * **범용 편집기로 열리는 Sling:resourceTypes** 필드에 리소스 목록을 제공합니다.
1. **저장**&#x200B;을 클릭합니다.
1. [externalizer 구성](/help/sites-developing/externalizer.md)을 확인하고 최소한 다음 예와 같이 로컬, 작성자 및 게시 환경이 설정되어 있는지 확인합니다.

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

이러한 구성 단계가 완료되면 AEM에서 다음 순서대로 페이지에 대한 범용 편집기가 열립니다.

1. AEM은 `Universal Editor Opening Mapping` 아래의 매핑을 확인하고, 콘텐츠가 해당 매핑에 정의된 경로 아래에 있으면 해당 콘텐츠에 대한 범용 편집기가 열립니다.
1. `Universal Editor Opening Mapping`에 정의된 경로 아래에 없는 콘텐츠의 경우 AEM은 콘텐츠의 `resourceType`이 **범용 편집기로 열리는 Sling:resourceTypes**&#x200B;에 정의된 항목과 일치하는지 확인하고, 콘텐츠가 이러한 유형 중 하나와 일치하면 `${author}${path}.html`에서 범용 편집기가 열립니다.
1. 그렇지 않으면 AEM에서 페이지 편집기가 열립니다.

다음 변수는 `Universal Editor Opening Mapping`에서 매핑을 정의하는 데 사용할 수 있습니다.

* `path`: 열고자 하는 리소스의 콘텐츠 경로
* `localhost`: 스키마가 없는 `localhost`에 대한 외부화 항목(예: `localhost:4502`)
* `author`: 스키마가 없는 작성자에 대한 외부화 항목(예:`localhost:4502`)
* `publish`: 스키마가 없는 게시에 대한 외부화 항목(예:`localhost:4503`)
* `preview`: 스키마가 없는 미리보기에 대한 외부화 항목(예:`localhost:4504`)
* `env`: 정의된 Sling 실행 모드에 기반한 `prod`, `stage`, `dev`
* `token`: `QueryTokenAuthenticationHandler`에 필요한 쿼리 토큰

매핑 예:

* AEM 작성자에서 `/content/foo` 아래의 모든 페이지를 엽니다.
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * 이렇게 하면 `https://localhost:4502/content/foo/x.html?login-token=<token>`이 열립니다.
* 원격 NextJS 서버에서 `/content/bar` 아래의 모든 페이지를 열고 모든 변수를 정보로 제공합니다.
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * 이렇게 하면 `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`이 열립니다.

### 범용 편집기 서비스 설정 {#set-up-ue}

AEM을 업데이트하고 구성하면 로컬 개발 및 테스트를 위해 로컬 범용 편집기 서비스를 설정할 수 있습니다.

1. Node.js 버전 20 이상을 설치합니다.
1. [소프트웨어 배포](https://experienceleague.adobe.com/ko/docs/experience-cloud/software-distribution/home)에서 최신 범용 편집기 서비스를 다운로드하고 압축을 풉니다.
1. 환경 변수 또는 `.env` 파일을 통해 범용 편집기 서비스를 구성합니다.
   * [자세한 내용은 범용 편집기의 AEM as a Cloud Service 설명서를 참조하십시오.](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * 내부 IP를 다시 작성해야 하는 경우 `UES_MAPPING` 옵션을 사용해야 할 수도 있습니다.
1. `universal-editor-service.cjs`를 실행합니다.

### Dispatcher 업데이트 {#update-dispatcher}

AEM이 구성되고 로컬 범용 편집기 서비스가 실행 중이면 [Dispatcher에서](https://experienceleague.adobe.com/ko/docs/experience-manager-dispatcher/using/dispatcher) 새 서비스에 대한 역방향 프록시를 허용해야 합니다.

1. 작성자 인스턴스의 vhost 파일을 조정하여 역방향 프록시를 포함합니다.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080은 기본 포트입니다. [`.env` 파일](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)의 `UES_PORT` 매개변수를 사용하여 해당 값을 변경하면 여기서 포트 값을 그에 따라 조정해야 합니다.

1. Apache를 다시 시작합니다.

## 앱 계측 {#instrumentation}

AEM이 업데이트되고 로컬 범용 편집기 서비스가 실행 중이면 범용 편집기를 사용하여 헤드리스 콘텐츠 편집을 시작할 수 있습니다.

하지만 범용 편집기를 활용하려면 앱을 계측해야 합니다. 여기에는 편집자에게 콘텐츠를 어떻게, 어디에 영구적으로 보관해야 하는지를 알려주는 메타 태그를 포함하는 작업이 포함됩니다. 이 계측에 대한 자세한 내용은 [AEM as a Cloud Service의 범용 편집기 설명서](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)에서 확인할 수 있습니다.

AEM as a Cloud Service의 범용 편집기 설명서를 참조할 때 AEM 6.5에서 해당 범용 편집기를 사용하는 경우 다음과 같은 변경 사항이 적용됩니다.

* 메타 태그의 프로토콜은 `aem` 대신 `aem65`여야 합니다.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* 범용 편집기 서비스 엔드포인트는 메타 태그를 통해 알려야 합니다.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* 구성 요소 정의의 `plugins` 섹션에서 `aem` 대신 `aem65`를 사용해야 합니다.

>[!TIP]
>
>범용 편집기를 처음 사용하는 개발자를 위한 포괄적인 안내서를 보려면 이 섹션에서 명시된 AEM 6.5 지원에 필요한 변경 사항을 염두에 두고 AEM as a Cloud Service의 [AEM 개발자를 위한 범용 편집기 개요](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) 설명서를 참조하십시오.

## AEM 6.5와 AEM as a Cloud Service의 차이점 {#differences}

AEM 6.5의 범용 편집기는 UI와 대부분의 설정을 포함하여 AEM as a Cloud Service와 거의 동일하게 작동합니다. 그러나 주목해야 할 차이점도 있습니다.

* 6.5의 범용 편집기는 헤드리스 사용 사례만 지원합니다.
* 6.5의 범용 편집기 설정이 약간 다릅니다(현재 문서에 [설명됨](#setup)).
* 6.5 버전의 범용 편집기는 AEM as a Cloud Service와 다른 자산 선택기와 콘텐츠 조각 선택기를 사용합니다.
