---
title: 문자 세트 변경
seo-title: 문자 세트 변경
description: 출력 스트림을 인코딩하는 데 사용되는 문자 세트를 지정할 수 있습니다. 문자 집합을 변경하는 방법을 알아봅니다.
seo-description: 출력 스트림을 인코딩하는 데 사용되는 문자 세트를 지정할 수 있습니다. 문자 집합을 변경하는 방법을 알아봅니다.
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---

# 문자 집합 {#change-the-character-set} 변경

출력 스트림을 인코딩하는 데 사용되는 문자 세트를 지정할 수 있습니다.

1. 관리 콘솔에서 **[!UICONTROL 서비스 > output]**&#x200B;을 클릭합니다.
1. 국제화에서 문자 집합 목록에서 문자 집합을 선택합니다. 이 설정은 API를 통해 지정된 `TransformationFormat` 및 `PrintFormat`에 따라 다릅니다. 나열된 문자 세트가 아닌 문자 집합을 지정하려면 [사용자 지정]을 선택하고 표시되는 상자에 인코딩 값을 지정합니다.

   `TransformationFormat`이 PDF이고 PDF/A 또는 `PrintFormat`이 PCL, PostScript, Zebra 레이블, IPL, DPL, TPCL, GenericColorPCL 또는 GenericPSLevel3이면 특정 문자 집합만 지원됩니다.

   문자 집합은 유효한 정식 이름이어야 합니다. 기본값은 ISO-8859-1입니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
