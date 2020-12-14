---
title: 새로운 렌더링 및 제출 서비스
seo-title: 새로운 렌더링 및 제출 서비스
description: 액세스한 장치에 따라 XDP 양식을 HTML 또는 PDF로 렌더링하려면 워크벤치에서 렌더링 및 제출 서비스를 정의합니다.
seo-description: 액세스한 장치에 따라 XDP 양식을 HTML 또는 PDF로 렌더링하려면 워크벤치에서 렌더링 및 제출 서비스를 정의합니다.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---


# 새 렌더링 및 전송 서비스{#new-render-and-submit-service}

## 소개 {#introduction}

워크벤치에서 `AssignTask` 작업을 정의할 때 특정 양식(XDP 또는 PDF 양식)을 지정합니다. 또한 작업 프로필을 통해 렌더링 및 제출 서비스 세트를 지정합니다.

XDP를 PDF 양식 또는 HTML 양식으로 렌더링할 수 있습니다. 새로운 기능에는 다음과 같은 기능이 포함됩니다.

* XDP 양식을 HTML로 렌더링 및 제출
* 데스크탑에서 XDP 양식을 PDF로 렌더링하고 전송할 뿐만 아니라 모바일 디바이스에서 HTML로 전송(예: iPad)

### 새 HTML Forms 서비스 {#new-html-forms-service}

새로운 HTML Forms 서비스는 Forms의 새로운 기능을 활용하여 XDP 양식의 HTML 렌더링을 지원합니다. 새 HTML Forms 서비스는 다음 메서드를 노출합니다.

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

모바일 양식 프로필에 대한 자세한 내용은 [사용자 지정 프로필 만들기](/help/forms/using/custom-profile.md)를 참조하십시오.

## 새 HTML 양식 렌더링 및 제출 프로세스 {#new-html-form-render-amp-submit-processes}

모든 &#39;AssignTask&#39; 작업에 대해 Render 및 Submit 프로세스를 양식에서 지정합니다. 이러한 프로세스는 사용자 지정 처리를 허용하도록 TaskManager `renderForm`및 `submitForm`API에서 호출됩니다. 새 HTML 양식에 대한 이러한 프로세스의 의미 체계:

### 새 HTML 양식 {#render-a-new-html-form} 렌더링

모든 렌더링 프로세스와 마찬가지로 HTML을 렌더링하는 새로운 프로세스에는 다음과 같은 입출력 매개 변수가 있습니다.

입력 - `taskContext`

출력 - `runtimeMap`

출력 - `outFormDoc`

이 메서드는 NewHTMLFormsService의 `renderHTMLForm` API의 정확한 동작을 시뮬레이션합니다. 양식의 HTML 변환에 대한 URL을 가져오려면 `generateFormURL` API를 호출합니다. 그런 다음 runtimeMap에 다음 키 또는 값을 채웁니다.

new html form = true

newHTMLFormURL = `generateFormURL` API를 호출한 후 반환된 URL입니다.

### 새 HTML 양식 {#submit-a-new-html-form} 제출

새 HTML 양식을 제출하는 이 프로세스는 다음 입출력 매개 변수와 함께 작동합니다.

입력 - `taskContext`

출력 - `runtimeMap`

출력 - `outputDocument`

이 프로세스는 `outputDocument`을 `taskContext`에서 읽어들인 `inputDocument`로 설정합니다.

## 기본 렌더링 또는 제출 프로세스 및 작업 프로필 {#default-render-or-submit-processes-and-action-profiles}

기본 렌더링 및 제출 서비스는 데스크탑에서 PDF 렌더링을 지원하고 모바일 장치(iPad)에서 HTML을 렌더링하는 지원을 제공합니다.

### 기본 렌더링 양식 {#default-render-form}

이 프로세스는 여러 플랫폼에 XDP 양식을 원활하게 렌더링합니다. 이 프로세스는 `taskContext`에서 사용자 에이전트를 검색하고 데이터를 사용하여 프로세스를 호출하여 HTML 또는 PDF를 렌더링합니다.

![default-render-form](assets/default-render-form.png)

### 기본 제출 양식 {#default-submit-form}

이 프로세스는 여러 플랫폼에 XDP 양식을 원활하게 제출합니다. `taskContext`에서 사용자 에이전트를 검색하고 데이터를 사용하여 프로세스를 호출하여 HTML 또는 PDF를 제출합니다.

![default-submit-form](assets/default-submit-form.png)

## 모바일 양식의 렌더링을 PDF에서 HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}으로 전환

브라우저는 Adobe Acrobat 및 Adobe Acrobat Reader용 플러그인을 포함하여 NPAPI 기반 플러그인에 대한 지원을 점차 철회하고 있습니다. 다음 단계에 따라 모바일 양식의 렌더링을 PDF에서 HTML로 변경할 수 있습니다.

1. Workbench에 유효한 사용자로 로그인합니다.
1. **파일** > **응용 프로그램 가져오기**&#x200B;를 선택합니다.

   애플리케이션 가져오기 대화 상자가 나타납니다.

1. 모바일 양식 렌더링을 변경할 애플리케이션을 선택하고 **확인**&#x200B;을 클릭합니다.
1. 렌더링을 변경할 프로세스를 엽니다.
1. 대상 시작 지점/작업을 열고 프레젠테이션 및 데이터 섹션으로 이동한 다음 **작업 프로필 관리**&#x200B;를 클릭합니다.

   작업 프로필 관리 대화 상자가 나타납니다.
1. 기본 렌더링 프로필 구성을 PDF에서 HTML로 변경하고 **확인**&#x200B;을 클릭합니다.
1. 프로세스를 확인합니다.
1. 다른 프로세스에 대한 렌더링을 변경하려면 단계를 반복합니다.
1. 변경한 프로세스와 관련된 응용 프로그램을 배포합니다.

### 기본 작업 프로필 {#default-action-profile}

기본 작업 프로필은 XDP 양식을 PDF로 렌더링했습니다. 이제 이 동작이 기본 렌더링 양식 및 기본 제출 양식 프로세스를 사용하도록 변경되었습니다.

작업 프로파일에 대한 FAQ는 다음과 같습니다.

![gen_question_b_20](assets/gen_question_b_20.png) **어떤 렌더링/제출 프로세스를 즉시 사용할 수 있습니까?**

* 렌더링 안내서(안내선은 더 이상 사용되지 않음)
* 렌더링 양식 가이드
* PDF 양식 렌더링
* HTML 양식 렌더링
* 새 HTML 양식 렌더링(새로운 기능)
* 기본 렌더링 양식(새로운 기능)

등가 제출 프로세스

![gen_question_b_20](assets/gen_question_b_20.png) **어떤 작업 프로필을 즉시 사용할 수 있습니까?**

XDP Forms:

* 기본값(새로운 &#39;기본 렌더링/제출&#39; 프로세스를 사용하여 렌더링/제출)

![gen_question_b_20](assets/gen_question_b_20.png) **처리 디자이너가 양식을 장치의 HTML과 데스크탑의 PDF에서 렌더링할 수 있도록 하려면 어떻게 해야 합니까?**

아무것도... 기본 작업 프로필이 자동으로 선택되고 렌더링 모드도 자동으로 처리됩니다.

![gen_question_b_20](assets/gen_question_b_20.png) **양식을 데스크탑의 HTML로 렌더링하려면 어떻게 해야 합니까?**

사용자는 기본 프로파일에 대한 HTML 라디오 단추를 선택해야 합니다.

![gen_question_b_20](assets/gen_question_b_20.png) **기본 작업 프로필 동작 변경에 대한 업그레이드 영향이 있습니까?**

예. 기본 작업 프로필과 관련된 이전 렌더링 및 제출 서비스는 다르므로 기존 양식의 사용자 정의 서비스로 간주됩니다. **기본값 복원**&#x200B;을 클릭하면 기본 렌더링 및 제출 서비스가 대신 설정됩니다.

기존 PDF 양식 서비스를 수정하거나 사용자 정의 서비스(사용자 정의1)를 만든 경우, 이제 HTML 변환에 동일한 기능을 사용하려고 합니다. 새로운 렌더링 또는 전송 서비스(예: custom2)를 복제하고 이와 유사한 사용자 지정을 적용해야 합니다. 이제 렌더링이나 제출을 위한 custom1 대신 custom2 services 사용을 시작하려면 XDP에 대한 작업 프로필을 수정합니다.

처리 디자이너가 장치의 HTML 및 데스크탑의 PDF에서 양식을 렌더링할 수 있도록 하려면 어떻게 해야 합니까?
처리 디자이너가 장치의 HTML 및 데스크탑의 PDF에서 양식을 렌더링할 수 있도록 하려면 어떻게 해야 합니까?
