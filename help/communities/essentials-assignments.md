---
title: 지정 필수 항목
seo-title: 지정 필수 항목
description: 지원 커뮤니티에 대한 지정 기능 개요
seo-description: 지원 커뮤니티에 대한 지정 기능 개요
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
exl-id: 75cef5da-4f93-4721-99c0-ad44c8ab76d4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 12%

---

# 지정 필수 항목 {#assignments-essentials}

[지원 커뮤니티](/help/communities/overview.md#enablement-community) 사이트의 지정 기능 작업에 필요한 필수 정보를 숙지하려면 를 참조하십시오.

지정 기능은 지원 커뮤니티 구성원에게 지원 리소스와 학습 경로를 할당하는 기능입니다.

## 클라이언트측 {#essentials-for-client-side}에 대한 필수 사항

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>아니오</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrums<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learning path</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> 속성</strong></td>
   <td><a href="/help/communities/assignments.md">지정 기능</a>을 참조하십시오.</td>
  </tr>
 </tbody>
</table>

### 완료 및 성공 상태 {#completion-and-success-status}

완료 및 성공 상태는 지정 의 보고서 및 상태 배너에 사용됩니다.

완료 상태:

* 지정되지 않음
* 시작되지 않음(신규)
* 진행 중
* 완료

성공 상태:

* 알 수 없음
* 합격
* 실패

완료 및 성공 상태의 조합은 다음과 뿐입니다.

| **완료** | **성공** |
|---|---|
| 시작되지 않음 | 알 수 없음 |
| 진행 중 | 알 수 없음 |
| 완료 | 합격 |
| 완료 | 실패 |

## 서버측 {#essentials-for-server-side}에 대한 필수 사항

### 지정 기능 {#assignments-function}

[할당 함수](/help/communities/functions.md#assignments-function)를 포함하는 커뮤니티 사이트 구조에는 구성된 ` [assignments](/help/communities/assignments.md)` 구성 요소가 포함되어 있습니다.

### 참조 API {#reference-apis}

* [지원 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [보고 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [Reporting Analytics API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/analytics/api/package-summary.html)
