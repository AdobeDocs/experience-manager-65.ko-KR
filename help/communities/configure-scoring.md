---
title: 점수 및 배지 필수
seo-title: 점수 및 배지 필수
description: 점수 지정 및 배지 기능 개요
seo-description: 점수 지정 및 배지 기능 개요
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
translation-type: tm+mt
source-git-commit: 4170c7fe48a740e0574a32c7823841dc311fd565
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 1%

---


# 점수 및 배지 필수 {#scoring-and-badges-essentials}

AEM Communities 채점 및 배지 기능을 사용하면 커뮤니티 구성원을 식별하고 보상할 수 있습니다.

기능 설정에 대한 자세한 내용은

* [커뮤니티 점수 및 배지](/help/communities/implementing-scoring.md)

이 페이지에는 추가 기술 세부 사항이 포함되어 있습니다.

* 배지 [를 이미지 또는 텍스트로](#displaying-badges) 표시하는 방법
* 광범위한 [디버그 로깅을 설정하는 방법](#debug-log-for-scoring-and-badging)
* 점수 지정 및 배지 [와](#ugc-for-scoring-and-badging) 관련된 UGC에 액세스하는 방법

>[!CAUTION]
>
>CRXDE Lite에 표시되는 구현 구조는 변경될 수 있습니다.

## 배지 표시 {#displaying-badges}

HBS 템플릿의 클라이언트 쪽에서 배지가 텍스트 또는 이미지로 표시되는지 여부.

예를 들어 다음 `this.isAssigned` 에서 검색 `/libs/social/forum/components/hbs/topic/list-item.hbs`:

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

true인 경우 isAssigned는 역할에 대해 배지가 지정되었음을 나타내고 배지는 텍스트로 표시되어야 합니다.

false인 경우, [할당]은 획득 점수에 대해 배지가 부여되었음을 나타내고 배지는 이미지로 표시되어야 합니다.

이 비헤이비어에 대한 모든 변경 사항은 사용자 지정된 스크립트(재정의 또는 오버레이)로 이루어져야 합니다. 클라이언트측 [사용자 지정을 참조하십시오](/help/communities/client-customize.md).

## 점수 지정 및 배지 로그 디버그 {#debug-log-for-scoring-and-badging}

점수 지정 및 배지 디버깅에 도움이 되도록 사용자 지정 로그 파일을 설정할 수 있습니다. 이 기능에 문제가 발생하는 경우 이 로그 파일의 내용을 고객 지원에 제공할 수 있습니다.

자세한 지침은 사용자 [정의 로그 파일 만들기를 참조하십시오](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

슬링 로그 파일을 신속하게 설정하려면:

1. 예를 들어 **Adobe Experience Manager 웹 콘솔 로그 지원**&#x200B;액세스

   * https://localhost:4502/system/console/slinglog

1. 새 로거 **추가 선택**

   1. 로그 수준 `DEBUG` 에 대해 **선택**

   1. 로그 파일 이름 **을**&#x200B;입력합니다.

      * logs/scoring-debug.log
   1. Logger **** (클래스) 항목 2개 입력( `+` 아이콘 사용)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. **저장**&#x200B;을 선택합니다



![chlimage_1-248](assets/chlimage_1-248.png)

로그 항목을 보려면

* 웹 콘솔에서

   * 상태 **메뉴** 아래
   * 로그 **파일 선택**
   * 로그 파일 이름(예: `scoring-debug`

* 서버의 로컬 디스크에

   * 로그 파일은 &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log에 있습니다.

   * 예, `.../crx-quickstart/logs/scoring-debug.log`

![chlimage_1-249](assets/chlimage_1-249.png)

## 점수 지정 및 배지 지정 {#ugc-for-scoring-and-badging}

선택한 SRP가 JSRP 또는 MSRP일 때 점수 및 배지 지정과 관련된 UGC를 볼 수 있지만 ASRP는 볼 수 없습니다. (이러한 용어에 익숙하지 않은 경우 [커뮤니티 컨텐츠 저장소](/help/communities/working-with-srp.md) 및 [저장소 리소스 공급자 개요를 참조하십시오](/help/communities/srp.md).)

CRXDE Lite를 사용하여 UGC에 쉽게 액세스할 수 있으므로 점수 및 배지 데이터에 액세스하기 위한 설명은 JSRP를 [사용합니다](/help/sites-developing/developing-with-crxde-lite.md).

**작성자의 JSRP**: 작성 환경에서 테스트하면 작성 환경에서만 표시되는 UGC가 만들어집니다.

**게시**&#x200B;시 JSRP: 마찬가지로 게시 환경에서 테스트하는 경우 게시 인스턴스에 대한 관리 권한이 있는 CRXDE Lite에 액세스해야 합니다. 게시 인스턴스가 [프로덕션 모드](/help/sites-administering/production-ready.md) (nosamplecontent runmode)에서 실행 중인 경우 CRXDE Lite를 [활성화해야 합니다](/help/sites-administering/enabling-crxde-lite.md).

JSRP에 대한 UGC의 기본 위치는 입니다 `/content/usergenerated/asi/jcr/`.

### 점수 지정 및 배지 API {#scoring-and-badging-apis}

다음 API를 사용할 수 있습니다.

* [com.adobe.cq.sosocial.scoring.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/scoring/api/package-summary.html)
* [com.adobe.cq.sosocial.badging.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/badging/api/package-summary.html)

설치된 기능 팩에 대한 최신 Javadocs는 Adobe 저장소의 개발자가 사용할 수 있습니다. 커뮤니티에 대한 [Maven 사용을 참조하십시오. Javadocs](/help/communities/maven.md#javadocs).

**저장소의 UGC의 위치와 형식은 경고**&#x200B;없이 변경될 수 있습니다.

### 예제 설정 {#example-setup}

저장소 데이터의 스크린샷은 서로 다른 두 AEM 사이트의 포럼에 대한 점수 지정 및 배지 설정으로부터 나옵니다.

1. 고유 ID가 *있는* AEM 사이트(마법사를 사용하여 만든 커뮤니티 사이트):

   * 시작하기 자습서(참여) 사이트 사용( [시작하기 자습서)](/help/communities/getting-started.md)
   * 포럼 페이지 노드 찾기

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

   * 포럼 구성 요소 노드 찾기

      `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 디스플레이 배지에 속성 추가

      `allowBadges = true`

   * 사용자가 로그인하고 포럼 항목을 만들며 브론즈 배지를 수여합니다


1. 고유 ID가 *없는* AEM 사이트:

   * 커뮤니티 구성 [요소 안내서 사용](/help/communities/components-guide.md)
   * 포럼 페이지 노드 찾기

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

   * 포럼 구성 요소 노드 찾기

      `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 디스플레이 배지에 속성 추가

      `allowBadges = true`

   * 사용자가 로그인하고 포럼 항목을 만들며 브론즈 배지를 수여합니다


1. 사용자에게 cURL을 사용하여 중재자 배지가 할당됩니다.

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   사용자가 두 개의 청동 배지를 받았고 사회자 배지가 수여됨에 따라 포럼 참가자가 표시되는 방식은 다음과 같습니다.

![chlimage_1-250](assets/chlimage_1-250.png)

>[!NOTE]
>
>이 예는 다음과 같은 우수 사례를 따르지 않습니다.
>
>* 점수 규칙 이름은 전체적으로 고유해야 합니다. 같은 이름으로 끝나서는 안 됩니다.
   >  하지 *말아야* 할 사항의 예:
   >  /libs/settings/community/scoring/rules/site1/forums-scoring
   >  /libs/settings/community/scoring/rules/site2/forums-scoring
   >
   >
* 다양한 AEM 사이트에 대한 고유한 배지 이미지 만들기

>



### 액세스 점수 UGC {#access-scoring-ugc}

API [를 사용하는 것이](#scoring-and-badging-apis) 좋습니다.

이 예제에 JSRP를 사용하면 점수가 포함된 기본 폴더는 조사 목적으로

* `/content/usergenerated/asi/jcr/scoring`

의 하위 노드 `scoring` 는 점수 지정 규칙 이름입니다. 따라서 서버의 점수 지정 규칙 이름은 전역적으로 고유하도록 하는 것이 좋습니다.

Geometrixx Engage 사이트의 경우 사용자 및 점수는 점수 규칙 이름, 커뮤니티 사이트의 사이트 ID(), 고유 ID 및 사용자 ID로 구성된 경로에 있습니다. `engage-ba81p`

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

커뮤니티 구성 요소 안내서 사이트의 경우 사용자 및 점수는 점수 지정 규칙 이름, 기본 id(), 고유 id 및 사용자 id로 구성된 경로에 있습니다. `default-site`

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

점수는 직접 값만 포함하거나 atomicCounter를 간접적으로 참조할 수 `scoreValue_tl` 있는 속성에 저장됩니다.

![chlimage_1-251](assets/chlimage_1-251.png)

### 배지 UGC 액세스 {#access-badging-ugc}

API [를 사용하는 것이](#scoring-and-badging-apis) 좋습니다.

예를 들어, JSRP를 사용하면 할당되거나 수여된 배지에 대한 정보가 포함된 기본 폴더가 조사됩니다

* `/content/usergenerated/asi/jcr`

그 뒤에 사용자의 프로필 경로,

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### 수상 배지 {#awarded-badge}

![chlimage_1-252](assets/chlimage_1-252.png)

#### 지정된 배지 {#assigned-badge}

![chlimage_1-253](assets/chlimage_1-253.png)

## 추가 정보 {#additional-information}

포인트를 기준으로 정렬된 멤버 목록을 표시하려면 다음을 수행하십시오.

* [커뮤니티 사이트 또는 그룹 템플릿에 포함하기 위한 리드 보드 함수](/help/communities/functions.md#leaderboard-function) .
* [페이지 작성을 위한 Leaderboard 함수의 주요 구성 요소인](/help/communities/enabling-leaderboard.md)Leaderboard 구성 요소입니다.

