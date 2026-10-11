---
title: 레퍼러 필터를 허용으로 설정
description: 레퍼러 필터에 대해 알아봅니다. Adobe Experience Manager(AEM) 모바일 애플리케이션 뷰어가 작성자 인스턴스의 앱을 볼 수 있도록 하려면 HTML 레퍼러 필터를 '허용'으로 설정해야 합니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%
---
# 레퍼러 필터를 허용으로 설정{#setting-your-referrer-filter-to-allow-empty}

{{ue-over-mobile}}

Adobe Experience Manager(AEM) 모바일 애플리케이션 뷰어가 작성자 인스턴스의 앱을 볼 수 있도록 하려면 HTML 레퍼러 필터를 &#39;허용&#39;으로 설정해야 합니다.

응용 프로그램 뷰어를 사용하여 개발 및 스테이징 상태에서 응용 프로그램을 검토하지 않으려는 경우 레퍼러 필터의 기본 설정을 변경할 필요가 없습니다.

실행 중인 AEM 작성자 인스턴스 내에서 [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)&#x200B;(으)로 이동하여 &#39;Apache Sling Referrer Filter&#39;를 검색합니다. 레퍼러 필터를 편집하고 &#39;빈 허용&#39; 확인란을 선택합니다(아래 이미지 참조). 그런 다음 저장 버튼을 누르고 브라우저 페이지를 닫습니다.

![레퍼러 필터 설정](assets/chlimage_1-106.png)
