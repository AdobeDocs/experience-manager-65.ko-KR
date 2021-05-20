---
title: 끝점 추가, 활성화, 수정 또는 제거
seo-title: 끝점 추가, 활성화, 수정 또는 제거
description: 끝점을 추가, 활성화, 수정 및 제거하는 방법을 알아봅니다.
seo-description: 끝점을 추가, 활성화, 수정 및 제거하는 방법을 알아봅니다.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 끝점 {#adding-enabling-modifying-or-removing-endpoints} 추가, 활성화, 수정 또는 제거

## 서비스 {#add-an-endpoint-to-a-service}에 끝점 추가

끝점은 서비스에만 추가할 수 있습니다. 끝점은 단독으로 존재할 수 없습니다.서비스와 연결되어 있어야 합니다.

>[!NOTE]
>
>끝점을 추가할 때는 고유 이름을 사용하는 것이 좋습니다.

1. 관리 콘솔에서 서비스 > 애플리케이션 및 서비스 > 서비스 관리를 클릭합니다.
1. 서비스 관리 페이지에서 구성할 서비스를 클릭합니다.
1. 끝점 탭의 목록에서 추가할 끝점 유형을 선택하고 추가 를 클릭합니다.
1. 끝점 유형에 따라 추가 끝점 설정을 구성합니다.

[감시 폴더 끝점 설정](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[전자 메일 끝점 설정](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[작업 관리자 끝점 구성](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[원격 끝점 설정](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 추가를 클릭합니다.

## 끝점 {#enable-or-disable-an-endpoint} 활성화 또는 비활성화

기본적으로 새 엔드포인트는 자동으로 활성화됩니다. 그러나 종단점을 비활성화한 경우 종단점이 작동하도록 설정해야 합니다.

서비스에 문제가 발생하는 경우 관련 끝점을 비활성화하여 문제를 더 잘 해결하십시오. 일반 시스템 유지 관리 중에 또는 서비스를 업그레이드할 때 끝점을 비활성화할 수도 있습니다.

1. 관리 콘솔에서 서비스 > 응용 프로그램 및 서비스 > 끝점 관리 를 클릭합니다.
1. Endpoint Management 페이지에서 엔드포인트에 대한 확인란을 활성화 또는 비활성화하고 활성화 또는 비활성화를 클릭합니다.

## 끝점 수정 {#modify-an-endpoint}

>[!NOTE]
>
>관리 콘솔을 사용하여 엔드포인트 구성에 변경한 내용은 애플리케이션의 디자인 타임 사본에 반영되지 않습니다. 응용 프로그램을 재배포하는 경우 관리 콘솔을 사용하여 종단점에 변경한 내용이 모두 손실됩니다.

1. 관리 콘솔에서 서비스 > 응용 프로그램 및 서비스 > 끝점 관리 를 클릭합니다.
1. Endpoint Management 페이지에서 수정할 끝점을 클릭합니다.
1. 끝점 업데이트 페이지에서 끝점 이름, 설명 및 설정을 수정합니다.

   >[!NOTE]
   >
   >작업 공간에서 표시되는 이름 또는 설명이 잘리기 때문에 이름 또는 설명에 &lt; 문자를 포함하지 마십시오.

1. 변경 사항을 저장하려면 업데이트를 클릭합니다.

서비스를 선택한 다음 엔드포인트 탭을 클릭하여 서비스 관리 페이지에서 이 작업을 수행할 수도 있습니다.

## 끝점 제거 {#remove-an-endpoint}

1. 관리 콘솔에서 서비스 > 응용 프로그램 및 서비스 > 끝점 관리 를 클릭합니다.
1. 끝점 관리 페이지에서 제거할 끝점에 대한 확인란을 선택하고 제거를 클릭합니다. 끝점이 더 이상 표시되지 않습니다.
