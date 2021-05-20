---
title: 양식 라이브러리 항목에 사용자 지정 작업 추가
seo-title: 양식 라이브러리 항목에 사용자 지정 작업 추가
description: 양식 개발자는 forms 포털 페이지의 양식 목록에 추가 작업을 추가할 수 있습니다. 기본적으로 양식 목록을 사용하면 양식에 액세스하여 작성하고 제출할 수 있습니다.
seo-description: 양식 개발자는 forms 포털 페이지의 양식 목록에 추가 작업을 추가할 수 있습니다. 기본적으로 양식 목록을 사용하면 양식에 액세스하여 작성하고 제출할 수 있습니다.
uuid: 5703ba27-7fb8-482e-b933-a060574165dc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: c34dd4c2-5fff-4355-b86d-cc8a956dd8af
docset: aem65
exl-id: 7c2a91c8-9b68-4491-88e2-f7ea68f5a79f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 양식 라이브러리 항목에 사용자 지정 작업 추가{#adding-custom-action-on-form-lister-items}

AEM Forms에서 사용 가능한 양식을 나열하는 포털 페이지를 만들 수 있습니다. 기본적으로 포털 페이지에서 양식을 검색하고 나열할 수 있습니다. 양식을 열어 정보를 작성하고 제출할 수 있습니다. 포털 페이지에 나열된 양식에 대해 렌더링 작업만 즉시 제공됩니다. 포털 페이지에서 사용 가능한 작업에 대해 자세히 알려면 [양식 포털 페이지 만들기](../../forms/using/creating-form-portal-page.md) 를 참조하십시오.

포털 페이지에 다른 옵션을 추가할 수 있습니다. Forms 포털의 템플릿을 사용자 지정하여 이러한 옵션 또는 작업을 사용자 지정할 수 있습니다.

이 문서에서는 Forms 포털 페이지에서 직접 양식 링크를 전송하는 단추를 만드는 방법을 소개합니다. 이 사용자 지정을 사용하려면 Search &amp; Lister 구성 요소에 대한 템플릿을 업데이트해야 합니다.

템플릿에 작업을 추가하는 데 필요한 코드는 아래에서 사용할 수 있습니다. 코드 조각에 있는 `onclick` 속성에는 이메일을 통해 양식 링크를 전송하는 스크립트가 있습니다.

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

사용자 지정 템플릿에 유사한 작업을 추가할 수 있습니다. JavaScript 함수를 정의하려면 페이지 수준 스크립트에서 함수를 추가하고 필수 HTML 요소와 연결합니다. 위의 예에서 `onclick` 표현식은 연결된 함수입니다.

템플릿을 편집한 후 샘플 포털 페이지에는 아래와 같이 이메일을 통해 양식 링크를 전송하는 버튼이 포함되어 있습니다.

![email](assets/email.png)
