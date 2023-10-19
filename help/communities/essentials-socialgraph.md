---
title: 소셜 그래프 기본 사항
description: 커뮤니티 사이트에서 다음 및 팔로우 구성 요소를 사용하여 소셜 그래프의 기본 사항에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# 소셜 그래프 기본 사항  {#social-graph-essentials}

커뮤니티 회원이 팔로우할 수 있는 기능 [활동](essentials-activities.md) 및 는 다음 두 가지 구성 요소를 통해 설정됩니다.

다음 `following` 구성 요소는 다른 리소스와 연결되어 있어야 하며 이 연결은 의 기존 Communities 구성원 및 기능에 대해 이미 설정되어 있습니다. [커뮤니티 사이트](overview.md#communitiessites).

다음 `following` 구성 요소는 현재 멤버 뒤에 오거나 현재 멤버가 뒤에 오는 멤버를 나열합니다. 구성원 간의 관계에 대한 이 소셜 그래프는 커뮤니티 사이트에 대해 설정된 사용자 프로필에 포함됩니다.

## 클라이언트측 핵심 사항 {#essentials-for-client-side}

### 팔로잉 {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relations</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>포함하기 쉬워</strong></a></td>
   <td>아니요</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
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
   <td>다음을 참조하십시오 <a href="socialgraph.md">소셜 그래프 사용</a></td>
  </tr>
  <tr>
   <td><strong> 선택 사항<br /> 속성</strong></td>
   <td>
    <ul>
     <li>이름: <strong><code>outgoing</code></strong></li>
     <li>유형: 부울</li>
     <li>값:<br />
      <ul>
       <li><i>True </i>- <code>following</code> 구성 요소는 로그인한 멤버를 나열합니다. <code>follows</code></li>
       <li><i>False </i>- <code>following</code> 구성 요소는 다음과 같은 멤버를 나열합니다. <code>follow </code>로그인한 멤버</li>
      </ul> </li>
    </ul> <p>기본값은 입니다. <i>true</i> 속성이 누락된 경우. 작성자 모드에서 편집 대화 상자를 사용하여 이 속성을 설정할 수 없습니다. 속성을 의 인스턴스에 추가해야 합니다 <code>following</code> 를 사용한 노드 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### 팔로우 {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**포함하기 쉬워**](scf.md#add-or-include-a-communities-component) | 아니요 |
| **템플릿** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [클라이언트측 사용자 지정](client-customize.md)

## 서버측 Essentials {#essentials-for-server-side}

* [소셜 그래프 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [소셜 그래프 엔드포인트](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [서버측 사용자 지정](server-customize.md)
