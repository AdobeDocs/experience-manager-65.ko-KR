---
title: 디지털 자산 권한 관리
description: AEM 파섹
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Digital Rights Management for digital assets {#digital-rights-management-in-assets}

디지털 자산은 종종 사용약관과 사용 기간을 지정하는 라이선스와 연결됩니다. AEM(Adobe Experience Manager) 자산은 AEM 플랫폼과 완전히 통합되므로 자산 만료 정보 및 자산 상태를 효율적으로 관리할 수 있습니다. 라이선스 정보를 에셋과 연결할 수도 있습니다.

## 자산 만료 {#asset-expiration}

에셋 만료는 에셋에 대한 라이선스 요구 사항을 적용하는 효과적인 방법입니다. 이렇게 하면 게시된 자산이 만료될 때 게시가 취소되어 라이선스 위반 가능성을 방지합니다. 관리자 권한이 없는 사용자는 만료된 자산을 편집, 복사, 이동, 게시 및 다운로드할 수 없습니다.

자산 콘솔의 카드 보기 및 목록 보기 모두에서 자산의 만료 상태를 볼 수 있습니다.

![expired_flag_card](assets/expired_flag_card.png)

*그림:카드 보기에서 카드의 플래그는 만료된 자산을 나타냅니다.*

**목록 보기**

![expired_flag_list](assets/expired_flag_list.png)

*그림:목록 보기에서는 상태[!UICONTROL 열에]만료된[!UICONTROL 배너가]표시됩니다.*

타임라인에서 자산의 만료 상태를 볼 수 있습니다. 자산을 선택하고 전역 탐색 메뉴에서 타임라인을 선택합니다.

![chlimage_1-144](assets/chlimage_1-144.png)

참조 레일에서 자산의 만료 상태를 볼 수도 **[!UICONTROL 있습니다]** . 복합 자산과 참조된 하위 자산, 컬렉션 및 프로젝트 간의 관계 및 자산 만료 상태를 관리합니다.

1. 참조하는 웹 페이지와 복합 자산을 보려는 자산으로 이동합니다.
1. 자산 및 Experience Manager 로고를 선택합니다.

1. 메뉴에서 **[!UICONTROL 참조를]** 선택합니다.

   ![chlimage_1-146](assets/chlimage_1-146.png)

   만료된 자산의 경우, 참조 레일은 만료 상태 **[!UICONTROL 자산이 만료됨]** 맨 위에 표시됩니다.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   자산이 만료된 하위 자산이 있는 경우 참조 레일에는 자산이 만료된 **[!UICONTROL 하위 자산이 표시됩니다]**.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### 만료된 자산 검색 {#search-expired-assets}

[검색] 패널에서 만료된 하위 자산을 포함하여 만료된 자산을 검색할 수 있습니다.

1. 자산 콘솔의 도구 모음에서 **[!UICONTROL 검색을]** 클릭하여 Omnisearch 상자를 표시합니다.

1. Omnisearch 상자에 커서를 놓고 Return 키를 눌러 검색 결과 페이지를 표시합니다.

   ![chlimage_1-150](assets/chlimage_1-150.png)

1. Experience Manager 로고를 클릭하여 검색 패널을 표시합니다.

   ![chlimage_1-151](assets/chlimage_1-151.png)

1. 만료 **[!UICONTROL 상태]** 옵션을 클릭하여 확장합니다.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 만료됨을 **[!UICONTROL 선택합니다]**. 만료된 자산이 검색 결과에 표시됩니다.

   ![chlimage_1-153](assets/chlimage_1-153.png)

만료됨 **옵션을 선택하면 자산** 콘솔은 복합 자산에서 참조하는 만료된 자산과 하위 자산만 표시합니다. 만료된 하위 자산을 참조하는 복합 자산은 하위 자산이 만료된 즉시 표시되지 않습니다. 대신, AEM 자산에서 스케줄러가 다음에 실행될 때 만료된 하위 자산을 참조한다는 것을 감지하면 표시됩니다.

게시된 자산의 만료 날짜를 현재 스케줄러 주기보다 빠른 날짜로 수정해도 예약은 이 자산이 다음 번 실행될 때 만료된 자산으로 계속 감지하고 그에 따라 상태를 반영합니다.

또한, 오류나 오류가 스케줄러가 현재 주기에 만료된 자산을 검색하지 못하게 하는 경우 스케줄러는 다음 주기에 이러한 자산을 다시 검사하여 만료된 상태를 검색합니다.

자산 콘솔에서 참조된 복합 자산을 만료된 하위 자산과 함께 표시하려면 AEM Configuration Manager **에서 Adobe CQ DAM 만료 알림** 워크플로우를 구성합니다.

1. AEM 구성 관리자를 엽니다.
1. Adobe **[!UICONTROL CQ DAM 만료 알림을 선택합니다]**. 기본적으로 시간 **[!UICONTROL 기반 스케줄러가]** 선택되어 자산이 만료된 하위 자산이 있는지 여부를 특정 시간에 확인할 작업을 예약합니다. 작업이 완료되면 만료된 하위 자산 및 참조된 자산이 검색 결과에 만료된 것으로 표시됩니다.

   ![chlimage_1-154](assets/chlimage_1-154.png)

1. 작업을 주기적으로 실행하려면 시간 기반 스케줄러 **[!UICONTROL 규칙]** 필드를 지우고 시간(초) **[!UICONTROL 을]** 수정합니다. 예: 예제 표현식 &#39;0 &amp;ast;&amp;ast;?&#39; 00시간에 작업을 트리거합니다.
1. 자산이 만료될 때 이메일을 **[!UICONTROL 받으려면 이메일]** 보내기를 선택합니다.

   >[!NOTE]
   >
   >자산 생성자(AEM 자산에 특정 자산을 업로드하는 사람)만 자산이 만료되면 이메일을 받습니다. 전체 [AEM](/help/sites-administering/notification.md) 수준에서 이메일 알림 구성에 대한 자세한 내용은 이메일 알림 구성을 참조하십시오.

1. 이전 **[!UICONTROL 알림(초]** 단위) 필드에서 만료 관련 알림을 받을 때 자산이 만료되기 전 시간(초)을 지정합니다. 관리자 또는 자산 작성자는 자산이 만료되기 전에 지정된 시간 후에 만료될 것임을 알려주는 메시지를 받게 됩니다.

   자산이 만료되면 만료를 확인하는 다른 알림을 받게 됩니다. 또한 만료된 자산은 비활성화됩니다.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

## 자산 상태 {#asset-states}

AEM(Adobe Experience Manager) 자산의 자산 콘솔은 자산에 대한 다양한 상태를 표시할 수 있습니다. 특정 자산의 현재 상태에 따라 카드 보기에는 상태를 설명하는 레이블이 표시됩니다(예: 만료됨, 게시됨, 승인됨, 거부됨 등).

1. 자산 사용자 인터페이스에서 자산을 선택합니다.

   ![chlimage_1-155](assets/chlimage_1-155.png)

1. 도구 **[!UICONTROL 모음에서]** 게시를 클릭합니다. 도구 모음에 [게시] **가** 표시되지 않으면 도구 모음에서 [자세히 **]** 를 **[!UICONTROL 클릭하고 [게시]** ]옵션을 찾습니다.

   ![chlimage_1-156](assets/chlimage_1-156.png)

1. 메뉴에서 **[!UICONTROL 게시를]** 선택한 다음 확인 대화 상자를 닫습니다.
1. 선택 모드를 종료합니다. 자산에 대한 게시 상태는 카드 보기의 자산 축소판 아래쪽에 표시됩니다. 목록 보기에서 게시된 열에는 자산이 게시된 시간이 표시됩니다.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 자산 인터페이스에서 자산을 선택하고 속성을 클릭하여 **[!UICONTROL 자산]** 세부 사항 페이지를 표시합니다.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 고급 탭의 만료 필드에서 자산의 만료 날짜를 **[!UICONTROL 설정합니다]** .

   ![만료일 필드에서 자산 만료 날짜 및 시간 설정](assets/asset-properties-advanced-tab.png)


   *그림:자산 속성의 고급 탭을 사용하여 에셋 만료 설정*

1. 저장을 **[!UICONTROL 클릭한]** 다음 **[!UICONTROL 닫기를 클릭하여]** 자산 콘솔을 표시합니다.
1. 자산에 대한 게시 상태는 카드 보기에서 자산 축소판의 아래쪽에 있는 만료된 상태를 나타냅니다. 목록 보기에서는 자산의 상태가 만료됨으로 **[!UICONTROL 표시됩니다]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. 자산 콘솔에서 폴더를 선택하고 폴더에 검토 작업을 만듭니다.
1. 검토 작업의 자산을 검토 및 승인/거부하고 완료를 **[!UICONTROL 클릭합니다]**.
1. 검토 작업을 만든 폴더로 이동합니다. 승인/거부를 한 자산의 상태는 카드 보기의 하단에 표시됩니다. 목록 보기에서는 승인 및 만료 상태가 적절한 열에 표시됩니다.

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. 상태를 기반으로 자산을 검색하려면 검색을 클릭하여 **[!UICONTROL Omniture]** 막대를 표시합니다.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Return 키를 누른 다음 **[!UICONTROL GlobalNav를]** 클릭하여 검색 패널을 표시합니다.
1. 검색 패널에서 게시 **[!UICONTROL 상태를 클릭하고]** 게시됨을 선택하여 **[!UICONTROL AEM]** 자산에서 게시된 자산을 검색합니다.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 승인 **[!UICONTROL 상태를]** 클릭하고 적절한 옵션을 클릭하여 승인되거나 거부된 자산을 검색합니다.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 만료 상태를 기반으로 에셋을 검색하려면 검색 **[!UICONTROL 패널에서]** 만료 상태를 선택하고 적절한 옵션을 선택합니다.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 다양한 검색 패싯 아래의 상태 조합을 기반으로 자산을 검색할 수도 있습니다. 예를 들어, 검색 패싯에서 적절한 옵션을 선택하여 아직 만료되지 않은 검토 작업에서 승인되어 게시된 자산을 검색할 수 있습니다.

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management in Assets {#digital-rights-management-in-assets-1}

이 기능은 Adobe Experience Manager Assets에서 라이선스가 부여된 자산을 다운로드하기 전에 사용권 계약에 동의함을 적용합니다.

보호된 자산을 선택하고 다운로드를 **[!UICONTROL 클릭하면]**&#x200B;사용권 계약에 동의하는 라이센스 페이지로 리디렉션됩니다. 사용권 계약에 동의하지 않으면 다운로드 **[!UICONTROL 단추가]** 비활성화됩니다.

선택한 자산에 여러 개의 보호된 자산이 포함되어 있는 경우 한 번에 하나의 자산을 선택하고 사용권 계약에 동의한 다음 에셋 다운로드를 계속합니다.

다음 조건 중 하나가 충족되면 자산이 보호되는 것으로 간주됩니다.

* 자산 메타데이터 속성은 자산에 대한 사용권 계약을 포함하는 페이지의 경로를 `xmpRights:WebStatement` 가리킵니다.
* 자산 메타데이터 속성의 값은 사용권 계약을 지정하는 원시 HTML입니다. `adobe_dam:restrictions`

>[!NOTE]
>
>이전 버전의 AEM에서 라이선스를 저장하는 데 `/etc/dam/drm/licenses` 사용되는 위치는 더 이상 사용되지 않습니다.
>
>라이선스 페이지를 만들거나 수정하거나 이전 AEM 릴리스에서 전송하는 경우 `/apps/settings/dam/drm/licenses` 또는 아래에 저장하는 것이 좋습니다 `/conf/&ast;/settings/dam/drm/licenses`.

### DRM으로 보호된 에셋 다운로드 {#downloading-drm-assets}

1. 카드 보기에서 다운로드할 자산을 선택하고 다운로드를 **[!UICONTROL 클릭합니다]**.
1. 저작권 **[!UICONTROL 관리]** 페이지의 목록에서 다운로드할 자산을 선택합니다.
1. 라이센스 창에서 동의를 **[!UICONTROL 선택합니다]**. 사용권 계약에 동의하는 자산 옆에 확인 표시가 나타납니다. [다운로드] **[!UICONTROL 단추를]** 클릭합니다.

   >[!NOTE]
   >
   >[ **[!UICONTROL 다운로드]** ] 단추는 보호된 자산에 대한 사용권 계약에 동의하도록 선택한 경우에만 활성화됩니다. 그러나 선택한 항목이 보호되거나 보호되지 않은 자산으로 구성된 경우 왼쪽 창에 보호된 자산만 나열되며 **[!UICONTROL [다운로드]** ] 단추를 사용하여 보호되지 않은 자산을 다운로드할 수 있습니다. 여러 개의 보호된 자산에 대한 사용권 계약을 동시에 수락하려면 목록에서 자산을 선택한 다음 [동의]를 **[!UICONTROL 선택합니다]**.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 대화 상자에서 다운로드를 클릭하여 **[!UICONTROL 자산]** 또는 표현물을 다운로드합니다.
