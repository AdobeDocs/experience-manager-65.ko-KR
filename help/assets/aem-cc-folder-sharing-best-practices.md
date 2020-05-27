---
title: Adobe Experience Manager를 Adobe Creative Cloud 폴더 공유 모범 사례
description: Experience Manager Assets의 사용자가 Adobe Creative Cloud(CC) 사용자와 폴더를 교환할 수 있도록 Adobe Experience Manager를 구성합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---


# Adobe Experience Manager를 Adobe Creative Cloud 폴더 공유 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Experience Manager to Creative Cloud Folder Sharing 기능은 더 이상 사용되지 않습니다. Adobe에서는 [Adobe Asset Link](https://helpx.adobe.com/kr/enterprise/using/adobe-asset-link.html) 또는 [Experience Manager 데스크탑 앱과 같은 최신 기능을 사용할 것을 적극 권장합니다](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Experience Manager [및 Creative Cloud 통합 모범 사례를](/help/assets/aem-cc-integration-best-practices.md)참조하십시오.

Adobe Experience Manager를 Assets 사용자가 Adobe Creative Cloud 앱 사용자와 폴더를 공유할 수 있도록 구성하여 Adobe Creative Cloud Assets 서비스에서 공유 폴더로 사용할 수 있습니다. 이 기능을 사용하여 크리에이티브 팀과 자산 사용자 간에 파일을 교환할 수 있습니다. 특히 크리에이티브 사용자가 자산 인스턴스에 액세스할 수 없는 경우(기업 네트워크에 있지 않음)

이러한 유형의 통합은 다음 사용 사례에서 특히 자산에 직접 액세스하지 않는 사용자와 작업할 때 사용할 수 있습니다.

* 자산 사용자가 Adobe Creative Cloud Files 사용자와 특정 자산 세트를 공유합니다(예: 새 마케팅 활동을 위한 디자인 작업을 위해 승인된 자산 집합).
* 에셋 사용자는 Adobe Creative Cloud 앱 사용자가 만든 새 파일을 받습니다.

>[!NOTE]
>
>이 문서를 읽기 전에 전체 [Experience Manager와 Creative Cloud 통합 모범 사례를](/help/assets/aem-cc-integration-best-practices.md) 검토하여 주제에 대한 개요를 살펴볼 수 있습니다.

## 개요 {#overview}

Adobe Experience Manager와 Creative Cloud 폴더 공유는 자산과 Creative Cloud 계정 간에 폴더 및 파일을 서버측에서 공유하는 것에 의존합니다. 데스크탑에서 Creative Cloud 데스크탑 앱을 사용하는 크리에이티브 전문가는 Adobe CreativeSync 기술을 사용하여 자신의 디스크에서 바로 공유 폴더를 이용할 수 있도록 할 수 있습니다.

다음 다이어그램은 통합에 대한 개요를 제공합니다.

![chlimage_1-179](assets/chlimage_1-406.png)

통합에는 다음 요소가 포함됩니다.

* **엔터프라이즈 네트워크에 배포된 Experience Manager Assets 서버** (관리 서비스 또는 온-프레미스): 폴더 공유가 여기에서 시작됩니다.
* **Adobe Marketing Cloud Assets 핵심 서비스**: Adobe Experience Manager와 Creative Cloud 스토리지 서비스 간의 중간 역할을 수행합니다. 통합을 사용하는 회사의 관리자는 Marketing Cloud 조직과 자산 인스턴스 간에 신뢰 관계를 설정해야 합니다. 또한 자산 사용자가 추가 보안을 위해 폴더를 공유할 수 있도록 승인된 Creative Cloud 협력자 [목록을](https://marketing.adobe.com/resources/help/en_US/mcloud/t_admin_add_cc_user.html)정의합니다.

* **Creative Cloud Assets 웹 서비스** (스토리지 및 Creative Cloud Files 웹 UI): 여기에서 에셋 폴더를 공유한 특정 Creative Cloud 앱 사용자는 초대를 수락할 수 있으며 Creative Cloud 계정 저장소의 폴더를 볼 수 있습니다.
* **Creative Cloud 데스크탑 앱**: (선택 사항) Creative Cloud Assets 저장소와 동기화를 통해 크리에이티브 사용자의 데스크탑에서 공유 폴더/파일에 직접 액세스할 수 있습니다.

## 특성 및 제한 사항 {#characteristics-and-limitations}

* **변경 사항의 단방향 전파:** 파일 변경 사항은 자산을 원래 제작(업로드됨)한 시스템(Experience Manager 또는 Creative Cloud Assets)에서 한 방향으로만 전파됩니다. 통합에서는 두 시스템 간의 완전 자동 양방향 동기화를 제공하지 않습니다.
* **버전 관리:**

   * Adobe Experience Manager는 파일이 Experience Manager에서 생성되었고 업데이트되는 경우에만 업데이트 시 자산의 버전만 만듭니다.
   * Creative Cloud Assets는 진행 중인 작업 [업데이트(기본적으로 최대 10일 동안 업데이트 저장)를 대상으로 하는 고유한 버전 관리 기능을](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 제공합니다

* **공간 제한:** 교환된 파일의 크기와 용량은 크리에이티브 사용자를 위한 특정 [Creative Cloud Assets 할당량](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) (구독 수준에 따라 다름)에 의해 제한되며 최대 파일 크기는 5GB로 제한됩니다. 공간이 Adobe Marketing Cloud Assets 핵심 서비스에 있는 자산 할당량에 따라 추가로 제한됩니다.

* **공간 요구 사항:** 또한 공유 폴더의 파일은 Experience Manager에 물리적으로 저장한 다음 Creative Cloud 계정에 저장되어야 하며 Marketing Cloud Assets 핵심 서비스의 캐시된 복사본입니다.
* **네트워킹 및 대역폭:** 공유 폴더의 파일과 모든 업데이트를 시스템 간에 네트워크를 통해 전송해야 합니다. 관련 파일 및 업데이트만 공유되도록 해야 합니다.
* **폴더 유형**: 해당 유형의 자산 폴더 `sling:OrderedFolder`는 Adobe Marketing Cloud에서 공유하는 컨텍스트에서 지원되지 않습니다. 폴더를 공유하려는 경우 자산에서 폴더를 만들 때 [정렬됨] 옵션을 선택하지 마십시오.

## Best practices {#best-practices}

Adobe Experience Manager를 Creative Cloud 폴더 공유에 활용하는 모범 사례에는 다음이 포함됩니다.

* **볼륨 고려 사항:** Adobe Experience Manager/Creative Cloud 폴더 공유를 사용하면 특정 캠페인 또는 활동과 관련된 더 적은 수의 파일을 공유할 수 있습니다. 조직에서 승인된 모든 자산과 같이 더 큰 자산 세트를 공유하려면 다른 배포 방법(예: 자산 브랜드 포털) 또는 Experience Manager 데스크탑 앱을 사용하십시오.

* **계층 공유 방지:** 공유는 반복적으로 작동하며 선택적 공유를 허용하지 않습니다. 일반적으로 하위 폴더가 없거나 하위 폴더 수준 1과 같이 매우 낮은 계층 구조를 가진 폴더만 공유하는 것으로 간주됩니다.
* **단방향 공유를 위한 개별 폴더:** 최종 에셋을 Creative Cloud 파일에 공유하고 Creative Cloud 파일에서 에셋으로 되돌아가는 크리에이티브 에셋을 공유하려면 별도의 폴더를 사용해야 합니다. 이러한 폴더에 대한 훌륭한 명명 규칙과 함께, 자산 및 Creative Cloud 사용자 모두를 위한 이해하기 쉬운 작업 환경을 만듭니다.
* **공유 폴더의 WIP 방지:** 진행 중인 작업에 공유 폴더를 사용할 수 없습니다. 파일을 자주 변경해야 하는 작업을 수행하려면 Creative Cloud 파일의 별도의 폴더를 사용하십시오.
* **공유 폴더 외부에서 새 작업 시작:** 새 디자인(크리에이티브 파일)은 Creative Cloud 파일의 별도의 WIP 폴더에서 시작해야 하며, Assets 사용자와 공유할 준비가 되었으면 공유 폴더로 이동하거나 저장해야 합니다.
* **공유 구조 간소화:** 더욱 관리가 용이한 운영 체제를 원한다면 공유 구조를 단순화하는 것이 좋습니다. 모든 크리에이티브 사용자와 공유하는 대신 에셋 폴더는 크리에이티브 디렉터나 팀 관리자와 같은 팀 담당자만 공유해야 합니다. 크리에이티브 팀의 관리자는 최종 자산을 받고 작업 할당을 결정한 다음 디자이너가 WIP 자산에 대해 자신의 Creative Cloud 계정에서 작업을 할 수 있도록 합니다. Creative Cloud 공동 작업 기능을 사용하여 작업을 조정하고, Assets로 다시 공유할 준비가 된 에셋을 선택하여 크리에이티브한 공유 폴더로 가져올 수 있습니다.

다음 다이어그램은 자산의 기존 최종 자산을 기반으로 새 디자인을 만들기 위한 예제 구성을 보여줍니다.

![chlimage_1-180](assets/chlimage_1-407.png)
