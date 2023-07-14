---
title: 폴더 공유 대상 [!DNL Adobe Creative Cloud] 우수 사례
description: 구성 [!DNL Adobe Experience Manager] 에서 사용자를 허용하려면 [!DNL Experience Manager Assets] Adobe Creative Cloud 사용자와 폴더를 교환하려는 경우
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 끝 [!DNL Adobe Creative Cloud] 폴더 공유 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>다음 [!DNL Experience Manager] 끝 [!DNL Creative Cloud] 폴더 공유 기능은 더 이상 사용되지 않습니다. Adobe은 다음과 같은 최신 기능을 사용할 것을 권장합니다. [Adobe 에셋 링크](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html) 또는 [Experience Manager 데스크탑 앱](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). 다음에서 자세히 알아보기 [Experience Manager 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] 에서 사용자를 허용하도록 구성 가능 [!DNL Assets] 의 사용자와 폴더를 공유하려면 [!DNL Adobe Creative Cloud] 앱으로 이동하여 [!DNL Adobe Creative Cloud] 에셋 서비스. 이 기능은 크리에이티브 팀과 간에 파일을 교환하는 데 사용할 수 있습니다. [!DNL Assets] 특히 크리에이티브 사용자가 다음에 액세스할 수 없는 경우 [!DNL Assets] 배포(엔터프라이즈 네트워크에 없음).

이러한 유형의 통합은 다음 사용 사례에서 사용할 수 있습니다. 특히, 에 대한 직접 액세스 권한이 없는 사용자와 작업하는 경우 [!DNL Assets]:

* [!DNL Assets] 사용자는 다음과 같은 사용자와 특정 디지털 에셋 세트를 공유합니다. [!DNL Adobe Creative Cloud] 파일(예: 새 마케팅 활동을 위한 디자인 작업을 위해 크리에이티브 개요 및 승인된 에셋 세트).
* [!DNL Assets] 사용자는에서 생성한 새 파일을 받습니다. [!DNL Adobe Creative Cloud] 앱 사용자.

>[!NOTE]
>
>이 문서를 읽기 전에 전체 내용을 검토할 수 있습니다. [Experience Manager 및 Creative Cloud 통합 우수 사례](/help/assets/aem-cc-integration-best-practices.md) 를 참조하십시오.

## 개요 {#overview}

[!DNL Experience Manager] 끝 [!DNL Creative Cloud] 폴더 공유는 다음 기간 동안 폴더 및 파일을 서버측에서 공유합니다. [!DNL Assets] 및 [!DNL Creative Cloud] 계정. 다음을 사용하는 크리에이티브 전문가 [!DNL Creative Cloud] 데스크탑의 데스크탑 앱에서 공유 폴더를 를 사용하여 디스크에서 직접 사용할 수 있도록 설정할 수도 있습니다. [!DNL Adobe CreativeSync] 기술.

다음 다이어그램은 통합에 대한 개요를 제공합니다.

![chlimage_1-179](assets/chlimage_1-406.png)

통합에는 다음 요소가 포함됩니다.

* **[!DNL Experience Manager Assets]** 엔터프라이즈 네트워크(Managed Services 또는 온-프레미스)에 배포됨: 여기에서 폴더 공유가 시작됩니다.
* **[!DNL Adobe Experience Cloud Assets]핵심 서비스**: 를 중개하는 역할을 합니다 [!DNL Experience Manager] 및 [!DNL Creative Cloud] 스토리지 서비스. 통합을 사용하는 조직의 관리자는 Experience Cloud 조직과 [!DNL Assets] 배포. 또한 [승인된 Creative Cloud 협력자 목록 정의](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html), [!DNL Assets] 사용자는 추가 보안을 위해 폴더도 공유할 수 있습니다.

* **[!DNL Creative Cloud]Assets 웹 서비스** (스토리지 및 [!DNL Creative Cloud] file web UI): 여기에서 특정 Creative Cloud 앱 사용자를 관리할 수 있습니다. [!DNL Assets] 폴더가 공유되었습니다. 이(가) 초대를 수락하고 Creative Cloud 계정 저장소에 있는 폴더를 볼 수 있습니다.
* **Creative Cloud 데스크탑 앱**: (선택 사항) 와 동기화를 통해 크리에이티브 사용자의 데스크탑에서 공유 폴더/파일에 직접 액세스할 수 있습니다. [!DNL Creative Cloud] 에셋 스토리지.

## 특성 및 제한 사항 {#characteristics-and-limitations}

* **변경 사항의 단방향 전파:** 파일 변경 사항은 시스템에서 한 방향으로만 전파됩니다([!DNL Experience Manager] 또는 [!DNL Creative Cloud Assets]), 에셋이 원래 생성(업로드)된 위치입니다. 통합은 두 시스템 간에 완전히 자동화된 양방향 동기화를 제공하지 않습니다.
* **버전 관리:**

   * [!DNL Experience Manager] 에서 파일이 시작된 경우에만 업데이트에서 에셋의 버전을 만듭니다. [!DNL Experience Manager] 및 이(가) 거기서 업데이트됩니다.
   * [!DNL Creative Cloud] Assets는 자체 제공 [버전 관리 기능](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 진행 중인 작업 업데이트(기본적으로 최대 10일 동안 업데이트 저장)를 대상으로 합니다.

* **공간 제한:** 교환되는 파일의 크기와 볼륨은 다음에 따라 제한됩니다. [Creative Cloud 에셋 할당량](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 크리에이티브 사용자의 경우(구독 수준에 따라 다름) 및 최대 파일 크기가 5GB로 제한됩니다. 또한 공간은 조직이 Adobe Experience Cloud Assets 핵심 서비스에 보유한 에셋 할당량에 의해 제한됩니다.

* **공간 요구 사항:** 공유 폴더의 파일도 실제로 [!DNL Experience Manager] 다음 [!DNL Creative Cloud] 계정, 캐시된 사본 포함 [!DNL Experience Cloud Assets] 핵심 서비스.
* **네트워킹 및 대역폭:** 공유 폴더의 파일과 모든 업데이트는 시스템 간에 네트워크를 통해 전송되어야 합니다. 관련 파일과 업데이트만 공유되는지 확인합니다.
* **폴더 유형**: 공유 [!DNL Assets] 유형의 폴더 `sling:OrderedFolder`는 의 공유 컨텍스트에서 지원되지 않습니다. [!DNL Adobe Experience Cloud]. 폴더를 공유하려면에서 만들 때 [!DNL Assets], 을(를) 선택하지 마십시오. [!UICONTROL 주문됨] 옵션을 선택합니다.

## 우수 사례 {#best-practices}

사용 모범 사례 [!DNL Experience Manager] 끝 [!DNL Creative Cloud] 폴더 공유에는 다음이 포함됩니다.

* **볼륨 고려 사항:** [!DNL Experience Manager] 및 [!DNL Creative Cloud] 폴더 공유는 특정 캠페인이나 활동과 관련하여 더 적은 수의 파일을 공유하는 데 사용해야 합니다. 조직의 승인된 모든 에셋과 같이 더 큰 에셋 세트를 공유하려면 다른 분배 방법을 사용합니다(예: [!DNL Assets Brand Portal]) 또는 [!DNL Experience Manager] 데스크탑 앱입니다.
* **깊은 계층 구조를 공유하지 마십시오.** 공유는 재귀적으로 작동하며 선택적 공유를 허용하지 않습니다. 일반적으로 하위 폴더가 없거나 하나의 하위 폴더 수준과 같은 얕은 계층 구조를 가진 폴더만 공유하는 것으로 간주합니다.
* **단방향 공유를 위한 별도의 폴더:** 최종 자산을 공유할 때는 별도의 폴더를 사용해야 합니다. [!DNL Assets] 끝 [!DNL Creative Cloud] 파일 및 크리에이티브 준비가 끝난 에셋을 다시 공유할 수 있는 [!DNL Creative Cloud] 파일 위치: [!DNL Assets]. 이러한 폴더에 대한 좋은 이름 지정 규칙과 함께, 를 이해하기 쉬운 작업 환경을 만듭니다. [!DNL Assets] 및 [!DNL Creative Cloud] 비슷하게 사용합니다.
* **공유 폴더의 WIP 방지:** 공유 폴더는 진행 중인 작업에 사용해서는 안 됩니다. 파일을 자주 변경해야 하는 작업을 수행하려면 Creative Cloud 파일에 별도의 폴더를 사용하십시오.
* **공유 폴더 외부에서 새 작업 시작:** 새 디자인(크리에이티브 파일)은 Creative Cloud 파일의 개별 WIP 폴더에서 시작되어야 하며 공유할 준비가 되면 [!DNL Assets] 사용자는 공유 폴더로 이동하거나 저장해야 합니다.
* **공유 구조 단순화:** 관리 가능한 운영 설정을 만들려면 공유 구조를 단순화하는 것이 좋습니다. 모든 크리에이티브 사용자와 공유하는 대신, [!DNL Assets] 폴더는 크리에이티브 디렉터 또는 팀 관리자와 같은 팀 담당자와만 공유해야 합니다. 크리에이티브 쪽의 관리자는 최종 에셋을 수신하고 작업 할당을 결정한 다음 디자이너가 WIP 에셋의 자체 Creative Cloud 계정에서 작업할 수 있도록 합니다. Creative Cloud 공동 작업 기능을 사용하여 작업을 조정하고, 마지막으로 공유할 준비가 된 에셋을 선택한 다음 대상에 배치할 수 있습니다 [!DNL Assets] 을(를) 크리에이티브 준비가 완료된 공유 폴더로 복사합니다.

다음 다이어그램은에서 기존의 최종 자산을 기반으로 하는 디자인을 만들기 위한 예제 구성을 보여 줍니다 [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
