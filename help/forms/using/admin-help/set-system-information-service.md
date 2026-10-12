---
title: 시스템 정보 서비스 설정
description: 시스템 정보 서비스를 설정하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 734ed463-2441-49fc-bacb-deb40851af42
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
source-wordcount: '114'
ht-degree: 100%
---
# 시스템 정보 서비스 설정 {#set-up-the-system-information-service}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

시스템 정보 서비스에서는 정보를 가져오기 위한 REST API를 제공합니다. 시스템 정보 서비스를 사용하려면 관리 콘솔에서 REST 엔드포인트를 활성화합니다. REST 엔드포인트를 활성화하려면 다음 단계를 수행하십시오.

1. 관리 콘솔에 로그인합니다. 관리 콘솔의 기본 URL은 `https://[hostname]:'port'/adminui.`입니다.
1. 서비스 > 애플리케이션 및 서비스 > 서비스 관리로 이동합니다.
1. 서비스 관리 페이지에서 **SystemInfo** 서비스를 클릭합니다.
1. 엔드포인트 탭 목록에서 REST를 선택하고 **추가**&#x200B;를 클릭합니다.
1. REST 엔드포인트 추가 화면에서 **추가**&#x200B;를 클릭합니다.
