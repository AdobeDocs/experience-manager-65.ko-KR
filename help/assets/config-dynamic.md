---
title: Dynamic Media 구성 - 하이브리드 모드
description: Dynamic Media - 하이브리드 모드를 구성하는 방법에 대해 알아봅니다.
mini-toc-levels: 3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: User, Admin
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuration,Hybrid Mode
solution: Experience Manager, Experience Manager Assets
source-git-commit: e1a8a73e10101a380183658d64f08a7dc5933ee0
workflow-type: tm+mt
source-wordcount: '7992'
ht-degree: 1%

---

# Dynamic Media 구성 - 하이브리드 모드 {#configuring-dynamic-media-hybrid-mode}

## Dynamic Media - 하이브리드 추가 기능 패키지(AEM 6.5.23 이상)

AEM 6.5 서비스 팩 23부터 Dynamic Media - 하이브리드 모드에 새 추가 기능 패키지를 사용할 수 있습니다. 이 패키지에는 Dynamic Media - 하이브리드 실행 모드와 호환되는 `cq-scene7-imaging` 번들이 포함되어 있습니다.

**키 수정 포함**

오류 없이 복제가 성공해도 `/conf/global/settings/dam/dm/imageserver`의 `catalog.expiration` 매개 변수에 대한 업데이트가 서버 또는 작성자 URL에 반영되지 않는 Dynamic Media - 하이브리드 배포의 문제를 해결했습니다. 업데이트는 CRX/DE, 서버 응답 및 공개 게재 URL 간에 일관된 만료 값을 보장합니다. 결과적으로 캐시 비헤이비어와 이미지 변환의 신뢰성을 향상시킵니다. (ASSETS-44837)

**중요 고려 사항**

* 기본 AEM 6.5.23 이상 설치의 `cq-scene7-imaging` 번들은 Dynamic Media - 하이브리드 실행 모드와 *호환되지 않음*&#x200B;입니다.
* 서비스 팩 23 이상을 설치하면 Dynamic Media - 하이브리드(`-r dynamicmedia` 실행 모드)에 대해 구성된 AEM 인스턴스에서 기존 `cq-scene7-imaging` 번들을 *자동으로 업데이트하지 않습니다*.

**하이브리드 추가 기능 패키지를 설치할 때**

* AEM 6.5.19 또는 이전 버전에서 AEM 6.5.23(또는 이상)으로 직접 업그레이드하는 경우.
* Dynamic Media - 하이브리드 기능 관련 수정 사항이 필요한 경우.
* 새 Dynamic Media - 하이브리드 인스턴스를 AEM 6.5 GA(일반 가용성)에서 서비스 팩 23(이상)으로 직접 배포할 때

**하이브리드 추가 기능 패키지 다운로드**

하이브리드 추가 기능 패키지는 2025년 5월 22일 목요일부터 Adobe 소프트웨어 배포에서 공식 릴리스인 AEM 6.5.23과 함께 공개적으로 사용할 수 있습니다. 사용자는 소프트웨어 배포에서 **AEM 6.5 Dynamic Media 하이브리드 추가 기능 패키지**&#x200B;를 검색하여 찾을 수 있습니다.


## SSL 2.0 및 3.0과 TLS 1.0 및 1.1에 대한 지원 종료.

Secure Socket Layer 2.0 및 3.0 과 Transport Layer Security 1.0 및 1.1에 대한 지원 종료.

2024년 4월 30일부터 Adobe Dynamic Media는 다음에 대한 지원을 종료했습니다.

* SSL(보안 소켓 계층) 2.0
* SSL 3.0
* TLS(전송 계층 보안) 1.0 및 1.1
* TLS 1.2의 다음과 같은 약한 암호:
  `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  `TLS_RSA_WITH_AES_256_GCM_SHA384`
  `TLS_RSA_WITH_AES_256_CBC_SHA256`
  `TLS_RSA_WITH_AES_256_CBC_SHA`
  `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  `TLS_RSA_WITH_AES_128_GCM_SHA256`
  `TLS_RSA_WITH_AES_128_CBC_SHA256`
  `TLS_RSA_WITH_AES_128_CBC_SHA`
  `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

[Dynamic Media 제한 사항](/help/assets/limitations.md)도 참조하세요.

<!-- FOR ABOVE - CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->


Dynamic Media-Hybrid를 사용하도록 활성화하고 구성해야 합니다. 사용 사례에 따라 Dynamic Media에는 여러 [지원되는 구성](#supported-dynamic-media-configurations)이 있습니다.

>[!NOTE]
>
>Scene7 실행 모드에서 Dynamic Media를 구성하고 실행하려면 [Dynamic Media 구성 - Scene7 모드](/help/assets/config-dms7.md)를 참조하십시오.
>
>하이브리드 실행 모드에서 Dynamic Media를 구성하고 실행하려면 이 페이지의 지침을 따르십시오.

Dynamic Media에서 [비디오](/help/assets/video.md) 작업에 대해 자세히 알아보세요.

>[!NOTE]
>
>개발, 스테이징 및 라이브 프로덕션 환경용과 같이 서로 다른 환경에 대해 설정된 Adobe Experience Manager을 사용하는 경우 각 환경에 대해 Dynamic Media Cloud Services를 구성합니다.

>[!NOTE]
>
>Dynamic Media 구성에 문제가 있는 경우 Dynamic Media에 관련된 로그 파일을 확인하십시오. 이러한 파일은 Dynamic Media를 활성화할 때 자동으로 설치됩니다.
>
>* `s7access.log`
>* `ImageServing.log`
>
>[Experience Manager 인스턴스 모니터링 및 유지 관리](/help/sites-deploying/monitoring-and-maintaining.md)에 문서화되어 있습니다.

하이브리드 게시 및 게재는 Adobe Experience Manager에 추가되는 Dynamic Media의 핵심 기능입니다. 하이브리드 게시를 사용하면 Experience Manager 게시 노드가 아닌 클라우드에서 이미지, 세트 및 비디오와 같은 Dynamic Media 자산을 제공할 수 있습니다.

Dynamic Media 뷰어, 사이트 페이지 및 정적 콘텐츠와 같은 기타 콘텐츠는 Experience Manager 게시 노드에서 계속 제공됩니다.

Dynamic Media의 고객인 경우 모든 Dynamic Media 콘텐츠에 대한 게재 메커니즘으로 하이브리드 게재를 사용해야 합니다.

## 비디오용 하이브리드 게시 아키텍처 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## 이미지를 위한 하이브리드 게시 아키텍처 {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## 지원되는 Dynamic Media 구성 {#supported-dynamic-media-configurations}

다음 구성 작업은 다음 용어를 참조합니다.

| **용어** | **Dynamic Media 사용** | **설명** |
|---|---|---|
| Experience Manager 작성자 노드 | 녹색 원의 흰색 확인 표시 | 온프레미스 또는 Managed Services을 통해 배포하는 작성자 노드. |
| Experience Manager 게시 노드 | 흰색 &quot;X&quot;가 빨간색 사각형에 있습니다. | 온-프레미스 또는 Managed Services을 통해 배포하는 게시 노드입니다. |
| 이미지 서비스 게시 노드 | 녹색 원에 흰색 확인 표시. | Adobe에서 관리하는 데이터 센터에서 실행하는 게시 노드입니다. 이미지 서비스 URL을 나타냅니다. |

이미징에만, 비디오에만 또는 이미징과 비디오 모두에 대해 Dynamic Media를 구현하도록 선택할 수 있습니다. 특정 시나리오에 맞게 Dynamic Media를 구성하는 단계를 결정하려면 다음 표를 참조하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>시나리오</strong></td>
   <td ><strong>작동 방법</strong></td>
   <td><strong>구성 단계</strong></td>
  </tr>
  <tr>
   <td>프로덕션에서 이미지만 제공</td>
   <td>이미지는 Adobe의 전 세계 데이터 센터에 있는 서버를 통해 전달된 다음 확장 가능한 성능과 글로벌 도달 범위를 위해 CDN에 의해 캐시됩니다.</td>
   <td>
    <ol>
     <li>Experience Manager <strong>작성자</strong> 노드에서 <a href="#enabling-dynamic-media">Dynamic Media를 활성화</a>합니다.</li>
     <li><a href="#configuring-dynamic-media-cloud-services">Dynamic Media Cloud Services</a>에서 이미징을 구성하십시오.</li>
     <li><a href="#configuring-image-replication">이미지 복제를 구성합니다</a>.</li>
     <li><a href="#replicating-catalog-settings">카탈로그 설정을 복제합니다</a>.</li>
     <li><a href="#replicating-viewer-presets">뷰어 사전 설정을 복제합니다</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">복제에 기본 자산 필터 사용</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media 이미지 서버 설정을 구성</a>합니다.</li>
     <li><a href="#delivering-assets">자산 배달</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>사전 프로덕션(개발, QE, 스테이징 등)에서 이미지만 제공합니다.</td>
   <td>이미지는 Experience Manager 게시 노드를 통해 전달됩니다. 이 시나리오에서는 트래픽이 최소화되므로 Adobe의 데이터 센터에 이미지를 전달할 필요가 없습니다. 또한 프로덕션 시작 전에 콘텐츠를 안전하게 미리 볼 수 있습니다.</td>
   <td>
    <ol>
     <li>Experience Manager <strong>작성자</strong> 노드에서 <a href="#enabling-dynamic-media">Dynamic Media를 활성화</a>합니다.</li>
     <li>Experience Manager <strong>게시</strong> 노드에서 <a href="#enabling-dynamic-media">Dynamic Media를 활성화</a>합니다.</li>
     <li><a href="#replicating-viewer-presets">뷰어 사전 설정을 복제합니다</a>.</li>
     <li>비프로덕션 이미지에 대한 <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">자산 필터</a>를 설정합니다.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media 이미지 서버 설정을 구성합니다.</a></li>
     <li><a href="#delivering-assets">자산을 제공합니다.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>모든 환경(프로덕션, 개발, QE, 스테이징 등)에서 비디오만 제공</td>
   <td>비디오는 확장 가능한 성능과 글로벌 도달 범위를 위해 CDN에 의해 전달되고 캐시됩니다. 비디오 포스터 이미지(재생이 시작되기 전에 표시되는 비디오의 썸네일)는 Experience Manager 게시 인스턴스에 의해 전달됩니다.</td>
   <td>
    <ol>
     <li>Experience Manager <strong>작성자</strong> 노드에서 <a href="#enabling-dynamic-media">Dynamic Media를 활성화</a>합니다.</li>
     <li>Experience Manager <strong>게시</strong> 노드에서 <a href="#enabling-dynamic-media">Dynamic Media를 활성화</a>(게시 인스턴스는 비디오 포스터 이미지를 제공하고 비디오 재생을 위한 메타데이터를 제공함)합니다.</li>
     <li><a href="#configuring-dynamic-media-cloud-services">Dynamic Media 클라우드 서비스에서 비디오를 구성합니다.</a></li>
     <li><a href="#replicating-viewer-presets">뷰어 사전 설정을 복제합니다</a>.</li>
     <li><a href="#setting-up-asset-filters-for-video-only-deployments">비디오 전용 자산 필터</a>를 설정합니다.</li>
     <li><a href="#delivering-assets">자산을 제공합니다.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>프로덕션에서 이미지와 비디오 모두 제공</td>
   <td><p>비디오는 확장 가능한 성능과 글로벌 도달 범위를 위해 CDN에 의해 전달되고 캐시됩니다. 이미지 및 비디오 포스터 이미지는 Adobe의 전 세계 데이터 센터에 있는 서버를 통해 전달된 다음 확장 가능한 성능과 글로벌 도달 범위를 위해 CDN에 의해 캐시됩니다.</p> <p>사전 프로덕션에서 이미지 또는 비디오를 설정하려면 이전 섹션을 참조하십시오. </p> </td>
   <td>
    <ol>
     <li>Experience Manager <strong>작성자</strong> 노드에서 <a href="#enabling-dynamic-media">Dynamic Media를 활성화</a>합니다.</li>
     <li><a href="#configuring-dynamic-media-cloud-services">Dynamic Media 클라우드 서비스에서 비디오를 구성합니다.</a></li>
     <li><a href="#configuring-dynamic-media-cloud-services">Dynamic Media 클라우드 서비스에서 이미징을 구성합니다.</a></li>
     <li><a href="#configuring-image-replication">이미지 복제를 구성합니다</a>.</li>
     <li><a href="#replicating-catalog-settings">카탈로그 설정을 복제합니다</a>.</li>
     <li><a href="#replicating-viewer-presets">뷰어 사전 설정을 복제합니다</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">복제에 기본 자산 필터를 사용합니다.</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media 이미지 서버 설정을 구성합니다.</a></li>
     <li><a href="#delivering-assets">자산을 제공합니다.</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Dynamic Media 활성화 {#enabling-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)은(는) 기본적으로 비활성화되어 있습니다. Dynamic Media 기능을 이용하려면 `dynamicmedia` 실행 모드(예: `publish` 실행 모드)를 사용하여 Dynamic Media를 활성화해야 합니다. 활성화하기 전에 [기술 요구 사항](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on)을 검토하십시오.

>[!NOTE]
>
>실행 모드를 통해 Dynamic Media를 활성화하면 `dynamicMediaEnabled` 플래그를 **[!UICONTROL true]**(으)로 설정하여 Dynamic Media를 활성화한 Experience Manager 6.1 및 Experience Manager 6.0의 기능이 바뀝니다. 이 플래그는 Experience Manager 6.2 이상에서는 사용할 수 없습니다. 또한 Dynamic Media를 활성화하기 위해 빠른 시작을 다시 시작할 필요가 없습니다.

Dynamic Media를 활성화하면 UI에서 Dynamic Media 기능을 사용할 수 있으며, 업로드된 모든 이미지 자산은 동적 이미지 렌디션의 빠른 전송에 사용되는 *cqdam.pyramid.tiff* 렌디션을 받습니다. 이러한 PTIFF는 다음과 같은 중요한 이점이 있습니다.

* 하나의 기본 소스 이미지만 관리하고 추가 스토리지 없이 무한한 렌디션을 즉시 생성할 수 있습니다.
* 확대/축소, 팬 및 회전 등 대화형 시각화를 사용할 수 있습니다.

Experience Manager에서 Dynamic Media Classic을 사용하려면 [특정 시나리오](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media)를 사용하지 않는 한 Dynamic Media를 사용하지 마십시오. 실행 모드를 통해 Dynamic Media를 활성화하지 않으면 Dynamic Media가 비활성화됩니다.

Dynamic Media를 활성화하려면 명령줄 또는 빠른 시작 파일 이름에서 Dynamic Media 실행 모드를 활성화해야 합니다.

**Dynamic Media를 사용하려면:**

1. 명령줄에서 빠른 시작을 시작할 때 다음을 수행합니다.

   * jar 파일을 시작할 때 명령줄 끝에 `-r dynamicmedia`을(를) 추가합니다.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   s7delivery에 게시하는 경우 다음 trustStore 인수도 포함해야 합니다.

   ```shellsession {.line-numbers}
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. `https://localhost:4502/is/image`을(를) 요청하고 이미지 서버가 현재 실행 중인지 확인하십시오.

   >[!NOTE]
   >
   >Dynamic Media 관련 문제를 해결하려면 `crx-quickstart/logs/` 디렉터리에서 다음 로그를 참조하십시오.
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log - ImageServer 로그는 내부 ImageServer 프로세스의 동작을 분석하는 데 사용되는 통계 및 분석 정보를 제공합니다.
   >
   >이미지 서버 로그 파일 이름의 예: `ImageServer-57346-2020-07-25.log`
   >
   >* s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - s7access 로그는 `/is/image` 및 `/is/content`을(를) 통해 Dynamic Media에 수행된 각 요청을 기록합니다.
   >
   >이러한 로그는 Dynamic Media가 활성화된 경우에만 사용됩니다. `system/console/status-Bundlelist` 페이지에서 생성된 **전체 다운로드** 패키지에 포함되지 않습니다. Dynamic Media 문제가 있는 경우 고객 지원 센터에 문의할 때 이 두 로그를 모두 문제에 추가하십시오.

### Experience Manager을 다른 포트 또는 컨텍스트 경로에 설치한 경우... {#if-you-installed-aem-to-a-different-port-or-context-path}

[Experience Manager을 응용 프로그램 서버](/help/sites-deploying/application-server-install.md)에 배포하고 Dynamic Media를 사용하도록 설정한 경우 외부화에서 **자체 도메인**&#x200B;을(를) 구성해야 합니다. 그렇지 않으면 Dynamic Media 에셋에 대해 에셋의 썸네일 생성이 제대로 작동하지 않습니다.

또한 다른 포트 또는 컨텍스트 경로에서 빠른 시작을 실행하는 경우 **자체 도메인**&#x200B;도 변경해야 합니다.

Dynamic Media가 활성화되면 Dynamic Media를 사용하여 이미지 에셋에 대한 정적 썸네일 변환이 생성됩니다. Dynamic Media에 대해 썸네일 생성이 제대로 작동하려면 Experience Manager이 자신에게 URL 요청을 수행해야 하며 포트 번호와 컨텍스트 경로를 모두 알고 있어야 합니다.

Experience Manager:

* [Externalizer](/help/sites-developing/externalizer.md)의 **self-domain**&#x200B;은(는) 포트 번호와 컨텍스트 경로를 모두 검색하는 데 사용됩니다.
* 구성된 **자체 도메인**&#x200B;이 없으면 Jetty HTTP 서비스에서 포트 번호 및 컨텍스트 경로를 검색합니다.

Experience Manager QuickStart WAR 배포에서는 포트 번호와 컨텍스트 경로를 파생할 수 없으므로 **자체 도메인**&#x200B;을 구성해야 합니다. **자체 도메인**&#x200B;을 구성하는 방법에 대해서는 [외부화 설명서](/help/sites-developing/externalizer.md)를 참조하십시오.

>[!NOTE]
>
>[Experience Manager 빠른 시작 독립 실행형 배포](/help/sites-deploying/deploy.md)에서는 포트 번호 및 컨텍스트 경로를 자동으로 구성할 수 있으므로 **자체 도메인**&#x200B;을 구성할 필요가 없습니다. 그러나 모든 네트워크 인터페이스가 꺼져 있으면 **자체 도메인**&#x200B;을 구성해야 합니다.

## Dynamic Media 비활성화  {#disabling-dynamic-media}

Dynamic Media는 기본적으로 활성화되어 있지 않습니다. 그러나 이전에 Dynamic Media를 활성화한 경우 나중에 비활성화할 수 있습니다.

Dynamic Media를 사용하도록 설정한 후 사용하지 않도록 설정하려면 `-r dynamicmedia` 실행 모드 플래그를 제거합니다.

**Dynamic Media를 사용하지 않도록 설정하려면:**

1. 명령줄에서 빠른 시작을 실행하면 다음 중 하나를 수행할 수 있습니다.

   * jar 파일을 시작할 때 명령줄에 `-r dynamicmedia`을(를) 추가하지 마십시오.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. `https://localhost:4502/is/image`을(를) 요청합니다. Dynamic Media가 비활성화되었다는 메시지가 표시됩니다.

   >[!NOTE]
   >
   >Dynamic Media 실행 모드가 비활성화되면 `cqdam.pyramid.tiff` 렌디션을 생성하는 워크플로 단계를 자동으로 건너뜁니다. 동적 렌디션 지원 및 기타 Dynamic Media 기능도 비활성화됩니다.
   >
   >또한 Experience Manager 서버를 구성한 후 Dynamic Media 실행 모드가 비활성화되면 해당 실행 모드에 따라 업로드된 모든 자산이 유효하지 않습니다.

## (선택 사항) Dynamic Media 사전 설정 및 구성을 6.3에서 6.5 제로 다운타임으로 마이그레이션 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Experience Manager - Dynamic Media를 6.3에서 6.5로 업그레이드하는 경우(이제 다운타임 없는 배포 기능이 포함됨) 다음 curl 명령을 실행해야 합니다. 이 명령은 CRXDE Lite의 `/etc`에서 `/conf`(으)로 모든 사전 설정 및 구성을 마이그레이션합니다.

>[!NOTE]
>
>호환성 모드에서 Experience Manager 인스턴스를 실행하는 경우(즉, 호환성 패키지가 설치되어 있는 경우) 이 명령을 실행할 필요가 없습니다.

호환성 패키지가 있거나 없는 모든 업그레이드의 경우 다음 Linux® curl 명령을 실행하여 원래 Dynamic Media와 함께 제공되었던 기본 즉시 사용 가능한 뷰어 사전 설정을 복사할 수 있습니다.

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

`/etc`에서 만든 사용자 지정 뷰어 사전 설정 및 구성을 `/conf`(으)로 마이그레이션하려면 다음 Linux® curl 명령을 실행하십시오.

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 이미지 복제 구성 {#configuring-image-replication}

Dynamic Media 이미지 게재는 Experience Manager 작성자의 비디오 썸네일 등 이미지 에셋을 게시하고 Adobe의 주문형 복제 서비스(복제 서비스 URL)에 복제하여 작동합니다. 그런 다음 Assets은 온디맨드 이미지 제공 서비스(이미지 서비스 URL)를 통해 제공됩니다.

다음 작업을 수행합니다.

1. [인증 설정](#setting-up-authentication).
1. [복제 에이전트를 구성합니다](#configuring-the-replication-agent).

복제 에이전트는 이미지, 비디오 메타데이터 및 집합과 같은 Dynamic Media 에셋을 Adobe에서 호스팅하는 이미지 서비스에 게시합니다. 복제 에이전트는 기본적으로 활성화되어 있지 않습니다.

복제 에이전트를 구성한 후에는 [성공적으로 설정되었는지 확인](#validating-the-replication-agent-for-dynamic-media)해야 합니다. 이 섹션에서는 이러한 절차에 대해 설명합니다.

>[!NOTE]
>
>PTIFF 작성에 대한 기본 메모리 제한은 모든 워크플로우에서 3GB입니다. 예를 들어, 다른 워크플로우가 일시 중지된 동안 3GB의 메모리가 필요한 이미지 하나를 처리하거나, 각각 300MB의 메모리가 필요한 10개의 이미지를 동시에 처리할 수 있습니다.
>
>메모리 제한은 구성이 가능하며 시스템 리소스 가용성과 처리 중인 이미지 콘텐츠 유형에 맞춥니다. 큰 에셋이 많고 시스템에 메모리가 충분한 경우 이미지가 병렬로 처리되도록 이 제한을 늘릴 수 있습니다.
>
>최대 메모리 제한보다 많은 메모리가 필요한 이미지가 거부되었습니다.
>
>PTIFF 만들기에 대한 메모리 제한을 변경하려면 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]** > **[!UICONTROL Adobe CQ Scene7 PTiffManager]**&#x200B;로 이동하여 **[!UICONTROL maxMemory]** 값을 변경하십시오.

### 인증 설정 {#setting-up-authentication}

Dynamic Media 이미지 게재 서비스에 이미지를 복제할 수 있도록 작성자에 대한 복제 인증을 설정합니다. 먼저 KeyStore를 가져온 다음 **[!UICONTROL dynamic-media-replication]** 사용자 아래에 저장하고 구성합니다. 회사 관리자가 프로비저닝 프로세스 중에 KeyStore 파일과 필요한 자격 증명이 포함된 시작 이메일을 받았습니다. 이 정보를 받지 못한 경우 Adobe 고객 지원 센터에 문의하십시오.

**인증을 설정하려면:**

1. 파일 및 암호가 없는 경우 Adobe 고객 지원 센터에 문의하여 KeyStore 파일 및 암호를 확인하십시오. 이 정보는 프로비저닝에 필요한 부분입니다. 계정 키를 연결합니다.

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 보안]** > **[!UICONTROL 사용자]**(으)로 이동합니다.

1. 사용자 관리 페이지에서 **[!UICONTROL dynamic-media-replication]** 사용자로 이동한 다음 선택하여 엽니다.

   ![dm-replication](assets/dm-replication.png)

1. Dynamic-media 복제에 대한 사용자 설정 편집 페이지에서 **[!UICONTROL Keystore]** 탭을 선택한 다음 **[!UICONTROL KeyStore 만들기]**&#x200B;를 선택합니다.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. **[!UICONTROL KeyStore 액세스 암호 설정]** 대화 상자에서 암호를 입력하고 암호를 확인하십시오.

   >[!NOTE]
   >
   >나중에 복제 에이전트를 구성할 때 암호를 다시 입력해야 하므로 암호를 기억하십시오.

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. **[!UICONTROL Dynamic-media-replication에 대한 사용자 설정 편집]** 페이지에서 **KeyStore 파일에서 개인 키 추가** 영역을 확장하고 다음을 추가하십시오(다음 이미지 참조).

   * **[!UICONTROL 새 별칭]** 필드에 나중에 복제 구성에서 사용할 별칭의 이름을 입력합니다. 예를 들어 `replication`을(를) 별칭으로 사용할 수 있습니다.
   * **[!UICONTROL KeyStore 파일]**&#x200B;을(를) 선택하십시오. Adobe에서 제공한 KeyStore 파일로 이동하여 선택한 다음 **[!UICONTROL 열기]**&#x200B;를 선택합니다.
   * **[!UICONTROL KeyStore 파일 암호]** 필드에 KeyStore 파일 암호를 입력합니다. 이 암호는 5단계에서 만든 KeyStore 암호가 **아니요**&#x200B;이지만 Adobe에서 제공하는 KeyStore 파일 암호입니다. 프로비저닝 중에 받은 환영 전자 메일의 암호입니다. KeyStore 파일 암호를 받지 못한 경우 Adobe 고객 지원 센터에 문의하십시오.
   * **[!UICONTROL 개인 키 암호]** 필드에 개인 키 암호를 입력합니다(이전 단계에서 입력한 것과 동일한 개인 키 암호일 수 있음). Adobe은 프로비저닝 중에 전송된 시작 이메일에 개인 키 암호를 제공합니다. 개인 키 암호를 받지 않은 경우 Adobe 고객 지원 센터에 문의하십시오.
   * **[!UICONTROL 개인 키 별칭]** 필드에 개인 키 별칭을 입력합니다. 예, `*companyname*-alias`. Adobe은 프로비저닝 중에 전송된 시작 이메일에 개인 키 별칭을 제공합니다. 개인 키 별칭을 받지 못한 경우 Adobe 고객 지원 센터에 문의하십시오.

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 선택하여 이 사용자에 대한 변경 내용을 저장합니다.

   그런 다음 [복제 에이전트를 구성](#configuring-the-replication-agent)해야 합니다.

### 복제 에이전트 구성 {#configuring-the-replication-agent}

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** > **[!UICONTROL 작성자의 에이전트]**&#x200B;로 이동합니다.
1. 작성자의 에이전트 페이지에서 **[!UICONTROL Dynamic Media 하이브리드 이미지 복제(s7delivery)]**&#x200B;를 선택합니다.
1. **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. **[!UICONTROL 설정]** 탭을 선택한 후 다음을 입력하십시오.

   * **[!UICONTROL 사용]** - 복제 에이전트를 사용하려면 이 확인란을 선택하십시오.
   * **[!UICONTROL 지역]** - 북미, 유럽 또는 아시아 지역으로 설정합니다.
   * **[!UICONTROL 테넌트 ID]** - 이 값은 복제 서비스에 게시하는 회사/테넌트의 이름입니다. 이 값은 프로비저닝 중에 Adobe이 보낸 환영 이메일에서 제공하는 테넌트 ID입니다. 이 정보를 받지 못한 경우 Adobe 고객 지원 센터에 문의하십시오.
   * **[!UICONTROL 키 저장소 별칭]** - 이 값은 [인증 설정](#setting-up-authentication)에서 키를 생성할 때 설정된 **새 별칭** 값과 동일합니다(예: `replication`). ([인증 설정](#setting-up-authentication)의 7단계를 참조하세요.)
   * **[!UICONTROL 키 저장소 암호]** - **[!UICONTROL 키 저장소 만들기]**&#x200B;를 탭했을 때 만들어진 KeyStore 암호입니다. Adobe은 이 암호를 제공하지 않습니다. [인증 설정](#setting-up-authentication)의 5단계를 참조하세요.

   다음 이미지는 샘플 데이터가 있는 복제 에이전트를 보여 줍니다.

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.

### Dynamic Media에 대한 복제 에이전트의 유효성 검사 {#validating-the-replication-agent-for-dynamic-media}

Dynamic Media용 복제 에이전트의 유효성을 검사하려면 다음을 수행하십시오.

**[!UICONTROL 연결 테스트]**&#x200B;를 선택하십시오. 출력 예는 다음과 같습니다.

```shell
11.03.2016 10:57:55 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
11.03.2016 10:57:55 - * Auth User: replication-receiver
11.03.2016 10:57:55 - * HTTP Version: 1.1
11.03.2016 10:57:55 - * Using OAuth 2.0 Authorization Grants
11.03.2016 10:57:55 - * OAuth 2.0 User: dynamic-media-replication
11.03.2016 10:57:55 - * OAuth 2.0 Token: '*****' initialized
11.03.2016 10:57:55 - Publishing: POST[https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=xfpuu-6613]
11.03.2016 10:57:55 - Publish response: OK[]
11.03.2016 10:57:55 - Transfer succeeded in 141 ms for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
-------------------------------------------------------------------------------------------------------------------------------
Replication test succeeded
```

>[!NOTE]
>
>다음 중 하나를 수행하여 확인할 수도 있습니다.
>
>* 복제 로그에서 자산이 복제되었는지 확인합니다.
>* 이미지를 게시합니다. 이미지를 선택하고 드롭다운 메뉴에서 **[!UICONTROL 뷰어]**&#x200B;를 선택한 다음 뷰어 사전 설정을 선택합니다. **[!UICONTROL URL]**&#x200B;을(를) 선택하십시오. 이미지가 표시되는지 확인하려면 브라우저에서 URL 경로를 복사하여 붙여넣습니다.
>

### 인증 문제 해결 {#troubleshooting-authentication}

인증을 설정할 때 해당 솔루션에서 발생할 수 있는 몇 가지 문제가 있습니다. 이러한 문제를 확인하기 전에 복제를 설정했는지 확인하십시오.

#### 문제: HTTP 상태 코드 401(메시지 포함) - 권한 부여 필요 {#problem-http-status-code-with-message-authorization-required}

이 문제는 `dynamic-media-replication` 사용자에 대해 KeyStore를 설정하지 못했기 때문에 발생할 수 있습니다.

```shell
Replication test to s7delivery:https://s7bern.macromedia.com:8580/is-publish/
17.06.2016 18:54:43 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}
17.06.2016 18:54:43 - * Auth User: replication-receiver
17.06.2016 18:54:43 - * HTTP Version: 1.1
17.06.2016 18:54:43 - * Using OAuth 2.0 Authorization Grants
17.06.2016 18:54:43 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 18:54:43 - No OAuth token available. OAuth not initialized
17.06.2016 18:54:43 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 18:54:43 - Publishing: POST[https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough]
17.06.2016 18:54:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
17.06.2016 18:54:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309,
 userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
```

**솔루션:**
`KeyStore`이(가) **dynamic-media-replication** 사용자에게 저장되고 올바른 암호가 제공되었는지 확인하십시오.

#### 문제: 키를 해독할 수 없음 - 데이터를 해독할 수 없음 {#problem-could-not-decrypt-key-could-not-decrypt-data}

```xml
Replication test to s7delivery:https://<localhost>:8580/is-publish/
17.06.2016 19:00:16 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}
17.06.2016 19:00:16 - * Auth User: replication-receiver
17.06.2016 19:00:16 - * HTTP Version: 1.1
17.06.2016 19:00:16 - * Using OAuth 2.0 Authorization Grants
17.06.2016 19:00:16 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 19:00:16 - No OAuth token available. OAuth not initialized
17.06.2016 19:00:16 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 19:00:16 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}. java.lang.SecurityException: java.security.UnrecoverableKeyException: Could not decrypt key: Could not decrypt data.
```

**솔루션:**
암호를 확인합니다. 복제 에이전트에 저장된 암호가 키 저장소를 생성하는 데 사용된 암호와 다릅니다.

#### 문제: InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

이 문제는 Experience Manager 작성자 인스턴스의 구성 오류로 인해 발생합니다. 작성자의 Java™ 프로세스가 올바른 `javax.net.ssl.trustStore`을(를) 가져오지 않습니다. 복제 로그에 이 오류가 표시됩니다.

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

또는 오류 로그:

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.

java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**솔루션:**
Experience Manager 작성자의 Java™ 프로세스에 유효한 Truststore로 설정된 시스템 속성 `-Djavax.net.ssl.trustStore=`이(가) 있는지 확인하십시오.

#### 문제: KeyStore가 설정되지 않았거나 초기화되지 않았습니다. {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

이 문제는 핫픽스 또는 dynamic-media-user 또는 keystore 노드를 덮어쓰는 기능 팩으로 인해 발생할 수 있습니다.

복제 로그 예:

```shell
Replication test to s7delivery:https://replicate-na.assetsadobe.com/is-publish
02.08.2016 14:37:44 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}
02.08.2016 14:37:44 - * Auth User: replication-receiver
02.08.2016 14:37:44 - * HTTP Version: 1.1
02.08.2016 14:37:44 - * Using OAuth 2.0 Authorization Grants
02.08.2016 14:37:44 - * OAuth 2.0 User: dynamic-media-replication
02.08.2016 14:37:44 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}. com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised key store for user dynamic-media-replication
```

**솔루션:**

1. 사용자 관리 페이지로 이동합니다.
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. 사용자 관리 페이지에서 `dynamic-media-replication` 사용자로 이동한 다음 선택하여 엽니다.
1. **[!UICONTROL KeyStore]** 탭을 선택합니다. **[!UICONTROL KeyStore 만들기]** 단추가 나타나면 [인증 설정](#setting-up-authentication)의 단계를 먼저 다시 실행해야 합니다.
1. KeyStore 설정을 다시 실행해야 하는 경우 [복제 에이전트 구성](/help/assets/config-dynamic.md#configuring-the-replication-agent)도 다시 수행해야 합니다.

   s7delivery 복제 에이전트를 다시 구성합니다.
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. 구성이 올바른지 확인하려면 **[!UICONTROL 연결 테스트]**&#x200B;를 선택하십시오.

#### 문제: 게시 에이전트가 OAuth 대신 SSL을 사용하고 있습니다. {#problem-publish-agent-is-using-ssl-instead-of-oauth}

이 문제는 핫픽스 또는 기능 팩이 올바르게 설치되지 않았거나 설정을 덮어쓴 경우에 발생할 수 있습니다.

로그 복제 예:

```shell
01.08.2016 18:42:59 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}
01.08.2016 18:42:59 - * Auth User: replication-receiver
01.08.2016 18:42:59 - * HTTP Version: 1.1
01.08.2016 18:42:59 - * Using Client Auth SSL alias - replication-receiver *
01.08.2016 18:42:59 - Publishing: POST[https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=altayerstaging]
01.08.2016 18:42:59 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
01.08.2016 18:42:59 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
```

**솔루션:**

1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**(으)로 이동합니다.

   `localhost:4502/crx/de/index.jsp`

1. s7delivery 복제 에이전트 노드로 이동합니다.
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. 이 설정을 복제 에이전트(값이 **[!UICONTROL True]**(으)로 설정된 부울)에 추가하십시오.

   `enableOauth=true`

1. 페이지의 왼쪽 상단 모서리 근처에서 **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.

### 구성 테스트 {#testing-your-configuration}

Adobe에서는 구성의 전체적인 테스트를 수행할 것을 권장합니다.

이 테스트를 시작하기 전에 다음을 이미 수행했는지 확인하십시오.

* 이미지 사전 설정을 추가했습니다.
* 클라우드 서비스에서 **[!UICONTROL Dynamic Media 구성(6.3 이전)]**&#x200B;을 구성하십시오. 이 테스트에는 이미지 서비스 URL이 필요합니다.

**구성을 테스트하려면:**

1. 이미지 자산을 업로드합니다. (Assets에서 **[!UICONTROL 만들기]** > **[!UICONTROL 파일]**(으)로 이동하여 파일을 선택합니다.)
1. 워크플로우가 완료될 때까지 기다립니다.
1. 이미지 자산을 게시합니다. (자산을 선택하고 **[!UICONTROL 빠른 게시]**&#x200B;를 선택합니다.)
1. 이미지를 열고 **[!UICONTROL 렌디션]**&#x200B;을 눌러 해당 이미지의 렌디션으로 이동합니다.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. 동적 렌디션을 선택합니다.
1. 이 자산의 URL을 가져오려면 **[!UICONTROL URL]**&#x200B;을(를) 선택하십시오.
1. 선택한 URL로 이동하여 이미지가 예상대로 작동하는지 확인합니다.

자산이 전달되었는지 테스트하는 또 다른 방법은 req=exists 를 URL에 추가하는 것입니다.

## Dynamic Media 클라우드 서비스 구성 {#configuring-dynamic-media-cloud-services}

Dynamic Media Cloud Service은 특히 이미지 및 비디오, 비디오 분석 및 비디오 인코딩의 하이브리드 게시 및 전달을 지원합니다.

구성의 일부로, 등록 ID, 비디오 서비스 URL, 이미지 서비스 URL, 복제 서비스 URL을 입력하고 인증을 설정해야 합니다. 이 정보는 계정 프로비저닝 프로세스의 일부로 이메일로 전송되었습니다. 이 정보를 받지 못한 경우 Adobe Experience Manager 관리자 또는 Adobe 고객 지원 센터에 문의하여 정보를 얻으십시오.

>[!NOTE]
>
>Dynamic Media Cloud Services를 설정하기 전에 게시 인스턴스를 설정해야 합니다. 또한 Dynamic Media Cloud Services를 구성하기 전에 복제를 설정해야 합니다.

**Dynamic Media 클라우드 서비스를 구성하려면:**

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 클라우드 서비스]** > **[!UICONTROL Dynamic Media 구성(6.3 이전)]**&#x200B;으로 이동합니다.
1. Dynamic Media 구성 브라우저 페이지의 왼쪽 창에서 **[!UICONTROL 전역]**&#x200B;을(를) 선택한 다음 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.
1. **[!UICONTROL Dynamic Media 구성 만들기]** 대화 상자의 제목 필드에 제목을 입력합니다.
1. 비디오용 Dynamic Media를 구성하는 경우,

   * **[!UICONTROL 등록 ID]** 필드에 등록 ID를 입력합니다.
   * **[!UICONTROL 비디오 서비스 URL]** 필드에 Dynamic Media Gateway의 비디오 서비스 URL을 입력하십시오.

1. 이미징을 위해 Dynamic Media를 구성하는 경우 **[!UICONTROL 이미지 서비스 URL]** 필드에 Dynamic Media Gateway의 이미지 서비스 URL을 입력하십시오.
1. **[!UICONTROL 저장]**&#x200B;을 선택하여 Dynamic Media 구성 브라우저 페이지로 돌아갑니다.
1. 전역 탐색 콘솔에 액세스하려면 Experience Manager 로고를 선택합니다.

## 비디오 보고 구성 {#configuring-video-reporting}

Dynamic Media Hybrid를 사용하여 Experience Manager의 여러 설치 간에 비디오 보고를 구성할 수 있습니다.

**사용 시기:** Dynamic Media 구성(6.3 이전)을 구성할 때 비디오 보고를 비롯한 다양한 기능이 시작됩니다. 이 구성은 지역 Analytics 회사에 보고서 세트를 만듭니다. 여러 작성자 노드를 구성하는 경우, 각 작성자 노드에 대해 별도의 보고서 세트를 만듭니다. 따라서 설치 시 보고 데이터가 일관되지 않습니다. 또한 각 작성자 노드가 동일한 하이브리드 게시 서버를 참조하는 경우 마지막 작성자 설치에서 모든 비디오 보고에 대한 대상 보고서 세트를 변경합니다. 이 문제는 보고서 세트가 너무 많은 Analytics 시스템을 오버로드합니다.

**시작하기:** 다음 세 가지 작업을 완료하여 비디오 보고를 구성합니다.

1. 첫 번째 작성자 노드에서 Dynamic Media 구성(6.3 이전)을 구성한 후 Video Analytics 사전 설정 패키지를 만듭니다. 이 초기 작업은 새 구성이 동일한 보고서 세트를 계속 사용할 수 있도록 하기 때문에 중요합니다.
1. Dynamic Media 구성(6.3 이전)을 구성하는 ***new*** 작성자 노드 ***before***&#x200B;에 Video Analytics 사전 설정 패키지를 설치합니다.
1. 패키지 설치를 확인하고 디버그합니다.

### 첫 번째 작성자 노드를 구성한 후 Video Analytics 사전 설정 패키지 만들기 {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

이 작업을 완료하면 Video Analytics 사전 설정이 포함된 패키지 파일이 있습니다. 이러한 사전 설정에는 보고서 세트, 추적 서버, 추적 네임스페이스 및 Experience Cloud 조직 ID(사용 가능한 경우)가 포함되어 있습니다.

1. 아직 구성하지 않은 경우 Dynamic Media 구성(6.3 이전)을 구성합니다.
1. (선택 사항) 보고서 세트 ID를 보고 복사합니다(JCR에 대한 액세스 권한이 있어야 함). 보고서 세트 ID가 필요하지 않으면 더 쉽게 확인할 수 있습니다.
1. 패키지 관리자를 사용하여 패키지를 만듭니다.
1. 필터를 포함하도록 패키지를 편집합니다.

   Experience Manager에서: `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. 패키지를 빌드합니다.
1. Video Analytics 사전 설정 패키지를 다운로드하거나 공유하여 이후의 새 작성자 노드와 공유할 수 있습니다.

### 더 많은 작성자 노드를 구성하기 전에 Video Analytics 사전 설정 패키지를 설치하십시오 {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

Dynamic Media 구성(6.3 이전)을 구성하려면 이 작업을 ***전에***&#x200B;완료해야 합니다. 이렇게 하지 않으면 사용하지 않는 다른 보고서 세트가 생성됩니다. 또한 비디오 보고가 올바르게 작동해도 데이터 수집이 최적화되지 않습니다.

새 작성자 노드에서 첫 번째 작성자 노드의 Video Analytics 사전 설정 패키지에 액세스할 수 있는지 확인합니다.

1. 이전에 만든 Video Analytics 사전 설정 패키지를 패키지 관리자에 업로드합니다.
1. Video Analytics 사전 설정 패키지 설치
1. Dynamic Media 구성(6.3 이전)

### 패키지 설치 확인 및 디버그 {#verifying-and-debugging-the-package-installation}

1. 다음 중 하나를 수행하여 패키지 설치를 확인하고 필요한 경우 디버그합니다.

   * **JCR을 통해 Video Analytics 사전 설정을 확인**
JCR을 통해 Video Analytics 사전 설정을 확인하려면 CRXDE Lite에 대한 액세스 권한이 있어야 합니다.

     Experience Manager - CRXDE Lite에서 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`(으)로 이동

     `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`에서와 같이

     작성자 노드에서 CRXDE Lite에 액세스할 수 없는 경우 게시 서버를 통해 사전 설정을 확인할 수 있습니다.

   * **이미지 서버를 통해 Video Analytics 사전 설정을 확인**

     이미지 서버 req=userdata 요청을 하여 Video Analytics 사전 설정의 유효성을 직접 확인할 수 있습니다.
예를 들어 작성자 노드에서 Analytics 사전 설정을 보려면 다음 요청을 수행할 수 있습니다.

     `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

     게시 서버에 있는 사전 설정의 유효성을 검사하기 위해 게시 서버에 유사한 직접 요청을 할 수 있습니다. 응답은 Author 및 Publish 노드에서 동일합니다. 응답은 다음과 유사합니다.

     ```
     marketingCloudOrgId=0FC4E86B573F99CC7F000101
      reportSuite=aemaem6397618-2018-05-23
      trackingNamespace=aemvideodal
      trackingServer=aemvideodal.d2.sc.omtrdc.net
     ```

   * **Experience Manager의 Video Reporting 도구를 통해 Video Analytics 사전 설정을 확인**
**[!UICONTROL 도구]** > **[!UICONTROL Assets]** > **[!UICONTROL 비디오 보고]**(으)로 이동

     `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

     다음 오류 메시지가 표시되면 보고서 세트를 사용할 수 있지만 채워지지 않은 것입니다. 시스템이 데이터를 수집하기 전에 새 설치에서 이 오류는 올바르고 원하는 것입니다.

   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   보고 데이터를 생성하려면 비디오 하나를 업로드하고 게시하십시오. **[!UICONTROL URL 복사]**&#x200B;를 사용하여 비디오를 한 번 이상 실행하십시오.

   비디오 뷰어 사용에서 보고 데이터를 채우려면 최대 12시간이 걸릴 수 있습니다.

   오류가 있고 보고서 세트가 올바르게 설정되지 않은 경우 다음 경고가 표시됩니다.

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   이 오류는 Dynamic Media 구성(6.3 이전) 서비스를 구성하기 전에 비디오 보고를 실행하는 경우에도 표시됩니다.

### 비디오 보고 구성 문제 해결 {#troubleshooting-the-video-reporting-configuration}

* 설치하는 동안 경우에 따라 Analytics API 서버에 대한 연결 시간이 초과됩니다. 설치가 연결을 20번 다시 시도하지만 여전히 실패합니다. 이러한 상황이 발생하면 로그 파일에 여러 오류가 기록됩니다. `SiteCatalystReportService` 검색
* Analytics 사전 설정 패키지를 먼저 설치하지 않으면 새 보고서 세트가 생성될 수 있습니다.
* Experience Manager 6.3에서 Experience Manager 6.4 또는 Experience Manager 6.4.1로 업그레이드한 후 Dynamic Media 구성(6.3 이전)을 구성해도 보고서 세트가 생성됩니다. 이 문제는 알려져 있으며 Experience Manager 6.4.2에서 수정될 예정입니다.

### Video Analytics 사전 설정 정보 {#about-the-video-analytics-preset}

Video Analytics 사전 설정(간단히 Analytics 사전 설정이라고도 함)은 Dynamic Media의 뷰어 사전 설정 옆에 저장됩니다. 기본적으로 뷰어 사전 설정과 동일하지만 AppMeasurement 및 비디오 하트비트 보고를 구성하는 데 사용되는 정보가 있습니다.

사전 설정의 속성은 다음과 같습니다.

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId`(이전 Experience Manager 버전에는 없음)

Experience Manager 6.4 이상 버전은 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`에 이 사전 설정을 저장합니다.

## 카탈로그 설정 복제 {#replicating-catalog-settings}

JCR을 통해 설정 프로세스의 일부로 자체 기본 카탈로그 설정을 게시합니다. 카탈로그 설정을 복제하려면:

1. 터미널 창에서 다음을 실행합니다.

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. Experience Manager에서 CRXDE Lite의 다음 위치로 이동합니다(관리자 권한 필요).

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. **[!UICONTROL 복제]** 탭을 선택합니다.
1. **[!UICONTROL 복제]**&#x200B;를 선택합니다.

## 뷰어 사전 설정 복제 {#replicating-viewer-presets}

뷰어 사전 설정이 있는 *자산을 전달하려면 뷰어 사전 설정을 복제/게시*&#x200B;해야 합니다. (에셋의 URL 또는 포함 코드를 가져오려면 모든 뷰어 사전 설정을 *및* 복제하여 활성화해야 합니다.)
자세한 내용은 [뷰어 사전 설정 게시](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)를 참조하십시오.

>[!NOTE]
>
>기본적으로, 자산의 세부 사항 보기에서 **[!UICONTROL 렌디션]**&#x200B;을 선택하면 다양한 렌디션이 표시되고 **[!UICONTROL 뷰어]**&#x200B;를 선택하면 다양한 뷰어 사전 설정이 표시됩니다. 표시되는 수를 늘리거나 줄일 수 있습니다. [표시되는 이미지 사전 설정 수 늘리기](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) 또는 [표시되는 뷰어 사전 설정 수 늘리기](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)를 참조하십시오.

## 복제할 자산 필터링 {#filtering-assets-for-replication}

비 Dynamic Media 배포에서는 Experience Manager 작성 환경에서 Experience Manager 게시 노드로 *모든* 자산(이미지와 비디오 모두)을 복제합니다. Experience Manager 게시 서버에서도 자산을 전달하므로 이 워크플로우가 필요합니다.

그러나 Dynamic Media 배포에서는 자산이 클라우드를 통해 전달되므로 동일한 자산을 Experience Manager 게시 노드에 복제할 필요가 없습니다. 이러한 &quot;하이브리드 게시&quot; 워크플로는 자산을 복제하기 위해 추가 스토리지 비용과 더 긴 처리 시간을 피합니다. Dynamic Media 뷰어, 사이트 페이지 및 정적 콘텐츠와 같은 기타 콘텐츠는 Experience Manager 게시 노드에서 계속 제공됩니다.

에셋을 복제하는 것 외에도 다음과 같은 비에셋도 복제됩니다.

* Dynamic Media 게재 구성: `/conf/global/settings/dam/dm/imageserver/jcr:content`
* 이미지 사전 설정: `/conf/global/settings/dam/dm/presets/macros`
* 뷰어 사전 설정: `/conf/global/settings/dam/dm/presets/viewer`

필터에서는 Experience Manager 게시 노드에 복제되지 않도록 자산을 *제외*&#x200B;할 수 있습니다.

### 복제에 기본 자산 필터 사용 {#using-default-asset-filters-for-replication}

프로덕션 *또는*(2) 이미징 및 비디오에서 (1) 이미징에 Dynamic Media를 사용하는 경우 Adobe에서 제공하는 기본 필터를 그대로 사용할 수 있습니다. 다음 필터는 기본적으로 활성화되어 있습니다.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>필터</strong></td>
   <td><strong>Mime 유형</strong></td>
   <td><strong>렌디션</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media 이미지 게재</td>
   <td><p>filter-image</p> <p>필터 세트</p> <p> </p> </td>
   <td><p><strong>이미지/</strong>(으)로 시작</p> <p><strong>application/</strong>을(를) 포함하고 <strong>set</strong>(으)로 끝납니다.</p> </td>
   <td>기본 제공되는 "filter-images"(대화형 이미지를 포함한 단일 이미지 자산에 적용) 및 "filter-sets"(스핀 세트, 이미지 세트, 혼합 미디어 세트 및 회전 메뉴 세트에 적용)는 다음과 같습니다.
    <ul>
     <li>복제를 위한 PTIFF 이미지 및 메타데이터(<strong>cqdam</strong>(으)로 시작하는 모든 렌디션)를 포함합니다.</li>
     <li>원본 이미지 및 정적 이미지 렌디션을 복제하지 마십시오.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media 비디오 게재</td>
   <td>filter-video</td>
   <td><strong>비디오/</strong>(으)로 시작</td>
   <td>기본 제공되는 "filter-video"는 다음과 같습니다.
    <ul>
     <li>프록시 비디오 렌디션, 비디오 썸네일/포스터 이미지, 복제를 위한 메타데이터(<strong>cqdam</strong>(으)로 시작하는 모든 렌디션)를 포함합니다.</li>
     <li>원본 비디오 및 정적 썸네일 렌디션을 복제에서 제외합니다.<br /> <br /> <strong>참고:</strong> 프록시 비디오 렌디션에는 바이너리가 포함되지 않고 노드 속성만 포함됩니다. 따라서 게시자 저장소 크기에는 영향을 주지 않습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Classic (Scene7) 통합</td>
   <td><p>filter-image</p> <p>필터 세트</p> <p>filter-video</p> </td>
   <td><p><strong>이미지/</strong>(으)로 시작</p> <p><strong>application/</strong>을(를) 포함하고 <strong>set</strong>(으)로 끝납니다.</p> <p><strong>비디오/</strong>(으)로 시작</p> </td>
   <td><p>Adobe Dynamic Media Cloud Replication Service URL 대신 Experience Manager 게시 서버를 가리키도록 전송 URI를 구성합니다. 이 필터를 설정하면 Dynamic Media Classic에서 Experience Manager 게시 인스턴스 대신 자산을 제공할 수 있습니다.</p> <p>기본 제공되는 "filter-images", "filter-sets" 및 "filter-video"는 다음과 같습니다.</p>
    <ul>
     <li>복제를 위한 PTIFF 이미지, 프록시 비디오 표현물 및 메타데이터를 포함합니다. 그러나 Experience Manager - Dynamic Media Classic 통합을 실행하는 그룹의 경우 JCR에 존재하지 않으므로 사실상 아무 작업도 수행하지 않습니다.</li>
     <li>원본 이미지, 정적 이미지 변환, 원본 비디오 및 정적 썸네일 변환을 복제하지 마십시오. 대신 Dynamic Media Classic은 이미지 및 비디오 자산을 제공합니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>필터는 MIME 유형에 적용되며 경로별로 지정할 수 없습니다.

### 비디오 전용 배포용 자산 필터 설정 {#setting-up-asset-filters-for-video-only-deployments}

비디오 전용으로 Dynamic Media를 사용하는 경우 다음 단계에 따라 복제용 자산 필터를 설정하십시오.

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** > **[!UICONTROL 작성자의 에이전트]**&#x200B;로 이동합니다.
1. 작성자의 에이전트 페이지에서 **[!UICONTROL 기본 에이전트(게시)]**&#x200B;를 선택합니다.
1. **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. **[!UICONTROL 에이전트 설정]** 대화 상자의 **[!UICONTROL 설정]** 탭에서 **[!UICONTROL 사용]**&#x200B;을 선택하여 에이전트를 켭니다.
1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.
1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**(으)로 이동합니다.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`(으)로 이동
1. **[!UICONTROL filter-video]**&#x200B;을(를) 찾아 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 복사]**&#x200B;를 선택합니다.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/publish`(으)로 이동
1. `jcr:content`을(를) 찾아 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 붙여넣기]**&#x200B;를 선택합니다.

이러한 단계는 비디오 자체가 Dynamic Media Cloud Service에 의해 제공되는 동안 Experience Manager 게시 인스턴스를 설정하여 비디오 포스터 이미지와 재생에 필요한 비디오 메타데이터를 전달합니다. 또한 원본 비디오 및 정적 썸네일 렌디션은 게시 인스턴스에 필요하지 않으므로 복제에서 제외됩니다.

### 비프로덕션 배포에서 이미징을 위한 자산 필터 설정 {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

비프로덕션 배포에서 이미징에 Dynamic Media를 사용하는 경우 다음 단계에 따라 복제용 자산 필터를 설정하십시오.

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 배포]** > **[!UICONTROL 복제]** > **[!UICONTROL 작성자의 에이전트]**&#x200B;로 이동합니다.
1. 작성자의 에이전트 페이지에서 **[!UICONTROL 기본 에이전트(게시)]**&#x200B;를 선택합니다.
1. **[!UICONTROL 편집]**&#x200B;을 선택합니다.
1. **[!UICONTROL 에이전트 설정]** 대화 상자의 **[!UICONTROL 설정]** 탭에서 **[!UICONTROL 사용]**&#x200B;을 선택하여 에이전트를 켭니다.
1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.
1. Experience Manager에서 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**(으)로 이동합니다.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`(으)로 이동

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. **[!UICONTROL 필터 이미지]**&#x200B;를 찾아 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 복사]**&#x200B;를 선택합니다.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/publish`(으)로 이동
1. `jcr:content`을(를) 찾아 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 만들기]** > **[!UICONTROL 노드 만들기]**(으)로 이동합니다. `nt:unstructured` 유형의 `damRenditionFilters` 이름을 입력하십시오.
1. `damRenditionFilters`을(를) 찾아 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL 붙여넣기]**&#x200B;를 선택합니다.

이 단계에서는 Experience Manager 게시 인스턴스를 설정하여 이미지를 비프로덕션 환경에 전달합니다. 원본 이미지 및 정적 변환은 게시 인스턴스에 필요하지 않으므로 복제에서 제외됩니다.

>[!NOTE]
>
>작성자에 여러 필터가 있는 경우 각 에이전트에는 서로 다른 사용자가 할당되어야 합니다. granite 코드는 사용자당 하나의 필터 모델을 적용합니다. 필터 설정마다 항상 다른 사용자가 있어야 합니다.
>
>서버에서 필터를 두 개 이상 사용하고 있습니까? 예를 들어 게시할 복제에 대한 한 개의 필터와 s7delivery에 대한 두 번째 필터입니다. 그렇다면 이 두 필터에 `jcr:content` 노드에서 다른 **userId**&#x200B;이(가) 할당되어 있는지 확인해야 합니다. 다음 이미지를 참조하십시오.

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### 복제를 위한 자산 필터 사용자 지정(선택 사항) {#customizing-asset-filters-for-replication}

1. Experience Manager에서 Experience Manager 로고를 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**(으)로 이동합니다.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`(으)로 이동하여 필터를 검토합니다.

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. 필터에 대한 MIME 유형을 정의하려면 다음과 같이 MIME 유형을 찾을 수 있습니다.

   왼쪽 레일에서 `content > dam > <locate_your_asset> >  jcr:content > metadata`을(를) 확장한 다음 테이블에서 `dc:format`을(를) 찾습니다.

   다음 그래픽은 `dc:format`에 대한 자산의 경로의 예입니다.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   자산 `Fiji Red.jpg`의 `dc:format`이(가) `image/jpeg`입니다.

   이 필터가 형식에 관계없이 모든 이미지에 적용되도록 하려면 값을 `image/*`(으)로 설정합니다. 여기서 `*`은(는) 모든 형식의 모든 이미지에 적용되는 정규 표현식입니다.

   JPEG 유형의 이미지에만 필터를 적용하려면 `image/jpeg` 값을 입력하십시오.

1. 복제에서 포함 또는 제외할 변환을 정의합니다.

   복제를 위해 필터링하는 데 사용할 수 있는 문자는 다음과 같습니다.

   | 사용할 문자 | 복제를 위해 자산을 필터링하는 방법 |
   | --- | --- |
   | `*` | 와일드카드 문자 |
   | `+` | 복제용 자산 포함 |
   | `-` | 복제에서 자산 제외 |

   다음으로 이동 `content/dam/<locate your asset>/jcr:content/renditions`.

   다음 그래픽은 에셋 표현물의 예입니다.

   ![chlimage_1-513](assets/chlimage_1-4.png)

   위의 예를 사용하여 PTIFF(피라미드 TIFF)만 복제하려는 경우 `cqdam`로 시작하는 모든 표현물이 포함된 `+cqdam,*`을(를) 입력합니다. 이 예제에서 해당 렌디션은 `cqdam.pyramid.tiff`입니다.

   원본만 복제하려면 `+original`을(를) 입력해야 합니다.

## Dynamic Media 이미지 서버 설정 구성 {#configuring-dynamic-media-image-server-settings}

Dynamic Media 이미지 서버 구성에는 Adobe CQ Scene7 ImageServer 번들 및 Adobe CQ Scene7 PlatformServer 번들의 편집이 포함됩니다.

>[!NOTE]
>
>Dynamic Media는 [사용하도록 설정된 후](#enabling-dynamic-media)즉시 작동합니다. 그러나 Dynamic Media 이미지 서버를 특정 사양 또는 요구 사항에 맞게 구성하여 설치를 세부 조정하도록 선택할 수도 있습니다.

**필수 구성 요소** - *Dynamic Media 이미지 서버를 구성하기 전에* Windows®의 VM에 Microsoft® Visual C++ 라이브러리가 설치되어 있는지 확인하십시오. 라이브러리는 Dynamic Media 이미지 서버를 실행하는 데 필요합니다. 여기에서 [Microsoft® Visual C++ 2010 재배포 가능 패키지(x64)를 다운로드할 수 있습니다](https://www.microsoft.com/en-us/download/details.aspx?id=26999).

Dynamic Media 이미지 서버 설정을 구성하려면 다음 작업을 수행하십시오.

1. Experience Manager의 왼쪽 상단 모서리에서 **[!UICONTROL Adobe Experience Manager]**&#x200B;을(를) 선택하여 전역 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;로 이동합니다.
1. Adobe Experience Manager 웹 콘솔 구성 페이지에서 **[!UICONTROL OSGi]** > **[!UICONTROL 구성]**(으)로 이동하여 현재 Experience Manager 내에서 실행 중인 모든 번들을 나열합니다.

   Dynamic Media 게재 서버는 목록의 다음 이름 아래에 있습니다.

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. 번들 목록의 Adobe CQ Scene7 ImageServer 오른쪽에 있는 **[!UICONTROL 편집]** 아이콘을 선택합니다.
1. Adobe CQ Scene7 ImageServer 대화 상자에서 다음 구성 값을 설정합니다.

   >[!NOTE]
   >
   >일반적으로 기본값을 변경할 필요가 없습니다. 그러나 기본값을 변경하는 경우 변경 사항을 적용하려면 번들을 다시 시작해야 합니다.

   | 속성 | 기본 값 | 설명 |
   | --- | --- | --- |
   | `TcpPort.name` | *`empty`* | ImageServer 프로세스와의 통신에 사용할 포트 번호입니다. 기본적으로 사용 가능한 포트는 자동으로 검색됩니다. |
   | `AllowRemoteAccess.name` | *`empty`* | ImageServer 프로세스에 대한 원격 액세스를 허용하거나 허용하지 않습니다. false인 경우 이미지 서버는 localhost에서만 수신합니다.localhost를 가리키는 <br> 기본 외부화 설정은 특정 VM 인스턴스의 실제 도메인 또는 IP 주소를 지정해야 합니다. 그 이유는 localhost가 VM의 상위 시스템을 가리키기 때문입니다.<br>VM의 도메인 또는 IP 주소에 호스트 파일 항목이 있어야 VM에서 자체적으로 확인할 수 있습니다. |
   | `MaxRenderRgnPixels` | 16피코미터 | 렌더링되는 최대 크기(메가픽셀). |
   | `MaxMessageSize` | 16MB | 게재되는 최대 메시지 크기(MB)입니다. |
   | `RandomAccessUrlTimeout` | 20 | 이미지 서버가 JCR이 광범위한 타일 요청에 응답할 때까지 대기하는 시간(초)에 대한 시간 초과 값입니다. |
   | `WorkerThreads` | 10 | 작업자 스레드 수. |

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. 번들 목록의 Adobe CQ Scene7 PlatformServer 오른쪽에 있는 **[!UICONTROL 편집]** 아이콘을 선택합니다.
1. Adobe CQ Scene7 PlatformServer 대화 상자에서 다음 기본값 옵션을 설정합니다.

   >[!NOTE]
   >
   >Dynamic Media 이미지 서버는 자체 디스크 캐시를 사용하여 응답을 캐시합니다. Experience Manager HTTP 캐시와 Dispatcher을 사용하여 Dynamic Media 이미지 서버의 응답을 캐시할 수 없습니다.

   | 속성 | 기본 값 | 설명 |
   |---|---|---|
   | 캐시 활성화됨 | 선택됨 | 응답 캐시의 사용 여부 |
   | 캐시 루트 | 캐시 | 응답 캐시 폴더에 대한 하나 이상의 경로. 상대 경로는 내부 s7imaging 번들 폴더에 대해 확인됩니다. |
   | 캐시 최대 크기 | 200000000 | 응답 캐시의 최대 크기(바이트)입니다. |
   | 캐시 최대 항목 | 100000 | 캐시에서 허용되는 최대 항목 수입니다. |

### 기본 매니페스트 설정 {#default-manifest-settings}

기본 매니페스트를 사용하면 Dynamic Media 게재 응답을 생성하는 데 사용되는 기본값을 구성할 수 있습니다. 품질(JPEG 품질, 해상도, 리샘플링 모드), 캐싱(만료)을 미세 조정하고 너무 큰 이미지(defaultpix, defaultthumbpix, maxpix)의 렌더링을 방지할 수 있습니다.

기본 매니페스트 구성의 위치는 **[!UICONTROL Adobe CQ Scene7 PlatformServer]** 번들의 **[!UICONTROL 카탈로그 루트]** 기본값에서 가져옵니다. 기본적으로 이 값은 **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]** 내의 다음 경로에 있습니다.

`/conf/global/settings/dam/dm/imageserver/`

![CRXDE Lite에서 이미지 서버 구성](assets/configimageservercrxdelite.png)

아래 표에 설명된 대로 새 값을 입력하여 등록 정보 값을 변경할 수 있습니다.

기본 매니페스트를 변경했으면 페이지의 왼쪽 상단 모서리에서 **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.

속성 탭 오른쪽에 있는 **[!UICONTROL 액세스 제어]** 탭을 선택한 다음 모든 사용자 및 dynamic-media-replication 사용자에 대해 액세스 제어 권한을 `jcr:read`(으)로 설정하십시오.

![CRXDE Lite에서 이미지 서버 구성 및 액세스 제어 탭 설정](assets/configimageservercrxdeliteaccesscontroltab.png)

매니페스트 설정 표 및 그 기본값:

| 속성 | 기본 값 | 설명 |
| --- | --- | --- |
| `bkgcolor` | `FFFFFF` | 기본 배경색입니다. 실제 이미지 데이터를 포함하지 않는 응답 이미지의 영역을 채우는 데 사용되는 RGB 값입니다. 이미지 제공 API에서 [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html?lang=ko#image-serving-api)도 참조하세요. |
| `defaultpix` | `300,300` | 기본 보기 크기입니다. 요청에서 wid=, hei= 또는 scl=을 사용하여 보기 크기를 명시적으로 지정하지 않을 경우, 서버에서 응답 이미지가 이 너비 및 높이보다 크지 않도록 제한합니다.<br>쉼표로 구분된 0보다 큰 두 개의 정수로 지정되었습니다. 폭 및 높이(픽셀 단위). 두 값 중 하나 또는 모두를 0으로 설정하여 구속을 해제할 수 있습니다. 중첩/포함된 요청에는 적용되지 않습니다.<br>이미지 제공 API에서 [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html?lang=ko#image-serving-api)도 참조하십시오.<br>그러나 일반적으로 뷰어 사전 설정 또는 이미지 사전 설정을 사용하여 자산을 전달합니다. Defaultpix는 뷰어 사전 설정 또는 이미지 사전 설정을 사용하지 않는 자산에만 적용됩니다. |
| `defaultthumbpix` | `100,100` | 기본 썸네일 크기입니다. 썸네일 요청(`req=tmb`)에 대해 attribute::DefaultPix 대신 사용됩니다.<br>서버에서 응답 이미지가 이 너비 및 높이보다 크지 않도록 제한합니다. 썸네일 요청(`req=tmb`)이 크기를 명시적으로 지정하지 않고 `wid=`, `hei=` 또는 `scl=`을 사용하여 보기 크기를 명시적으로 지정하지 않으면 이 작업은 true입니다.<br>쉼표로 구분된 0보다 큰 두 개의 정수로 지정되었습니다. 폭 및 높이(픽셀 단위). 두 값 중 하나 또는 모두를 0으로 설정하여 구속을 해제할 수 있습니다.<br>중첩/포함된 요청에는 적용되지 않습니다.<br>이미지 제공 API에서 [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html?lang=ko#image-serving-api)도 참조하십시오. |
| `expiration` | `36000000` | 기본 클라이언트 캐시 TTL(Time to Live). 특정 카탈로그 레코드에 유효한 카탈로그::Expiration 값이 없는 경우 기본 만료 간격을 제공합니다.<br>실수, 0 이상. 응답 데이터가 생성된 이후 만료까지 남은 시간(밀리초). 응답 이미지를 항상 즉시 만료하여 클라이언트 캐싱을 효과적으로 비활성화하려면 0으로 설정합니다. 기본적으로 이 값은 10시간으로 설정되어 있습니다. 즉, 새 이미지가 게시되는 경우 이전 이미지가 사용자의 캐시를 벗어나는 데 10시간이 걸립니다. 캐시를 더 빨리 정리해야 하는 경우 고객 지원 센터에 문의하십시오.<br>이미지 제공 API의 [만료](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html?lang=ko)도 참조하세요. |
| `jpegquality` | `80` | 기본 JPEG 인코딩 속성입니다. JPEG 응답 이미지의 기본 특성을 지정합니다.<br>쉼표로 구분된 정수와 플래그입니다. 첫 번째 값은 1..100 범위에 있으며 품질을 정의합니다. 두 번째 값은 정상적인 동작에 대해 0일 수 있고, JPEG 인코더에 의해 채용된 RGB 색도 다운샘플링을 비활성화하기 위해 1일 수 있다.<br>이미지 제공 API에서 [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html?lang=ko#image-serving-api)도 참조하세요. |
| `maxpix` | `2000,2000` | 응답 이미지 크기 제한. 클라이언트로 반환되는 응답 이미지의 최대 너비 및 높이입니다.<br>너비 또는 높이가 특성::MaxPix보다 큰 응답 이미지를 요청하면 서버에서 오류가 반환됩니다.<br>이미지 제공 API에서 [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html?lang=ko#image-serving-api)도 참조하십시오. |
| `resmode` | `SHARP2` | 기본 재샘플링 모드. 이미지 데이터 크기를 조정하는 데 사용할 기본 재샘플링 및 보간 특성을 지정합니다.<br>요청에 `resMode=`이(가) 지정되지 않은 경우 사용됩니다.<br>허용되는 값은 `BILIN`, `BICUB` 또는 `SHARP2`입니다.<br>열거형입니다. `bilin`의 경우 2, `bicub`의 경우 3, `sharp2` 보간 모드의 경우 4로 설정합니다. 최상의 결과를 얻으려면 `sharp2` 사용<br>이미지 제공 API에서 [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html?lang=ko#image-serving-api)도 참조하세요. |
| `resolution` | `72` | 기본 오브젝트 확인. 특정 카탈로그 레코드에 유효한 catalog::Resolution 값이 없는 경우 기본 개체 해상도를 제공합니다.<br>실수입니다. 0보다 큽니다. 일반적으로 인치당 픽셀로 표시되지만, 미터당 픽셀과 같은 다른 단위로도 표시할 수 있습니다.<br>이미지 제공 API의 [해상도](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html?lang=ko#image-serving-api)도 참조하세요. |
| `thumbnailtime` | `1%,11%,21%,31%,41%,51%,61%,71%,81%,91%` | 이 값은 비디오 재생 시간의 스냅숏을 나타내며 [encoding.com](https://www.encoding.com/)에 전달됩니다. 자세한 내용은 [비디오 축소판 정보](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode)를 참조하세요. |

## Dynamic Media 색상 관리 구성 {#configuring-dynamic-media-color-management}

Dynamic Media 색상 관리를 사용하면 미리 볼 자산을 색상 수정할 수 있습니다.

색상 수정을 사용하면 수집된 에셋의 색상 공간(RGB, CMYK, 회색)과 생성된 피라미드 TIFF 렌디션에 임베드된 색상 프로파일이 유지됩니다. 동적 렌디션을 요청하면 이미지 색상이 대상 색상 공간으로 수정됩니다. JCR의 Dynamic Media 게시 설정에서 출력 색상 프로파일을 구성합니다.

Adobe의 색상 관리는 ICC에서 정의한 형식인 ICC(International Color Consortium) 프로파일을 사용합니다.

CMYK, RGB 또는 회색 출력을 사용하여 Dynamic Media 색상 관리를 구성하고 이미지 사전 설정을 구성할 수 있습니다. [이미지 사전 설정 구성](/help/assets/managing-image-presets.md)을 참조하십시오.

고급 사용 사례에서는 수동 구성 `icc=` 수정자를 사용하여 출력 색상 프로필을 명시적으로 선택할 수 있습니다.

* `icc` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html?lang=ko](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html?lang=ko)

* `iccEmbed` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html?lang=ko](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html?lang=ko)

>[!NOTE]
>
>표준 Adobe 색상 프로파일 세트는 [소프트웨어 배포의 기능 팩 12445](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445)이 설치된 경우에만 사용할 수 있습니다. 모든 기능 팩과 서비스 팩은 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)에서 사용할 수 있습니다. 기능 팩 12445은 Adobe의 색상 프로필을 제공합니다.


### 기능 팩 12445 설치 {#installing-feature-pack}

Dynamic Media 색상 관리 기능을 사용하려면 기능 팩 을 12445.

**기능 팩 12445 설치:**

1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)&#x200B;(으)로 이동하여 `cq-6.3.0-featurepack-12445`을(를) 다운로드합니다.

   [!DNL Adobe Experience Manager]에서 패키지를 사용하는 방법에 대한 자세한 내용은 [패키지를 사용하여 작업하는 방법](/help/sites-administering/package-manager.md)을 참조하십시오.

1. 기능 팩을 설치합니다.

### 기본 색상 프로파일 구성 {#configuring-the-default-color-profiles}

기능 팩을 설치한 후 RGB 또는 CMYK 이미지 데이터를 요청할 때 색상 수정을 활성화하도록 적절한 기본 색상 프로파일을 구성합니다.

**기본 색 프로필을 구성하려면:**

1. **[!UICONTROL 도구]** > **[!UICONTROL 일반]** > **[!UICONTROL CRXDE Lite]**&#x200B;에서 기본 Adobe Color 프로필이 포함된 `/conf/global/settings/dam/dm/imageserver/jcr:content`(으)로 이동합니다.

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. **[!UICONTROL 속성]** 탭 아래쪽으로 스크롤하여 색상 교정 속성을 추가합니다. 다음 표에 설명된 등록 정보 이름, 유형 및 값을 수동으로 입력합니다. 값을 입력한 후 **[!UICONTROL 추가]**&#x200B;를 선택한 다음 **[!UICONTROL 모두 저장]**&#x200B;을 선택하여 값을 저장합니다.

   색상 교정 속성은 **색상 교정 속성** 표에 설명되어 있습니다. 색상 교정 속성에 지정할 수 있는 값은 **색상 프로필** 표에 있습니다.

   예를 들어 **[!UICONTROL 이름]**&#x200B;에서 `iccprofilecmyk`을(를) 추가하고 **[!UICONTROL 유형]** `String`을(를) 선택한 다음 `WebCoated`을(를) **[!UICONTROL 값]**(으)로 추가합니다. **[!UICONTROL 추가]**&#x200B;를 선택한 다음 **[!UICONTROL 모두 저장]**&#x200B;을 선택하여 값을 저장합니다.

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **색상 수정 속성 표**

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>기본값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html?lang=ko">iccprofilergb</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>기본 RGB 색상 프로필의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html?lang=ko">iccprofilecmyk</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>기본 CMYK 색상 프로파일의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html?lang=ko">iccprofilegray</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>기본 회색 색상 프로파일의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html?lang=ko">iccprofilesrcrgb</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>임베드된 색상 프로파일이 없는 RGB 이미지에 사용되는 기본 RGB 색상 프로파일의 이름</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html?lang=ko">iccprofilesrcmyk</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>임베드된 색상 프로파일이 없는 CMYK 이미지에 사용되는 기본 CMYK 색상 프로파일의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html?lang=ko">iccprofilescrgray</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>임베드된 색상 프로파일이 없는 CMYK 이미지에 사용되는 기본 회색 색상 프로파일의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html?lang=ko">iccblackpointcompensation</a></td>
   <td>부울</td>
   <td>참</td>
   <td>색상 교정 중에 검은 점 보상이 수행되는지 여부를 지정합니다. Adobe에서는 이 설정이 켜져 있을 것을 권장합니다.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html?lang=ko">아이스디더</a></td>
   <td>부울</td>
   <td>거짓</td>
   <td>색상 교정 중에 디더링을 수행할지 여부를 지정합니다.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html?lang=ko">iccrenderintent</a></td>
   <td>문자열</td>
   <td>상대적</td>
   <td><p>렌더링 의도를 지정합니다. 허용되는 값은 <strong>가시 범위, 상대, 채도, 절대입니다. </strong><i></i>Adobe에서는 기본적으로 <strong>상대 </strong><i></i>을(를) 권장합니다.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>속성 이름은 대/소문자를 구분하며 모두 소문자여야 합니다.

**색 프로필 표**

다음 색상 프로파일이 설치됩니다.

<table>
 <tbody>
  <tr>
   <th><p>이름</p> </th>
   <th><p>색상 속도</p> </th>
   <th><p>설명</p> </th>
  </tr>
  <tr>
   <td>Adobe RGB</td>
   <td>RGB</td>
   <td>Adobe RGB (1998)</td>
  </tr>
  <tr>
   <td>애플RGB</td>
   <td>RGB</td>
   <td>Apple RGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>CIE RGB</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>코팅 FOGRA27(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>코팅 FOGRA39(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraaCol</td>
   <td>CMYK</td>
   <td>코팅 GRACoL 2006 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>색상 일치RGB</td>
   <td>RGB</td>
   <td>ColorMatch RGB</td>
  </tr>
  <tr>
   <td>유럽 ISOC 기반</td>
   <td>CMYK</td>
   <td>유럽 ISO 코팅 FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>유로 스케일 코팅 v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncoated</td>
   <td>CMYK</td>
   <td>유로 스케일 코팅되지 않음 v2</td>
  </tr>
  <tr>
   <td>JapanColorCoating</td>
   <td>CMYK</td>
   <td>Japan Color 2001 코팅</td>
  </tr>
  <tr>
   <td>일본 컬러 신문</td>
   <td>CMYK</td>
   <td>일본 색상 2002 신문</td>
  </tr>
  <tr>
   <td>JapanColorUncoating</td>
   <td>CMYK</td>
   <td>Japan Color 2001 무코팅</td>
  </tr>
  <tr>
   <td>JapanColorWebCoating</td>
   <td>CMYK</td>
   <td>Japan Color 2003 웹 코팅</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>Japan Web Coated (Ad)</td>
  </tr>
  <tr>
   <td>신문 인쇄2007</td>
   <td>CMYK</td>
   <td>미국 신문용지(SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC(1953)</td>
  </tr>
  <tr>
   <td>PAL</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>ProPhoto RGB</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMYK</td>
   <td>Photoshop 4 기본 CMYK</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMYK</td>
   <td>Photoshop 5 기본 CMYK</td>
  </tr>
  <tr>
   <td>SheetfedCoating</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Coated v2</td>
  </tr>
  <tr>
   <td>SheetfedUncoating</td>
   <td>CMYK</td>
   <td>미국 Sheetfed Uncoated v2</td>
  </tr>
  <tr>
   <td>SMPTE</td>
   <td>RGB</td>
   <td>SMPTE-C</td>
  </tr>
  <tr>
   <td>sRGB</td>
   <td>RGB</td>
   <td>sRGB IEC61966-2.1</td>
  </tr>
  <tr>
   <td>UncoatedFogra29</td>
   <td>CMYK</td>
   <td>코팅되지 않은 FOGRA29(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>웹 코팅</td>
   <td>CMYK</td>
   <td>U.S. Web Coated (SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>웹 코팅 FOGRA28 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Web Coated SWOP 2006 Grade 3 용지</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>웹코팅 SWOP 2006 Grade 5 용지</td>
  </tr>
  <tr>
   <td>웹 코팅되지 않음</td>
   <td>CMYK</td>
   <td>U.S. Web Uncoated v2</td>
  </tr>
  <tr>
   <td>광영역RGB</td>
   <td>RGB</td>
   <td>광영역 RGB</td>
  </tr>
 </tbody>
</table>

1. **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.

예를 들어 **[!UICONTROL iccprofilergb]**&#x200B;을(를) `sRGB`(으)로 설정하고 **[!UICONTROL iccprofilecmyk]**&#x200B;을(를) **[!UICONTROL WebCoated]**(으)로 설정할 수 있습니다.

이렇게 하면 다음 작업이 수행됩니다.

* RGB 및 CMYK 이미지에 대해 색상 교정을 활성화합니다.
* 색상 프로파일이 없는 RGB 이미지는 *sRGB* 색상 공간에 있는 것으로 간주됩니다.
* 색상 프로필이 없는 CMYK 이미지는 *WebCoated* 색상 공간에 있는 것으로 간주됩니다.
* RGB 출력을 반환하고 *sRGB *색상 공간으로 반환하는 동적 변환입니다.
* CMYK 출력을 반환하고 *WebCoated* 색상 공간으로 반환하는 동적 변환입니다.

## Assets 제공 {#delivering-assets}

위의 모든 작업을 완료하면 이미지 또는 비디오 서비스에서 활성화된 Dynamic Media 자산이 제공됩니다. Experience Manager에서 이 기능은 **[!UICONTROL 이미지 URL 복사]**, **[!UICONTROL 뷰어 URL 복사]**, **[!UICONTROL 뷰어 코드 포함]** 및 WCM에 표시됩니다.

[Dynamic Media Assets 배달](/help/assets/delivering-dynamic-media-assets.md)을 참조하세요.

<table>
 <tbody>
  <tr>
   <td><strong>다음을 수행하는 경우</strong></td>
   <td><strong>결과</strong></td>
  </tr>
  <tr>
   <td>이미지 URL 복사</td>
   <td><p>URL 복사 대화 상자에는 다음과 유사한 URL이 표시됩니다(URL은 데모용으로만 사용).</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>여기서 <code>IMAGESERVICEPUBLISHNODE</code>은(는) 이미지 서비스 URL을 나타냅니다.</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media Assets 배달</a>도 참조하세요.</p> </td>
  </tr>
  <tr>
   <td>뷰어 URL 복사</td>
   <td><p>URL 복사 대화 상자에는 다음과 유사한 URL이 표시됩니다(URL은 데모용으로만 사용).</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>여기서 <code>PUBLISHNODE</code>은(는) 일반 Experience Manager 게시 노드를 참조하고 <code>IMAGESERVICEPUBLISHNODE</code>은(는) 이미지 서비스 URL을 참조합니다.</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media Assets 배달</a>도 참조하세요.</p> </td>
  </tr>
  <tr>
   <td>뷰어의 포함 코드 복사</td>
   <td><p>포함 코드 복사 대화 상자에는 다음과 유사한 코드 조각이 표시됩니다(코드 샘플은 데모용으로만 사용됨).</p> <p><code class="code">&lt;style type="text/css"&gt;
       &#x200B;#s7basiczoom_div.s7basiczoomviewer&lbrace;
       width:100%;
       height:auto;
       &rbrace;
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer(&lbrace;
       "containerId" : "s7basiczoom_div",
       "params" : &lbrace;
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" &rbrace;
       &rbrace;).init();
       &lt;/script&gt;</code></p> <p>여기서 <code>PUBLISHNODE</code>은(는) 일반 Experience Manager 게시 노드를 참조하고 <code>IMAGESERVICEPUBLISHNODE</code>은(는) 이미지 서비스 URL을 참조합니다.</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media Assets 배달</a>도 참조하세요.</p> </td>
  </tr>
 </tbody>
</table>

### WCM Dynamic Media 및 대화형 미디어 구성 요소 {#wcm-dynamic-media-and-interactive-media-components}

Dynamic Media 및 대화형 미디어 구성 요소를 참조하는 WCM 페이지는 게재 서비스를 참조합니다.
