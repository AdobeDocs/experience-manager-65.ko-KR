---
title: 컨텐츠 속성을 사용하여 컨텐츠 내보내기
seo-title: 컨텐츠 속성을 사용하여 컨텐츠 내보내기
description: 다음 페이지에는 앱 속성 및 노드가 표시됩니다.
seo-description: 다음 페이지에는 앱 속성 및 노드가 표시됩니다.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---


# 콘텐츠 속성을 사용하여 콘텐츠 내보내기{#using-content-properties-to-export-content}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에서는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

앱은 AEM에서 *cq:Pages*&#x200B;로 표시됩니다.

통합 지원 속성을 나타내는 아래 표시된 다른 속성과 함께 *cq:Page*&#x200B;에 있는 동일한 공통 속성을 공유합니다.

## 앱 속성 {#app-properties}

다음 표는 **앱 속성 및 노드**&#x200B;를 보여줍니다.

<table>
 <tbody>
  <tr>
   <td><strong>PropertyName</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>문자열:경로</td>
   <td><p>구성된 Mobile On-Demand Cloud Service에 대한 경로입니다. AEM Mobile에서 모바일 온디맨드 작업(API 호출)에 사용됨</p> <p>이 연결은 작성자가 앱을 연결할 모바일 온디맨드 Cloud Service을 선택할 때 연결 관리 타일을 통해 구성됩니다.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>문자열:경로</td>
   <td><p>앱의 내보내기 구성 경로입니다. 내보내기 구성은 두 개의 하위 ContentSync 내보내기 구성 템플릿이 있는 폴더입니다.</p> <p><i>dps-article</i>:아티클 콘텐츠 내보내기를 위한 ContentSync 내보내기 구성</p> <p><i>dps-HTMLResources</i>:ContentSync 내보내기 구성을 통해 앱/아티클 공유 리소스 내보내기</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>문자열</td>
   <td><p>이 앱이 연결/바인딩되어 있는 모바일 온디맨드 프로젝트의 ID/URI입니다.</p> <p>이 연결은 작성자가 연결된 모바일 온디맨드 Cloud Service에 대해 사용 가능한 프로젝트 목록에서 프로젝트를 선택할 때 연결 관리 타일을 통해 구성됩니다.</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>문자열</td>
   <td>앱 제목.</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>문자열</td>
   <td>컨텐츠 유형.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>날짜</td>
   <td>AEM에서 AEM Mobile으로 공유 리소스의 마지막 업로드 날짜입니다.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>문자열:userid</td>
   <td>AEM에서 AEM Mobile으로 공유 리소스 요청을 마지막으로 업로드한 사용자의 ID입니다.</td>
  </tr>
  <tr>
   <td>pge-dashboard-config</td>
   <td>문자열:경로</td>
   <td>대시보드 구성에 대한 경로입니다. 필요에 따라 경로를 사용자 지정 대시보드 구성으로 리디렉션할 수 있습니다.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>문자열:경로</td>
   <td><p><i>mobileapps/core/components/instance를 확장하거나 확장되는 cq:Component로의 경로입니다.</i></p> <p>앱 카탈로그에서 현재 상태 및 렌더링을 제공합니다.</p> </td>
  </tr>
 </tbody>
</table>

***콘텐츠 속성***&#x200B;을 사용하여 콘텐츠를 만들 수 있습니다. 아티클 및 공유 리소스를 만들고 내보내려면 다음 리소스를 참조하십시오.

* [콘텐츠 속성](/help/mobile/content-properties.md)
* [아티클 내보내기 구성 만들기](/help/mobile/creating-article-export-configuration.md)
* [공유 리소스 내보내기 구성 만들기](/help/mobile/creating-shared-resources-export-configuration.md)
