---
title: 폴더 공유 대상 [!DNL Adobe Creative Cloud] 우수 사례
description: 폴더를 Adobe Creative Cloud(CC) 사용자와 교환하도록  [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] 을 구성합니다.
contentOwner: AG
role: Business Practitioner, Administrator
feature: 협업
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 폴더 공유 [!DNL Adobe Creative Cloud] 로  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager] - [!DNL Creative Cloud] 폴더 공유 기능은 더 이상 사용되지 않습니다. Adobe은 [Adobe 자산 링크](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) 또는 [Experience Manager 데스크탑 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)과 같은 최신 기능을 사용할 것을 강력히 권장합니다. 자세한 내용은 [Experience Manager 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md)를 참조하십시오.

[!DNL Adobe Experience Manager] 에서는 사용자가 앱 사용자 [!DNL Assets] 와 폴더를 공유할 수 있도록 구성할 수  [!DNL Adobe Creative Cloud] 있으므로  [!DNL Adobe Creative Cloud] 자산 서비스에서 공유 폴더로 사용할 수 있습니다. 이 기능은 크리에이티브 팀과 [!DNL Assets] 사용자 간에 파일을 교환하는 데 사용할 수 있습니다. 특히 크리에이티브 사용자가 [!DNL Assets] 배포에 액세스할 수 없는 경우(엔터프라이즈 네트워크에 있지 않음).

이 유형의 통합은 다음 사용 사례에서 사용할 수 있습니다. 특히 [!DNL Assets]에 직접 액세스할 수 없는 사용자와 작업할 때 사용됩니다.

* [!DNL Assets] 사용자는 특정 디지털 자산 세트를  [!DNL Adobe Creative Cloud] 파일 사용자와 공유합니다(예: 새 마케팅 활동에 대해 디자인할 승인된 자산의 세트).
* [!DNL Assets] 사용자는  [!DNL Adobe Creative Cloud] 앱 사용자가 만든 새 파일을 받습니다.

>[!NOTE]
>
>이 문서를 읽기 전에 통합 개요를 보려면 전체 [Experience Manager 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md)를 검토하십시오.

## 개요 {#overview}

[!DNL Experience Manager] 폴더  [!DNL Creative Cloud] 공유는  [!DNL Assets] 및  [!DNL Creative Cloud] 계정 간에 폴더 및 파일을 서버측 공유로 사용합니다. 데스크탑에서 [!DNL Creative Cloud] 데스크탑 앱을 사용하는 크리에이티브 전문가는 [!DNL Adobe CreativeSync] 기술을 사용하여 공유 폴더를 디스크에서 직접 사용할 수 있도록 만들 수도 있습니다.

다음 다이어그램은 통합에 대한 개요를 제공합니다.

![chlimage_1-179](assets/chlimage_1-406.png)

통합에는 다음 요소가 포함됩니다.

* **[!DNL Experience Manager Assets]** 엔터프라이즈 네트워크(관리 서비스 또는 온-프레미스)에 배포됩니다.여기에서 폴더 공유가 시작됩니다.
* **[!DNL Adobe Marketing Cloud Assets]핵심 서비스**:및  [!DNL Experience Manager]   [!DNL Creative Cloud] 스토리지 서비스 간의 중간 역할을 합니다. 통합을 사용하는 조직의 관리자는 Marketing Cloud 조직과 [!DNL Assets] 배포 간의 신뢰 관계를 설정해야 합니다. 또한 [승인된 Creative Cloud 협력자 목록](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)을 정의하여 [!DNL Assets] 사용자가 추가 보안을 위해 폴더를 공유할 수 있습니다.

* **[!DNL Creative Cloud]Assets 웹 서비스** (저장소 및  [!DNL Creative Cloud] 파일 웹 UI):여기에서 폴더를 공유한 특정 Creative Cloud 앱  [!DNL Assets] 사용자는 초대를 수락하고 Creative Cloud 계정 저장소에서 폴더를 볼 수 있습니다.
* **Creative Cloud 데스크탑 앱**:(선택 사항)  [!DNL Creative Cloud] 자산 저장소와 동기화를 통해 크리에이티브 사용자의 데스크탑에서 공유 폴더/파일에 직접 액세스할 수 있습니다.

## 특성 및 제한 사항 {#characteristics-and-limitations}

* **변경 사항의 단방향 전파:** 파일 변경 사항은 원래 자산이 생성되어 업로드된 시스템([!DNL Experience Manager]  또는  [!DNL Creative Cloud Assets])에서 한 방향으로만 전파됩니다. 통합은 두 시스템 간에 완전히 자동화된 양방향 동기화를 제공하지 않습니다.
* **버전 관리:**

   * [!DNL Experience Manager] 파일에서 가 시작되어 이 업데이트되는 경우에만 업데이트 시 자산 버전 [!DNL Experience Manager] 을 만듭니다.
   * [!DNL Creative Cloud] Assets는 진행  [중인 작업 ](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 업데이트(기본적으로 최대 10일 동안 업데이트 저장)를 대상으로 하는 자체 버전 관리 기능을 제공합니다

* **공간 제한:** 교환된 파일의 크기와 볼륨은 크리에이티브 사용자 [를 위한 특정 ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud 자산 수( 구독 수준에 따라 다름)로 제한되고 최대 파일 크기는 5GB로 제한됩니다. 조직은 Adobe Marketing Cloud Assets 핵심 서비스에 있는 자산 할당량에 의해 공간이 추가로 제한됩니다.

* **공간 요구 사항:** 공유 폴더의 파일도 물리적으로  [!DNL Experience Manager] 에 저장된 다음  [!DNL Creative Cloud] 계정에  [!DNL Marketing Cloud Assets] 핵심 서비스의 캐시된 복사본을 사용하여 저장해야 합니다.
* **네트워킹 및 대역폭:**  공유 폴더의 파일과 모든 업데이트를 시스템 간 네트워크를 통해 전송해야 합니다. 관련 파일 및 업데이트만 공유되도록 해야 합니다.
* **폴더 유형**:유형 [!DNL Assets] 의 폴더 `sling:OrderedFolder`를 공유하는 것은 의 공유 컨텍스트에서 지원되지 않습니다  [!DNL Adobe Marketing Cloud]. 폴더를 공유하려면 [!DNL Assets]에서 만들 때 [!UICONTROL 순서가 지정된] 옵션을 선택하지 마십시오.

## 우수 사례 {#best-practices}

[!DNL Experience Manager] 을 [!DNL Creative Cloud] 폴더 공유에 활용하는 우수 사례는 다음과 같습니다.

* **볼륨 고려 사항:** [!DNL Experience Manager] 및  [!DNL Creative Cloud] 폴더 공유 는 특정 캠페인이나 활동과 관련된 작은 수의 파일을 공유하는 데 사용해야 합니다. 조직에서 승인된 모든 자산과 같이 더 큰 자산 세트를 공유하려면 다른 배포 방법(예: [!DNL Assets Brand Portal]) 또는 [!DNL Experience Manager] 데스크탑 앱을 사용합니다.
* **딥 계층을 공유하지 마십시오:**  공유는 재귀적으로 작동하며 선택적 공유 취소를 허용하지 않습니다. 일반적으로 하위 폴더가 없거나 하위 폴더 레벨과 같이 매우 낮은 계층 구조를 가진 폴더만 공유로 간주해야 합니다.
* **단방향 공유를 위한 별도의 폴더:** 최종 자산 [!DNL Assets] 을 파일로부터  [!DNL Creative Cloud] 파일로 공유하고,  [!DNL Creative Cloud] 파일에서 로 직접 크리에이티브 자산을 공유하려면 별도의 폴더를 사용해야  [!DNL Assets]합니다. 이러한 폴더에 대한 올바른 이름 지정 규칙을 함께 사용하면 [!DNL Assets] 및 [!DNL Creative Cloud] 사용자에 대해 이해하기 쉬운 작업 환경을 만들 수 있습니다.
* **공유 폴더의 WIP를 피하십시오.** 진행 중인 작업에 공유 폴더를 사용하지 마십시오. 파일을 자주 변경해야 하는 작업을 수행하려면 Creative Cloud 파일의 별도의 폴더를 사용하십시오.
* **공유 폴더 외부에서 새 작업 시작:** 새 디자인(크리에이티브 파일)은 Creative Cloud 파일의 별도의 WIP 폴더에서 시작해야 하며  [!DNL Assets] 사용자와 공유할 준비가 되면 공유 폴더로 이동하거나 저장해야 합니다.
* **공유 구조 간소화:** 관리할 수 있는 운영 체제를 갖추려면 공유 구조를 간소화하는 것이 좋습니다. 모든 크리에이티브 사용자와 공유하는 대신 [!DNL Assets] 폴더는 크리에이티브 디렉터나 팀 관리자와 같은 팀 담당자에게만 공유되어야 합니다. 크리에이티브 측의 관리자는 최종 자산을 수신하고, 작업 지정을 결정한 다음, 디자이너가 WIP 자산에서 자신의 Creative Cloud 계정으로 작업할 수 있도록 합니다. Creative Cloud 공동 작업 기능을 사용하여 작업을 조정하고, 마지막으로 [!DNL Assets]에 다시 공유할 준비가 된 자산을 선택하고 해당 크리에이티브 지원 공유 폴더로 배치할 수 있습니다.

다음 다이어그램은 [!DNL Assets]의 기존 최종 자산을 기반으로 새 디자인을 생성하기 위한 예제 구성을 보여줍니다.

![chlimage_1-180](assets/chlimage_1-407.png)
