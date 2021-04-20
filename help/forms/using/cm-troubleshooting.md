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
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 6%

---


# 통신 관리:{#correspondence-management-troubleshooting} 문제 해결

## 문자 {#errors-when-saving-a-letter} 저장 시 오류 발생

### 문제 {#issue}

문자를 저장할 때 다음 오류 중 하나가 표시되었습니다.

* 텍스트 모듈에 데이터 바인딩이 없습니다.
* 다음에 필요한 속성 정보를 제공하십시오

### 이유 {#reason}

다음 중 하나로 인해 이러한 오류가 발생할 수 있습니다.

* 데이터 사전은 편지에 바인딩되지만 서버에 없습니다.
* 데이터 사전은 이 문자에 바인딩되지만 이름에 밑줄(_)이 있습니다.

### 해결 방법 {#workaround}

문자에서 사용 중인 데이터 사전이 서버에 있으며 이름에 밑줄(_)이 없는지 확인합니다.

## 문자 {#error-when-previewing-a-letter}을(를) 미리 볼 때 오류가 발생했습니다.

### 문제 {#issue-1}

문자를 미리 보는 동안 &quot;편지 로드 중 오류:XML 입력에서 에셋을 가져올 수 없음&quot;은 이전에 게시되지 않은 텍스트 에셋이 게시되더라도 나타납니다.

### 해결 방법 {#workaround-1}

다음 단계를 사용하여 게시 인스턴스에서 편지 캐시를 재설정한 다음 편지 보기를 다시 시도하십시오.

1. **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`**&#x200B;으로 이동하여 관리자로 로그인합니다.
1. **메일 관리 구성**&#x200B;을 선택합니다.
1. **메일 관리 구성**&#x200B;에서 **편지 캐시 사용**&#x200B;을 비활성화한 다음 **저장을 클릭합니다.**
1. **문자 캐시 사용**&#x200B;을 활성화한 다음 **저장**&#x200B;을 클릭합니다.
1. 편지 보기를 다시 시도하십시오.

