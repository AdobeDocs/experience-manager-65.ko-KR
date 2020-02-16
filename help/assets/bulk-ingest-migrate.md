---
title: 벌크 에셋 마이그레이션을 위한 기능 팩 18912 설치
description: 기능 팩 18912를 사용하면 FTP를 통해 자산을 벌크 인제스트하거나 Dynamic Media Classic에서 AEM의 Dynamic Media로 자산을 마이그레이션할 수 있습니다. 이 선택적 기능 팩은 Adobe 지원을 통해 제공됩니다.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 벌크 에셋 마이그레이션을 위한 기능 팩 18912 설치{#installing-feature-pack-for-bulk-asset-migration}

기능 팩 18912의 설치는 *선택 사항입니다*.

기능 팩 18912를 사용하면 FTP를 통해 AEM의 Dynamic Media - Scene7 모드로 바로 자산을 일괄적으로 인제스트하거나 Dynamic Media Classic에서 AEM의 Scene7 모드로 자산을 마이그레이션할 수 있습니다. 기능 팩은 Adobe Professional Services에서 [제공됩니다](https://www.adobe.com/experience-cloud/consulting-services.html).

>[!NOTE]
>
>기능 팩을 사용하여 직접 Dynamic Media Classic에서 Dynamic Media - AEM의 Scene 7 모드로 자산을 일괄적으로 마이그레이션하거나 Dynamic Media Classic의 FTP 기능을 사용하여 자산을 벌크 마이그레이션할 수 있지만, Adobe에서는 이러한 복잡성으로 인해 이 방법을 권장하지 *않습니다* .
>
>이와 같은 마이그레이션 기능 팩은 Adobe Professional Services를 통해 수행하는 경우 마이그레이션 프로젝트의 *일부로만* [지원됩니다](https://www.adobe.com/experience-cloud/consulting-services.html).

Feature Pack을 설치하려면 먼저 서비스 사용자를 만들고 해당 정보를 Adobe 지원에 제공해야 합니다.

동적 [미디어 구성 - Scene7 모드](/help/assets/config-dms7.md)구성을 참조하십시오.

**벌크 에셋 마이그레이션을 위한 기능 팩 18912를 설치하려면**

1. AEM 인스턴스에서 도구 > 보안 > **[!UICONTROL 사용자로 이동하고]** 사용자 **[!UICONTROL 만들기를 선택합니다]**. 이 서비스 사용자는 *읽기/쓰기* 권한이 있어야 합니다. `/content/dam.`
1. ID **[!UICONTROL 및]** 암호 **[!UICONTROL 필드에]** 사용자 이름과 암호를 입력합니다.예를 들어, FTP **사용자**. 이 이름은 타임라인에 자산을 만든 사용자로 표시됩니다. 자산이 FTP에서 업로드되면 자산이 FTP 서버에 업로드되고 AEM으로 푸시될 때 만들어지는 것으로 간주됩니다.
1. 기능 [팩 18912를](https://helpx.adobe.com/contact/enterprise-support.ec.html) 다운로드하려면 Adobe Enterprise Support for Experience Manager에 문의하십시오. 지원 센터에 문의할 때 다음 정보가 필요할 수 있습니다.

   * 작성자 인스턴스의 서버 IP 주소(기본적으로 포트 번호는 4502입니다.)
   * 이전 단계의 AEM 서비스 사용자 이름과 암호

1. AEM용 Adobe 엔터프라이즈 지원은 FTP 자격 증명 및 기능 팩 18912에 대한 액세스 권한을 제공합니다.
1. 기능 팩 18912를 받으면 설치합니다.

   AEM [에서 패키지 공유](/help/sites-administering/package-manager.md) 및 패키지 사용에 대한 자세한 내용은 패키지 사용 방법을 참조하십시오.

