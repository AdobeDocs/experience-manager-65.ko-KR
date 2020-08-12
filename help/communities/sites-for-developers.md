---
title: 커뮤니티 사이트 필수
seo-title: 커뮤니티 사이트 필수
description: 커뮤니티 사이트 내보내기 및 삭제 및 사용자 정의 사이트 템플릿 만들기
seo-description: 커뮤니티 사이트 내보내기 및 삭제 및 사용자 정의 사이트 템플릿 만들기
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
translation-type: tm+mt
source-git-commit: e49acbc042d84ae970058b4e99ab6f980866db5a
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---


# 커뮤니티 사이트 필수 {#community-site-essentials}

## 사용자 지정 사이트 템플릿 {#custom-site-template}

사용자 지정 사이트 템플릿은 커뮤니티 사이트의 각 언어 복사본에 대해 별도로 지정할 수 있습니다.

이렇게 하려면:

* 사용자 지정 템플릿을 만듭니다.
* 기본 사이트 템플릿 경로를 오버레이합니다.
* 오버레이 경로에 사용자 지정 템플릿을 추가합니다.
* 노드에 속성을 추가하여 사용자 지정 템플릿 `page-template` 을 `configuration` 지정합니다.

**기본 템플릿**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**오버레이 경로의 사용자 지정 템플릿**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**속성**:page-template

**유형**:문자열

**값**: `template-name` (확장 없음)

**구성 노드**:

`/content/community site path/lang/configuration`

예를 들어,`/content/sites/engage/en/configuration`

>[!NOTE]
>
>오버레이된 경로의 모든 노드는 유형이어야 합니다 `Folder`.


>[!CAUTION]
>
>사용자 지정 템플릿에 sitepage.hbs라는 이름이 *지정되면*&#x200B;모든 커뮤니티 사이트가 사용자 지정됩니다.


### 사용자 지정 사이트 템플릿 예 {#custom-site-template-example}

예를 들어 `vertical-sitepage.hbs` 는 메뉴 링크가 배너 아래가 가로로 아니라 페이지의 왼쪽에 세로로 배치되는 사이트 템플릿입니다.

[파일](assets/vertical-sitepage.hbs)가져오기 사용자 지정 사이트 템플릿을 오버레이 폴더에 배치합니다.

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

구성 노드에 속성을 추가하여 사용자 지정 템플릿 `page-template` 을 식별합니다.

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

모두 **저장하고 사용자** 지정 코드를 모든 AEM 인스턴스에 복제하십시오(사용자 지정 코드는 콘솔에서 커뮤니티 사이트 컨텐츠가 게시될 때 포함되지 않음).

사용자 지정 코드를 복제하는 데 권장되는 방법은 패키지를 [만들어](../../help/sites-administering/package-manager.md#creating-a-new-package) 모든 인스턴스에 배포하는 것입니다.

## 커뮤니티 사이트 내보내기 {#exporting-a-community-site}

커뮤니티 사이트가 만들어지면 사이트를 패키지 관리자에 저장된 AEM 패키지로 내보낼 수 있으며 다운로드 및 업로드할 수 있습니다.

커뮤니티 사이트 콘솔에서 [사용할 수 있습니다](sites-console.md#exporting-the-site).

UGC 및 사용자 지정 코드는 커뮤니티 사이트 패키지에 포함되지 않습니다.

UGC를 내보내려면 GitHub에서 사용할 수 있는 오픈 소스 마이그레이션 도구인 [AEM Communities UGC 마이그레이션](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)도구를 사용하십시오.

## 커뮤니티 사이트 삭제 {#deleting-a-community-site}

AEM Communities 6.3 서비스 팩 1의 경우 사이트 삭제 아이콘이 커뮤니티 **** > **[!UICONTROL 사이트 콘솔에서 커뮤니티 사이트 위로 마우스를 가져가면]** 나타납니다. 개발 중에 커뮤니티 사이트를 삭제하고 새로 시작하려면 이 기능을 사용할 수 있습니다. 커뮤니티 사이트를 삭제하면 해당 사이트와 연관된 다음 항목이 제거됩니다.

* [UGC](#user-generated-content)
* [사용자 그룹](#community-user-groups)
* [자산](#enablement-assets)
* [데이터베이스 레코드](#database-records)

### 커뮤니티 고유 사이트 ID {#community-unique-site-id}

CRXDE를 사용하여 커뮤니티 사이트와 연관된 고유 사이트 ID를 식별하려면:

* 사이트의 언어 루트(예: )로 이동합니다 `/content/sites/*<site name>*/en/rep:policy`.

* 이 형식 `allow<#>` 으로 노드를 `rep:principalName` 찾습니다 `rep:principalName = *community-enable-nrh9h-members*`.

* 사이트 ID는 `rep:principalName`

   예를 들어 `rep:principalName = community-enable-nrh9h-members`

   * **site name** = *enable*
   * **site ID** = *nrh9h*
   * **고유 사이트 ID** = *enable-nrh9h*

### 사용자 생성 콘텐츠 {#user-generated-content}

Github에서 communities-srp-tools 프로젝트를 얻습니다.

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

여기에는 모든 SRP에서 모든 UGC를 삭제하는 서블릿이 포함됩니다.

모든 UGC는 제거되거나 특정 사이트에 대해 제거될 수 있습니다. 예:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

이렇게 하면 사용자가 생성한 컨텐츠(게시에 입력됨)만 제거되고 컨텐츠(작성자에 입력됨)는 작성되지 않습니다. 따라서 [그림자 노드는](srp.md#shadownodes) 영향을 받지 않습니다.

### 커뮤니티 사용자 그룹 {#community-user-groups}

모든 작성자 및 게시 인스턴스의 [보안 콘솔에서](../../help/sites-administering/security.md)다음과 같은 [사용자 그룹을 찾아](users.md) 제거합니다.

* 미리 수정한 날짜 `community`
* 뒤에 [고유 사이트 ID 표시](#community-unique-site-id)

예, `community-engage-x0e11-members`.

### 활성 에셋 {#enablement-assets}

주 콘솔에서:

* Select **[!UICONTROL Assets]**.
* 선택 **[!UICONTROL 모드를]** 입력합니다.
* 고유한 사이트 ID로 명명된 [폴더를 선택합니다](#community-unique-site-id).
* [ **[!UICONTROL 삭제]** ]를 선택합니다(자세히... **[!UICONTROL 에서 선택해야 할 수 있음]**).

### 데이터베이스 레코드 {#database-records}

특정 활성 커뮤니티 사이트에 대한 데이터베이스 항목을 선택적으로 삭제하는 도구는 없습니다.

모든 커뮤니티 사이트가 삭제되는 경우 MySQL Workbench를 사용하여 활성 DB와 표준 엔진을 삭제합니다.
