---
title: 중복 에셋 감지 활성화
description: Experience Manager에서 중복 에셋을 탐지하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 중복 에셋 감지 활성화 {#enable-detection-of-duplicate-assets}

에 있는 에셋을 업로드하려는 경우 [!DNL Adobe Experience Manager Assets], 중복 감지 기능은 중복으로 식별합니다. 중복 검색은 기본적으로 비활성화되어 있습니다. 이 기능을 활성화하려면 다음 단계를 수행하십시오.

1. 를 엽니다. [!DNL Experience Manager] 에 액세스하여 웹 콘솔 구성 페이지 `https://[aem_server]:[port]/system/console/configMgr`.
1. 서블릿에 대한 구성 편집 **[!UICONTROL 일별 CQ DAM 자산 만들기]**.
1. 다음 항목 선택 **[!UICONTROL 중복 감지]** 옵션 및 클릭 **[!UICONTROL 저장]**.

   ![서블릿에서 중복 감지 옵션을 선택합니다.](assets/chlimage_1-377.png)

   *그림: 서블릿에서 중복 감지 옵션을 선택합니다.*

이제 중복 감지 기능이 다음에서 활성화됩니다. [!DNL Assets]. 사용자가 에셋이에 있는 에셋을 업로드하려고 할 때 [!DNL Experience Manager]에서 시스템이 충돌을 확인하고 충돌을 나타냅니다. 자산은에 저장된 SHA-1 해시를 사용하여 식별됩니다. `jcr:content/metadata/dam:sha1`: 파일 이름과 관계없이 중복 에셋이 검색됨을 의미합니다.

>[!MORELIKETHIS]
>
>* [기존 저장소의 자산 복제(커뮤니티 구성원의 튜토리얼)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

