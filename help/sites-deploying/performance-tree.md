---
title: 성능 트리
seo-title: 성능 트리
description: AEM의 성능 문제를 해결하기 위해 수행해야 하는 단계에 대해 알아봅니다.
seo-description: AEM의 성능 문제를 해결하기 위해 수행해야 하는 단계에 대해 알아봅니다.
uuid: ab0624f7-6b39-4255-89e0-54c74b54cd98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 5febbb1e-795c-49cd-a8f4-c6b4b540673d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 5%

---


# 성능 트리{#performance-tree}

## 범위 {#scope}

아래 다이어그램은 성능 문제를 해결하기 위해 수행해야 하는 단계에 대한 지침을 제공하기 위한 것입니다. 읽기 쉽도록 5개 부분으로 나뉘어져 있습니다.

다이어그램의 각 단계는 설명서 리소스 또는 권장 사항에 연결됩니다.

## 전제 조건 및 가정 {#prerequisites-and-assumptions}

성능 문제가 지정된 페이지(AEM 콘솔 또는 웹 페이지)에서 발견되고 일관되게 재현될 수 있다고 가정합니다. 테스트를 시작하기 전에 성능을 테스트하거나 모니터링할 수 있는 방법이 반드시 필요합니다.

분석은 0단계에서 시작됩니다. 목표는 성능 문제를 담당하는 개체(디스패처, 외부 호스트 또는 AEM)을 결정한 다음 어떤 영역(서버 또는 네트워크)을 조사해야 하는지 결정하는 것입니다.

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
   <td><p>브라우저에서 표준 HTTP 요청 분석을 사용하여 요청 흐름을 분석할 수 있습니다. Chrome에서 이 작업을 수행하는 방법에 대한 자세한 내용은 <br /> 참조 </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-</a><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing"><br /> loadinghttps://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>2단계</strong></td>
   <td>외부 호스트에서 요청이 오고 있습니까?</td>
   <td>브라우저에서 표준 HTTP 요청 분석을 사용하여 요청 흐름을 분석할 수 있습니다. Chrome에서 이 작업을 수행하는 방법에 대한 위의 링크를 참조하십시오.<br /> </td>
  </tr>
  <tr>
   <td><strong>3단계</strong></td>
   <td>요청을 캐시할 수 있습니까?</td>
   <td>액세스 가능한 요청 및 일반 Dispatcher 성능 최적화 안내에 대한 자세한 내용은 <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Dispatcher 성능 최적화</a>를 참조하십시오.</td>
  </tr>
  <tr>
   <td><strong>4단계</strong></td>
   <td>Dispatcher에서 요청이 오고 있습니까?</td>
   <td><p><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#debugging">Dispatcher 디버깅 설명서</a>에서 요청이 제대로 캐시되는지 확인하십시오.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>5단계</strong></td>
   <td>디스패처가 AEM을 통해 각 요청을 인증하려고 합니까?</td>
   <td>디스패처가 캐시된 리소스를 전달하기 전에 AEM에 인증을 위해 <code>HEAD</code> 요청을 전송하는지 확인합니다. AEM <code>access.log</code>에서 <code>HEAD</code> 요청을 찾아 이 작업을 수행할 수 있습니다. 자세한 내용은 <a href="/help/sites-deploying/configure-logging.md">로깅</a>을 참조하십시오.<br /> </td>
  </tr>
  <tr>
   <td><strong>6단계</strong></td>
   <td>디스패처의 지리적 위치가 사용자와 멀리 떨어져 있습니까?</td>
   <td>Dispatcher를 사용자와 더 가깝게 이동합니다.</td>
  </tr>
  <tr>
   <td><strong>7단계</strong></td>
   <td>Dispatcher의 네트워크 레이어가 괜찮습니까?</td>
   <td><br /> 채도 및 지연 문제에 대한 네트워크 레이어를 조사합니다.<p> </p> </td>
  </tr>
  <tr>
   <td><strong>8단계</strong></td>
   <td>느림이란 지방 인스턴스로 재생됩니까?</td>
   <td><br /> <p><a href="/help/sites-developing/tough-day.md">힘든 날</a>을 사용하여 프로덕션 인스턴스에서 "실제" 조건을 복제할 수 있습니다. 개발 단계에서 이것이 현실적이지 않은 경우 다른 네트워크 컨텍스트에서 프로덕션 인스턴스(또는 동일한 스테이징 인스턴스)를 테스트해야 합니다.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>9단계</strong></td>
   <td>서버의 지리적 위치가 사용자와 멀리 떨어져 있습니까?</td>
   <td>서버를 사용자에게 더 가깝게 이동합니다.</td>
  </tr>
  <tr>
   <td><strong>10단계 및 29단계</strong></td>
   <td>네트워크 레이어 조사</td>
   <td><p>채도 및 지연 문제에 대한 네트워크 레이어를 조사합니다.</p> <p>작성자 계층의 경우 지연이 100밀리초를 넘지 않는 것이 좋습니다.</p> <p>성능 최적화 팁에 대한 자세한 내용은 <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">이 페이지</a>를 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td><strong>11단계</strong></td>
   <td>서버를 더 가깝게 이동하거나 영역당 하나 추가</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>12단계</strong></td>
   <td>AEM 서버 문제 해결</td>
   <td>자세한 내용은 다이어그램의 다음 하위 단계를 확인하십시오.</td>
  </tr>
  <tr>
   <td><strong>13단계</strong></td>
   <td>하드웨어 요구 사항 확인</td>
   <td><a href="/help/managing/hardware-sizing-guidelines.md">하드웨어 크기 조정 지침</a>에 대한 설명서를 확인하십시오.<br /> </td>
  </tr>
  <tr>
   <td><strong>14단계</strong></td>
   <td>자주 발생하는 성능 문제 확인</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>15단계</strong></td>
   <td>느린 요청 찾기</td>
   <td><p><code>request.log</code>을 분석하거나 <code>rlog.jar</code>을 사용하여 느린 요청을 확인할 수 있습니다.</p> <p>rlog.jar 사용에 대한 자세한 내용은 이 페이지를 참조하십시오.</p> <p><a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">rlog.jar를 사용하여 기간이 긴 요청을 찾습니다</a>.<br />. </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>16단계</strong></td>
   <td>프로필 서버</td>
   <td><p>AEM에서 사용할 수 있는 프로파일링 도구에 대한 자세한 내용은 <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">성능 모니터링 및 분석을 위한 도구</a>를 참조하십시오.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>17단계</strong></td>
   <td>프로파일링에서 느린 방법 찾기</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>18단계</strong></td>
   <td>프로파일링 일반적인 시나리오</td>
   <td>성능 최적화 섹션의 <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">특정 시나리오 분석</a>을 참조하십시오.<br /> </td>
  </tr>
  <tr>
   <td><strong>19단계</strong></td>
   <td>100% CPU</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://helpx.adobe.com/experience-manager/6-3/sites-deploying/monitoring-and-maintaining.html#MonitoringPerformance</a></td>
  </tr>
  <tr>
   <td><strong>20단계</strong></td>
   <td>메모리 부족</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">메모리 부족</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">내 애플리케이션에서 메모리 부족 오류가 발생합니다.</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html">도움말의 메모리 문제 분석</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>21단계</strong></td>
   <td>디스크 I/O</td>
   <td><p>모니터링 및 유지 관리 설명서의 <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">디스크 I/O</a> 섹션을 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td><strong>단계 22 및 22.1</strong></td>
   <td>캐시 비율</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio">Dispatcher 캐시 비율 계산</a>을 참조하십시오.<br /> <br /> </td>
  </tr>
  <tr>
   <td><strong>23단계</strong></td>
   <td>느린 쿼리</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">쿼리 및 색인 작성 우수 사례</a></td>
  </tr>
  <tr>
   <td><strong>24단계</strong></td>
   <td>저장소 조정</td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">성능 조정 팁</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">성능 구성</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">저장소 성능 조정</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>25단계</strong></td>
   <td>실행 중인 워크플로우</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">동시 워크플로우 처리</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">특정 워크플로우에 대한 큐 구성</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">워크플로우 인스턴스의 정기적인 제거</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">임시 워크플로우</a><br /> </li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>26단계</strong></td>
   <td>MSM 인프라</td>
   <td><p><a href="/help/sites-administering/msm-best-practices.md">다중 사이트 관리자 우수 사례</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>27단계</strong></td>
   <td>자산 조정</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">자산 동기화 서비스</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">여러 DAM 인스턴스</a></li>
     <li>성능 조정 팁 아티클 <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">여기</a>및 <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">여기</a>에 <br />. </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>28단계</strong></td>
   <td>닫히지 않은 세션</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">닫히지 않은 JCR 세션 확인</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>30단계</strong></td>
   <td>디스패처를 더 가깝게 이동("지역"당 하나 추가)</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>31단계</strong></td>
   <td>발송자 앞에서 CDN 사용</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">CDN에 Dispatcher 사용</a><br /> </td>
  </tr>
  <tr>
   <td><strong>32단계</strong></td>
   <td>디스패처 수준의 세션 관리를 사용하여 AEM 서버 오프로드</td>
   <td><p><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement">보안 세션 활성화</a></p> </td>
  </tr>
  <tr>
   <td><strong>33단계</strong></td>
   <td>요청 액세스 가능</td>
   <td>
    <ol>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html">일반 발송자 구성</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache">발송자 캐시 구성</a></li>
    </ol> <p>캐시 비율을 개선하는 방법;요청 캐시 사용 가능(발송자 우수 사례)</p> <p>또한 캐싱 구성을 최적화하려면 아래 설정을 고려하십시오<br /> </p>
    <ol>
     <li>GET이 아닌 HTTP 요청에 대한 캐시 없음 규칙 설정</li>
     <li>쿼리 문자열을 취소할 수 없도록 구성</li>
     <li>누락된 익스텐션을 사용하여 URL 캐시 안 함</li>
     <li>캐시 인증 헤더(Dispatcher 버전 4.1.10 이후 가능)</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>34단계</strong></td>
   <td>업그레이드 발송자 버전</td>
   <td><p>다음 위치에서 최신 Dispatcher 버전을 다운로드할 수 있습니다.</p> <p><a href="https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html">링크를 따르십시오.</a></p> </td>
  </tr>
  <tr>
   <td><strong>35단계</strong></td>
   <td>발송자 구성</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html">디스패처 구성</a><br /> </td>
  </tr>
  <tr>
   <td><strong>36단계</strong></td>
   <td>캐시 무효화 확인</td>
   <td><br />
    <ul>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment">작성자 계층의 캐시 무효화</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance">게시 계층의 캐시 무효화입니다.</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>37단계 및 38단계</strong></td>
   <td>레이지 로딩</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">AEM Web Performance의 Gem Session을 참조하십시오.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>39단계</strong></td>
   <td>사전 연결 기능을 사용하여 연결 오버헤드 감소</td>
   <td>위에 표시된 Gem 세션을 참조하십시오. 또한 W3c:<a href="https://www.w3.org/TR/resource-hints/#dfn-preconnect"> https://www.w3.org/TR/resource-hints/#dfn-preconnect</a>에 대한 추가 설명서가 미리 연결됩니다.</td>
  </tr>
  <tr>
   <td><strong>40단계 및 41단계</strong><br /> </td>
   <td>외부 호스트 지연 및 응답 시간</td>
   <td>외부 호스트에 대한 지연 및 응답 시간을 조사합니다.</td>
  </tr>
  <tr>
   <td><strong>45단계<br /> 와 47단계</strong><br /> </td>
   <td>HTTP/2 사용</td>
   <td>37,38 및 39단계는 Gem Session을 참조하십시오. 또한 HTTP/2 지원에 대한 이<a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html"> 포럼 게시물을 확인하십시오.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>49단계</strong></td>
   <td>페이로드 크기 축소</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">Gzip</a> 을 활성화하고  <a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">이미지 크기를 축소합니다</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>42단계 및 43단계</strong></td>
   <td>Keep-Alive</td>
   <td><p>연결을 다시 사용하기 위한 다른 요청에 <code>Keep-Alive</code> 헤더가 있습니까? 그렇지 않으면 각 요청이 다른 연결 설정으로 연결되므로 불필요한 오버헤드가 발생할 수 있습니다. (브라우저의 표준 HTTP 요청 분석)</p> <p><a href="/help/sites-administering/proxy-jar.md">프록시 서버 도구</a>를 확인하여 연결 상태를 유지할 수 있습니다.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>44단계</strong></td>
   <td>요청이 몇 개나 됩니까?</td>
   <td>브라우저에서 표준 HTTP 요청 분석을 수행합니다.</td>
  </tr>
  <tr>
   <td><strong>46단계</strong></td>
   <td>요청 수 감소</td>
   <td>
    <ol>
     <li>연결된 리소스(이미지, CSS 스프라이트, JSON 등)<br /> </li>
     <li>Clientlibs 포함:
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">클라이언트 라이브러리 폴더</a>  만들기 - 임베드를 사용하여 요청 최소화 머리글 참조</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>48단계</strong></td>
   <td>페이로드 크기가 어떻게 되나요?</td>
   <td>브라우저의 표준 HTTP 요청 분석</td>
  </tr>
  <tr>
   <td><strong>50단계 및 51단계</strong></td>
   <td>JS 코드 차단</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">https://docs.adobe.com/ddc/en/gems/aem-web-performance.html</a></td>
  </tr>
 </tbody>
</table>

