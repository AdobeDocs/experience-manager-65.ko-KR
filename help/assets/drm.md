---
title: 에셋 Digital Rights Management
description: ' [!DNL Experience Manager]에서 사용 허가된 자산에 대한 자산 만료 상태 및 정보를 관리하는 방법을 알아봅니다.'
contentOwner: AG
role: User, Admin
feature: DRM,Asset Management
exl-id: a49cfd25-e8d9-492f-be5e-acab0cf67a28
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 8%

---

# 자산용 Digital Rights Management {#digital-rights-management-in-assets}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/drm.html?lang=en) |
| AEM 6.5 | 이 문서 |

디지털 에셋은 종종 사용 약관 및 기간을 지정하는 라이선스와 연결됩니다. [!DNL Adobe Experience Manager Assets]은(는) [!DNL Experience Manager] 플랫폼과 완전히 통합되므로 자산 만료 정보 및 자산 상태를 효율적으로 관리할 수 있습니다. 라이선스 정보를 자산과 연결할 수도 있습니다.

## 에셋 만료 {#asset-expiration}

에셋 만료는 에셋에 대한 라이선스 요구 사항을 적용할 수 있는 효과적인 방법입니다. 게시된 에셋이 만료되면 게시 취소되므로 라이센스 위반 가능성을 방지할 수 있습니다. 관리자 권한이 없는 사용자는 만료된 에셋을 편집, 복사, 이동, 게시 및 다운로드할 수 없습니다.

카드 보기와 목록 보기 모두에서 [!DNL Assets] 콘솔에서 에셋의 만료 상태를 볼 수 있습니다.

![expired_flag_list](assets/expired_flag_list.png)

*그림: 목록 보기에서 [!UICONTROL 상태] 열은 [!UICONTROL 만료됨] 배너를 표시합니다.*

왼쪽 레일의 [!UICONTROL 타임라인]에서 자산의 만료 상태를 볼 수 있습니다.

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>시간대가 다른 사용자에 대해 에셋의 만료 날짜가 다르게 표시됩니다.

**[!UICONTROL 참조]** 레일에서 자산의 만료 상태를 볼 수도 있습니다. 복합 에셋과 참조된 하위 에셋, 컬렉션 및 프로젝트 간의 에셋 만료 상태 및 관계를 관리합니다.

1. 참조 웹 페이지 및 복합 자산을 보려는 자산으로 이동합니다.
1. 자산을 선택하고 왼쪽 레일에서 **[!UICONTROL 참조]**&#x200B;를 엽니다. 만료된 에셋의 경우 [!UICONTROL 참조] 레일이 맨 위에 만료 상태 **[!UICONTROL 에셋이 만료됨]**&#x200B;을(를) 표시합니다.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   에셋이 만료된 경우 [!UICONTROL 참조] 레일에 **[!UICONTROL 에셋이 만료된 하위 Assets]** 상태가 표시됩니다.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### 만료된 에셋 검색 {#search-expired-assets}

검색 패널에서 만료된 하위 에셋을 포함하여 만료된 에셋을 검색할 수 있습니다.

1. [!DNL Assets] 콘솔에서 도구 모음의 **[!UICONTROL 검색]**&#x200B;을 클릭하여 Omnisearch 상자를 표시합니다.

1. Omnisearch 상자에 커서를 놓고 `Enter` 키를 선택하여 검색 결과 페이지를 표시합니다.
1. 왼쪽 레일에서 검색 패널을 엽니다. **[!UICONTROL 만료 상태]** 옵션을 클릭하여 확장합니다.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. **[!UICONTROL 만료됨]**&#x200B;을(를) 선택하십시오. 검색 결과를 필터링하면 만료된 에셋만 표시됩니다.

**[!UICONTROL 만료됨]** 옵션을 선택하면 [!DNL Assets] 콘솔에는 복합 에셋에서 참조하는 만료된 에셋 및 하위 에셋만 표시됩니다. 만료된 하위 에셋을 참조하는 복합 에셋은 하위 에셋이 만료된 직후에 표시되지 않습니다. 대신 [!DNL Experience Manager]이(가) 다음에 스케줄러를 실행할 때 만료된 하위 자산을 참조하고 있음을 감지하면 표시됩니다.

게시된 에셋의 만료 날짜를 현재 스케줄러 주기보다 빠른 날짜로 수정하는 경우 스케줄은 다음에 이 에셋을 실행할 때 만료된 에셋으로 계속 감지하고 상태에 맞게 을 반영합니다.

또한 사소한 결함이나 오류로 인해 스케줄러가 현재 주기에서 만료된 에셋을 감지할 수 없는 경우 스케줄러는 다음 주기에서 이러한 에셋을 다시 검사하고 만료된 상태를 감지합니다.

[!DNL Assets] 콘솔에서 만료된 하위 자산과 함께 참조 복합 자산을 표시할 수 있도록 하려면 [!DNL Experience Manager] Configuration Manager에서 **[!UICONTROL Adobe CQ DAM 만료 알림]** 워크플로우를 구성하십시오.

1. [!DNL Experience Manager] 구성 관리자를 엽니다.
1. **[!UICONTROL Adobe CQ DAM 만료 알림]**&#x200B;을 선택합니다. 기본적으로 **[!UICONTROL 시간 기반 스케줄러]**&#x200B;가 선택되어 있으며, 이 스케줄러는 자산이 만료된 하위 자산인지 특정 시간에 확인하도록 작업을 예약합니다. 작업이 완료되면 만료된 하위 에셋 및 참조된 에셋이 검색 결과에 만료된 것으로 표시됩니다.

1. To run the job periodically, clear the **[!UICONTROL Time Based Scheduler Rule]** field and modify the time in seconds in the **[!UICONTROL Periodic Scheduler]** field. 예를 들어 표현식 `0 0 0 * * ?`의 예는 00시간에 작업을 트리거합니다.
1. 자산이 만료되면 이메일을 받으려면 **[!UICONTROL 이메일 보내기]**&#x200B;를 선택하십시오.

   >[!NOTE]
   >
   >에셋이 만료되면 에셋 작성자(특정 에셋을 [!DNL Assets]에 업로드하는 사람)만 이메일을 받습니다. 전체 [!DNL Experience Manager] 수준에서 전자 메일 알림 구성에 대한 자세한 내용은 [전자 메일 알림을 구성하는 방법](/help/sites-administering/notification.md)을 참조하십시오.

1. **[!UICONTROL 이전 알림(초)]** 필드에서 만료와 관련된 알림을 받으려면 자산이 만료되기 전 시간을 초 단위로 지정합니다. 에셋 생성자는 에셋이 만료되기 전에 지정된 시간 이후에 만료될 것임을 알리는 메시지를 수신합니다. 자산이 만료된 후 만료를 확인하는 다른 알림을 받게 됩니다. 또한 만료된 에셋은 비활성화됩니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 자산 상태 {#asset-states}

[!DNL Assets] 콘솔에서는 자산의 다양한 상태를 표시할 수 있습니다. 특정 에셋의 현재 상태에 따라 해당 카드 보기에는 만료됨, 게시됨, 승인됨, 거부됨 등과 같은 에셋 상태를 설명하는 레이블이 표시됩니다.

1. [!DNL Assets] 사용자 인터페이스에서 자산을 선택합니다.
1. 도구 모음에서 **[!UICONTROL Publish]**&#x200B;를 클릭합니다. 도구 모음에 **Publish**&#x200B;이 표시되지 않으면 도구 모음에서 **[!UICONTROL 자세히]**&#x200B;를 클릭하고 **[!UICONTROL Publish]** ![게시 옵션](assets/do-not-localize/publish-globe.png) 옵션을 찾습니다.
1. 메뉴에서 **[!UICONTROL Publish]**&#x200B;을(를) 선택한 다음 확인 대화 상자를 닫습니다.
1. 선택 모드를 종료합니다. 에셋의 게시 상태는 카드 보기의 에셋 썸네일 하단에 나타납니다. 목록 보기의 게시됨 열에는 에셋이 게시된 시간이 표시됩니다.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 자산 세부 정보 페이지를 표시하려면 [!DNL Assets] 인터페이스에서 자산을 선택하고 **[!UICONTROL 속성]** ![속성 보기](assets/do-not-localize/info-circle-icon.png)를 클릭합니다.

1. [!UICONTROL 고급] 탭에서 **[!UICONTROL 만료]** 필드에서 에셋의 만료 날짜를 설정합니다.

   ![만료 필드에서 에셋 만료 날짜 및 시간 설정](assets/asset-properties-advanced-tab.png)

   *그림: 에셋 [!UICONTROL 속성] 페이지의 [!UICONTROL 고급] 탭에서 에셋 만료를 설정합니다.*

1. **[!UICONTROL 저장]**&#x200B;을 클릭한 다음 **[!UICONTROL 닫기]**&#x200B;를 클릭하여 자산 콘솔을 표시합니다.
1. 에셋의 게시 상태는 카드 보기의 에셋 썸네일 하단에 만료됨 상태를 나타냅니다. 목록 보기에서 에셋의 상태가 **[!UICONTROL 만료됨]**(으)로 표시됩니다.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. [!DNL Assets] 콘솔에서 폴더를 선택하고 폴더에 대한 검토 작업을 만듭니다.
1. 검토 작업에서 에셋을 검토하고 승인/거부하고 **[!UICONTROL 완료]**&#x200B;를 클릭합니다.
1. 검토 작업을 생성한 폴더로 이동합니다. 승인/거부한 에셋의 상태가 카드 보기의 맨 아래에 표시됩니다. 목록 보기에서 승인 및 만료 상태가 적절한 열에 표시됩니다.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. 상태에 따라 에셋을 검색하려면 **[!UICONTROL 검색]** ![검색 옵션](assets/do-not-localize/search_icon.png)을 클릭하여 Omnisearch 막대를 표시합니다.
1. `Return`을(를) 선택하고 [!DNL Experience Manager]을(를) 클릭하여 검색 패널을 표시합니다.
1. 검색 패널에서 **[!UICONTROL Publish 상태]**&#x200B;를 클릭하고 **[!UICONTROL 게시됨]**&#x200B;을(를) 선택하여 [!DNL Assets]에서 게시된 에셋을 검색합니다.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. **[!UICONTROL 승인 상태]**&#x200B;를 클릭하고 적절한 옵션을 클릭하여 승인 또는 거부된 자산을 검색합니다.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. To search for assets based on their expiration status, select **[!UICONTROL Expiry Status]** in the Search panel and choose the appropriate option.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 다양한 검색 패싯 아래의 상태 조합을 기반으로 에셋을 검색할 수도 있습니다. 예를 들어 검색 패싯에서 적절한 옵션을 선택하여 검토 작업에서 승인되고 아직 만료되지 않은 게시된 자산을 검색할 수 있습니다.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## [!DNL Assets]의 Digital Rights Management {#digital-rights-management-in-assets-1}

이 기능은 [!DNL Adobe Experience Manager Assets]에서 사용 허가된 자산을 다운로드하기 전에 라이선스 계약 수락을 시행합니다.

보호된 자산을 선택하고 **[!UICONTROL 다운로드]**&#x200B;를 클릭하면 사용권 계약에 동의하도록 라이선스 페이지로 리디렉션됩니다. 사용권 계약에 동의하지 않으면 **[!UICONTROL 다운로드]** 옵션을 사용할 수 없습니다.

선택 항목에 여러 개의 보호된 자산이 포함된 경우 한 번에 하나의 자산을 선택하고 라이선스 계약에 동의한 다음 자산 다운로드를 진행합니다.

다음 조건 중 하나가 충족되면 자산이 보호되는 것으로 간주됩니다.

* 에셋 메타데이터 속성 `xmpRights:WebStatement`은(는) 에셋에 대한 라이선스 계약이 포함된 페이지의 경로를 가리킵니다.
* 에셋 메타데이터 HTML `adobe_dam:restrictions`의 값이 사용권 계약을 지정하는 원시 속성입니다.

>[!NOTE]
>
>[!DNL Experience Manager]의 이전 릴리스에서 라이선스를 저장하는 데 사용된 위치 `/etc/dam/drm/licenses`은(는) 더 이상 사용되지 않습니다.
>
>Adobe 라이선스 페이지를 만들거나 수정하거나 이전 [!DNL Experience Manager] 릴리스에서 포팅하는 경우 `/apps/settings/dam/drm/licenses` 또는 `/conf/&ast;/settings/dam/drm/licenses` 아래에 저장하는 것이 좋습니다.

### DRM 보호 에셋 다운로드 {#downloading-drm-assets}

1. 카드 보기에서 다운로드할 자산을 선택하고 **[!UICONTROL 다운로드]**&#x200B;를 클릭합니다.
1. In the **[!UICONTROL Copyright Management]** page, select the asset you want to download from the list.
1. [!UICONTROL 라이선스] 창에서 **[!UICONTROL 동의]**&#x200B;를 선택합니다. 자산 옆에 확인 표시가 나타납니다. **[!UICONTROL 다운로드]** 옵션을 클릭합니다.

   >[!NOTE]
   >
   >**[!UICONTROL 다운로드]** 옵션은 보호된 자산에 대한 사용권 계약에 동의하도록 선택한 경우에만 사용할 수 있습니다. 그러나 선택한 항목이 보호된 자산과 보호되지 않은 자산을 모두 포함하는 경우 보호된 자산만 창에 나열되며 **[!UICONTROL 다운로드]** 옵션을 사용하여 보호되지 않은 자산을 다운로드할 수 있습니다. To simultaneously accept license agreements for multiple protected assets, select the assets from the list and then choose **[!UICONTROL Agree]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 대화 상자에서 **[!UICONTROL 다운로드]**&#x200B;를 클릭하여 에셋 또는 해당 렌디션을 다운로드합니다.
