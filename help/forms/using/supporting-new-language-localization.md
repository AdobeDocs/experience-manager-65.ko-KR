---
title: 적응형 양식 지역화를 위한 새 로케일 지원
description: AEM Forms을 사용하면 적응형 양식을 현지화하기 위한 새 로케일을 추가할 수 있습니다. 기본적으로 지원되는 로케일은 영어, 프랑스어, 독일어 및 일본어입니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
feature: Adaptive Forms,Foundation Components
role: Admin,User
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 2%

---

# 적응형 양식 지역화를 위한 새 로케일 지원{#supporting-new-locales-for-adaptive-forms-localization}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization.html) |
| AEM 6.5 | 이 문서 |

## 로케일 사전 정보 {#about-locale-dictionaries}

적응형 양식의 현지화는 두 가지 유형의 로케일 사전을 사용합니다.

**양식별 사전**&#x200B;에 적응형 양식에 사용되는 문자열이 포함되어 있습니다. 예를 들어 레이블, 필드 이름, 오류 메시지, 도움말 설명 등이 있습니다. 각 로케일에 대한 XLIFF 파일 집합으로 관리되며 `https://<host>:<port>/libs/cq/i18n/translator.html`에서 액세스할 수 있습니다.

**전역 사전** AEM 클라이언트 라이브러리에 JSON 개체로 관리되는 두 개의 전역 사전이 있습니다. 이러한 사전에는 기본 오류 메시지, 월 이름, 통화 기호, 날짜 및 시간 패턴 등이 포함됩니다. CRXDe Lite( /libs/fd/xfaforms/clientlibs/I18N )에서 이러한 사전을 찾을 수 있습니다. 이러한 위치에는 각 로케일에 대해 별도의 폴더가 있습니다. 전역 사전은 일반적으로 자주 업데이트되지 않으므로 각 로케일에 대해 별도의 JavaScript 파일을 유지하면 브라우저가 이를 캐시할 수 있고 동일한 서버의 다른 적응형 양식에 액세스할 때 네트워크 대역폭 사용을 줄일 수 있습니다.

### 적응형 양식의 현지화 작동 방식 {#how-localization-of-adaptive-form-works}

적응형 양식의 로케일을 식별하는 방법에는 두 가지가 있습니다. 적응형 양식이 렌더링되면 은 요청된 로케일을 식별합니다.

* 적응형 양식 URL에서 `[local]` 선택기를 봅니다. URL 형식은 `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`입니다. `[local]` 선택기를 사용하면 적응형 양식을 캐싱할 수 있습니다.

* 다음 매개 변수를 지정된 순서로 봅니다.

   * 요청 매개 변수 `afAcceptLang`
사용자의 브라우저 로캘을 재정의하려면 `afAcceptLang` 요청 매개 변수를 전달하여 로캘을 강제 적용할 수 있습니다. 예를 들어 다음 URL은 일본어 로케일로 양식을 렌더링하도록 강제되어 있습니다.
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * `Accept-Language` 헤더를 사용하여 요청에 지정된 사용자에 대한 브라우저 로케일 집합입니다.

   * AEM에 지정된 사용자의 언어 설정입니다.

   * 브라우저 로케일은 기본적으로 활성화되어 있습니다. 브라우저 로케일 설정을 변경하려면
      * 구성 관리자를 엽니다. URL은 `http://[server]:[port]/system/console/configMgr`입니다.
      * **[!UICONTROL 적응형 양식 및 대화형 통신 웹 채널]** 구성을 찾아 엽니다.
      * **[!UICONTROL 브라우저 로케일 사용]** 옵션 및 **[!UICONTROL 구성 저장]**&#x200B;의 상태를 변경합니다.

로케일이 식별되면 적응형 양식에서 양식별 사전을 선택합니다. 요청된 로케일에 대한 양식 특정 사전을 찾을 수 없으면 적응형 양식이 작성된 언어용 사전을 사용합니다.

로케일 정보가 없으면 적응형 양식이 양식의 원래 언어로 전달됩니다. 원래 언어는 적응형 양식을 개발할 때 사용되는 언어입니다.

요청한 로케일에 대한 클라이언트 라이브러리가 없으면 로케일에 있는 언어 코드에 대한 클라이언트 라이브러리를 확인합니다. 예를 들어 요청된 로케일이 `en_ZA`(남아프리카 영어)이고 `en_ZA`에 대한 클라이언트 라이브러리가 없는 경우 적응형 양식은 `en`(영어) 언어의 클라이언트 라이브러리가 있는 경우 이를 사용합니다. 단, 해당 항목이 없으면 적응형 양식에서 `en` 로케일에 대한 사전을 사용합니다.

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
1. **Guide Localization Service** 구성 요소를 편집하려면 클릭하십시오.
1. 추가할 로케일을 지원되는 로케일 목록에 추가합니다.

![GuideLocalizationService](assets/configservice.png)

### 로케일에 대한 XFA 클라이언트 라이브러리 추가 {#add-xfa-client-library-for-a-locale-br}

`etc/<folderHierarchy>` 아래에 `cq:ClientLibraryFolder` 형식의 노드를 만들고 `xfaforms.I18N.<locale>` 범주를 사용하여 다음 파일을 클라이언트 라이브러리에 추가하십시오.

* `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`에 정의된 대로 `<locale>`에 대해 `xfalib.locale.Strings`을(를) 정의하는 **I18N.js**.

* 다음을 포함하는 **js.txt**:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 로케일에 대한 적응형 양식 클라이언트 라이브러리 추가 {#add-adaptive-form-client-library-for-a-locale-br}

`etc/<folderHierarchy>` 아래에 `cq:ClientLibraryFolder` 유형의 노드를 만드십시오. 이 노드는 범주가 `guides.I18N.<locale>`(으)로, 종속성이 `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` 및 `guide.common`(으)로 설정되어 있습니다. &quot;

클라이언트 라이브러리에 다음 파일을 추가합니다.

* [로케일 집합 지정](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)에 설명된 XFA 사양에 따라 `<locale>`에 대해 &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` 패턴을 가진 `guidelib.i18n`을(를) 정의하는 **i18n.js**. `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`에서 지원되는 다른 로케일에 대해 정의된 방법도 확인할 수 있습니다.
* `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`에 정의된 대로 `<locale>`에 대해 `guidelib.i18n.strings` 및 `guidelib.i18n.LogMessages`을(를) 정의하는 **LogMessages.js**.
* 다음을 포함하는 **js.txt**:

```text
i18n.js
LogMessages.js
```

### 사전에 대한 로케일 지원 추가 {#add-locale-support-for-the-dictionary-br}

추가하려는 `<locale>`이(가) `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`에 없는 경우에만 이 단계를 수행하십시오.

1. 아직 없는 경우 `etc`에 `nt:unstructured` 노드 `languages`을(를) 만듭니다.

1. 다중 값 문자열 속성 `languages`이(가) 아직 없는 경우 노드에 추가하십시오.
1. `<locale>` 기본 로케일 값 `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`을(를) 추가합니다(아직 없는 경우).

1. `/etc/languages`의 `languages` 속성 값에 `<locale>`을(를) 추가합니다.

`<locale>`이(가) `https://'[server]:[port]'/libs/cq/i18n/translator.html`에 나타납니다.

### 서버 다시 시작 {#restart-the-server}

추가된 로케일을 적용하려면 AEM 서버를 다시 시작합니다.

>[!NOTE]
>
> SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

## 스페인어 지원 추가용 샘플 라이브러리 {#sample-libraries-for-adding-support-for-spanish}

스페인어 지원 추가를 위한 샘플 클라이언트 라이브러리

[파일 가져오기](assets/sample.zip)
