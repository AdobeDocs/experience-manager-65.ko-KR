---
title: 중복 에셋 감지 활성화
description: AEM 파섹
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# 중복 에셋 감지 활성화 {#enable-detection-of-duplicate-assets}

AEM(Adobe Experience Manager) 자산에 있는 자산을 업로드하려고 하면 중복 감지 기능이 이를 중복으로 식별합니다. 기본적으로 중복 감지는 비활성화됩니다. 이 기능을 활성화하려면 다음 단계를 수행하십시오.

1. 액세스하여 AEM 웹 콘솔 구성 페이지를 엽니다 `https://[aem_server]:[port]/system/console/configMgr`.
1. servlet Day CQ DAM 자산 **[!UICONTROL 생성 구성]**&#x200B;편집
1. 복제 **[!UICONTROL 검색]** 옵션을 선택하고 저장을 **[!UICONTROL 클릭합니다]**.

   ![서블릿에서 중복 검색 옵션을 선택합니다.](assets/chlimage_1-377.png)

   *그림:서블릿에서 중복 검색 옵션을 선택합니다.*

이제 AEM 자산에서 중복 검색 기능이 활성화됩니다. 사용자가 AEM에 있는 자산을 업로드하려고 하면 시스템에서 충돌이 있는지 확인하고 이를 표시합니다. 자산은 에 저장된 SHA-1 해시를 사용하여 식별되므로 `jcr:content/metadata/dam:sha1`파일 이름에 관계없이 중복된 자산이 검색됩니다.

>[!MORELIKETHIS]
>
>* [기존 저장소의 자산 복제(커뮤니티 구성원의 자습서)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

