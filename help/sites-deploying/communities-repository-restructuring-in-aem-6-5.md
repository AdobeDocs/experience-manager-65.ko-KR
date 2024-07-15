---
title: 6.4의 AEM Communities에 대한 저장소 재구성
description: AEM 6.4 for Communities에서 새 저장소 구조로 마이그레이션하는 데 필요한 변경 작업을 수행하는 방법에 대해 알아봅니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---

# 6.5의 AEM Communities에 대한 저장소 재구성 {#repository-restructuring-for-aem-communities-in}

AEM 6.4](/help/sites-deploying/repository-restructuring.md)의 상위 [저장소 재구성 페이지에 설명된 대로 AEM 6.5로 업그레이드하는 고객은 이 페이지를 사용하여 AEM Communities 솔루션에 영향을 주는 저장소 변경 사항과 관련된 작업 노력을 평가해야 합니다. 일부 변경 사항은 AEM 6.5 업그레이드 프로세스 중에 작업이 필요하지만, 다른 변경 사항은 향후 업그레이드 전까지 연기될 수 있습니다.

**6.5 업그레이드 포함**

* [전자 메일 알림 템플릿](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [구독 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**향후 업그레이드 전**

* [구성 배지 지정](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [클래식 커뮤니티 콘솔 디자인](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Facebook 소셜 로그인 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [언어 옵션 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Pinterest 소셜 로그인 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [채점 구성](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [소셜 로그인 구성 twitter](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [기타](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## 6.5 업그레이드 포함 {#with-upgrade}

### 전자 메일 알림 템플릿 {#e-mail-notification-templates}

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
   <td><p>"<code>/apps/settings</code>" 아래의 새 경로로 이동하려면 수동 마이그레이션이 필요합니다. Granite 구성 관리자를 사용하여 마이그레이션을 수행할 수 있습니다.</p> <p>"<code>/libs/settings/community/subscriptions</code>" 노드에서 속성 <code>mergeList</code>을(를) <code>true</code>(으)로 설정하고 <code>nt:unstructured</code> 자식 노드를 추가하여 마이그레이션을 수행할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
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
   <td><p>"<code>/apps/settings</code>" 아래의 새 경로로 이동하려면 수동 마이그레이션이 필요합니다. Granite 구성 관리자를 사용하여 마이그레이션을 수행할 수 있습니다.</p> <p>"<code>/libs/settings/community/subscriptions</code>" 노드에서 속성 <code>mergeList</code>을(를) <code>true</code>(으)로 설정하고 <code>nt:unstructured</code> 자식 노드를 추가하여 마이그레이션을 수행할 수 있습니다.</p> </td>
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
   <td>지연 마이그레이션 작업을 사용하여 커뮤니티 구성을 정리할 수 있습니다.<br /> <p>작업이 watchwords를 <code>/etc/watchwords</code>에서 <code>/conf/global/settings/community/watchwords</code>(으)로 이동합니다.</p> <p>사용자 지정된 Watchwords가 SCM에 저장된 경우 <code>/apps/settings/...</code>에 배포되어야 하며 우선 순위가 높은 오버레이 <code>/conf/global/settings/...</code> 구성이 없는지 확인해야 합니다.</p> <p>마이그레이션 작업이 <code>/etc</code>개의 위치를 제거합니다.</p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

## 향후 업그레이드 전 {#prior-to-upgrade}

### 구성 배지 지정 {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>이전 위치</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>새 위치</strong></td>
   <td><p><strong>배지 규칙:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>배지 이미지:</strong></p> <p>기본 이미지의 경우: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>사용자 지정 이미지의 경우: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>구조 조정 지침</strong></td>
   <td><p>수동 마이그레이션이 필요합니다.</p> <p>인스턴스가 배지/채점 규칙을 사용자 지정한 경우 모든 규칙을 버킷에 배치하는 자동화된 방법이 없습니다. 사이트에 사용할 conf 버킷(전역 또는 사이트별)에 대한 고객 입력이 필요합니다.</p> <p>사이트에 대한 배지 및 점수를 구성하는 데 사용할 수 있는 UI가 없습니다.</p> <p>새 저장소 구조에 맞추려면 다음과 같이 하십시오.</p>
    <ol>
     <li><strong>도구</strong>의 <strong>구성 브라우저</strong>를 사용하여 사이트 컨텍스트 버킷을 만듭니다.</li>
     <li>사이트 루트로 이동</li>
     <li>모든 설정을 저장할 버킷 경로로 <code>cq:confproperty</code>을(를) 설정합니다. 사이트 <strong>편집 마법사 - 클라우드 구성 입력 설정</strong>을 통해 동일한 내용을 설정할 수 있습니다.</li>
     <li>관련 배지 규칙 및 채점 규칙을 <code>/etc/community/*</code>에서 이전 단계에서 만든 사이트 컨텍스트 버킷으로 이동합니다.</li>
     <li>새 규칙 위치에 대한 상대 참조를 갖도록 사이트 루트의 배지 규칙 및 채점 규칙 속성을 조정합니다.
      <ol>
       <li>예를 들어 <code>cq:conf = /conf/we-retail</code>에 대한 속성을 사용하는 경우 이제 규칙이 이 새 버킷으로 이동되면 <code>badgingRules [] = community/badging/rules</code>이(가) 됩니다.</li>
      </ol> </li>
     <li>마찬가지로 상대 경로를 갖도록 배지 규칙 노드에서 채점 규칙에 대한 참조를 조정합니다.</li>
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
   <td>해당 사항 없음</td>
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
   <td><p>모든 새 Facebook 클라우드 구성은 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ol>
       <li><strong>도구 &gt; Cloud Service &gt; Facebook 소셜 로그인 구성</strong>에서 AEM 제작 UI를 통해 새 Facebook 소셜 로그인 구성을 수동으로 다시 만듭니다.<br /> 또는 <br /> </li>
       <li>이전 위치에서 <code>/conf/global or /conf/&lt;tenant&gt;</code> 아래의 적절한 새 위치로 새 Facebook 클라우드 구성을 복사합니다.</li>
      </ol> </li>
     <li><code>[cq:Page]/jcr:content@cq:conf</code> 속성을 새 위치의 절대 경로로 설정하여 새 Facebook 소셜 로그인 구성을 참조하도록 AEM Communities 사이트 루트를 업데이트합니다.</li>
     <li>새 위치를 참조하도록 업데이트된 AEM Communities 사이트 루트에서 기존 Facebook Connect Cloud Service의 연결을 해제합니다.</li>
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
   <td><p>모든 새 Pinterest 클라우드 구성은 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ol>
       <li><strong>도구 &gt; Cloud Service &gt; Pinterest 소셜 로그인 구성</strong>에서 AEM 제작 UI를 통해 새 Pinterest 소셜 로그인 구성을 수동으로 다시 만듭니다.<br /> 또는</li>
       <li>이전 위치에서 <code>/conf/global or /conf/&lt;tenant&gt;</code>의 적절한 새 위치로 새 Pinterest 클라우드 구성을 복사합니다.</li>
      </ol> </li>
     <li><code>[cq:Page]/jcr:content@cq:conf</code> 속성을 새 위치의 절대 경로로 설정하여 새 Pinterest 소셜 로그인 구성을 참조하도록 AEM Communities 사이트 루트를 업데이트합니다.</li>
     <li>새 위치를 참조하도록 업데이트된 AEM Communities 사이트 루트에서 기존 Pinterest Connect Cloud Service의 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 채점 구성 {#scoring-configurations}

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
   <td><p>새 저장소 구조에 맞추기 위해 채점 규칙을 <code>/apps/settings/</code> 또는 /<code>conf/.../settings</code></p>
    <ol>
     <li><code>/apps/settings</code>의 경우 SCM에서 관리되는 전역 또는 기본 규칙으로 작동합니다.</li>
    </ol> <p>CRXDELite를 사용하여 <code>/conf/</code>에서 컨텍스트 인식 구성을 만듭니다.</p>
    <ol>
     <li>원하는 <code>/conf/.../settings</code> 위치에 구성을 만듭니다<br /> </li>
     <li>커뮤니티 사이트에 <code>cq:conf </code> 속성이 설정되어 있어야 합니다.
      <ol>
       <li><code>cq:conf</code>이(가) 설정되지 않은 경우 사이트의 루트 노드에 있는 '<code>scoringRules</code>' 속성에 대해 지정된 경로에서 채점 규칙을 직접 읽습니다. 예를 들면 다음과 같습니다. <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>정리: 리소스를 제거합니다. <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 소셜 로그인 구성 twitter {#twitter-social-login-configurations}

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
   <td><p>새 Twitter 클라우드 구성은 새 위치로 마이그레이션해야 합니다.</p>
    <ol>
     <li>이전 위치의 기존 구성을 새 위치로 마이그레이션합니다.
      <ol>
       <li><strong>도구 &gt; Cloud Service &gt; 소셜 로그인 구성 Twitter</strong>에서 AEM 작성 UI를 통해 새 Twitter 소셜 로그인 구성을 수동으로 다시 만듭니다.<br /> 또는 <br /> </li>
       <li>이전 위치에서 <code>/conf/global or /conf/&lt;tenant&gt;</code> 아래의 적절한 새 위치로 새 Twitter 클라우드 구성을 복사합니다.</li>
      </ol> </li>
     <li><code>[cq:Page]/jcr:content@cq:conf</code> 속성을 새 위치의 절대 경로로 설정하여 새 Twitter 소셜 로그인 구성을 참조하도록 AEM Communities 사이트 루트를 업데이트합니다.</li>
     <li>새 위치를 참조하도록 업데이트된 AEM Communities 사이트 루트에서 기존 Twitter 연결 Cloud Service의 연결을 해제합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>해당 없음<br /> </td>
  </tr>
 </tbody>
</table>

### 기타 {#misc}

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
   <td><p>Adobe은 다음 위치에 마이그레이션 유틸리티를 제공했습니다.</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>메모</strong></td>
   <td>기존 사용자 지정 템플릿은으로 이동합니다. <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
