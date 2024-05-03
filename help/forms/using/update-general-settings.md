---
title: 일반 설정 업데이트 중
description: 홈 화면과 같은 AEM Forms 앱 설정을 업데이트하고 시작 지점 및 첨부 파일 옵션 가져오기
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# 일반 설정 업데이트 중{#updating-general-settings}

AEM Forms 앱의 일반 설정을 사용하면 첨부 파일 가져오기, 오프라인 모드, 랜딩 화면, 기본 범주 및 자동 저장 빈도 등의 설정을 지정할 수 있습니다.

## 앱에서 일반 설정 업데이트 {#working-with-the-form}

앱을 AEM Forms 서버와 동기화하면 모든 양식 및 정의된 작업이 모바일 장치에 다운로드됩니다.

기본 AEM Forms 앱 솔루션은 앱이 동기화될 때 각 양식과 연결된 첨부 파일을 다운로드하지 않습니다.

일반 탭에서 첨부 파일 다운로드, 오프라인 모드, 랜딩 화면, 자동 저장 및 동기화 설정을 변경합니다. 다음을 변경할 수 있습니다. [홈 화면](../../forms/using/home-screen.md) 앱에서 사용할 수 있습니다.

**설정 화면에서 일반 탭으로 이동합니다.**

1. 설정 화면으로 이동하려면 홈 화면의 왼쪽 상단에 있는 메뉴 버튼을 선택한 다음 선택 을 클릭합니다 **설정**.
1. 설정 화면에서 일반 탭을 선택합니다.

   ![AEM Forms 앱의 일반 설정](assets/gen-settings-1.png)

   일반 설정 화면

   >[!NOTE]
   >
   >옵션은 서로 다른 모바일 장치에서 다르게 표시될 수 있습니다.

### 일반 설정 {#general-settings}

앱 설정을 다음과 같이 변경할 수 있습니다.

* **작업 첨부 파일 가져오기**: 각 작업이 앱에 다운로드될 때 연결된 첨부 파일을 다운로드할지 여부를 지정합니다.
* **오프라인 모드**: AEM Forms 앱에 대한 오프라인 서비스를 활성화하거나 비활성화합니다. 다음을 참조하십시오 [오프라인 모드에서 작업](/help/forms/using/work-offline-mode.md) 을 참조하십시오.
* **랜딩 화면**: 시작 위치([홈 화면](../../forms/using/home-screen.md))을 참조하십시오.
사용 가능한 옵션:

   * Forms
   * 작업
   * 즐겨찾기

* **기본 범주**: 홈 화면에 표시할 양식 범주를 선택할 수 있습니다. 모두 를 선택하면 홈 화면에 모든 양식을 볼 수 있습니다. 카테고리는 앱에 로드된 양식을 기반으로 채워집니다. Forms은 AEM Forms 서버에 지정된 양식 설정에 따라 앱에서 사용할 수 있습니다.

* **자동 저장 빈도**: 다음에 대한 빈도를 설정합니다. [모바일 앱에서 양식 데이터 저장](../../forms/using/autosave-data-app.md) 로컬로.
* **동기화 빈도**: 다음에 대한 빈도를 설정합니다. [모바일 앱이 동기화됨](../../forms/using/sync-app.md) 온라인 모드로 AEM Forms 서버 사용.
  **로컬 데이터 지우기**: 장치에서 모든 사용자 및 파일 저장소에 대한 설정 및 로컬 데이터를 포함하여 데이터베이스를 지웁니다.

>[!NOTE]
>
>캐시를 지우면 앱에서 즉시 로그아웃됩니다.
>
>그러나 캐시 지우기 작업을 확인하는 메시지가 표시됩니다.
