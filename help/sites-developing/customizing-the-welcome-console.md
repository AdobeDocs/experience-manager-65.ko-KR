---
title: 시작 콘솔 사용자 지정(클래식 UI)
seo-title: Customizing the Welcome Console (Classic UI)
description: 시작 콘솔에서는 AEM 내의 다양한 콘솔 및 기능에 대한 링크 목록을 제공합니다
seo-description: The Welcome console provides a list of links to the various consoles and functionality within AEM
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
exl-id: 9e171b62-8efb-4143-a202-ba6555658d4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 12%

---

# 시작 콘솔 사용자 지정(클래식 UI){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>이 페이지에서는 기존 UI에 대해 다룹니다.
>
>자세한 내용은 [콘솔 사용자 지정](/help/sites-developing/customizing-consoles-touch.md) 표준 터치 지원 UI에 대한 자세한 내용은.

시작 콘솔에서는 AEM 내의 다양한 콘솔 및 기능에 대한 링크 목록을 제공합니다.

![cq_welcomeesscreen](assets/cq_welcomescreen.png)

표시되는 링크를 구성할 수 있습니다. 특정 사용자 및/또는 그룹에 대해 정의할 수 있습니다. 수행할 작업은 대상 유형(해당 작업이 있는 콘솔의 섹션과 상관 관계가 있음)에 따라 달라집니다.

* [기본 콘솔](#links-in-main-console-left-pane) - 기본 콘솔의 링크(왼쪽 창)
* [리소스, 설명서 및 참조, 기능](#links-in-sidebar-right-pane) - 사이드바의 링크(오른쪽 창)

## 기본 콘솔의 링크(왼쪽 창) {#links-in-main-console-left-pane}

여기에는 AEM의 기본 콘솔이 나열됩니다.

![cq_welcomeescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### 기본 콘솔 링크가 표시되는지 여부 구성 {#configuring-whether-main-console-links-are-visible}

노드 수준 권한은 링크를 볼 수 있는지 여부를 결정합니다. 해당 노드는 다음과 같습니다.

* **웹 사이트:** `/libs/wcm/core/content/siteadmin`

* **디지털 에셋:** `/libs/wcm/core/content/damadmin`

* **커뮤니티:** `/libs/collab/core/content/admin`

* **캠페인:** `/libs/mcm/content/admin`

* **받은 편지함:** `/libs/cq/workflow/content/inbox`

* **사용자:** `/libs/cq/security/content/admin`

* **도구:** `/libs/wcm/core/content/misc`

* **태깅:** `/libs/cq/tagging/content/tagadmin`

예:

* 에 대한 액세스를 제한하려면 **도구**&#x200B;에서 읽기 액세스 권한을 제거합니다.

   `/libs/wcm/core/content/misc`

자세한 내용은 [보안 섹션](/help/sites-administering/security.md) 를 참조하십시오.

### 사이드바의 링크(오른쪽 창) {#links-in-sidebar-right-pane}

![cq_welcomeescreensidebar](assets/cq_welcomescreensidebar.png)

이러한 링크는 *및* 다음 경로 아래의 노드에 대한 읽기 액세스 권한:

`/libs/cq/core/content/welcome`

기본적으로 세 개의 섹션(약간 간격)이 제공됩니다.

<table>
 <tbody>
  <tr>
   <td><strong>리소스</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> 클라우드 서비스</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> 워크플로</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> 작업 관리</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> 복제</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> 보고서</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> 발행물</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> 원고</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>설명서 및 참조</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> 설명서</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> 개발자 리소스</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>기능</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> 패키지</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> 패키지 공유</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> 클러스터링</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> 백업</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> 웹 콘솔<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> 웹 콘솔 상태 덤프<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### 사이드바 링크가 표시되는지 여부 구성 {#configuring-whether-sidebar-links-are-visible}

링크를 나타내는 노드에 대한 읽기 액세스를 제거하여 특정 사용자 또는 그룹에서 링크를 숨길 수 있습니다.

* 리소스 - 액세스 권한 제거:

   `/libs/cq/core/content/welcome/resources/<link-target>`

* 문서 - 액세스 권한 제거:

   `/libs/cq/core/content/welcome/docs/<link-target>`

* 기능 - 액세스 권한 제거:

   `/libs/cq/core/content/welcome/features/<link-target>`

예:

* 링크를 제거하려면 **보고서**&#x200B;에서 읽기 액세스 권한을 제거합니다.

   `/libs/cq/core/content/welcome/resources/reports`

* 링크를 제거하려면 **패키지**&#x200B;에서 읽기 액세스 권한을 제거합니다.

   `/libs/cq/core/content/welcome/features/packages`

자세한 내용은 [보안 섹션](/help/sites-administering/security.md) 를 참조하십시오.

### 링크 선택 메커니즘 {#link-selection-mechanism}

in `/libs/cq/core/components/welcome/welcome.jsp` 사용 [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html): 속성이 있는 노드에 대해 쿼리를 실행합니다.

* `jcr:mixinTypes` 값 사용: `cq:Console`

>[!NOTE]
>
>다음 쿼리를 실행하여 기존 목록을 확인합니다.
>
>* `select * from cq:Console`
>


사용자 또는 그룹에 mixin이 있는 노드에 대한 읽기 권한이 없는 경우 `cq:Console`로 설정되면 해당 노드는 `ConsoleUtil` 검색하므로 콘솔에 나열되지 않습니다.

### 사용자 지정 항목 추가 {#adding-a-custom-item}

다음 [링크 선택 메커니즘](#link-selection-mechanism) 링크 목록에 사용자 지정 항목을 추가하는 데 사용할 수 있습니다.

을(를) 추가하여 목록에 사용자 지정 항목을 추가합니다. `cq:Console` 위젯 또는 리소스에 혼합합니다. 이 작업은 속성을 정의하여 수행됩니다.

* `jcr:mixinTypes` 값 사용: `cq:Console`
