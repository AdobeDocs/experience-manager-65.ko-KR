---
title: ' [!DNL Adobe Creative Cloud] 모범 사례에 폴더 공유'
description: ' [!DNL Experience Manager Assets] 의 사용자가 Adobe Creative Cloud 사용자와 폴더를 교환할 수 있도록  [!DNL Adobe Experience Manager] 을(를) 구성하십시오.'
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager]에서 [!DNL Adobe Creative Cloud] 폴더 공유 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager] - [!DNL Creative Cloud] 폴더 공유 기능은 더 이상 사용되지 않습니다. Adobe은 [Adobe 에셋 링크](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html) 또는 [Experience Manager 데스크톱 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)과 같은 최신 기능을 사용할 것을 권장합니다. [Experience Manager 및 Creative Cloud 통합 모범 사례](/help/assets/aem-cc-integration-best-practices.md)에서 자세히 알아보세요.

[!DNL Assets]의 사용자가 [!DNL Adobe Creative Cloud] 앱의 사용자와 폴더를 공유할 수 있도록 [!DNL Adobe Experience Manager]을(를) 구성할 수 있으므로 해당 폴더는 [!DNL Adobe Creative Cloud] 자산 서비스에서 공유 폴더로 사용할 수 있습니다. 특히 크리에이티브 사용자가 [!DNL Assets] 배포에 액세스할 수 없는 경우(엔터프라이즈 네트워크에 없는 경우) 이 기능을 사용하여 크리에이티브 팀과 [!DNL Assets] 사용자 간에 파일을 교환할 수 있습니다.

이러한 통합 유형은 특히 [!DNL Assets]에 대한 직접 액세스 권한이 없는 사용자와 작업할 때 다음 사용 사례에서 사용할 수 있습니다.

* [!DNL Assets]명의 사용자가 [!DNL Adobe Creative Cloud]개 파일의 사용자와 특정 디지털 자산 집합을 공유합니다(예: 새 마케팅 활동을 위한 디자인 작업을 위한 크리에이티브 개요 및 승인된 자산 집합).
* [!DNL Assets] 사용자가 [!DNL Adobe Creative Cloud] 앱 사용자가 만든 새 파일을 받습니다.

>[!NOTE]
>
>이 문서를 읽기 전에 통합에 대한 개요를 살펴보기 위해 전체 [Experience Manager 및 Creative Cloud 통합 모범 사례](/help/assets/aem-cc-integration-best-practices.md)를 검토할 수 있습니다.

## 개요 {#overview}

[!DNL Experience Manager]에서 [!DNL Creative Cloud] 폴더 공유는 [!DNL Assets]과(와) [!DNL Creative Cloud] 계정 간에 폴더와 파일을 서버측에서 공유하는 것을 사용합니다. 데스크톱에서 [!DNL Creative Cloud] 데스크톱 앱을 사용하는 크리에이티브 전문가는 [!DNL Adobe CreativeSync] 기술을 사용하여 디스크에서 직접 공유 폴더를 사용할 수도 있습니다.

다음 다이어그램은 통합에 대한 개요를 제공합니다.

![chlimage_1-179](assets/chlimage_1-406.png)

통합에는 다음 요소가 포함됩니다.

* 엔터프라이즈 네트워크(Managed Services 또는 온-프레미스)에 배포된 **[!DNL Experience Manager Assets]**: 여기에서 폴더 공유가 시작됩니다.
* **[!DNL Adobe Experience Cloud Assets]핵심 서비스**: [!DNL Experience Manager]과(와) [!DNL Creative Cloud] 저장소 서비스 사이에서 중개 역할을 합니다. 통합을 사용하는 조직의 관리자는 Experience Cloud 조직과 [!DNL Assets] 배포 간에 트러스트 관계를 설정해야 합니다. [승인된 Creative Cloud 공동 작업자 목록을 정의](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html)합니다. [!DNL Assets]명의 사용자도 추가 보안을 위해 폴더를 공유할 수 있습니다.

* **[!DNL Creative Cloud]Assets 웹 서비스**(저장소 및 [!DNL Creative Cloud] 파일 웹 UI): [!DNL Assets] 폴더를 공유한 특정 Creative Cloud 앱 사용자가 초대를 수락하고 Creative Cloud 계정 저장소에서 해당 폴더를 볼 수 있는 곳입니다.
* **Creative Cloud 데스크톱 앱**: (선택 사항) [!DNL Creative Cloud] Assets 스토리지와의 동기화를 통해 크리에이티브 사용자의 데스크톱에서 공유 폴더/파일에 직접 액세스할 수 있습니다.

## 특성 및 제한 사항 {#characteristics-and-limitations}

* **변경 사항의 단방향 전파:** 파일 변경 사항은 원래 에셋이 만들어진(업로드된) 시스템([!DNL Experience Manager] 또는 [!DNL Creative Cloud Assets])에서 한 방향으로만 전파됩니다. 통합은 두 시스템 간에 완전히 자동화된 양방향 동기화를 제공하지 않습니다.
* **버전 관리:**

   * [!DNL Experience Manager]은(는) 파일이 [!DNL Experience Manager]에서 시작되고 업데이트되는 경우에만 업데이트 시 에셋의 버전을 만듭니다.
   * [!DNL Creative Cloud] Assets은 진행 중인 작업 업데이트(기본적으로 최대 10일 동안 업데이트 저장)를 대상으로 하는 자체 [버전 관리 기능](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html)을 제공합니다.

* **공간 제한:** 교환되는 파일의 크기 및 볼륨은 Creative Users의 특정 [Creative Cloud Assets 할당량](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html)에 의해 제한됩니다(구독 수준에 따라 다름). 최대 파일 크기는 5GB입니다. 또한 공간은 조직이 Adobe Experience Cloud Assets 핵심 서비스에 보유한 에셋 할당량에 의해 제한됩니다.

* **공간 요구 사항:** 공유 폴더의 파일도 실제로 [!DNL Experience Manager]에 저장한 다음 [!DNL Creative Cloud] 계정에 [!DNL Experience Cloud Assets] 핵심 서비스에 캐시된 복사본을 저장해야 합니다.
* **네트워킹 및 대역폭:** 공유 폴더의 파일과 모든 업데이트는 시스템 간에 네트워크를 통해 전송되어야 합니다. 관련 파일과 업데이트만 공유되는지 확인합니다.
* **폴더 형식**: `sling:OrderedFolder` 형식의 [!DNL Assets] 폴더를 공유하는 작업은 [!DNL Adobe Experience Cloud]에서 공유하는 컨텍스트에서 지원되지 않습니다. 폴더를 공유하려면 [!DNL Assets]에서 폴더를 만들 때 [!UICONTROL 정렬됨] 옵션을 선택하지 마십시오.

## 모범 사례 {#best-practices}

[!DNL Experience Manager]에서 [!DNL Creative Cloud] 폴더 공유를 사용하는 우수 사례는 다음과 같습니다.

* **볼륨 고려 사항:** [!DNL Experience Manager] 및 [!DNL Creative Cloud] 폴더 공유는 특정 캠페인이나 활동과 관련된 파일을 더 적게 공유하는 데 사용해야 합니다. 조직의 승인된 모든 자산과 같이 더 큰 자산 집합을 공유하려면 다른 배포 방법(예: [!DNL Assets Brand Portal]) 또는 [!DNL Experience Manager] 데스크톱 앱을 사용하십시오.
* **심층 계층 공유를 피하십시오.** 공유는 재귀적으로 작동하며 선택적 공유를 해제할 수 없습니다. 일반적으로 하위 폴더가 없거나 하나의 하위 폴더 수준과 같은 얕은 계층 구조를 가진 폴더만 공유하는 것으로 간주합니다.
* **단방향 공유를 위한 개별 폴더:** [!DNL Assets]에서 [!DNL Creative Cloud] 파일로 최종 자산을 공유하고 [!DNL Creative Cloud] 파일에서 [!DNL Assets] 파일로 창의적인 준비가 된 자산을 다시 공유하는 데 개별 폴더를 사용해야 합니다. 이러한 폴더에 대한 좋은 명명 규칙을 함께 사용하면 [!DNL Assets] 및 [!DNL Creative Cloud] 사용자가 이해하기 쉬운 작업 환경을 만들 수 있습니다.
* **공유 폴더에서 WIP 방지:** 진행 중인 작업에 공유 폴더를 사용하지 마십시오. 파일을 자주 변경해야 하는 작업을 수행하려면 Creative Cloud 파일에 별도의 폴더를 사용하십시오.
* **공유 폴더 외부에서 새 작업 시작:** 새 디자인(크리에이티브 파일)은 Creative Cloud 파일의 개별 WIP 폴더에서 시작해야 하며 [!DNL Assets] 사용자와 공유할 준비가 되면 공유 폴더로 이동하거나 저장해야 합니다.
* **공유 구조 간소화:** 관리 가능한 운영 설정을 만들려면 공유 구조를 단순화하는 것이 좋습니다. 모든 크리에이티브 사용자와 공유하지 않고 [!DNL Assets]개의 폴더를 크리에이티브 디렉터나 팀 관리자와 같은 팀 담당자만 공유해야 합니다. 크리에이티브 쪽의 관리자는 최종 에셋을 수신하고 작업 할당을 결정한 다음 디자이너가 WIP 에셋의 자체 Creative Cloud 계정에서 작업할 수 있도록 합니다. Creative Cloud 공동 작업 기능을 사용하여 작업을 조정하고, 마지막으로 공유할 준비가 된 자산을 선택하여 [!DNL Assets]에 바로 게시할 수 있는 공유 폴더에 넣을 수 있습니다.

다음 다이어그램은 [!DNL Assets]의 기존 최종 자산을 기반으로 디자인을 만드는 예제 구성을 보여 줍니다.

![chlimage_1-180](assets/chlimage_1-407.png)
