---
title: '"통신 관리:문제 해결"'
seo-title: 통신 관리 문제 해결
description: 통신 관리 문제 해결
seo-description: 통신 관리 문제 해결
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 통신 관리:문제 해결 {#correspondence-management-troubleshooting}

## 편지 저장 시 오류 {#errors-when-saving-a-letter}

### 문제 {#issue}

문자를 저장할 때 표시되는 오류 중 하나:

* 텍스트 모듈에 데이터 바인딩이 없습니다.
* 다음에 필요한 속성 정보를 제공하십시오

### 이유 {#reason}

이러한 오류는 다음 중 하나로 인해 발생할 수 있습니다.

* 데이터 사전은 해당 서신에 바인딩되지만 서버에 없습니다.
* 데이터 사전은 문자에 바인딩되지만 이름에 밑줄(_)이 있습니다.

### 해결 방법 {#workaround}

문자에서 사용 중인 데이터 사전이 서버에 있고 이름에 밑줄(_)이 없는지 확인합니다.

## 편지 미리 보기 오류 {#error-when-previewing-a-letter}

### 문제 {#issue-1}

문자를 미리 보는 동안 &quot;Error in loading letter:XML 입력에서 에셋을 가져올 수 없음&quot;은 이전에 게시되지 않은 텍스트 에셋이 해당 서신의 게시되더라도 나타납니다.

### 해결 방법 {#workaround-1}

다음 단계를 사용하여 게시 인스턴스의 편지 캐시를 재설정한 다음 편지 보기를 다시 시도하십시오.

1. 관리자로 **`https://[server]:[port]/[contextPath]/system/console/configMgr`** 이동하여 로그인합니다.
1. 통신 **관리 구성을 선택합니다**.
1. 통신 **관리 구성에서**&#x200B;편지 **캐시 사용을 비활성화한**&#x200B;다음 저장을 클릭합니다&#x200B;**.**
1. 편지 **캐시 활성화를** 활성화한 다음 저장을 **클릭합니다**.
1. 편지 보기를 다시 시도하십시오.

