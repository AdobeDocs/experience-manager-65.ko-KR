---
title: 권한 관리에 대한 보안 주체 보기
description: 권한 관리를 용이하게 하는 새로운 Touch UI 인터페이스에 대해 알아봅니다.
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 1%

---


# 권한 관리에 대한 보안 주체 보기{#principal-view-for-permissions-management}

## 개요 {#overview}

AEM 6.5에는 사용자 및 그룹에 대한 권한 관리가 도입되었습니다. 기본 기능은 클래식 UI와 동일하게 유지되지만 보다 사용자 친화적이고 효율적입니다.

## 사용 방법 {#how-to-use}

### UI 액세스 {#accessing-the-ui}

새 UI 기반 권한 관리는 아래와 같이 보안 아래의 권한 카드를 통해 액세스할 수 있습니다.

![권한 관리 UI](assets/screen_shot_2019-03-17at63333pm.png)

새 보기를 사용하면 명시적으로 권한이 부여된 모든 경로에서 특정 주체에 대한 전체 권한 및 제한 사항을 보다 쉽게 볼 수 있습니다. 이렇게 하면 (으)로 이동할 필요가 없습니다.

고급 권한 및 제한 사항을 관리하는 CRXDE입니다. 동일한 보기로 통합되었습니다. 보기의 기본값은 그룹 &quot;everyone&quot;입니다.

![&quot;모든 사용자&quot; 그룹 보기](assets/unu-1.png)

사용자가 확인할 주도자 유형을 선택할 수 있는 필터가 있습니다 **사용자**, **그룹**, 또는 **모두**&#x200B;모든 사용자를 검색합니다.**.**

![주체 유형 검색](assets/image2019-3-20_23-52-51.png)

### 주체에 대한 권한 보기 {#viewing-permissions-for-a-principal}

왼쪽의 프레임을 사용하면 아래와 같이 아래로 스크롤하여 주체를 찾거나 선택한 필터를 기반으로 그룹 또는 사용자를 검색할 수 있습니다.

![사용자에 대한 권한 보기](assets/doi-1.png)

이름을 클릭하면 오른쪽에 할당된 권한이 표시됩니다. 권한 창에는 구성된 제한 사항과 함께 특정 경로의 액세스 제어 항목 목록이 표시됩니다.

![ACL 목록 보기](assets/trei-1.png)

### 주체에 대한 새 액세스 제어 항목 추가 {#adding-new-access-control-entry-for-a-principal}

액세스 제어 항목을 추가하여 새 권한을 추가할 수 있습니다. ACE 추가 버튼을 클릭하면 됩니다.

![주체에 대한 새 ACL 추가](assets/patru.png)

이렇게 하면 아래에 표시된 창이 나타나며, 다음 단계는 권한을 구성해야 하는 경로를 선택하는 것입니다.

![권한 경로 구성](assets/cinci-1.png)

여기에서 권한을 구성할 수 있는 경로를 선택합니다. **dam-users**:

![dam 사용자에 대한 구성 예](assets/sase-1.png)

경로를 선택하면 워크플로가 이 화면으로 돌아갑니다. 그러면 사용자는 사용 가능한 네임스페이스에서 하나 이상의 권한을 선택할 수 있습니다(예: `jcr`, `rep` 또는 `crx`)을 참조하십시오.

텍스트 필드를 사용하여 검색한 다음 목록에서 선택하여 권한을 추가할 수 있습니다.

>[!NOTE]
>
>권한 및 설명의 전체 목록은 다음을 참조하십시오. [이 페이지](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![주어진 경로에 대한 검색 권한.](assets/image2019-3-21_0-5-47.png) ![세로 열에서 선택한 경로로 표시되는 대로 &#39;dam-users&#39;에 대한 새 항목을 추가합니다.](assets/image2019-3-21_0-6-53.png)

권한 목록을 선택한 후 사용자는 아래와 같이 권한 유형: 거부 또는 허용 을 선택할 수 있습니다.

![권한 선택](assets/screen_shot_2019-03-17at63938pm.png) ![권한 선택](assets/screen_shot_2019-03-17at63947pm.png)

### 제한 사용 {#using-restrictions}

지정된 경로에 대한 권한 목록 및 권한 유형 외에도 이 화면에서는 아래와 같이 세분화된 액세스 제어에 대한 제한을 추가할 수 있습니다.

![제한 추가](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>각 제한의 의미에 대한 자세한 내용은 [jackrabbit Oak 설명서](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

제한 유형을 선택하고 값을 입력한 다음 을 눌러 아래와 같이 제한을 추가할 수 있습니다. **+** 아이콘.

![제한 유형 추가](assets/sapte-1.png) ![제한 유형 추가](assets/opt-1.png)

새 ACE는 아래와 같이 액세스 제어 목록에 반영됩니다. 참고: `jcr:write` 은 다음을 포함하는 집계 권한입니다. `jcr:removeNode` 위에서 추가되었지만, 다음에서 다루는 것처럼 아래에 표시되지 않습니다. `jcr:write`.

### ACE 편집 {#editing-aces}

주도자를 선택하고 편집할 ACE를 선택하여 액세스 제어 항목을 편집할 수 있습니다.

예를 들어 다음 항목을 편집할 수 있습니다. **dam-users** 오른쪽의 연필 아이콘을 클릭하여:

![제한 추가](assets/image2019-3-21_0-35-39.png)

편집 화면은 구성된 ACE가 미리 선택된 상태로 표시되며, 이 ACE 옆에 있는 교차 아이콘을 클릭하여 삭제하거나 아래와 같이 주어진 경로에 대해 새 권한을 추가할 수 있습니다.

![항목 편집](assets/noua-1.png)

다음 `addChildNodes` 다음에 대한 권한이 추가되었습니다. **dam-users** 지정한 경로에서.

![권한 추가](assets/image2019-3-21_0-45-35.png)

변경 사항은 다음을 클릭하여 저장할 수 있습니다. **저장** 오른쪽 상단의 단추를 클릭하면 변경 사항이 의 새 권한에 반영됩니다. **dam-users** 아래와 같이:

![변경 내용 저장](assets/zece-1.png)

### ACE 삭제 {#deleting-aces}

액세스 제어 항목을 삭제하여 특정 경로의 사용자에게 부여된 모든 권한을 제거할 수 있습니다. ACE 옆에 있는 X 아이콘을 사용하여 아래와 같이 삭제할 수 있습니다.

![ACE 삭제](assets/image2019-3-21_0-53-19.png) ![ACE 삭제](assets/unspe.png)

### 클래식 UI 권한 조합 {#classic-ui-privilege-combinations}

새 권한 UI는 부여된 정확한 기본 권한을 반영하지 않는 사전 정의된 조합 대신 기본 권한 집합을 명시적으로 사용합니다.

이는 정확히 무엇을 구성하고 있는지에 대한 혼동을 유발하였다. 다음 표에는 기본 UI에서 해당 권한을 구성하는 실제 권한으로의 권한 조합 간의 매핑이 나열되어 있습니다.

<table>
 <tbody>
  <tr>
   <th>클래식 UI 권한 조합</th>
   <th>권한 UI 권한</th>
  </tr>
  <tr>
   <td>읽기</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>수정</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>만들기</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>삭제</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>ACL 읽기</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>ACL 편집</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>복제</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
