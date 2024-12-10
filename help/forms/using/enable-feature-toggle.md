---
title: 얼리어답터 및 프리릴리스 기능 통합을 위한 기능 전환 활성화
description: 기능 토글 은 관리자가 런타임 환경에서 새로운 기능을 활성화할 수 있는 AEM의 기능입니다.
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
source-git-commit: 794d93d890ba752f9036a85831f7cbc8391fb545
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 2%

---

# Adobe Experience Manager(AEM) 6.5의 기능 전환{#enable-feature-toggle-aem-forms-65}

기능 토글 은 관리자가 특정 기능을 동적으로 활성화 또는 비활성화할 수 있는 AEM의 기능입니다. 이 기능은 코드 베이스에 대한 주요 배포 또는 변경 없이 **얼리어답터 기능** 및 **프리릴리스 기능**&#x200B;을 관리하는 데 특히 유용합니다. AEM 환경에서 액세스할 수 있는 기능을 유연하게 제어할 수 있습니다.

## 기능 활성화 전환 {#enable-feature-toggle-65}

조기 채택자 또는 새 기능에 대한 기능 전환은 아래 단계에 따라 **AEM 웹 콘솔**&#x200B;을 통해 구성할 수 있습니다.

1. AEM Forms 인스턴스에 로그인.
2. 다음으로 이동 `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. 구성 관리자에서 **Adobe Granite 동적 전환 공급자**&#x200B;를 검색합니다.
4. ![연필 아이콘](assets/illustratorcc_penciltool_cur_edit_2_17.png) 아이콘을 클릭합니다.
5. [!UICONTROL 전환 사용] 섹션에서 ![연필 아이콘](assets/aem6forms_add.png)을 클릭하세요.
6. 아래 이미지에 표시된 대로 기능에 대한 기능 전환 ID를 추가합니다.
   ![전환 추가](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >얼리어답터 기능과 관련된 문서에서 기능 전환 ID를 찾을 수 있습니다.

7. 저장을 클릭합니다.

## 기능 비활성화 전환 {#disable-feature-toggle-65}

토글이 활성화된 피쳐에 대해 피쳐 토글을 비활성화하려면 아래 단계를 따르십시오.

1. AEM Forms 인스턴스에 로그인.
2. 다음으로 이동 `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. 구성 관리자에서 **Adobe Granite 동적 전환 공급자**&#x200B;를 검색합니다.
4. ![연필 아이콘](assets/illustratorcc_penciltool_cur_edit_2_17.png) 아이콘을 클릭합니다.
5. [!UICONTROL 토글 사용 안 함] 섹션에서 ![연필 아이콘](assets/aem6forms_add.png)을 클릭하세요.
6. 비활성화할 기능의 토글 번호를 추가합니다.
   ![토글 제거](assets/remove_toggle_feature_forms.png)
7. 저장을 클릭합니다.

## 기술적 고려 사항

기능 전환은 환경에 따라 다르며 런타임 시 관리되므로 서버를 다시 시작할 필요가 없습니다. 그러나 일부 기능을 사용하려면 관련 페이지를 새로 고치거나 변경 사항을 반영하도록 캐시를 지워야 할 수 있습니다.
`http://<author-instance-url>:4502/etc.clientlibs/toggles.json`을(를) 통해 환경에 대한 기능 전환을 통해 활성화된 기능 목록에 액세스할 수 있습니다.