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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# 적응형 양식 로컬라이제이션을 위한 새로운 로케일 지원{#supporting-new-locales-for-adaptive-forms-localization}

## 로케일 사전 정보 {#about-locale-dictionaries}

적응형 양식의 현지화는 다음 두 가지 로케일 사전을 사용합니다.

**양식별 사전** 적응형 양식에 사용된 문자열을 포함합니다. 예를 들어 레이블, 필드 이름, 오류 메시지, 도움말 설명 등이 있습니다. 이 파일은 각 로케일에 대한 XLIFF 파일 세트로 관리되며, 여기에서 액세스할 수 있습니다 `https://<host>:<port>/libs/cq/i18n/translator.html`.

**전역 사전** AEM 클라이언트 라이브러리에 JSON 개체로 관리되는 두 개의 글로벌 사전이 있습니다. 이러한 사전에는 기본 오류 메시지, 월 이름, 통화 기호, 날짜 및 시간 패턴 등이 포함되어 있습니다. 이러한 사전은 /libs/fd/xfaforms/clientlibs/I18N의 CRXDe Lite에서 찾을 수 있습니다. 이러한 위치에는 각 로케일에 대한 개별 폴더가 포함되어 있습니다. 글로벌 사전은 일반적으로 자주 업데이트되지 않으므로 각 로케일에 대해 별도의 JavaScript 파일을 유지하면 동일한 서버에서 다른 응용 양식에 액세스할 때 브라우저가 이를 캐싱하고 네트워크 대역폭 사용을 줄일 수 있습니다.

### 적응형 양식의 로컬라이제이션 방식 {#how-localization-of-adaptive-form-works}

적응형 양식이 렌더링되면 지정된 순서로 다음 매개 변수를 확인하여 요청된 로케일을 식별합니다.

* 요청 매개 변수 `afAcceptLang`사용자의 브라우저 로케일을 무시하려면 
`afAcceptLang` request 매개 변수를 사용하여 로케일을 강제 적용합니다. 예를 들어 다음 URL은 양식을 일본어 로케일로 강제로 렌더링합니다.
   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* 사용자에 대한 브라우저 로케일 집합으로서, 헤더를 사용하여 요청에 지정되어 `Accept-Language` 있습니다.

* AEM에 지정된 사용자의 언어 설정.

로케일이 식별되면 적응형 양식에서 양식별 사전을 선택합니다. 요청된 로케일에 대한 양식별 사전을 찾을 수 없으면 영어(en) 사전이 사용됩니다.

요청한 로케일에 대한 클라이언트 라이브러리가 없는 경우 로케일에 있는 언어 코드가 클라이언트 라이브러리에 있는지 확인합니다. 예를 들어 요청된 로케일이 `en_ZA` (남아프리카 영어)이고 클라이언트 라이브러리가 `en_ZA` 없는 경우 적응형 양식이 클라이언트 라이브러리를 `en` (영어) 언어로 사용합니다(있는 경우). 그러나 응용 양식에 로케일이 없는 경우 사전에서는 `en` 로케일에 사용됩니다.

## 지원되지 않는 로케일에 로컬라이제이션 지원 추가 {#add-localization-support-for-non-supported-locales}

AEM Forms은 현재 영어(en), 스페인어(es), 프랑스어(fr), 이탈리아어(it), 독일어(de), 일본어(ja), 포르투갈어(브라질)(pt-BR), 중국어(zh-CN), 중국어(zh-TW) 및 한국어(ko-KR) 로케일로 적응형 양식 컨텐츠의 로컬라이제이션을 지원합니다.

적응형 양식 런타임에서 새 로케일에 대한 지원을 추가하려면:

1. [GuideLocalizationService 서비스에 로케일 추가](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [로케일용 XFA 클라이언트 라이브러리 추가](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [로케일용 응용 양식 클라이언트 라이브러리 추가](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [사전에 대한 로케일 지원 추가](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [서버 다시 시작](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 가이드 현지화 서비스에 로케일 추가 {#add-a-locale-to-the-guide-localization-service-br}

1. 이동 `https://'[server]:[port]'/system/console/configMgr`.
1. 를 클릭하여 **가이드 로컬라이제이션 서비스 구성 요소를** 편집합니다.
1. 지원되는 로케일 목록에 추가할 로케일을 추가합니다.

![GuideLocalizationService](assets/configservice.png)

### 로케일용 XFA 클라이언트 라이브러리 추가 {#add-xfa-client-library-for-a-locale-br}

범주 `cq:ClientLibraryFolder` 아래 `etc/<folderHierarchy>``xfaforms.I18N.<locale>`의 유형 노드를 만들고 다음 파일을 클라이언트 라이브러리에 추가합니다.

* **I18N.js** 정의 `xfalib.locale.Strings` 에 `<locale>` 정의된 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`대로

* **js.txt** :

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 로케일용 응용 양식 클라이언트 라이브러리 추가 {#add-adaptive-form-client-library-for-a-locale-br}

카테고리 및 종속성 `cq:ClientLibraryFolder` 과 같은 `etc/<folderHierarchy>`범주 `guides.I18N.<locale>` 및 종속 항목을 포함하는 유형 노드 `xfaforms.3rdparty`를 `xfaforms.I18N.<locale>` 만들고, `guide.common`및 &quot;

클라이언트 라이브러리에 다음 파일을 추가합니다.

* **i18n.js** 정의 `guidelib.i18n`, &quot;CalendarSymbols&quot;, `datePatterns`, `timePatterns``dateTimeSymbols`, `numberPatterns`Camera Set Locale에 설명된 XFA 사양당 `numberSymbols`XFA 사양에 따라 &quot;CalendarSymbols&quot;의 패턴, CalendarSymbols, N, Exfa에 대해 `currencySymbols``typefaces` `<locale>` [](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)정의하십시오. 또한 에서 지원되는 다른 로케일에 대해 어떻게 정의되는지 확인할 수 있습니다 `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **에 정의된 대로** 및 `guidelib.i18n.strings` 에 `guidelib.i18n.LogMessages` 대한 LogMessages.js `<locale>` 를 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`참조하십시오.
* **js.txt** :

```text
i18n.js
LogMessages.js
```

### 사전에 대한 로케일 지원 추가 {#add-locale-support-for-the-dictionary-br}

추가하려는 내용이 `<locale>` 중에 없는 경우에만 이 단계 `en`를 수행합니다. 이 단계 `de`는 `es`, `fr`,, `it`, `pt-br``zh-cn``zh-tw``ja``ko-kr`에만 수행합니다.

1. 아직 없는 경우 `nt:unstructured` 아래 `languages` 에 `etc`노드를 만듭니다.

1. 다중 값 문자열 속성 `languages` 을 노드에 추가합니다(아직 없는 경우).
1. 기본 로케일 값 `<locale>` , `de`Locale 값, Facebook, `es`, Facebook `fr`이 없는 경우 기본 로케일 값 `it``pt-br``zh-cn``zh-tw``ja``ko-kr`을 추가합니다.

1. 의 속성 값 `<locale>` 에 를 `languages` 추가합니다 `/etc/languages`.

The `<locale>` will appear at `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### 서버 다시 시작 {#restart-the-server}

추가된 로케일이 적용되도록 AEM 서버를 다시 시작합니다.

## 스페인어 지원을 추가하기 위한 샘플 라이브러리 {#sample-libraries-for-adding-support-for-spanish}

스페인어 지원을 추가하기 위한 샘플 클라이언트 라이브러리

[파일 가져오기](assets/sample.zip)
