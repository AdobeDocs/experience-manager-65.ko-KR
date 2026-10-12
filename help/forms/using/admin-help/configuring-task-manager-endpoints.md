---
title: 작업 관리자 엔드포인트 구성
description: 서비스를 호출하도록 작업 관리자 엔드포인트를 구성하는 방법을 알아봅니다. 작업 관리자 엔드포인트를 구성하려면 서로 다른 설정이 필요합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
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
source-wordcount: '245'
ht-degree: 100%
---
# 작업 관리자 엔드포인트 구성 {#configuring-task-manager-endpoints}

Workspace 사용자는 작업 관리자 엔드포인트를 통해 서비스를 호출할 수 있습니다.

**작업 관리자 엔드포인트 설정**

다음 설정을 사용하여 작업 관리자 엔드포인트를 구성합니다.

**이름:** (필수) 엔드포인트를 식별합니다. 이름은 Workspace의 카드 보기에 표시됩니다. &lt; 문자를 포함하지 마십시오. Workspace에 표시되는 이름이 잘립니다. 엔드포인트 이름으로 URL을 입력하는 경우 해당 URL이 RFC1738에 지정된 구문 규칙을 준수하는지 확인하십시오.

**설명:** 엔드포인트에 대한 설명입니다. &lt; 문자를 포함하지 마십시오. Workspace에 표시되는 설명이 잘립니다.

**작업 지침:** 이 워크플로를 시작하는 사용자를 위한 지침입니다.

**프로세스 소유자:** 프로세스를 담당자 이름입니다.

**사용자가 작업을 전달할 수 있음:** 사용자가 초기 작업을 전달할 수 있습니다.

**첨부 파일 창 표시:** 사용자가 첨부 파일 창을 볼 수 있도록 합니다.

**첨부 파일 추가 허용:** 사용자가 첨부 파일과 메모를 추가할 수 있도록 합니다.

**작업 초기 잠금:** 초기 작업을 잠급니다.

**공유 대기열에 대한 ACL 추가:** 초기 작업은 공유 대기열 사용자에 대한 ACL로 생성됩니다.

**분류:** (필수) 사용자가 Workspace에서 양식을 볼 수 있는 카테고리입니다. 목록에서 카테고리를 선택하거나 새 카테고리를 선택하여 카테고리를 추가합니다.

**작업 이름:** (필수) 엔드포인트에 할당할 수 있는 작업 목록입니다.
