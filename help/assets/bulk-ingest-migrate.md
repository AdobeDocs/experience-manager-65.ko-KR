---
title: 벌크 자산 마이그레이션용 기능 팩 18912 설치
description: 기능 팩 18912을 사용하면 FTP를 통해 자산을 대량 수집하거나 Dynamic Media Classic에서 Adobe Experience Manager의 Dynamic Media으로 자산을 마이그레이션할 수 있습니다. 이 선택적 기능 팩은 Adobe 지원에서 사용할 수 있습니다.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# 벌크 자산 마이그레이션용 기능 팩 18912 설치{#installing-feature-pack-for-bulk-asset-migration}

기능 팩 18912 설치는 *선택 사항*&#x200B;입니다.

기능 팩 18912을 사용하면 FTP를 통해 자산을 Dynamic Media - Scene7 Adobe Experience Manager 모드로 직접 대량 수집할 수 있습니다. 또한 Experience Manager에서 Dynamic Media Classic의 자산을 Dynamic Media - Scene7 모드로 마이그레이션할 수 있습니다. 기능 팩은 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)에서 사용할 수 있습니다.

>[!IMPORTANT]
>
>기능 팩을 사용하여 Experience Manager에서 Dynamic Media Classic에서 Dynamic Media - Scene7 모드로 자산을 대량 마이그레이션할 수 있습니다. Dynamic Media Classic의 FTP 기능을 사용하여 자산을 대량 마이그레이션할 수도 있습니다. 그러나 Adobe은 복잡성 때문에 이러한 방법 중 하나를 사용하는 것이 좋습니다(*not*).
>
>따라서 이 마이그레이션 기능 팩은 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)을(를) 통해 완료 시 마이그레이션 프로젝트의 일부로 *only*&#x200B;이(가) 지원됩니다.

기능 팩을 설치하기 전에 서비스 사용자를 만들고 Adobe 지원에 해당 정보를 제공합니다.

[Dynamic Media - Scene7 모드 구성](/help/assets/config-dms7.md)도 참조하세요.

**일괄 에셋 마이그레이션에 대한 기능 팩 18912을 설치하려면:**

1. Experience Manager 인스턴스에서 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**(으)로 이동하고 **[!UICONTROL 사용자 만들기]**&#x200B;를 선택합니다. 이 서비스 사용자는 `/content/dam.`에 대한 *읽기/쓰기* 권한이 있어야 합니다.
1. **[!UICONTROL ID]** 및 **[!UICONTROL 암호]** 필드에 사용자 이름과 암호를 입력합니다(예: **FTP 사용자**). 이 이름은 타임라인에 자산을 만든 사용자로 나타납니다. FTP에서 에셋을 업로드하는 경우 FTP 서버에 에셋을 업로드하고 Experience Manager으로 푸시할 때 에셋이 생성된 것으로 간주됩니다.
1. 다운로드를 위해 기능 팩 18912에 대한 액세스를 요청하려면 [Experience Manager 고객 지원 Adobe](https://experienceleague.adobe.com/ko?support-solution=General#support)에 문의하십시오. 지원 센터에 문의할 때 다음 정보가 필요할 수 있습니다.

   * 포트 번호를 포함한 작성자 인스턴스의 서버 IP 주소(기본적으로 포트 번호는 4502입니다.)
   * 이전 단계의 Experience Manager 서비스 사용자 이름 및 암호입니다.

1. Experience Manager에 대한 고객 지원 Adobe은 FTP 자격 증명과 기능 팩 18912 액세스 권한을 제공합니다.
1. 기능 팩 18912을 받으면 설치합니다.

   Experience Manager에서 소프트웨어 배포 및 패키지를 사용하는 방법에 대한 자세한 내용은 [패키지를 사용하여 작업하는 방법](/help/sites-administering/package-manager.md)을 참조하십시오.
