---
title: 서신 관리 | 사용자 데이터 처리
seo-title: 서신 관리 | 사용자 데이터 처리
description: 서신 관리 | 사용자 데이터 처리
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: Admin
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# 서신 관리 | 사용자 데이터 처리 {#correspondence-management-handling-user-data}

AEM Forms 서신 관리를 사용하면 안전하고 개인화된 고객 커뮤니케이션을 생성, 관리 및 간소화할 수 있습니다. 비즈니스 사용자가 사전 승인된 컨텐츠 블록과 미디어 요소를 사용하여 메시지를 만들 수 있도록 직관적인 사용자 인터페이스를 제공합니다. 서신 만들기에 대한 자세한 내용은 [서신 만들기](/help/forms/using/create-correspondence.md)를 참조하십시오.

비즈니스 사용자 또는 에이전트가 서신을 초안으로 저장하거나 제출하면 편지 인스턴스가 AEM 저장소에 저장됩니다. 편지 인스턴스에는 서신 데이터 및 메타데이터가 포함됩니다.

>[!NOTE]
>
>AEM 6.5 Forms에서는 서신 관리를 즉시 사용할 수 없습니다. 이전 AEM Forms 버전에서 업그레이드하는 경우 호환성 패키지를 설치하고 서신 관리 자산을 마이그레이션하여 AEM 6.5 Forms에서 계속 사용합니다. 자세한 내용은 [호환성 패키지](/help/forms/using/compatibility-package.md)를 참조하십시오.

## 사용자 데이터 및 데이터 저장소 {#data}

서신 관리는 게시 인스턴스가 편지 인스턴스를 관리하도록 구성된 경우에만 AEM 저장소에 초안 및 제출된 편지에 대한 데이터를 저장합니다. 구성에 대한 자세한 내용은 [서신 관리 구성 속성](/help/forms/using/cm-configuration-properties.md)을 참조하십시오.

AEM 배포에 대해 구성된 데이터 저장소 지속성에 따라 초안 및 제출된 서신 데이터는 다음 위치에 저장됩니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>지속성 유형</strong></p> </td>
   <td><p><strong>데이터 저장소</strong></p> </td>
   <td><p><strong>위치</strong></p> </td>
  </tr>
  <tr>
   <td><p>기본값</p> </td>
   <td><p>역방향 복제 구성에 지정된 게시 인스턴스 및 작성자 인스턴스의 AEM 저장소</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>원격</p> </td>
   <td><p>원격 처리 작성자 인스턴스의 AEM 저장소</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

위에 지정된 AEM 저장소 위치에서 다음을 수행합니다.

* `[yyyy]/[mm]/[dd]` 은 편지 인스턴스가 생성된 날짜를 기반으로 하는 노드 구조입니다
* `[node-id]` 는 문자가 포함된 폴더에 지정된 ID입니다
* `[letter-instance-name]` 은 편지를 저장하거나 제출할 때 지정된 이름입니다

[letter-instance-name] 노드 아래에 다음 노드 구조가 생성되고 각 편지 인스턴스에 대한 데이터가 AEM 저장소에 저장됩니다.

| 노드 | 설명 |
|---|---|
| `extendedProperties` | 편지 인스턴스의 메타데이터 속성을 저장합니다. |
| `dataXML` | 서신 데이터가 포함된 다운로드 가능한 dataXML 파일을 이진 형식으로 저장합니다. |
| `processedXDP` | 제출된 편지를 만드는 데 사용되는 XDP 템플릿의 세부 정보를 포함합니다. 이 노드는 제출된 대상에 대해서만 만들어집니다. |
| `submittedLetter` | 제출된 편지 데이터를 다운로드 가능한 이진 형식으로 저장합니다. 이 노드는 제출된 대상에 대해서만 만들어집니다. |

## 사용자 데이터 액세스 및 삭제 {#access-and-delete-user-data}

구성된 데이터 저장소에서 초안 및 제출된 서신 데이터에 액세스할 수 있으며, 필요한 경우 삭제할 수 있습니다.

### 사용자 데이터 액세스 {#access-user-data}

서신 관리는 초안 및 제출된 편지 인스턴스를 찾고 액세스하는 데 사용할 수 있는 API를 제공합니다. API를 사용하여 편지 인스턴스 ID 또는 서신을 저장하거나 제출한 사용자를 사용하여 편지 인스턴스를 찾고 열 수 있습니다. 자세한 내용은 [API를 참조하여 문자 인스턴스](/help/forms/using/cm-apis-to-access-letter-instances.md)에 액세스하십시오.

또는 CRX DELite를 사용하여 AEM 저장소의 편지 인스턴스로 이동할 수 있습니다. 저장된 데이터 및 저장소 위치에 대한 자세한 내용은 [사용자 데이터 및 데이터 저장소](/help/forms/using/correspondence-management-handling-user-data.md#data)를 참조하십시오.

### 사용자 데이터 삭제 {#delete-user-data}

특정 사용자의 데이터가 포함된 편지 인스턴스를 찾으려면 다음을 수행할 수 있습니다.

* 편지 인스턴스 이름 또는 초안을 저장하거나 서신을 제출한 사용자를 알고 있는 경우 서신 관리 API를 사용합니다
* 이메일 ID 또는 이름과 같은 개인 식별 정보를 사용하여 AEM 저장소 검색을 사용하여 정보가 저장된 노드를 찾습니다

초안 및 제출된 서신 데이터를 AEM 시스템에서 완전히 삭제하려면 적용 가능한 모든 AEM 인스턴스에서 편지 인스턴스 노드를 수동으로 삭제해야 합니다.
