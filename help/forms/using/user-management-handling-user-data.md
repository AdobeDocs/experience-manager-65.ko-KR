---
title: Forms 사용자 관리 | 사용자 데이터 처리
description: AEM Forms JEE 사용자 관리 구성 요소를 사용하여 AEM Forms에 액세스해야 하는 사용자를 만들고, 인증하고, 관리하는 방법을 알아봅니다.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Forms 사용자 관리 | 사용자 데이터 처리 {#forms-user-management-handling-user-data}

사용자 관리는 AEM Forms 사용자가 AEM Forms에 액세스할 수 있도록 생성, 관리 및 인증할 수 있는 AEM Forms JEE 구성 요소입니다. 사용자 관리는 사용자 정보를 얻기 위한 디렉터리로 도메인을 사용합니다. 지원되는 도메인 유형은 다음과 같습니다.

**로컬 도메인**: 이 유형의 도메인이 타사 스토리지 시스템에 연결되어 있지 않습니다. 대신 사용자 및 그룹이 로컬로 생성되고 사용자 관리 데이터베이스에 상주합니다. 암호는 로컬에 저장되고 인증은 로컬 데이터베이스를 사용하여 수행됩니다.

**하이브리드 도메인**: 이 유형의 도메인은 타사 스토리지 시스템에 연결되어 있지 않습니다. 대신 사용자 및 그룹이 로컬로 생성되고 사용자 관리 데이터베이스에 상주합니다. 로컬 도메인과 달리 하이브리드 도메인은 LDAP, Kerberos, SAML 또는 사용자 지정 인증 공급자인 외부 인증 공급자를 사용합니다.

**엔터프라이즈 도메인**: LDAP 디렉터리와 같은 타사 스토리지 시스템에 있는 사용자 및 그룹으로 구성됩니다. User Management에서 타사 스토리지 시스템에 쓰지 않습니다. 대신 사용자 관리는 사용자 및 그룹 정보를 사용자 관리 데이터베이스와 동기화합니다. 또한 엔터프라이즈 도메인은 LDAP, Kerberos, SAML 또는 사용자 지정 인증 공급자인 외부 인증 공급자를 사용합니다.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## 사용자 데이터 및 데이터 저장소 {#user-data-and-data-stores}

사용자 관리는 My Sql, Oracle, MS® SQL Server 및 IBM® DB2®와 같은 데이터베이스에 사용자 데이터를 저장합니다. 또한 `https://'[server]:[port]'lc`에 AEM 작성자의 Forms 애플리케이션에 한 번 이상 로그인한 사용자는 AEM 저장소에 생성됩니다. 따라서 사용자 관리는 다음 데이터 저장소에 저장됩니다.

* 데이터베이스
* AEM 저장소
* LDAP 디렉토리와 같은 타사 스토리지

>[!NOTE]
>
>타사 저장소에 저장된 데이터는 이 문서의 범위를 벗어납니다. 이러한 저장소에서 사용자 데이터를 관리하려면 서드파티 공급업체에 직접 문의하십시오.

### 데이터베이스 {#database}

사용자 관리는 다음 데이터베이스 테이블에 사용자 데이터를 저장합니다.

<table>
 <tbody>
  <tr>
   <td>데이터베이스 테이블</td>
   <td>설명</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>주체 엔티티에 대한 정보를 저장합니다. 주도자는 사용자, 그룹 또는 역할일 수 있습니다.</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>사용자의 PII(개인 식별 정보)를 저장합니다. 여기에는 로컬, 엔터프라이즈 및 하이브리드 도메인의 모든 사용자에 대한 항목이 포함됩니다.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Oracle 및 MS® SQL 데이터베이스)</p> </td>
   <td>로컬 사용자에 대한 데이터만 저장합니다.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(Oracle 및 MS® SQL 데이터베이스)</p> </td>
   <td>로컬, 엔터프라이즈 및 하이브리드 도메인의 모든 사용자 항목을 포함합니다. 여기에는 사용자 이메일 ID가 포함되어 있습니다.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code><br /> (Oracle 및 MS® SQL 데이터베이스)</p> </td>
   <td>사용자와 그룹 간의 매핑을 저장합니다.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>사용자와 그룹 모두에 대한 역할과 주체 간의 매핑을 저장합니다.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>사용자와 그룹 모두에 대한 사용자 및 권한 간의 매핑을 저장합니다.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code><br /> (Oracle 및 MS® SQL 데이터베이스)</p> </td>
   <td>주체에 해당하는 이전 및 새 특성 값을 저장합니다.<br /> </td>
  </tr>
 </tbody>
</table>

### AEM 저장소 {#aem-repository}

`https://'[server]:[port]'lc` 아래의 Forms 응용 프로그램에 한 번 이상 액세스한 사용자의 사용자 관리 데이터도 AEM 저장소에 저장됩니다.

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

사용자 관리 데이터베이스 및 AEM 저장소의 사용자에 대한 사용자 관리 데이터에 액세스하고 내보낼 수 있으며, 필요한 경우 영구적으로 삭제할 수 있습니다.

### 데이터베이스 {#database-1}

사용자 관리 데이터베이스에서 사용자 데이터를 내보내거나 삭제하려면 데이터베이스 클라이언트를 사용하여 데이터베이스에 연결하고 사용자의 일부 PII를 기반으로 주체 ID를 찾아야 합니다. 예를 들어 로그인 ID를 사용하여 사용자의 보안 주체 ID를 검색하려면 데이터베이스에서 다음 `select` 명령을 실행합니다.

`select` 명령에서 `<user_login_id>`을(를) 검색할 사용자 ID의 로그인 ID로 바꿉니다.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

주체 ID를 알게 되면 사용자 데이터를 내보내거나 삭제할 수 있습니다.

#### 사용자 데이터 내보내기 {#export-user-data}

데이터베이스 테이블에서 사용자 ID에 대한 사용자 관리 데이터를 내보낼 수 있도록 다음 데이터베이스 명령을 실행합니다. `select` 명령에서 `<principal_id>`을(를) 데이터를 내보내려는 사용자의 보안 주체 ID로 바꾸십시오.

>[!NOTE]
>
>다음 명령은 My SQL 및 IBM® DB2® 데이터베이스에서 데이터베이스 테이블 이름을 사용합니다. oracle 및 MS® SQL 데이터베이스에서 이러한 명령을 실행할 때 명령에서 다음 테이블 이름을 바꿉니다.
>
>* `EdcPrincipalLocalAccountEntity`을(를) `EdcPrincipalLocalAccount`(으)로 바꾸기
>
>* `EdcPrincipalEmailAliasEntity`을(를) `EdcPrincipalEmailAliasEn`(으)로 바꾸기
>
>* `EdcPrincipalMappingEntity`을(를) `EdcPrincipalMappingEntit`(으)로 바꾸기
>
>* `EdcPrincipalGrpCtmntEntity`을(를) `EdcPrincipalGrpCtmntEnti`(으)로 바꾸기
>

```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### 사용자 데이터 삭제 {#delete-user-data}

데이터베이스 테이블에서 주도자 ID에 대한 사용자 관리 데이터를 삭제하려면 다음을 수행합니다.

1. 해당되는 경우 [사용자 데이터 삭제](/help/forms/using/user-management-handling-user-data.md#delete-aem)에 설명된 대로 AEM 저장소에서 사용자 데이터를 삭제합니다.
1. AEM Forms 서버를 종료합니다.
1. 데이터베이스 테이블에서 사용자 ID에 대한 사용자 관리 데이터를 삭제할 수 있도록 다음 데이터베이스 명령을 실행합니다. `Delete` 명령에서 `<principal_id>`을(를) 삭제하려는 데이터의 사용자 ID로 바꿉니다.

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. AEM Forms 서버를 시작합니다.

### AEM 저장소 {#aem-repository-1}

Forms JEE 사용자는 AEM Forms 작성자 인스턴스에 최소 한 번 이상 액세스한 경우 AEM 저장소에 데이터가 있습니다. AEM 저장소에서 해당 사용자 데이터에 액세스하고 삭제할 수 있습니다.

#### 사용자 데이터 액세스 {#access-user-data}

AEM 저장소에서 만든 사용자를 보려면 AEM 관리자 자격 증명으로 `https://'[server]:[port]'/lc/useradmin`에 로그인하십시오. URL의 `server` 및 `port`은(는) AEM 작성자 인스턴스의 것입니다. 여기에서 사용자 이름으로 사용자를 검색할 수 있습니다. 사용자에 대한 속성, 권한 및 그룹 등의 정보를 볼 수 있도록 사용자를 두 번 클릭합니다. 사용자의 `Path` 속성은 AEM 리포지토리에서 만든 사용자 노드로의 경로를 지정합니다.

#### 사용자 데이터 삭제 {#delete-aem}

사용자를 삭제하려면 다음을 수행하십시오.

1. AEM 관리자 자격 증명으로 `https://'[server]:[port]'/lc/useradmin`(으)로 이동합니다.
1. 사용자를 검색하고 사용자 이름을 두 번 클릭하여 사용자 속성을 엽니다. `Path` 속성을 복사합니다.
1. `https://'[server]:[port]'/lc/crx/de/index.jsp`의 AEM CRXDE Lite으로 이동하여 사용자 경로를 탐색하거나 검색하십시오.
1. 경로를 삭제하고 **[!UICONTROL 모두 저장]**&#x200B;을 클릭하여 AEM 저장소에서 사용자를 영구적으로 삭제합니다.
