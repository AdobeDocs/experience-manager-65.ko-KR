---
title: 성능 트리
seo-title: Performance Tree
description: AEM의 성능 문제를 해결하기 위해 수행해야 하는 단계에 대해 알아봅니다.
uuid: ab0624f7-6b39-4255-89e0-54c74b54cd98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 5febbb1e-795c-49cd-a8f4-c6b4b540673d
exl-id: f2f968b8-b21c-487d-bc0d-ed60903bc4bf
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 9%

---

# 성능 트리{#performance-tree}

## 범위 {#scope}

다음 다이어그램은 성능 문제를 해결하기 위해 수행해야 하는 단계에 대한 지침을 제공하기 위한 것입니다. 읽기 쉽도록 다섯 섹션으로 나뉩니다.

다이어그램의 각 단계는 설명서 리소스 또는 권장 사항에 연결됩니다.

## 전제 조건 및 가정 {#prerequisites-and-assumptions}

특정 페이지(AEM 콘솔 또는 웹 페이지)에서 성능 문제가 관찰되며 일관되게 재현될 수 있다고 가정합니다. 성과를 테스트하거나 모니터링할 수 있는 방법을 갖추는 것은 조사를 시작하기 전에 반드시 요구되는 사항입니다.

분석은 0단계에서 시작됩니다. 목표는 성능 문제를 담당하는 엔티티(Dispatcher, 외부 호스트 또는 AEM)를 확인한 다음 조사해야 하는 영역(서버 또는 네트워크)을 결정하는 것입니다.

### 섹션 1 {#section}

![chlimage_1-103](assets/chlimage_1-103.png)

### 섹션 2 {#section-1}

![chlimage_1-104](assets/chlimage_1-104.png)

### 섹션 3 {#section-2}

![chlimage_1-105](assets/chlimage_1-105.png)

### 섹션 4 {#section-3}

![chlimage_1-106](assets/chlimage_1-106.png)

### 섹션 5 {#section-4}

![chlimage_1-107](assets/chlimage_1-107.png)

## 참조 링크 {#reference-links}

<table>
 <tbody>
  <tr>
   <td><strong>단계</strong></td>
   <td><strong>제목</strong></td>
   <td><strong>리소스</strong></td>
  </tr>
  <tr>
   <td><strong>0단계</strong></td>
   <td>요청 흐름 분석</td>
   <td><p>브라우저에서 표준 HTTP 요청 분석을 사용하여 요청 흐름을 분석할 수 있습니다. Chrome에서 이 분석을 수행하는 방법에 대한 자세한 내용은 다음을 참조하십시오.<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developer.chrome.com/docs/devtools/</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>2단계</strong></td>
   <td>외부 호스트에서 요청이 오나요?</td>
   <td>브라우저에서 표준 HTTP 요청 분석을 사용하여 요청 흐름을 분석할 수 있습니다. Chrome에서 이 분석을 수행하는 방법에 대한 자세한 내용은 위의 링크를 참조하십시오.<br /> </td>
  </tr>
  <tr>
   <td><strong>3단계</strong></td>
   <td>요청을 캐시할 수 있습니까?</td>
   <td>캐시 가능한 요청 및 일반 Dispatcher 성능 최적화 권고 사항에 대한 자세한 내용은 다음을 참조하십시오. <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Dispatcher 성능 최적화</a>.</td>
  </tr>
  <tr>
   <td><strong>4단계</strong></td>
   <td>Dispatcher에서 요청이 옵니까?</td>
   <td><p>요청이 제대로 캐시되는지 확인하려면 다음을 확인하십시오. <a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#debugging">Dispatcher 디버깅 설명서</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>5단계</strong></td>
   <td>Dispatcher가 AEM을 통해 각 요청을 인증하려고 합니까?</td>
   <td>Dispatcher가 다음을 전송하는지 확인 <code>HEAD</code> 캐시된 리소스를 전달하기 전에 인증을 위해 AEM에 요청합니다. 다음을 찾습니다. <code>HEAD</code> AEM의 요청 <code>access.log</code>. 자세한 내용은 <a href="/help/sites-deploying/configure-logging.md">로깅</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>6단계</strong></td>
   <td>Dispatcher의 지리적 위치는 사용자와 멀리 있습니까?</td>
   <td>Dispatcher를 사용자에게 가깝게 이동합니다.</td>
  </tr>
  <tr>
   <td><strong>7단계</strong></td>
   <td>Dispatcher의 네트워크 레이어가 괜찮습니까?</td>
   <td><br /> 네트워크 계층에서 포화 및 지연 문제를 조사합니다.<p> </p> </td>
  </tr>
  <tr>
   <td><strong>8단계</strong></td>
   <td>로컬 인스턴스에서 느린 속도를 재현할 수 있습니까?</td>
   <td><br /> <p>사용 <a href="/help/sites-developing/tough-day.md">Tough Day</a> 프로덕션 인스턴스에서 "실제" 조건을 복제합니다. 이 시나리오가 개발 공간에 적합하지 않은 경우 다른 네트워크 컨텍스트에서 프로덕션 인스턴스(또는 동일한 스테이징 인스턴스)를 테스트해야 합니다.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>9단계</strong></td>
   <td>서버의 지리적 위치는 사용자와 멀리 떨어져 있습니까?</td>
   <td>서버를 사용자에게 가깝게 이동합니다.</td>
  </tr>
  <tr>
   <td><strong>10단계 및 29단계</strong></td>
   <td>네트워크 레이어 조사</td>
   <td><p>네트워크 계층에서 포화 및 지연 문제를 조사합니다.</p> <p>작성 계층의 경우 지연 시간이 100밀리초를 넘지 않는 것이 좋습니다.</p> <p>성능 최적화 팁에 대한 자세한 내용은 <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">이 페이지</a>.</p> </td>
  </tr>
  <tr>
   <td><strong>11단계</strong></td>
   <td>서버를 더 가깝게 이동하거나 지역당 하나씩 추가</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>12단계</strong></td>
   <td>AEM 서버 문제 해결</td>
   <td>자세한 내용은 다이어그램에서 다음 하위 단계를 확인하십시오.</td>
  </tr>
  <tr>
   <td><strong>13단계</strong></td>
   <td>하드웨어 요구 사항 확인</td>
   <td>에 대한 설명서 확인 <a href="/help/managing/hardware-sizing-guidelines.md">하드웨어 크기 조정 지침</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>14단계</strong></td>
   <td>성능 문제의 빈번한 원인 확인</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>15단계</strong></td>
   <td>느린 요청 찾기</td>
   <td><p>를 분석하여 느린 요청이 있는지 확인할 수 있습니다. <code>request.log</code> 또는 를 사용하여 <code>rlog.jar</code>.</p> <p>rlog.jar 사용에 대한 자세한 내용은 이 페이지를 참조하십시오.</p> <p>다음을 참조하십시오 <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">rlog.jar를 사용하여 지속 시간이 긴 요청 찾기</a>.<br /> </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>16단계</strong></td>
   <td>프로필 서버</td>
   <td><p>AEM에서 사용할 수 있는 프로파일링 도구에 대한 자세한 내용은 <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">성능 모니터링 및 분석 툴</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>17단계</strong></td>
   <td>프로파일링에서 느린 방법 찾기</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>18단계</strong></td>
   <td>프로파일링의 일반적인 시나리오</td>
   <td>다음을 참조하십시오 <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">특정 시나리오 분석</a> 성능 최적화 섹션에서 다음을 수행합니다.<br /> </td>
  </tr>
  <tr>
   <td><strong>19단계</strong></td>
   <td>100% CPU</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html</a></td>
  </tr>
  <tr>
   <td><strong>20단계</strong></td>
   <td>메모리 부족</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">메모리 부족</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">내 응용 프로그램에서 메모리 부족 오류가 발생합니다.</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=ko">메모리 문제 분석.</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>21단계</strong></td>
   <td>디스크 I/O</td>
   <td><p>다음을 참조하십시오. <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">디스크 I/O</a> 섹션 을 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td><strong>22단계 및 22.1단계</strong></td>
   <td>캐시 비율</td>
   <td>다음을 참조하십시오 <a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio">Dispatcher 캐시 비율 계산</a>.<br /> <br /> </td>
  </tr>
  <tr>
   <td><strong>23단계</strong></td>
   <td>느린 쿼리</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">쿼리 및 색인 생성에 대한 우수 사례</a></td>
  </tr>
  <tr>
   <td><strong>24단계</strong></td>
   <td>저장소 조정</td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">성능 조정 팁</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">성능을 위한 구성</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">저장소 성능 조정</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>25단계</strong></td>
   <td>실행 중인 워크플로</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">동시 워크플로우 처리</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">특정 워크플로우에 대한 큐 구성</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">정기적인 워크플로 인스턴스 제거</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">임시 워크플로</a><br /> </li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>26단계</strong></td>
   <td>MSM 인프라</td>
   <td><p><a href="/help/sites-administering/msm-best-practices.md">다중 사이트 관리자 우수 사례</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>27단계</strong></td>
   <td>에셋 조정</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">자산 동기화 서비스</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">여러 DAM 인스턴스</a></li>
     <li>성능 조정 팁 문서 <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">여기</a>.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>28단계</strong></td>
   <td>닫히지 않은 세션</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">닫히지 않은 JCR 세션 확인</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>30단계</strong></td>
   <td>Dispatcher를 더 가깝게 이동("지역"당 하나를 추가하시겠습니까?)</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>31단계</strong></td>
   <td>Dispatcher 앞에서 CDN 사용</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko#using-dispatcher-with-a-cdn">CDN에 Dispatcher 사용</a><br /> </td>
  </tr>
  <tr>
   <td><strong>32단계</strong></td>
   <td>AEM 서버를 오프로드하려면 Dispatcher 수준에서 세션 관리를 사용합니다</td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement">보안 세션 활성화</a></p> </td>
  </tr>
  <tr>
   <td><strong>33단계</strong></td>
   <td>요청을 캐시할 수 있도록 만들기</td>
   <td>
    <ol>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ko">일반 Dispatcher 구성</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache">Dispatcher 캐시 구성</a></li>
    </ol> <p>캐시 비율을 개선하는 방법, 캐시 가능한 요청을 하는 방법(Dispatcher 모범 사례)</p> <p>또한 캐싱 구성을 최적화하려면 아래 설정을 고려하십시오<br /> </p>
    <ol>
     <li>GET이 아닌 HTTP 요청에 대해 no-cache 규칙을 설정합니다.</li>
     <li>캐시 불가능 쿼리 문자열 구성</li>
     <li>확장명이 누락된 URL은 캐시하지 않음</li>
     <li>캐시 인증 헤더(Dispatcher 버전 4.1.10 이후 가능)</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>34단계</strong></td>
   <td>Dispatcher 버전 업그레이드</td>
   <td><p>이 위치에서 최신 Dispatcher 버전을 다운로드할 수 있습니다.</p> <p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=en">링크 따라가기</a></p> </td>
  </tr>
  <tr>
   <td><strong>35단계</strong></td>
   <td>Dispatcher 구성</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ko-KR">Dispatcher 구성</a><br /> </td>
  </tr>
  <tr>
   <td><strong>36단계</strong></td>
   <td>캐시 무효화 확인</td>
   <td><br />
    <ul>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-the-authoring-environment">작성자 계층에 대한 캐시 무효화</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance">게시 계층에 대한 캐시 무효화.</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>37단계 및 38단계</strong></td>
   <td>레이지 로드</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=en">AEM 웹 성능에서 Gem 세션 을 참조하십시오.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>39단계</strong></td>
   <td>연결 오버헤드를 줄이려면 사전 연결 사용</td>
   <td>위의 Gem 세션을 참조하십시오. 또한 W3c에 대한 추가 사전 연결 설명서:<a href="https://html.spec.whatwg.org/#linkTypes"> https://html.spec.whatwg.org/#linkTypes</a></td>
  </tr>
  <tr>
   <td><strong>40단계 및 41단계</strong><br /> </td>
   <td>외부 호스트 지연 및 응답 시간</td>
   <td>외부 호스트에 대한 지연 시간 및 응답 시간을 조사합니다.</td>
  </tr>
  <tr>
   <td><strong>단계 45<br /> 및 47</strong><br /> </td>
   <td>HTTP/2 사용</td>
   <td>37, 38 및 39단계는 Gem 세션 을 참조하십시오. 또한, 체크아웃 <a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html">이</a> http/2 지원 시 포럼 게시물.<br /> </td>
  </tr>
  <tr>
   <td><strong>49단계</strong></td>
   <td>페이로드 크기 축소</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">Gzip 활성화</a> 및 <a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=en">이미지 크기 축소</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>42단계 및 43단계</strong></td>
   <td>Keep-Alive</td>
   <td><p>다음 <code>Keep-Alive</code> 다른 요청에 있는 헤더로 연결을 재사용할 수 있습니까? 그렇지 않으면, 각 요청이 또 다른 연결 수립으로 이어져 불필요한 오버헤드가 유발되는 것을 의미할 것이다. (브라우저의 표준 HTTP 요청 분석)</p> <p>다음을 확인할 수 있습니다. <a href="/help/sites-administering/proxy-jar.md">프록시 서버 도구</a> Keep-Alive 연결을 확인합니다.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>44단계</strong></td>
   <td>몇 번이나 요청합니까?</td>
   <td>브라우저에서 표준 HTTP 요청 분석을 수행합니다.</td>
  </tr>
  <tr>
   <td><strong>46단계</strong></td>
   <td>요청 수 감소</td>
   <td>
    <ol>
     <li>리소스(이미지, CSS 스프라이트, JSON) 연결<br /> </li>
     <li>Clientlibs 포함:
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">클라이언트 라이브러리 폴더 만들기</a> - 제목 을 참조하십시오. 요청을 최소화하기 위해 포함 사용</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>48단계</strong></td>
   <td>페이로드 크기는 얼마입니까?</td>
   <td>브라우저의 표준 HTTP 요청 분석</td>
  </tr>
  <tr>
   <td><strong>50단계 및 51단계</strong></td>
   <td>JS 코드 차단</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=en">https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=en</a></td>
  </tr>
 </tbody>
</table>
