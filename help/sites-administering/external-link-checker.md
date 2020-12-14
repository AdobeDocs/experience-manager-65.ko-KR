---
title: 외부 링크 검사기
seo-title: 외부 링크 검사기
description: AEM의 외부 링크 검사기에 대해 알아봅니다.
seo-description: AEM의 외부 링크 검사기에 대해 알아봅니다.
uuid: 09160594-e45f-4604-8b36-f14b148b9f63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d1ccd194-8549-4188-8932-7136be1e88a2
docset: aem65
translation-type: tm+mt
source-git-commit: 0a94bf49a7136c5831c42eb274d07517c12014ec
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---


# 외부 링크 검사기{#the-external-link-checker}

AEM 내에서 외부 링크 검사기가 제공됩니다. 링크 검사기:

* 모든 컨텐츠 페이지 스캔
* 모든 유효한 및 잘못된 링크 목록을 생성합니다.
* 개별 컨텐츠 페이지에서 잘못된 링크가 sites에서 끊어진 것으로 표시

## 외부 링크 유효성 검사 방법 {#how-to-validate-external-links}

외부 링크 검사기를 사용하려면:

1. **내비게이션**&#x200B;을 사용하여 **도구**&#x200B;를 선택한 다음 **사이트**&#x200B;를 선택합니다.
1. **외부 링크 검사기**&#x200B;를 선택하면 모든 외부 링크 목록이 생성됩니다.
1. 목록에서 링크를 선택한 다음 **확인**&#x200B;을 클릭하여 특정 링크의 유효성을 확인합니다.

   ![](assets/telc-01.png)

   정보가 표시됩니다.

   * **링크** 상태
   * **URL**
   * **레퍼러**
   * 링크가 **마지막으로 확인된 날짜**(유효함) 이후 시간
   * **마지막 상태**&#x200B;이(가) 반환되었습니다.

   * 링크가 **마지막으로 사용 가능한 시간**
   * 링크가 **마지막으로 액세스한 시간**

1. 개별 컨텐츠 페이지에서 잘못된 링크가 끊어진 것으로 표시됩니다.

   ![](assets/chlimage_1-143.png)