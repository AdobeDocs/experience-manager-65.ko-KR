---
title: 양식 및 문서 게시 및 게시 취소
seo-title: 양식 및 문서 게시 및 게시 취소
description: 양식의 게시 및 게시 취소를 예약할 수 있습니다. 게시된 양식은 게시 인스턴스에서 복제됩니다.
seo-description: 양식의 게시 및 게시 취소를 예약할 수 있습니다. 게시된 양식은 게시 인스턴스에서 복제됩니다.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# 양식 및 문서 게시 및 게시 취소{#publishing-and-unpublishing-forms-and-documents}

AEM Forms를 사용하면 양식을 손쉽게 작성, 게시 및 게시 취소할 수 있습니다. AEM Forms에 대한 자세한 내용은 [양식](../../forms/using/introduction-managing-forms.md)관리 소개를 참조하십시오.

AEM Forms 서버는 다음 두 가지 인스턴스를 제공합니다.작성 및 게시. 작성 인스턴스는 양식 자산 및 리소스를 만들고 관리하는 데 사용됩니다. 게시 인스턴스는 최종 사용자가 사용할 수 있는 자산 및 관련 리소스를 유지하는 것입니다. 작성 모드에서 XDP 및 PDF 양식을 가져올 수 있습니다. 자세한 내용은 AEM Forms [에서 XDP 및 PDF 문서 가져오기를 참조하십시오](../../forms/using/get-xdp-pdf-documents-aem.md).

## 지원되는 에셋 {#supported-assets-nbsp}

AEM Forms는 다음 유형의 자산을 지원합니다.

* 적응형 양식
* 적응형 문서
* 적응형 양식 조각
* 테마
* 양식 템플릿(XFA 양식)
* PDF 양식
* 문서(기본 PDF 문서)
* 양식 세트
* 리소스(이미지, 스키마 및 스타일 시트)

처음에는 모든 자산을 작성자 인스턴스에서만 사용할 수 있습니다. 관리자나 양식 작성자는 리소스를 제외한 모든 자산을 게시할 수 있습니다.

양식을 선택하고 게시하면 관련 자산 및 리소스도 게시됩니다. 그러나 종속 자산은 게시되지 않습니다. 이 컨텍스트에서 관련 자산 및 리소스는 게시된 자산이 사용하거나 참조하는 자산입니다. 종속 자산은 게시된 자산을 참조하는 자산입니다.

적응형 양식은 자동으로 게시되지 않는 일부 구성, 설정 및 사용자 지정을 활용할 수 있습니다. 적응형 양식을 게시하기 전에 이러한 리소스를 게시하거나 활성화하는 것이 좋습니다.

* 편집 가능한 적응형 양식 템플릿
* Adobe Sign, Typekit, reCAPTCHA 및 양식 데이터 모델에 대한 클라우드 서비스 구성
* 다른 클라우드 서비스 구성은 사용자에게 관리자 권한이 있는 경우에만 활성화됩니다.
* 사용자 정의. 여기에는 다음이 포함되지만 이에 국한되지 않습니다.

   * 사용자 정의 레이아웃
   * 사용자 정의 모양
   * CSS 파일 - 적응형 양식 컨테이너 속성 대화 상자에서 입력으로 취함
   * 클라이언트 라이브러리 카테고리 - 적응형 양식 컨테이너 속성 대화 상자에서 입력으로 가져옴
   * 응용 양식 템플릿의 일부로 포함되어 있을 수 있는 다른 클라이언트 라이브러리
   * 디자인 경로

## 자산 상태 {#asset-states}

자산은 다음 상태를 가질 수 있습니다.

* **** 게시 안 됨:게시되지 않은 자산(게시 취소된 상태는 양식 자산에만 적용됩니다. 통신 관리 자산에 게시 취소 상태가 없습니다.)
* **게시됨**:게시되었으며 게시 인스턴스에서 사용할 수 있는 자산
* **수정됨**:게시한 후 수정된 자산

## 자산 게시 {#publish-an-asset}

1. AEM Forms 서버에 로그인합니다.
1. 다음 중 하나를 사용하여 자산을 선택하고 게시합니다.

   1. 포인터를 자산 위로 이동하고 **[!UICONTROL aem6forms_globe]** 게시를 ![누릅니다](assets/aem6forms_globe.pngasset.png).
   1. 다음 중 하나를 수행하고 게시를 누릅니다.

      * 카드 보기에 있는 경우 선택 **[!UICONTROL 항목]** 시작을 탭하고 ![자산을](assets/aem6forms_check-circle.png)탭합니다. 자산이 선택됩니다.
      * 목록 보기에 있는 경우 자산의 확인란을 선택합니다. 자산이 선택됩니다.
      * 자산을 탭하여 세부 사항을 표시합니다.
      * 속성 보기를 탭하여 자산의 속성을 ![표시합니다](assets/viewproperties.png).
      >[!NOTE]
      >
      >여러 자산을 선택하지 마십시오. 여러 자산을 한 번에 게시할 수 없습니다.


1. 게시 프로세스가 시작되면 관련 자산 및 리소스가 모두 나열된 확인 대화 상자가 나타납니다. 관련 에셋이 포함된 대화 상자에서 게시를 **[!UICONTROL 누릅니다]**. 자산이 게시되고 [자산 게시 성공] 대화 상자가 나타납니다.

   >[!NOTE]
   >
   >관련 자산과 함께 적응형 양식의 경우 적응형 양식 페이지 이름도 표시됩니다.

   ![모든 관련 자산 및 리소스가 포함된 확인 대화 상자](assets/p4.png)

   모든 관련 자산 및 리소스가 포함된 확인 대화 상자

   >[!NOTE]
   >
   >Forms Manager의 경우 사용자에게 나열된 자산을 게시할 권한이 없으면 게시 작업이 비활성화됩니다. 추가 권한이 필요한 자산은 빨간색으로 표시됩니다.

   자산이 게시되면 자산의 메타데이터 속성이 게시 인스턴스에 복사되고 자산의 상태가 게시됨으로 변경됩니다. 게시된 종속 자산의 상태도 게시됨으로 변경됩니다.

   자산을 게시한 후 Forms 포털을 사용하여 웹 페이지의 모든 자산을 표시할 수 있습니다. 자세한 내용은 [포털에서](../../forms/using/introduction-publishing-forms.md)양식 게시 소개를 참조하십시오.

## Publish all the Correspondence Management Assets {#publish-all-the-correspondence-management-assets}

AEM Forms를 사용하면 모든 통신 관리 자산을 한 번에 서버에 게시할 수 있습니다. 게시된 자산은 모든 통신 관리 자산 및 관련 종속성을 포함합니다.

서버에 모든 통신 관리 에셋을 게시하려면 다음 단계를 완료하십시오.

1. AEM Forms 서버에 로그인합니다.
1. 전역 **탐색** 막대에서 Adobe Experience Manager를 누릅니다.
1. 도구를 ![누른](assets/tools.png)다음 양식을 **누릅니다**.
1. Tap **Publish Correspondence Management Assets**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   [모든 통신메일 관리 자산 게시] 페이지가 나타나고 [통신메일 관리 자산 게시] 프로세스가 마지막으로 시도되었을 때의 정보가 표시됩니다.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. 게시를 **누르고** 확인 메시지에서 확인을 **누릅니다**.

   배치 프로세스가 완료되면 마지막 실행 세부 정보를 볼 수 있습니다. 여기에는 관리자 로그인 및 일괄 처리가 성공적으로 실행되거나 실패한 경우 등의 정보가 포함됩니다.

   >[!NOTE]
   >
   >게시 프로세스가 시작되면 취소할 수 없습니다. 또한 게시 작업이 진행되는 동안 자산을 만들거나, 삭제하거나, 수정하거나, 게시하거나, 모든 통신 관리 자산 내보내기 작업을 시작하지 마십시오.

## 양식 및 문서에 대한 게시 및 게시 취소 자동화 {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms를 사용하면 양식 및 문서에 대한 자산 게시 및 게시 취소를 예약할 수 있습니다. 메타데이터 편집기에서 일정을 지정할 수 있습니다. 양식 메타데이터 관리에 대한 자세한 내용은 양식 [메타데이터 관리를 참조하십시오.](../../forms/using/manage-form-metadata.md)

양식 및 문서 자산을 게시 및 게시 취소하는 날짜와 시간을 예약하려면 다음 단계를 따르십시오.

1. 자산을 선택하고 속성 보기를 **[!UICONTROL 누릅니다]**. 메타데이터 속성 페이지가 열립니다.
1. 메타데이터 속성 페이지에서 고급을 **[!UICONTROL 누른]**&#x200B;다음 **[!UICONTROL 편집]** illustratororcc_penciltool_cur_edit_2_17을 ![누릅니다](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. [ **[!UICONTROL 시간에 게시] 및]** [ **[!UICONTROL 시간]** 외 게시] 필드에서날짜 및 시간을 선택합니다.\
   Done **[!UICONTROL aem]** 6forms_ ![check](assets/aem6forms_check.png)작업을 누릅니다.

## 자산 게시 취소 {#unpublish-an-asset}

1. 게시되는 자산을 선택하고 게시 **[!UICONTROL 취소를]** 누릅니다 ![](assets/unpublish.png).
1. 다음 중 하나를 사용하여 자산을 선택하고 게시 취소합니다.

   1. 포인터를 자산 위로 이동하고 게시 **[!UICONTROL 취소를]** 누릅니다 ![](assets/unpublish.png).
   1. 다음 중 하나를 수행하고 게시 취소를 누릅니다.

      * 카드 보기에 있는 경우 선택 **[!UICONTROL 항목]** 시작을 탭하고 ![자산을](assets/aem6forms_check-circle.png)탭합니다. 자산이 선택됩니다.

      * 목록 보기에 있는 경우 자산을 마우스로 가리키고 ![selectassetcheckmark를 누릅니다](assets/selectassetcheckmark.png) . 자산이 선택됩니다.

      * 자산을 탭하여 세부 사항을 표시합니다.
      * 속성 보기를 탭하여 자산의 속성을 ![표시합니다](assets/viewproperties.png).

1. 게시 취소 프로세스가 시작되면 확인 대화 상자가 나타납니다. 게시 **[!UICONTROL 취소를 누릅니다]**.

   >[!NOTE]
   >
   >선택한 자산만 게시 취소되고, 하위 자산과 참조된 자산이 있는 경우 게시 취소되지 않습니다.

## 자산 또는 문자를 이전에 게시된 버전으로 되돌리기 {#revert-an-asset-or-letter-to-the-previously-published-version}

에셋 또는 문자를 편집한 후 게시할 때마다 에셋 또는 글자의 버전이 만들어집니다. 자산이나 문자를 이전에 게시된 버전으로 되돌릴 수 있습니다. 현재 버전의 자산이나 문서에 문제가 있는 경우 이를 수행해야 할 수 있습니다.

>[!NOTE]
>
>게시된 편지에서 사용된 종속 자산이 시스템에서 삭제된 경우 문자를 마지막으로 게시된 상태로 되돌리지 마십시오.

1. 자산을 선택하고 [이전에 게시된 버전으로 **[!UICONTROL 되돌리기]를]** 탭하면 ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png).
1. 자산이 되돌려지기 전에 확인 대화 상자가 나타납니다. 되돌리기를 **[!UICONTROL 누릅니다]**.

   자산이나 문자가 이전에 게시된 버전으로 롤백됩니다.

## 자산 삭제 {#delete-an-asset}

>[!NOTE]
>
>자산을 삭제하면 게시 인스턴스에서 제거됩니다. 자산을 삭제하면 기본 버전을 제외한 버전 내역도 제거됩니다.

1. 자산을 선택하고 삭제를 **[!UICONTROL 누릅니다]**![](assets/delete.png).

   >[!NOTE]
   >
   >[삭제] 옵션은 자산을 탭하여 자산 세부 사항을 표시하거나 [속성 보기] ![뷰속성을](assets/viewproperties.png)탭하여 자산의 속성을 표시하는 경우에도 사용할 수 있습니다.

1. 자산이 삭제되기 전에 확인 대화 상자가 나타납니다. 삭제를 **[!UICONTROL 누릅니다]**.

   >[!NOTE]
   >
   >선택한 자산만 삭제되고 종속 자산도 삭제되지 않습니다. 자산의 참조를 확인하려면 ![참조를](assets/references.png) 누른 다음 자산을 선택합니다.
   >
   >
   >삭제하려는 자산이 다른 자산의 하위 자산인 경우 삭제되지 않습니다. 이러한 자산을 삭제하려면 다른 자산에서 이 자산의 참조를 제거한 다음 다시 시도하십시오.

## 보호된 적응형 양식 {#protected-adaptive-forms}

선택한 사용자가 액세스할 양식에 대한 인증을 활성화할 수 있습니다. 양식에 대한 인증을 활성화하면 액세스 전에 로그인 화면이 표시됩니다. 권한이 있는 자격 증명을 가진 사용자만 양식에 액세스할 수 있습니다.

양식에 대한 인증을 활성화하려면

1. 브라우저에서 게시 인스턴스에서 configMgr을 엽니다.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Adobe Experience Manager 웹 콘솔 구성에서 Apache Sling **인증 서비스를** 클릭하여 구성합니다.
1. 표시되는 Apache Sling 인증 서비스 대화 상자에서 **+** 단추를 사용하여 경로를 추가합니다.\
   경로를 추가하면 해당 경로에서 양식에 대해 인증 서비스가 활성화됩니다.
