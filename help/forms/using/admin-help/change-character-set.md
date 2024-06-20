---
title: 문자 집합 변경
description: 출력 스트림을 인코딩하는 데 사용되는 문자 집합을 지정할 수 있습니다. 문자 집합을 변경하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 1%

---

# 문자 집합 변경 {#change-the-character-set}

출력 스트림을 인코딩하는 데 사용되는 문자 집합을 지정할 수 있습니다.

1. 관리 콘솔에서 다음을 클릭합니다. **[!UICONTROL 서비스 > 출력]**.
1. 국제화 아래의 문자 집합 목록에서 문자 집합을 선택합니다. 이 설정은 `TransformationFormat` 및 `PrintFormat` API를 통해 지정됩니다. 나열된 문자 세트 이외의 문자 세트를 지정하려면 사용자 정의를 선택하고 표시되는 상자에서 인코딩 값을 지정합니다.

   If `TransformationFormat` 은(는) PDF 및 PDF/A 또는 `PrintFormat` 은(는) PCL, PostScript, Zebra 레이블, IPL, DPL, TPCL, GenericColorPCL 또는 GenericPSLevel3이며, 특정 문자 집합만 지원됩니다.

   문자 집합은 유효한 정식 이름이어야 합니다. 기본값은 ISO-8859-1입니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
