---
title: 소셜 그래프 필수
seo-title: 소셜 그래프 필수
description: 구성 요소 따라하기 및 다음 구성 요소 개요
seo-description: 구성 요소 따라하기 및 다음 구성 요소 개요
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---


# 소셜 그래프 필수 항목 {#social-graph-essentials}

다음 두 구성 요소를 통해 [활동](essentials-activities.md)을 따르고 따를 수 있는 커뮤니티 멤버가 설정됩니다.

`following` 구성 요소는 다른 리소스와 연결되어 있어야 하며 이 연결은 이미 [커뮤니티 사이트](overview.md#communitiessites)의 기존 커뮤니티 구성원 및 기능에 대해 설정되어 있습니다.

`following` 구성 요소에는 현재 구성원을 팔로우하거나 현재 구성원이 뒤에 오는 멤버가 나열됩니다. 구성원 간의 관계에 대한 이 소셜 그래프는 커뮤니티 사이트에 대해 설정된 사용자 프로필에 포함됩니다.

## Essentials for Client-Side {#essentials-for-client-side}

### 팔로잉 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relations</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>아니오</td>
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
   <td><a href="socialgraph.md">소셜 그래프 사용</a> 참조</td>
  </tr>
  <tr>
   <td><strong> optional<br /> 속성</strong></td>
   <td>
    <ul>
     <li>이름: <strong><code>outgoing</code></strong></li>
     <li>Type: Boolean</li>
     <li>값:<br />
      <ul>
       <li><i>참  </i>-  <code>following</code> 구성 요소에는 현재 로그인한 구성원이 있는 구성원이 나열됩니다 <code>follows</code></li>
       <li><i>False  </i>-  <code>following</code> 구성 요소에는  <code>follow </code>현재 로그인한 구성원이 있는 구성원이 나열됩니다</li>
      </ul> </li>
    </ul> <p>속성이 없는 경우 기본값은 <i>true</i>입니다. 현재 작성 모드에서 편집 대화 상자를 사용하여 이 속성을 설정할 수 없습니다. 속성은 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>를 사용하여 <code>following </code>노드 인스턴스에 추가해야 합니다.</p> </td>
  </tr>
 </tbody>
</table>

### 팔로우 {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**includable**](scf.md#add-or-include-a-communities-component) | 아니오 |
| **템플릿** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [클라이언트측 사용자 지정](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [소셜 그래프 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [소셜 그래프 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [서버측 사용자 정의](server-customize.md)

