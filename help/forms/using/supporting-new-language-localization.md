---
title: 적응형 양식 지역화를 위한 새 로케일 지원
seo-title: Supporting new locales for adaptive forms localization
description: AEM Forms을 사용하면 적응형 양식을 현지화하기 위한 새 로케일을 추가할 수 있습니다. 기본적으로 지원되는 로케일은 영어, 프랑스어, 독일어 및 일본어입니다.
seo-description: AEM Forms lets you add new locales for localizing adaptive forms. The supported locales by default are English, French, German, and Japanese.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
feature: Adaptive Forms
role: Admin
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 2%

---

# 적응형 양식 지역화를 위한 새 로케일 지원{#supporting-new-locales-for-adaptive-forms-localization}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization.html) |
| AEM 6.5 | 이 문서 |

## 로케일 사전 정보 {#about-locale-dictionaries}

적응형 양식의 현지화는 두 가지 유형의 로케일 사전을 사용합니다.

**양식 특정 사전** 적응형 양식에 사용되는 문자열을 포함합니다. 예를 들어 레이블, 필드 이름, 오류 메시지, 도움말 설명 등이 있습니다. 각 로케일에 대한 XLIFF 파일 세트로 관리되며 다음 위치에서 액세스할 수 있습니다. `https://<host>:<port>/libs/cq/i18n/translator.html`.

**글로벌 사전** AEM 클라이언트 라이브러리에는 JSON 개체로 관리되는 두 개의 글로벌 사전이 있습니다. 이러한 사전에는 기본 오류 메시지, 월 이름, 통화 기호, 날짜 및 시간 패턴 등이 포함됩니다. CRXDe Lite( /libs/fd/xfaforms/clientlibs/I18N )에서 이러한 사전을 찾을 수 있습니다. 이러한 위치에는 각 로케일에 대해 별도의 폴더가 있습니다. 전역 사전은 일반적으로 자주 업데이트되지 않으므로 각 로케일에 대해 별도의 JavaScript 파일을 유지하면 브라우저가 이를 캐시할 수 있고 동일한 서버의 다른 적응형 양식에 액세스할 때 네트워크 대역폭 사용을 줄일 수 있습니다.

### 적응형 양식의 현지화 작동 방식 {#how-localization-of-adaptive-form-works}

적응형 양식의 로케일을 식별하는 방법에는 두 가지가 있습니다. 적응형 양식이 렌더링되면 은 요청된 로케일을 식별합니다.

* 를 보는 중 `[local]` 적응형 양식 URL의 선택기. URL 형식은 `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`입니다. 사용 `[local]` 선택기를 사용하여 적응형 양식을 캐싱할 수 있습니다.

* 다음 매개 변수를 지정된 순서로 봅니다.

   * 요청 매개 변수 `afAcceptLang`
사용자의 브라우저 로케일을 재정의하려면 `afAcceptLang` 로케일을 강제 적용하기 위한 매개 변수를 요청합니다. 예를 들어 다음 URL은 일본어 로케일로 양식을 강제로 렌더링합니다.
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 을 사용하여 요청에 지정된 사용자에 대한 브라우저 로케일 집합입니다. `Accept-Language` 머리글입니다.

   * AEM에 지정된 사용자의 언어 설정입니다.

   * 브라우저 로케일은 기본적으로 활성화되어 있습니다. 브라우저 로케일 설정을 변경하려면
      * 구성 관리자를 엽니다. URL은 `http://[server]:[port]/system/console/configMgr`
      * 을(를) 찾아 엽니다. **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널]** 구성.
      * 의 상태 변경 **[!UICONTROL 브라우저 로케일 사용]** 옵션 및  **[!UICONTROL 저장]** 구성.

로케일이 식별되면 적응형 양식에서 양식별 사전을 선택합니다. 요청된 로케일에 대한 양식 특정 사전을 찾을 수 없으면 적응형 양식이 작성된 언어용 사전을 사용합니다.

로케일 정보가 없으면 적응형 양식이 양식의 원래 언어로 전달됩니다. 원래 언어는 적응형 양식을 개발할 때 사용되는 언어입니다.

요청한 로케일에 대한 클라이언트 라이브러리가 없으면 로케일에 있는 언어 코드에 대한 클라이언트 라이브러리를 확인합니다. 예를 들어 요청된 로케일이 `en_ZA` (남아프리카 영어) 및 클라이언트 라이브러리 `en_ZA` 이(가) 존재하지 않습니다. 적응형 양식은 다음 작업에 대한 클라이언트 라이브러리를 사용합니다. `en` (영어) 언어(있는 경우). 단, 존재하지 않는 경우 적응형 양식에서는 다음 작업을 위해 사전을 사용합니다 `en` 로케일.

## 지원되지 않는 로케일에 대한 현지화 지원 추가 {#add-localization-support-for-non-supported-locales}

AEM Forms은 현재 영어(en), 스페인어(es), 프랑스어(fr), 이탈리아어(it), 독일어(de), 일본어(ja), 포르투갈어(브라질), 중국어(zh-CN), 중국어(zh-TW) 및 한국어(ko-KR) 로케일로 된 적응형 양식 콘텐츠의 현지화를 지원합니다.

적응형 양식 런타임 시 새 로케일에 대한 지원을 추가하려면 다음 작업을 수행하십시오.

1. [GuideLocalizationService 서비스에 로케일 추가](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [로케일에 대한 XFA 클라이언트 라이브러리 추가](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [로케일에 대한 적응형 양식 클라이언트 라이브러리 추가](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [사전에 대한 로케일 지원 추가](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [서버 다시 시작](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 가이드 현지화 서비스에 로케일 추가 {#add-a-locale-to-the-guide-localization-service-br}

1. `https://'[server]:[port]'/system/console/configMgr`로 이동합니다.
1. 클릭하여 편집 **안내서 로컬라이제이션 서비스** 구성 요소.
1. 추가할 로케일을 지원되는 로케일 목록에 추가합니다.

![GuideLocalizationService](assets/configservice.png)

### 로케일에 대한 XFA 클라이언트 라이브러리 추가 {#add-xfa-client-library-for-a-locale-br}

유형의 노드 만들기 `cq:ClientLibraryFolder` 아래에 `etc/<folderHierarchy>`, 범주 포함 `xfaforms.I18N.<locale>`를 클릭하고 클라이언트 라이브러리에 다음 파일을 추가합니다.

* **I18N.js** 정의 `xfalib.locale.Strings` 대상: `<locale>` 에서 정의된대로 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** 다음을 포함:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 로케일에 대한 적응형 양식 클라이언트 라이브러리 추가 {#add-adaptive-form-client-library-for-a-locale-br}

유형의 노드 만들기 `cq:ClientLibraryFolder` 아래에 `etc/<folderHierarchy>`, 범주 포함 `guides.I18N.<locale>` 및 종속성 `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` 및 `guide.common`. &quot;

클라이언트 라이브러리에 다음 파일을 추가합니다.

* **i18n.js** 정의 `guidelib.i18n`, &quot;calendarSymbols&quot; 패턴 포함, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` 대상: `<locale>` 에 설명된 XFA 사양에 따라 [로케일 집합 사양](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). 에서 지원되는 다른 로케일에 대해 정의되는 방식을 확인할 수도 있습니다. `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** 정의 `guidelib.i18n.strings` 및 `guidelib.i18n.LogMessages` 대상: `<locale>` 에서 정의된대로 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** 다음을 포함:

```text
i18n.js
LogMessages.js
```

### 사전에 대한 로케일 지원 추가 {#add-locale-support-for-the-dictionary-br}

다음 경우에만 이 단계를 수행하십시오. `<locale>` 을(를) 추가하고 있는 이(가) 다음에 없습니다. `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. 만들기 `nt:unstructured` 노드 `languages` 아래에 `etc`, 아직 존재하지 않는 경우.

1. 다중 값 문자열 속성 추가 `languages` 노드(아직 없는 경우)에 추가합니다.
1. 추가 `<locale>` 기본 로케일 값 `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, 아직 존재하지 않는 경우.

1. 추가 `<locale>` 의 값에 `languages` 다음의 속성 `/etc/languages`.

다음 `<locale>` 다음 위치에 표시됩니다. `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### 서버 다시 시작 {#restart-the-server}

추가된 로케일을 적용하려면 AEM 서버를 다시 시작합니다.

## 스페인어 지원 추가용 샘플 라이브러리 {#sample-libraries-for-adding-support-for-spanish}

스페인어 지원 추가를 위한 샘플 클라이언트 라이브러리

[파일 가져오기](assets/sample.zip)
