---
title: 다국어 자산 및 자산 번역
description: 이진, 메타데이터 및 태그를 포함한 자산을 여러 언어로 번역하는 워크플로우를 자동화하는 방법을 알아봅니다.
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 15%

---

# 다국어 자산 {#multilingual-assets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | 이 문서 |
| AEM 6.4 | [여기를 클릭하십시오.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/multilingual-assets.html?lang=en) |

[!DNL Adobe Experience Manager Assets] 자산(바이너리, 메타데이터 및 태그 포함)에 대한 번역 워크플로우를 자동화하여 다국어 프로젝트에서 사용할 다른 언어로 자산을 생성할 수 있습니다.

번역 워크플로우를 자동화하기 위해 번역 서비스 공급자를 [!DNL Experience Manager] 자산을 여러 언어로 번역할 프로젝트를 만들 수 있습니다. [!DNL Experience Manager] 은 사람 및 기계 번역 워크플로우를 지원합니다.

인간 번역: 번역된 자산이 반환되고 [!DNL Experience Manager]. 번역 공급자가 [!DNL Experience Manager], 자산이 다음 사이 자동으로 전송됩니다. [!DNL Experience Manager] 그리고 번역 공급자입니다.

기계 번역: 기계 번역 서비스는 자산의 메타데이터와 태그를 즉시 변환합니다.

자산을 번역하면 다음 사항이 포함됩니다.

1. [번역 서비스 공급자와 Experience Manager 연결](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [번역 통합 프레임워크 구성 만들기](/help/sites-administering/tc-tic.md)
1. [자산 번역 준비](preparing-assets-for-translation.md)
1. [폴더에 번역 클라우드 서비스 적용](transition-cloud-services.md)
1. [번역 프로젝트 만들기](translation-projects.md)

번역 서비스 공급자가 [!DNL Experience Manager]를 사용하려면 [대체 프로세스](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

또한, [컨텐츠 조각에 대한 번역 프로젝트 만들기](creating-translation-projects-for-content-fragments.md).
