---
title: 점수 책정 및 배지 핵심 사항
seo-title: 점수 책정 및 배지 핵심 사항
description: 점수 및 배지 기능 개요
seo-description: 점수 및 배지 기능 개요
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 0%

---

# 점수 및 배지 필수 패키지 {#scoring-and-badges-essentials}

AEM Communities 점수 및 배지 기능은 커뮤니티 구성원을 식별하고 포상하는 기능을 제공합니다.

기능 설정에 대한 자세한 내용은

* [커뮤니티 점수 및 배지](/help/communities/implementing-scoring.md)

이 페이지에는 추가적인 기술 세부 사항 이 포함되어 있습니다.

* [배지](#displaying-badges)를 이미지 또는 텍스트로 표시하는 방법
* 광범위한 [디버그 로깅](#debug-log-for-scoring-and-badging)을 설정하는 방법
* 점수 및 배지 매기와 관련된 [UGC](#ugc-for-scoring-and-badging)에 액세스하는 방법

>[!CAUTION]
>
>CRXDE Lite에 표시되는 구현 구조는 변경될 수 있습니다.

## 배지 {#displaying-badges} 표시

배지가 텍스트로 표시되는지 아니면 이미지가 HBS 템플릿의 클라이언트 측에서 제어되는지 여부를 나타냅니다.

예를 들어 `/libs/social/forum/components/hbs/topic/list-item.hbs`에서 `this.isAssigned`을 검색합니다.

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

true인 경우 isAssigned 는 역할에 대해 배지가 할당되었음을 나타내고 배지는 텍스트로 표시되어야 합니다.

false인 경우, 할당됨은 획득한 배지가 이미지로 표시되어야 함을 나타냅니다.

이 동작에 대한 모든 변경 사항은 사용자 지정된 스크립트(재정의 또는 오버레이)로 수행해야 합니다. [클라이언트측 사용자 지정](/help/communities/client-customize.md)을 참조하십시오.

## 점수 및 배지 {#debug-log-for-scoring-and-badging}에 대한 디버그 로그

점수부여 및 배지 디버깅에 도움이 되도록 사용자 지정 로그 파일을 설정할 수 있습니다. 이 기능에 문제가 발생하는 경우 이 로그 파일의 내용을 고객 지원에 제공할 수 있습니다.

자세한 지침은 [사용자 지정 로그 파일 만들기](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)를 참조하십시오.

슬링로그 파일을 신속하게 설정하려면 다음을 수행하십시오.

1. 예를 들어 **Adobe Experience Manager 웹 콘솔 로그 지원**&#x200B;에 액세스합니다

   * https://localhost:4502/system/console/slinglog

1. **새 로거 추가** 선택

   1. **로그 수준**&#x200B;에 대해 `DEBUG`을 선택합니다.

   1. 예를 들어, **로그 파일**&#x200B;의 이름을 입력합니다

      * logs/scoring-debug.log
   1. **로거** (클래스) 항목을 두 개 입력합니다( `+` 아이콘 사용)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. **저장**&#x200B;을 선택합니다



![debug-scoring-log](assets/debug-scoring-log.png)

로그 항목을 보려면

* 웹 콘솔에서

   * **상태** 메뉴 아래에 있습니다.
   * **로그 파일 선택**
   * `scoring-debug` 등의 로그 파일 이름을 검색합니다.

* 서버의 로컬 디스크

   * 로그 파일은 &lt;*server-install-dir*/crx-quickstart/logs/&lt;*log-file-name*.log에 있습니다.

   * 예, `.../crx-quickstart/logs/scoring-debug.log`

![점수 책정 로그](assets/scoring-log.png)

## 점수 및 배지 {#ugc-for-scoring-and-badging}에 대한 UGC

선택한 SRP가 JSRP 또는 MSRP이지만 ASRP가 아닌 경우 점수 및 배지 지정과 관련된 UGC를 볼 수 있습니다. (이러한 용어에 익숙하지 않은 경우 [커뮤니티 컨텐츠 저장소](/help/communities/working-with-srp.md) 및 [저장소 리소스 공급자 개요](/help/communities/srp.md)를 참조하십시오.)

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)을 사용하여 UGC에 쉽게 액세스할 수 있으므로 점수부여 및 배지 데이터에 액세스하기 위한 설명은 JSRP를 사용합니다.

**작성자의 JSRP**:작성 환경에서 테스트하면 작성 환경에서만 표시되는 UGC가 만들어집니다.

**게시할 때의 JSRP**:마찬가지로, 게시 환경에서 테스트하는 경우 게시 인스턴스에 대한 관리 권한이 있는 CRXDE Lite에 액세스해야 합니다. 게시 인스턴스가 [프로덕션 모드](/help/sites-administering/production-ready.md)(nosamplecontent runmode)에서 실행 중인 경우 [CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md)을 활성화해야 합니다.

JSRP에 대한 UGC의 기본 위치는 `/content/usergenerated/asi/jcr/`입니다.

### 점수 및 배지 API {#scoring-and-badging-apis}

다음 API를 사용할 수 있습니다.

* [com.adobe.cq.social.scoring.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/scoring/api/package-summary.html)
* [com.adobe.cq.social.badging.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/badging/api/package-summary.html)

설치된 기능 팩의 최신 Javadocs는 Adobe 리포지토리의 개발자가 사용할 수 있습니다. [Communities용 Maven 사용 을 참조하십시오.Javadocs](/help/communities/maven.md#javadocs).

**저장소에서 UGC의 위치와 형식은 경고** 없이 변경될 수 있습니다.

### 설치 예 {#example-setup}

저장소 데이터의 스크린샷은 두 개의 서로 다른 AEM 사이트에 있는 포럼에 대한 점수 및 배지 설정으로부터 나옵니다.

1. 고유 ID(마법사를 사용하여 만든 커뮤니티 사이트)가 있는 AEM 사이트 *입니다.*

   * [시작 자습서](/help/communities/getting-started.md) 중에 만든 시작 자습서(참여) 사이트 사용
   * 포럼 페이지 노드를 찾습니다.

      `/content/sites/engage/en/forum/jcr:content`

   * 점수 및 배지 속성 추가

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * 포럼 구성 요소 노드를 찾습니다.

      `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 속성을 추가하여 배지 표시

      `allowBadges = true`

   * 사용자가 로그인하고 포럼 주제를 만들며 청동 배지를 받습니다


1. 고유한 ID가 없는 AEM 사이트 *입니다.*

   * [커뮤니티 구성 요소 안내서](/help/communities/components-guide.md) 사용
   * 포럼 페이지 노드를 찾습니다.

      `/content/community-components/en/forum/jcr:content`

   * 점수 및 배지 속성 추가

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * 포럼 구성 요소 노드를 찾습니다.

      `/content/community-components/en/forum/jcr:content/content/forum`
(  `sling:resourceType = social/forum/components/hbs/forum`)

   * 속성을 추가하여 배지 표시

      `allowBadges = true`

   * 사용자가 로그인하고 포럼 주제를 만들며 청동 배지를 받습니다


1. 사용자에게 cURL 을 사용하여 중재자 배지가 지정됩니다.

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   사용자가 청동 배지 두 개를 획득하고 중재자 배지 수여를 받았으므로 사용자가 포럼 항목과 함께 표시되는 방식입니다.

   ![중재자](assets/moderator.png)

>[!NOTE]
>
>이 예는 다음 우수 사례를 따르지 않습니다.
>
>* 점수 규칙 이름은 전역적으로 고유해야 합니다.같은 이름으로 끝나면 안 됩니다.
>
>  
*이*&#x200B;하지 않을 작업의 예:
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* 다양한 AEM 사이트에 대한 고유한 배지 이미지 만들기


### 액세스 점수 UGC {#access-scoring-ugc}

[API](#scoring-and-badging-apis)를 사용하는 것이 좋습니다.

조사 목적으로 예제에 JSRP를 사용하면 점수가 포함된 기본 폴더는 다음과 같습니다

* `/content/usergenerated/asi/jcr/scoring`

`scoring`의 하위 노드는 점수 규칙 이름입니다. 따라서 서버의 점수 규칙 이름을 전역적으로 고유하도록 지정하는 것이 가장 좋습니다.

Geometrixx 참여 사이트의 경우 사용자 및 해당 점수는 점수 규칙 이름, 커뮤니티 사이트의 사이트 ID( `engage-ba81p`), 고유 ID 및 사용자 ID 가 포함된 경로에 있습니다.

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

커뮤니티 구성 요소 안내서 사이트의 경우 사용자 및 해당 점수는 점수 규칙 이름, 기본 ID( `default-site`), 고유 ID 및 사용자 ID로 구성된 경로에 있습니다.

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

점수는 `scoreValue_tl` 속성에 저장됩니다. 이 속성에는 직접 값만 포함되거나 atomicCounter를 간접적으로 참조할 수 있습니다.

![access-scoring-ugc](assets/access-scoring-ugc.png)

### 배지 UGC {#access-badging-ugc}에 액세스

[API](#scoring-and-badging-apis)를 사용하는 것이 좋습니다.

예를 들어 JSRP를 사용하여 조사 목적으로 지정된 배지에 대한 정보가 포함된 기본 폴더는 다음과 같습니다

* `/content/usergenerated/asi/jcr`

다음에 사용자의 프로필 경로가 나타나고 다음과 같은 배지 폴더로 끝납니다.

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### 수여된 배지 {#awarded-badge}

![수상 배지-ugc](assets/access-badging-ugc.png)

#### 할당된 배지 {#assigned-badge}

![지정된 배지](assets/assigned-badge.png)

## 추가 정보 {#additional-information}

점을 기준으로 정렬된 멤버 목록을 표시하려면 다음을 수행합니다.

* [커뮤니티 ](/help/communities/functions.md#leaderboard-function) 사이트 또는 그룹 템플릿에 포함할 리드 보드 기능.
* [리더보드](/help/communities/enabling-leaderboard.md) 기능의 주요 구성 요소인 페이지 작성을 위한 리더보드 구성 요소입니다.
