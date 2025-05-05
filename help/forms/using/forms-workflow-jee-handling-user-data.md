---
title: Forms JEE 워크플로 | 사용자 데이터 처리
description: AEM Forms JEE 워크플로우를 사용하여 비즈니스 프로세스를 디자인, 생성 및 관리하는 방법을 알아봅니다.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Forms JEE 워크플로 | 사용자 데이터 처리 {#forms-jee-workflows-handling-user-data}

AEM Forms JEE 워크플로우는 비즈니스 프로세스를 디자인, 생성 및 관리하는 도구를 제공합니다. 워크플로 프로세스는 지정된 순서로 실행되는 일련의 단계로 구성됩니다. 각 단계는 사용자에게 작업을 할당하거나 이메일 메시지를 보내는 등의 특정 작업을 수행합니다. 프로세스는 자산, 사용자 계정 및 서비스와 상호 작용할 수 있으며, 다음 방법 중 하나를 사용하여 트리거할 수 있습니다.

* AEM Forms Workspace에서 프로세스 시작
* SOAP 또는 RESTful 서비스 사용
* 적응형 양식 제출
* 감시 폴더 사용
* 이메일 사용

AEM Forms JEE 워크플로우 프로세스 만들기에 대한 자세한 내용은 [Workbench 도움말](https://www.adobe.com/go/learn_aemforms_workbench_65_kr)을 참조하십시오.

## 사용자 데이터 및 데이터 저장소 {#user-data-and-data-stores}

프로세스가 트리거되고 진행됨에 따라 프로세스 참여자에 대한 데이터, 프로세스와 연결된 양식의 참여자가 입력한 데이터 및 양식에 추가된 첨부 파일을 캡처합니다. 데이터는 AEM Forms JEE 서버 데이터베이스에 저장되고 구성된 경우 첨부 파일과 같은 일부 데이터가 GDS(Global Document Storage) 디렉토리에 저장됩니다. GDS 디렉토리는 공유 파일 시스템 또는 데이터베이스에 구성할 수 있습니다.

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

프로세스가 트리거되면 고유한 프로세스 인스턴스 ID 및 장기 호출 ID가 생성되고 프로세스 인스턴스와 연결됩니다. 장기 호출 ID를 기반으로 프로세스 인스턴스의 데이터에 액세스하고 삭제할 수 있습니다. 작업을 제출한 프로세스 개시자 또는 프로세스 참여자의 사용자 이름으로 프로세스 인스턴스의 장기 호출 ID를 추론할 수 있습니다.

하지만 다음과 같은 경우에는 이니시에이터의 프로세스 인스턴스 ID를 식별할 수 없습니다.

* **감시 폴더를 통해 트리거된 프로세스**: 감시 폴더에 의해 프로세스가 트리거된 경우 프로세스 인스턴스를 해당 초기자를 사용하여 식별할 수 없습니다. 이 때, 사용자 정보는 저장된 데이터에 부호화된다.
* **게시 AEM 인스턴스에서 시작된 프로세스**: AEM 게시 인스턴스에서 트리거된 모든 프로세스 인스턴스가 초기자에 대한 정보를 캡처하지 않습니다. 그러나 사용자 데이터는 프로세스와 연결된 양식으로 캡처되어 워크플로우 변수에 저장될 수 있습니다.
* **전자 메일을 통해 시작된 프로세스**: 보낸 사람의 전자 메일 ID는 직접 쿼리할 수 없는 `tb_job_instance` 데이터베이스 테이블의 불투명 blob 열에 속성으로 캡처됩니다.

### 워크플로우 개시자 또는 참가자를 알 경우 프로세스 인스턴스 ID 식별 {#initiator-participant}

워크플로우 개시자 또는 참가자의 프로세스 인스턴스 ID를 식별할 수 있도록 다음 단계를 수행합니다.

1. AEM Forms 서버 데이터베이스에서 다음 명령을 실행하여 `edcprincipalentity` 데이터베이스 테이블에서 워크플로 개시자 또는 참가자의 주체 ID를 검색합니다.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   쿼리가 지정된 `user_ID`에 대한 주체 ID를 반환합니다.

1. (**워크플로 개시자의 경우**) 다음 명령을 실행하여 `tb_task` 데이터베이스 테이블에서 개시자의 주체 ID와 연결된 모든 작업을 검색합니다.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   쿼리가 지정된 `initiator`_ `principal_id`에 의해 시작된 작업을 반환합니다. 작업은 두 가지 유형으로 구성됩니다.

   * **완료된 작업**: 이러한 작업이 제출되었으며 `process_instance_id` 필드에 영숫자 값이 표시됩니다. 제출된 작업에 대한 모든 프로세스 인스턴스 ID를 기록하고 단계를 계속합니다.
   * **작업이 시작되었지만 완료되지 않음**: 이러한 작업이 시작되었지만 아직 제출되지 않았습니다. 이 작업의 `process_instance_id` 필드 값은 **0**(영)입니다. 이 경우 해당 작업 ID를 기록하고 [고아 작업](#orphan)을(를) 참조하십시오.

1. (**워크플로 참가자의 경우**) 다음 명령을 실행하여 `tb_assignment` 데이터베이스 테이블에서 초기자에 대한 프로세스 참가자의 주체 ID와 연결된 프로세스 인스턴스 ID를 검색합니다.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   쿼리는 참가자가 작업을 제출하지 않은 프로세스를 포함하여 참가자와 연결된 모든 프로세스에 대한 인스턴스 ID를 반환합니다.

   제출된 작업에 대한 모든 프로세스 인스턴스 ID를 기록하고 단계를 계속합니다.

   `process_instance_id`이(가) 0인 고아 작업 또는 작업의 경우 해당 작업 ID를 기록하고 [고아 작업](#orphan)을(를) 참조하십시오.

1. 식별된 프로세스 인스턴스 ID에 대한 사용자 데이터를 삭제할 수 있도록 [프로세스 인스턴스 ID를 기반으로 워크플로우 인스턴스에서 사용자 데이터 제거](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 섹션의 지침을 따릅니다.

### 사용자 데이터가 기본 변수에 저장되는 경우 프로세스 인스턴스 ID를 식별합니다 {#primitive}

사용자 데이터가 데이터베이스에 Blob으로 저장되는 변수에 캡처되도록 워크플로우를 디자인할 수 있습니다. 이러한 경우 사용자 데이터가 다음 기본 유형 변수 중 하나에 저장된 경우에만 쿼리할 수 있습니다.

* **문자열**: 사용자 ID를 직접 또는 하위 문자열로 포함하며 SQL을 사용하여 쿼리할 수 있습니다.
* **숫자**: 사용자 ID를 직접 포함합니다.
* **XML**: 사용자 ID를 데이터베이스에 텍스트 열로 저장된 텍스트 내에 하위 문자열로 포함하고 문자열로 쿼리할 수 있습니다.

원시 유형 변수에 데이터를 저장하는 워크플로우에 사용자에 대한 데이터가 포함되어 있는지 확인할 수 있도록 다음 단계를 수행합니다.

1. 다음 데이터베이스 명령을 실행합니다.

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   쿼리에서 지정한 응용 프로그램(`app_name`) 및 워크플로(`workflow_name`)에 대해 `tb_<number>` 형식의 테이블 이름을 반환합니다.

   >[!NOTE]
   >
   >응용 프로그램 내의 하위 폴더에 워크플로가 중첩되어 있으면 `name` 속성의 값이 복잡할 수 있습니다. `omd_object_type` 데이터베이스 테이블에서 가져올 수 있는 워크플로의 정확한 전체 경로를 지정해야 합니다.

1. `tb_<number>` 테이블 스키마를 검토합니다. 이 표에는 지정된 워크플로우에 대한 사용자 데이터를 저장하는 변수가 포함되어 있습니다. 표의 변수는 워크플로우의 변수에 해당합니다.

   사용자 ID가 포함된 워크플로 변수에 해당하는 변수를 식별하고 기록해 두십시오. 식별된 변수가 기본 유형인 경우 쿼리를 실행하여 사용자 ID와 연결된 워크플로 인스턴스를 확인할 수 있습니다.

1. 다음 데이터베이스 명령을 실행합니다. 이 명령에서 `user_var`은(는) 사용자 ID를 포함하는 기본 형식 변수입니다.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   쿼리가 지정된 `user_ID`과(와) 연결된 모든 프로세스 인스턴스 ID를 반환합니다.

1. 식별된 프로세스 인스턴스 ID에 대한 사용자 데이터를 삭제할 수 있도록 [프로세스 인스턴스 ID를 기반으로 워크플로우 인스턴스에서 사용자 데이터 제거](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 섹션의 지침을 따릅니다.

### 프로세스 인스턴스 ID를 기반으로 워크플로우 인스턴스에서 사용자 데이터 제거 {#purge}

사용자와 연결된 프로세스 인스턴스 ID를 식별했으므로 다음을 수행하여 각 프로세스 인스턴스에서 사용자 데이터를 삭제합니다.

1. `tb_process_instance` 테이블에서 프로세스 인스턴스의 장기 호출 ID 및 상태를 검색할 수 있도록 다음 명령을 실행합니다.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   쿼리가 지정된 `process_instance_id`에 대한 장기 호출 ID 및 상태를 반환합니다.

1. 올바른 연결 설정이 있는 `ServiceClientFactory` 인스턴스를 사용하여 공용 `ProcessManager` 클라이언트(`com.adobe.idp.workflow.client.ProcessManager`)의 인스턴스를 만듭니다.

   자세한 내용은 [Class ProcessManager](https://helpx.adobe.com/kr/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html)에 대한 Java™ API 참조를 참조하십시오.

1. 워크플로 인스턴스의 상태를 확인합니다. 상태가 2(COMPLETE) 또는 4(TERMINATED)가 아니면 다음 메서드를 호출하여 먼저 인스턴스를 종료합니다.

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`

1. 다음 메서드를 호출하여 워크플로 인스턴스를 제거합니다.

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   `purgeProcessInstance` 메서드는 구성된 경우 AEM Forms 서버 데이터베이스 및 GDS에서 지정된 호출 ID에 대한 모든 데이터를 완전히 삭제합니다.

### 고아 작업 {#orphan}

고아 작업은 포함 프로세스가 시작되었지만 아직 제출되지 않은 작업입니다. 이 경우 `process_instance_id`은(는) **0**(영)입니다. 따라서 프로세스 인스턴스 ID를 사용하여 고립 작업에 대해 저장된 사용자 데이터를 추적할 수 없습니다. 그러나 고아 작업의 작업 ID를 사용하여 추적할 수 있습니다. [워크플로 개시자 또는 참가자를 알 때 프로세스 인스턴스 ID 식별](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant)에 설명된 대로 사용자에 대한 `tb_task` 테이블에서 작업 ID를 식별할 수 있습니다.

작업 ID가 있는 경우 다음을 수행하여 GDS 및 데이터베이스에서 고립 작업이 있는 관련 파일 및 데이터를 제거합니다.

1. 식별된 작업 ID에 대한 ID를 검색할 수 있도록 AEM Forms 서버 데이터베이스에서 다음 명령을 실행합니다.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   쿼리가 ID 목록을 반환합니다. 결과에 반환된 각 ID(`fd_id`)에 대해 다음과 같이 세션 ID 문자열 목록을 만듭니다.

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. GDS가 파일 시스템을 가리키는지 아니면 데이터베이스를 가리키는지에 따라 다음 단계 중 하나를 수행합니다.

   1. 파일 시스템의 **GDS**

      GDS 파일 시스템에서:

      1. 다음 세션 ID 문자열이 확장명인 파일을 검색합니다.

      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      이러한 확장자를 가진 파일이 마커 파일입니다. 파일 이름은 다음과 같은 형식으로 저장됩니다.

      `<file_name_guid>.session<session_id_string>`

      1. 파일 시스템에서 모든 마커 파일 및 `<file_name_guid>`과(와) 동일한 파일 이름을 가진 다른 파일을 삭제합니다.

   1. 데이터베이스의 **GDS**

      각 세션 ID에 대해 다음 명령을 실행합니다.

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```

1. AEM Forms 서버 데이터베이스에서 작업 ID에 대한 데이터를 삭제할 수 있도록 다음 명령을 실행합니다.

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
