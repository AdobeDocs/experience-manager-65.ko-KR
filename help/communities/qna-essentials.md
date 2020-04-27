---
title: QnA Essentials
seo-title: QnA Essentials
description: 질문 및 답변 포럼 기능
seo-description: 질문 및 답변 포럼 기능
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
translation-type: tm+mt
source-git-commit: ca15258a5dc7ca99b6c9d6ae85e42c77a3802c87

---


# QnA Essentials {#qna-essentials}

이 페이지에서는 질문 및 답변(QnA) 포럼 기능 작업에 필요한 정보를 제공합니다.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">includable</a></td>
   <td>아니오</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientlibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vocting<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> 템플릿</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> 속성</td>
   <td>Q <a href="working-with-qna.md">&amp;A 포럼 기능 보기</a></td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 정의](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [QnA API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [QnA 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [서버측 사용자 정의](server-customize.md)

### QnA 기능 {#qna-function}

QnA 함수를 [포함하는 커뮤니티 사이트 구조에는](functions.md#qna-function) `QnA` 구성 요소뿐만 아니라 중재 및 태그 지정에 영향을 주는 설정이 포함됩니다. QnA 함수는 [권한 있는 구성원 사용자 그룹](users.md#privileged-members-group)식별을 지원합니다.

### UGC(포럼 게시물) 액세스 {#accessing-qna-forum-posts-ugc}

UGC는 중재에 대한 표준 방법 중 하나를 사용하여 중재해야 합니다.
사용자 [생성 컨텐츠 중재를 참조하십시오](moderate-ugc.md).

AEM 6.1 Communities의 경우, UGC용 [공용 스토어를](working-with-srp.md) 사용하면 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 상관없이 프로그래머틱 방식으로 UGC에 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고**&#x200B;없이 변경될 수 있습니다.

다음을 참조하십시오.

* [스토리지 자원 공급자 개요](srp.md) - 소개 및 저장소 사용 개요
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 방법 및 예
* [SRP를 사용하여 UGC에](accessing-ugc-with-srp.md) 액세스 - 코딩 지침
* [SocialUtils 리팩토링](socialutils.md) - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.

