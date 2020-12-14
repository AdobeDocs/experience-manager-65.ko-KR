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
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# 양식 및 문서 게시 및 게시 취소{#publishing-and-unpublishing-forms-and-documents}

AEM Forms을 사용하면 양식을 손쉽게 작성, 게시 및 게시 취소할 수 있습니다. AEM Forms에 대한 자세한 내용은 [양식 관리 소개](../../forms/using/introduction-managing-forms.md)를 참조하십시오.

AEM Forms 서버는 다음 두 가지 인스턴스를 제공합니다.작성 및 게시를 참조하십시오. 작성 인스턴스는 양식 자산 및 리소스를 만들고 관리하는 데 사용됩니다. 게시 인스턴스는 최종 사용자가 사용할 수 있는 자산 및 관련 리소스를 유지하는 데 사용됩니다. 작성 모드에서 XDP 및 PDF forms을 가져올 수 있습니다. 자세한 내용은 AEM Forms](../../forms/using/get-xdp-pdf-documents-aem.md)에서 [XDP 및 PDF 문서 가져오기를 참조하십시오.

## 지원되는 에셋   {#supported-assets-nbsp}

AEM Forms은 다음 유형의 자산을 지원합니다.

* 적응형 양식
* 적응형 문서
* 적응형 양식 조각
* 테마
* 양식 템플릿(XFA 양식)
* PDF forms
* 문서(기본 PDF 문서)
* 양식 세트
* 리소스(이미지, 스키마 및 스타일 시트)

처음에는 모든 자산을 작성자 인스턴스에서만 사용할 수 있습니다. 관리자나 양식 작성자는 리소스를 제외한 모든 자산을 게시할 수 있습니다.

양식을 선택하고 게시하면 관련 자산 및 리소스도 게시됩니다. 그러나 종속 자산은 게시되지 않습니다. 이러한 컨텍스트에서 관련 자산 및 리소스는 게시된 자산이 사용하거나 참조하는 자산입니다. 종속 자산은 게시된 자산을 참조하는 자산입니다.

응용 Forms은 자동으로 게시되지 않는 일부 구성, 설정 및 사용자 지정을 활용할 수 있습니다. 적응형 양식을 게시하기 전에 이러한 리소스를 게시하거나 활성화하는 것이 좋습니다.

* 편집 가능한 적응형 양식 템플릿
* Adobe Sign, Typekit, reCAPTCHA 및 양식 데이터 모델에 대한 Cloud Service 구성
* 다른 클라우드 서비스 구성은 사용자에게 관리자 권한이 있는 경우에만 활성화됩니다.
* 사용자 지정. 여기에는 다음이 포함되지만 이에 국한되지 않습니다.

   * 사용자 정의 레이아웃
   * 사용자 정의 모양
   * CSS 파일 - 적응형 양식 컨테이너 속성 대화 상자에서 입력으로 가져옴
   * 클라이언트 라이브러리 범주 - 적응형 양식 컨테이너 속성 대화 상자에서 입력으로 가져옴
   * 적응형 양식 템플릿의 일부로 포함할 수 있는 다른 클라이언트 라이브러리
   * 디자인 패스

## 자산 상태 {#asset-states}

자산은 다음 상태를 가질 수 있습니다.

* **게시** 안됨: 게시된 적이 없는 자산(게시 취소된 상태는 Forms 자산에만 적용됩니다. 통신 관리 자산에 게시 취소된 상태가 없습니다.)
* **게시됨**:게시 인스턴스에서 게시 및 사용할 수 있는 자산
* **수정됨**:게시 후 수정된 자산

## 자산 {#publish-an-asset} 게시

1. AEM Forms 서버에 로그인합니다.
1. 자산을 선택하고 게시하려면 다음 중 하나를 사용합니다.

   1. 포인터를 에셋 위로 이동하고 **[!UICONTROL 게시]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png)를 누릅니다.
   1. 다음 중 하나를 수행하고 게시를 누릅니다.

      * 카드 보기에 있는 경우 **[!UICONTROL 선택 입력]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)을 탭하고 자산을 탭합니다. 자산이 선택됩니다.
      * 목록 보기에 있는 경우 자산의 확인란을 선택합니다. 자산이 선택됩니다.
      * 자산을 탭하여 세부 사항을 표시합니다.
      * 속성 보기 ![뷰속성](assets/viewproperties.png)을 탭하여 자산의 속성을 표시합니다.

      >[!NOTE]
      >
      >여러 자산을 선택하지 마십시오. 여러 자산을 한 번에 게시할 수 없습니다.


1. 게시 프로세스가 시작되면 관련 자산 및 리소스가 모두 나열된 확인 대화 상자가 나타납니다. 관련 에셋이 포함된 대화 상자에서 **[!UICONTROL 게시]**&#x200B;를 탭합니다. 자산이 게시되고 [자산 게시 성공] 대화 상자가 나타납니다.

   >[!NOTE]
   >
   >관련 자산과 함께 적응형 양식의 경우 적응형 양식 페이지 이름도 표시됩니다.

   ![모든 관련 자산 및 리소스가 포함된 확인 대화 상자](assets/p4.png)

   모든 관련 자산 및 리소스가 포함된 확인 대화 상자

   >[!NOTE]
   >
   >Forms Manager의 경우 사용자에게 나열된 자산을 게시할 권한이 없는 경우 게시 작업이 비활성화됩니다. 추가 권한이 필요한 자산은 빨간색으로 표시됩니다.

   자산이 게시되면 자산의 메타데이터 속성이 게시 인스턴스로 복사되고 자산의 상태가 게시됨으로 변경됩니다. 게시된 종속 자산의 상태도 게시됨으로 변경됩니다.

   자산을 게시한 후 Forms 포털을 사용하여 웹 페이지에 있는 모든 자산을 표시할 수 있습니다. 자세한 내용은 [포털](../../forms/using/introduction-publishing-forms.md)에 양식 게시 소개를 참조하십시오.

## 모든 통신 관리 자산 {#publish-all-the-correspondence-management-assets} 게시

AEM Forms을 사용하면 모든 통신 관리 에셋을 한 번에 서버에 게시할 수 있습니다. 게시된 자산은 모든 통신 관리 자산 및 관련 종속성을 포함합니다.

서버에 모든 통신 관리 자산을 게시하려면 다음 단계를 완료하십시오.

1. AEM Forms 서버에 로그인합니다.
1. 전역 탐색 막대에서 **Adobe Experience Manager**&#x200B;을 누릅니다.
1. ![도구](assets/tools.png)를 누른 다음 **Forms**&#x200B;을(를) 누릅니다.
1. **메일 관리 자산 게시**&#x200B;를 누릅니다.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   [모든 메일 관리 자산 게시] 페이지가 나타나고 [메일 관리 자산 게시] 프로세스가 시도되었을 때의 정보를 표시합니다.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. **게시**&#x200B;를 누르고 확인 메시지에서 **확인**&#x200B;을 누릅니다.

   배치 프로세스가 완료되면 마지막 실행 상세내역을 볼 수 있습니다. 여기에는 관리자 로그인 및 일괄 처리가 성공적으로 실행되거나 실패한 경우 등의 정보가 포함됩니다.

   >[!NOTE]
   >
   >일단 시작된 게시 프로세스는 취소할 수 없습니다. 또한 게시 작업이 진행 중인 동안에는 자산을 생성, 삭제, 수정 또는 게시하거나 모든 통신 관리 자산 내보내기 작업을 시작하지 마십시오.

## Forms 및 문서에 대한 게시 및 게시 취소 자동화 {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms을 사용하면 Forms 및 문서에 대한 자산 게시 및 게시 취소를 예약할 수 있습니다. 메타데이터 편집기에서 일정을 지정할 수 있습니다. 양식 메타데이터 관리에 대한 자세한 내용은 [양식 메타데이터 관리를 참조하십시오.](../../forms/using/manage-form-metadata.md)

Forms 및 문서 자산을 게시 및 게시 취소하는 날짜와 시간을 예약하려면 다음 단계를 수행합니다.

1. 자산을 선택하고 **[!UICONTROL 속성 보기]**&#x200B;를 탭합니다. 메타데이터 속성 페이지가 열립니다.
1. 메타데이터 속성 페이지에서 **[!UICONTROL 고급]**&#x200B;을 탭한 다음 **[!UICONTROL 편집]** ![illustratorcc_penciiltool_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png)을 탭합니다.
1. **[!UICONTROL 시간에 게시]** 및 **[!UICONTROL 시간 게시]** 필드에서 날짜 및 시간을 선택합니다.\
   **[!UICONTROL 완료]** ![aem6forms_check](assets/aem6forms_check.png)를 누릅니다.

## 자산 {#unpublish-an-asset} 게시 취소

1. 게시되는 자산을 선택하고 **[!UICONTROL 게시 취소]** ![게시 취소](assets/unpublish.png)를 누릅니다.
1. 자산을 선택하고 게시 취소하려면 다음 중 하나를 사용합니다.

   1. 포인터를 에셋 위로 이동하고 **[!UICONTROL 게시 취소]** ![게시 취소](assets/unpublish.png)를 누릅니다.
   1. 다음 중 하나를 수행하고 게시 취소를 누릅니다.

      * 카드 보기에 있는 경우 **[!UICONTROL 선택 입력]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)을 탭하고 자산을 탭합니다. 자산이 선택됩니다.

      * 목록 보기에 있는 경우 자산을 마우스로 가리키고 ![selectassetcheckmark](assets/selectassetcheckmark.png)를 누릅니다. 자산이 선택됩니다.

      * 자산을 탭하여 세부 사항을 표시합니다.
      * 속성 보기 ![뷰속성](assets/viewproperties.png)을 탭하여 자산의 속성을 표시합니다.

1. 게시 취소 프로세스가 시작되면 확인 대화 상자가 나타납니다. **[!UICONTROL 게시 취소]**&#x200B;를 누릅니다.

   >[!NOTE]
   >
   >선택한 자산만 게시 취소되고 해당 하위 자산과 참조된 자산이 있는 경우 게시 취소되지 않습니다.

## 자산 또는 문자를 이전에 게시된 버전 {#revert-an-asset-or-letter-to-the-previously-published-version}으로 되돌리기

에셋 또는 편지를 편집한 후 게시할 때마다 에셋 또는 글자의 버전이 만들어집니다. 자산 또는 문자를 이전에 게시된 버전으로 되돌릴 수 있습니다. 현재 버전의 에셋 또는 문서에 문제가 있는 경우 이 작업을 수행해야 할 수도 있습니다.

>[!NOTE]
>
>게시된 편지에서 사용된 종속 자산이 시스템에서 삭제되는 경우 문서를 마지막으로 게시된 상태로 되돌리지 마십시오.

1. 자산을 선택하고 **[!UICONTROL 이전에 게시된 버전으로 되돌리기]** ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png)을 누릅니다.
1. 자산이 되돌려지기 전에 확인 대화 상자가 나타납니다. **[!UICONTROL 되돌리기]**&#x200B;를 누릅니다.

   자산이나 문자가 이전에 게시된 버전으로 롤백됩니다.

## 자산 {#delete-an-asset} 삭제

>[!NOTE]
>
>자산을 삭제하면 게시 인스턴스에서 해당 자산이 제거됩니다. 자산을 삭제하면 기본 버전을 제외한 버전 내역도 제거됩니다.

1. 자산을 선택하고 **[!UICONTROL 삭제]** ![삭제](assets/delete.png)를 누릅니다.

   >[!NOTE]
   >
   >삭제 옵션은 자산을 탭하여 자산 세부 사항을 표시하거나 속성 보기 ![뷰속성](assets/viewproperties.png)을 탭하여 자산의 속성을 표시할 때도 사용할 수 있습니다.

1. 자산이 삭제되기 전에 확인 대화 상자가 나타납니다. **[!UICONTROL 삭제]**&#x200B;를 누릅니다.

   >[!NOTE]
   >
   >선택한 자산만 삭제되고 종속 자산도 삭제되며 삭제되지 않습니다. 자산의 참조를 확인하려면 ![참조](assets/references.png)를 누른 다음 자산을 선택합니다.
   >
   >
   >삭제하려는 자산이 다른 자산의 하위 자산인 경우 삭제되지 않습니다. 이러한 자산을 삭제하려면 다른 자산에서 이 자산의 참조를 제거한 다음 다시 시도하십시오.

## 보호된 적응형 양식 {#protected-adaptive-forms}

선택한 사용자가 액세스할 양식에 대한 인증을 활성화할 수 있습니다. 양식에 대한 인증을 활성화하면 액세스 전에 로그인 화면이 표시됩니다. 권한이 있는 자격 증명을 가진 사용자만 양식에 액세스할 수 있습니다.

양식에 대한 인증을 활성화하려면:

1. 브라우저에서 게시 인스턴스의 configMgr을 엽니다.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Adobe Experience Manager 웹 콘솔 구성에서 **Apache Sling 인증 서비스**&#x200B;를 클릭하여 구성합니다.
1. 표시되는 Apache Sling 인증 서비스 대화 상자에서 **+** 단추를 사용하여 경로를 추가합니다.\
   경로를 추가하면 해당 경로의 양식에 대해 인증 서비스가 활성화됩니다.
