---
title: 파일 라이브러리 필수
seo-title: 파일 라이브러리 필수
description: 파일 라이브러리 기능 사용
seo-description: 파일 라이브러리 기능 사용
uuid: 0630f13e-97b4-4f93-9dce-07f559287c29
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9019b967-fff8-4dda-bc5a-fd4a3e14a4ef
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 2%

---


# 파일 라이브러리 필수 {#file-library-essentials}

이 페이지에서는 파일 라이브러리 기능 작업에 필요한 정보를 제공합니다.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/filelibrary/components/hbs/filelibrary</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>아니오</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vocing<br /> cq.social.hbs.filelibrary</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/filelibrary.hbs<br /> /libs/social/filelibrary/components/hbs/folder/folder.hbs<br /> /libs/social/filelibrary/components/hbs/folder/item.hbs<br /> /libs/social/filelibrary/components/hbs/document/document.hbs<br /> /libs/social/filelibrary/components/hbs/document/item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/clientlibs/filelibrary.css</td>
  </tr>
  <tr>
   <td><strong> 속성</strong></td>
   <td>파일 <a href="file-library.md">라이브러리 기능 보기</a></td>
  </tr>
 </tbody>
</table>

* [클라이언트측 사용자 지정](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [파일 라이브러리 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/api/package-summary.html)

* [파일 라이브러리 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/endpoints/package-summary.html)

* [서버측 사용자 정의](server-customize.md)

### 파일 라이브러리 기능 {#file-library-function}

파일 라이브러리 함수를 포함하는 [커뮤니티 사이트](functions.md#file-library-function)구조에는 구성된 `file library` 구성 요소가 포함됩니다.

### UGC(파일 라이브러리)에 게시된 주석 액세스 {#accessing-comments-posted-for-file-libraries-ugc}

중재의 표준 방법 중 하나를 사용하여 UGC를 중재해야 합니다.
사용자 [생성 컨텐츠 중재를 참조하십시오](moderate-ugc.md).

AEM 6.1 Communities의 경우, UGC용 [공용 스토어](working-with-srp.md) 사용에는 선택한 스토리지 옵션(예: ASRP, MSRP 또는 JSRP)에 상관없이 UGC에 대한 프로그래머틱 액세스가 포함됩니다.

**저장소의 UGC의 위치와 형식은 경고**&#x200B;없이 변경될 수 있습니다.

다음을 참조하십시오.

* [스토리지 리소스 공급자 개요](srp.md) - 소개 및 저장소 사용 개요
* [SRP 및 UGC Essentials](srp-and-ugc.md) - SRP 유틸리티 방법 및 예
* [SRP를 사용하여 UGC](accessing-ugc-with-srp.md) 액세스 - 코딩 가이드라인.
* [SocialUtils 리팩토링](socialutils.md) - 사용되지 않는 유틸리티 메서드를 현재 SRP 유틸리티 메서드에 매핑합니다.

