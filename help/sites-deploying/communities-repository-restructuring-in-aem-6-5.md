---
title: Repository Recommendations for AEM Communities 6.4
seo-title: Repository Recommendations for AEM Communities 6.4
description: AEM 6.4 for Communities의 새로운 저장소 구조로 마이그레이션하기 위해 필요한 변경 방법을 알아봅니다.
seo-description: AEM 6.4 for Communities의 새로운 저장소 구조로 마이그레이션하기 위해 필요한 변경 방법을 알아봅니다.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 3%

---


# AEM Communities에 대한 리포지토리 재조정(6.5 {#repository-restructuring-for-aem-communities-in})

상위 [AEM 6.4](/help/sites-deploying/repository-restructuring.md) 페이지의 저장소 재조정 페이지에 설명된 대로 AEM 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM Communities 솔루션에 영향을 주는 저장소 변경과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업해야 하는 반면 다른 변경 사항은 향후 업그레이드 시까지 연기될 수 있습니다.

**6.5 업그레이드**

* [이메일 알림 템플릿](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [구독 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**업그레이드 전**

* [배지 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [클래식 커뮤니티 콘솔 디자인](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Facebook 소셜 로그인 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [언어 옵션 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Pinterest 소셜 로그인 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [점수 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Twitter 소셜 로그인 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [기타](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## 6.5 업그레이드 시 {#with-upgrade}

### 이메일 알림 템플릿 {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>"<code>/apps/settings</code>"에서 새 경로로 이동하려면 수동 마이그레이션이 필요합니다. [화강암 구성 관리자]를 사용하여 마이그레이션을 수행할 수 있습니다.</p> <p>"<code>/libs/settings/community/subscriptions</code>" 노드에서 속성 <code>mergeList</code>을 <code>true</code>으로 설정하고 <code>nt:unstructured</code> 하위 노드를 추가하여 마이그레이션을 수행할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

### 구독 구성 {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>"<code>/apps/settings</code>"에서 새 경로로 이동하려면 수동 마이그레이션이 필요합니다. [화강암 구성 관리자]를 사용하여 마이그레이션을 수행할 수 있습니다.</p> <p>"<code>/libs/settings/community/subscriptions</code>" 노드에서 속성 <code>mergeList</code>을 <code>true</code>으로 설정하고 <code>nt:unstructured</code> 하위 노드를 추가하여 마이그레이션을 수행할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### Watchwords 구성 {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td>Lazy Migration 작업을 사용하여 Communities 구성을 정리할 수 있습니다.<br /> <p>작업이 감시어를 <code>/etc/watchwords</code>에서 <code>/conf/global/settings/community/watchwords</code>(으)로 이동합니다.</p> <p>사용자 지정된 감시 단어가 SCM에 저장되어 있는 경우 해당 감시어를 <code>/apps/settings/...</code>에 배포해야 하며, 우선 적용되는 오버레이 <code>/conf/global/settings/...</code> 구성이 없는지 확인해야 합니다.</p> <p>마이그레이션 작업은 <code>/etc</code> 위치를 제거합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

## 업그레이드 전 {#prior-to-upgrade}

### 배지 구성 {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><strong>배지 규칙:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>배지 이미지:</strong></p> <p>기본 이미지의 경우: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>사용자 정의 이미지의 경우: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>수동 마이그레이션이 필요합니다.</p> <p>인스턴스가 배지/점수 지정 규칙을 사용자 지정한 경우 버킷 아래에 모든 규칙을 배치할 자동화된 방법은 없습니다. 사이트에 사용할 구성 버킷(글로벌 또는 사이트별)에 대한 고객 입력이 필요합니다.</p> <p>사이트에 대한 배지 지정 및 점수 구성에 사용할 수 있는 UI가 없습니다.</p> <p>새 저장소 구조에 정렬하려면 다음을 수행하십시오.</p>
    <ol>
     <li><strong>도구</strong>에서 <strong>구성 브라우저</strong>를 사용하여 사이트 컨텍스트 버킷을 만듭니다.</li>
     <li>사이트 루트로 이동</li>
     <li>모든 설정을 저장할 버킷 경로에 <code>cq:confproperty</code>을 설정합니다. 사이트 <strong>편집 마법사 - 클라우드 구성 입력 설정</strong>을 통해 동일한 항목을 설정할 수 있습니다.</li>
     <li>관련 배지 규칙 및 점수 규칙을 <code>/etc/community/*</code>에서 이전 단계에서 만든 사이트 컨텍스트 버킷으로 이동합니다.</li>
     <li>새 규칙 위치에 대한 상대 참조를 포함하도록 사이트 루트의 배지 규칙 및 점수 규칙 속성을 조정합니다.
      <ol>
       <li>예를 들어 <code>cq:conf = /conf/we-retail</code>에 대한 속성이 있는 경우, 규칙이 이제 이 새 버킷으로 이동되는 경우 <code>badgingRules [] = community/badging/rules</code>.</li>
      </ol> </li>
     <li>마찬가지로 배지 규칙 노드의 점수 지정 규칙에 대한 참조를 조정하여 상대 경로를 만듭니다.</li>
    </ol> <p> </p> <p>마지막으로 리소스를 제거하여 정리합니다. <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 클래식 커뮤니티 콘솔 디자인 {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td>N/A</td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### Facebook 소셜 로그인 구성 {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새로운 Facebook 클라우드 구성은 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ol>
       <li>AEM 제작 UI를 통해 <strong>도구 &gt; Cloud Services &gt; Facebook 소셜 로그인 구성</strong>에서 새 Facebook 소셜 로그인 구성을 수동으로 다시 만듭니다.<br /> 또는 <br /> </li>
       <li>새 Facebook 클라우드 구성을 이전 위치의 적절한 새 위치로 <code>/conf/global or /conf/&lt;tenant&gt;</code> 아래에 복사합니다.</li>
      </ol> </li>
     <li><code>[cq:Page]/jcr:content@cq:conf</code> 속성을 새 위치의 절대 경로로 설정하여 새 Facebook 소셜 로그인 구성을 참조하도록 AEM Communities 사이트 루트를 업데이트합니다.</li>
     <li>새 위치를 참조하도록 업데이트된 모든 AEM Communities 사이트 루트에서 기존 Facebook Connect Cloud Service의 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 언어 옵션 구성 {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### Pinterest 소셜 로그인 구성 {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새로운 Pinterest 클라우드 구성은 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ol>
       <li><strong>도구 &gt; Cloud Services &gt; Pinterest 소셜 로그인 구성</strong>에서 AEM 작성 UI를 통해 새 Pinterest 소셜 로그인 구성을 수동으로 다시 만듭니다.<br /> 또는</li>
       <li>새 Pinterest 클라우드 구성을 이전 위치에서 <code>/conf/global or /conf/&lt;tenant&gt;</code> 아래의 적절한 새 위치로 복사합니다.</li>
      </ol> </li>
     <li>새 위치에 있는 절대 경로로 <code>[cq:Page]/jcr:content@cq:conf</code> 속성을 설정하여 새로운 Pinterest 소셜 로그인 구성을 참조하도록 AEM Communities 사이트 루트를 업데이트합니다.</li>
     <li>새 위치를 참조하도록 업데이트된 모든 AEM Communities 사이트 루트에서 기존 Pinterest Connect Cloud Service의 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 점수 지정 구성 {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>새 저장소 구조에 맞춰 정렬하려면 점수 지정 규칙을 <code>/apps/settings/</code> 또는 /<code>conf/.../settings</code></p>
    <ol>
     <li><code>/apps/settings</code>의 경우 SCM에서 관리되는 전역 또는 기본 규칙 역할을 합니다.</li>
    </ol> <p>CRXDELite를 사용하여 <code>/conf/</code>에서 컨텍스트 인식 구성을 만듭니다.</p>
    <ol>
     <li>원하는 <code>/conf/.../settings</code> 위치<br />에 구성을 만듭니다. </li>
     <li>커뮤니티 사이트에는 <code>cq:conf </code>속성 속성이 설정되어 있어야 합니다.
      <ol>
       <li><code>cq:conf</code>이(가) 설정되지 않은 경우, 점수 지정 규칙은 사이트의 루트 노드에서 속성 '<code>scoringRules</code>'에 대한 지정된 경로에서 직접 읽습니다. 예: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>정리:리소스 제거 <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter 소셜 로그인 구성 {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>모든 새로운 Twitter 클라우드 구성은 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ol>
       <li><strong>도구 &gt; Cloud Services &gt; Twitter 소셜 로그인 구성</strong>에서 AEM 작성 UI를 통해 새 Twitter 소셜 로그인 구성을 수동으로 다시 만듭니다.<br /> 또는 <br /> </li>
       <li>새 Twitter 클라우드 구성을 이전 위치에서 <code>/conf/global or /conf/&lt;tenant&gt;</code> 아래의 적절한 새 위치로 복사합니다.</li>
      </ol> </li>
     <li><code>[cq:Page]/jcr:content@cq:conf</code> 속성을 새 위치의 절대 경로로 설정하여 새 Twitter 소셜 로그인 구성을 참조하도록 AEM Communities 사이트 루트를 업데이트합니다.</li>
     <li>새 위치를 참조하도록 업데이트된 모든 AEM Communities 사이트 루트에서 기존 Twitter Connect Cloud Service의 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 잘못된 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>Adobe은 다음 위치에서 마이그레이션 유틸리티를 제공했습니다.</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>기존 사용자 지정 템플릿은 <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>

