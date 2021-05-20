---
title: QnA 핵심 사항
seo-title: QnA 핵심 사항
description: 질문 및 답변 포럼 기능
seo-description: 질문 및 답변 포럼 기능
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# QnA 필수 패키지 {#qna-essentials}

이 페이지에서는 QnA(질문 및 답변) 포럼 기능 작업에 필요한 필수 정보를 제공합니다.

## 클라이언트측 {#essentials-for-client-side}에 대한 필수 사항

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">포함 가능</a></td>
   <td>아니오</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientlibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.qna</td>
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
   <td><a href="working-with-qna.md">Q&amp;A 포럼 기능</a> 을 참조하십시오.</td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 {#essentials-for-server-side}에 대한 필수 사항

* [QnA API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [QnA 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [서버측 사용자 지정](server-customize.md)

### QnA 기능 {#qna-function}

[QnA 함수](functions.md#qna-function)를 포함하는 커뮤니티 사이트 구조에는 조정 및 태깅에 영향을 주는 설정과 구성된 `QnA` 구성 요소가 있습니다. QnA 함수는 [권한이 있는 구성원 사용자 그룹 식별](users.md#privileged-members-group)을 지원합니다.

### QnA 포럼 게시물 액세스(UGC) {#accessing-qna-forum-posts-ugc}

조정을 위한 표준 방법 중 하나를 사용하여 UGC가 중재되어야 합니다.
[사용자가 생성한 콘텐츠 중재](moderate-ugc.md)를 참조하십시오.

AEM 6.1 Communities에서 UGC용 [공용 스토어](working-with-srp.md)를 사용하면 선택한 저장소 옵션(예: ASRP, MSRP 또는 JSRP)에 관계없이 UGC에 프로그래밍 방식으로 액세스할 수 있습니다.

**저장소에서 UGC의 위치와 형식은 경고** 없이 변경될 수 있습니다.

다음을 참조하십시오.

* [저장소 리소스 공급자 개요](srp.md)  - 소개 및 저장소 사용 개요.
* [SRP 및 UGC Essentials](srp-and-ugc.md)  - SRP 유틸리티 메서드 및 예제.
* [SRP를 사용하여 UGC 액세스](accessing-ugc-with-srp.md)  - 코딩 지침.
* [SocialUtils 리팩터링](socialutils.md)  - 사용 중단된 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.
