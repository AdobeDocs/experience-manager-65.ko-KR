---
title: 벌크 자산 마이그레이션용 기능 팩 18912 설치
description: 기능 팩 18912을 사용하면 FTP를 통해 자산을 벌크하거나 Dynamic Media Classic에서 AEM의 Dynamic Media으로 자산을 마이그레이션할 수 있습니다. 이 선택적 기능 팩은 Adobe 지원에서 사용할 수 있습니다.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: 자산 관리
role: Business Practitioner, Administrator
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# 벌크 자산 마이그레이션용 기능 팩 18912 설치{#installing-feature-pack-for-bulk-asset-migration}

기능 팩 18912 설치은 *선택 사항*&#x200B;입니다.

기능 팩 18912을 사용하면 FTP를 통해 AEM에서 Dynamic Media - Scene7 모드로 직접 자산을 일괄 수집하거나, Dynamic Media Classic에서 AEM의 Dynamic Media - Scene7 모드로 자산을 마이그레이션할 수 있습니다. 기능 팩은 [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)에서 사용할 수 있습니다.

>[!NOTE]
>
>기능 팩을 사용하여 자산을 Dynamic Media Classic에서 Dynamic Media - Scene 7 모드로 직접 마이그레이션하거나 AEM Classic의 FTP 기능을 사용하여 자산을 벌크로 마이그레이션하는 것이 가능하지만, Adobe은 관련된 복잡성으로 인해 *이 아닌*&#x200B;을 추천합니다.
>
>이와 같은 마이그레이션 기능 팩은 *만 [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)을 통해 완료할 때 마이그레이션 프로젝트의 일부로 지원됩니다.*

기능 팩을 설치하려면 먼저 서비스 사용자를 만들고 해당 정보를 Adobe 지원에 제공해야 합니다.

[Dynamic Media 구성 - Scene7 모드](/help/assets/config-dms7.md)도 참조하십시오.

**벌크 자산 마이그레이션용 기능 팩 18912을 설치하려면**

1. AEM 인스턴스에서 **[!UICONTROL 도구 > 보안 > 사용자]**&#x200B;로 이동하고 **[!UICONTROL 사용자 만들기]**&#x200B;를 선택합니다. 이 서비스 사용자에게는 `/content/dam.`에 대한 *읽기/쓰기* 권한이 있어야 합니다.
1. **[!UICONTROL ID]** 및 **[!UICONTROL 암호]** 필드에 사용자 이름과 암호를 입력합니다.예: **FTP 사용자** 이 이름은 자산을 만든 사용자로 타임라인에 나타납니다. 자산이 FTP에서 업로드되면 자산이 FTP 서버에 업로드되면 자산이 만들어지고 AEM으로 푸시되는 것으로 간주됩니다.
1. 기능 팩 18912에 대한 액세스를 요청하려면 [Experience Manager에 대한 엔터프라이즈 고객 지원 센터 Adobe](https://experienceleague.adobe.com/?support-solution=General#support)에 문의하십시오. 지원에 문의할 때 다음 정보가 필요할 수 있습니다.

   * 작성자 인스턴스의 서버 IP 주소(기본적으로 포트 번호는 4502임)
   * 이전 단계의 AEM 서비스 사용자 이름 및 암호입니다.

1. AEM용 Adobe 엔터프라이즈 고객 지원 팀에서는 FTP 자격 증명과 기능 팩 18912에 대한 액세스 권한을 제공합니다.
1. 기능 팩 18912을 받으면 설치합니다.

   AEM에서 소프트웨어 배포 및 패키지 사용에 대한 자세한 내용은 [패키지 사용 방법](/help/sites-administering/package-manager.md)을 참조하십시오.
