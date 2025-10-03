---
title: '[!DNL Assets] 홈 페이지 환경'
description: ' [!DNL Experience Manager Assets] 홈 페이지를 개인화하여 자산에 대한 최근 활동 스냅샷이 포함된 풍부한 시작 화면 환경을 제공합니다.'
contentOwner: AG
feature: Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '562'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager Assets] 홈 페이지 환경 {#aem-assets-home-page-experience}

[!DNL Adobe Experience Manager Assets] 홈 페이지를 개인화하여 자산에 대한 최근 활동 스냅샷이 포함된 풍부한 시작 화면 환경을 제공합니다.

[!DNL Assets] 홈 페이지는 풍부하고 개인화된 시작 화면 환경을 제공하며 최근에 보거나 업로드한 자산 등 최근 활동 스냅샷을 포함합니다.

[!DNL Assets] 홈 페이지는 기본적으로 비활성화되어 있습니다. 이를 활성화하려면 다음 단계를 수행하십시오.

1. [!DNL Experience Manager] 구성 관리자 `https://[aem_server]:[port]/system/console/configMgr`을 엽니다.
1. **[!UICONTROL Day CQ DAM 이벤트 레코더]** 서비스를 엽니다.
1. **[!UICONTROL 이 서비스 활성화]**&#x200B;를 선택하여 활동 기록을 활성화합니다.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. **[!UICONTROL 이벤트 유형]** 목록에서 기록할 이벤트를 선택하고 변경 사항을 저장합니다.

   >[!CAUTION]
   >
   >열어 본 자산, 열어 본 프로젝트, 열어 본 컬렉션 옵션을 활성화하면 기록되는 이벤트 수가 크게 늘어납니다.

1. 구성 관리자 `https://[aem_server]:[port]/system/console/configMgr`에서 **[!UICONTROL DAM 자산 홈 페이지 기능 플래그]** 서비스를 엽니다.
1. `isEnabled.name` 옵션을 선택하여 [!DNL Assets] 홈 페이지 기능을 활성화합니다. 변경 사항을 저장합니다.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. **[!UICONTROL 사용자 환경 설정]** 대화 상자를 열고 **[!UICONTROL 자산 홈 페이지 활성화]**&#x200B;를 선택합니다. 변경 사항을 저장합니다.

   ![사용자 환경 설정 대화 상자에서 자산 홈 페이지 활성화](assets/Annotation-color.png)

[!DNL Assets] 홈 페이지를 활성화한 후 탐색 페이지에서 [!DNL Assets] 사용자 인터페이스로 이동하거나 `https://[aem_server]:[port]/aem/assetshome.html/content/dam` URL에서 직접 액세스합니다.

![자산 사용자 인터페이스에서 환경 링크 구성](assets/config-experience-link.png)

**[!UICONTROL 환경 링크를 구성하려면 여기를 클릭]**&#x200B;을 클릭하여 사용자 이름, 배경 이미지, 프로필 이미지를 추가합니다.

[!DNL Assets] 홈 페이지는 다음 섹션으로 구성되어 있습니다.

* 시작 섹션
* 위젯 섹션

**시작 섹션**

프로필이 있는 경우 시작 섹션에 사용자에게 전달된 환영 메시지가 표시됩니다. 또한 프로필 사진과 시작 이미지(이미 구성된 경우)가 표시됩니다.

프로필 작성이 완료되지 않은 경우 시작 섹션에 일반 환영 메시지와 프로필 사진을 넣을 자리 표시자가 표시됩니다.

**위젯 섹션**

이 섹션은 시작 섹션 아래에 나타나며 다음 섹션 아래에 기본 제공 위젯을 표시합니다.

* 활동
* 최근
* 검색

**활동**: 이 섹션의 **[!UICONTROL 내 활동]** 위젯은 로그인한 사용자가 자산(렌디션이 없는 자산 포함)을 사용하여 수행한 최근 활동을 표시합니다. 예를 들어 자산 업로드, 다운로드, 자산 생성, 편집, 댓글, 주석, 공유가 있습니다.

**최근에 사용한 항목**: 이 섹션의 **[!UICONTROL 최근에 열어 본 항목]** 위젯은 폴더, 컬렉션, 프로젝트를 포함하여 로그인한 사용자가 최근에 액세스한 엔터티를 표시합니다.

**탐색**: 이 섹션의 **[!UICONTROL 새]** 위젯은 최근에 [!DNL Assets] 배포에 업로드된 자산과 렌디션을 표시합니다.

사용자 활동 데이터 제거를 활성화하려면 구성 관리자에서 **[!UICONTROL DAM 이벤트 제거 서비스]**&#x200B;를 활성화합니다. 이 서비스를 활성화하면 로그인한 사용자의 활동 중 지정된 수를 초과하는 활동은 시스템에서 삭제됩니다.

시작 화면에서는 폴더, 컬렉션, 카탈로그에 액세스할 수 있는 도구 모음 아이콘 등 간편한 탐색 도구를 제공합니다.

>[!NOTE]
>
>[!UICONTROL Day CQ DAM 이벤트 레코더] 및 [!UICONTROL DAM 이벤트 제거] 서비스를 활성화하면 JCR에 대한 쓰기 작업과 검색 색인화가 늘어나 [!DNL Experience Manager] 서버 부하가 크게 증가합니다. [!DNL Experience Manager] 서버에 추가로 가해지는 부하가 성능에 영향을 미칠 수 있습니다.

>[!CAUTION]
>
>[!DNL Assets] 홈 페이지에 필요한 사용자 활용을 캡처하고 필터링하며 제거하는 작업은 성능에 오버헤드를 줄 수 있습니다. 따라서 관리자는 대상 사용자를 위해 홈 페이지를 효과적으로 구성해야 합니다.
>
>대량 작업을 수행하는 관리자와 사용자는 사용자 활동이 증가하는 것을 방지하기 위해 자산 홈 페이지 기능을 사용하지 않는 것이 좋습니다. 또한 관리자는 [!UICONTROL 구성 관리자]에서 [!UICONTROL Day CQ DAM 이벤트 레코더]를 구성하여 특정 사용자에 대한 기록 활동을 제외할 수 있습니다.
>
>해당 기능을 사용하는 경우 서버 부하에 따라 제거 빈도를 예약하는 것이 좋습니다.
