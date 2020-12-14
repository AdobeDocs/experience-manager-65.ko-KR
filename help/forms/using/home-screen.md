---
title: 홈 화면
seo-title: 홈 화면
description: AEM Forms 앱 홈 화면의 구성 요소에 대한 설명
seo-description: AEM Forms 앱 홈 화면의 구성 요소에 대한 설명
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# 홈 화면{#home-screen}

AEM Forms 앱에 로그인하면 홈 화면으로 리디렉션됩니다.

## 기본 홈 화면 {#default-home-screen}

기본적으로 홈 화면에는 연결된 축소판과 함께 시작 지점 및 작업(연결된 서버가 AEM Forms Workflow가 활성화된 경우)을 포함한 모든 양식이 표시됩니다. AEM Forms 서버에서 축소판을 지정할 수 있습니다.

다음 그림은 기본 홈 화면에서 기본 구성 요소에 대한 설명으로 주석을 달 수 있습니다.

![Forms 앱 홈 화면](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **메뉴 단추**:메뉴  **** 단추를 눌러 작업, Forms, 보낼 편지함 및 설정으로 이동합니다. AEM Forms 앱이 AEM Forms JEE 서버에 연결되어 있으면 작업 옵션을 볼 수 있습니다. 작업 옵션은 프로세스에서 생성된 초안을 프로세스에 저장합니다. AEM Forms OSGi 서버의 경우 작업 옵션이 숨겨집니다. 보낼 편지함은 저장된 양식과 초안을 서버와 동기화하기 전에 저장합니다. 앱이 서버](../../forms/using/sync-app.md)과 동기화된 [인 경우 보낼 편지함에 저장된 모든 양식과 초안이 AEM Forms 서버에 업로드됩니다. 설정에 대한 자세한 내용은 [일반 설정 업데이트](../../forms/using/update-general-settings.md)를 참조하십시오.
1. **작업 또는 양식**:작업할 나열된 작업 또는 양식을 누릅니다.
1. **수평 줄임표**:양식에서 작업을 사용할 수 있음을 나타냅니다. 줄임표를 누르면 작성자가 제공한 작업 및 설명이 표시됩니다. 줄임표를 탭하면 **초안 삭제** 및 **완료** 옵션이 표시됩니다.
1. **새로 고침 아이콘**:새로 고침 아이콘을 눌러 앱을 AEM Forms 서버와 동기화합니다.

### 홈 화면 사용자 지정 {#customizing-the-home-screen}

![일반 설정](assets/gen-settings.png)

앱의 **[일반 설정](../../forms/using/update-general-settings.md)** 또는 HTML 작업 영역의 **기본 설정** 탭에서 앱의 기본 홈 화면을 변경할 수 있습니다.

앱의 [홈] 화면 설정에 대한 변경 사항은 현재 로그인한 사용자 또는 현재 모바일 장치의 사용자에 대한 [홈] 화면에 영향을 줍니다.

그러나 HTML Workspace의 변경 사항은 AEM Forms 서버에 로그온한 모든 AEM Forms 앱 사용자에게 영향을 줍니다.
