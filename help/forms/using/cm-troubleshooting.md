---
title: "서신 관리: 문제 해결"
seo-title: Correspondence Management Troubleshooting
description: 서신 관리 문제 해결
seo-description: Correspondence Management Troubleshooting
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 6%

---

# 서신 관리: 문제 해결 {#correspondence-management-troubleshooting}

## 편지를 저장할 때 오류 발생 {#errors-when-saving-a-letter}

### 문제 {#issue}

편지를 저장할 때 다음 오류 중 하나가 표시됩니다.

* 텍스트 모듈에 대한 데이터 바인딩이 없습니다.
* 다음에 필요한 속성 정보를 제공하십시오

### 이유 {#reason}

다음 중 하나로 인해 이러한 오류가 발생할 수 있습니다.

* 데이터 사전은 편지에 바인딩되어 있지만 서버에 없습니다.
* 데이터 사전은 편지에 바인딩되지만 이름에 밑줄(_)이 있습니다.

### 해결 방법 {#workaround}

편지에서 사용하는 데이터 사전이 서버에 있고 해당 이름에 밑줄(_)이 없는지 확인합니다.

## 문자를 미리 보는 동안 오류가 발생했습니다. {#error-when-previewing-a-letter}

### 문제 {#issue-1}

문자를 미리 보는 동안 &quot;편지 로드 중 오류: 편지에서 이전에 게시 취소된 텍스트 자산이 게시되었더라도 &quot;XML 입력에서 자산을 가져올 수 없습니다.&quot;가 표시됩니다.

### 해결 방법 {#workaround-1}

다음 단계를 사용하여 게시 인스턴스에서 편지 캐시를 재설정한 다음 편지 보기를 다시 시도하십시오.

1. 이동 **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** 관리자로 로그인합니다.
1. 선택 **서신 관리 구성**.
1. in **서신 관리 구성**, 비활성화 **편지 캐시 사용**&#x200B;을 클릭한 다음&#x200B;**저장.**
1. 활성화 **편지 캐시 사용** 을 클릭한 다음 **저장**.
1. 편지 보기를 다시 시도하십시오.
