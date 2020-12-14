---
title: 문자 세트 변경
seo-title: 문자 세트 변경
description: 출력 스트림을 인코딩하는 데 사용되는 문자 집합을 지정할 수 있습니다. 문자 집합을 변경할 수 있는 방법을 알아봅니다.
seo-description: 출력 스트림을 인코딩하는 데 사용되는 문자 집합을 지정할 수 있습니다. 문자 집합을 변경할 수 있는 방법을 알아봅니다.
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---


# 문자 세트 {#change-the-character-set} 변경

출력 스트림을 인코딩하는 데 사용되는 문자 집합을 지정할 수 있습니다.

1. 관리 콘솔에서 **[!UICONTROL 서비스 > 출력]**&#x200B;을 클릭합니다.
1. 국제화의 문자 집합 목록에서 문자 집합을 선택합니다. 이 설정은 API를 통해 지정된 `TransformationFormat` 및 `PrintFormat`에 따라 달라집니다. 나열된 문자 집합 이외의 문자 집합을 지정하려면 [사용자 정의]를 선택하고 표시되는 상자에 인코딩 값을 지정합니다.

   `TransformationFormat`이 PDF 및 PDF/A 또는 `PrintFormat`이면 PCL, PostScript, Zebra 레이블, IPL, DPL, TPCL, GenericColorPCL 또는 GenericPSLevel3이 지원됩니다.

   문자 집합은 유효한 정식 이름이어야 합니다. 기본값은 ISO-8859-1입니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

