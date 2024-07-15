---
title: "[!DNL Assets] 홈 페이지 경험"
description: 자산에 대한 최근 활동 스냅숏을 포함하여 다양한 시작 화면 환경을 위해  [!DNL Experience Manager Assets] 홈 페이지를 개인화합니다.
contentOwner: AG
feature: Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager Assets] 홈 페이지 경험 {#aem-assets-home-page-experience}

자산에 대한 최근 활동 스냅숏을 포함하여 다양한 시작 화면 환경을 위해 [!DNL Adobe Experience Manager Assets] 홈 페이지를 개인화합니다.

[!DNL Assets] 홈 페이지는 최근에 보거나 업로드한 에셋과 같은 최근 활동에 대한 스냅숏을 포함하여 풍부하고 개인화된 시작 화면 환경을 제공합니다.

[!DNL Assets] 홈 페이지는 기본적으로 비활성화되어 있습니다. 활성화하려면 다음 단계를 수행하십시오.

1. [!DNL Experience Manager] 구성 관리자 `https://[aem_server]:[port]/system/console/configMgr`을(를) 엽니다.
1. **[!UICONTROL 일 CQ DAM 이벤트 레코더]** 서비스를 엽니다.
1. 활동 기록을 사용하려면 **[!UICONTROL 이 서비스를 사용하도록 설정]**&#x200B;을 선택하세요.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. **[!UICONTROL 이벤트 유형]** 목록에서 기록할 이벤트를 선택하고 변경 내용을 저장합니다.

   >[!CAUTION]
   >
   >에셋 조회, 프로젝트 조회 및 컬렉션 조회 옵션을 활성화하면 기록된 이벤트의 수가 크게 증가합니다.

1. 구성 관리자 `https://[aem_server]:[port]/system/console/configMgr`에서 **[!UICONTROL DAM 자산 홈 페이지 기능 플래그]** 서비스를 엽니다.
1. [!DNL Assets] 홈 페이지 기능을 사용하려면 `isEnabled.name` 옵션을 선택하십시오. 변경 사항을 저장합니다.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. **[!UICONTROL 사용자 환경 설정]** 대화 상자를 열고 **[!UICONTROL Assets 홈 페이지 사용]**&#x200B;을 선택합니다. 변경 사항을 저장합니다.

   ![사용자 환경 설정 대화 상자에서 에셋 홈 페이지 사용](assets/Annotation-color.png)

[!DNL Assets] 홈 페이지를 사용하도록 설정한 후 탐색 페이지에서 [!DNL Assets] 사용자 인터페이스로 이동하거나 URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`에서 직접 액세스합니다.

![Assets 사용자 인터페이스에서 경험 링크 구성](assets/config-experience-link.png)

사용자 이름, 배경 이미지 및 프로필 이미지를 추가하려면 **[!UICONTROL 여기를 클릭하여 경험 링크를 구성하십시오]**.

[!DNL Assets] 홈 페이지에는 다음 섹션이 포함되어 있습니다.

* 시작 섹션
* 위젯 섹션

**시작 섹션**

프로필이 있는 경우 시작 섹션에 주소가 지정된 시작 메시지가 표시됩니다. 또한 프로필 사진과 시작 이미지가 표시됩니다(이미 구성된 경우).

프로필이 불완전한 경우 시작 섹션에는 일반적인 시작 메시지와 프로필 사진에 대한 자리 표시자가 표시됩니다.

**위젯 섹션**

이 섹션은 시작 섹션 아래에 표시되며 다음 섹션 아래에 기본 위젯이 표시됩니다.

* 활동
* 최근
* 검색

**활동**: 이 섹션 아래에서 **[!UICONTROL 내 활동]** 위젯에 에셋(렌디션이 없는 에셋 포함)과 함께 로그인한 사용자가 수행한 최근 활동(예: 에셋 업로드, 다운로드, 에셋 생성, 편집, 댓글, 주석 및 공유)이 표시됩니다.

**최근 항목**: 이 섹션 아래의 **[!UICONTROL 최근에 본 항목]** 위젯은 폴더, 컬렉션 및 프로젝트를 포함하여 로그인한 사용자가 최근에 액세스한 엔터티를 표시합니다.

**검색**: 이 섹션 아래의 **[!UICONTROL 새로 만들기]** 위젯에는 [!DNL Assets] 배포에 최근에 업로드한 에셋 및 표현물이 표시됩니다.

사용자 활동 데이터를 제거하려면 구성 관리자에서 **[!UICONTROL DAM 이벤트 제거 서비스]**&#x200B;를 사용하도록 설정하십시오. 이 서비스를 사용하면 로그인한 사용자가 지정한 수를 초과하는 활동이 시스템에서 삭제됩니다.

시작 화면에서는 폴더, 컬렉션 및 카탈로그에 액세스할 수 있는 아이콘과 같은 간단한 탐색 도구를 제공합니다.

>[!NOTE]
>
>[!UICONTROL 일 CQ DAM 이벤트 레코더] 및 [!UICONTROL DAM 이벤트 제거] 서비스를 사용하면 JCR 및 검색 색인화에 대한 쓰기 작업이 증가하여 [!DNL Experience Manager] 서버의 로드가 크게 증가합니다. [!DNL Experience Manager] 서버에 대한 추가 로드는 성능에 영향을 줄 수 있습니다.

>[!CAUTION]
>
>[!DNL Assets] 홈 페이지에 필요한 사용자 활동을 캡처, 필터링 및 지우면 성능에 오버헤드가 발생합니다. 따라서 관리자는 타겟 사용자를 위해 홈 페이지를 효과적으로 구성해야 합니다.
>
>Adobe은 대량 작업을 수행하는 관리자 및 사용자는 에셋 홈페이지 기능을 사용하여 사용자 활동이 증가하지 않도록 할 것을 권장합니다. 또한 관리자는 [!UICONTROL 구성 관리자]에서 [!UICONTROL 일 CQ DAM 이벤트 기록기]를 구성하여 특정 사용자에 대한 기록 활동을 제외할 수 있습니다.
>
>Adobe 이 기능을 사용하는 경우 서버 로드를 기준으로 제거 빈도를 예약하는 것이 좋습니다.
