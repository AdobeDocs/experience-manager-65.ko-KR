---
title: 적응형 양식 현지화를 위한 새로운 로케일 지원
seo-title: 적응형 양식 현지화를 위한 새로운 로케일 지원
description: AEM Forms를 사용하면 적응형 양식을 현지화하기 위한 새로운 로캘을 추가할 수 있습니다. 기본적으로 지원되는 로케일은 영어, 프랑스어, 독일어 및 일본어입니다.
seo-description: AEM Forms를 사용하면 적응형 양식을 현지화하기 위한 새로운 로캘을 추가할 수 있습니다. 기본적으로 지원되는 로케일은 영어, 프랑스어, 독일어 및 일본어입니다.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# 적응형 양식 현지화를 위한 새로운 로케일 지원{#supporting-new-locales-for-adaptive-forms-localization}

## 로케일 사전 정보 {#about-locale-dictionaries}

적응형 양식의 현지화는 다음 두 가지 유형의 로케일 사전을 사용합니다.

**양식별 사전** 적응형 양식에 사용된 문자열을 포함합니다. 예를 들어 레이블, 필드 이름, 오류 메시지, 도움말 설명 등이 있습니다. 각 로케일에 대한 XLIFF 파일 세트로 관리되며 에서 액세스할 수 `https://<host>:<port>/libs/cq/i18n/translator.html`있습니다.

**글로벌 사전** AEM 클라이언트 라이브러리에 JSON 개체로 관리되는 두 개의 글로벌 사전이 있습니다. 이러한 사전에는 기본 오류 메시지, 월 이름, 통화 기호, 날짜 및 시간 패턴 등이 포함되어 있습니다. 이러한 사전은 /libs/fd/xfaforms/clientlibs/I18N의 CRXDe Lite에서 찾을 수 있습니다. 이러한 위치에는 각 로케일에 대한 개별 폴더가 포함되어 있습니다. 글로벌 사전은 일반적으로 자주 업데이트되지 않으므로, 각 로케일에 대해 별도의 JavaScript 파일을 유지하면 브라우저가 동일한 서버에서 다른 적응형 양식에 액세스할 때 이를 캐싱하고 네트워크 대역폭 사용을 줄일 수 있습니다.

### 적응형 양식의 현지화 작동 방식 {#how-localization-of-adaptive-form-works}

적응형 양식이 렌더링되면, 지정된 순서로 다음 매개 변수를 확인하여 요청된 로케일을 식별합니다.

* 요청 매개 `afAcceptLang`변수 사용자의 브라우저 로케일을 무시하려면 `afAcceptLang` 요청 매개 변수를 전달하여 로케일을 강제 적용할 수 있습니다. 예를 들어 다음 URL은 일본어 로케일에서 양식을 강제로 렌더링합니다.
   `https://[server]:[port]/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* 사용자에 대한 브라우저 로케일 집합으로서, `Accept-Language` 헤더를 사용하여 요청에 지정됩니다.

* AEM에 지정된 사용자의 언어 설정.

로케일이 식별되면 적응형 양식은 양식별 사전을 선택합니다. 요청한 로케일에 대한 양식별 사전을 찾을 수 없으면 영어(en) 사전이 사용됩니다.

요청한 로케일에 대한 클라이언트 라이브러리가 없는 경우 클라이언트 라이브러리에서 로케일에 있는 언어 코드가 있는지 확인합니다. 예를 들어, 요청된 로케일이 `en_ZA` (남아프리카 영어)이고 클라이언트 라이브러리가 `en_ZA` 없는 경우 적응형 양식은 클라이언트 라이브러리(영어)를 `en` (있는 경우)에 사용합니다. 그러나 이 중 하나가 없는 경우 적응형 양식에서는 `en` 로케일에 대한 사전을 사용합니다.

## 지원되지 않는 로케일에 대한 현지화 지원 추가 {#add-localization-support-for-non-supported-locales}

AEM Forms는 현재 영어(en), 스페인어(es), 프랑스어(fr), 이탈리아어(it), 독일어(de), 일본어(ja), 포르투갈어(브라질)(pt-br), 중국어(zh-tn), 중국어(zh-대만) 및 한국어(ko-kr)로 적응형 양식 컨텐츠의 현지화를 지원합니다.

적응형 양식 런타임 시 새 로케일에 대한 지원을 추가하려면:

1. [GuideLocalizationService 서비스에 로케일 추가](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [로케일용 XFA 클라이언트 라이브러리 추가](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [로케일용 응용 양식 클라이언트 라이브러리 추가](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [사전에 대한 로케일 지원 추가](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [서버 다시 시작](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 가이드 현지화 서비스에 로케일 추가 {#add-a-locale-to-the-guide-localization-service-br}

1. 이동 `https://[server]:[port]/system/console/configMgr`.
1. 가이드 현지화 서비스 **구성 요소를 편집하려면** 클릭하십시오.
1. 지원되는 로케일 목록에 추가할 로케일을 추가합니다.

![GuideLocalizationService](assets/configservice.png)

### 로케일용 XFA 클라이언트 라이브러리 추가 {#add-xfa-client-library-for-a-locale-br}

범주 `cq:ClientLibraryFolder` 아래에 `etc/<folderHierarchy>``xfaforms.I18N.<locale>`유형 노드를 만들고 다음 파일을 클라이언트 라이브러리에 추가합니다.

* **I18N.js** 정의 `xfalib.locale.Strings` 에 `<locale>` `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`있는 JS

* **js.txt** :

```
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 로케일용 응용 양식 클라이언트 라이브러리 추가 {#add-adaptive-form-client-library-for-a-locale-br}

범주 `cq:ClientLibraryFolder` 및 종속성과 같은 `etc/<folderHierarchy>`범주 `guides.I18N.<locale>` 및 종속 항목을 사용하여 `xfaforms.3rdparty`및 `xfaforms.I18N.<locale>` `guide.common`에 유형의 노드를 만듭니다.&quot;

클라이언트 라이브러리에 다음 파일을 추가합니다.

* **i18n** .js `guidelib.i18n`에는 &quot;심볼&quot;, &quot;달력 `datePatterns`&quot;, &quot;달력&quot;, &quot;달력&quot;, `timePatterns`XFA 사양에 따라 정의되는 달력 `dateTimeSymbols``numberPatterns``numberSymbols``currencySymbols``typefaces` `<locale>` [](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf), XFA 사양에는 &quot;로케일 집합&quot; 로케일에 설명되어 있는 CFA 사양과 같은 패턴이 있습니다. 에서 지원되는 다른 로케일에 대해 어떻게 정의되는지 확인할 수도 `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`있습니다.
* **LogMessages.js** 정의 `guidelib.i18n.strings` 및 에 `guidelib.i18n.LogMessages` 정의된 `<locale>` 대로 에 대한 LogMessages.js `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`를 참조하십시오.
* **js.txt** :

```
i18n.js
LogMessages.js
```

### 사전에 대한 로케일 지원 추가 {#add-locale-support-for-the-dictionary-br}

추가하고 `<locale>` 있는 항목이 `en``de`아닌 경우, 이 단계를 수행 `es`, `fr``it``pt-br`, 남은 단계, `zh-tn`남은 단계, `zh-tw``ja``ko-kr`남은 단계만 수행합니다.

1. 아직 없는 경우 `nt:unstructured` `languages` `etc`아래에 노드를 만듭니다.

1. 다중 값 문자열 속성을 노드에 추가합니다(아직 없는 경우). `languages`
1. 기본 값, `<locale>` 로케일, `de`이미 있는 로케일, 사용 중인 로케일, 사용 중인 로케일, 사용 중인 로케일, 사용 중인 로케일, `es`사용 중인 로케일, `fr`사용 중인 로케일, 사용 중인 로케일, 사용 중인 로케일, 또는 사용 중인 로케일, 사용 중인 로케일, 사용, 사용 중인 로케일, 또는 `it``pt-br``zh-tn``zh-tw``ja``ko-kr`이미 없는 경우 이 항목을 추가합니다.

1. 의 `<locale>` 속성 값에 를 `languages` 추가합니다 `/etc/languages`.

에 `<locale>` 표시됩니다 `https://[server]:[port]/libs/cq/i18n/translator.html`.

### 서버 다시 시작 {#restart-the-server}

추가된 로케일을 적용하려면 AEM 서버를 다시 시작합니다.

## 스페인어 지원을 추가하기 위한 샘플 라이브러리 {#sample-libraries-for-adding-support-for-spanish}

스페인어 지원을 추가하기 위한 샘플 클라이언트 라이브러리

[파일 가져오기](assets/sample.zip)
