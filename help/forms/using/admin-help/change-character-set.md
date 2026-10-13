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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
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
