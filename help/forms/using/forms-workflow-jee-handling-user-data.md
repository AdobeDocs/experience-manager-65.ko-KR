---
title: Forms JEE 워크플로우 | 사용자 데이터 처리
seo-title: Forms JEE 워크플로우 | 사용자 데이터 처리
description: Forms JEE 워크플로우 | 사용자 데이터 처리
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
role: Administrator
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---

# Forms JEE 워크플로우 | 사용자 데이터 처리 {#forms-jee-workflows-handling-user-data}

AEM Forms JEE 워크플로우는 비즈니스 프로세스를 디자인, 만들기 및 관리하는 도구를 제공합니다. 워크플로우 프로세스는 지정된 순서로 실행되는 일련의 단계로 구성됩니다. 각 단계에서는 사용자에게 작업을 할당하거나 이메일 메시지를 보내는 등의 특정 작업을 수행합니다. 프로세스는 자산, 사용자 계정 및 서비스와 상호 작용할 수 있으며, 다음 방법 중 하나를 사용하여 트리거할 수 있습니다.

* AEM Forms Workspace에서 프로세스 시작
* SOAP 또는 RESTful 서비스 사용
* 적응형 양식 제출
* 감시 폴더 사용
* 이메일 사용

AEM Forms JEE 워크플로우 프로세스 만들기에 대한 자세한 내용은 [Workbench 도움말](http://www.adobe.com/go/learn_aemforms_workbench_65)을 참조하십시오.

## 사용자 데이터 및 데이터 저장소 {#user-data-and-data-stores}

프로세스가 트리거되고 진행되면 프로세스 참여자에 대한 데이터, 프로세스와 연관된 양식의 참여자가 입력한 데이터 및 양식에 추가된 첨부 파일을 캡처합니다. 데이터는 AEM Forms JEE 서버 데이터베이스에 저장되며, 구성된 경우 첨부 파일과 같은 일부 데이터는 GDS(Global Document Storage) 디렉토리에 저장됩니다. GDS 디렉토리는 공유 파일 시스템 또는 데이터베이스에 구성할 수 있습니다.

## 사용자 데이터 {#access-and-delete-user-data} 액세스 및 삭제

프로세스가 트리거되면 고유한 프로세스 인스턴스 ID 및 긴 기간 호출 ID가 생성되어 프로세스 인스턴스와 연결됩니다. 긴 기간 동안의 호출 ID를 기반으로 프로세스 인스턴스에 대한 데이터에 액세스하고 삭제할 수 있습니다. 프로세스 개시자의 사용자 이름 또는 작업을 제출한 프로세스 참여자의 사용자 이름으로 프로세스 인스턴스의 장기 방문 ID를 줄일 수 있습니다.

그러나 다음 시나리오에서는 이니시에이터에 대한 프로세스 인스턴스 ID를 식별할 수 없습니다.

* **감시 폴더를 통해 트리거된 프로세스**:감시 폴더에 의해 프로세스가 트리거되는 경우 해당 이니시에이터를 사용하여 프로세스 인스턴스를 식별할 수 없습니다. 이 경우, 사용자 정보는 저장된 데이터로 인코딩됩니다.
* **게시 AEM 인스턴스에서 시작된 프로세스**:AEM 게시 인스턴스에서 트리거된 모든 프로세스 인스턴스는 초기자에 대한 정보를 캡처하지 않습니다. 하지만 사용자 데이터는 워크플로우 변수에 저장된 프로세스와 연결된 양식으로 캡처될 수 있습니다.
* **이메일을 통해 시작된 프로세스**:보낸 사람의 전자 메일 ID는 직접 쿼리할 수 없는  `tb_job_instance` 데이터베이스 테이블의 불투명한 blob 열에 속성으로 캡처됩니다.

### 워크플로우 개시자 또는 참여자가 {#initiator-participant}인 경우 프로세스 인스턴스 ID 식별

워크플로우 개시자 또는 참여자에 대한 프로세스 인스턴스 ID를 식별하려면 다음 단계를 수행하십시오.

1. AEM Forms 서버 데이터베이스에서 다음 명령을 실행하여 `edcprincipalentity` 데이터베이스 테이블에서 워크플로우 개시자 또는 참여자에 대한 주체 ID를 검색합니다.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   쿼리는 지정된 `user_ID`에 대한 주체 ID를 반환합니다.

1. (**워크플로우 개시자의 경우**) 다음 명령을 실행하여 `tb_task` 데이터베이스 테이블에서 개시자의 주 ID와 연관된 모든 작업을 검색합니다.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   쿼리는 지정된 `initiator`_ `principal_id`에 의해 시작된 작업을 반환합니다. 작업은 두 가지 유형으로 구성됩니다.

   * **완료된 작업**:이러한 작업이 제출되어 필드에 영숫자 값을  `process_instance_id` 표시합니다. 제출된 작업에 대한 모든 프로세스 인스턴스 ID를 기록하고 단계를 계속합니다.
   * **시작되었지만 완료되지 않은 작업**:이러한 작업은 시작되었지만 아직 제출되지 않았습니다. 이러한 작업에 대한 `process_instance_id` 필드의 값은 **0**(영)입니다. 이 경우 해당 작업 ID를 기록하고 [고아 작업](#orphan)을 참조하십시오.

1. (**워크플로우 참여자의 경우**) 다음 명령을 실행하여 `tb_assignment` 데이터베이스 테이블에서 개시자에 대한 프로세스 참여자의 주 ID와 연관된 프로세스 인스턴스 ID를 검색합니다.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   질의는 참여자가 작업을 제출하지 않은 프로세스를 포함하여 참여자와 연관된 모든 프로세스에 대한 인스턴스 ID를 반환합니다.

   제출된 작업에 대한 모든 프로세스 인스턴스 ID를 기록하고 단계를 계속합니다.

   `process_instance_id`이 0(영)인 고아 작업 또는 작업의 경우 해당 작업 ID를 기록하고 [고아 작업](#orphan)을 참조하십시오.

1. 식별된 프로세스 인스턴스 ID에 대한 사용자 데이터를 삭제하려면 [프로세스 인스턴스 ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 섹션의 지침에 따라 워크플로우 인스턴스에서 사용자 데이터를 삭제합니다.

### 사용자 데이터가 기본 변수에 저장될 때 프로세스 인스턴스 ID를 식별합니다 {#primitive}

워크플로우는 사용자 데이터가 데이터베이스의 blob으로 저장되는 변수에 캡처되도록 디자인할 수 있습니다. 이러한 경우 사용자 데이터가 다음 기본 유형 변수 중 하나에 저장된 경우에만 쿼리할 수 있습니다.

* **문자열**:사용자 ID를 직접 또는 하위 문자열로 포함하며 SQL을 사용하여 쿼리할 수 있습니다.
* **숫자**:사용자 ID를 직접 포함합니다.
* **XML**:사용자 ID를 데이터베이스에 텍스트 열로 저장된 텍스트 내에 하위 문자열로 포함하므로 문자처럼 쿼리할 수 있습니다.

다음 단계를 수행하여 데이터를 기본 유형 변수에 저장하는 워크플로우에 사용자의 데이터가 포함되어 있는지 확인합니다.

1. 다음 데이터베이스 명령을 실행합니다.

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   쿼리는 지정된 응용 프로그램( `app_name`)과 워크플로( `workflow_name`)에 대해 `tb_<number>` 형식으로 테이블 이름을 반환합니다.

   >[!NOTE]
   >
   >워크플로우가 애플리케이션 내의 하위 폴더 내에 중첩된 경우 `name` 속성 값이 복잡할 수 있습니다. 워크플로우에 대한 정확한 전체 경로를 지정합니다. 이 경로는 `omd_object_type` 데이터베이스 테이블에서 얻을 수 있습니다.

1. `tb_<number>` 테이블 스키마를 검토합니다. 표에는 지정된 워크플로우의 사용자 데이터를 저장하는 변수가 포함되어 있습니다. 테이블의 변수는 워크플로우의 변수에 해당합니다.

   사용자 ID를 포함하는 워크플로우 변수에 해당하는 변수를 식별하고 확인합니다. 식별된 변수가 기본 유형인 경우 쿼리를 실행하여 사용자 ID와 연결된 워크플로우 인스턴스를 결정할 수 있습니다.

1. 다음 데이터베이스 명령을 실행합니다. 이 명령에서 `user_var`은 사용자 ID를 포함하는 기본 유형 변수입니다.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   쿼리는 지정된 `user_ID`에 연결된 모든 프로세스 인스턴스 ID를 반환합니다.

1. 식별된 프로세스 인스턴스 ID에 대한 사용자 데이터를 삭제하려면 [프로세스 인스턴스 ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) 섹션의 지침에 따라 워크플로우 인스턴스에서 사용자 데이터를 삭제합니다.

### 프로세스 인스턴스 ID를 기반으로 워크플로우 인스턴스에서 사용자 데이터 제거 {#purge}

사용자와 연결된 프로세스 인스턴스 ID를 식별했으므로 각 프로세스 인스턴스에서 사용자 데이터를 삭제하려면 다음을 수행합니다.

1. 다음 명령을 실행하여 `tb_process_instance` 테이블에서 프로세스 인스턴스에 대한 오래 지속되는 호출 ID 및 상태를 검색합니다.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   쿼리는 지정된 `process_instance_id`에 대한 오래 지속된 호출 ID 및 상태를 반환합니다.

1. 올바른 연결 설정으로 `ServiceClientFactory` 인스턴스를 사용하여 공용 `ProcessManager` 클라이언트( `com.adobe.idp.workflow.client.ProcessManager`)의 인스턴스를 만듭니다.

   자세한 내용은 [Class ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html)에 대한 Java API 참조를 참조하십시오.

1. 워크플로우 인스턴스의 상태를 확인합니다. 상태가 2(완료) 또는 4(종료됨) 이외의 경우에는 다음 메서드를 호출하여 인스턴스를 먼저 종료합니다.

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. 다음 메서드를 호출하여 워크플로우 인스턴스를 삭제합니다.

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   `purgeProcessInstance` 메서드는 구성된 경우 AEM Forms 서버 데이터베이스 및 GDS에서 지정된 호출 ID에 대한 모든 데이터를 완전히 삭제합니다.

### 고아 작업 {#orphan}

Orphan 작업은 포함 프로세스가 시작되었지만 아직 제출되지 않은 작업입니다. 이 경우 `process_instance_id`은 **0**(영)입니다. 따라서 프로세스 인스턴스 ID를 사용하여 고아 작업에 대해 저장된 사용자 데이터는 추적할 수 없습니다. 그러나 고아 작업에 대한 작업 ID를 사용하여 추적할 수 있습니다. [워크플로우 개시자나 참가자가 알려진 경우 프로세스 인스턴스 ID 식별에 설명된 대로 사용자의 `tb_task` 테이블에서 작업 ID를 식별할 수 있습니다](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

작업 ID가 있으면 다음을 수행하여 GDS 및 데이터베이스의 고아 태스크로 연결된 파일 및 데이터를 제거합니다.

1. AEM Forms 서버 데이터베이스에서 다음 명령을 실행하여 식별된 작업 ID에 대한 ID를 검색합니다.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   쿼리는 ID 목록을 반환합니다. 결과에 반환되는 각 ID( `fd_id`)에 대해 다음과 같이 세션 ID 문자열 목록을 만듭니다.

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. GDS가 파일 시스템을 가리키는지 아니면 데이터베이스를 가리키는지에 따라 다음 단계 중 하나를 수행합니다.

   1. **파일 시스템의 GDS**

      GDS 파일 시스템에서 다음을 수행합니다.

      1. 다음 세션 ID 문자열이 있는 파일을 해당 확장자로 검색합니다.
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      이러한 확장자가 인 파일은 마커 파일입니다. 파일 이름과 함께 다음 형식으로 저장됩니다.

      `<file_name_guid>.session<session_id_string>`

      1. 파일 시스템에서 정확한 파일 이름이 `<file_name_guid>`인 모든 마커 파일 및 기타 파일을 삭제합니다.
   1. **데이터베이스의 GDS**

      각 세션 ID에 대해 다음 명령을 실행합니다.

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. 다음 명령을 실행하여 AEM Forms 서버 데이터베이스에서 작업 ID에 대한 데이터를 삭제합니다.

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
