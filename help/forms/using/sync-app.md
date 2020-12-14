---
title: 앱 동기화
seo-title: 앱 동기화
description: 모바일 디바이스의 AEM Forms 앱을 AEM Forms 서버와 동기화합니다.
seo-description: 모바일 디바이스의 AEM Forms 앱을 AEM Forms 서버와 동기화합니다.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# 앱 동기화 중{#synchronizing-the-app}

## 앱 {#synchronizing-the-app-1} 동기화

앱의 양식은 AEM Forms 서버에서 다운로드됩니다. 양식은 작업 및 Forms 탭 아래에 다운로드됩니다. 양식에서 만든 초안이 초안 탭에 다운로드되고 작업에서 만든 초안이 작업 탭에 다운로드됩니다. OSGi 서버의 독립형 양식의 경우, 양식 및 초안이 각각 Forms 및 초안 탭에서 다운로드됩니다.

양식을 작성하고 제출하면 앱이 온라인 상태인 경우 즉시 AEM Forms 서버로 양식이 다시 업로드됩니다. 앱이 동기화되면 서버에서 양식을 가져옵니다. 그러나 앱이 온라인 상태인 경우 초안이 서버와 즉시 동기화됩니다.

AEM Forms 서버를 통해 온라인 상태이면 기본적으로 앱이 15분마다 동기화됩니다. 그러나 동기화 빈도를 변경할 수 있습니다. 또는 언제든지 앱을 수동으로 동기화할 수 있습니다.

**앱을 수동으로 동기화하려면**

홈 화면의 오른쪽 아래에 있는 동기화 버튼 ![sync-app](assets/sync-app.png)을 누릅니다.

**동기화 빈도를 변경하려면**

1. 설정 화면으로 이동하려면 홈 화면의 왼쪽 위 모서리에 있는 메뉴 단추를 누른 다음 **설정**&#x200B;을 탭합니다.
1. 설정 화면에서 일반 탭을 누릅니다.

   ![일반 설정 창의 동기화 빈도 설정](assets/gen-settings-2.png)

1. 동기화 빈도 옵션에서 동기화 빈도 오른쪽에 있는 값을 누릅니다.
1. 드롭다운 목록에서 새 동기화 빈도를 선택합니다.

### 기술 사양 {#technical-specifications}

* 오프라인 앱 데이터를 AEM Forms 서버에 제출하는 기본 논리는 runtime/offline/util/offline.js에 포함되어 있습니다.
* .js에서 processOfflineSubmittedSavedTasks(..) 함수에 대한 호출은 저장된/제출된 작업을 서버로 전송합니다. 또한 동기화 프로세스에서 오류 또는 충돌을 처리할 수 있습니다. 작업을 제출하지 않으면 앱의 작업이 실패로 표시됩니다. 또한 작업은 보낼 편지함에 남아 있습니다.
* syncSubmittedTask() 및 syncSavedTask() 함수는 개별 작업에 대해 작업을 수행합니다.
* processOfflineSubmittedSavedTasks() 함수에 대한 호출은 사용자가 오프라인 상태를 서버에 동기화하도록 선택하거나 백그라운드 스레드에 의한 자동 동기화를 선택하면 작업 목록 구성 요소에 의해 시작됩니다.
