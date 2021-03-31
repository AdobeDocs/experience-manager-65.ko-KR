---
title: ' [!DNL Adobe Creative Cloud] 우수 사례에 폴더 공유'
description: Adobe Creative Cloud(CC) 사용자와 폴더를 교환하도록  [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] 을 구성합니다.
contentOwner: AG
role: 비즈니스 전문가, 관리자
feature: 협업
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 을  [!DNL Adobe Creative Cloud] 클릭하여 폴더 공유  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager]에서 [!DNL Creative Cloud] 폴더 공유 기능은 더 이상 사용하지 않습니다. Adobe은 [Adobe 자산 링크](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) 또는 [Experience Manager 데스크톱 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)과 같은 최신 기능을 사용하는 것이 좋습니다. [Experience Manager 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md)에 대해 자세히 알아보십시오.

[!DNL Adobe Experience Manager] 사용자가 앱 사용자 [!DNL Assets] 와 폴더를 공유할 수 있도록 구성할 수  [!DNL Adobe Creative Cloud] 있으므로  [!DNL Adobe Creative Cloud] 에셋 서비스에서 공유 폴더로 사용할 수 있습니다. 이 기능은 크리에이티브 팀과 [!DNL Assets] 사용자 간에 파일을 교환하는 데 사용할 수 있습니다. 특히 크리에이티브 사용자가 [!DNL Assets] 배포에 액세스할 수 없는 경우(기업 네트워크에 있지 않음).

이러한 유형의 통합은 다음 사용 사례에서 사용할 수 있습니다. 특히 [!DNL Assets]에 직접 액세스할 수 없는 사용자와 작업할 때 사용됩니다.

* [!DNL Assets] 사용자는 특정 디지털 자산 세트를  [!DNL Adobe Creative Cloud] 파일 사용자와 공유합니다(예: 새 마케팅 활동을 위한 디자인 작업을 위해 승인된 자산 세트).
* [!DNL Assets] 사용자는  [!DNL Adobe Creative Cloud] 앱 사용자가 만든 새 파일을 받습니다.

>[!NOTE]
>
>이 문서를 읽기 전에 전체 [Experience Manager 및 Creative Cloud 통합 모범 사례](/help/assets/aem-cc-integration-best-practices.md)를 검토하여 통합에 대한 개요를 확인할 수 있습니다.

## 개요 {#overview}

[!DNL Experience Manager] 폴더  [!DNL Creative Cloud] 공유는 계정 간에 폴더 및 파일을 서버측에서 공유하는  [!DNL Assets] 데  [!DNL Creative Cloud] 의존합니다. 데스크탑에서 [!DNL Creative Cloud] 데스크탑 앱을 사용하는 크리에이티브 전문가는 [!DNL Adobe CreativeSync] 기술을 사용하여 디스크에서 바로 공유 폴더를 사용할 수 있도록 할 수 있습니다.

다음 다이어그램은 통합에 대한 개요를 제공합니다.

![chlimage_1-179](assets/chlimage_1-406.png)

통합에는 다음 요소가 포함됩니다.

* **[!DNL Experience Manager Assets]** 엔터프라이즈 네트워크에 배포(관리 서비스 또는 온프레미스):폴더 공유가 여기에서 시작됩니다.
* **[!DNL Adobe Marketing Cloud Assets]핵심 서비스**:서비스 [!DNL Experience Manager] 와  [!DNL Creative Cloud] 스토리지 서비스 간의 중간 역할을 합니다. 통합을 사용하는 조직의 관리자는 Marketing Cloud 조직과 [!DNL Assets] 배포 간에 신뢰 관계를 설정해야 합니다. 또한 [승인된 Creative Cloud 협력자 목록](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)을 정의하여 추가 보안을 위해 [!DNL Assets] 사용자가 폴더를 공유할 수 있습니다.

* **[!DNL Creative Cloud]에셋 웹 서비스** (저장소 및  [!DNL Creative Cloud] 파일 웹 UI):폴더를 공유한 특정 Creative Cloud 앱 사용자가 초대를  [!DNL Assets] 수락하고 Creative Cloud 계정 저장소의 폴더를 볼 수 있는 곳입니다.
* **Creative Cloud 데스크탑 앱**:(선택 사항)  [!DNL Creative Cloud] 에셋 저장소와 동기화를 통해 크리에이티브 사용자의 데스크탑에서 공유 폴더/파일에 직접 액세스할 수 있습니다.

## 특성 및 제한 사항 {#characteristics-and-limitations}

* **변경 사항의 단방향 전파:** 파일 변경 사항은 자산이 원래 생성(업로드됨)된 시스템([!DNL Experience Manager] 또는  [!DNL Creative Cloud Assets])에서 한 방향으로만 전파됩니다. 통합은 두 시스템 간에 완전히 자동화된 양방향 동기화를 제공하지 않습니다.
* **버전 관리:**

   * [!DNL Experience Manager] 파일이 에서 시작되어 업데이트되는 경우에만 업데이트 시 에셋 버전 [!DNL Experience Manager] 을 만듭니다.
   * [!DNL Creative Cloud] 자산은 진행 중인 작업 업데이트 [ ](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 를 대상으로 하는 자체 버전 관리 기능을 제공합니다(기본적으로 최대 10일 동안 업데이트 저장).

* **공간 제한:** 교환된 파일의 크기 및 용량은 크리에이티브 사용자를 위한 특정  [Creative Cloud 에셋 ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 할당량(가입 수준에 따라 다름)에 의해 제한되며 최대 파일 크기는 5GB로 제한됩니다. 조직은 Adobe Marketing Cloud Assets 핵심 서비스에 있는 자산 할당량에 따라 공간을 추가로 제한합니다.

* **공간 요구 사항:** 공유 폴더의 파일은  [!DNL Experience Manager] 핵심 서비스에 캐시된 사본을 사용하여 물리적으로 저장  [!DNL Creative Cloud] 후  [!DNL Marketing Cloud Assets] 계정에 저장해야 합니다.
* **네트워킹 및 대역폭:** 공유 폴더의 파일과 모든 업데이트를 시스템 간에 네트워크를 통해 전송해야 합니다. 관련 파일 및 업데이트만 공유되도록 해야 합니다.
* **폴더 유형**:이  [!DNL Assets] 유형의 폴더 `sling:OrderedFolder`는 공유 시 지원되지 않습니다 [!DNL Adobe Marketing Cloud]. 폴더를 공유하려면 [!DNL Assets]에서 폴더를 만들 때 [!UICONTROL 주문됨] 옵션을 선택하지 마십시오.

## 우수 사례 {#best-practices}

[!DNL Experience Manager]을(를) [!DNL Creative Cloud] 폴더 공유에 활용하기 위한 우수 사례에는 다음이 포함됩니다.

* **볼륨 고려 사항:** [!DNL Experience Manager] 및  [!DNL Creative Cloud] 폴더 공유를 사용하여 특정 캠페인 또는 활동과 관련된 더 적은 수의 파일을 공유해야 합니다. 조직에서 승인된 모든 자산과 같이 더 큰 자산 세트를 공유하려면 다른 배포 방법(예: [!DNL Assets Brand Portal]) 또는 [!DNL Experience Manager] 데스크탑 앱을 사용하십시오.
* **계층 구조 공유 안 함: 공유** 는 재귀적으로 작동하며 선택적 공유를 허용하지 않습니다. 일반적으로 하위 폴더가 없거나 하위 폴더 수준 1과 같이 매우 얕은 계층 구조를 가진 폴더만 공유할 수 있습니다.
* **한 방향 공유를 위한 폴더 분리:** 최종 자산을 파일에서 파일 [!DNL Assets] 로 공유하고,  [!DNL Creative Cloud] 바로 만들 수 있는 에셋을  [!DNL Creative Cloud] 파일에서 파일로 다시 공유하려면 별도의 폴더를 사용해야  [!DNL Assets]합니다. 이러한 폴더에 대한 적절한 명명 규칙과 함께 [!DNL Assets] 및 [!DNL Creative Cloud] 사용자에 대해 이해하기 쉬운 작업 환경을 만듭니다.
* **공유 폴더의 WIP 방지:** 공유 폴더는 진행 중인 작업에 사용해서는 안 됩니다. 파일을 자주 변경해야 하는 작업을 수행하려면 Creative Cloud 파일의 별도의 폴더를 사용하십시오.
* **공유 폴더 외부에서 새 작업 시작:** 새 디자인(크리에이티브 파일)은 Creative Cloud 파일의 별도의 WIP 폴더에서 시작해야 하며 사용자와 공유할 준비가  [!DNL Assets] 된 경우 공유 폴더로 이동하거나 저장해야 합니다.
* **공유 구조 간소화:** 더욱 관리가 용이한 운영 설정을 위해서는 공유 구조를 단순화하는 것이 좋습니다. 모든 크리에이티브 사용자와 공유하는 대신 [!DNL Assets] 폴더는 크리에이티브 디렉터 또는 팀 관리자와 같은 팀 담당자와만 공유해야 합니다. 크리에이티브 쪽의 관리자는 최종 자산을 받고, 작업 할당을 결정한 다음, 디자이너가 WIP 자산에 대한 자신의 Creative Cloud 계정에서 작업을 하도록 합니다. Creative Cloud 공동 작업 기능을 사용하여 작업을 조정하고, 마지막으로 [!DNL Assets]에 공유할 준비가 된 에셋을 선택하고 다시 크리에이티브한 공유 폴더로 가져올 수 있습니다.

다음 다이어그램은 [!DNL Assets]의 기존 최종 자산을 기반으로 새 디자인을 만들기 위한 예제 구성을 보여줍니다.

![chlimage_1-180](assets/chlimage_1-407.png)
