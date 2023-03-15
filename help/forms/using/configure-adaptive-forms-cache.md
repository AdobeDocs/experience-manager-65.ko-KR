---
title: 적응형 양식 캐시 구성
seo-title: Configure adaptive forms cache
description: 적응형 양식 캐시는 적응형 양식 및 문서를 위해 특별히 설계되었습니다. 클라이언트에서 적응형 양식 또는 문서를 렌더링하는 데 필요한 시간을 줄이기 위한 목적으로 적응형 양식 및 적응형 문서를 캐시합니다.
seo-description: The adaptive forms cache is designed specifically for adaptive forms and documents. It caches adaptive forms and adaptive documents with the objective of reducing the time required to render an adaptive form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
role: Admin
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 1%

---

# 적응형 양식 캐시 구성 {#configure-adaptive-forms-cache}

캐시는 데이터 액세스 시간을 단축하고 지연 시간을 줄이며 입출력 속도를 향상시키는 메커니즘입니다. 적응형 양식 캐시는 미리 채워진 데이터를 저장하지 않고 적응형 양식의 HTML 컨텐츠 및 JSON 구조만 저장합니다. 클라이언트에서 적응형 양식을 렌더링하는 데 필요한 시간을 줄이는 데 도움이 됩니다. 특히 적응형 양식을 위해 디자인되었습니다.

## 작성자 및 게시 인스턴스에서 적응형 양식 캐시 구성 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. 에서 AEM 웹 콘솔 구성 관리자로 이동합니다. `https://[server]:[port]/system/console/configMgr`.
1. 클릭 **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널 구성]** 구성 값을 편집하려면 다음을 수행하십시오.
1. 다음에서 [!UICONTROL 구성 값 편집] 대화 상자에서 AEM의 인스턴스에 대한 양식 또는 문서의 최대 수를 지정합니다. [!DNL Forms] 서버가 캐싱할 수 있는 대상: **[!UICONTROL 적응형 Forms 수]** 필드. 기본값은 100입니다.

   >[!NOTE]
   >
   >캐시를 비활성화하려면 적응형 Forms 수 필드의 값을 다음으로 설정하십시오. **0**. 캐시 구성을 비활성화하거나 변경하면 캐시가 재설정되고 모든 양식 및 문서가 캐시에서 제거됩니다.

   ![적응형 양식 HTML 캐시를 위한 구성 대화 상자](assets/cache-configuration-edit.png)

1. 클릭 **[!UICONTROL 저장]** 구성을 저장합니다.

캐시 적응형 양식 및 관련 에셋을 사용하도록 환경이 구성되어 있습니다.


## (선택 사항) Dispatcher에서 적응형 양식 캐시 구성 {#configure-the-cache}

추가적인 성능 향상을 위해 Dispatcher에서 적응형 양식 캐싱을 구성할 수도 있습니다.

### 전제 조건 {#pre-requisites}

* 활성화 [클라이언트에서 데이터 병합 또는 미리 채우기](prepopulate-adaptive-form-fields.md#prefill-at-client) 옵션을 선택합니다. 이렇게 하면 미리 채워진 양식의 각 인스턴스에 대해 고유한 데이터를 병합하는 데 도움이 됩니다.

### Dispatcher에서 적응형 양식을 캐싱하기 위한 고려 사항 {#considerations}

* 적응형 양식 캐시를 사용하는 경우 AEM을 사용합니다 [!DNL Dispatcher] 를 클릭하여 적응형 양식의 클라이언트 라이브러리(CSS 및 JavaScript)를 캐시합니다.
* 사용자 지정 구성 요소를 개발하는 동안 개발에 사용되는 서버에서 적응형 양식 캐시를 비활성화 상태로 유지합니다.
* 확장명이 없는 URL은 캐시되지 않습니다. 예: 패턴 패턴이 있는 URL`/content/forms/[folder-structure]/[form-name].html` 은 캐시되며 캐싱은 패턴이 있는 URL을 무시합니다. `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. 따라서 캐싱의 이점을 활용하려면 확장과 함께 URL을 사용하십시오.
* 현지화된 적응형 양식에 대한 고려 사항:
   * URL 형식 사용 `http://host:port/content/forms/af/<afName>.<locale>.html` 을(를) 대신해 지역화된 버전의 적응형 양식을 요청하려면 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [브라우저 로케일 사용 비활성화](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) 형식이 있는 URL의 경우 `http://host:port/content/forms/af/<adaptivefName>.html`.
   * URL 형식을 사용하는 경우 `http://host:port/content/forms/af/<adaptivefName>.html`, 및 **[!UICONTROL 브라우저 로케일 사용]** 구성 관리자가 비활성화되면 현지화되지 않은 버전의 적응형 양식이 제공됩니다. 현지화되지 않은 언어는 적응형 양식을 개발하는 동안 사용되는 언어입니다. 브라우저에 대해 구성된 로케일(브라우저 로케일)은 고려하지 않으며 현지화되지 않은 버전의 적응형 양식이 제공됩니다.
   * URL 형식을 사용하는 경우 `http://host:port/content/forms/af/<adaptivefName>.html`, 및 **[!UICONTROL 브라우저 로케일 사용]** 구성 관리자가 활성화되면 현지화된 버전의 적응형 양식이 제공됩니다(사용 가능한 경우). 현지화된 적응형 양식의 언어는 브라우저에 대해 구성된 로케일(브라우저 로케일)을 기반으로 합니다. 다음으로 이어질 수 있습니다. [적응형 양식의 첫 번째 인스턴스만 캐싱]. 인스턴스에서 문제가 발생하지 않도록 하려면 다음을 참조하십시오. [문제 해결](#only-first-insatnce-of-adptive-forms-is-cached).

### Dispatcher에서 캐싱 활성화

Dispatcher에서 캐싱 적응형 양식을 활성화하고 구성하려면 아래 나열된 단계를 수행하십시오.

1. 환경의 모든 게시 인스턴스에 대해 다음 URL을 열고 [환경의 게시 인스턴스에 대해 플러시 에이전트 활성화](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [dispatcher.any 파일에 다음 내용을 추가합니다](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files):

   ```JSON
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
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   위의 내용을 추가할 때:

   * 적응형 양식은 업데이트된 버전의 양식이 게시되지 않을 때까지 캐시에 남아 있습니다.

   * 적응형 양식에서 참조된 리소스의 새 버전이 게시되면 영향을 받은 적응형 양식이 자동으로 무효화됩니다. 참조된 리소스의 자동 무효화에 대한 몇 가지 예외가 있습니다. 예외에 대한 해결 방법은 를 참조하십시오. [문제 해결](#troubleshooting) 섹션.
1. [아래 규칙 dispatcher.any 또는 사용자 지정 규칙 파일을 추가합니다.](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache). 캐싱을 지원하지 않는 URL은 제외합니다. 예를 들어 대화형 통신.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [URL 매개 변수 무시 목록에 다음 매개 변수를 추가합니다](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

AEM 환경이 적응형 양식을 캐시하도록 구성되었습니다. 모든 유형의 적응형 양식을 캐시합니다. 캐시된 페이지를 전달하기 전에 페이지에 대한 사용자 액세스 권한을 확인해야 하는 경우 다음을 참조하십시오. [보안 콘텐츠 캐싱](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=ko-KR).

## 문제 해결 {#troubleshooting}

### 이미지 또는 비디오가 포함된 일부 적응형 양식은 Dispatcher 캐시에서 자동으로 무효화되지 않습니다 {#videos-or-images-not-auto-invalidated}

#### 문제 {#issue1}

에셋 브라우저를 통해 이미지 또는 비디오를 선택하여 적응형 양식에 추가하고 이러한 이미지 및 비디오를 에셋 편집기에서 편집하면 이러한 이미지가 포함된 적응형 양식이 Dispatcher 캐시에서 자동으로 무효화되지 않습니다.

#### 솔루션 {#Solution1}

이미지 및 비디오를 게시한 후 이러한 자산을 참조하는 적응형 양식을 명시적으로 게시 취소하고 게시합니다.

### 적응형 양식의 첫 번째 인스턴스만 캐시됩니다. {#only-first-instance-of-adaptive-forms-is-cached}

#### 문제 {#issue3}

적응형 양식 URL에 현지화 정보가 없는 경우 **[!UICONTROL 브라우저 로케일 사용]** configuration manager가 활성화되면 적응형 양식의 현지화된 버전이 제공되고 적응형 양식의 첫 번째 인스턴스만 캐시되고 모든 후속 사용자에게 전달됩니다.

#### 솔루션 {#Solution3}

문제를 해결하려면 다음 단계를 수행하십시오.

1. 런타임 시 로드되도록 구성된 conf.d/httpd-dispatcher.conf 또는 기타 구성 파일을 엽니다.

1. 다음 코드를 파일에 추가하고 저장합니다. 샘플 코드이며 환경에 맞게 수정합니다.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
