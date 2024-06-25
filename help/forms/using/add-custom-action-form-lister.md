---
title: 양식 목록 항목에 대한 사용자 지정 작업 추가
description: 양식 개발자는 Forms 포털 페이지의 양식 목록에 더 많은 작업을 추가할 수 있습니다. 기본적으로 양식 목록을 사용하여 양식에 액세스하고 양식을 입력한 다음 제출할 수 있습니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 양식 목록 항목에 대한 사용자 지정 작업 추가{#adding-custom-action-on-form-lister-items}

AEM Forms에서 사용 가능한 양식을 나열하는 포털 페이지를 만들 수 있습니다. 기본적으로 포털 페이지에서 양식을 검색하고 나열할 수 있습니다. 작성을 위한 양식을 열고 정보를 제출할 수 있습니다. 포털 페이지에 나열된 양식에 대해 즉시 렌더링 작업만 제공됩니다. 포털 페이지에서 사용할 수 있는 작업에 대해 자세히 알아보려면 다음을 참조하십시오. [Forms 포털 페이지 만들기](../../forms/using/creating-form-portal-page.md).

포털 페이지에 다른 옵션을 추가할 수 있습니다. 양식 포털의 템플릿을 사용자 지정하여 이러한 옵션 또는 작업을 사용자 지정할 수 있습니다.

이 문서에서는 Forms 포털 페이지에서 직접 양식 링크를 보내는 단추를 만드는 방법을 보여 줍니다. 이 사용자 지정을 사용하려면 검색 및 목록 구성 요소에 대한 템플릿을 업데이트해야 합니다.

템플릿에 작업을 추가하는 데 필요한 코드는 아래에서 확인할 수 있습니다. 다음 `onclick` 코드 조각의 속성에는 전자 메일을 통해 양식 링크를 전송하는 스크립트가 있습니다.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

사용자 지정 템플릿에 유사한 작업을 추가할 수 있습니다. JavaScript 함수를 정의하려면 페이지 수준 스크립트에 함수를 추가하고 필요한 HTML 요소와 연결합니다. 위의 예에서 `onclick` expression은 연결된 함수입니다.

템플릿을 편집한 후에는 아래 표시된 대로 샘플 포털 페이지에 양식을 이메일로 전송하는 버튼이 포함되어 있습니다.

![이메일](assets/email.png)
