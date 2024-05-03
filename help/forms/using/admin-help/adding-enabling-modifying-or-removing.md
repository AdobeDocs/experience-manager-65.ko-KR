---
title: 끝점 추가, 활성화, 수정 또는 제거
description: 엔드포인트를 추가, 활성화, 수정 및 제거하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 끝점 추가, 활성화, 수정 또는 제거 {#adding-enabling-modifying-or-removing-endpoints}

## 서비스에 끝점 추가 {#add-an-endpoint-to-a-service}

끝점은 서비스에만 추가할 수 있습니다. 끝점은 단독으로 존재할 수 없으며 서비스와 연결되어야 합니다.

>[!NOTE]
>
>끝점을 추가할 때 고유한 이름을 사용하는 것이 좋습니다.

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 서비스 관리 를 클릭합니다.
1. 서비스 관리 페이지에서 구성할 서비스를 클릭합니다.
1. 끝점 탭의 목록에서 추가할 끝점 유형을 선택하고 추가 를 클릭합니다.
1. 끝점 유형에 따라 추가 끝점 설정을 구성합니다.

[감시 폴더 끝점 설정](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[이메일 엔드포인트 설정](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[작업 관리자 끝점 구성](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[원격 끝점 설정](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 추가를 클릭합니다.

## 엔드포인트 활성화 또는 비활성화 {#enable-or-disable-an-endpoint}

기본적으로 새 끝점은 자동으로 활성화됩니다. 그러나 끝점을 비활성화한 경우 엔드포인트가 작동하려면 활성화해야 합니다.

서비스에 문제가 있는 경우 관련 끝점을 비활성화하여 문제를 보다 효과적으로 해결하십시오. 또한 정기적인 시스템 유지 관리 또는 서비스 업그레이드 중에 엔드포인트를 비활성화할 수 있습니다.

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > Endpoint Management를 클릭합니다.
1. Endpoint Management 페이지에서 활성화 또는 비활성화할 끝점의 확인란을 선택하고 활성화 또는 비활성화를 누릅니다.

## 엔드포인트 수정 {#modify-an-endpoint}

>[!NOTE]
>
>관리 콘솔을 사용하여 끝점 구성을 변경한 사항은 응용 프로그램의 디자인 타임 사본에 반영되지 않습니다. 응용 프로그램을 다시 배포하면 관리 콘솔을 사용하여 종단점을 변경한 내용이 모두 손실됩니다.

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > Endpoint Management를 클릭합니다.
1. Endpoint Management 페이지에서 수정할 끝점을 클릭합니다.
1. 끝점 업데이트 페이지에서 끝점 이름, 설명 및 설정을 수정합니다.

   >[!NOTE]
   >
   >작업 영역에 표시되는 이름이나 설명이 잘리므로 이름이나 설명에 &lt; 문자를 포함하지 마십시오.

1. 변경 사항을 저장하려면 업데이트를 클릭합니다.

서비스를 선택한 다음 끝점 탭을 클릭하여 서비스 관리 페이지에서 이 작업을 수행할 수도 있습니다.

## 엔드포인트 제거 {#remove-an-endpoint}

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > Endpoint Management를 클릭합니다.
1. Endpoint Management 페이지에서 제거할 끝점의 확인란을 선택하고 제거를 누릅니다. 끝점이 더 이상 표시되지 않습니다.
