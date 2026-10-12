---
title: PDF Generator 백업 제한 사항
description: PDF Generator 백업 제한 사항을 알아봅니다. PDF Generator가 사용하는 임시 디렉터리는 설정된 간격으로 콘텐츠를 지우기 때문에 백업할 수 없습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
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
source-wordcount: '73'
ht-degree: 100%
---
# PDF Generator 백업 제한 사항 {#pdf-generator-backup-limitations}

PDF Generator가 파일을 변환하는 데 사용하는 임시 디렉터리는 백업할 수 없습니다. 서비스가 제대로 복구되었더라도 PDF Generator가 설정된 간격으로 임시 디렉터리의 콘텐츠를 검토하고 지우기 때문에 데이터가 손실될 수 있습니다.
