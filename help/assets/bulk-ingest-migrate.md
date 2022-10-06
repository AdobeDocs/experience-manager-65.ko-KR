---
title: 벌크 자산 마이그레이션용 기능 팩 18912 설치
description: 기능 팩 18912을 사용하면 FTP를 통해 자산을 벌크하거나 Dynamic Media Classic에서 Adobe Experience Manager의 Dynamic Media으로 자산을 마이그레이션할 수 있습니다. 이 선택적 기능 팩은 Adobe 지원에서 사용할 수 있습니다.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 1%

---

# 벌크 자산 마이그레이션용 기능 팩 18912 설치{#installing-feature-pack-for-bulk-asset-migration}

기능 팩 18912 설치은 다음과 같습니다 *옵션*.

기능 팩 18912을 사용하면 FTP를 통해 Adobe Experience Manager에서 Dynamic Media - Scene7 모드로 자산을 직접 수집할 수 있습니다. 또한 자산을 Dynamic Media Classic에서 Experience Manager의 Dynamic Media - Scene7 모드로 마이그레이션할 수 있습니다. 기능 팩은 다음에서 사용할 수 있습니다. [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>기능 팩을 사용하여 Experience Manager에서 Dynamic Media Classic에서 Dynamic Media - Scene7 모드로 자산을 직접 벌크로 마이그레이션할 수 있습니다. Dynamic Media Classic의 FTP 기능을 사용하여 자산을 벌크로 마이그레이션할 수도 있습니다. 그러나 Adobe은 *not* 관련된 복잡성으로 인해 이러한 메서드를 사용하는 것이 좋습니다.
>
>따라서 이 마이그레이션 기능 팩은 다음과 같습니다 *전용* 를 통해 완료할 때 마이그레이션 프로젝트의 일부로 지원됨 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

기능 팩을 설치하기 전에 서비스 사용자를 만들고 해당 정보를 Adobe 지원에 제공합니다.

참조 - [Dynamic Media 구성 - Scene7 모드](/help/assets/config-dms7.md).

**벌크 자산 마이그레이션용 기능 팩 18912을 설치하려면 다음을 수행하십시오.**

1. Experience Manager 인스턴스에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]** 을(를) 선택합니다. **[!UICONTROL 사용자 만들기]**. 이 서비스 사용자는 *읽기/쓰기* 권한 `/content/dam.`
1. 에서 **[!UICONTROL ID]** 및 **[!UICONTROL 암호]** 필드에 사용자 이름과 암호를 입력합니다. 예 **FTP 사용자**. 이 이름은 자산을 만든 사용자로 타임라인에 나타납니다. 자산이 FTP에서 업로드되면 자산이 FTP 서버에 업로드되면 자산이 만들어지고 Experience Manager으로 푸시되는 것으로 간주됩니다.
1. 연락처 [Experience Manager Adobe 고객 지원](https://experienceleague.adobe.com/?support-solution=General#support) 기능 팩 18912에 대한 액세스를 요청하여 다운로드하십시오. 지원에 문의할 때 다음 정보가 필요할 수 있습니다.

   * 작성자 인스턴스의 서버 IP 주소(기본적으로 포트 번호는 4502임)
   * 이전 단계의 Experience Manager 서비스 사용자 이름 및 암호입니다.

1. Experience Manager에 대한 Adobe 고객 지원 에서는 FTP 자격 증명을 제공하고 기능 팩 18912에 액세스할 수 있습니다.
1. 기능 팩 18912을 받으면 설치합니다.

   자세한 내용은 [패키지 작업 방법](/help/sites-administering/package-manager.md) Experience Manager에서 소프트웨어 배포 및 패키지 사용에 대한 자세한 정보.
