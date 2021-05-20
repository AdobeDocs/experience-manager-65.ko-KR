---
title: 양식 및 문서 게시 및 게시 취소
seo-title: 양식 및 문서 게시 및 게시 취소
description: 양식의 게시 및 게시 취소를 예약할 수 있습니다. 게시된 양식이 게시 인스턴스에 복제됩니다.
seo-description: 양식의 게시 및 게시 취소를 예약할 수 있습니다. 게시된 양식이 게시 인스턴스에 복제됩니다.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
exl-id: f26c4268-7885-4e61-a258-219d98288548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---

# 양식 및 문서 게시 및 게시 취소{#publishing-and-unpublishing-forms-and-documents}

AEM Forms에서 양식을 쉽게 만들고, 게시하고, 게시 취소할 수 있습니다. AEM Forms에 대한 자세한 내용은 [양식 관리 소개](../../forms/using/introduction-managing-forms.md)를 참조하십시오.

AEM Forms 서버는 두 가지 인스턴스를 제공합니다.작성 및 게시. 작성 인스턴스는 양식 자산 및 리소스를 만들고 관리하는 것입니다. 게시 인스턴스는 최종 사용자가 사용할 수 있는 자산 및 관련 리소스를 유지하는 것입니다. 작성자 모드에서 XDP 및 PDF forms을 가져올 수 있습니다. 자세한 내용은 AEM Forms](../../forms/using/get-xdp-pdf-documents-aem.md)에서 [XDP 및 PDF 문서 가져오기 를 참조하십시오.

## 지원되는 자산   {#supported-assets-nbsp}

AEM Forms은 다음 유형의 자산을 지원합니다.

* 적응형 양식
* 응용 문서
* 적응형 양식 조각
* 테마
* 양식 템플릿(XFA 양식)
* PDF forms
* 문서(플랫 PDF 문서)
* 양식 세트
* 리소스(이미지, 스키마 및 스타일 시트)

처음에는 모든 자산을 작성자 인스턴스에서만 사용할 수 있습니다. 관리자나 양식 작성자는 리소스를 제외한 모든 자산을 게시할 수 있습니다.

양식을 선택하고 게시하면 관련 자산 및 리소스도 게시됩니다. 그러나 종속 자산은 게시되지 않습니다. 이 컨텍스트에서 관련 자산 및 리소스는 게시된 자산이 사용하거나 참조하는 자산입니다. 종속 자산은 게시된 자산을 참조하는 자산입니다.

적응형 Forms은 자동으로 게시되지 않는 일부 구성, 설정 및 사용자 지정을 활용할 수 있습니다. 적응형 양식을 게시하기 전에 이러한 리소스를 게시하거나 활성화하는 것이 좋습니다.

* 편집 가능한 적응형 양식 템플릿
* Adobe Sign, Typekit, reCAPTCHA 및 양식 데이터 모델에 대한 Cloud Service 구성
* 다른 클라우드 서비스 구성은 사용자에게 관리자 권한이 있는 경우에만 활성화됩니다.
* 사용자 지정. 이러한 기능은 다음과 같습니다.

   * 사용자 정의 레이아웃
   * 사용자 정의 모양
   * CSS 파일 - 적응형 양식 컨테이너 속성 대화 상자에서 입력으로 가져옴
   * 클라이언트 라이브러리 카테고리 - 적응형 양식 컨테이너 속성 대화 상자에서 입력으로 가져옴
   * 적응형 양식 템플릿의 일부로 포함될 수 있는 다른 모든 클라이언트 라이브러리입니다.
   * 디자인 경로

## 자산 상태 {#asset-states}

자산에는 다음 상태가 있을 수 있습니다.

* **게시되지 않음:**  게시되지 않은 자산입니다(게시 취소된 상태는 Forms 자산에만 적용할 수 있습니다.) 서신 관리 자산에 게시 취소 상태가 없습니다.)
* **게시됨**:게시된 자산이며 게시 인스턴스에서 사용할 수 있습니다
* **수정됨**:게시된 후 수정된 자산

## 자산 게시 {#publish-an-asset}

1. AEM Forms 서버에 로그인합니다.
1. 다음 중 하나를 사용하여 자산을 선택하고 게시합니다.

   1. 포인터를 자산 위로 이동하고 **[!UICONTROL 게시]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png)를 누릅니다.
   1. 다음 중 하나를 수행하고 게시 를 탭합니다.

      * 카드 보기에 있는 경우 **[!UICONTROL 선택 입력]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)을(를) 탭하고 자산을 탭합니다. 자산이 선택되어 있습니다.
      * 목록 보기에 있는 경우, 자산의 확인란을 선택합니다. 자산이 선택되어 있습니다.
      * 자산을 탭하여 세부 사항을 표시합니다.
      * 속성 보기 ![속성 보기](assets/viewproperties.png)를 탭하여 자산의 속성을 표시합니다.

      >[!NOTE]
      >
      >여러 자산을 선택하지 마십시오. 한 번에 여러 자산을 게시할 수 없습니다.


1. 게시 프로세스가 시작되면 관련 자산 및 리소스를 모두 나열하는 확인 대화 상자가 나타납니다. 관련 자산이 포함된 대화 상자에서 **[!UICONTROL 게시]**&#x200B;를 누릅니다. 자산이 게시되고 자산 게시 성공 대화 상자가 나타납니다.

   >[!NOTE]
   >
   >적응형 양식의 경우 관련 자산과 함께 적응형 양식 페이지 이름도 표시됩니다.

   ![모든 관련 자산 및 리소스를 포함하는 확인 대화 상자](assets/p4.png)

   모든 관련 자산 및 리소스가 포함된 확인 대화 상자

   >[!NOTE]
   >
   >Forms Manager의 경우 사용자에게 나열된 자산을 게시할 권한이 없는 경우 게시 작업이 비활성화됩니다. 추가 권한이 필요한 자산은 빨간색으로 표시됩니다.

   자산이 게시되면 자산의 메타데이터 속성이 게시 인스턴스에 복사되고 자산의 상태가 게시됨으로 변경됩니다. 게시된 종속 자산의 상태도 게시됨으로 변경됩니다.

   자산을 게시한 후 Forms Portal 을 사용하여 웹 페이지에 모든 자산을 표시할 수 있습니다. 자세한 내용은 [포털에 양식 게시 소개](../../forms/using/introduction-publishing-forms.md)를 참조하십시오.

## 모든 서신 관리 자산 게시 {#publish-all-the-correspondence-management-assets}

AEM Forms을 사용하면 한 번에 서버에 모든 서신 관리 자산을 게시할 수 있습니다. 게시된 자산에는 모든 서신 관리 자산 및 관련 종속성이 포함됩니다.

서버에 모든 서신 관리 자산을 게시하려면 다음 단계를 완료하십시오.

1. AEM Forms 서버에 로그인합니다.
1. 전역 탐색 막대에서 **Adobe Experience Manager**&#x200B;을 누릅니다.
1. ![도구](assets/tools.png)를 탭한 다음, **Forms**&#x200B;을 탭합니다.
1. **서신 관리 자산 게시**&#x200B;를 누릅니다.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   모든 서신 관리 자산 게시 페이지가 나타나고 Publish Correspondence Management Assets 프로세스가 마지막으로 시도된 시간에 대한 정보가 표시됩니다.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. **게시**&#x200B;를 누르고 확인 메시지에서 **확인**&#x200B;을 누릅니다.

   배치 프로세스가 완료되면 마지막 실행 상세내역을 볼 수 있습니다. 여기에는 관리자 로그인 및 배치가 성공적으로 실행되거나 실패한 경우 등의 정보가 포함됩니다.

   >[!NOTE]
   >
   >게시 프로세스를 시작한 후에는 취소할 수 없습니다. 또한 게시 작업이 진행 중인 동안에는 자산을 생성, 삭제, 수정 또는 게시하거나 모든 서신 관리 자산 내보내기 작업을 시작하지 마십시오.

## Forms 및 문서에 대한 게시 및 게시 취소 자동화 {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms을 사용하면 Forms 및 문서에 대한 자산 게시 및 게시 취소를 예약할 수 있습니다. 메타데이터 편집기에서 일정을 지정할 수 있습니다. 양식 메타데이터 관리에 대한 자세한 내용은 [양식 메타데이터 관리를 참조하십시오.](../../forms/using/manage-form-metadata.md)

Forms 및 문서 자산을 게시하고 게시를 취소하는 날짜와 시간을 예약하려면 다음 단계를 따르십시오.

1. 자산을 선택하고 **[!UICONTROL 속성 보기]**&#x200B;를 누릅니다. 메타데이터 속성 페이지가 열립니다.
1. 메타데이터 속성 페이지에서 **[!UICONTROL 고급]**&#x200B;을 탭한 다음, **[!UICONTROL 편집]** ![illustrator_cc_penciltool_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png)을 탭합니다.
1. **[!UICONTROL 시간에 게시]** 및 **[!UICONTROL 시간 게시]** 필드에서 날짜 및 시간을 선택합니다.\
   **[!UICONTROL 완료]** ![aem6forms_check](assets/aem6forms_check.png)를 누릅니다.

## 자산 게시 취소 {#unpublish-an-asset}

1. 게시된 자산을 선택하고 **[!UICONTROL 게시 취소]** ![게시 취소](assets/unpublish.png)를 누릅니다.
1. 다음 중 하나를 사용하여 자산을 선택하고 게시 취소합니다.

   1. 포인터를 자산 위로 이동하고 **[!UICONTROL 게시 취소]** ![게시 취소](assets/unpublish.png)를 탭합니다.
   1. 다음 중 하나를 수행하고 게시 취소 를 탭합니다.

      * 카드 보기에 있는 경우 **[!UICONTROL 선택 입력]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)을(를) 탭하고 자산을 탭합니다. 자산이 선택되어 있습니다.

      * 목록 보기에 있는 경우 자산을 마우스로 가리킨 다음 ![selectassetcheckmark](assets/selectassetcheckmark.png) 를 탭합니다. 자산이 선택되어 있습니다.

      * 자산을 탭하여 세부 사항을 표시합니다.
      * 속성 보기 ![속성 보기](assets/viewproperties.png)를 탭하여 자산의 속성을 표시합니다.

1. 게시 취소 프로세스가 시작되면 확인 대화 상자가 나타납니다. **[!UICONTROL 게시 취소]**&#x200B;를 누릅니다.

   >[!NOTE]
   >
   >선택한 자산만 게시 취소되고, 해당 하위 자산과 참조된 자산이 있는 경우 게시 취소되지 않습니다.

## 자산 또는 문자를 이전에 게시된 버전 {#revert-an-asset-or-letter-to-the-previously-published-version}에 되돌리기

자산 또는 문자를 편집한 후 게시할 때마다 자산 또는 문자의 버전이 만들어집니다. 자산이나 문자를 이전에 게시된 버전으로 되돌릴 수 있습니다. 현재 버전의 자산 또는 문서에 문제가 있는 경우 이 작업을 수행해야 할 수 있습니다.

>[!NOTE]
>
>게시된 편지에 사용된 종속 자산이 시스템에서 삭제되는 경우 편지를 마지막으로 게시된 상태로 되돌리지 마십시오.

1. 자산을 선택하고 **[!UICONTROL 이전에 게시된 버전으로 되돌리기]** ![reverttoprevisypublishedversion](assets/reverttopreviouslypublishedversion.png)를 탭합니다.
1. 자산이 반환되기 전에 확인 대화 상자가 나타납니다. **[!UICONTROL 되돌리기]**&#x200B;를 누릅니다.

   자산 또는 문자가 이전에 게시된 버전으로 롤백됩니다.

## 자산 삭제 {#delete-an-asset}

>[!NOTE]
>
>자산을 삭제하면 게시 인스턴스에서 자산이 제거됩니다. 자산을 삭제하면 기본 버전을 제외한 버전 내역도 제거됩니다.

1. 자산을 선택하고 **[!UICONTROL 삭제]** ![삭제](assets/delete.png)를 누릅니다.

   >[!NOTE]
   >
   >삭제 옵션은 자산을 탭하여 자산 세부 사항을 표시하거나 속성 보기 ![속성 보기](assets/viewproperties.png)를 탭하여 자산의 속성을 표시하는 경우에도 사용할 수 있습니다.

1. 자산을 삭제하기 전에 확인 대화 상자가 나타납니다. **[!UICONTROL 삭제]**&#x200B;를 누릅니다.

   >[!NOTE]
   >
   >선택한 자산만 삭제되고 종속 자산만 삭제되며 삭제되지 않습니다. 자산의 참조를 확인하려면 ![참조](assets/references.png)를 탭한 다음 자산을 선택합니다.
   >
   >
   >삭제하려는 자산이 다른 자산의 하위 자산인 경우 삭제되지 않습니다. 이러한 자산을 삭제하려면 다른 자산에서 이 자산의 참조를 제거한 다음 다시 시도하십시오.

## 보호된 적응형 양식 {#protected-adaptive-forms}

선택한 사용자가 액세스할 양식에 대해 인증을 활성화할 수 있습니다. 양식에 대해 인증을 활성화하면 사용자에게 액세스 전에 로그인 화면이 표시됩니다. 권한이 있는 자격 증명이 있는 사용자만 양식에 액세스할 수 있습니다.

양식에 대해 인증을 활성화하려면

1. 브라우저에서 게시 인스턴스에서 configMgr 을 엽니다.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Adobe Experience Manager 웹 콘솔 구성에서 **Apache Sling 인증 서비스**&#x200B;를 클릭하여 구성합니다.
1. 표시되는 Apache Sling 인증 서비스 대화 상자에서 **+** 버튼을 사용하여 경로를 추가합니다.\
   경로를 추가하면 해당 경로에 있는 양식에 대해 인증 서비스가 활성화됩니다.
