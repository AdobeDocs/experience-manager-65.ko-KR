---
title: 주석 핵심 사항
seo-title: 주석 핵심 사항
description: 댓글 구성 요소 개요
seo-description: 댓글 구성 요소 개요
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 3%

---

# 설명 필수 요소 {#comments-essentials}

이 페이지에서는 댓글 시스템(주석 구성 요소) 작업 필수 사항과 구성원이 댓글 또는 답글을 게시할 때 생성되는 UGC(사용자 생성 컨텐츠)를 관리하는 옵션을 제공합니다.

댓글 구성 요소는 각 개별 게시물이 댓글 구성 요소(단일)로 표시되도록 주석 시스템을 설정합니다. 페이지에 포함된 주석 시스템입니다. 호출되면 주석 시스템에서 개별 주석을 생성합니다.

## 클라이언트측 {#essentials-for-client-side}에 대한 필수 사항

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>예 - 속성은 <i>디자인 </i>모드에서 편집할 수 있습니다</td>
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
   <td> <a href="comments.md">댓글 사용</a> 을 참조하십시오.</td>
  </tr>
 </tbody>
</table>

[클라이언트측 사용자 지정](client-customize.md)

### 페이지당 하나의 인스턴스 {#one-instance-per-page}

페이지 매김 및 캐싱 및 연결에 URL을 사용하려면 URL이 주석 시스템당 고유해야 합니다. 따라서 페이지당 댓글 시스템의 인스턴스는 하나만 허용됩니다.

다른 기능에는 이미 댓글 시스템이 포함되어 있습니다. 이 4가지 주요 원칙은 다음과 같습니다.

* [블로그](blog-developer-basics.md)
* [달력](calendar-basics-for-developers.md)
* [파일 라이브러리](essentials-file-library.md)
* [포럼](essentials-forum.md)
* [QnA](qna-essentials.md)
* [검토](reviews-basics.md)

### 플래그 이유 목록 {#flag-reason-list}

플래그 지정 이유 목록은 앱에 있는 항목을 덮어쓸 수 있도록 flarasonlist.hbs를 추가하여 사용자 지정할 수 있습니다

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

이는 주석 시스템을 확장하는 모든 구성 요소에 적용됩니다.

## 서버측 {#essentials-for-server-side}에 대한 필수 사항

* [댓글 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [댓글 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### 게시된 댓글 액세스(UGC) {#accessing-posted-comments-ugc}

조정을 위한 표준 방법 중 하나를 사용하여 UGC가 중재되어야 합니다.
[사용자가 생성한 콘텐츠 중재](moderate-ugc.md)를 참조하십시오.

AEM 6.1 Communities에서 UGC용 [공용 스토어](working-with-srp.md)를 사용하면 선택한 저장소 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고** 없이 변경될 수 있습니다.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md)  - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](srp-and-ugc.md)  - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC 액세스](accessing-ugc-with-srp.md)  - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md)  - 사용 중단된 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
