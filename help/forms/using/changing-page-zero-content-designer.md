---
title: 디자이너의 페이지 제로 컨텐츠 변경
seo-title: 디자이너의 페이지 제로 컨텐츠 변경
description: Adobe가 아닌 PDF 뷰어에서 XFA PDF를 볼 때 XFA PDF의 페이지 0에 표시되는 메시지를 어떻게 변경할 수 있는지 알고 계십니까?
seo-description: Adobe가 아닌 PDF 뷰어에서 XFA PDF를 볼 때 XFA PDF의 페이지 0에 표시되는 메시지를 어떻게 변경할 수 있는지 알고 계십니까?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
translation-type: tm+mt
source-git-commit: f778f8f6acf5f091465b8ec6a0b94bd30758e082

---


# 디자이너의 페이지 제로 컨텐츠 변경{#changing-page-zero-content-in-designer}

Chrome 또는 Firefox의 기본 PDF 뷰어와 같이 Adobe가 아닌 뷰어가 PDF/XFA 양식의 컨텐츠를 읽을 수 없을 때 기본적으로 페이지 제로 컨텐츠가 표시됩니다. 기본 페이지 제로 메시지는 아래에 표시됩니다.

![defaultpage0message](assets/defaultpage0message.png)

AEM Forms Feature Pack 1 버전의 Designer를 사용하면 페이지 0에 표시되는 메시지를 변경할 수 있습니다. 페이지 제로 메시지를 변경하려면 다음 단계를 수행하십시오.

1. AEM Forms Feature Pack 1 버전의 Designer가 설치되어 있는지 확인합니다. 디자이너의 정보 화면에서 버전을 확인할 수 있습니다.

1. 페이지 제로 컨텐츠를 변경할 양식을 엽니다.

1. 파일 **> 양식 속성을 클릭합니다**.

1. 양식 속성 대화 상자에서 ![더하기](assets/plus.png) (더하기 아이콘)를 클릭하여 사용자 지정 속성을 추가합니다.

1. 속성 이름으로 **_pagezerocontent** 를 지정합니다.
1. 새 페이지 제로 메시지를 리치 텍스트 형식으로 값으로 추가합니다. 예:

   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. 양식을 PDF로 저장합니다.

1. 브라우저에서 PDF 양식을 보고 메시지가 업데이트되었는지 확인합니다. 위의 예제 값은 다음과 같이 나타납니다.

   ![변경 메시지](assets/changedmessage.png)

>[!NOTE]
>
>양식을 다시 열면 방금 만든 사용자 지정 속성이 양식 속성 대화 상자에 제대로 표시되지 않을 수 있습니다. 하지만 제대로 작동하며 업데이트된 페이지 제로 메시지가 표시됩니다.

