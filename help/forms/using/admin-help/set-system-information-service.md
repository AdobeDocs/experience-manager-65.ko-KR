---
title: 시스템 정보 서비스 설정
description: 시스템 정보 서비스를 설정하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 734ed463-2441-49fc-bacb-deb40851af42
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 시스템 정보 서비스 설정 {#set-up-the-system-information-service}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인합니다.

시스템 정보 서비스는 정보를 검색할 수 있는 REST API를 제공합니다. 시스템 정보 서비스를 사용하려면 관리 콘솔에서 REST 끝점을 사용하도록 설정하십시오. REST 끝점을 활성화하려면 다음 단계를 수행하십시오.

1. 관리 콘솔에 로그인합니다. 관리 콘솔의 기본 URL은 `https://[hostname]:'port'/adminui.`입니다.
1. 서비스 > 애플리케이션 및 서비스 > 서비스 관리로 이동합니다.
1. 서비스 관리 페이지에서 **SystemInfo** 서비스를 클릭합니다.
1. 끝점 탭의 목록에서 REST를 선택하고 **추가**&#x200B;를 클릭합니다.
1. REST 끝점 추가 화면에서 **추가**&#x200B;를 클릭합니다.
