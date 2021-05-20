---
title: 레퍼러 필터를 비워 둡니다.
seo-title: 레퍼러 필터를 비워 둡니다.
description: 레퍼러 필터에 대해 알려면 이 페이지를 따르십시오. AEM Mobile Application Viewer가 작성자 인스턴스에서 앱을 볼 수 있도록 하려면 HTML 레퍼러 필터를 '빈 허용'으로 설정해야 합니다.
seo-description: 레퍼러 필터에 대해 알려면 이 페이지를 따르십시오. AEM Mobile Application Viewer가 작성자 인스턴스에서 앱을 볼 수 있도록 하려면 HTML 레퍼러 필터를 '빈 허용'으로 설정해야 합니다.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 3%

---

# 레퍼러 필터를 Empty{#setting-your-referrer-filter-to-allow-empty}로 설정

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM Mobile Application Viewer가 작성자 인스턴스에서 앱을 볼 수 있도록 하려면 HTML 레퍼러 필터를 &#39;빈 허용&#39;으로 설정해야 합니다.

애플리케이션 뷰어를 사용하여 개발 및 스테이징 상태 내에서 애플리케이션을 검토하지 않으려는 경우 레퍼러 필터의 기본 설정을 변경할 필요가 없습니다.

실행 중인 AEM 작성자 인스턴스 내에서 다음 위치로 이동합니다.[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) 및 &#39;Apache Sling Referrer Filter&#39;를 검색합니다. 를 클릭하여 레퍼러 필터를 편집하고 &#39;빈 항목 허용&#39; 확인란을 선택합니다(아래 이미지 참조). 다음 저장 단추를 누르고 브라우저 페이지를 닫습니다.

![레퍼러 필터 설정](assets/chlimage_1-106.png)
