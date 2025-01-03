---
title: 안전 백업 모드 활성화 및 비활성화
description: '[백업 설정] 페이지에서는 데이터베이스 및 GDS(Global Document Storage) 디렉토리를 안정적으로 백업할 수 있도록 AEM Forms를 안전한 백업 모드로 운영할 수 있습니다. 안전 백업 모드를 활성화하고 비활성화하는 방법에 대해 알아봅니다.'
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 안전 백업 모드 활성화 및 비활성화 {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

[백업 설정] 페이지에서는 데이터베이스 및 GDS(Global Document Storage) 디렉토리를 안정적으로 백업할 수 있도록 AEM Forms를 안전한 백업 모드로 운영할 수 있습니다.

AEM Forms는 안전 백업 모드에 있지만 GDS 디렉토리에서 파일을 적극적으로 제거하지 않는다는 점을 제외하면 정상적으로 작동합니다.

>[!NOTE]
>
>이 옵션을 설정하면 시스템이 백업되지 않습니다. 시스템을 백업하도록 준비합니다.

## 안전 백업 모드 사용 {#enable-safe-backup-mode}

1. 관리 콘솔에서 설정 > 핵심 시스템 설정 > 백업 설정 을 클릭합니다.
1. 백업 설정 페이지에서 안전 백업 모드에서 작업을 선택하고 확인을 클릭합니다.

>[!NOTE]
>
>시스템이 이미 안전 백업 모드에서 실행 중인 경우 [확인]을 클릭해도 새 예약이 만들어지지 않습니다.

## 안전 백업 모드 비활성화 {#disable-safe-backup-mode}

1. 관리 콘솔에서 설정 > 핵심 시스템 설정 > 백업 설정 을 클릭합니다.
1. [백업 설정] 페이지에서 [안전 백업 모드에서 작동]을 선택 취소하고 [확인]을 클릭합니다.
