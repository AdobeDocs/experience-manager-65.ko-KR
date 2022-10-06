---
title: 소셜 그래프 핵심 사항
seo-title: Social Graph Essentials
description: 구성 요소 및 다음 구성 요소 개요 추가
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 3%

---

# 소셜 그래프 핵심 사항  {#social-graph-essentials}

커뮤니티 구성원이 수행할 수 있는 기능 [활동](essentials-activities.md) 또한 다음 두 가지 구성 요소를 통해 구축됩니다.

다음 `following` 구성 요소는 다른 리소스와 연결되어 있어야 하며 이 연결은 이미 의 기존 Communities 구성원 및 기능에 대해 설정되어 있습니다 [커뮤니티 사이트](overview.md#communitiessites).

다음 `following` 구성 요소는 현재 멤버를 따르거나 현재 멤버가 뒤에 오는 멤버를 나열합니다. 구성원 간의 관계에 대한 이 소셜 그래프는 커뮤니티 사이트에 대해 설정된 사용자 프로필에 포함되어 있습니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

### 팔로잉 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>소셜/소셜 그래프/구성 요소/hbs/관계</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함 가능</strong></a></td>
   <td>아니요</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>템플릿</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> 속성</strong></td>
   <td>자세한 내용은 <a href="socialgraph.md">소셜 그래프 사용</a></td>
  </tr>
  <tr>
   <td><strong> 옵션<br /> 속성</strong></td>
   <td>
    <ul>
     <li>이름: <strong><code>outgoing</code></strong></li>
     <li>Type: Boolean</li>
     <li>값:<br />
      <ul>
       <li><i>True </i>- <code>following</code> 구성 요소는 현재 로그인한 구성원을 나열할 것입니다 <code>follows</code></li>
       <li><i>False </i>- <code>following</code> 구성 요소는 <code>follow </code>현재 로그인한 구성원</li>
      </ul> </li>
    </ul> <p>기본값은 입니다. <i>true</i> 속성이 누락된 경우 현재 작성 모드에서는 편집 대화 상자를 사용하여 이 속성을 설정할 수 없습니다. 속성을 <code>following </code>노드 사용 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 팔로우 {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**포함 가능**](scf.md#add-or-include-a-communities-component) | 아니요 |
| **템플릿** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 핵심 사항 {#essentials-for-server-side}

* [소셜 그래프 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [소셜 그래프 엔드포인트](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [서버측 사용자 지정](server-customize.md)
