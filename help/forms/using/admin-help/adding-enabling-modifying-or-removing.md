---
title: 엔드포인트 추가, 활성화, 수정 또는 제거
description: 엔드포인트를 추가, 활성화, 수정 및 제거하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '381'
ht-degree: 100%

---

# 엔드포인트 추가, 활성화, 수정 또는 제거 {#adding-enabling-modifying-or-removing-endpoints}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

## 서비스에 엔드포인트 추가 {#add-an-endpoint-to-a-service}

엔드포인트는 서비스에만 추가할 수 있습니다. 엔드포인트는 단독으로 존재할 수 없으며 서비스와 연결되어야 합니다.

>[!NOTE]
>
>엔드포인트를 추가할 때는 고유한 이름을 사용하는 것이 좋습니다.

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 서비스 관리를 클릭합니다.
1. 서비스 관리 페이지에서 구성할 서비스를 클릭합니다.
1. 엔드포인트 탭에 있는 목록에서 추가할 엔드포인트 유형을 선택하고 추가를 클릭합니다.
1. 엔드포인트 유형에 따라 엔드포인트 설정을 추가로 구성합니다.

[감시 폴더 엔드포인트 설정](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[이메일 엔드포인트 설정](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[작업 관리자 엔드포인트 구성](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[Remoting 엔드포인트 설정](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 추가를 클릭합니다.

## 엔드포인트 활성화 또는 비활성화 {#enable-or-disable-an-endpoint}

기본적으로 새 엔드포인트는 자동으로 활성화됩니다. 하지만 엔드포인트를 비활성화한 경우 작동시키려면 엔드포인트를 활성화해야 합니다.

서비스에 문제가 발생하는 경우 연결된 엔드포인트를 비활성화하면 문제를 더 효과적으로 해결할 수 있습니다. 정기 시스템 유지 관리나 서비스 업그레이드 시에도 엔드포인트를 비활성화하는 것이 좋습니다.

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 엔드포인트 관리를 클릭합니다.
1. 엔드포인트 관리 페이지에서 활성화 또는 비활성화할 엔드포인트의 확인란을 선택하고 활성화 또는 비활성화를 클릭합니다.

## 엔드포인트 수정 {#modify-an-endpoint}

>[!NOTE]
>
>관리 콘솔을 사용하여 엔드포인트 구성에 적용하는 변경 사항은 애플리케이션의 디자인 시점 사본에 반영되지 않습니다. 애플리케이션을 다시 배포하는 경우 관리 콘솔을 사용하여 엔드포인트에 적용한 모든 변경 사항이 손실됩니다.

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 엔드포인트 관리를 클릭합니다.
1. 엔드포인트 관리 페이지에서 수정할 엔드포인트를 클릭합니다.
1. 엔드포인트 업데이트 페이지에서 엔드포인트 이름, 설명 및 설정을 수정합니다.

   >[!NOTE]
   >
   >이름이나 설명에 &lt; 문자를 포함하지 마십시오. Workspace에 표시되는 이름이나 설명이 잘립니다.

1. 변경 사항을 저장하려면 업데이트를 클릭합니다.

서비스 관리 페이지에서 서비스를 선택한 후 엔드포인트 탭을 클릭하여 이 작업을 수행할 수도 있습니다.

## 엔드포인트 제거 {#remove-an-endpoint}

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 엔드포인트 관리를 클릭합니다.
1. 엔드포인트 관리 페이지에서 제거할 엔드포인트의 확인란을 선택하고 제거를 클릭합니다. 엔드포인트가 더 이상 표시되지 않습니다.
