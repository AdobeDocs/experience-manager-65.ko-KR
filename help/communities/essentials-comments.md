---
title: 주석 필수
seo-title: 주석 필수
description: 주석 구성 요소 개요
seo-description: 주석 구성 요소 개요
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# 주석 필수 {#comments-essentials}

이 페이지에서는 댓글 시스템(주석 구성 요소)을 사용하는 데 필요한 필수 사항과 구성원이 댓글 또는 답글을 게시할 때 생성되는 사용자 생성 컨텐츠(UGC)를 관리하는 옵션을 제공합니다.

댓글 구성 요소는 각 개별 게시물이 주석 구성 요소(단일)로 표현되도록 주석 시스템을 설정합니다. 페이지에 포함된 주석 시스템입니다. 주석 시스템은 호출될 때 개별 주석을 만듭니다.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>예 - <i>디자인 </i>모드에서 속성을 편집할 수 있습니다.</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs를</strong></a></td>
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
   <td> 주석 <a href="comments.md">사용을 참조하십시오.</a></td>
  </tr>
 </tbody>
</table>

[클라이언트측 사용자 정의](client-customize.md)

### 페이지당 하나의 인스턴스 {#one-instance-per-page}

페이지 매김 및 캐싱 및 연결에 대한 URL을 사용하려면 URL이 주석 시스템당 고유해야 합니다. 따라서 페이지당 하나의 주석 시스템 인스턴스만 허용됩니다.

다른 기능에는 이미 주석 시스템이 포함되어 있습니다. 다음과 같습니다.

* [블로그](blog-developer-basics.md)
* [달력](calendar-basics-for-developers.md)
* [파일 라이브러리](essentials-file-library.md)
* [포럼](essentials-forum.md)
* [QnA](qna-essentials.md)
* [검토](reviews-basics.md)

### 플래그 이유 목록 {#flag-reason-list}

플래그를 지정하는 이유 목록은 flagreasonlist.hbs를 앱에 추가하여

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

이것은 주석 시스템을 확장하는 모든 구성 요소에 적용됩니다.

## Essentials for Server-Side {#essentials-for-server-side}

* [주석 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [댓글 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [서버측 사용자 정의](server-customize.md)

### 게시된 댓글 액세스(UGC) {#accessing-posted-comments-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재해야 합니다.
사용자 [생성 컨텐츠 중재를 참조하십시오](moderate-ugc.md).

AEM 6.1 Communities의 경우, UGC용 [공용 스토어를](working-with-srp.md) 사용하면 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 상관없이 프로그래머틱 방식으로 UGC에 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고**&#x200B;없이 변경될 수 있습니다.

다음을 참조하십시오.

* [스토리지 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 방법 및 예제
* [SRP를 사용하여 UGC](accessing-ugc-with-srp.md) 액세스 - 코딩 지침
* [SocialUtils 리팩토링](socialutils.md) - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑

