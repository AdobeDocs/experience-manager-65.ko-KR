---
title: 동기화 스케줄러 구성
seo-title: Configuring the synchronization scheduler
description: 에셋을 마이그레이션하고 동기화하고, 동기화 스케줄러를 구성하고, 폴더를 사용하여 에셋을 정렬하는 방법을 알아봅니다.
seo-description: Learn how to migrate and sync assets, configure sync scheduler, and use folders to arrange assets.
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# 동기화 스케줄러 구성 {#configuring-the-synchronization-scheduler}

기본적으로 동기화 스케줄러는 3분마다 실행되어 LiveCycle Workbench 11을 통해 저장소에서 수정 및 업데이트된 모든 에셋을 동기화합니다. 양식 및 리소스가 포함된 애플리케이션은 동기화 프로세스가 완료되면 AEM Forms 사용자 인터페이스에 표시됩니다.

## 동기화 스케줄러의 간격 변경 {#change-interval-of-the-synchronization-scheduler}

동기화 스케줄러의 간격을 변경하려면 다음 단계를 수행하십시오.

1. AEM 구성 관리자에 로그인합니다. 구성 관리자의 URL은 다음과 같습니다. `https://'[server]:[port]'/lc/system/console/configMgr`

1. 을(를) 찾아 엽니다. **FormsManager 구성** 번들.

1. 다음에 대한 새 값 지정 **동기화 스케줄러 빈도** 옵션을 선택합니다.

   빈도의 단위는 분입니다. 예를 들어 60분마다 실행되도록 스케줄러를 구성하려면 60을 지정합니다.

## 자산 동기화 {#synchronizing-assets}

다음을 사용할 수 있습니다. **저장소에서 자산 동기화** 자산을 수동으로 동기화하는 옵션입니다. 자산을 수동으로 동기화하려면 다음 단계를 수행하십시오.

1. AEM Forms에 로그인. 기본 URL은 `https://'[server]:[port]'/lc/aem/forms/`.

   ![AEM Forms 사용자 인터페이스](assets/aem_forms_ui.png)

   **그림:** *AEM Forms 사용자 인터페이스*

1. 다음을 클릭합니다. ![aem6forms_sync](assets/aem6forms_sync.png) 아이콘을 클릭합니다. 마지막으로 구성된 경로에 에셋이 없는 경우 아래와 같이 대화 상자를 엽니다. 클릭 **시작** 동기화를 시작합니다.

   ![동기화 대화 상자](assets/migrate-and-syncronize.png)

   **그림:** *동기화 대화 상자*

## 동기화 문제 해결 오류 {#troubleshooting-synchronization-error}

워크플로우 디자이너(LiveCycle 워크벤치)에서 새 응용 프로그램을 만들 수 있습니다.

새로 만든 응용 프로그램과 /content/dam/formsanddocuments에 있는 폴더의 이름이 동일한 경우 &quot; 오류가 발생합니다.*이 응용 프로그램과 이름이 같은 자산이 루트 수준에 이미 있습니다.*&quot;로그인되어 있습니다.

충돌을 해결하려면 애플리케이션 이름을 바꾸고 자산을 수동으로 동기화합니다.

![자산 동기화 대화 상자에서 충돌 발생](assets/sync-conflict.png)

**그림:** *자산 동기화 대화 상자에서 충돌 발생*
