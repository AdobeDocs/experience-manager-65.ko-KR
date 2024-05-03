---
title: Forms 포털 | 사용자 데이터 처리
description: AEM Forms 포털에서 액세스, 삭제 및 데이터 저장소와 같은 사용자 데이터 관리에 대해 알아봅니다.
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: 791524a4-a8bb-4632-a68d-e96864e139a9
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Forms 포털 | 사용자 데이터 처리 {#forms-portal-handling-user-data}

[!DNL AEM Forms] 포털은 적응형 양식, HTML5 양식 및 기타 Forms 에셋을 나열하는 데 사용할 수 있는 구성 요소를 제공합니다. [!DNL AEM Sites] 페이지를 가리키도록 업데이트하는 중입니다. 또한 로그인한 사용자의 초안 및 제출된 적응형 양식과 HTML 5 양식을 표시하도록 구성할 수 있습니다. Forms 포털에 대한 자세한 내용은 [포털에 양식 게시 소개](/help/forms/using/introduction-publishing-forms.md).

로그인한 사용자가 적응형 양식을 초안으로 저장하거나 제출하면 Forms 포털의 초안 및 제출 탭에 표시됩니다. 초안 또는 제출된 양식의 데이터는 AEM 배포용으로 구성된 데이터 저장소에 저장됩니다. 익명 사용자의 초안 및 제출은 Forms 포털 페이지에 표시되지 않지만 데이터는 구성된 데이터 저장소에 저장됩니다. 다음을 참조하십시오 [초안 및 제출을 위한 스토리지 서비스 구성](/help/forms/using/configuring-draft-submission-storage.md).

## 사용자 데이터 및 데이터 저장소 {#user-data-and-data-stores}

Forms 포털은 다음 시나리오에서 초안 및 제출된 양식에 대한 데이터를 저장합니다.

* 적응형 양식에 구성된 제출 액션은 다음과 같습니다. **Forms 포털 제출 액션**.
* 제출 액션 제외 **Forms 포털 제출 액션**, **[!UICONTROL Forms 포털에 데이터 저장]** 옵션이에서 활성화됨 **[!UICONTROL 제출]** 적응형 양식 컨테이너 속성.

Forms 포털은 로그인 사용자와 익명 사용자의 초안 및 제출된 양식마다 다음 데이터를 저장합니다.

* 양식 이름, 양식 경로, 초안 또는 제출 ID, 첨부 파일 경로 및 사용자 데이터 ID와 같은 양식 메타데이터
* 데이터 바이트로 양식 첨부 파일
* 양식 데이터를 데이터 바이트로

구성된 데이터 저장소 지속성에 따라 초안 및 제출된 양식 데이터가 다음 위치에 저장됩니다.

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
   <td>데이터베이스 테이블 <code>data</code>, <code>metadata</code>, 및 <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

구성된 데이터 저장소에서 로그인한 사용자 및 익명 사용자에 대한 초안 및 제출된 양식 데이터에 액세스하고, 필요한 경우 삭제할 수 있습니다.

### AEM 인스턴스 {#aem-instances}

로그인 및 익명 사용자의 AEM 인스턴스(작성자, 게시 또는 원격)에 있는 모든 초안 및 제출된 양식 데이터는에 저장됩니다. `/content/forms/fp/` 적용 가능한 AEM 저장소의 노드. 로그인 또는 익명 사용자가 초안을 저장하거나 양식을 제출할 때마다 `draft ID` 또는 `submission ID`, a `user data ID`및 임의 `ID` 각 첨부 파일(해당되는 경우)에 대해 생성됩니다. 해당 초안 또는 제출과 연관됩니다.

#### 사용자 데이터 액세스 {#access-user-data}

로그인한 사용자가 초안을 저장하거나 양식을 제출할 때 하위 노드가 해당 사용자 ID로 생성됩니다. 예를 들어 사용자 ID가 인 Sarah Rose에 대한 초안 및 제출 데이터 `srose` 저장 위치: `/content/forms/fp/srose/` AEM 저장소의 노드 사용자 ID 노드 내에서 데이터는 계층 구조로 구성됩니다.

다음 표에서는 모든 초안에 대한 데이터의 기준 `srose` AEM 저장소에 저장됩니다.

>[!NOTE]
>
>다음과 같은 정확한 구조 `drafts` 다음에 대해 제출된 양식용으로 복제됨: `srose` 다음 아래에 `/content/forms/fp/srose/submit/` 노드.
>
>모든 초안 및 제출 기준 `anonymous` 사용자는 아래에 저장됩니다. `/content/forms/fp/anonymous/` 노드: 모든 익명 사용자에 대한 초안 및 제출 구성 `draft` 및 `submit` 노드.

| 노드 | 설명 |
|---|---|
| `/content/forms/fp/srose/drafts` | 사용자가 모든 초안에 대한 컨테이너 노드 데이터 |
| `/content/forms/fp/srose/drafts/attachments/` | 초안 ID를 기반으로 사용자의 모든 첨부 파일 구성 |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | 선택한 ID에 대한 첨부 파일을 이진 형식으로 포함합니다. |
| `/content/forms/fp/srose/drafts/metadata/` | 초안 ID를 기반으로 사용자의 양식 메타데이터 구성 |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | 선택한 초안 ID에 대한 양식 메타데이터 포함 |
| `/content/forms/fp/srose/drafts/data/` | 사용자 데이터 ID를 기반으로 사용자의 양식 데이터를 구성합니다. |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | 선택한 사용자 데이터 ID의 양식 데이터를 이진 형식으로 포함합니다. |

#### 사용자 데이터 삭제 {#delete-user-data}

초안에서 사용자 데이터를 삭제하고 AEM 시스템에서 로그인한 사용자에 대한 제출을 완전히 삭제하려면 `user ID` 작성자 노드의 특정 사용자에 대한 노드입니다. 적용 가능한 모든 AEM 인스턴스에서 데이터를 수동으로 삭제합니다.

모든 익명 사용자에 대한 초안 및 제출 데이터는 일반 내에 저장됩니다. `drafts` 및 `submit` 노드 `/content/forms/fp/anonymous`. 일부 식별 가능한 정보를 알 수 없는 한 특정 익명 사용자에 대한 데이터를 찾을 수 있는 방법은 없습니다. 이 경우 AEM 저장소에서 익명 사용자를 식별하는 정보를 검색하고 해당하는 모든 AEM 인스턴스에서 해당 사용자가 포함된 노드를 수동으로 삭제하여 AEM 시스템에서 데이터를 제거할 수 있습니다. 그러나 모든 익명 사용자에 대한 데이터를 삭제하려면 `anonymous` 모든 익명 사용자에 대한 초안 및 제출 데이터를 제거할 노드입니다.

### 데이터베이스 {#database}

AEM이 데이터베이스에 데이터를 저장하도록 구성된 경우 Forms 포털 초안 및 제출 데이터는 로그인한 사용자와 익명 사용자 모두에 대해 다음 데이터베이스 테이블에 저장됩니다.

* 데이터
* 메타데이터
* additionalmetadata

#### 사용자 데이터 액세스 {#access-user-data-1}

데이터베이스 테이블에서 로그인한 사용자와 익명 사용자에 대한 초안 및 제출 데이터에 액세스하려면 다음 데이터베이스 명령을 실행합니다. 쿼리에서 바꾸기 `logged-in user` (또는 와 함께 액세스하려는 데이터의 사용자 ID 포함) `anonymous` 익명 사용자용

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### 사용자 데이터 삭제 {#delete-user-data-1}

데이터베이스 테이블에서 로그인한 사용자에 대한 초안 및 제출 데이터를 삭제하려면 다음 데이터베이스 명령을 실행합니다. 쿼리에서 바꾸기 `logged-in user` 삭제하려는 데이터 또는 를 사용하는 사용자 ID 포함 `anonymous` 익명 사용자용 데이터베이스에서 특정 익명 사용자에 대한 데이터를 삭제하려면 일부 식별 정보를 사용하여 해당 데이터를 찾은 다음 해당 정보가 포함된 데이터베이스 테이블에서 삭제해야 합니다.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```
