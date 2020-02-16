---
title: AEM 6.5의 저장소 재구성
seo-title: AEM 6.5의 저장소 재구성
description: AEM 6.5의 리포지토리 재구성에 대해 알아봅니다.
seo-description: AEM 6.5의 리포지토리 재구성에 대해 알아봅니다.
uuid: bc577c82-3279-4ddd-898c-607864868db0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 274a7f5a-d509-4ca9-9ae5-30e48f34f171
docset: aem65
redirecttarget: /content/help/en/experience-manager/6-5/help/sites-deploying/repository-restructuring.html
translation-type: tm+mt
source-git-commit: bd0dc09ea230416ad3544d14440b7b74b80ec406

---


# AEM 6.5의 저장소 재구성 {#repository-restructuring-in-aem}

## 소개 {#introduction}

AEM 6.5 이전에 고객 코드는 업그레이드 시 변경될 수 있는 JCR의 예측할 수 없는 영역에 배포되었습니다. 이러한 이유로, 공식 AEM 릴리스(주 버전, 기능 팩, 서비스 팩 또는 핫픽스)에서 사용자 지정 코드, 구성 또는 컨텐츠를 덮어쓰는 것이 일반적입니다. 또한 고객이 AEM 제품 코드 또는 컨텐츠를 덮어써서 제품 기능을 깨는 경우도 있습니다.

이러한 충돌이 항상 자동 해결 가능하지는 않으며, 플래그를 지정하는데 상당한 처리 시간이 필요했고 해결 방법이 항상 명확하지는 않았습니다. AEM 제품 코드 및 고객 코드에 대한 계층 구조를 명확하게 구분함으로써 이러한 충돌을 방지할 수 있습니다.

이를 위해 AEM 6.5부터 시작하여 향후 릴리스에서 계속 진행할 예정인 컨텐츠는 다음 고급 규칙을 준수하면서 어디에 `/etc` 적용되는 컨텐츠에 대한 지침과 함께 저장소의 다른 폴더로 재구성됩니다.

* AEM 제품 코드는 항상 `/libs`삽입되며, 사용자 지정 코드로 덮어써서는 안 됩니다.
* 사용자 지정 코드는 `/apps`, `/content`및 `/conf`

이 아티클은 다음 세 섹션으로 구성되어 `/etc`있습니다.

1. 구성
1. 클라이언트측 라이브러리
1. 기타

각 섹션에는 다음이 포함됩니다.

* 재구성된 위치 및 추가 컨텍스트가 포함된 표. 조만간 이 탁자들이 가독성을 높이기 위해 아첨으로 된 구조로 만들어질 것으로 예상된다.
* 사용자 지정 코드가 아래 있는 AEM 애플리케이션 코드를 성공적으로 확장할 수 있도록 하는 확장성 전략입니다 `/libs`.

## 이전 버전과의 호환성 {#backwards-compatibility}

대부분의 경우 이전 위치로의 이전 호환성은 AEM 6.5로 업그레이드한 후에도 유지됩니다.이 작업은 새로운 위치가 추가되는 것 외에도 제품 코드에 의해 보존되고 존경 받는 이전 위치에 의해 수행됩니다. 대부분의 경우 조건부 논리를 사용하여 기존 폴더가 있는지 확인하고 새 위치가 아닌 여기에서 컨텐츠를 읽을 수 있습니다.

6.5 업그레이드 후 시간표를 바탕으로 고객은 이전 위치를 제거하여 새 위치의 컨텐츠를 사용하는 것이 좋습니다. 아래 표에는 위치별로 새로운 컨텐츠 구조를 유지할 수 있는 지침이 나와 있습니다.

>[!NOTE]
>
>업그레이드된 즉석 인스턴스는 새 위치 외에 이전 컨텐츠 위치를 포함합니다. 새 개발자 설치에는 새 위치만 포함됩니다.

## 표를 읽는 방법 {#how-to-read-the-tables}

각 섹션의 표는 다음과 같습니다.

* 이 컨텐츠가 관련된 AEM 솔루션(사이트, 자산, 양식 등)
* 이전(6.4 및 이전) 위치
* 새로운 6.5 위치
* 새로운 컨텐츠 구조에 맞게 조정하는 지침 예를 들어 6.5를 업그레이드한 후 몇 주 또는 몇 달 안에 스크립트를 실행하거나 파일을 수동으로 이동해야 할 수 있습니다
* 이전 버전에서 AEM 6.5로 업그레이드하는 고객을 위해 이전 컨텐츠 위치의 이전 버전과의 호환성을 유지하기 위해 AEM이 사용한 접근 방식

## 구성 {#configuration}

이 섹션의 컨텐츠 위치는 일반적으로 `/settings` 폴더 아래, `/libs``/apps`또는 `/conf`폴더에 있는 컨텐츠를 나타냅니다.

### 확장성 전략 {#extensibility-strategy}

일반적으로 몇 가지 예외를 제외하고 이 섹션 아래의 내용은 Apache Sling의 컨텍스트 인식 구성 기능을 사용하여 확장할 수 [ 있습니다](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) .

간단히 말해, 컨텍스트 인식 구성을 사용하면 저장소의 한 부분에 있는 컨텐츠를 저장소의 다른 부분에 있는 컨텐츠별로 여러 번 오버레이할 수 있습니다. 예를 들어 의 컨텐츠를 의 컨텐츠에 의해 오버레이할 `/libs` 수 `/apps`있으며, 이렇게 하면 컨텐츠에 의해 오버레이될 수 `/conf`있습니다. 또한 아래 글로벌 폴더의 컨텐츠를 특정 &quot;테넌트&quot; 또는 &quot;사이트&quot;(예: `/conf` 
     `/conf/we-retail/settings`).

일반적으로 컨텍스트 인식 구성은 기능 구성을 확장하기 위한 전략으로 사용되지만 다른 컨텐츠 유형에서 사용되는 경우도 있습니다.

아래 표에는 &quot;구성 유형&quot;이라는 추가 열이 있어 구성을 오버레이할 수 있는 범위를 설명합니다. 다음은 이러한 구성 유형에 대한 추가 정보입니다.

**컨텍스트 인식 안 함**

* 리소스가 컨텍스트 인식 폴더 구조(예: `/libs/settings`)에 있지만 절대 경로를 통해 항상 참조되므로 컨텍스트 인식이 적용되지 않습니다.
* 어디에서나 리소스 활용 예를 들어 자산 DRM 라이센스는 `/content/my-customer/licenses/creative-commons.html`
* 예:

   * 워크플로우 스크립트 -> `/apps/settings/workflow/scripts/noop.ecma`
   * 자산 DRM 라이선스 -> `/apps/settings/dam/drm/my-license`

**only global**

* 전역 구성만 있는 기능
* 다음 예에서는 참조점으로 설정보다 우선합니다. `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global`

* AEM은 글로벌 구성만 지원하며 임차인 지정 구성은 지원하지 않습니다.
* AEM은 항상 /conf/global 수준에서 구성을 먼저 찾기 시작합니다.

* 예:

   * 워크플로 런처 -> `/libs/settings/workflow/launcher`
   * 워크플로우 모델 -> `/conf/global/settings/workflow/models`

**임차인 인식**

* 테넌트 인식 구성의 경우 다음 예제에 구성 경로의 우선 순위를 참조하십시오.&lt; `/libs/settings` &lt; `/apps/settings` `/conf/global` &lt; `/conf/we-retail`, where we-retail은 임차인 이름입니다. 테넌트 인식 구성은 하위 세입자를 지원합니다.

* AEM 파섹 계층 구조의 `cq:conf` 속성을 준수합니다.
* 예:

   * 편집 가능한 템플릿 -> `/conf/we-retail/settings/wcm/templates`
   * 클라우드 구성 -> `/conf/we-retail/settings/cloudsettings`

<table>
 <tbody>
  <tr>
   <td><strong>솔루션</strong></td>
   <td><strong>이전 위치</strong><br /> </td>
   <td><strong>새 위치</strong></td>
   <td><strong>컨텍스트 인식 구성 유형</strong><br /> </td>
   <td><strong>이전 버전과의 호환성 방법</strong></td>
   <td><strong>최신 모델에 맞게 요구 사항 조정</strong></td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Forms</td>
   <td><p><code>/etc/cloudservices/typekit</code></p> <p><code>/etc/cloudservices/recaptcha</code></p> <p><code>/etc/cloudservices/echosign</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/typekit</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/recaptcha</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/echosign</code></p> </td>
   <td>임차인 인식</td>
   <td><p>기존 클라우드 서비스.</p> <p>즉석 업그레이드를 계속 진행합니다. AEM에 폴백으로 여전히 표시되는 목록 작성 및 읽기 코드입니다.</p> </td>
   <td>Lazy content migration 유틸리티는 Forms Migration UI에 의해 트리거될 수 있으므로 새 경로로 자동으로 변환할 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>AEM 양식</td>
   <td><code>/etc/cloudservices/fdm</code></td>
   <td><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/fdm</code></td>
   <td>임차인 인식</td>
   <td><p>기존 클라우드 서비스.</p> <p>업그레이드된 즉석 설정을 유지합니다. AEM에 폴백으로 여전히 표시되는 목록 작성 및 읽기 코드입니다.</p> </td>
   <td>Lazy content migration 유틸리티는 Forms Migration UI에 의해 트리거될 수 있으므로 새 경로로 자동으로 변환할 수 있습니다.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/adhocassetshare</code></td>
   <td><code>/libs/settings/dam/adhocassetshare</code></td>
   <td>임차인 인식</td>
   <td>기존 컨텐츠 구조는 새로운 OOTB 컨텐츠 구조에 비해 우선 순위가 높습니다.</td>
   <td>프로젝트 수준 사용자 지정을 잘라내어 해당되는 <code>/apps</code> 경로 또는 <code>/conf</code> 경로에 붙여넣어야 합니다.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
   <td><code>/libs/settings/dam/workflow</code></td>
   <td>임차인 인식</td>
   <td>기존 컨텐츠 구조는 새로운 OOTB 컨텐츠 구조에 비해 우선 순위가 높습니다.</td>
   <td>프로젝트 수준 사용자 지정을 잘라내어 해당되는 <code>/apps</code> 경로 또는 <code>/conf</code> 경로에 붙여넣어야 합니다.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/drm/licenses/</code></td>
   <td><code>/libs/settings/dam/drm</code></td>
   <td>컨텍스트 인식 안 함</td>
   <td>기존 컨텐츠 구조는 새로운 OOTB 컨텐츠 구조에 비해 우선 순위가 높습니다.</td>
   <td>프로젝트 수준 사용자 지정을 잘라내어 해당되는 <code>/apps</code> 경로 또는 <code>/conf</code> 경로에 붙여넣어야 합니다.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/indesign/scripts</code></td>
   <td><code>/libs/settings/dam/indesign</code></td>
   <td>임차인 인식</td>
   <td>기존 컨텐츠 구조는 새로운 OOTB 컨텐츠 구조에 비해 우선 순위가 높습니다.</td>
   <td><p>프로젝트 수준 사용자 지정을 잘라내어 해당되는 <code>/apps</code> 경로 또는 <code>/conf</code> 경로 아래에 붙여넣어야 합니다.</p> <p>사용자 정의된 자산 처리 작업 과정을 실행할 때, /etc의 이전 위치에 대한 참조는 미디어 추출 프로세스 구성에 여전히 존재합니다. 스크립트를 /etc에서 /apps 및 /conf 경로로 이동하는 것과 함께 사용자 정의된 미디어 추출 프로세스 인수를 변경 사항에 맞게 절대 경로에서 상대 경로로 변경해야 합니다.</p> <p>자세한 내용은 <a href="https://helpx.adobe.com/experience-manager/6-2/help/assets/indesign.html">이 페이지를</a>참조하십시오.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video</code></td>
   <td><code>/libs/settings/dam/video</code></td>
   <td>임차인 인식</td>
   <td>기존 컨텐츠 구조는 기본적으로 새로운 컨텐츠 구조보다 우선 순위가 높습니다.</td>
   <td>프로젝트 수준 사용자 지정을 잘라내어 해당되는 <code>/apps</code> 경로 또는 <code>/conf</code> 경로에 붙여넣어야 합니다.</td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/notification/email/default</code></td>
   <td><code>/libs/settings/dam/notification</code></td>
   <td>임차인 인식</td>
   <td>기존 컨텐츠 구조는 기본적으로 새로운 컨텐츠 구조보다 우선 순위가 높습니다.</td>
   <td>프로젝트 수준 사용자 지정을 잘라내어 해당되는 <code>/apps</code> 경로 또는 <code>/conf</code> 경로에 붙여넣어야 합니다.</td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Assets</td>
   <td><code>/etc/designs</code> </td>
   <td><code>/libs/settings/wcm/designs</code></td>
   <td>컨텍스트 인식 안 함</td>
   <td><p>서비스 소비는 이전 위치를 인식합니다.</p> <p>기존 위치의 구성은</p> </td>
   <td><br /> 새로운 저장소 구조에 맞게 사용자 정의 컨텐츠를 <code>/etc/design</code> 에서 <code>/apps/settings/wcm/design</code> 로 이동합니다. 향후 디자인 모드와 이 컨텐츠의 필요성을 대체하는 편집 가능한 템플릿 기능을 사용하도록 사이트를 업그레이드하는 것이 좋습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/scaffolding</code></td>
   <td><p><code>/libs/settings/wcm/template-types/scaffolding/scaffolding</code></p> <p><code>/apps/settings/wcm/template-types/scaffolding/scaffolding</code></p> </td>
   <td>텍스트 인식 안 함</td>
   <td>이전 위치의 구성 요소는 계속 <code>/etc/scaffolding</code> 작동하지만 더 이상 사용되지 않습니다.</td>
   <td>새 위치 아래에 새 Scaffold 구성 요소를 사용하는 것이 좋습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/blueprints</code></td>
   <td><p>기본 스크린 및 상거래 블루프린트 구성을 위한 /libs/msm</p> <p> </p> </td>
   <td>컨텍스트 인식 안 함</td>
   <td><p>서비스 소비는 이전 위치를 인지합니다.</p> <p>기존 위치의 구성이 고려됩니다.</p> </td>
   <td>구성을 새 위치로 복사해야 합니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/mobile</code></td>
   <td><code>/libs/settings/mobile</code></td>
   <td>임차인 인식</td>
   <td>이 기능은 Configuration Manager를 활용하며 여전히 이전 위치를 폴백으로 지원합니다.</td>
   <td>
    <ol>
     <li>구성을 에서 <code>/etc</code> 로 재배치 <code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li>그런 다음 컨텐츠의 참조를 다음과 같이 업데이트합니다.</li>
    </ol> <p><code>/content/&lt;tenant&gt;/jcr:content/cq:deviceGroups{String[]}=mobile/groups/responsive</code></p> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/msm/rolloutConfigs</code></td>
   <td><code>/libs/msm/wcm/rolloutconfigs</code></td>
   <td>N/A</td>
   <td><p>기존 위치에 대해 서비스 소비가 인식됩니다.</p> <p>기존 위치에서 구성이 감지되면 사용됩니다.</p> </td>
   <td>새 모델에 맞게 새 위치에 구성을 만들어야 하며 아래 이전 위치는 삭제해야 <code>/etc</code> 합니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/segmentation/contexthub</code></td>
   <td><code>/conf/we-retail/settings/wcm/segments</code></td>
   <td>임차인 인식</td>
   <td><p>이전 위치의 세그먼트:</p>
    <ul>
     <li>대상 콘솔에서 읽기 전용 모드로 유지됩니다.</li>
     <li>페이지 속성 &gt; 개인화 &gt; 세그먼트 경로에서 지정된 경로를 선택한 <strong>경우 여전히 페이지에 로드됩니다</strong>.</li>
     <li>컨텐츠 타깃팅에 사용할 수 있습니다.</li>
    </ul> </td>
   <td>세그먼트 마이그레이션 <a href="/help/sites-deploying/upgrading-code-and-customizations.md#migrateconfigurations">도구를 사용하여</a> 새 위치로 마이그레이션할 수 있습니다.</td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/social/config/languageOpts</code></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
   <td>N/A</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/templates</code></td>
   <td><code>/libs/settings/community/templates</code></td>
   <td> </td>
   <td><p>코드는 이전 템플릿의 위치를 인식합니다. 기존 템플릿은 계속 참조되고 읽기/쓰기가 <code>/etc</code>수행됩니다.</p> <p><br /> 이메일 템플릿의 경우, 고객이 AEM Communities 이메일 회신 구성에서 템플릿 루트 <strong>경로를</strong> 구성하여 <strong>사용자 지정</strong> 템플릿을 이미 다른 경로로 가지고 있는 경우에는 그대로유지됩니다.</p> </td>
   <td><p>마이그레이션 <a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration" target="_blank">유틸리티는</a> 최신 AEM Communities 템플릿 모델에 정렬할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/badging</code></td>
   <td><p><strong>배지 규칙:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>배지 이미지:</strong></p> <p>의 이전 위치에 있는 기본 이미지는 다음 위치로 <code>/etc/community/badging/images</code> 이동합니다. <code>/libs/community/badging/images </code> </p> <p> </p> <p>사용자 정의 이미지가 로 <code>/content/community/badging/images</code>이동됩니다.</p> <p> </p> </td>
   <td>임차인 인식</td>
   <td><p>코드는 이전 배지 경로에 대해 인식합니다.</p> <p><br /> 먼저 이전 경로가<br /> 있는지 확인합니다. 없는 경우 새 경로를 사용합니다.</p> </td>
   <td><p>최신 모델에 맞게 수동 마이그레이션이 필요합니다. 아래 단계에 따라 이 작업을 수행하십시오.</p>
    <ol>
     <li>도구 아래의 구성 브라우저를 사용하여 사이트 컨텍스트 버킷 <strong>만들기</strong></li>
     <li>사이트 루트로 이동</li>
     <li>모든 구성을 저장할 버킷 경로로 <code>cq:conf</code> 속성을 설정합니다. 사이트 편집 마법사 - 클라우드 <strong>구성 입력을 설정한 다음 변경 내용을 저장할</strong>수 있습니다.</li>
     <li>관련 배지 규칙 및 점수 규칙을 이전 단계에서 만든 사이트 컨텍스트 버킷으로 <code>etc/community/*</code> 이동합니다.</li>
     <li>사이트 루트의 <code>badgingRules</code> 및 <code>scoringRules</code> 속성을 조정하여 새 규칙 위치에 대한 상대 참조를 만듭니다. 예를 들어, 를 <code>cq:conf</code> 로 <code>/conf/we-retail</code>설정하면 규칙이 이제 이 새 버킷으로 이동되는 <code>badgingRules</code> 경우 값이 <code>community/badging/rules</code> 됩니다</li>
     <li>마찬가지로 배지 규칙 노드의 점수 지정 규칙에 대한 참조를 조정하여 상대 경로를 지정합니다.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/cloudservices/facebookconnect</code></p> <p><code>/etc/cloudservices/twitterconnect</code></p> <p><code>/etc/cloudservices/pinterestconnect</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> </td>
   <td>임차인 인식</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/scoring</code></td>
   <td><code>/libs/settings/community/scoring</code></td>
   <td> </td>
   <td><p>코드는 이전 배지 경로에 대해 인식합니다.</p> <p><br /> 먼저 이전 경로가<br /> 있는지 확인합니다. 없는 경우 새 경로를 사용합니다.</p> </td>
   <td><p>최신 모델에 맞게 수동으로 마이그레이션해야 합니다.</p> <p>위의 배지 규칙에서는 단계가 동일합니다.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/notifications</code></td>
   <td><code>/libs/settings/community/notifications</code></td>
   <td>컨텍스트 인식 안 함</td>
   <td><p>이러한 구성은 이전 버전과 호환되지 않습니다. 새 위치로 마이그레이션하는 방법에 대한 단계는 "최신 모델에 맞게 정렬하는 요구 사항" 열을 참조하십시오.<br /> </p> <br /> </td>
   <td><p>최신 모델에 맞게 수동으로 마이그레이션해야 합니다. [MOCK] You can use the configuration to move the new path to the under <code>/apps/settings</code>.</p> <p>따라서 <code>mergeList</code> 노드에서 <code>/libs/settings/community/subscriptions</code> 속성을 true로 설정한 다음 <code>nt:unstructured</code> 자식 노드를 추가해야 합니다.<br /> </p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/subscriptions</code></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
   <td>컨텍스트 인식 안 함</td>
   <td>이러한 구성은 이전 버전과 호환되지 않습니다. 새 위치로 마이그레이션하는 방법에 대한 단계는 "최신 모델에 맞게 정렬하는 요구 사항" 열을 참조하십시오.</td>
   <td><p>최신 모델에 맞게 수동으로 마이그레이션해야 합니다. [MOCK] You can use the configuration to move the new path to the under <code>/apps/settings</code>.</p> <p>따라서 <code>mergeList</code> 노드에서 <code>/libs/settings/community/subscriptions</code> 속성을 true로 설정한 다음 <code>nt:unstructured</code> 자식 노드를 추가해야 합니다.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/socialconfig/srpc/defaultconfiguration</code></td>
   <td><code>/conf/global/settings/community/srpc/defaultconfiguration</code></td>
   <td>글로벌</td>
   <td>이러한 구성은 이전 버전과 호환됩니다. 이전 경로가 검색되면 사용됩니다. 그렇지 않으면 새 경로가 우선합니다.</td>
   <td><p>게으른 컨텐츠 마이그레이션 작업은 <code>CQ64CommunitiesConfigsCleanupTask</code>의 형태로 사용할 수 있습니다.</p> <p>자세한 내용은 <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">레이지 마이그레이션 설명서를</a>참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/watchwords</code></td>
   <td><code>/libs/community/watchwords</code></td>
   <td>N/A</td>
   <td>이러한 구성은 이전 버전과 호환됩니다. 이전 경로가 검색되면 사용됩니다. 그렇지 않으면 새 경로가 우선합니다.</td>
   <td><p>게으른 컨텐츠 마이그레이션 작업은 <code>CQ64CommunitiesConfigsCleanupTask</code>의 형태로 사용할 수 있습니다.</p> <p>감시 단어는 수동으로 에서 <code>/etc/watchwords</code> 로 이동해야 <code>/conf/global/settings/community/watchwords</code>합니다.</p> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code> </p> <p><code>/var/workflow/models</code></p> </td>
   <td>글로벌</td>
   <td><p>이전 위치는 <code>/libs</code> 또는 에 구성이 없는 경우 사용됩니다 <code>/conf</code>.</p> <p>OOTB 워크플로우 모델을 편집할 때 컨텍스트 인식 오버레이를 만들어 수정할 수 <code>/conf</code> 있도록 해야 합니다.</p> <p>패키지 내보내기에 모델을 포함하거나 런타임 모델을 <code>/libs</code> 포함시켜야 <code>/conf</code> 합니다. <code>/var/workflow/models.</code></p> </td>
   <td><p>새로 만든 모델이 <code>/conf/global/settings</code> 해당 위치에 생성됩니다.</p> <p>편집 작업을 수행하기 <code>/etc</code> <code>/libs</code> <code>/conf/global/settings</code> 전에 에서 편집하거나 재정의해야 하는 경우 편집 단추를 선택해야 재정의 기능이 만들어지고 편집이 <code>/conf</code> 허용됩니다.</p> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/workflow/launcher</code></td>
   <td><p><code>/libs/settings/workflow/launcher</code></p> <p><code>/conf/global/settings/workflow/launcher</code></p> </td>
   <td>글로벌</td>
   <td>이전 위치는 존재하는 경우 사용되며 구성이<br /> <code>/libs</code> 또는 <code>/conf</code> 위치에 존재하지 않는 경우에 사용됩니다. 이렇게, 맞춤형 방사선은 보존됩니다.</td>
   <td><p>새로 만들거나 편집한 실행 프로그램 구성은 해당 <code>/conf</code> 위치에 있습니다.</p> <p>모든 방사포는 기존 <code>/etc</code> 위치에서<code> /conf/global/settings/workflow/launcher.</code></p> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> </td>
   <td>글로벌</td>
   <td>이전 위치는 존재하는 경우 사용되며 구성이<br /> <code>/libs</code> 또는 <code>/conf</code> 위치에 존재하지 않는 경우에 사용됩니다. 이렇게 하면 사용자 정의 워크플로우 모델이 유지됩니다.</td>
   <td><p>모든 워크플로우 모델은 이전 <code>/etc</code> 위치에서 (으)로 이동되어야 합니다 <code>/conf/global/settings/workflow/models</code>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/workflow/notification</code></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
   <td>컨텍스트 인식 안 함</td>
   <td><p>이전 버전과의 호환성을 위해 기존 위치가 있을 경우 사용됩니다.</p> <p>이전에는 기본 템플릿을 편집할 때 무시해야 <code>/etc</code>했습니다. 이제 재정의는 에 저장해야 합니다 <code>/conf/global</code>.</p> </td>
   <td>자세한 내용은 Workflow 설명서를 참조하십시오.<br /> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/cloudservices/translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> <p> </p> </td>
   <td>임차인 인식</td>
   <td>기존 클라우드 서비스. 업그레이드된 설정 위치에 유지됩니다. 이러한 항목을 나열하고 읽을 수 있는 코드는 여전히 대비책으로 제품에 있습니다.</td>
   <td><p>클라우드 구성을 다음으로 이동하려면 다음 중 <code>/conf</code>하나를 수행합니다.</p>
    <ul>
     <li>새로운 터치 UI를 사용하여 구성<br /> 만들기 또는<br /> </li>
     <li>구성을 <code>/etc/cloudservices/translation</code> 새 위치로 복사</li>
    </ul> <p>이 작업이 완료되면, 구성은 사용자 인터페이스에서 사이트 &gt; <strong>속성을 통해</strong> 사이트와 연결해야 합니다.</p> <p><em>참고:이 작업을 수행하려면 번역 커넥터가 AEM 6.5와 호환되어야 합니다.</em></p> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/cloudservices/msft-translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/msft-translation</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/msft-translation</code></p> </td>
   <td>임차인 인식</td>
   <td>기존 클라우드 서비스. 업그레이드된 설정 위치에 유지됩니다. 이러한 항목을 나열하고 읽을 수 있는 코드는 여전히 대비책으로 제품에 있습니다.</td>
   <td><p>클라우드 구성을 다음으로 이동하려면 다음 중 <code>/conf</code>하나를 수행합니다.</p>
    <ul>
     <li>새로운 터치 UI를 사용하여 구성 만들기 또는<br /> </li>
     <li>이전 구성을 <code>/etc/cloudservices/translation</code> 새 위치로 복사</li>
    </ul> <p>이 작업이 완료되면, 구성은 사용자 인터페이스에서 사이트 &gt; <strong>속성을 통해</strong> 사이트와 연결해야 합니다.</p> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/cloudsettings</code></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
   <td>임차인 인식</td>
   <td><p>인스턴스 업그레이드에 대한 기존 항목은 그대로 <code>/etc</code> 유지됩니다.</p> <p>업그레이드 후 클라우드 설정 UI에 액세스하면 이전 버전과의 호환성을 위해 기존 컨텐츠를 그대로 유지하면서 기존 클라우드 설정을 새 저장소 구조에 복사합니다.</p> </td>
   <td><p>컨텐츠 모델은 동일하며, 컨텍스트 인식 구성에 맞게 위치가 변경되었습니다.</p> <p>이러한 <a href="/help/sites-deploying/lazy-content-migration.md">클라우드 설정을 포함하는 레이지 마이그레이션 작업은</a> 다음 작업을 수행합니다.</p>
    <ul>
     <li>기존 클라우드 설정을 <code>/etc/cloudsettings</code> <code>/conf/global/settings/cloudsettings</code></li>
     <li>모든 하위 항목 제거 <code>/etc/cloudsettings</code></li>
    </ul> <p>그러나 업그레이드 후 또는 지연 마이그레이션 작업을 실행하기 전에 필요한 수동 단계는 다음과 같습니다.</p>
    <ul>
     <li>가리키는 모든 참조를 업데이트하여 <code>/etc/cloudsettings/*</code> <code>/conf/global</code></li>
    </ul> <p>Caveat:</p>
    <ul>
     <li>컨테이너를 <code>/etc/cloudsettings</code> 보존해야 합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
   <td>only global</td>
   <td><p>다이내믹 미디어에 대한 클라우드 구성 - Scene7(<code>dynamicmedia_scene7</code> runmode) 설정은 동일한 위치에 유지됩니다. 이 과정은 그대로 작동합니다. 클라우드 구성 값을 조정해야 하는 경우 다음 두 가지 옵션을 사용할 수 있습니다.</p>
    <ol>
     <li>기존 클라우드 구성 UI를 통해 기존 구성을 업데이트합니다.</li>
     <li>새 터치 UI를 통해 새 클라우드 구성을 만듭니다. 이것은 이전 것보다 더 높은 우선순위를 갖게 될 것이다.</li>
    </ol> </td>
   <td><p>최신 모델에 정렬하려면 다음 위치에 있는 스크립트를 실행해야 합니다.</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/viewer</code></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
   <td>only global</td>
   <td><p>OOTB 뷰어 사전 설정은 새 위치에서만 사용할 수 있으며, 사용자 정의 뷰어 사전 설정은 수정 작업이 발생할 때까지 계속 아래에 <code>/etc</code> 있습니다.</p> <p>수정된 후에는 레이지 마이그레이션을 통해 새 위치에 저장됩니다. 내장 이미지 서버는 요청을 받을 때 이전 경로와 새 경로를 모두 봅니다. 따라서 임베드 코드나 URL을 변경할 필요가 없습니다.</p> </td>
   <td><p>기본 뷰어 사전 설정은 새 위치에서만 사용할 수 있습니다. 사용자 정의 뷰어 사전 설정의 경우 다음 위치에서 마이그레이션 스크립트를 실행해야 합니다.</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p>이전 버전과의 호환성 케이스와 마찬가지로 copyURL/포함 코드를 조정할 필요가 <code>/conf</code>없습니다. 기존 요청은 백그라운드에서 올바른 컨텐츠로 다시 <code>/etc</code> 라우팅됩니다 <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/imageserver/macros</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
   <td>only global</td>
   <td>아래 매크로는 <code>/etc</code> 여전히 유효합니다. 수정하면 수정된 노드가 레이지 마이그레이션 작업을 통해 새 위치로 이동됩니다 <code>/conf</code> .</td>
   <td><p>다음 위치에서 마이그레이션 스크립트를 실행해야 합니다.</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia/Adaptive Video Encoding</code></td>
   <td><code>/libs/settings/dam/dm/presets/video/jcr:content/Adaptive Video Encoding</code></td>
   <td>N/A</td>
   <td><p>프로필로 연결되는 자산 폴더 속성을 업데이트하지 않으면 기본 비디오 프로필이 제거됩니다.</p> <p>인코딩 프로세스에서는 이전 위치와 새 위치 간에 번역이 내장되어 있습니다. 이전 경로를 새 프로필 경로로 변환합니다.</p> </td>
   <td>변경이 필요하지 않습니다.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
   <td>only global</td>
   <td><p>사용자 정의 비디오 프로필은 수정할 때까지 그대로 유지됩니다.</p> <p>그런 다음 레이지 마이그레이션 작업을 통해 새 위치로 이동합니다. 이는 인코딩 조회 시 즉시 사용할 수 있는 비디오 사전 설정과 유사합니다. 인코딩 프로세스에는 먼저 이전 위치를 찾은 다음 비디오 프로필의 새 위치를 확인할 수 있는 내장 경로 변환기가 있습니다.</p> </td>
   <td><p>최신 모델에 맞게 다음 위치에서 마이그레이션 스크립트를 실행할 수 있습니다.</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
   <td>only global</td>
   <td><p>Dynamic Media 하이브리드 설정(<code>dynamicmedia</code> runmode)에 대한 이 클라우드 구성은 동일한 위치에 유지됩니다. 이 프로세스는 그대로 작동합니다. 구성 값을 조정해야 하는 경우 두 가지 방법으로 조정할 수 있습니다.</p>
    <ol>
     <li>기존 클라우드 구성 UI를 통해 기존 구성을 업데이트합니다.</li>
     <li>새 터치 UI를 통해 새 클라우드 구성을 만듭니다. 이것은 이전 것보다 더 높은 우선순위를 갖게 될 것이다.</li>
    </ol> </td>
   <td><p>최신 모델에 맞게 마이그레이션 스크립트를 실행해야 합니다. 다음 위치에서 스크립트를 찾을 수 있습니다.<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/youtube</code></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
   <td>only global</td>
   <td><p>DM-Youtube 설정에 대한 클라우드 구성이 동일한 위치에 유지됩니다. 이 프로세스는 그대로 작동합니다. 클라우드 구성 값을 조정해야 하는 경우 다음 두 가지 방법으로 조정할 수 있습니다.</p>
    <ol>
     <li>기존 클라우드 구성 UI를 통해 기존 구성을 업데이트합니다.</li>
     <li>새 터치 UI를 통해 새 클라우드 구성을 만듭니다. 이것은 이전 것보다 더 높은 우선순위를 갖게 될 것이다.</li>
    </ol> </td>
   <td><p>마이그레이션 스크립트를 실행하여 최신 모델에 정렬할 수 있습니다. 스크립트는 다음 위치에 있습니다.<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/analytics</code></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
   <td>only global</td>
   <td>필요한 작업이 없습니다.</td>
   <td><p>마이그레이션 스크립트를 실행하여 최신 모드에 맞게 정렬할 수 있습니다. 스크립트는 다음 위치에 있습니다.<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><p><code>/etc/notification/email/default/com.day.cq.replication</code></p> <p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
   <td><code>/libs/settings/notification-templates</code></td>
   <td>only global</td>
   <td>의 템플릿이 의 템플릿보다 <code>/etc/notification/email/default/</code> 우선합니다 <code>/libs/settings/notification-templates</code>.</td>
   <td>최신 모델에 맞게 새 템플릿을 만들고 여기에서 새 <code>/apps/settings/notification-templates</code> 수정을 수행할 수 있습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/msm/rolloutconfigs/launch</code></p> <p><code>/etc/msm/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td><p><code>/libs/msm/launches/rolloutconfigs/launch</code></p> <p><code>/libs/msm/launches/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td>N/A</td>
   <td><p>서비스 소비는 이전 위치를 인지합니다.</p> <p>기존 위치에서 구성이 감지되면 사용됩니다.</p> </td>
   <td>새 모델에 맞게 새 위치에 구성을 만들어야 하며 아래 이전 위치는 삭제해야 <code>/etc</code> 합니다.</td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/translation/supportedLanguages</code></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
   <td>컨텍스트 인식 안 함</td>
   <td>주의 사항은 사용자 정의된 언어를 목록에 추가해야 한다는 것입니다.<br /> </td>
   <td>새 목록을 추가 언어(있는 경우)로 오버레이하고 업데이트합니다. 또는 이전 목록을 <code>/apps</code> 위치에 복사하는 것도 작동합니다.</td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
   <td>only global</td>
   <td>업그레이드된 즉석 설정에서 유지됩니다. 코드를 작성하여 제품에 여전히 포함되어 있는지 확인합니다.</td>
   <td>변경 내용을 유지하려면 XML 파일을 에서 <code>/etc</code> 또는 <code>/libs</code> 으로 복사하십시오 <code>/conf</code>. 또는 에서<strong> 파일을 </strong>제거합니다 <code>/etc</code>.</td>
  </tr>
 </tbody>
</table>

## 클라이언트측 라이브러리 {#client-side-libraries}

[클라이언트측 라이브러리는](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/clientlibs.html) 브라우저에서 처리되는 javascript 및 CSS 코드입니다.

### 확장성 전략 {#extensibility-strategy-1}

AEM에서는 여러 JavaScript 파일을 추가할 수 있는 확장 프레임워크를 제공합니다. 동일한 &quot;카테고리&quot; 속성을 가진 모든 파일이 추가되어 사용자 지정 코드가 아래에 있는 AEM 코드를 확장할 수 `/libs`있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>솔루션</strong></td>
   <td><strong>이전 위치</strong><br /> </td>
   <td><strong>새 위치</strong></td>
   <td><strong>이전 버전과의 호환성 방법</strong></td>
   <td><strong>최신 모델에 맞게 요구 사항 조정</strong></td>
  </tr>
  <tr>
   <td>AEM 양식</td>
   <td><code>/etc/clientlibs/fd/fp</code></td>
   <td><code>/libs/fd/fp/components</code></td>
   <td><p>즉석 업그레이드를 통해 업그레이드된 인스턴스에서 유지될 이전 clientlib입니다.</p> <p>새 clientlibs는 이전 및 새 clientlibs의 병합을 방지하기 위해 "<strong><code>replaces</code></strong>" 속성과 함께 동일한 카테고리 이름을 갖습니다.</p> </td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM 양식</td>
   <td><code>/etc/clientlibs/fd/rte</code></td>
   <td><code>/libs/fd/rte</code></td>
   <td><p>즉석 업그레이드를 통해 업그레이드된 인스턴스에서 유지될 이전 clientlibs입니다.</p> <p>새 clientlibs는 이전 및 새 clientlibs의 병합을 방지하기 위해 "<strong><code>replaces</code></strong>" 속성과 함께 동일한 카테고리 이름을 갖습니다.</p> </td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM 양식</td>
   <td><code>/etc/clientlibs/fd/af</code></td>
   <td><code>/libs/fd/af/authoring/clientlibs</code></td>
   <td>레거시 클라이언트 즉석 업그레이드를 통해 업그레이드된 인스턴스에서 유지됩니다. 새 clientlibs는 이전 및 새 clientlibs의 병합을 방지하기 위해 "<strong><code>replaces</code></strong>" 속성과 함께 동일한 카테고리 이름을 갖습니다.</td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM 양식</td>
   <td><code>/etc/clientlibs/fd/themes/themeLibrary</code></td>
   <td>더 이상 AEM 6.5의 일부로 제공되지 않습니다.</td>
   <td><p>적응형 양식의 테마 활용</p> <p>업그레이드된 즉석 설정에서 유지됩니다.</p> </td>
   <td>일부 사용자가 생성한 컨텐츠입니다. 이것은 <code>aem-forms-reference-themes</code> 이름이 있는 참조 컨텐츠 패키지로 전달됩니다.</td>
  </tr>
  <tr>
   <td>AEM 양식</td>
   <td><code>/etc/clientlibs/fd/expeditor</code></td>
   <td><code>/libs/fd/expeditor/clientlibs</code></td>
   <td>레거시 클라이언트 즉석 업그레이드를 통해 업그레이드된 인스턴스에서 유지됩니다. 새 clientlibs는 이전 및 새 clientlibs의 병합을 방지하기 위해 "<strong><code>replaces</code></strong>" 속성과 함께 동일한 카테고리 이름을 갖습니다.</td>
   <td>필요한 작업이 없습니다.<p> </p> </td>
  </tr>
  <tr>
   <td>AEM 양식</td>
   <td><code>/etc/clientlibs/fd/fmaddon</code></td>
   <td><code>/libs/fd/fmaddon</code></td>
   <td>직접 소비되지 않도록 되어 있는 기존 Analytics 및 Target 클라이언트 </td>
   <td>정리 필터를 사용하여 업그레이드 후 정리했습니다.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
   <td><code>/libs/dam/clientlibs</code></td>
   <td>이전 클라이언트에는 다른 클라이언트 카테고리 이름이 있습니다.</td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td> </td>
   <td><code>/etc/clientlibs/ckeditor</code></td>
   <td><code>/libs/clientlibs/ckeditor</code></td>
   <td>레거시 클라이언트입니다. 업그레이드된 즉석 설정에서 유지됩니다. 새 clientlibs는 이전 및 새 clientlibs 병합을 방지하기 위해 "<code>replaces</code>" 속성과 함께 동일한 카테고리 이름을 가집니다.</td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/sitecatalyst</code></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
   <td><p>레거시 클라이언트입니다. 업그레이드된 즉석 설정에서 유지됩니다.</p> <p>새 clientlibs의 카테고리 이름이 동일합니다.</p> </td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/personalization</code></td>
   <td><code>/libs/cq/personalization/clientlibs/personalization</code></td>
   <td><p>레거시 클라이언트입니다. 업그레이드된 즉석 설정에서 유지됩니다.</p> <p>새 clientlibs의 카테고리 이름이 동일합니다.</p> </td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/searchpromote</code></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
   <td><p>레거시 클라이언트입니다. 업그레이드된 즉석 설정에서 유지됩니다.</p> <p>새 clientlibs의 카테고리 이름이 동일함</p> </td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/target</code></td>
   <td><code>/libs/cq/target/clientlibs/target</code></td>
   <td><p>레거시 클라이언트입니다. 업그레이드된 즉석 설정에서 유지됩니다.</p> <p>새 clientlibs의 카테고리 이름이 동일합니다.</p> </td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/address</code></td>
   <td><code>/libs/cq/address/clientlibs</code></td>
   <td>새 clientlibs의 카테고리 이름이 동일합니다.</td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation</code></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
   <td>레거시 클라이언트 업그레이드된 즉석 설정에서 유지됩니다. 새 clientlibs는 이전 및 새 clientlibs의 병합을 방지하기 위해 "<strong>교체</strong>" 속성과 함께 동일한 카테고리 이름을 갖습니다.</td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
   <td><p><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></p> </td>
   <td><p>즉석 업그레이드에서는 기존 파일(/etc/clientlibs/wcm/..._)이 그대로 유지되며 자동으로 제거되지 않으므로 기존 /etc/clientlibs/wcm/foundation/grid/grid_base.less폴더에 대한 참조는 계속 보관됩니다.</p> <p><em>는 이 LESS 파일이 LESS @import 문을 통해 절대 경로에서 참조되고, NOT by clientlib 카테고리가 참조되는 이상입니다.</em></p> <p>'grid_base.less'를 참조하는 LESS가 기존 파일이 아닌 파일을 가리키면 편집 가능한 템플릿 레이아웃 모드가 중단되며, 이로 인해 수행된 모든 조정 내용이 표시되지 않습니다(예: 모든 구성 요소는 페이지의 전체 너비가 됩니다.)</p> </td>
   <td>사용자 지정 코드의 모든 참조(즉, 이동한 grid_base.less 파일을 참조하는 모든 LESS 파일에서)를 업데이트하여 새 위치를 가리키고 이전 위치를 제거합니다.</td>
  </tr>
 </tbody>
</table>

이것들은 이전 섹션에 해당되지 않는 다른 구조입니다.

### 확장성 전략 {#extensibility-strategy-2}

지원되는 모든 확장성 모델에 대한 각 표 행을 참조하십시오. 이 섹션의 컨텐츠는 일반적으로 확장되지 않습니다.

## 기타 {#miscellaneous}

<table>
 <tbody>
  <tr>
   <td><strong>솔루션</strong></td>
   <td><strong>이전 위치</strong><br /> </td>
   <td><strong>새 위치</strong></td>
   <td><strong>이전 버전과의 호환성 방법</strong></td>
   <td><strong>최신 모델에 맞게 요구 사항 조정</strong></td>
  </tr>
  <tr>
   <td>AEM 양식</td>
   <td><code>/etc/designs/fd/fp</code></td>
   <td><code>/libs/fd/fp</code></td>
   <td><p>레거시 AEM Forms 포털 OTB 템플릿. 이러한 템플릿은 업그레이드된 설정 후에도 /etc에 유지됩니다.</p> <p>템플릿 목록에서 "사용되지 않음<em> "이라는 단어가</em>템플릿 제목에 추가되어 새로운 템플릿과 구분됩니다.</p> </td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM 양식</td>
   <td><code>/etc/aep</code></td>
   <td><code>/var/fd/content/annotations</code></td>
   <td>기존 연락 관리 주석 파일. 직접적으로 소비되는 것은 아닙니다. 정리 필터를 사용하여 업그레이드 후에 정리됩니다.</td>
   <td>정리 필터를 사용한 기존 위치 정리 후 업그레이드.</td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/tags</code></td>
   <td><code>/content/cq:tags</code></td>
   <td>태그 관리자 API는 이전 위치와 새 위치를 모두 지원합니다. JCR Tag Manager Factory OSGi 구성 요소가 시작되면 업그레이드된 인스턴스 또는 기존 인스턴스에서 실행 중인지 감지하여 적절한 위치를 사용합니다.<br /> </td>
   <td><p>새 모델에 맞게 정렬하려면:</p>
    <ol>
     <li>이전 모델(<code>/etc/tags</code>)에 대한 참조를 새 모델(<code>/content/cq:tags</code>)으로 바꿉니다. <code>tagID.</code></li>
     <li>CRXDE Lite에 로그인</li>
     <li>태그를 에서 <code>/etc/tags</code> 로 이동 <code>/content/cq:tags</code></li>
     <li>OSGi 구성 요소 다시 시작 <code class="code">com.day.cq.tagging.impl.JcrTagManagerFactoryImpl.
        </code></li>
    </ol> <p> </p> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>기내 워크플로우 처리에<br /> 사용된 기존 위치. 새 워크플로우는 <code>/var.</code></td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/workflow/scripts</code></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
   <td><p>기존 워크플로우 모델 에서 기존 위치에서 워크플로우 스크립트를 참조하는 단계는 업그레이드 후 이러한 스크립트를 계속 가리키며 제대로 실행됩니다. <code>/etc/workflow/scripts</code></p> <p>워크플로우 단계 작성(프로세스, 분할 등)을 위한 AEM UI를 참조하십시오. 워크플로우 스크립트에서 선택한 <code>/etc/workflow/scripts</code> 드롭다운에 더 이상 스크립트가 표시되지 않습니다.</p> </td>
   <td><p>연결된 워크플로우 프로세스 단계가 AEM에서 편집되지 않은 경우 이러한 스크립트를 활용하는 워크플로우는 예상대로 계속 작동합니다.</p> <p>그러나 단계 편집 시기를 포함하여 이전 버전과의 완벽한 호환을 위해서는 고객 사후 업그레이드 시 수동으로 수행해야 합니다.</p>
    <ul>
     <li>스크립트를 <code>/etc/workflow/scripts</code> 다음으로 이동해야 합니다. <code>/apps/workflow/scripts.</code></li>
     <li>워크플로우<strong> 모델 단계에 대한 </strong>참조는 새 <code>/etc/workflow/scripts</code> <code>/apps/workflow/scripts</code> 위치를 참조하도록 업데이트해야 합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/replication/treeactivation</code></td>
   <td><code>/libs/replication/treeactivation</code></td>
   <td>ClassicUI 유틸리티 페이지는 업그레이드 시 그대로 유지됩니다.</td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/jobs</code></td>
   <td><code>/var/dam/jobs</code></td>
   <td><p>AEM 자산 다운로드 작업 호출에 대해 생성된 zip 파일을 저장할 임시 위치입니다.</p> <p>클라이언트가 에셋 다운로드를 요청하면 새 위치에 파일이 생성되므로 업데이트할 필요가 없습니다.</p> </td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/products</code></td>
   <td><code>/var/commerce/products</code></td>
   <td><p>이전 컨텐츠는 그대로 유지되며 업그레이드 후에도 사용할 수 있습니다.</p> <p>새 위치로 마이그레이션하기 위해 레이지 마이그레이션 작업이 제공됩니다.</p> </td>
   <td><p>마이그레이션은 레이지 마이그레이션 작업을 통해 수행됩니다. <code>CQ64CommerceMigrationTask.</code></p> <p>다음 단계를 수행합니다.</p>
    <ul>
     <li>이전 위치에서 새 위치를 가리키도록 참조를 조정합니다.</li>
     <li>기존 위치에서 새 위치로 컨텐츠 이동</li>
     <li><p>전체 시스템에서 새 위치의 사용을 활성화할 수 있는 이전 위치를 제거합니다.</p> </li>
    </ul> <p>작업이 다루는 위치는 다음과 같습니다.</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>큰 카탈로그의 경우 다음 Java 시스템 속성을 AEM에 전달하여 상거래 마이그레이션 작업을 개별적으로 실행하는 것이 좋습니다.</p>
    <ul>
     <li>속성 이름: <code>com.adobe.upgrade.forcemigration</code></li>
     <li>속성 값: <code>com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></li>
    </ul> <p>마이그레이션 후 AEM을 다시 시작해야 합니다.</p> </td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/orders</code></td>
   <td><code>/var/commerce/orders</code></td>
   <td><p>이전 컨텐츠는 그대로 유지되며 업그레이드 후에도 사용할 수 있습니다.</p> <p>새 위치로 마이그레이션하기 위해 레이지 마이그레이션 작업이 제공됩니다.</p> </td>
   <td>위의 설명을 참조하십시오 <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/collections</code></td>
   <td><code>/var/commerce/collections</code></td>
   <td><p>이전 컨텐츠는 그대로 유지되며 업그레이드 후에도 사용할 수 있습니다.</p> <p>새 위치로 마이그레이션하기 위해 레이지 마이그레이션 작업이 제공됩니다.</p> </td>
   <td>위의 설명을 참조하십시오 <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/classifications</code></td>
   <td><code>/var/commerce/classifications</code></td>
   <td>필요한 작업이 없습니다.</td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/shipping-methods</code></td>
   <td><code>/var/commerce/shipping-methods</code></td>
   <td><p>이전 컨텐츠는 그대로 유지되며 업그레이드 후에도 사용할 수 있습니다.</p> <p>새 위치로 마이그레이션하기 위해 레이지 마이그레이션 작업이 제공됩니다.</p> </td>
   <td>위의 설명을 참조하십시오 <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/payment-methods</code></td>
   <td><code>/var/commerce/payment-methods</code></td>
   <td><p>이전 컨텐츠는 그대로 유지되며 업그레이드 후에도 사용할 수 있습니다.</p> <p>새 위치로 마이그레이션하기 위해 레이지 마이그레이션 작업이 제공됩니다.</p> </td>
   <td>위의 설명을 참조하십시오 <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/taskmanagement</code></td>
   <td><code>/var/taskmanagement</code></td>
   <td><p>새 작업은 <code>/var/taskmanagement</code></p> <p>기존 위치의 기존 작업은 여전히 AEM 받은 편지함에 표시됩니다.</p> </td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/workflow/packages</code></td>
   <td><code>/var/workflow/packages</code></td>
   <td><p>AEM 패키지 관리자를 통해 생성된 AEM 패키지는 <code>/etc/workflow/packages.</code></p> <p>AEM 사이트 및 워크플로우를 통해 생성된 기타 패키지는<code>/var/workflow/packages.</code></p> <p>두 패키지 모두에서 찾을 <code>/etc/workflow/packages</code> 수 있으며 <code>/var/workflow/packages</code> AEM의 패키지 관리자를 통해 계속 편집할 수 있습니다. </p> </td>
   <td><p>필요한 작업이 없습니다.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>새 워크플로우 인스턴스는 <code>/var</code> 자동으로 생성됩니다.</td>
   <td>필요한 작업이 없습니다.</td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/commerce/searchpromote</code></td>
   <td><code>/var/cq/searchpromote</code></td>
   <td><p>피드 컨텐츠 검색 및 홍보를 위한 새 위치입니다.</p> <p>이전 URL은 계속 작동하고 요청은 ServletFilter가 새 위치로 전달합니다.</p> </td>
   <td><br /> 필요한 작업이 없습니다. <br /> </td>
  </tr>
  <tr>
   <td>모든</td>
   <td><code>/etc/dtm-hook</code></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
   <td><p>DTM Web-Hooks의 새로운 위치.</p> <p>이전 URL은 계속 작동하고 요청은 ServletFilter가 새 위치로 전달합니다.</p> </td>
   <td><br /> 필요한 작업이 없습니다. <br /> </td>
  </tr>
 </tbody>
</table>

