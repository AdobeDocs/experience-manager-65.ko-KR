---
title: 커뮤니티 사이트 기본 사항
seo-title: Community Site Essentials
description: 커뮤니티 사이트 내보내기 및 삭제, 사용자 지정 사이트 템플릿 만들기
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# 커뮤니티 사이트 기본 사항 {#community-site-essentials}

## 사용자 지정 사이트 템플릿 {#custom-site-template}

사용자 지정 사이트 템플릿은 커뮤니티 사이트의 각 언어 사본에 대해 별도로 지정할 수 있습니다.

방법은 다음과 같습니다.

* 사용자 지정 템플릿을 만듭니다.
* 기본 사이트 템플릿 경로를 오버레이합니다.
* 사용자 지정 템플릿을 오버레이 경로에 추가합니다.
* 을(를) 추가하여 사용자 지정 템플릿 지정 `page-template` 에 대한 속성 `configuration` 노드.

**기본 템플릿**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**오버레이 경로의 사용자 정의 템플릿**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**속성**: page-template

**유형**: 문자열

**값**: `template-name` (확장 없음)

**구성 노드**:

`/content/community site path/lang/configuration`

예를 들어`/content/sites/engage/en/configuration`

>[!NOTE]
>
>오버레이된 경로의 모든 노드는 유형만 사용해야 합니다. `Folder`.

>[!CAUTION]
>
>사용자 지정 템플릿에 이름이 지정된 경우 *sitepage.hbs*&#x200B;를 입력하면 모든 커뮤니티 사이트가 사용자 지정됩니다.

### 사용자 지정 사이트 템플릿 예 {#custom-site-template-example}

예를 들어, `vertical-sitepage.hbs` 는 배너 수평 아래가 아닌 페이지 왼쪽 수직 아래로 메뉴 링크를 배치하는 사이트 템플릿입니다.

[파일 가져오기](assets/vertical-sitepage.hbs)
사용자 지정 사이트 템플릿을 오버레이 폴더에 넣습니다.

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

을(를) 추가하여 사용자 지정 템플릿 식별 `page-template` 속성을 구성 노드에 추가합니다.

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

다음을 확인합니다. **모두 저장** 모든 AEM 인스턴스에 사용자 지정 코드를 복제합니다(커뮤니티 사이트 콘텐츠가 콘솔에서 게시되는 경우 사용자 지정 코드는 포함되지 않음).

사용자 지정 코드를 복제하는 데 권장되는 방법은 다음과 같습니다. [패키지 만들기](../../help/sites-administering/package-manager.md#creating-a-new-package) 모든 인스턴스에 배포합니다.

## 커뮤니티 사이트 내보내기 {#exporting-a-community-site}

커뮤니티 사이트가 생성되면 패키지 관리자에 저장된 AEM 패키지로 사이트를 내보내고 다운로드 및 업로드할 수 있습니다.

다음에서 사용할 수 있습니다. [커뮤니티 사이트 콘솔](sites-console.md#exporting-the-site).

UGC 및 사용자 지정 코드는 커뮤니티 사이트 패키지에 포함되지 않습니다.

UGC를 내보내려면 [AEM Communities UGC 마이그레이션 도구](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration): GitHub에서 사용할 수 있는 오픈 소스 마이그레이션 도구입니다.

## 커뮤니티 사이트 삭제 {#deleting-a-community-site}

AEM Communities 6.3 서비스 팩 1부터 사이트 삭제 아이콘이에서 커뮤니티 사이트 위로 마우스를 가져가면 표시됩니다. **[!UICONTROL 커뮤니티]** > **[!UICONTROL 사이트]** 콘솔. 개발 중에 커뮤니티 사이트를 삭제하고 새로 시작하려는 경우 이 기능을 사용할 수 있습니다. 커뮤니티 사이트를 삭제하면 해당 사이트와 연결된 다음 항목이 제거됩니다.

* [UGC](#user-generated-content)
* [사용자 그룹](#community-user-groups)
* [Assets](#enablement-assets)
* [데이터베이스 레코드](#database-records)

### 커뮤니티 고유 사이트 ID {#community-unique-site-id}

CRXDE를 사용하여 커뮤니티 사이트와 연결된 고유한 사이트 ID를 식별하려면 다음을 수행하십시오.

* 다음과 같이 사이트의 언어 루트로 이동합니다. `/content/sites/*<site name>*/en/rep:policy`.

* 다음 찾기 `allow<#>` 가 있는 노드 `rep:principalName` 이 형식으로 `rep:principalName = *community-enable-nrh9h-members*`.

* 사이트 ID는 의 세 번째 구성 요소입니다 `rep:principalName`

   예를 들어 다음과 같습니다. `rep:principalName = community-enable-nrh9h-members`

   * **사이트 이름** = *활성화*
   * **사이트 ID** = *nrh9h*
   * **고유 사이트 ID** = *enable-nrh9h*

### 사용자 생성 콘텐츠 {#user-generated-content}

Github에서 communities-srp-tools 프로젝트 가져오기:

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

여기에는 SRP에서 모든 UGC를 삭제하는 서블릿이 포함되어 있습니다.

모든 UGC를 제거하거나 특정 사이트에 대해 다음을 수행할 수 있습니다.

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

이렇게 하면 사용자가 생성한 콘텐츠(게시 시 입력)만 제거되고 작성된 콘텐츠(작성 시 입력)는 제거되지 않습니다. 따라서 [그림자 노드](srp.md#shadownodes) 영향을 받지 않습니다.

### 커뮤니티 사용자 그룹 {#community-user-groups}

모든 작성자 및 게시 인스턴스에서 [보안 콘솔](../../help/sites-administering/security.md), 를 찾아 제거합니다. [사용자 그룹](users.md) 즉,

* 접두사 `community`
* 뒤에 오는 [고유 사이트 id](#community-unique-site-id)

(예: `community-engage-x0e11-members`)

### 지원 에셋 {#enablement-assets}

메인 콘솔에서:

* 선택 **[!UICONTROL 에셋]**.
* 입력 **[!UICONTROL 선택]** 모드.
* 이름이 인 폴더 선택 [고유 사이트 ID](#community-unique-site-id).
* 선택 **[!UICONTROL 삭제]** (다음 중에서 선택해야 할 수 있음) **[!UICONTROL 자세히...]**).

### 데이터베이스 레코드 {#database-records}

특정 지원 커뮤니티 사이트에 대한 데이터베이스 항목을 선택적으로 삭제하는 도구가 없습니다.

모든 커뮤니티 사이트를 삭제하는 경우 MySQL Workbench를 사용하여 enablementdb 및 scormenginedb를 삭제합니다.
