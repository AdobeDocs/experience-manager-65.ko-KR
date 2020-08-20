---
title: Forms 포털 | 사용자 데이터 처리
seo-title: Forms 포털 | 사용자 데이터 처리
description: 'null'
seo-description: 'null'
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: 4e0709031aca030e50840811a9b3717f3cb20340
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# Forms 포털 | 사용자 데이터 처리 {#forms-portal-handling-user-data}

[!DNL AEM Forms] 포털에서는 페이지에 적응형 양식, HTML5 양식 및 기타 Forms 자산을 나열하는 데 사용할 수 있는 구성 요소를 [!DNL AEM Sites] 제공합니다. 또한 로그인한 사용자에 대해 초안 및 제출된 적응형 양식 및 HTML5 양식을 표시하도록 구성할 수 있습니다. 양식 포털에 대한 자세한 내용은 포털 [에 양식 게시 소개를 참조하십시오](/help/forms/using/introduction-publishing-forms.md).

로그인한 사용자가 적응형 양식을 초안으로 저장하거나 제출하면 양식 포털의 초안 및 제출 탭에 표시됩니다. 초안 또는 제출된 양식의 데이터는 AEM 배포를 위해 구성된 데이터 저장소에 저장됩니다. 익명 사용자의 초안 및 제출은 양식 포털 페이지에 표시되지 않습니다.하지만 데이터는 구성된 데이터 저장소에 저장됩니다. 자세한 내용은 초안 및 제출 [에 대한 스토리지 서비스 구성을 참조하십시오](/help/forms/using/configuring-draft-submission-storage.md).

## 사용자 데이터 및 데이터 저장소 {#user-data-and-data-stores}

Forms 포털은 다음 시나리오에서 초안 및 제출 양식에 대한 데이터를 저장합니다.

* 적응형 양식에 구성된 제출 작업은 **Forms 포털 제출 동작입니다**.
* Forms **포털 제출 작업**&#x200B;이외의 제출 작업의 경우 **[!UICONTROL 양식 포털에]** 데이터 **[!UICONTROL 저장]** 옵션이 적응형 양식 컨테이너의제출속성에서 활성화됩니다.

로그인 및 익명 사용자를 위한 모든 초안 및 제출 양식에 대해 양식 포털은 다음 데이터를 저장합니다.

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
   <td><p>작성자 및 게시 인스턴스 AEM 저장소</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>원격</p> </td>
   <td><p>작성자 및 원격 AEM 인스턴스 AEM 저장소</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>데이터베이스</p> </td>
   <td><p>작성자 인스턴스 및 데이터베이스 테이블 AEM 저장소</p> </td>
   <td>데이터베이스 테이블 <code>data</code>, <code>metadata</code>및 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

구성된 데이터 저장소에서 로그인 및 익명 사용자를 위해 초안 및 제출된 양식 데이터에 액세스할 수 있으며, 필요한 경우 삭제할 수 있습니다.

### AEM 인스턴스 {#aem-instances}

로그인 및 익명 사용자에 대한 AEM 인스턴스(작성자, 게시 또는 원격)의 모든 초안 및 제출된 양식 데이터는 해당 AEM 저장소의 `/content/forms/fp/` 노드에 저장됩니다. 로그인 또는 익명 사용자가 초안을 저장하거나 각 첨부 파일에 대한 양식, a `draft ID` 또는 `submission ID`A `user data ID`및 임의 `ID` 를 제출할 때마다(해당하는 경우) 해당 초안 또는 제출과 연관됩니다.

#### 사용자 데이터 액세스 {#access-user-data}

로그인한 사용자가 초안을 저장하거나 양식을 제출하면 사용자 ID로 하위 노드가 만들어집니다. 예를 들어 사용자 ID가 AEM 저장소의 노드에 저장된 Sarah Rose에 대한 초안 및 제출 데이터 `srose` 가 `/content/forms/fp/srose/` 있습니다. 사용자 ID 노드 내에서 데이터는 계층 구조로 구성됩니다.

다음 표에서는 모든 초안의 데이터를 AEM 저장소에 저장하는 방법 `srose` 을 설명합니다.

>[!NOTE]
>
>노드 아래에 있는 양식 `drafts` 에 대해 제출된 양식에 대한 정확한 구조 `srose` 가 `/content/forms/fp/srose/submit/` 복제됩니다.
>
>사용자의 모든 초안 및 제출 `anonymous` 은 `/content/forms/fp/anonymous/` 노드 아래에 저장되며, 이 노드는 `draft` 및 `submit` 노드 아래에 있는 모든 익명 사용자에 대한 초안 및 제출을 구성합니다.

| 노드 | 설명 |
|---|---|
| `/content/forms/fp/srose/drafts` | 사용자가 모든 초안의 컨테이너 노드 데이터 |
| `/content/forms/fp/srose/drafts/attachments/` | 초안 ID를 기반으로 사용자에 대한 모든 첨부 파일을 구성합니다. |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 선택한 ID에 대한 첨부 파일을 이진 형식으로 포함합니다. |
| `/content/forms/fp/srose/drafts/metadata/` | 초안 ID를 기반으로 사용자에 대한 양식 메타데이터를 구성합니다. |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 선택한 초안 ID에 대한 양식 메타데이터 포함 |
| `/content/forms/fp/srose/drafts/data/` | 사용자 데이터 ID를 기반으로 사용자의 양식 데이터를 구성합니다. |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 선택한 사용자 데이터 ID의 양식 데이터를 이진 형식으로 포함 |

#### 사용자 데이터 삭제 {#delete-user-data}

AEM 시스템에서 로그인한 사용자에 대한 초안 및 제출에서 사용자 데이터를 완전히 삭제하려면 작성자 노드에서 특정 사용자의 `user ID` 노드를 삭제해야 합니다. 적용 가능한 모든 AEM 인스턴스에서 데이터를 수동으로 삭제해야 합니다.

모든 익명 사용자에 대한 초안 및 제출 데이터는 아래의 공통 `drafts` 및 노드 `submit` 내에 `/content/forms/fp/anonymous`저장됩니다. 일부 식별 정보가 알려지지 않는 한 특정 익명 사용자에 대한 데이터를 찾을 수 있는 방법은 없습니다. 이 경우 AEM 저장소의 익명 사용자를 식별하는 정보를 검색하고 해당 노드가 포함된 노드를 모든 해당 AEM 인스턴스에서 수동으로 삭제하여 AEM 시스템에서 데이터를 제거할 수 있습니다. 하지만 모든 익명 사용자에 대한 데이터를 삭제하려면 노드를 삭제하여 모든 익명 사용자에 대한 초안 및 제출 데이터를 제거할 수 있습니다. `anonymous`

### 데이터베이스 {#database}

AEM이 데이터베이스에 데이터를 저장하도록 구성되면 양식 포털 초안 및 제출 데이터는 로그인된 사용자와 익명 사용자 모두를 위한 다음 데이터베이스 테이블에 저장됩니다.

* 데이터
* 메타데이터
* 추가 메타데이터

#### 사용자 데이터 액세스 {#access-user-data-1}

데이터베이스 테이블에서 로그인한 사용자와 익명 사용자에 대한 초안 및 제출 데이터에 액세스하려면 다음 데이터베이스 명령을 실행하십시오. 쿼리에서 액세스하려는 데이터 `logged-in user` 의 사용자 ID나 익명 사용자를 `anonymous` 위한 ID로 바꿉니다.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 사용자 데이터 삭제 {#delete-user-data-1}

로그인한 사용자의 초안 및 제출 데이터를 데이터베이스 테이블에서 삭제하려면 다음 데이터베이스 명령을 실행합니다. 쿼리에서 삭제할 데이터의 사용자 ID `logged-in user` 로 바꾸거나 익명 사용자를 `anonymous` 위한 ID로 바꿉니다. 데이터베이스에서 특정 익명 사용자에 대한 데이터를 삭제하려면 일부 식별 가능한 정보를 사용하여 해당 데이터를 찾고 정보가 포함된 데이터베이스 테이블에서 삭제해야 합니다.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

