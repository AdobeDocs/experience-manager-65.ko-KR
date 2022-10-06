---
title: 부재 설정 구성
seo-title: Configuring Out of Office Settings
description: 부재 기능을 사용하면 사용자가 부재 중일 시기를 지정하고 AEM Forms에서 지정한 작업을 완료할 수 없습니다.
seo-description: The Out of Office feature enables you to specify when a user will be out of the office and unable to complete tasks assigned by AEM forms.
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 부재 설정 구성 {#configuring-out-of-office-settings}

부재 기능을 사용하면 사용자 또는 관리자가 사용자가 부재 중일 시기를 지정하고 AEM Forms에서 지정한 작업을 완료할 수 없습니다. 사용자가 부재 로 설정되는 동안 사용자의 작업은 하나 이상의 지정된 사용자에게 할당됩니다. 사용자는 Workspace에서 부재 설정 을 변경하거나 관리자는 Forms Workflow에서 사용자를 대신하여 설정을 변경할 수 있습니다.

프로세스를 만들 때 Workbench 사용자는 부재 설정으로 인해 작업을 리디렉션할 수 있는지 여부를 지정할 수 있습니다.

## 사용자의 부재 중 정보 보기 {#view-a-user-s-out-of-office-information}

1. 관리 콘솔에서 서비스 > 양식 워크플로우 > 부재 중 을 클릭합니다.
1. 부재 페이지 상단 근처에 있는 상자에서 다음 중 하나를 수행할 수 있습니다.

   **이름별로 검색**

   이름별 검색 옵션을 선택합니다. 사용자 이름의 전체 또는 일부를 입력하고 찾기를 클릭합니다. 필드를 비워 두면 Forms 워크플로우는 모든 사용자 목록을 반환합니다

   **날짜 범위별로 검색**

   날짜 범위별 검색 옵션을 선택합니다. 검색 결과 범위를 좁히려면 시작 및 종료 날짜를 원하는 타임스탬프와 함께 지정합니다. 찾기를 클릭합니다.

1. 사용자 이름 을 클릭하여 사용자 목록 아래에 사용자의 부재 중 정보를 표시합니다.

## 사용자의 부재 상태 변경 {#change-a-user-s-out-of-office-status}

1. 에 설명된 대로 사용자를 찾습니다. [사용자의 부재 중 정보 보기](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 변경할 사용자의 이름을 클릭합니다.
1. 에서 *사용자 이름* 현재 목록인 경우 [Office에서] 또는 [Out of the Office]를 선택합니다.
1. 저장을 클릭합니다.

## 사용자의 부재 날짜 범위 추가 {#add-an-out-of-office-date-range-for-a-user}

1. 에 설명된 대로 사용자를 찾습니다. [사용자의 부재 중 정보 보기](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 변경할 사용자의 이름을 클릭합니다.
1. 날짜 범위 추가를 클릭합니다.
1. 시작 시간 및 종료 시간을 입력합니다. 달력 아이콘을 클릭하여 날짜를 선택할 수 있습니다. 종료 시간을 지정하지 않으면 사용자가 무기한 부재 상태로 설정됩니다.
1. 저장을 클릭합니다.

## 부재 작업 사용자 할당 {#assign-a-user-for-out-of-office-tasks}

사용자가 부재 중일 때 한 명 이상의 사용자를 할당하여 사용자를 위해 새로운 작업을 수행할 수 있습니다. 다음 구성을 설정할 수 있습니다.

* 모든 새 작업을 지정된 기본 사용자에게 할당합니다.
* 작업을 재할당하지 마십시오. 부재 중인 사용자에게 새 작업이 계속 할당됩니다.
* 사용자의 대부분의 작업을 받을 기본 사용자를 할당하되 특정 프로세스의 작업이 다른 사용자에게 재할당되거나 부재 중인 사용자에게 할당되도록 지정합니다.
* 기본 사용자를 할당하지 않고 특정 프로세스의 특정 작업을 특정 사용자에게 할당합니다.

   1. 에 설명된 대로 사용자를 찾습니다. [사용자의 부재 중 정보 보기](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. 변경할 사용자의 이름을 클릭합니다.
   1. 부재 작업의 기본 사용자 목록에서 사용자를 선택합니다. 재지정된 항목을 받을 기본 사용자를 지정하지 않으려면 지정 안 함을 선택합니다.

      해당 사용자 이름이 목록에 표시되지 않으면 사용자 찾기를 클릭하고 사용자 찾기 대화 상자를 사용하여 사용자를 검색합니다. 목록에서 해당 사용자를 선택하고 사용자 선택을 클릭합니다. 사용자 찾기 대화 상자에서 사용자 일정 보기 를 클릭하여 선택한 사용자의 부재 일정을 확인할 수도 있습니다.

   1. 기본 사용자에게 전송하지 않아야 하는 프로세스가 있는 경우 예외 추가를 누른 다음 프로세스를 선택하고 목록에서 다른 사용자를 선택합니다. [할당 안 함]을 선택하여 부재 중인 사용자에게 작업을 계속 할당할 수도 있습니다.
   1. 저장을 클릭합니다.
