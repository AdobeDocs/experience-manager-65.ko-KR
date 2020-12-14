---
title: 일반 설정 업데이트
seo-title: 일반 설정 업데이트
description: 홈 화면과 같은 AEM Forms 앱 설정을 업데이트하고 시작 지점 및 첨부 파일 가져오기 옵션
seo-description: 홈 화면과 같은 AEM Forms 앱 설정을 업데이트하고 시작 지점 및 첨부 파일 가져오기 옵션
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 1%

---


# 일반 설정 업데이트 중{#updating-general-settings}

AEM Forms 앱의 일반 설정을 사용하면 첨부 파일 가져오기, 오프라인 모드, 랜딩 화면, 기본 카테고리, 자동 저장 빈도 등의 설정을 지정할 수 있습니다.

## 앱 {#working-with-the-form}의 일반 설정 업데이트

앱을 AEM Forms 서버와 동기화하면 모든 양식 및 정의된 작업이 모바일 장치에 다운로드됩니다.

기본 AEM Forms 앱 솔루션은 앱이 동기화될 때 각 양식과 연결된 첨부 파일을 다운로드하지 않습니다.

일반 탭에서 다운로드 첨부 파일, 오프라인 모드, 랜딩 화면, 자동 저장 및 동기화 설정을 변경합니다. 앱의 [홈 화면](../../forms/using/home-screen.md)을 변경할 수 있습니다.

**설정 화면의 일반 탭으로 이동**

1. 설정 화면으로 이동하려면 홈 화면의 왼쪽 위 모서리에 있는 메뉴 단추를 누른 다음 **설정**&#x200B;을 탭합니다.
1. 설정 화면에서 일반 탭을 누릅니다.

   ![AEM Forms 앱의 일반 설정](assets/gen-settings-1.png)

   일반 설정 화면

   >[!NOTE]
   >
   >옵션은 다른 모바일 장치에서 다르게 표시될 수 있습니다.

### 일반 설정 {#general-settings}

앱 설정을 다음과 같이 변경할 수 있습니다.

* **작업 첨부 파일 가져오기**:각 작업을 앱에 다운로드할 때 관련 첨부 파일을 다운로드할지 여부를 지정하려면
* **오프라인 모드**:AEM Forms 앱에 대한 오프라인 서비스를 활성화하거나 비활성화하려면 자세한 내용은 [오프라인 모드에서 작업](/help/forms/using/work-offline-mode.md)을 참조하십시오.
* **랜딩 화면**:앱의 시작 위치([홈 화면](../../forms/using/home-screen.md))를 설정하려면
사용 가능한 옵션:

   * 양식
   * 작업
   * 즐겨찾기

* **기본 카테고리**:홈 화면에 표시할 양식 범주를 선택할 수 있습니다. 모두를 선택하면 홈 화면에서 모든 양식을 볼 수 있습니다. 카테고리는 앱에 로드된 양식을 기반으로 채워집니다. Forms은 AEM Forms 서버에 지정된 양식 설정을 기반으로 앱에서 사용할 수 있습니다.

* **자동 저장 주기**:모바일 앱에서 양식을 데이터 [로 저장하는 빈도를 ](../../forms/using/autosave-data-app.md) 설정합니다.
* **동기화 빈도**:온라인 모드에서  [모바일 앱이 AEM Forms ](../../forms/using/sync-app.md) 서버와 동기화되는 빈도를 설정하려면
   **로컬 데이터 지우기**:모든 사용자의 설정 및 로컬 데이터, 장치의 파일 저장소 등 데이터베이스를 지웁니다.

>[!NOTE]
>
>캐시를 지우면 앱에서 즉시 로그아웃됩니다.
>
>그러나 캐시 지우기 작업을 확인하는 메시지가 표시됩니다.
