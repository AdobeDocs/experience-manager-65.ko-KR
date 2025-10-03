---
title: 문자 세트 변경
description: 출력 스트림을 인코딩하는 데 사용되는 문자 세트를 지정할 수 있습니다. 문자 세트를 변경하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9ff75d98-54ad-425d-912f-d5a7501bf564
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '144'
ht-degree: 100%

---

# 문자 세트 변경 {#change-the-character-set}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

출력 스트림을 인코딩하는 데 사용되는 문자 세트를 지정할 수 있습니다.

1. 관리 콘솔에서 **[!UICONTROL 서비스 > Output]**&#x200B;을 클릭합니다.
1. 국제화의 문자 세트 목록에서 문자 세트를 선택합니다. 이 설정은 API를 통해 지정된 `TransformationFormat` 및 `PrintFormat`에 따라 달라집니다. 나열된 문자 세트 외의 다른 문자 세트를 지정하려면 사용자 정의를 선택하고 표시되는 상자에서 인코딩 값을 지정합니다.

   `TransformationFormat`이 PDF 및 PDF/A이거나 `PrintFormat`이 PCL, PostScript, Zebra 레이블, IPL, DPL, TPCL, GenericColorPCL 또는 GenericPSLevel3인 경우 특정 문자 세트만 지원됩니다.

   문자 세트는 유효한 정식 이름이어야 합니다. 기본값은 ISO-8859-1입니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.
