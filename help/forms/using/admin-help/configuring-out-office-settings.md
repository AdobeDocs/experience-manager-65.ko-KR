---
title: 부재중 설정 구성
description: 부재중 기능을 사용하면 사용자가 부재중이어서 AEM Forms에서 할당한 작업을 완료할 수 없는 시기를 지정할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '671'
ht-degree: 100%

---

# 부재중 설정 구성 {#configuring-out-of-office-settings}

부재중 기능을 사용하면 사용자 또는 관리자가, 사용자가 부재중이어서 AEM Forms에서 할당한 작업을 완료할 수 없는 시기를 지정할 수 있습니다. 사용자가 부재중으로 설정된 동안 해당 사용자의 작업은 한 명 이상의 지정된 사용자에게 할당됩니다. 사용자는 Workspace에서 부재중 설정을 변경할 수 있고 관리자는 Forms Workflow에서 사용자를 대신하여 해당 설정을 변경할 수 있습니다.

프로세스를 생성할 때 워크벤치 사용자는 부재중 설정으로 인해 작업을 리디렉션할 수 있는지 여부를 지정할 수 있습니다.

## 사용자의 부재중 정보 보기 {#view-a-user-s-out-of-office-information}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

1. 관리 콘솔에서 서비스 > Forms Workflow > 부재중을 클릭합니다.
1. 부재중 페이지 상단 근처의 상자에서 다음 옵션 중 하나를 수행할 수 있습니다.

   **이름별 검색**

   이름별 검색 옵션을 선택합니다. 사용자 이름을 전부 또는 일부 입력하고 찾기를 클릭합니다. 이 필드를 비워 두면 Forms Workflow에서 모든 사용자 목록을 반환합니다.

   **날짜 범위별 검색**

   날짜 범위별 검색 옵션을 선택합니다. 시작 일자 및 종료 일자와 원하는 타임스탬프를 지정하여 검색 결과 범위를 좁힙니다. 찾기를 클릭합니다.

1. 사용자 이름을 클릭하면 사용자 목록 아래에 해당 사용자의 부재중 정보가 표시됩니다.

## 사용자의 부재중 상태 변경 {#change-a-user-s-out-of-office-status}

1. [사용자의 부재중 정보 보기](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)에 설명된 대로 사용자를 찾습니다.
1. 변경할 사용자 이름을 클릭합니다.
1. 현재 *사용자 이름* 목록에서 근무 중 또는 부재중을 선택합니다.
1. 저장을 클릭합니다.

## 사용자의 부재중 날짜 범위 추가 {#add-an-out-of-office-date-range-for-a-user}

1. [사용자의 부재중 정보 보기](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)에 설명된 대로 사용자를 찾습니다.
1. 변경할 사용자 이름을 클릭합니다.
1. 날짜 범위 추가를 클릭합니다.
1. 시작 시간과 종료 시간을 입력합니다. 캘린더 아이콘을 클릭하면 날짜를 선택할 수 있습니다. 종료 시간을 지정하지 않으면 사용자는 무기한 부재중으로 설정됩니다.
1. 저장을 클릭합니다.

## 부재중 작업에 사용자 할당 {#assign-a-user-for-out-of-office-tasks}

사용자가 부재중일 때 한 명 이상의 사용자를 할당하여 해당 사용자의 새 작업을 수행하도록 할 수 있습니다. 다음 구성을 설정할 수 있습니다.

* 모든 새 작업을 지정된 기본 사용자에게 할당합니다.
* 어떠한 작업도 재할당하지 않습니다. 부재중인 사용자에게 새 작업이 계속 할당됩니다.
* 해당 사용자 작업의 대부분을 받을 기본 사용자를 할당하지만, 특정 프로세스의 작업은 다른 사용자에게 재할당되거나 부재중인 사용자에게 계속 할당되도록 지정합니다.
* 기본 사용자를 할당하지 않고 특정 프로세스의 특정 작업을 특정 사용자에게 할당합니다.

   1. [사용자의 부재중 정보 보기](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)에 설명된 대로 사용자를 찾습니다.
   1. 변경할 사용자 이름을 클릭합니다.
   1. 부재중 작업의 기본 사용자 목록에서 사용자를 선택합니다. 재할당된 항목을 받을 기본 사용자를 지정하지 않으려면 할당 안 함을 선택하십시오.

      목록에 해당 사용자 이름이 나타나지 않으면 사용자 찾기를 클릭하고 사용자 찾기 대화 상자를 사용하여 사용자를 검색합니다. 목록에서 해당 사용자를 선택하고 사용자 선택을 클릭합니다. 사용자 찾기 대화 상자에서 사용자 일정 보기를 클릭하면 선택한 사용자의 부재중 일정도 볼 수 있습니다.

   1. 기본 사용자에게 보내면 안 되는 프로세스가 있는 경우 예외 추가를 클릭한 후 해당 프로세스를 선택하고 목록에서 다른 사용자를 선택합니다. 부재중인 사용자에게 작업이 계속 할당되도록 하려면 할당 안 함을 선택할 수도 있습니다.
   1. 저장을 클릭합니다.
