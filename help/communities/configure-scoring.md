---
title: 채점 및 배지 핵심 사항
description: Adobe Experience Manager Communities 점수 및 배지 기능이 커뮤니티 구성원을 식별하고 보상하는 방법에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 채점 및 배지 핵심 사항 {#scoring-and-badges-essentials}

AEM Communities 점수 및 배지 기능은 커뮤니티 구성원을 식별하고 보상합니다.

기능 설정에 대한 세부 사항은에서 설명합니다.

* [커뮤니티 점수 및 배지](/help/communities/implementing-scoring.md)

이 페이지에는 추가 기술 세부 정보 가 포함되어 있습니다.

* [배지를 이미지 또는 텍스트로 표시](#displaying-badges)하는 방법
* 광범위한 [디버그 로깅](#debug-log-for-scoring-and-badging)을 켜는 방법
* 채점 및 배지와 관련된 [UGC에 액세스](#ugc-for-scoring-and-badging)하는 방법

>[!CAUTION]
>
>CRXDE Lite에 표시되는 구현 구조는 변경될 수 있습니다.

## 배지 표시 {#displaying-badges}

배지가 텍스트 또는 이미지로 표시되는지 여부는 HBS 템플릿의 클라이언트측에서 제어됩니다.

예를 들어 `/libs/social/forum/components/hbs/topic/list-item.hbs`에서 `this.isAssigned`을(를) 검색합니다.

```
{{#each author.badges}}

  {{#if this.isAssigned}}

    <div class="scf-badge-text">

      {{this.title}}

    </div>

  {{/if}}

{{/each}}

{{#each author.badges}}

  {{#unless this.isAssigned}}

    <img class="scf-badge-image" alt="{{this.title}}" title="{{this.title}}" src="{{this.imageUrl}}" />

  {{/unless}}

{{/each}}
```

true인 경우 `isAssigned`은(는) 배지가 역할에 할당되었음을 나타내며 배지는 텍스트로 표시되어야 합니다.

false인 경우 `isAssigned`은(는) 배지가 획득한 점수에 대해 부여되었으며 배지가 이미지로 표시되어야 함을 나타냅니다.

이 비헤이비어에 대한 모든 변경은 사용자 지정된 스크립트(오버라이드 또는 오버레이)에서 수행해야 합니다. [클라이언트측 사용자 지정](/help/communities/client-customize.md)을 참조하십시오.

## 점수 및 배지 디버그 로그 {#debug-log-for-scoring-and-badging}

채점 및 배지를 디버깅하기 위해 사용자 지정 로그 파일을 설정할 수 있습니다. 이 로그 파일의 내용은 기능에 문제가 발생하는 경우 고객 지원 센터에 제공될 수 있습니다.

자세한 지침은 [사용자 지정 로그 파일 만들기](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)를 참조하세요.

slinglog 파일을 빠르게 설정하려면:

1. 예를 들어 **Adobe Experience Manager 웹 콘솔 로그 지원**&#x200B;에 액세스합니다

   * https://localhost:4502/system/console/slinglog

1. **새 로거 추가** 선택

   1. **로그 수준**&#x200B;에 대해 `DEBUG` 선택

   1. **로그 파일**&#x200B;의 이름을 입력하십시오. 예:

      * logs/scoring-debug.log

   1. 두 개의 **Logger**(클래스) 항목 입력(`+` 아이콘 사용)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`

   1. **저장** 선택

![debug-scoring-log](assets/debug-scoring-log.png)

로그 항목을 보려면 다음 작업을 수행하십시오.

* 웹 콘솔에서

   * **상태** 메뉴 아래
   * **로그 파일** 선택
   * 로그 파일 이름 검색(예: `scoring-debug`)

* 서버의 로컬 디스크에서

   * 로그 파일이 &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log에 있습니다.

   * 예, `.../crx-quickstart/logs/scoring-debug.log`

![scoring-log](assets/scoring-log.png)

## 채점 및 배지를 위한 UGC {#ugc-for-scoring-and-badging}

선택된 SRP가 JSRP 또는 MSRP이지만 ASRP가 아닌 경우 채점 및 배지와 관련된 UGC를 볼 수 있습니다. (이 용어에 익숙하지 않은 경우 [커뮤니티 콘텐츠 저장소](/help/communities/working-with-srp.md) 및 [저장소 리소스 공급자 개요](/help/communities/srp.md)를 참조하십시오.)

UGC는 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)을(를) 사용하여 쉽게 액세스할 수 있으므로 채점 및 배지 데이터에 액세스하는 설명은 JSRP를 사용합니다.

**작성자의 JSRP**: 작성자 환경에서 테스트하면 작성자 환경에서만 볼 수 있는 UGC가 생성됩니다.

**게시의 JSRP**: 마찬가지로 게시 환경에서 테스트하는 경우 게시 인스턴스에 대한 관리자 권한으로 CRXDE Lite에 액세스해야 합니다. 게시 인스턴스가 [프로덕션 모드](/help/sites-administering/production-ready.md)(nosamplecontent 실행 모드)에서 실행 중인 경우 [CRXDE Lite을 활성화](/help/sites-administering/enabling-crxde-lite.md)해야 합니다.

JSRP에서 UGC의 기본 위치는 `/content/usergenerated/asi/jcr/`입니다.

### 채점 및 배지 API {#scoring-and-badging-apis}

다음 API를 사용할 수 있습니다.

* 6.3의 [com.adobe.cq.social.scoring.api](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko)
* 6.3의 [com.adobe.cq.social.badging.api](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko)

설치된 기능 팩의 최신 Javadocs는 Adobe 저장소에서 개발자가 사용할 수 있습니다. [커뮤니티용 Maven 사용: Javadocs](/help/communities/maven.md#javadocs)을 참조하십시오.

**저장소에서 UGC의 위치 및 형식은 경고 없이 변경될 수 있습니다**.

### 예제 설정 {#example-setup}

저장소 데이터의 스크린샷은 두 개의 다른 AEM 사이트에서 포럼에 대한 점수 및 배지 설정에서 가져옵니다.

1. AEM 사이트 *이(가) 고유 ID(마법사를 사용하여 만든 커뮤니티 사이트)*&#x200B;입니다.

   * [시작 자습서](/help/communities/getting-started.md) 중에 생성된 시작 자습서(참여) 사이트 사용
   * 포럼 페이지 노드를 찾습니다

     `/content/sites/engage/en/forum/jcr:content`

   * 채점 및 배지 속성 추가

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * 포럼 구성 요소 노드 찾기

     `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 배지를 표시하려면 속성을 추가하십시오

     `allowBadges = true`

   * 사용자가 로그인하고 포럼 주제를 만들고 브론즈 배지를 받습니다

1. AEM 사이트 *없음* 고유 ID:

   * [커뮤니티 구성 요소 가이드 사용](/help/communities/components-guide.md)
   * 포럼 페이지 노드를 찾습니다

     `/content/community-components/en/forum/jcr:content`

   * 채점 및 배지 속성 추가

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * 포럼 구성 요소 노드 찾기

     `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 배지를 표시하려면 속성을 추가하십시오

     `allowBadges = true`

   * 사용자가 로그인하고 포럼 주제를 만들고 브론즈 배지를 받습니다

1. 사용자에게 cURL 을 사용하는 중재자 배지가 할당됩니다.

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   사용자가 두 개의 브론즈 배지를 받고 중재자 배지가 수여되면 다음과 같이 포럼 항목이 있는 사용자가 표시됩니다.

   ![중재자](assets/moderator.png)

>[!NOTE]
>
>이 예는 다음 모범 사례를 따르지 않습니다.
>
>* 채점 규칙 이름은 전체적으로 고유해야 하며 동일한 이름으로 끝나서는 안 됩니다.
>
>  *수행할 작업이*&#x200B;이(가) 아닌 작업의 예:
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* 다양한 AEM 사이트에 대한 고유한 배지 이미지 만들기

### 액세스 점수 UGC {#access-scoring-ugc}

[API](#scoring-and-badging-apis)을(를) 사용하는 것이 좋습니다.

조사 목적으로 예를 들어 JSRP를 사용하는 경우 점수가 포함된 기본 폴더는 다음과 같습니다.

* `/content/usergenerated/asi/jcr/scoring`

`scoring`의 자식 노드가 채점 규칙 이름입니다. 따라서 가장 좋은 방법은 서버의 채점 규칙 이름이 전체적으로 고유해야 하는 것입니다.

Geometrixx 참여 사이트의 경우 사용자 및 해당 점수는 채점 규칙 이름, 커뮤니티 사이트의 사이트 ID(`engage-ba81p`), 고유 ID 및 사용자 ID로 구성된 경로에 있습니다.

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

커뮤니티 구성 요소 안내서 사이트의 경우, 사용자 및 해당 점수는 채점 규칙 이름, 기본 ID( `default-site`), 고유 ID 및 사용자 ID 로 구성된 경로에 있습니다.

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

점수는 값만 포함하거나 atomicCounter를 간접적으로 참조할 수 있는 `scoreValue_tl` 속성에 저장됩니다.

![access-scoring-ugc](assets/access-scoring-ugc.png)

### 액세스 배지 UGC {#access-badging-ugc}

[API](#scoring-and-badging-apis)을(를) 사용하는 것이 좋습니다.

조사 목적으로 예를 들어 JSRP를 사용하는 경우 할당되거나 부여된 배지에 대한 정보가 포함된 기본 폴더는 입니다.

* `/content/usergenerated/asi/jcr`

뒤에 사용자 프로필에 대한 경로가 표시되고 배지 폴더로 끝납니다. 예:

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### 수여된 배지 {#awarded-badge}

![수여된 배지-ugc](assets/access-badging-ugc.png)

#### 할당된 배지 {#assigned-badge}

![할당된 배지](assets/assigned-badge.png)

## 추가 정보 {#additional-information}

점을 기준으로 정렬된 멤버 목록을 표시하려면 다음을 수행합니다.

* 커뮤니티 사이트 또는 그룹 템플릿에 포함할 [순위표 함수](/help/communities/functions.md#leaderboard-function).
* [리더보드 구성 요소](/help/communities/enabling-leaderboard.md), 페이지 작성을 위한 리더보드 기능의 추천 구성 요소.
