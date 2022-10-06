---
title: 중복 자산 탐지 활성화
description: Experience Manager에서 중복 자산을 탐지할 수 있는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 중복 자산 탐지 활성화 {#enable-detection-of-duplicate-assets}

에 있는 자산을 업로드하려고 하는 경우 [!DNL Adobe Experience Manager Assets]를 지정하면, 중복 감지 기능이 이를 중복으로 식별합니다. 중복 감지는 기본적으로 비활성화되어 있습니다. 이 기능을 활성화하려면 다음 단계를 수행하십시오.

1. 를 엽니다. [!DNL Experience Manager] 웹 콘솔 구성 페이지에 액세스하여 `https://[aem_server]:[port]/system/console/configMgr`.
1. 서블릿에 대한 구성 편집 **[!UICONTROL Day CQ DAM 자산 만들기]**.
1. 을(를) 선택합니다 **[!UICONTROL 중복 검색]** 옵션을 선택하고 **[!UICONTROL 저장]**.

   ![서블릿에서 중복 감지 옵션을 선택합니다](assets/chlimage_1-377.png)

   *그림: 서블릿에서 중복 감지 옵션을 선택합니다.*

이제 중복 검색 기능이에서 활성화됩니다. [!DNL Assets]. 사용자가 에 있는 자산을 업로드하려고 할 때 [!DNL Experience Manager]과 같은 방식으로 설정되면 시스템에서 충돌이 있는지 확인하고 이를 표시합니다. 자산은 에 저장된 SHA-1 해시를 사용하여 식별됩니다 `jcr:content/metadata/dam:sha1`- 파일 이름과 관계없이 중복 자산이 검색됩니다.

>[!MORELIKETHIS]
>
>* [기존 저장소의 중복된 자산(커뮤니티 구성원의 자습서)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

