---
title: 비어 있는 참조를 허용하도록 레퍼러 필터 설정
seo-title: 비어 있는 참조를 허용하도록 레퍼러 필터 설정
description: 레퍼러 필터에 대해 알려면 이 페이지를 따르십시오. AEM Mobile Application Viewer가 작성자 인스턴스의 앱을 보도록 허용하려면 HTML 레퍼러 필터를 '빈 항목 허용'으로 설정해야 합니다.
seo-description: 레퍼러 필터에 대해 알려면 이 페이지를 따르십시오. AEM Mobile Application Viewer가 작성자 인스턴스의 앱을 보도록 허용하려면 HTML 레퍼러 필터를 '빈 항목 허용'으로 설정해야 합니다.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 3%

---


# 레퍼러 필터를 빈 {#setting-your-referrer-filter-to-allow-empty}으로 설정

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM Mobile Application Viewer가 작성자 인스턴스의 앱을 보도록 허용하려면 HTML 레퍼러 필터를 &#39;빈 항목 허용&#39;으로 설정해야 합니다.

Application Viewer를 사용하여 개발 및 스테이징 상태 내의 애플리케이션을 검토하지 않을 경우 레퍼러 필터의 기본 설정을 변경할 필요가 없습니다.

실행 중인 AEM 작성자 인스턴스 내에서 다음 위치로 이동합니다.[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)을(를) 사용하여 &#39;Apache Sling 레퍼러 필터&#39;를 검색합니다. 레퍼러 필터를 편집하려면 클릭하고 &#39;빈 항목 허용&#39; 확인란을 선택합니다(아래 이미지 참조). 저장 단추를 누르고 브라우저 페이지를 닫습니다.

![레퍼러 필터 설정](assets/chlimage_1-106.png)
