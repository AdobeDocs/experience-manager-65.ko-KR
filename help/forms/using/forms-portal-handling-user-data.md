---
title: Forms 포털| 사용자 데이터 처리
seo-title: Forms 포털| 사용자 데이터 처리
description: 'null'
seo-description: 'null'
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Forms 포털| 사용자 데이터 처리 {#forms-portal-handling-user-data}

AEM Forms 포털은 AEM Sites 페이지에서 적응형 양식, HTML5 양식 및 기타 양식 자산을 나열하는 데 사용할 수 있는 구성 요소를 제공합니다. 또한 로그인 사용자를 위해 초안 및 제출된 적응형 양식 및 HTML5 양식을 표시하도록 구성할 수 있습니다. 양식 포털에 대한 자세한 내용은 [포털에서](/help/forms/using/introduction-publishing-forms.md)양식 게시 소개를 참조하십시오.

로그인한 사용자가 적응형 양식을 초안으로 저장하거나 제출하면 양식 포털의 초안 및 제출 탭에 표시됩니다. 초안 또는 제출된 양식의 데이터는 AEM 배포를 위해 구성된 데이터 저장소에 저장됩니다. 익명 사용자의 초안 및 제출은 양식 포털 페이지에 표시되지 않습니다.하지만 데이터는 구성된 데이터 저장소에 저장됩니다. 자세한 내용은 초안 및 제출용 [스토리지 서비스 구성을](/help/forms/using/configuring-draft-submission-storage.md)참조하십시오.

## 사용자 데이터 및 데이터 저장소 {#user-data-and-data-stores}

양식 포털은 다음 시나리오에서 초안 및 제출된 양식에 대한 데이터를 저장합니다.

* 적응형 양식에 구성된 제출 작업은 Forms Portal **제출 동작입니다**.
* Forms 포털 제출 **작업 이외의 제출 작업의**&#x200B;경우 **[!UICONTROL 적응형 양식 컨테이너의 제출]** 속성에서 **양식 포털에** 데이터저장 옵션이 활성화됩니다.

양식 포털은 로그인 및 익명 사용자를 위해 초안 및 제출된 모든 양식에 다음 데이터를 저장합니다.

* 양식 이름, 양식 경로, 초안 또는 제출 ID, 첨부 파일 경로 및 사용자 데이터 ID와 같은 양식 메타데이터
* 데이터 바이트로 양식 첨부
* 데이터 바이트로 양식 데이터

구성된 데이터 저장소 지속성에 따라 초안 및 제출된 양식 데이터는 다음 위치에 저장됩니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>지속성 유형</strong></p> </td>
   <td><p><strong>데이터 저장소</strong></p> </td>
   <td><p><strong>위치</strong></p> </td>
  </tr>
  <tr>
   <td><p>기본값</p> </td>
   <td><p>작성자 및 게시 인스턴스의 AEM 저장소</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>원격</p> </td>
   <td><p>작성자 및 원격 AEM 인스턴스의 AEM 저장소</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>데이터베이스</p> </td>
   <td><p>작성자 인스턴스 및 데이터베이스 테이블의 AEM 저장소</p> </td>
   <td>데이터베이스 테이블 <code>data</code>, <code>metadata</code>및 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

구성된 데이터 저장소에서 로그인 및 익명 사용자를 위해 초안 및 제출된 양식 데이터에 액세스할 수 있으며, 필요한 경우 삭제할 수 있습니다.

### AEM 인스턴스 {#aem-instances}

로그인 및 익명 사용자에 대한 AEM 인스턴스(작성자, 게시 또는 원격)의 모든 초안 및 제출된 양식 데이터는 해당 AEM 저장소의 `/content/forms/fp/` 노드에 저장됩니다. 로그인한 사용자 또는 익명 사용자가 초안을 저장하거나 각 첨부 파일(해당되는 경우)에 대해 양식, a `draft ID` 또는 `submission ID`A `user data ID`및 `ID` Random을 생성할 때마다 해당 초안 또는 제출과 연결됩니다.

#### 사용자 데이터 액세스 {#access-user-data}

로그인한 사용자가 초안을 저장하거나 양식을 제출하면 하위 노드가 사용자 ID로 만들어집니다. 예를 들어 사용자 ID가 AEM 저장소의 `srose` `/content/forms/fp/srose/` 노드에 저장되는 Sarah Rose에 대한 초안 및 제출 데이터입니다. 사용자 ID 노드 내에서 데이터는 계층적 구조로 구성됩니다.

다음 표에서는 모든 초안의 데이터를 AEM 저장소에 저장하는 방법을 `srose` 설명합니다.

>[!NOTE]
>
>노드 아래에 `drafts` 제출된 양식에 대해 같은 구조가 `srose` `/content/forms/fp/srose/submit/` 복제됩니다.
>
>사용자가 제출한 모든 초안 및 제출은 `anonymous` 노드 아래에 저장되며, 이 노드는 `/content/forms/fp/anonymous/` 및 `draft` `submit` 노드 아래에 있는 모든 익명 사용자에 대한 초안 및 제출을 구성합니다.

| 노드 | 설명 |
|---|---|
| `/content/forms/fp/srose/drafts` | 사용자의 모든 초안에 대한 컨테이너 노드 데이터 |
| `/content/forms/fp/srose/drafts/attachments/` | 초안 ID를 기반으로 사용자의 모든 첨부 파일을 구성합니다. |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 이진 형식으로 선택한 ID에 대한 첨부 파일 포함 |
| `/content/forms/fp/srose/drafts/metadata/` | 초안 ID를 기반으로 사용자에 대한 양식 메타데이터를 구성합니다. |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 선택한 초안 ID에 대한 양식 메타데이터 포함 |
| `/content/forms/fp/srose/drafts/data/` | 사용자 데이터 ID를 기반으로 사용자에 대한 양식 데이터를 구성합니다. |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 선택한 사용자 데이터 ID의 양식 데이터를 이진 형식으로 포함 |

#### 사용자 데이터 삭제 {#delete-user-data}

AEM 시스템에서 로그인한 사용자에 대한 초안 및 제출에서 사용자 데이터를 완전히 삭제하려면 작성자 노드에서 특정 사용자에 대한 `user ID` 노드를 삭제해야 합니다. 모든 해당 AEM 인스턴스에서 데이터를 수동으로 삭제해야 합니다.

모든 익명 사용자에 대한 초안 및 제출 데이터는 아래의 공통 `drafts` 및 `submit` 노드 내에 저장됩니다 `/content/forms/fp/anonymous`. 일부 식별 가능한 정보가 알려지지 않는 한 특정 익명 사용자에 대한 데이터를 찾을 수 있는 방법이 없습니다.이 경우 AEM 저장소의 익명 사용자를 식별하는 정보를 검색하고 해당 노드가 포함된 노드를 모든 해당 AEM 인스턴스에서 수동으로 삭제하여 AEM 시스템에서 데이터를 제거할 수 있습니다. 하지만 익명 모든 사용자에 대한 데이터를 삭제하려면 노드를 삭제하여 모든 익명 사용자에 대한 초안 및 제출 데이터를 제거할 수 있습니다. `anonymous`

### 데이터베이스 {#database}

AEM이 데이터베이스에 데이터를 저장하도록 구성된 경우, 양식 포털 초안 및 제출 데이터는 로그인된 사용자와 익명 사용자 모두에 대해 다음 데이터베이스 테이블에 저장됩니다.

* data
* 메타데이터
* additionalmetadata

#### 사용자 데이터 액세스 {#access-user-data-1}

데이터베이스 테이블에서 로그인한 사용자와 익명 사용자에 대한 초안 및 제출 데이터에 액세스하려면 다음 데이터베이스 명령을 실행하십시오. 쿼리에서 액세스하려는 데이터의 사용자 ID `logged-in user` 로 바꾸거나 익명 사용자를 `anonymous` 위해 바꿉니다.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 사용자 데이터 삭제 {#delete-user-data-1}

데이터베이스 테이블에서 로그인한 사용자에 대한 초안 및 제출 데이터를 삭제하려면 다음 데이터베이스 명령을 실행합니다. 쿼리에서 삭제할 데이터의 사용자 ID `logged-in user` 로 바꾸거나 익명 사용자를 `anonymous` 위해 바꿉니다. 데이터베이스에서 특정 익명 사용자에 대한 데이터를 삭제하려면 일부 식별 가능한 정보를 사용하여 해당 데이터를 찾고 정보가 포함된 데이터베이스 테이블에서 삭제해야 합니다.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

