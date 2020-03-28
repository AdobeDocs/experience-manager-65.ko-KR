---
title: 소셜 그래프 필수
seo-title: 소셜 그래프 필수
description: 구성 요소 및 다음 구성 요소 개요
seo-description: 구성 요소 및 다음 구성 요소 개요
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# 소셜 그래프 필수 {#social-graph-essentials}

커뮤니티 구성원이 [활동을](essentials-activities.md) 따르고 따라야 하는 기능은 다음 두 가지 구성 요소를 통해 설정됩니다.

구성 `following` 요소는 다른 리소스와 연결되어 있어야 하며, 이 연결은 이미 [커뮤니티 사이트의](overview.md#communitiessites)기존 커뮤니티 구성원 및 기능에 대해 설정되어 있습니다.

구성 `following` 요소에는 현재 구성원을 팔로우하거나 현재 구성원이 뒤에 오는 멤버가 나열됩니다. 구성원 간의 관계에 대한 이 소셜 그래프는 커뮤니티 사이트에 대해 설정된 사용자 프로필에 포함됩니다.

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
   <td>소셜 <a href="socialgraph.md">그래프 사용을 참조하십시오.</a></td>
  </tr>
  <tr>
   <td><strong> 선택적<br /> 속성</strong></td>
   <td>
    <ul>
     <li>이름: <strong><code>outgoing</code></strong></li>
     <li>Type: Boolean</li>
     <li>값:<br />
      <ul>
       <li><i>참 </i>- <code>following</code> 구성 요소에는 현재 로그인된 멤버가 표시됩니다 <code>follows</code></li>
       <li><i>False </i>- <code>following</code> 구성 요소에는 <code>follow </code>현재 로그인한 구성원이 나열됩니다</li>
      </ul> </li>
    </ul> <p>속성이 누락된 경우 기본값은 <i>true</i> 입니다. 현재 작성 모드에서 편집 대화 상자를 사용하여 이 속성을 설정할 수 없습니다. 이 속성은 CRXDE|Lite를 사용하여 <code>following </code>노드의 인스턴스에 추가해야 <a href="../../help/sites-developing/developing-with-crxde-lite.md">합니다</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 팔로우 {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**includable **](scf.md#add-or-include-a-communities-component) | 아니오 |
| **템플릿** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [클라이언트측 사용자 정의](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [소셜 그래프 API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [소셜 그래프 끝점](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [서버측 사용자 정의](server-customize.md)

