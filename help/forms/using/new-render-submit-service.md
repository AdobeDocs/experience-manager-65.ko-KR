---
title: 새로운 렌더링 및 제출 서비스
description: Workbench에서 렌더링 및 제출 서비스를 정의하여 액세스하는 디바이스에 따라 XDP 양식을 HTML 또는 PDF으로 렌더링합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# 새로운 렌더링 및 제출 서비스{#new-render-and-submit-service}

## 소개 {#introduction}

Workbench에서 다음을 정의할 때 `AssignTask` 작업을 수행하려면 특정 양식(XDP 또는 PDF 양식)을 지정하십시오. 또한 작업 프로필을 통해 렌더링 및 제출 서비스 세트를 지정합니다.

XDP를 PDF 양식 또는 HTML 양식으로 렌더링할 수 있습니다. 새로운 기능에는 다음과 같은 기능이 포함됩니다.

* XDP 양식을 HTML으로 렌더링 및 제출
* XDP 양식을 데스크톱에서 PDF으로, 모바일 장치에서 HTML으로 렌더링 및 제출(예: iPad)

### 새로운 HTML Forms 서비스 {#new-html-forms-service}

새로운 HTML Forms 서비스는 Forms의 새로운 기능을 사용하여 XDP 양식을 HTML으로 렌더링할 수 있도록 지원합니다. 새 HTML Forms 서비스는 다음 메서드를 노출합니다.

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

모바일 양식 프로필에 대한 자세한 내용은 다음에서 확인하십시오. [사용자 지정 프로필 만들기](/help/forms/using/custom-profile.md).

## 새 HTML 양식 렌더링 및 제출 프로세스 {#new-html-form-render-amp-submit-processes}

모든 &#39;AssignTask&#39; 작업에 대해 양식으로 렌더링 및 제출 프로세스를 지정합니다. 이러한 프로세스는 TaskManager에 의해 호출됩니다. `renderForm`및 `submitForm`사용자 지정 처리를 허용하는 API입니다. 새 HTML 양식에 대한 이러한 프로세스의 의미:

### 새 HTML 양식 렌더링 {#render-a-new-html-form}

모든 렌더링 프로세스와 마찬가지로 HTML을 렌더링할 새 프로세스에는 다음과 같은 I/O 매개 변수가 있습니다.

입력 - `taskContext`

출력 - `runtimeMap`

출력 - `outFormDoc`

이 메서드는 의 정확한 동작을 시뮬레이션합니다. `renderHTMLForm` NewHTMLFormsService의 API입니다. 다음을 호출합니다. `generateFormURL` 양식의 HTML 표현물 URL을 가져오기 위한 API입니다. 그런 다음 runtimeMap을 다음 키 또는 값으로 채웁니다.

새 html 양식 = true

newHTMLFormURL = 호출 후 반환된 URL `generateFormURL` API.

### 새 HTML 양식 제출 {#submit-a-new-html-form}

새 HTML 양식을 제출하는 이 프로세스는 다음 I/O 매개 변수와 함께 작동합니다.

입력 - `taskContext`

출력 - `runtimeMap`

출력 - `outputDocument`

이 프로세스는 `outputDocument`(으)로 `inputDocument`에서 검색됨 `taskContext`.

## 기본 렌더링 또는 제출 프로세스 및 작업 프로필 {#default-render-or-submit-processes-and-action-profiles}

기본 Render 및 Submit 서비스를 사용하면 데스크탑에서 PDF을 렌더링하고 모바일 장치(iPad)에서 HTML을 지원할 수 있습니다.

### 기본 렌더링 양식 {#default-render-form}

이 프로세스는 여러 플랫폼에서 XDP 양식을 원활하게 렌더링합니다. 이 프로세스는에서 사용자 에이전트를 검색합니다. `taskContext`, 및 는 데이터를 사용하여 HTML 또는 PDF을 렌더링하는 프로세스를 호출합니다.

![default-render-form](assets/default-render-form.png)

### 기본 제출 양식 {#default-submit-form}

이 프로세스는 여러 플랫폼에서 XDP 양식을 원활하게 제출합니다. 에서 사용자 에이전트를 검색합니다. `taskContext`및 는 데이터를 사용하여 프로세스를 호출하여 HTML 또는 PDF을 제출합니다.

![default-submit-form](assets/default-submit-form.png)

## 모바일 양식의 렌더링을 PDF에서 HTML으로 전환 {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

브라우저에서는 Adobe Acrobat 및 Adobe Acrobat Reader용 플러그인을 포함하여 NPAPI 기반 플러그인에 대한 지원을 점차 중단하고 있습니다. 다음 단계를 사용하여 모바일 양식의 렌더링을 PDF에서 HTML으로 변경할 수 있습니다.

1. Workbench에 유효한 사용자로 로그인합니다.
1. 선택 **파일** > **애플리케이션 가져오기**.

   응용 프로그램 가져오기 대화 상자가 나타납니다.

1. 모바일 양식 렌더링을 변경할 응용 프로그램을 선택하고 을 클릭합니다 **확인**.
1. 렌더링을 변경할 프로세스를 엽니다.
1. 타깃팅된 시작 지점/작업을 열고 프레젠테이션 및 데이터 섹션으로 이동한 다음 **작업 프로필 관리**.

   [작업 프로필 관리] 대화 상자가 나타납니다.
1. 기본 렌더링 프로필 구성을 PDF에서 HTML으로 변경하고 **확인**.
1. 프로세스를 확인합니다.
1. 다른 프로세스에 대한 렌더링을 변경하려면 단계를 반복합니다.
1. 변경한 프로세스와 관련된 애플리케이션을 배포합니다.

### 기본 작업 프로필 {#default-action-profile}

기본 작업 프로필에서 XDP Form을 PDF으로 렌더링했습니다. 이 동작은 이제 기본 렌더링 양식 및 기본 제출 양식 프로세스를 사용하도록 변경되었습니다.

작업 프로필에 대한 몇 가지 FAQ는 다음과 같습니다.

![gen_question_b_20](assets/gen_question_b_20.png) **즉시 사용할 수 있는 렌더링/제출 프로세스는 무엇입니까?**

* 렌더링 안내서(안내서는 더 이상 사용되지 않음)
* 렌더링 양식 안내서
* PDF 양식 렌더링
* HTML 양식 렌더링
* 새 HTML 양식 렌더링(신규)
* 기본 렌더링 양식(신규)

및 동등한 제출 프로세스도 포함됩니다.

![gen_question_b_20](assets/gen_question_b_20.png) **즉시 사용할 수 있는 작업 프로필은 무엇입니까?**

XDP Forms의 경우:

* 기본값(새로운 &#39;기본 렌더링/제출&#39; 프로세스를 사용하여 렌더링/제출)

![gen_question_b_20](assets/gen_question_b_20.png) **장치의 PDF과 데스크탑의 HTML에서 양식을 렌더링할 수 있도록 프로세스 디자이너가 수행해야 하는 작업은 무엇입니까?**

아무것도 아냐 기본 작업 프로필이 자동으로 선택되고 렌더링 모드도 자동으로 처리됩니다.

![gen_question_b_20](assets/gen_question_b_20.png) **데스크탑에서 HTML 시 양식을 렌더링하기 위해 수행해야 하는 작업은 무엇입니까?**

사용자는 기본 프로필에 대한 HTML 라디오 단추를 선택해야 합니다.

![gen_question_b_20](assets/gen_question_b_20.png) **업그레이드가 기본 작업 프로필 동작을 변경하는 데 영향을 줍니까?**

예. 기본 작업 프로필과 연결된 이전 렌더링 및 제출 서비스가 서로 다르므로 기존 양식의 사용자 지정으로 처리됩니다. 클릭 시 **기본값 복원**, 기본 렌더링 및 제출 서비스가 대신 설정됩니다.

기존 렌더링 또는 제출 PDF 양식 서비스를 수정했거나 사용자 정의 서비스(예: custom1)를 만든 경우 이제 HTML 렌디션에 동일한 기능을 사용하려는 경우 새 렌더링 또는 제출 서비스(예: custom2)를 복제하고 유사한 사용자 지정을 적용해야 합니다. 이제 렌더링 또는 제출을 위한 사용자 지정1 대신 사용자 지정2 서비스를 사용하도록 XDP에 대한 작업 프로필을 수정합니다.

장치의 PDF과 데스크탑의 HTML에서 양식을 렌더링할 수 있도록 프로세스 디자이너가 수행해야 하는 작업은 무엇입니까?
장치의 PDF과 데스크탑의 HTML에서 양식을 렌더링할 수 있도록 프로세스 디자이너가 수행해야 하는 작업은 무엇입니까?
