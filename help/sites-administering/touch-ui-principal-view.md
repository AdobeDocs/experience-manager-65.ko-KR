---
title: 권한 관리를 위한 주요 보기
description: 권한 관리를 용이하게 하는 새로운 Touch UI 인터페이스에 대해 알아봅니다.
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 8adc566113beedc408698dccc3a4c072349af5dc
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 84%

---


# 권한 관리를 위한 주요 보기{#principal-view-for-permissions-management}

## 개요 {#overview}

AEM 6.5에는 사용자 및 그룹에 대한 권한 관리가 도입되었습니다. 주요 기능은 기존 UI와 동일하지만, 사용자 친화성과 효율성이 향상되었습니다.

## 사용 방법 {#how-to-use}

### UI에 액세스 {#accessing-the-ui}

새로운 UI 기반 권한 관리 기능은 아래와 같이 보안 섹션의 권한 카드에서 액세스할 수 있습니다.

![권한 관리 UI](assets/screen_shot_2019-03-17at63333pm.png)

새로운 보기를 사용하면 권한이 명시적으로 부여된 모든 경로에서 주어진 주체에 대한 전체 권한 및 제한 세트를 한눈에 확인할 수 있습니다. 이제 고급 권한 및 제한을 관리하기 위해

CRXDE로 이동할 필요가 없습니다. 모든 기능이 동일한 보기에 통합되었습니다. 보기의 기본값은 그룹 &quot;everyone&quot;입니다.

![모든 사용자 그룹 보기](assets/unu-1.png)

사용자는 필터를 사용하여 **사용자**, **그룹** 또는 **전체** 등 주체 유형을 선택하고, 원하는 주체를 검색할 수 있습니다&#x200B;**.**

![주체 유형 검색](assets/image2019-3-20_23-52-51.png)

### 주체에 대한 권한 보기 {#viewing-permissions-for-a-principal}

왼쪽 프레임에서 사용자는 아래로 스크롤하여 원하는 주체를 찾거나, 아래에 표시된 대로 선택한 필터를 기준으로 그룹이나 사용자를 검색할 수 있습니다.

![주체에 대한 권한 보기](assets/doi-1.png)

이름을 클릭하면 오른쪽에 할당된 권한이 표시됩니다. 권한 패널에는 특정 경로에 대한 액세스 제어 항목 목록과 구성된 제한 사항이 표시됩니다.

![ACL(액세스 제어 목록) 보기](assets/trei-1.png)

### 주체에 대한 새 액세스 제어 항목 추가 {#adding-new-access-control-entry-for-a-principal}

새 권한은 액세스 제어 항목을 추가하여 부여할 수 있습니다. ACE 추가 버튼을 클릭하면 됩니다.

![주체에 대한 새 ACL 추가](assets/patru.png)

이렇게 하면 아래에 표시된 창이 표시되고, 다음 단계에서는 권한을 구성해야 하는 경로를 선택합니다.

![권한 경로 구성](assets/cinci-1.png)

여기에서는 **dam-users**&#x200B;에 대한 권한을 구성할 수 있는 경로가 선택됩니다.

![dam-users를 위한 예제 구성](assets/sase-1.png)

경로를 선택하면 워크플로가 이 화면으로 돌아오며, 여기에서 사용자는 아래에 표시된 대로 사용 가능한 네임스페이스(`jcr`, `rep`, `crx` 등)에서 하나 이상의 권한을 선택할 수 있습니다.

텍스트 필드에서 권한을 검색한 후 목록에서 선택하여 권한을 추가할 수 있습니다.

>[!NOTE]
>
>권한 및 설명의 전체 목록은 [사용자, 그룹 및 액세스 권한 관리](/help/sites-administering/user-group-ac-admin.md#access-right-management)를 참조하십시오.

![지정된 경로에 대한 검색 권한입니다.](assets/image2019-3-21_0-5-47.png) ![수직 열에서 선택한 경로에 표시된 대로 &#39;dam-users&#39;에 대한 새 항목을 추가하십시오.](assets/image2019-3-21_0-6-53.png)

권한 목록을 선택한 후 사용자는 아래에 표시된 대로 ‘거부’ 또는 ‘허용’ 중 권한 유형을 지정할 수 있습니다.

![권한 선택](assets/screen_shot_2019-03-17at63938pm.png) ![권한 선택](assets/screen_shot_2019-03-17at63947pm.png)

### 제한 사용 {#using-restrictions}

이 화면에서는 지정된 경로에 대한 권한 목록 및 권한 유형 외에도 아래와 같이 세분화된 액세스 제어에 대한 제한을 추가할 수 있습니다.

![제한 추가](assets/image2019-3-21_1-4-14.png):

>[!NOTE]
>
>각 제한 사항이 의미하는 바에 대한 자세한 내용은 [Jackrabbit Oak 설명서](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)를 참조하십시오.

제한을 추가하려면 제한 유형을 선택하고 값을 입력한 뒤 **+** 아이콘을 클릭합니다.

![제한 유형 추가](assets/sapte-1.png) ![제한 유형 추가](assets/opt-1.png)

새로운 ACE는 아래와 같이 액세스 제어 목록에 반영됩니다. `jcr:write`은(는) 위에 추가된 `jcr:removeNode`을(를) 포함하는 집계 권한이지만 `jcr:write`에서 다루므로 아래에 표시되지 않습니다.

### ACE 편집 {#editing-aces}

액세스 제어 항목은 주체를 선택한 다음 편집하려는 ACE를 선택하여 편집할 수 있습니다.

예를 들어, 여기에서 오른쪽에 있는 연필 아이콘을 클릭하여 **dam-users**&#x200B;에 대한 아래 항목을 편집할 수 있습니다.

![제한 추가](assets/image2019-3-21_0-35-39.png):

편집 화면에는 구성된 ACE가 미리 선택된 상태로 표시됩니다. 해당 항목 옆의 십자 아이콘을 클릭하여 삭제할 수 있으며, 아래에 표시된 대로 지정된 경로에 새로운 권한을 추가할 수도 있습니다.

![항목 편집](assets/noua-1.png)

여기에서는 지정된 경로에 대한 **dam-users**&#x200B;에 `addChildNodes` 권한이 추가됩니다.

![권한 추가](assets/image2019-3-21_0-45-35.png)

변경 사항은 오른쪽 상단의 **저장** 단추를 클릭하여 저장할 수 있으며 아래와 같이 **dam-users**&#x200B;에 대한 새 권한에 반영됩니다.

![변경 내용 저장](assets/zece-1.png)

### ACE 삭제 {#deleting-aces}

액세스 제어 항목을 삭제하면 특정 경로에 대해 주체에 부여된 모든 권한이 제거됩니다. 아래와 같이 ACE 옆에 있는 X 아이콘을 클릭하여 해당 ACE를 삭제할 수 있습니다.

![ACE 삭제](assets/image2019-3-21_0-53-19.png) ![ACE 삭제](assets/unspe.png)

### 클래식 UI 권한 조합 {#classic-ui-privilege-combinations}

새로운 권한 UI는 실제로 부여된 하위 권한을 정확하게 반영하지 않는 미리 정의된 조합 대신 기본 권한 집합을 명시적으로 사용합니다.

이전에는 정확히 어떤 권한이 구성되고 있는지 혼란이 발생했습니다. 다음 표에는 클래식 UI의 권한 조합과 이를 구성하는 실제 권한 간의 매핑이 나와 있습니다.

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
