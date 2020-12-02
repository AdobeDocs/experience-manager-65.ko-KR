---
title: 적응형 양식 로컬라이제이션을 위한 새로운 로케일 지원
seo-title: 적응형 양식 로컬라이제이션을 위한 새로운 로케일 지원
description: AEM Forms을 사용하면 적응형 양식의 현지화를 위한 새로운 로캘을 추가할 수 있습니다. 기본적으로 지원되는 로케일은 영어, 프랑스어, 독일어 및 일본어입니다.
seo-description: AEM Forms을 사용하면 적응형 양식의 현지화를 위한 새로운 로캘을 추가할 수 있습니다. 기본적으로 지원되는 로케일은 영어, 프랑스어, 독일어 및 일본어입니다.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
translation-type: tm+mt
source-git-commit: 1a4bfc91cf91b4b56cc4efa99f60575ac1a9a549
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---


# 적응형 양식 현지화를 위한 새로운 로케일 지원{#supporting-new-locales-for-adaptive-forms-localization}

## 로케일 사전 정보 {#about-locale-dictionaries}

적응형 양식의 현지화는 다음 두 가지 로케일 사전을 사용합니다.

**양식별** 사전적응형 양식에 사용된 문자열을 포함합니다. 예를 들어 레이블, 필드 이름, 오류 메시지, 도움말 설명 등이 있습니다. 각 로케일에 대한 XLIFF 파일 세트로 관리되며 `https://<host>:<port>/libs/cq/i18n/translator.html`에서 액세스할 수 있습니다.

**글로벌** 사전AEM 클라이언트 라이브러리에 JSON 개체로서 관리되는 2개의 글로벌 사전이 있습니다. 이러한 사전에는 기본 오류 메시지, 월 이름, 통화 기호, 날짜 및 시간 패턴 등이 포함되어 있습니다. 이러한 사전은 /libs/fd/xfaforms/clientlibs/I18N의 CRXDe Lite에서 찾을 수 있습니다. 이러한 위치에는 각 로케일에 대한 개별 폴더가 포함되어 있습니다. 글로벌 사전은 일반적으로 자주 업데이트되지 않으므로 각 로케일에 대해 별도의 JavaScript 파일을 유지하면 동일한 서버에서 다른 응용 양식에 액세스할 때 브라우저가 이를 캐싱하고 네트워크 대역폭 사용을 줄일 수 있습니다.

### 적응형 양식의 현지화 작동 방식 {#how-localization-of-adaptive-form-works}

응용 양식의 로케일을 식별하는 두 가지 방법이 있습니다. 응용 양식이 렌더링되면, 요청된 로케일을 다음과 같이 식별합니다.

* 응용 양식 URL에서 `[local]` 선택기를 봅니다. URL의 형식은 `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`입니다. `[local]` 선택기를 사용하면 응용 양식을 캐싱할 수 있습니다.

* 지정된 순서로 다음 매개 변수를 봅니다.

   * 요청 매개 변수 `afAcceptLang`
사용자의 브라우저 로케일을 무시하려면 
`afAcceptLang` request 매개 변수를 사용하여 로케일을 강제 적용합니다. 예를 들어 다음 URL은 양식을 일본어 로케일로 강제로 렌더링합니다.
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 사용자에 대한 브라우저 로케일 집합으로서, `Accept-Language` 헤더를 사용하여 요청에 지정됩니다.

   * AEM에 지정된 사용자의 언어 설정입니다.

   * 브라우저 로케일은 기본적으로 활성화되어 있습니다. 브라우저 로케일 설정을 변경하려면
      * 구성 관리자를 엽니다. URL은 `http://[server]:[port]/system/console/configMgr`입니다.
      * **[!UICONTROL 응용 양식 및 대화형 통신 웹 채널]** 구성을 찾아 엽니다.
      * **[!UICONTROL 브라우저 로케일 사용]** 옵션 및 **[!UICONTROL Save]** 구성의 상태를 변경합니다.

로케일이 식별되면 적응형 양식에서 양식별 사전을 선택합니다. 요청한 로케일에 대한 양식별 사전을 찾을 수 없으면 적응형 양식이 작성되는 언어의 사전을 사용합니다.

로케일 정보가 없는 경우 적응형 양식이 양식의 원래 언어로 제공됩니다. 원래 언어는 적응형 양식을 개발하는 동안 사용되는 언어입니다.

요청한 로케일에 대한 클라이언트 라이브러리가 없는 경우 로케일에 있는 언어 코드가 클라이언트 라이브러리에 있는지 확인합니다. 예를 들어, 요청된 로케일이 `en_ZA`(남아프리카 영어)이고 `en_ZA`에 대한 클라이언트 라이브러리가 없는 경우 적응형 양식이 `en`(영어) 언어에 대해 클라이언트 라이브러리를 사용합니다. 그러나 응용 양식이 없을 경우 응용 양식은 `en` 로케일에 사전을 사용합니다.

## 지원되지 않는 로케일 {#add-localization-support-for-non-supported-locales}에 대한 로컬라이제이션 지원 추가

AEM Forms은 현재 영어(en), 스페인어(es), 프랑스어(fr), 이탈리아어(it), 독일어(de), 일본어(ja), 포르투갈어-브라질(pt-BR), 중국어(zh-CN), 중국어(zh-TW) 및 한국어(ko-KR) 로캘로 적응형 양식 컨텐츠의 로컬라이제이션을 지원합니다.

적응형 양식 런타임에서 새 로케일에 대한 지원을 추가하려면:

1. [GuideLocalizationService 서비스에 로케일 추가](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [로케일용 XFA 클라이언트 라이브러리 추가](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [로케일용 응용 양식 클라이언트 라이브러리 추가](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [사전에 대한 로케일 지원 추가](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [서버 다시 시작](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 가이드 현지화 서비스 {#add-a-locale-to-the-guide-localization-service-br}에 로케일 추가

1. 이동 `https://'[server]:[port]'/system/console/configMgr`.
1. **안내서 현지화 서비스** 구성 요소를 편집하려면 클릭하십시오.
1. 지원되는 로케일 목록에 추가할 로케일을 추가합니다.

![GuideLocalizationService](assets/configservice.png)

### 로케일 {#add-xfa-client-library-for-a-locale-br}에 대한 XFA 클라이언트 라이브러리 추가

`etc/<folderHierarchy>` 범주 아래에 `cq:ClientLibraryFolder` 유형의 노드를 만들고 다음 파일을 클라이언트 라이브러리에 추가합니다.`xfaforms.I18N.<locale>`

* **I18N.** jsdefining  `xfalib.locale.Strings` for the  `<locale>` as defined in  `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.** txt에 다음이 포함됩니다.

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 로케일 {#add-adaptive-form-client-library-for-a-locale-br}에 대한 응용 양식 클라이언트 라이브러리 추가

`etc/<folderHierarchy>` 아래에 `cq:ClientLibraryFolder` 유형의 노드를 만들고 `guides.I18N.<locale>` 카테고리와 `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` 및 `guide.common` 같은 종속성을 만듭니다. &quot;

클라이언트 라이브러리에 다음 파일을 추가합니다.

* **i18** n.jsdefining, with patterns of &quot;calendarCalendar&quot;,  `guidelib.i18n` `datePatterns`,  `timePatterns` `dateTimeSymbols`, and  `numberPatterns`, and, `numberSymbols`  `currencySymbols`  `typefaces`   `<locale>`   [ ](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf),for the XFA specificationsper the XFA specifications는symbols Set SpecificationLocale에 설명되어 있는 XFA 사양에 따라 정의할 수 있습니다. 또한 `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`에서 지원되는 다른 로케일에 대해 정의된 방법도 확인할 수 있습니다.
* **LogMessages.** jsdefining  `guidelib.i18n.strings` and  `guidelib.i18n.LogMessages` for the  `<locale>` as defining in  `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.** txt에 다음이 포함됩니다.

```text
i18n.js
LogMessages.js
```

### 사전 {#add-locale-support-for-the-dictionary-br}에 대한 로케일 지원 추가

추가할 `<locale>`이 `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr` 사이에 없는 경우에만 이 단계를 수행하십시오.

1. 아직 없는 경우 `etc` 아래에 `nt:unstructured` 노드 `languages`을(를) 만듭니다.

1. 다중 값 문자열 속성 `languages`을(를) 노드에 추가합니다(아직 없는 경우).
1. `<locale>` 기본 로케일 값 `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`를 추가합니다(아직 없는 경우).

1. `/etc/languages`의 `languages` 속성 값에 `<locale>`을 추가합니다.

`<locale>`은 `https://'[server]:[port]'/libs/cq/i18n/translator.html`에 나타납니다.

### 서버 {#restart-the-server}을(를) 다시 시작합니다.

추가된 로케일이 적용되도록 AEM 서버를 다시 시작합니다.

## 스페인어 {#sample-libraries-for-adding-support-for-spanish}에 대한 지원을 추가하기 위한 샘플 라이브러리

스페인어 지원을 추가하기 위한 샘플 클라이언트 라이브러리

[파일 가져오기](assets/sample.zip)
