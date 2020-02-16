---
title: 권한 관리를 위한 기본 보기
seo-title: 권한 관리를 위한 기본 보기
description: 권한 관리를 용이하게 하는 새로운 터치 UI 인터페이스에 대해 알아봅니다.
seo-description: 권한 관리를 용이하게 하는 새로운 터치 UI 인터페이스에 대해 알아봅니다.
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
translation-type: tm+mt
source-git-commit: a156e09e77951041dce017f2f78069bc050b6bdb

---


# 권한 관리를 위한 기본 보기{#principal-view-for-permissions-management}

## 개요 {#overview}

AEM 6.5에서는 사용자 및 그룹에 대한 권한 관리를 제공합니다. 기본 기능은 클래식 UI와 동일하게 유지되지만 사용자에게 더 친숙하고 효율적입니다.

## 사용 방법 {#how-to-use}

### UI 액세스 {#accessing-the-ui}

새 UI 기반 권한 관리는 아래와 같이 보안 아래의 권한 카드를 통해 액세스합니다.

![](assets/screen_shot_2019-03-17at63333pm.png)

새 보기를 사용하면 권한이 명시적으로 부여된 모든 경로에서 지정된 주체에 대한 전체 권한 및 제한 사항을 쉽게 확인할 수 있습니다. 이렇게 하면

CRXDE를 사용하여 고급 권한 및 제한 사항을 관리할 수 있습니다. 동일한 관점에서 통합되었습니다. 기본적으로 보기는 &quot;everyone&quot; 그룹으로 설정됩니다.

![](assets/unu-1.png)

사용자가 사용자, 그룹 또는 모두를 보고 **모든**&#x200B;주도자 **유형을 선택하고**&#x200B;주도자를 **검색할 수**&#x200B;있는&#x200B;**필터가 있습니다.**

![](assets/image2019-3-20_23-52-51.png)

### 주도자에 대한 권한 보기 {#viewing-permissions-for-a-principal}

왼쪽의 프레임에서는 아래에서와 같이 아래로 스크롤하여 주체를 찾거나 선택한 필터를 기반으로 그룹 또는 사용자를 검색할 수 있습니다.

![](assets/doi-1.png)

이름을 클릭하면 오른쪽의 할당된 권한이 표시됩니다. 권한 창에는 구성된 제한 사항과 함께 특정 경로에 대한 액세스 제어 항목 목록이 표시됩니다.

![](assets/trei-1.png)

### 주체용 새 액세스 제어 항목 추가 {#adding-new-access-control-entry-for-a-principal}

ACE 추가 버튼을 클릭하여 새로운 액세스 제어 항목을 추가하여 새 권한을 추가할 수 있습니다.

![](assets/patru.png)

이렇게 하면 아래에 표시된 창이 표시됩니다. 다음 단계는 권한을 구성해야 하는 경로를 선택하는 것입니다.

![](assets/cinci-1.png)

여기에서 **dam-users**&#x200B;권한을 구성할 경로를 선택합니다.

![](assets/sase-1.png)

경로를 선택하면 워크플로우가 이 화면으로 돌아갑니다. 이 화면에서 사용자는 아래 표시된 대로 사용 가능한 네임스페이스( `jcr`또는 `rep` 또는 `crx`)에서 하나 이상의 권한을 선택할 수 있습니다.

텍스트 필드를 사용한 검색 후 목록에서 선택하여 권한을 추가할 수 있습니다.

>[!NOTE]
>
>전체 권한 및 설명 목록은 [이 페이지를](/help/sites-administering/user-group-ac-admin.md#access-right-management)참조하십시오.

![](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

권한 목록을 선택한 후 사용자는 권한 유형을 선택할 수 있습니다.거부 또는 허용을 참조하십시오.

![](assets/screen_shot_2019-03-17at63938pm.png) ![](assets/screen_shot_2019-03-17at63947pm.png)

### 제한 사용 {#using-restrictions}

이 화면에서는 권한 목록 및 지정된 경로의 권한 유형 외에도 아래에 표시된 것처럼 세분화된 액세스 제어에 대한 제한을 추가할 수 있습니다.

![](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>각 제한 사항의 의미에 대한 자세한 내용은 [이 페이지를](/help/sites-administering/user-group-ac-admin.md#restrictions)참조하십시오.

제한 유형을 선택하고 값을 입력한 다음 **+** 아이콘을 눌러 아래와 같이 제한을 추가할 수 있습니다. ![](assets/sapte-1.png) ![](assets/opt-1.png)

새 ACE는 아래와 같이 액세스 제어 목록에 반영됩니다. 이 `jcr:write` 권한은 위에 `jcr:removeNode` 추가되었지만 아래에 그에 따라 표시되지 않는 집계 권한입니다 `jcr:write`.

### ACE 편집 {#editing-aces}

액세스 제어 항목은 주도자를 선택하고 편집할 ACE를 선택하여 편집할 수 있습니다.

예를 들어 오른쪽에 있는 연필 아이콘을 클릭하여 **dam 사용자를** 위한 아래 항목을 편집할 수 있습니다.

![](assets/image2019-3-21_0-35-39.png)

편집 화면은 구성된 ACE를 미리 선택한 상태로 표시되며, 이 ACE 옆에 있는 상호 아이콘을 클릭하여 삭제할 수 있고, 아래에 표시된 것처럼 지정된 경로에 대해 새 권한을 추가할 수 있습니다.

![](assets/noua-1.png)

여기서는 해당 경로에서 `addChildNodes` DAM 사용자에 **** 대한 권한을 추가합니다.

![](assets/image2019-3-21_0-45-35.png)

오른쪽 위에 있는 저장 **단추를 클릭하여** 변경 사항을 저장할 수 있으며, 변경 사항은 아래와 같이 **dam-users **에 대한 새 권한에 반영됩니다.

![](assets/zece-1.png)

### ACE 삭제 {#deleting-aces}

액세스 제어 항목을 삭제하여 특정 경로에서 주체에게 주어진 모든 권한을 제거할 수 있습니다. ACE 옆에 있는 X 아이콘을 사용하여 아래와 같이 삭제할 수 있습니다.

![](assets/image2019-3-21_0-53-19.png) ![](assets/unspe.png)

### 클래식 UI 권한 조합 {#classic-ui-privilege-combinations}

새 권한 UI는 부여된 정확한 기본 권한을 실제로 반영하지 않은 사전 정의된 조합 대신 기본 권한 집합을 명시적으로 사용합니다.

정확히 구성 중인 내용에 대한 혼동을 초래했습니다. 다음 표에는 클래식 UI에서 권한을 구성하는 실제 권한에 대한 권한 조합 간의 매핑이 나열되어 있습니다.

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

