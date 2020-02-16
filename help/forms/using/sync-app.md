---
title: 앱 동기화
seo-title: 앱 동기화
description: 모바일 장치의 AEM Forms 앱을 AEM Forms 서버와 동기화합니다.
seo-description: 모바일 장치의 AEM Forms 앱을 AEM Forms 서버와 동기화합니다.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 앱 동기화{#synchronizing-the-app}

## 앱 동기화 {#synchronizing-the-app-1}

앱의 양식은 AEM Forms 서버에서 다운로드됩니다. 양식은 작업 및 양식 탭 아래에 다운로드됩니다. 양식에서 만든 초안은 초안 탭에 다운로드되고 작업에서 만든 초안은 작업 탭에 다운로드됩니다. OSGi 서버에서 독립형 양식의 경우 양식과 초안이 각각 양식 및 초안 탭에 다운로드됩니다.

양식을 작성하고 제출하면 앱이 온라인 상태인 경우 양식이 다시 AEM Forms 서버로 업로드됩니다. 앱이 동기화되면 서버에서 양식을 가져옵니다. 그러나 앱이 온라인 상태인 경우 초안이 서버와 즉시 동기화됩니다.

AEM Forms 서버를 사용하여 온라인 상태에서는 기본적으로 앱이 15분마다 동기화됩니다. 그러나 동기화 빈도를 변경할 수 있습니다. 또는 언제든지 앱을 수동으로 동기화할 수 있습니다.

**앱을 수동으로 동기화하려면**

홈 화면의 오른쪽 아래에 있는 동기화 단추 ![동기화 앱을](assets/sync-app.png) 누릅니다.

**동기화 빈도를 변경하려면**

1. 설정 화면으로 이동하려면 홈 화면의 왼쪽 위에 있는 메뉴 단추를 누른 다음 설정을 **누릅니다**.
1. 설정 화면에서 일반 탭을 누릅니다.

   ![일반 설정 창에서 빈도 설정 동기화](assets/gen-settings-2.png)

1. 동기화 빈도 옵션에서 동기화 빈도 오른쪽에 있는 값을 누릅니다.
1. 드롭다운 목록에서 새 동기화 빈도를 선택합니다.

### 기술 사양 {#technical-specifications}

* 오프라인 앱 데이터를 AEM Forms 서버에 제출하는 기본 논리는 runtime/offline/util/offline.js에 포함되어 있습니다.
* .js에서 processOfflineSubmittedSavedTasks(...) 함수에 대한 호출은 저장된/제출된 작업을 서버에 전송합니다. 또한 동기화 프로세스의 오류 또는 충돌을 처리합니다. 작업 제출이 실패하면 앱의 작업이 실패로 표시됩니다. 또한 작업은 보낼 편지함에 남아 있습니다.
* syncSubmittedTask() 및 syncSavedTask() 함수는 개별 작업에 대해 작업을 수행합니다.
* 사용자가 오프라인 상태를 서버에 동기화하도록 선택하거나 백그라운드 스레드로 자동 동기화를 선택하면 processOfflineSubmittedSavedTasks() 함수에 대한 호출이 작업 목록 구성 요소에서 시작됩니다.

[지원 문의](https://www.adobe.com/account/sign-in.supportportal.html)
