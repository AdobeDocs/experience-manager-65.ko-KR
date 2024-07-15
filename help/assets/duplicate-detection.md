---
title: 중복 에셋 감지 활성화
description: Experience Manager에서 중복 에셋을 탐지하는 방법을 알아봅니다.
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 중복 에셋 감지 활성화 {#enable-detection-of-duplicate-assets}

[!DNL Adobe Experience Manager Assets]에 있는 에셋을 업로드하려고 하면 중복 검색 기능이 중복으로 식별됩니다. 중복 검색은 기본적으로 비활성화되어 있습니다. 이 기능을 활성화하려면 다음 단계를 수행하십시오.

1. `https://[aem_server]:[port]/system/console/configMgr`에 액세스하여 [!DNL Experience Manager] 웹 콘솔 구성 페이지를 엽니다.
1. 서블릿 **[!UICONTROL 일 CQ DAM 자산 만들기]**&#x200B;에 대한 구성을 편집합니다.
1. **[!UICONTROL 중복 검색]** 옵션을 선택하고 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

   ![서블릿에서 중복 감지 옵션을 선택합니다](assets/chlimage_1-377.png)

   *그림: 서블릿에서 중복 검색 옵션을 선택합니다.*

이제 중복 검색 기능을 [!DNL Assets]에서 사용할 수 있습니다. 사용자가 [!DNL Experience Manager]에 있는 에셋을 업로드하려고 하면 시스템에서 충돌을 확인하고 표시합니다. 자산은 `jcr:content/metadata/dam:sha1`에 저장된 SHA-1 해시를 사용하여 식별됩니다. 즉, 파일 이름과 관계없이 중복 자산이 검색됩니다.

>[!MORELIKETHIS]
>
>* [기존 저장소의 자산을 복제합니다(커뮤니티 멤버의 자습서)](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [AEM as a Cloud Service에서 중복 에셋 감지](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html)
