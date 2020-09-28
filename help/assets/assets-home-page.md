---
title: '[!DNL 자산] 홈 페이지 경험'
description: 홈 페이지 [!DNL Experience Manager Assets] 를 개인화하여 최근 자산 활동 요약 등 다양한 시작 화면 환경을 제공합니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] 홈 페이지 경험 {#aem-assets-home-page-experience}

자산에 대한 최근 활동 요약 등 다양한 시작 화면 환경을 위한 [!DNL Adobe Experience Manager Assets] 홈 페이지를 개인화할 수 있습니다.

[!DNL Assets] 홈 페이지는 최근 보거나 업로드된 자산과 같은 최근 활동의 요약 정보를 포함하는 풍부하고 개인화된 시작 화면 환경을 제공합니다.

홈 [!DNL Assets] 페이지는 기본적으로 비활성화됩니다. 활성화하려면 다음 단계를 수행하십시오.

1. 구성 [!DNL Experience Manager] 관리자를 엽니다 `https://[aem_server]:[port]/system/console/configMgr`.
1. Day **[!UICONTROL CQ DAM 이벤트 레코더]** 서비스를 엽니다.
1. 활동 **[!UICONTROL 기록을 활성화하려면 이 서비스]** 활성화를 선택합니다.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. [ **[!UICONTROL 이벤트 유형]** ] 목록에서 기록할 이벤트를 선택하고 변경 내용을 저장합니다.

   >[!CAUTION]
   >
   >조회한 자산, 본 프로젝트 및 본 컬렉션 옵션을 활성화하면 기록된 이벤트의 수가 크게 증가합니다.

1. Configuration Manager에서 **[!UICONTROL DAM 자산 홈 페이지 기능 플래그]** 서비스를 엽니다 `https://[aem_server]:[port]/system/console/configMgr`.
1. 홈 페이지 기능 `isEnabled.name` 을 활성화하려면 [!DNL Assets] 옵션을 선택합니다. 변경 사항을 저장합니다.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. [ **[!UICONTROL 사용자 환경 설정]** ] 대화 상자를 열고 [자산 홈 페이지 **[!UICONTROL 활성화]를 선택합니다]**. 변경 사항을 저장합니다.

   ![사용자 환경 설정 대화 상자에서 자산 홈 페이지 활성화](assets/Annotation-color.png)

홈 페이지를 [!DNL Assets] 활성화한 후 탐색 페이지에서 [!DNL Assets] 사용자 인터페이스로 이동하거나 URL에서 직접 액세스합니다 `https://[aem_server]:[port]/aem/assetshome.html/content/dam`.

![자산 사용자 인터페이스에서 경험 링크 구성](assets/config-experience-link.png)

사용자 **[!UICONTROL 이름, 배경 이미지 및 프로필 이미지를 추가하기 위해 경험 링크를]** 구성하려면 여기를 클릭하십시오.

홈 [!DNL Assets] 페이지에는 다음 섹션이 포함됩니다.

* 시작 섹션
* 위젯 섹션

**시작 섹션**

프로필이 있으면 시작 섹션에 전송된 환영 메시지가 표시됩니다. 또한 프로필 사진과 시작 이미지를 표시합니다(이미 구성된 경우).

프로필이 불완전한 경우 시작 섹션에 일반 환영 메시지와 프로필 사진 자리 표시자가 표시됩니다.

**위젯 섹션**

이 섹션은 시작 섹션 아래에 나타나며 다음 섹션 아래에 즉시 사용 가능한 위젯을 표시합니다.

* 활동
* 최근
* 검색

**활동**:이 섹션에서 **[!UICONTROL 내 활동]** 위젯은 로그인한 사용자가 자산(변환되지 않은 자산 포함)을 사용하여 수행한 최근 활동을 자산 업로드, 다운로드, 자산 생성, 편집, 댓글, 주석 및 공유 등의 방법으로 표시합니다.

**최근**:이 섹션 **[!UICONTROL 아래의 최근 조회]** 위젯은 폴더, 컬렉션, 프로젝트 등 로그인한 사용자가 최근에 액세스한 개체를 표시합니다.

**Discover**:이 섹션 **[!UICONTROL 아래의 새]** 위젯에는 최근 배포에 업로드된 자산 및 표현물이 [!DNL Assets] 표시됩니다.

사용자 활동 데이터 제거를 활성화하려면 Configuration Manager에서 **[!UICONTROL DAM 이벤트 제거 서비스를]** 활성화합니다. 이 서비스를 활성화하면 지정된 수를 초과하는 로그인한 사용자의 활동이 시스템에서 삭제됩니다.

시작 화면은 도구 모음의 아이콘 등 폴더, 컬렉션 및 카탈로그에 액세스하기 위한 편리한 탐색 도구를 제공합니다.

>[!NOTE]
>
>CQ [!UICONTROL DAM 이벤트 레코더] 및 [!UICONTROL DAM 이벤트 삭제] 서비스를 활성화하면 JCR 및 검색 색인 작성 작업이 증가하여 [!DNL Experience Manager] 서버 부하가 크게 증가합니다. 서버에 대한 추가 로드는 [!DNL Experience Manager] 성능에 영향을 줄 수 있습니다.

>[!CAUTION]
>
>홈 페이지에 필요한 사용자 활동을 캡처, 필터링 및 [!DNL Assets] 삭제하여 성능에 오버헤드를 적용합니다. 따라서 관리자는 대상 사용자에 대해 홈 페이지를 효과적으로 구성해야 합니다.
>
>Adobe은 벌크 작업을 수행하는 관리자와 사용자가 사용자 활동의 증가를 방지하기 위해 자산 홈 페이지 기능을 사용하지 않는 것이 좋습니다. 또한 관리자는 Configuration Manager에서 [!UICONTROL 일 CQ DAM 이벤트 레코더를 구성하여 특정 사용자에 대한 레코딩 활동을] 제외할 수 [!UICONTROL 있습니다].
>
>이 기능을 사용하는 경우 서버 로드를 기준으로 제거 빈도를 예약하는 것이 좋습니다.
