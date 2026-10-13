---
title: 안전 백업 모드 활성화 및 비활성화
description: '[백업 설정] 페이지에서는 데이터베이스 및 GDS(Global Document Storage) 디렉토리를 안정적으로 백업할 수 있도록 AEM 양식을 안전한 백업 모드로 운영할 수 있습니다. 안전 백업 모드를 활성화하고 비활성화하는 방법에 대해 알아봅니다.'
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 11%
---
# 안전 백업 모드 활성화 및 비활성화 {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

[백업 설정] 페이지에서는 데이터베이스 및 GDS(Global Document Storage) 디렉토리를 안정적으로 백업할 수 있도록 AEM 양식을 안전한 백업 모드로 운영할 수 있습니다.

AEM Forms는 안전 백업 모드에 있지만 GDS 디렉터리에서 파일을 적극적으로 제거하지 않는다는 점을 제외하면 정상적으로 작동합니다.

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
