---
title: MSM을 사용하여 자산 재사용
description: 상위 자산에서 파생되고 상위 자산에 연결된 여러 페이지/폴더에 있는 자산을 사용합니다. 자산은 기본 복사본과 동기화되고 몇 번의 클릭만으로 상위 자산으로부터 업데이트를 받습니다.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '3367'
ht-degree: 0%

---


# [!DNL Assets] {#reuse-assets-using-msm-for-assets}에 MSM을 사용하여 에셋 재사용

[!DNL Adobe Experience Manager]의 MSM(Multi Site Manager) 기능을 사용하면 사용자가 한 번 작성되어 여러 웹 위치에서 다시 사용하는 컨텐츠를 재사용할 수 있습니다. [!DNL Assets] 기능에 대해 MSM과 동일한 디지털 자산을 사용할 수 있습니다. [!DNL Assets]에 MSM을 사용하면 다음을 수행할 수 있습니다.

* 자산을 한 번 만든 다음 이러한 자산의 사본을 만들어 사이트의 다른 영역에서 재사용할 수 있습니다.
* 여러 사본을 동기화하여 원본 기본 복사본을 한 번 업데이트하면 변경 내용을 하위 복사본에 적용할 수 있습니다.
* 상위 및 하위 자산 간의 연결을 일시적으로 또는 영구적으로 일시 중단하여 로컬 변경 작업을 수행합니다.

## 전제 조건 {#configprereq}

[!DNL Assets]에 MSM을 사용하려면 서비스 팩 1 이상을 설치하십시오. 자세한 내용은 [릴리스 노트](/help/release-notes/sp-release-notes.md)를 참조하십시오.

## 이점 및 개념 {#concepts} 이해

### 작동 방식과 이점 {#how-it-works-and-the-benefits}

여러 웹 위치에서 동일한 컨텐츠(텍스트 및 자산)를 재사용하기 위한 사용 시나리오를 이해하려면 [가능한 MSM 시나리오](/help/sites-administering/msm.md)를 참조하십시오. [!DNL Experience Manager] 원본 자산과 LC(Live Copy)라고 하는 연결된 복사본 간의 링크를 유지합니다. 유지 관리되는 링크를 사용하면 중앙 집중식 변경 사항을 많은 Live Copy로 푸시할 수 있습니다. 이렇게 하면 복제 사본 관리의 제한 없이 작업을 완료하면서 보다 신속하게 업데이트할 수 있습니다. 변경 사항의 전달은 오류 없이 중앙에서 이루어집니다. 이 기능을 사용하면 선택한 Live Copy로 제한된 업데이트를 사용할 수 있습니다. 사용자는 기본 복사본이 업데이트되고 변경 내용이 롤아웃될 때 덮어쓰지 않는 로컬 편집 및 연결이 끊어질 수 있습니다. 일부 특정 메타데이터 필드 또는 전체 자산에 대해 분리할 수 있습니다. 기본 복사본에서 원래 상속된 자산을 로컬에서 업데이트할 수 있는 유연성을 제공합니다.

MSM은 소스 에셋과 Live Copy 간에 라이브 관계를 유지하여 다음과 같은 이점을 제공합니다.

* 소스 에셋에 대한 변경 사항은 Live Copy에도 적용(롤아웃됨)되므로 Live Copy는 소스와 동기화됩니다.
* 라이브 관계를 일시 중단하거나 일부 제한된 필드에 대한 상속을 제거하여 Live Copy를 업데이트할 수 있습니다. 소스 수정 사항은 더 이상 Live Copy에 적용되지 않습니다.

### [!DNL Assets] 용어에 대한 MSM 용어 {#glossary}

**소스:** 원래 자산 또는 폴더입니다. Live Copy가 파생되는 기본 복사본입니다.

**Live Copy:** 소스 에셋/폴더와 해당 소스와 동기화되는 복사본. Live Copy는 추가 Live Copy의 소스가 될 수 있습니다. LC를 만드는 방법을 참조하십시오.

**상속:** Live Copy 자산/폴더와 시스템에서 업데이트를 보낼 위치를 기억하는 데 사용하는 소스 간의 링크/참조입니다. 상속은 메타데이터 필드에 대한 세부 수준으로 존재합니다. 소스와 Live Copy 간의 라이브 관계를 유지하면서 선택적 메타데이터 필드에 대한 상속을 제거할 수 있습니다.

**롤아웃:** 소스 다운스트림에 대한 수정 사항을 Live Copy로 푸시하는 작업입니다. 롤아웃 작업을 사용하여 한 번에 하나 이상의 Live Copy를 업데이트할 수 있습니다. 롤아웃을 참조하십시오.

**롤아웃 구성:** 동기화할 속성, 방법 및 시기를 결정하는 규칙입니다. 이러한 구성은 Live Copy를 만들 때 적용됩니다.나중에 편집할 수 있습니다.하위 멤버는 상위 자산에서 롤아웃 구성을 상속할 수 있습니다. [!DNL Assets]에 대한 MSM의 경우 표준 롤아웃 구성만 사용하십시오. 다른 롤아웃 구성은 [!DNL Assets]에 대해 MSM에 사용할 수 없습니다.

**동기화:** 롤아웃 외에 소스 및 Live Copy 간에 업데이트를 소스에서 Live Copy로 전송하여 동등성을 제공하는 또 다른 작업입니다. 특정 Live Copy에 대한 동기화가 시작되어 작업이 소스에서 변경 내용을 가져옵니다. 이 작업을 사용하면 Live Copy 중 하나만 업데이트할 수 있습니다. 동기화 작업을 참조하십시오.

**일시 중단:** Live Copy와 소스 에셋/폴더 간의 라이브 관계를 일시적으로 제거합니다. 관계를 다시 시작할 수 있습니다. 작업 일시 중단을 참조하십시오.

**재시작:** Live Copy가 소스에서 업데이트를 다시 받기 시작하도록 라이브 관계를 다시 시작합니다. 재시작 작업을 참조하십시오.

**재설정:** 재설정 작업을 수행하면 로컬 변경 사항을 덮어써서 Live Copy가 소스 복제본으로 다시 설정됩니다. 또한 상속 취소가 제거되고 모든 메타데이터 필드에 대한 상속이 재설정됩니다. 나중에 로컬 수정을 수행하려면 특정 필드의 상속을 다시 취소해야 합니다. LC의 로컬 수정을 참조하십시오.

**분리:** Live Copy 자산/폴더의 라이브 관계를 완전히 제거할 수 있습니다. 작업을 분리하면 Live Copy는 소스에서 업데이트를 받을 수 없으며 더 이상 Live Copy가 되지 않습니다. 관계 제거를 참조하십시오.

## 에셋 {#createlc} Live Copy 만들기

하나 이상의 소스 에셋 또는 폴더에서 Live Copy를 만들려면 다음 중 하나를 수행합니다.

* 방법 1:소스 자산을 선택하고 맨 위의 도구 모음에서 **[!UICONTROL 만들기]** > **[!UICONTROL Live Copy]**&#x200B;를 클릭합니다.
* 방법 2:[!DNL Experience Manager] 사용자 인터페이스에서 **[!UICONTROL 만들기]** > **[!UICONTROL Live Copy]**&#x200B;를 클릭합니다.

자산 또는 폴더의 Live Copy를 한 번에 만들 수 있습니다. 자산이나 Live Copy 자체인 폴더에서 파생된 Live Copy를 만들 수 있습니다. CF(컨텐츠 조각)는 사용 사례에 대해 지원되지 않습니다. Live Copy를 만들려고 하면 CF가 관계 없이 그대로 복사됩니다. 복사된 CF는 시간 내 스냅샷이며 원본 CF가 업데이트될 때 업데이트되지 않습니다.

첫 번째 방법을 사용하여 Live Copy를 만들려면 다음 단계를 수행합니다.

1. 소스 에셋 또는 폴더를 선택합니다. 도구 모음에서 **[!UICONTROL 만들기]** > **[!UICONTROL Live Copy]**&#x200B;를 클릭합니다.

   ![Experience Manager 인터페이스에서 Live Copy 만들기](assets/create_lc1.png)

   *그림:인터페이스에서 Live Copy를  [!DNL Experience Manager] 만듭니다.*

1. 대상 폴더를 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 제목과 이름을 입력합니다. 자산에 자식이 없습니다. 폴더의 Live Copy를 만들 때 하위 폴더를 포함하거나 제외하도록 선택할 수 있습니다.
1. 롤아웃 구성을 선택합니다. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

두 번째 방법을 사용하여 Live Copy를 만들려면 다음 단계를 수행합니다.

1. [!DNL Experience Manager] 인터페이스의 오른쪽 위 모서리에서 **[!UICONTROL 만들기]** > **[!UICONTROL Live Copy]**&#x200B;를 클릭합니다.

   ![Experience Manager 인터페이스에서 Live Copy 만들기](assets/create_lc2.png)

   *그림:인터페이스에서 Live Copy를  [!DNL Experience Manager] 만듭니다.*

1. 소스 에셋 또는 폴더를 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 대상 폴더를 선택합니다. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 제목과 이름을 입력합니다. 자산에 자식이 없습니다. 폴더의 Live Copy를 만들 때 하위 폴더를 포함하거나 제외하도록 선택할 수 있습니다.
1. 롤아웃 구성을 선택합니다. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

>[!NOTE]
>
>소스 또는 Live Copy를 이동하면 관계는 유지됩니다. Live Copy가 삭제되면 관계가 제거됩니다.

## 소스 및 Live Copy {#properties}의 다양한 속성과 상태 보기

관계, 동기화, 롤아웃 등과 같은 Live Copy의 정보 및 MSM 관련 상태를 [!DNL Experience Manager] 사용자 인터페이스의 다양한 영역에서 볼 수 있습니다.

다음 두 가지 방법은 자산 및 폴더에 대해 작동합니다.

* Live Copy 자산을 선택하고 속성 페이지에서 정보를 찾습니다.
* 소스 폴더를 선택하고 [!UICONTROL Live Copy 콘솔]에서 각 Live Copy의 세부 정보를 찾습니다.

>[!TIP]
>
>몇 개의 개별 Live Copy의 상태를 확인하려면 속성 페이지에 있는 첫 번째 방법을 사용합니다. 많은 Live Copy의 상태를 확인하려면 두 번째 방법(즉, **[!UICONTROL 관계 상태]** 페이지)을 참조하십시오.

### Live Copy {#statuslcasset} 정보 및 상태

Live Copy 자산 또는 폴더의 정보 및 상태를 확인하려면 다음 단계를 수행합니다.

1. Live Copy 에셋 또는 폴더를 선택합니다. 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다. 또는 키보드 단축키 `p`을 사용합니다.
1. **[!UICONTROL Live Copy]**&#x200B;를 클릭합니다. 소스 경로, 일시 중단 상태, 동기화 상태, 마지막 롤아웃 날짜 및 마지막 롤아웃을 수행한 사용자를 확인할 수 있습니다.

   ![Live Copy 정보 및 상태는 [속성]의 콘솔에 표시됩니다](assets/lcfolder_info_properties.png)

   *그림:Live Copy 정보 및 상태.*

1. 하위 자산이 Live Copy 구성을 대여한 경우 활성화하거나 비활성화할 수 있습니다.

1. Live Copy에 대한 옵션을 선택하여 상위에서 롤아웃 구성을 상속하거나 구성을 변경할 수 있습니다.

### 폴더 {#statuslcfolder} 의 모든 Live Copy 정보 및 상태

[!DNL Experience Manager] 에서는 소스 폴더의 모든 Live Copy의 동상을 확인할 수 있는 콘솔을 제공합니다. 이 콘솔에는 모든 하위 자산의 상태가 표시됩니다.

1. 소스 폴더를 선택합니다. 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다. 또는 키보드 단축키 `p`을 사용합니다.
1. **[!UICONTROL Live Copy 소스]**&#x200B;를 클릭합니다. 콘솔을 열려면 **[!UICONTROL Live Copy 개요]**&#x200B;를 클릭합니다. 이 대시보드는 모든 하위 자산의 최상위 상태를 제공합니다.

   ![소스의 Live Copy 콘솔에서 Live Copy 상태 보기](assets/livecopy-statuses.png)

   *그림:소스의  [!UICONTROL Live Copy 콘솔에서 Live ] Copy 상태 보기*

1. Live Copy 폴더의 각 자산에 대한 자세한 정보를 보려면 자산을 선택하고 도구 모음에서 **[!UICONTROL 관계 상태]**&#x200B;를 클릭합니다.

   ![폴더에 있는 Live Copy 하위 자산의 세부 정보 및 상태](assets/livecopy_relationship_status.png)

   폴더에 있는 Live Copy 하위 자산의 세부 정보 및 상태

>[!TIP]
>
>너무 많이 찾아보지 않고도 다른 폴더의 Live Copy 상태를 빠르게 볼 수 있습니다. **[!UICONTROL Live Copy 개요]** 인터페이스의 위쪽 중간에 있는 팝업 목록의 폴더를 변경하기만 하면 됩니다.

### 소스 {#refrailsource}에 대한 참조 레일의 빠른 작업

소스 에셋 또는 폴더의 경우 다음 정보를 보고 참조 레일에서 바로 다음 작업을 수행할 수 있습니다.

* Live Copy 경로를 참조하십시오.
* [!DNL Experience Manager] 사용자 인터페이스에서 특정 Live Copy를 열거나 표시합니다.
* 업데이트를 특정 Live Copy에 동기화합니다.
* 특정 Live Copy에 대한 관계를 일시 중단하거나 롤아웃 구성을 변경합니다.
* Live Copy 개요 콘솔에 액세스합니다.

소스 에셋 또는 폴더를 선택하고 왼쪽 레일을 연 다음 **[!UICONTROL 참조]**&#x200B;를 클릭합니다. 또는 에셋 또는 폴더를 선택하고 키보드 단축키 `Alt + 4`을 사용합니다.

![선택한 소스의 참조 레일에서 사용할 수 있는 작업 및 정보](assets/referencerail_source.png)

*그림:선택한 소스의 참조 레일에서 사용할 수 있는 작업 및 정보.*

특정 Live Copy의 경우 **[!UICONTROL Edit Live Copy]**&#x200B;를 클릭하여 관계를 일시 중단하거나 롤아웃 구성을 변경합니다.

![특정 Live Copy의 경우 소스 에셋을 선택하면 참조 레일에서 관계를 일시 중단하거나 롤아웃 구성을 변경할 수 있습니다](assets/referencerail_editlc_options.png)

*그림:관계를 일시 중단하거나 특정 Live Copy의 롤아웃 구성을 변경합니다.*

### Live Copy {#refraillc}에 대한 참조 레일의 빠른 작업

Live Copy 자산 또는 폴더의 경우 다음 정보를 보고 참조 레일에서 바로 다음 작업을 수행할 수 있습니다.

* 소스 경로를 참조하십시오.
* [!DNL Experience Manager] 사용자 인터페이스에서 특정 Live Copy를 열거나 표시합니다.
* 업데이트를 롤아웃합니다.

Live Copy 에셋 또는 폴더를 선택하고 왼쪽 레일을 열고 **[!UICONTROL 참조]**&#x200B;를 클릭합니다. 또는 에셋 또는 폴더를 선택하고 키보드 단축키 `Alt + 4`을 사용합니다.

![선택한 Live Copy에 대한 참조 레일에서 사용할 수 있는 작업](assets/referencerail_livecopy.png)

*그림:선택한 Live Copy에 대한 참조 레일에서 사용할 수 있는 작업입니다.*

## 소스에서 Live Copy로 수정 내용 전달 {#rolloutsync}

소스가 수정되면 동기화 작업 또는 롤아웃 작업을 사용하여 변경 사항을 Live Copy에 전파할 수 있습니다. 두 작업 간의 차이를 이해하려면 [용어집](#glossary)을 참조하십시오.

### 롤아웃 작업 {#rollout}

소스 자산에서 롤아웃 작업을 시작하고 전체 또는 몇 개의 Live Copy를 업데이트할 수 있습니다.

1. Live Copy 에셋 또는 폴더를 선택합니다. 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다. 또는 키보드 단축키 `p`을 사용합니다.
1. **[!UICONTROL Live Copy 소스]**&#x200B;를 클릭합니다. 맨 위의 도구 모음에서 **[!UICONTROL 롤아웃]**&#x200B;을 클릭합니다.
1. 업데이트할 Live Copy를 선택합니다. **[!UICONTROL 롤아웃]**&#x200B;을 클릭합니다. 하위 자산에 대한 업데이트를 롤아웃하려면 **[!UICONTROL 롤아웃 소스 및 모든 하위]**&#x200B;를 선택합니다.

   ![소스의 수정 내용을 일부 또는 전체 Live Copy로 롤아웃합니다.](assets/livecopy_rollout_page.png)

   *그림:소스의 수정 내용을 일부 또는 전체 Live Copy로 롤아웃합니다.*

>[!NOTE]
>
>소스 자산에서 수정한 사항은 직접 관련된 Live Copy에만 롤아웃됩니다. Live Copy가 다른 Live Copy에서 파생된 경우, 수정 사항은 파생된 Live Copy로 롤아웃되지 않습니다.

또는 특정 Live Copy를 선택한 후 참조 레일에서 롤아웃 작업을 시작할 수 있습니다. 자세한 내용은 Live Copy[에 대한 참조 레일의 빠른 작업을 참조하십시오. ](#refraillc) 이 롤아웃 방식에서는 선택한 Live Copy 및 선택적으로 해당 하위 Live Copy만 업데이트됩니다.

![소스의 수정 내용을 선택한 Live Copy에 롤아웃합니다.](assets/livecopy_rollout_dialog.png)

*그림:소스의 수정 내용을 선택한 Live Copy에 롤아웃합니다.*

### 동기화 작업 {#aboutsync} 정보

동기화 작업은 소스 수정 내용을 선택한 Live Copy에만 가져옵니다. 동기화 작업은 상속을 취소한 후 수행한 로컬 수정 내용을 존중하고 유지합니다. 로컬 수정 내용을 덮어쓰지 않고 취소된 상속이 다시 설정되지 않습니다. 3가지 방법으로 동기화 작업을 시작할 수 있습니다.

| [!DNL Experience Manager] 인터페이스에서 위치 | 사용 시기 및 이유 | 사용 방법 |
|---|---|---|
|  참조레일 | 소스를 이미 선택한 경우 신속하게 동기화할 수 있습니다. | 소스[에 대한 참조 레일의 빠른 작업을 참조하십시오.](#refrailsource) |
| [!UICONTROL 속성] 페이지의 도구 모음 | Live Copy 속성이 이미 열려 있으면 동기화를 시작합니다. | [Live Copy 동기화](#synclc)를 참조하십시오. |
| [!UICONTROL Live Copy ] 개요 콘솔 | 소스 폴더를 선택하거나 [!UICONTROL Live Copy 개요] 콘솔이 이미 열려 있을 때 여러 자산을 신속하게 동기화할 수 있습니다(반드시 모든 것이 아닙니다). 한 번에 하나의 자산에 대해 동기화 작업이 시작되지만 한 번에 여러 자산에 대해 빠르게 동기화할 수 있습니다. | Live Copy 폴더[에 있는 많은 자산에 대한 작업을 참조하십시오.](#bulkactions) |

### Live Copy 동기화 {#synclc}

동기화 작업을 시작하려면 Live Copy의 **[!UICONTROL 속성]** 페이지를 열고 **[!UICONTROL Live Copy]**&#x200B;를 클릭한 다음 도구 모음에서 원하는 작업을 클릭합니다.

동기화 작업과 관련된 상태 및 정보를 보려면 [Live Copy](#statuslcasset) 및 [폴더](#statuslcfolder)의 모든 Live Copy의 정보 및 상태를 참조하십시오.

![동기화 작업은 변경 내용을 소스에 가져옵니다.](assets/livecopy_sync.png)

*그림:동기화 작업은 변경 내용을 소스에 가져옵니다.*

>[!NOTE]
>
>관계가 일시 중단된 경우 동기화 작업은 도구 모음에서 사용할 수 없습니다. 동기화 작업을 참조 레일에서 사용할 수 있지만, 수정 내용은 성공적인 롤아웃 시에도 전파되지 않습니다.

## 관계 일시 중단 및 다시 시작 {#suspendresume}

Live Copy가 소스 에셋 또는 폴더에 대한 수정 내용을 수신하지 못하도록 관계를 일시적으로 중단할 수 있습니다. 또한 Live Copy에서 소스에서 수정 내용을 받기 시작하기 위해 관계를 다시 시작할 수 있습니다.

일시 중단하거나 다시 시작하려면 Live Copy의 **[!UICONTROL 속성]** 페이지를 열고 **[!UICONTROL Live Copy]**&#x200B;를 클릭한 다음 도구 모음에서 원하는 작업을 클릭합니다.

또는 **[!UICONTROL Live Copy 개요]** 콘솔에서 Live Copy 폴더에 있는 여러 자산의 관계를 신속하게 일시 중단하거나 다시 시작할 수 있습니다. 자세한 내용은 [Live copy 폴더](#bulkactions)의 많은 자산에 대한 작업 수행을 참조하십시오.

## Live Copy {#localmods} 로컬 수정

Live Copy는 소스 생성 시 원본 소스의 복제본입니다. Live Copy의 메타데이터 값은 소스에서 상속됩니다. 메타데이터 필드는 소스 자산의 각 필드에 따라 상속을 개별적으로 유지합니다.

그러나 일부 선택 속성을 변경할 수 있도록 Live Copy의 로컬 수정 작업을 유연하게 수행할 수 있습니다. 로컬 수정을 수행하려면 원하는 속성의 상속을 취소합니다. 하나 이상의 메타데이터 필드의 상속이 취소되면 자산의 라이브 관계와 다른 메타데이터 필드의 상속이 유지됩니다. 모든 동기화 또는 롤아웃은 로컬 수정 내용을 덮어쓰지 않습니다. 이렇게 하려면 Live Copy 자산의 **[!UICONTROL 속성]** 페이지를 열고 메타데이터 필드 옆에 있는 **[!UICONTROL 상속 취소]** 옵션을 클릭합니다.

로컬 수정 내용을 모두 취소하고 에셋을 소스 상태로 되돌릴 수 있습니다. 작업을 전적으로 재설정하고 모든 로컬 수정 내용을 즉시 무시하고 모든 메타데이터 필드에 상속을 재설정합니다. 되돌리려면 Live Copy 자산의 **[!UICONTROL 속성]** 페이지에서 도구 모음에서 **[!UICONTROL 재설정]**&#x200B;을 클릭합니다.

![동작을 재설정하면 로컬 편집 내용을 덮어쓰고 Live Copy를 소스와 함께 가져옵니다.](assets/livecopy_reset.png)

*그림:동작을 재설정하면 로컬 편집 내용을 덮어쓰고 Live Copy를 소스와 함께 가져옵니다.*

## 라이브 관계 제거 {#detach}

분리 작업을 사용하여 소스와 Live Copy 간의 관계를 완전히 제거할 수 있습니다. Live Copy가 분리된 후 독립형 에셋 또는 폴더가 됩니다. 분리 후 즉시 [!DNL Experience Manager] 인터페이스에 새 에셋으로 표시됩니다. Live Copy를 소스에서 분리하려면 다음 단계를 수행합니다.

1. Live Copy 에셋 또는 폴더를 선택합니다. 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다. 또는 키보드 단축키 `p`을 사용합니다.

1. **[!UICONTROL Live Copy]**&#x200B;를 클릭합니다. 도구 모음에서 **[!UICONTROL 분리]**&#x200B;를 클릭합니다. 표시된 대화 상자에서 **[!UICONTROL 분리]**&#x200B;를 클릭합니다.

   ![작업을 분리하면 소스 및 Live Copy 간의 관계가 완전히 제거됩니다.](assets/livecopy_detach.png)

   *그림:작업을 분리하면 소스 및 Live Copy 간의 관계가 완전히 제거됩니다.*

   >[!CAUTION]
   >
   >대화 상자에서 **[!UICONTROL 분리]**&#x200B;를 클릭하면 해당 관계가 즉시 제거됩니다. 속성 페이지에서 **[!UICONTROL 취소]**&#x200B;를 클릭하면 실행 취소할 수 없습니다.

또는 **[!UICONTROL Live Copy 개요]** 콘솔에서 Live Copy 폴더에 있는 여러 자산을 빠르게 분리할 수 있습니다. 자세한 내용은 [Live copy 폴더](#bulkactions)의 많은 자산에 대한 작업 수행을 참조하십시오.

## Live Copy 폴더 {#bulkactions}에 있는 많은 자산에 대해 작업 수행

하나의 Live Copy 폴더에 여러 개의 자산이 있는 경우 각 자산에 대해 작업을 시작하는 것은 지루할 수 있습니다. [!UICONTROL Live Copy 콘솔]에서 많은 자산에 대한 기본 작업을 빠르게 시작할 수 있습니다. 위의 메서드는 개별 자산에 대해 계속 작동합니다.

1. 소스 폴더를 선택합니다. 도구 모음에서 **[!UICONTROL 속성]**&#x200B;을 클릭합니다. 또는 키보드 단축키 `p`을 사용합니다.
1. **[!UICONTROL Live Copy 소스]**&#x200B;를 클릭합니다. 콘솔을 열려면 **[!UICONTROL Live Copy 개요]**&#x200B;를 클릭합니다.
1. 이 대시보드의 Live Copy 폴더에서 Live Copy 자산을 선택합니다. 도구 모음에서 원하는 작업을 클릭합니다. 사용 가능한 작업은 **[!UICONTROL 동기화]**, **[!UICONTROL 재설정]**, **[!UICONTROL 일시 중단]** 및 **[!UICONTROL 분리]**&#x200B;입니다. 선택한 소스 폴더와 라이브 관계에 있는 Live Copy 폴더의 모든 에셋에서 이러한 작업을 신속하게 시작할 수 있습니다.

   ![Live Copy 개요 콘솔에서 Live Copy 폴더의 많은 에셋을 손쉽게 업데이트](assets/livecopyconsole_update_many_assets.png)

   *그림:Live Copy Overviewconsole에서 Live Copy 폴더의 많은  [!UICONTROL 에셋을 손쉽게 업데이트할 ] 수 있습니다.*

## [!DNL Assets] {#extendapi}에 대해 MSM 확장

[!DNL Experience Manager] MSM Java API를 사용하여 기능을 확장할 수 있습니다. [!DNL Assets]의 경우, 확장은 [!DNL Sites]에 대해 MSM에서 작동하는 것과 동일하게 작동합니다. 자세한 내용은 [MSM](/help/sites-developing/extending-msm.md) 확장 및 특정 작업에 대한 자세한 내용은 다음을 참조하십시오.

* [API 개요](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [새 동기화 작업 만들기](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [새 롤아웃 구성 만들기](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [간단한 LiveActionFactory 클래스 만들기 및 사용](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

>[!NOTE]
>
>* [!DNL Sites]에 대한 MSM의 블루프린트는 [!DNL Assets]에 대해 MSM의 Live Copy 소스라고 합니다.
>* 사이트 만들기 마법사에서 장 단계를 제거하는 것은 [!DNL Assets]에 대한 MSM에서 지원되지 않습니다.
>* 페이지 속성(터치가 활성화된 UI)에서 MSM 잠금 구성은 [!DNL Assets]에 대한 MSM에서 지원되지 않습니다.


## 자산 관리 작업이 Live Copy {#manageassets}에 미치는 영향

Live Copy와 소스는 디지털 자산으로서 어느 정도 관리할 수 있는 자산 또는 폴더입니다. [!DNL Experience Manager]의 일부 에셋 관리 작업은 Live Copy에 특정 영향을 줍니다.

* Live Copy를 복사하면 첫 번째 Live Copy와 동일한 소스의 Live Copy 에셋이 생성됩니다.
* 소스 또는 Live Copy를 이동하면 라이브 관계가 유지됩니다.
* Live Copy 자산에 대해 편집 작업이 작동하지 않습니다. Live Copy의 소스가 Live Copy 자체인 경우 편집 작업은 해당 사본에서 작동하지 않습니다.
* Live Copy 자산에 대해 체크아웃 작업을 사용할 수 없습니다.
* 소스 폴더의 경우 검토 작업을 만드는 옵션을 사용할 수 있습니다.
* 목록 보기 및 열 보기에서 자산 목록을 볼 때 Live Copy 자산 또는 폴더에 그에 대한 &#39;live copy&#39;가 표시됩니다. 이렇게 하면 폴더에 있는 Live Copy를 쉽게 식별할 수 있습니다.

## [!DNL Assets] 및 [!DNL Sites] {#comparison}에 대한 MSM 비교

더 많은 시나리오에서 [!DNL Assets]에 대한 MSM은 사이트에 대한 MSM 기능과 일치합니다. 메모의 주요 차이점은 다음과 같습니다.

* [!DNL Sites]에 대한 MSM의 블루프린트는 [!DNL Assets]에 대해 MSM의 Live Copy 소스라고 합니다.
* 사이트에서 블루프린트와 Live Copy를 비교할 수는 있지만 [!DNL Assets]에서는 소스를 Live Copy와 비교할 수는 없습니다.
* [!DNL Assets]에서는 Live Copy를 편집할 수 없습니다.
* 사이트에는 보통 하위 항목이 있지만 [!DNL Assets]은(는) 없습니다. 개별 자산의 Live Copy를 만들 때 자식을 포함하거나 제외하는 옵션이 없습니다.
* 사이트 만들기 마법사에서 장 단계를 제거하는 것은 [!DNL Assets]에 대한 MSM에서 지원되지 않습니다.
* 페이지 속성에서 MSM 잠금 구성(터치가 활성화된 UI)은 [!DNL Assets]에 대한 MSM에서 지원되지 않습니다.
* [!DNL Assets]에 대한 MSM의 경우 **[!UICONTROL 표준 롤아웃 구성]**&#x200B;만 사용하십시오. 다른 롤아웃 구성은 [!DNL Assets]에 대해 MSM에 사용할 수 없습니다.

## 우수 사례 {#bestpractices}

MSM에 대한 일부 우수 사례는 다음과 같습니다.

* 구현을 시작하기 전에 자산 및 컨텐츠 흐름의 상위-하위 관계를 계획합니다.

## [!DNL Assets] {#limitations}에 대한 MSM의 제한 사항 및 알려진 문제

다음은 [!DNL Assets]에 대한 MSM의 제한 사항입니다.

* CF(컨텐츠 조각)는 사용 사례에 대해 지원되지 않습니다. Live Copy를 만들려고 하면 CF가 관계 없이 그대로 복사됩니다. 복사된 CF는 시간 내 스냅샷이며 원본 CF가 업데이트될 때 업데이트되지 않습니다.
