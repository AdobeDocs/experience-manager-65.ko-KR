---
title: 중복 에셋 감지 사용
description: Adobe Experience Manager에서 중복된 자산을 검색하는 방법을 알아봅니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# 중복 에셋 감지 사용 {#enable-detection-of-duplicate-assets}

Adobe Experience Manager Assets에 있는 자산을 업로드하려고 하면 중복 검색 기능이 이를 중복으로 식별합니다. 중복 검색은 기본적으로 비활성화됩니다. 이 기능을 활성화하려면 다음 단계를 수행하십시오.

1. 액세스 권한을 통해 Experience Manager 웹 콘솔 구성 페이지를 엽니다 `https://[aem_server]:[port]/system/console/configMgr`.
1. 서블릿 Day CQ **[!UICONTROL DAM 자산 만들기에 대한 구성을 편집합니다]**.
1. 중복 **[!UICONTROL 검색]** 옵션을 선택하고 저장을 **[!UICONTROL 클릭합니다]**.

   ![서블릿에서 중복 검색 옵션을 선택합니다.](assets/chlimage_1-377.png)

   *그림: 서블릿에서 중복 검색 옵션을 선택합니다.*

이제 중복 검색 기능이 자산에서 활성화됩니다. 사용자가 Experience Manager에 있는 자산을 업로드하려고 하면 시스템에서 충돌을 확인하고 이를 표시합니다. 자산은 에 저장된 SHA-1 해시를 사용하여 식별되므로 파일 이름에 관계없이 중복된 자산 `jcr:content/metadata/dam:sha1`이 검색됩니다.

>[!MORELIKETHIS]
>
>* [기존 보관소의 에셋 복제(커뮤니티 멤버의 자습서)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

