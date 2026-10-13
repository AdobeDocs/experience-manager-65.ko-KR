---
title: '서신 관리: 문제 해결'
description: AEM Forms 환경에서 편지를 저장하는 프로세스 중에 발생하는 오류를 처리하는 방법에 대해 알아봅니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 4%
---
# 서신 관리: 문제 해결 {#correspondence-management-troubleshooting}

## 편지 저장 시 오류 발생 {#errors-when-saving-a-letter}

### 문제 {#issue}

편지를 저장할 때 다음 오류 중 하나가 표시됩니다.

* 텍스트 모듈에 대한 데이터 바인딩이 없습니다.
* 다음에 필요한 속성 정보 제공

### 이유 {#reason}

이러한 오류는 다음 중 하나로 인해 발생할 수 있습니다.

* 데이터 사전이 편지에 바인딩되어 있지만 서버에 없습니다.
* 데이터 사전은 편지에 바인딩되어 있지만 이름에 밑줄(_)이 있습니다.

### 해결 방법 {#workaround}

편지에서 사용 중인 데이터 사전이 서버에 있고 이름에 밑줄(_)이 없는지 확인합니다.

## 편지 미리 보기 시 오류 발생 {#error-when-previewing-a-letter}

### 문제 {#issue-1}

문자를 미리 보는 동안 편지에서 이전에 게시되지 않은 텍스트 자산이 게시되는 경우에도 &quot;편지 로드 오류: XML 입력에서 자산을 가져올 수 없습니다&quot; 오류가 표시됩니다.

### 해결 방법 {#workaround-1}

다음 단계를 사용하여 게시 인스턴스에서 편지 캐시를 재설정한 다음 편지 보기를 다시 시도하십시오.

1. **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`**(으)로 이동한 다음 관리자로 로그인합니다.
1. **서신 관리 구성**&#x200B;을 선택하십시오.
1. **서신 관리 구성**&#x200B;에서 **편지 캐시 사용**&#x200B;을 비활성화한 다음 **저장을 클릭하세요.**
1. **편지 캐시 사용**&#x200B;을 선택한 다음 **저장**&#x200B;을 클릭합니다.
1. 편지 보기를 다시 시도하십시오.
