---
title: 중복 에셋 감지 사용
description: Experience Manager에서 중복된 자산을 검색하는 방법을 알아봅니다.
contentOwner: AG
role: 비즈니스 전문가, 관리자
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# 중복된 자산 감지 활성화 {#enable-detection-of-duplicate-assets}

[!DNL Adobe Experience Manager Assets]에 있는 자산을 업로드하려고 하면 중복 감지 기능이 이를 중복으로 식별합니다. 중복 감지는 기본적으로 비활성화됩니다. 이 기능을 활성화하려면 다음 단계를 수행합니다.

1. `https://[aem_server]:[port]/system/console/configMgr`에 액세스하여 [!DNL Experience Manager] 웹 콘솔 구성 페이지를 엽니다.
1. **[!UICONTROL 일 CQ DAM 자산 만들기]** 서블릿에 대한 구성을 편집합니다.
1. **[!UICONTROL 중복]** 검색 옵션을 선택하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

   ![서블릿에서 중복 검색 옵션을 선택합니다.](assets/chlimage_1-377.png)

   *그림:서블릿에서 중복 검색 옵션을 선택합니다.*

이제 중복 검색 기능이 [!DNL Assets]에서 활성화됩니다. 사용자가 [!DNL Experience Manager]에 있는 에셋을 업로드하려고 하면 시스템에서 충돌이 있는지 확인하고 이를 표시합니다. 자산은 `jcr:content/metadata/dam:sha1`에 저장된 SHA-1 해시를 사용하여 식별되므로 파일 이름에 관계없이 중복된 자산이 검색됩니다.

>[!MORELIKETHIS]
>
>* [기존 저장소에 자산 복제(커뮤니티 구성원이 제공하는 자습서)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

