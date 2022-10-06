---
title: 문서 보안 | 사용자 데이터 처리
seo-title: Document Security | Handling user data
description: 문서 보안 | 사용자 데이터 처리
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
role: Admin
exl-id: 00c01a12-1180-4f35-9179-461bf177c787
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 문서 보안 | 사용자 데이터 처리 {#document-security-handling-user-data}

AEM Forms 문서 보안을 사용하면 사전 정의된 보안 설정을 작성, 저장 및 문서에 적용할 수 있습니다. 이렇게 하면 권한이 있는 사용자만 문서를 사용할 수 있습니다. 정책을 사용하여 문서를 보호할 수 있습니다. 정책은 보안 설정과 권한이 있는 사용자 목록을 포함하는 정보 모음입니다. 하나 이상의 문서에 정책을 적용하고 AEM Forms JEE 사용자 관리에 추가된 사용자를 인증할 수 있습니다.

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## 사용자 데이터 및 데이터 저장소 {#user-data-and-data-stores}

문서 보안은 My Sql, Oracle, MS SQL Server 및 IBM DB2와 같은 데이터베이스에 사용자 데이터를 포함하여 보호된 문서와 관련된 정책 및 데이터를 저장합니다. 또한, 정책에 있는 인증된 사용자에 대한 데이터는 사용자 관리에 저장됩니다. 사용자 관리에 저장된 데이터에 대해서는 [Forms 사용자 관리: 사용자 데이터 처리](/help/forms/using/user-management-handling-user-data.md).

다음 표는 문서 보안이 데이터베이스 테이블의 데이터를 구성하는 방법을 매핑합니다.

<table>
 <tbody>
  <tr>
   <td>데이터베이스 테이블</td>
   <td>설명</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>사용자의 주요 키에 대한 정보를 저장합니다. 키는 오프라인 문서 보안 워크플로우에서 사용됩니다.</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>사용자 이벤트, 문서 이벤트 및 정책 이벤트와 같은 감사 이벤트에 대한 정보를 저장합니다.</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>보호된 문서의 레코드를 저장합니다. 모든 보호된 문서에 대한 라이센스 세부 사항을 저장합니다.</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>시스템에서 생성된 모든 라이센스의 문서 이름을 저장합니다.</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>보호된 문서의 취소 및 복구에 대한 정보를 저장합니다.</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>정책 페이지의 내 정책 탭에 나타나는 개인 정책을 생성할 수 있는 사용자에 대한 정보를 저장합니다. </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>정책에 대한 정보를 저장합니다. 각 정책은 이 테이블의 행에 해당합니다.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>활성 정책에 사용할 XML 파일을 저장합니다. 정책 XML<sup> </sup>정책과 연결된 사용자의 주 ID에 대한 참조를 포함합니다. 정책 XML은 Blob 개체로 저장됩니다.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>보관된 정책에 대한 정보를 저장합니다. 아카이브된 정책에는 Blob 객체로 저장된 정책 XML이 포함되어 있습니다.</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> (Oracle 및 MS SQL 데이터베이스)</p> </td>
   <td>정책 세트와 사용자 간의 매핑을 저장합니다.</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>초대된 사용자에 대한 정보를 저장합니다.</td>
  </tr>
 </tbody>
</table>

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

데이터베이스의 사용자에 대한 문서 보안 데이터에 액세스하여 내보낼 수 있으며, 필요한 경우 영구적으로 삭제할 수 있습니다.

데이터베이스에서 사용자 데이터를 내보내거나 삭제하려면 데이터베이스 클라이언트를 사용하여 데이터베이스에 연결하고 사용자의 개인 식별 정보를 기반으로 주체 ID를 확인해야 합니다. 예를 들어 로그인 ID를 사용하여 사용자의 주체 ID를 검색하려면 다음을 실행하십시오 `select` 데이터베이스에 대한 명령.

에서 `select` 명령, 바꾸기 `<user_login_id>` (으)로부터 검색할 사용자 주체 ID의 로그인 ID를 사용하여 `EdcPrincipalUserEntity` 데이터베이스 테이블.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

주도자 ID를 알고 있으면 사용자 데이터를 내보내거나 삭제할 수 있습니다.

### 사용자 데이터 내보내기 {#export-user-data}

다음 데이터베이스 명령을 실행하여 데이터베이스 테이블에서 주체 ID에 대한 사용자 데이터를 내보냅니다. 에서 `select` 명령, 바꾸기 `<principal_id>` (데이터를 내보내려는 사용자의 주체 ID로).

>[!NOTE]
>
>다음 명령은 My SQL 및 IBM DB2 데이터베이스에서 데이터베이스 테이블 이름을 사용합니다. oracle 및 MS SQL 데이터베이스에서 이러한 명령을 실행하면 `EdcPolicySetPrincipalEntity` with `EdcPolicySetPrincipalEnt` 를 입력합니다.

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>에서 데이터를 내보내려면 `EdcAuditEntity` 표, [EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) 를 가져오는 API [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) 를 기준으로 감사 데이터를 내보내는 매개 변수로 `principalId`, `policyId`, 또는 `licenseId`.

시스템에서 사용자에 대한 전체 데이터를 가져오려면 사용자 관리 데이터베이스에서 데이터에 액세스하여 내보내야 합니다. 자세한 내용은 [Forms 사용자 관리: 사용자 데이터 처리](/help/forms/using/user-management-handling-user-data.md).

### 사용자 데이터 삭제 {#delete-user-data}

데이터베이스 테이블에서 주체 ID에 대한 문서 보안 데이터를 삭제하려면 다음을 수행합니다.

1. AEM Forms 서버를 종료합니다.
1. 다음 데이터베이스 명령을 실행하여 문서 보안을 위해 데이터베이스 테이블에서 주체 ID에 대한 데이터를 삭제합니다. 에서 `Delete` 명령, 바꾸기 `<principal_id>` 삭제할 데이터가 있는 사용자의 주체 ID와 함께 사용할 수 있습니다.

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >에서 데이터를 삭제하려면 `EdcAuditEntity` 표, [EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) 를 가져오는 API [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) 를 기준으로 감사 데이터를 삭제할 매개 변수로 `principalId`, `policyId`, 또는 `licenseId`.

1. 활성 및 아카이브된 정책 XML 파일은 `EdcPolicyXmlEntity` 및 `EdcPolicyArchiveEntity` 각각 데이터베이스 테이블. 이러한 테이블에서 사용자의 데이터를 삭제하려면 다음을 수행합니다.

   1. 에서 각 행의 XML 블롭 열기 `EdcPolicyXMLEntity` 또는 `EdcPolicyArchiveEntity` 표 및 XML 파일 추출 XML 파일은 아래 표시된 파일과 유사합니다.
   1. XML 파일을 편집하여 주체 ID의 블롭을 제거합니다.
   1. 다른 파일에 대해 1단계와 2단계를 반복합니다.

   >[!NOTE]
   >
   >내에서 전체 Blob를 제거해야 합니다 `Principal` 태그로 인해 주 ID 또는 정책 XML에 대한 태그가 손상되거나 사용할 수 없습니다.

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   또한 `EdcPolicyXmlEntity` 표, 다음 두 가지 방법으로 이 작업을 수행할 수 있습니다.

   **관리 콘솔 사용**

   1. 관리자는 https://에서 Forms JEE 관리 콘솔에 로그인합니다&#x200B;[*server*]:[*포트*]/adminui
   1. 다음으로 이동 **[!UICONTROL 서비스 > 문서 보안 > 정책 세트]**.
   1. 정책 세트를 열고 정책에서 사용자를 삭제합니다.

   **문서 보안 웹 페이지 사용**

   개인 정책을 만들 권한이 있는 문서 보안 사용자는 자신의 정책에서 사용자 데이터를 삭제할 수 있습니다. 방법은 다음과 같습니다.

   1. 개인 정책이 있는 사용자는 https://에서 문서 보안 웹 페이지에 로그인합니다&#x200B;[*server*]:[*포트*]/edc.
   1. 다음으로 이동 **[!UICONTROL 서비스 > 문서 보안 > 내 정책]**.
   1. 정책을 열고 정책에서 사용자를 삭제합니다.

   >[!NOTE]
   >
   >관리자는 **[!UICONTROL 서비스 > 문서 보안 > 내 정책]** 관리 콘솔 사용.

1. 사용자 관리 데이터베이스에서 주체 ID의 데이터를 삭제합니다. 자세한 단계는 [Forms 사용자 관리 | 사용자 데이터 처리](/help/forms/using/user-management-handling-user-data.md).
1. AEM Forms 서버를 시작합니다.
