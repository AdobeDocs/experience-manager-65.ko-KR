---
title: 새로운 렌더링 및 제출 서비스
seo-title: 새로운 렌더링 및 제출 서비스
description: 액세스 장치에 따라 XDP 양식을 HTML 또는 PDF로 렌더링하려면 Workbench에서 렌더링 및 제출 서비스를 정의합니다.
seo-description: 액세스 장치에 따라 XDP 양식을 HTML 또는 PDF로 렌더링하려면 Workbench에서 렌더링 및 제출 서비스를 정의합니다.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---

# 새 렌더링 및 제출 서비스{#new-render-and-submit-service}

## 소개 {#introduction}

Workbench에서 `AssignTask` 작업을 정의할 때 특정 양식(XDP 또는 PDF 양식)을 지정합니다. 또한 작업 프로필을 통해 렌더링 및 제출 서비스 세트를 지정합니다.

XDP를 PDF 양식 또는 HTML 양식으로 렌더링할 수 있습니다. 새로운 기능에는 다음과 같은 기능이 포함됩니다.

* XDP 양식을 HTML로 렌더링 및 제출
* XDP 양식을 데스크탑에서 PDF로 렌더링하고 제출하고 모바일 장치에서 HTML로 제출(예: iPad)

### 새 HTML Forms 서비스 {#new-html-forms-service}

새 HTML Forms 서비스는 Forms의 새로운 기능을 활용하여 XDP 양식의 HTML 렌더링을 지원합니다. 새 HTML Forms 서비스는 다음 메서드를 노출합니다.

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

모바일 양식 프로필에 대한 자세한 내용은 [사용자 지정 프로필 만들기](/help/forms/using/custom-profile.md)에서 확인할 수 있습니다.

## 새 HTML 양식 렌더링 및 제출 프로세스 {#new-html-form-render-amp-submit-processes}

모든 &#39;AssignTask&#39; 작업에 대해 양식을 사용하여 Render 및 Submit 프로세스를 지정합니다. 이러한 프로세스는 TaskManager `renderForm` 및 `submitForm`API에서 호출되어 사용자 지정 처리를 허용합니다. 새 HTML 양식에 대해 다음 프로세스의 의미 체계:

### 새 HTML 양식 {#render-a-new-html-form} 렌더링

모든 렌더링 프로세스와 마찬가지로 HTML을 렌더링하는 새 프로세스에는 다음과 같은 I/O 매개 변수가 있습니다.

입력 - `taskContext`

출력 - `runtimeMap`

출력 - `outFormDoc`

이 메서드는 NewHTMLFormsService의 `renderHTMLForm` API의 정확한 동작을 시뮬레이션합니다. 양식의 HTML 표현물에 대한 URL을 가져오려면 `generateFormURL` API를 호출하십시오. 그런 다음 runtimeMap을 다음 키 또는 값으로 채웁니다.

새 html 양식 = true

newHTMLFormURL = `generateFormURL` API를 호출한 후 반환되는 URL입니다.

### 새 HTML 양식 {#submit-a-new-html-form} 제출

새 HTML 양식을 제출하는 이 프로세스는 다음 I/O 매개 변수와 함께 작동합니다.

입력 - `taskContext`

출력 - `runtimeMap`

출력 - `outputDocument`

이 프로세스는 `outputDocument`을 `taskContext`에서 검색한 `inputDocument`로 설정합니다.

## 기본 렌더링 또는 제출 프로세스 및 작업 프로필 {#default-render-or-submit-processes-and-action-profiles}

기본 렌더링 및 제출 서비스를 사용하면 데스크탑에서 PDF를 렌더링하고 모바일 장치에서 HTML(iPad)을 렌더링할 수 있습니다.

### 기본 렌더링 양식 {#default-render-form}

이 프로세스는 여러 플랫폼에서 XDP 양식을 원활하게 렌더링합니다. 프로세스는 `taskContext`에서 사용자 에이전트를 검색하고 데이터를 사용하여 HTML 또는 PDF를 렌더링합니다.

![default-render-form](assets/default-render-form.png)

### 기본 제출 양식 {#default-submit-form}

이 프로세스는 여러 플랫폼에서 XDP 양식을 원활하게 제출합니다. `taskContext`에서 사용자 에이전트를 검색하고 데이터를 사용하여 프로세스를 호출하여 HTML 또는 PDF를 제출합니다.

![기본 제출 양식](assets/default-submit-form.png)

## 모바일 양식의 렌더링을 PDF에서 HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}으로 전환합니다.

브라우저에서는 Adobe Acrobat 및 Adobe Acrobat Reader용 플러그인을 포함하여 NPAPI 기반 플러그인에 대한 지원을 점차 철회하고 있습니다. 다음 단계를 사용하여 모바일 양식의 렌더링을 PDF에서 HTML로 변경할 수 있습니다.

1. 유효한 사용자로 Workbench에 로그인합니다.
1. **파일** > **응용 프로그램 가져오기**&#x200B;를 선택합니다.

   응용 프로그램 가져오기 대화 상자가 나타납니다.

1. 모바일 양식 렌더링을 변경할 애플리케이션을 선택하고 **확인**&#x200B;을 클릭합니다.
1. 렌더링을 변경할 프로세스를 엽니다.
1. 타깃팅된 시작점/작업을 열고 프레젠테이션 및 데이터 섹션으로 이동한 다음 **작업 프로필 관리**&#x200B;를 클릭합니다.

   작업 프로필 관리 대화 상자가 나타납니다.
1. 기본 렌더링 프로필 구성을 PDF에서 HTML로 변경하고 **확인**&#x200B;을 클릭합니다.
1. 프로세스를 확인합니다.
1. 다른 프로세스에 대한 렌더링을 변경하려면 단계를 반복합니다.
1. 변경한 프로세스와 관련된 응용 프로그램을 배포합니다.

### 기본 작업 프로필 {#default-action-profile}

기본 작업 프로필이 XDP 양식을 PDF로 렌더링했습니다. 이제 이 동작은 기본 렌더링 양식 및 기본 제출 양식 프로세스를 사용하도록 변경되었습니다.

작업 프로필에 대한 몇 가지 FAQ는 다음과 같습니다.

![gen_question_b_20](assets/gen_question_b_20.png) **어떤 렌더링/제출 프로세스를 즉시 사용할 수 있습니까?**

* Render Guide(안내서는 더 이상 사용되지 않음)
* Render Form 안내서
* PDF 양식 렌더링
* HTML 양식 렌더링
* 새 HTML 양식 렌더링(신규)
* 기본 렌더링 양식(신규)

또한 동등한 제출 프로세스를 사용합니다.

![gen_question_b_20](assets/gen_question_b_20.png) **즉시 사용할 수 있는 작업 프로필은 무엇입니까?**

XDP Forms의 경우:

* 기본값(새 &#39;기본 렌더링/제출&#39; 프로세스를 사용하여 렌더링/제출)

![gen_question_b_20](assets/gen_question_b_20.png) **양식을 장치에서 HTML로 렌더링하고 데스크탑에서 PDF로 렌더링할 수 있도록 프로세스 디자이너가 수행해야 하는 작업**

아무것도 없어 기본 작업 프로필이 자동으로 선택되고 렌더링 모드도 자동으로 선택됩니다.

![gen_question_b_20](assets/gen_question_b_20.png) **양식을 데스크탑에서 HTML로 렌더링하려면 어떻게 해야 합니까?**

사용자는 기본 프로필에 대한 HTML 라디오 단추를 선택해야 합니다.

![gen_question_b_20](assets/gen_question_b_20.png) **기본 작업 프로필 동작 변경에 대한 업그레이드 영향이 있습니까?**

예. 기본 작업 프로필과 연결된 이전 렌더링 및 제출 서비스는 다르므로 기존 양식의 사용자 지정으로 처리됩니다. **기본값 복원**&#x200B;을 클릭하면 대신 기본 렌더링 및 제출 서비스가 설정됩니다.

기존 Render 또는 Submit PDF Form 서비스를 수정하거나 사용자 지정 서비스(예: custom1)를 만든 경우, 이제 HTML 표현물에 동일한 기능을 사용하려고 합니다. 새로운 렌더링 또는 제출 서비스(예: 사용자 지정2)를 복제하고 이와 유사한 사용자 지정을 적용해야 합니다. 이제 렌더링 또는 전송을 위해 custom1 대신 custom2 services를 사용하도록 XDP에 대한 작업 프로필을 수정합니다.

양식을 장치에서 HTML로 렌더링하고 데스크탑에서 PDF로 렌더링할 수 있도록 프로세스 디자이너가 수행해야 하는 작업은 무엇입니까?
양식을 장치에서 HTML로 렌더링하고 데스크탑에서 PDF로 렌더링할 수 있도록 프로세스 디자이너가 수행해야 하는 작업은 무엇입니까?
