---
title: 'DB2&reg; 데이터베이스: 매주 프로세스 실행'
description: AEM Forms DB2&reg; 데이터베이스의 성능을 향상하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '148'
ht-degree: 100%

---

# DB2® 데이터베이스: 매주 프로세스 실행{#db-database-running-a-process-weekly}

AEM Forms DB2® 데이터베이스의 실행 속도가 느려지기 시작하는 경우 다음 프로세스를 매주 실행하면 성능이 향상될 수 있습니다.

1. DB2® Control Center를 시작합니다.

   (Windows) 시작 > 프로그램 > IBM® DB2® > 일반 관리 도구 > Control Center를 선택합니다.

   (Linux® 및 UNIX®) 명령 프롬프트에서 `db2jcc` 명령을 입력합니다.

1. DB2® Control Center 오브젝트 트리에서 모든 데이터베이스를 클릭합니다.
1. AEM Forms에 대해 만든 데이터베이스를 클릭하고 테이블 폴더를 클릭합니다.
1. 콘텐츠 창에서 모든 데이터베이스 테이블을 선택하고 마우스 오른쪽 버튼을 클릭한 후 통계 실행을 선택합니다.
1. 통계 > 색인 통계로 이동합니다.
1. 모든 색인에 대한 통계 수집을 선택하고 확장된 상세 통계가 포함된 색인에 대한 통계 수집을 선택한 후 확인을 클릭합니다.

프로세스가 완료되면 메시지가 나타납니다. 메시지를 닫습니다.
