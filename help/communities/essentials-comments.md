---
title: 댓글 기본 사항
description: 댓글 시스템(댓글 구성 요소) 작업 및 커뮤니티 구성원 게시물의 사용자 생성 콘텐츠(UGC) 관리에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 3%

---

# 댓글 기본 사항 {#comments-essentials}

이 페이지에서는 댓글 시스템(댓글 구성 요소) 작업의 기본 사항과 구성원이 댓글이나 댓글을 게시할 때 생성된 사용자 생성 콘텐츠(UGC)를 관리하는 옵션을 제공합니다.

comments 구성 요소는 각 개별 게시물이 댓글 구성 요소 (단수)로 표시되도록 댓글 시스템 을 설정합니다. 그것은 페이지에 포함된 댓글 시스템입니다. 주석 시스템은 호출 시 개별 주석을 생성합니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함되</strong></a></td>
   <td>예 - 다음 위치에서 편집 가능한 속성 <i>디자인 </i>모드</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> 속성</strong></td>
   <td> 다음을 참조하십시오 <a href="comments.md">주석 사용</a></td>
  </tr>
 </tbody>
</table>

[클라이언트측 사용자 지정](client-customize.md)

### 페이지당 하나의 인스턴스 {#one-instance-per-page}

페이지 매김과 캐싱 및 연결에 URL을 사용하려면 댓글 시스템별로 URL이 고유해야 합니다. 따라서 페이지당 하나의 댓글 시스템 인스턴스만 허용됩니다.

다른 기능에는 이미 주석 시스템이 포함되어 있습니다. 이 4가지 주요 원칙은 다음과 같습니다.

* [블로그](blog-developer-basics.md)
* [달력](calendar-basics-for-developers.md)
* [파일 라이브러리](essentials-file-library.md)
* [포럼](essentials-forum.md)
* [QnA](qna-essentials.md)
* [리뷰](reviews-basics.md)

### 플래그 이유 목록 {#flag-reason-list}

앱에 flagreasonlist.hbs를 추가하여 의 항목을 덮어쓰면 플래그 지정 이유 목록을 사용자 지정할 수 있습니다

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

주석 시스템을 확장하는 모든 구성 요소에 적용됩니다.

## 서버측 Essentials {#essentials-for-server-side}

* [댓글 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [주석 엔드포인트](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### 게시한 의견 액세스(UGC) {#accessing-posted-comments-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재되어야 합니다.
다음을 참조하십시오 [사용자 생성 컨텐츠 중재](moderate-ugc.md).

AEM 6.1 커뮤니티에서 [공동 저장소](working-with-srp.md) ugc의 경우 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스하는 기능이 포함됩니다.

**저장소에서 UGC의 위치 및 형식은 경고 없이 변경될 수 있습니다**.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요.
* [SRP 및 UGC 필수 패키지](srp-and-ugc.md) - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC에 액세스](accessing-ugc-with-srp.md) - 코딩 지침
* [SocialUtils 리팩터링](socialutils.md) - 더 이상 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
