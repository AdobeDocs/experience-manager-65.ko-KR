---
title: Dynamic Media 구성 - 하이브리드 모드
description: Dynamic Media 구성 방법 - 하이브리드 모드
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
translation-type: tm+mt
source-git-commit: df89d5cfd5060d493babb89e92a9a98e851b8879
workflow-type: tm+mt
source-wordcount: '8031'
ht-degree: 1%

---


# Dynamic Media 구성 - 하이브리드 모드{#configuring-dynamic-media-hybrid-mode}

Dynamic Media-Hybrid를 사용하도록 활성화하고 구성해야 합니다. 사용 사례에 따라 Dynamic Media에는 몇 가지 [지원되는 구성이 있습니다](#supported-dynamic-media-configurations).

>[!NOTE]
>
>Scene7 실행 모드에서 Dynamic Media을 구성하고 실행하려면 Dynamic Media 구성 - [Scene7 모드를 참조하십시오](/help/assets/config-dms7.md).
>
>하이브리드 실행 모드에서 Dynamic Media을 구성하고 실행하려면 이 페이지의 지침을 따르십시오.

Dynamic Media에서 [비디오](/help/assets/video.md) 작업에 대한 자세한 내용을 살펴보십시오.

>[!NOTE]
>
>개발 환경, 스테이징용 및 라이브 프로덕션용 환경과 같이 서로 다른 환경에 대해 설정된 Adobe Experience Manager을 사용하는 경우 해당 환경 각 환경에 대해 Dynamic Media Cloud Service을 구성해야 합니다.

>[!NOTE]
>
>Dynamic Media 구성에 문제가 있는 경우 중요한 위치를 동적 미디어 관련 로그 파일입니다. 다이내믹 미디어를 활성화하면 자동으로 설치됩니다.
>
>* `s7access.log`
>* `ImageServing.log`

>
>
AEM 인스턴스 [모니터링 및 유지 관리에 설명되어 있습니다](/help/sites-deploying/monitoring-and-maintaining.md).

하이브리드 게시 및 전달은 Adobe Experience Manager에 추가되는 Dynamic Media의 핵심 기능입니다. 하이브리드 게시를 사용하면 AEM 게시 노드가 아닌 클라우드에서 이미지, 세트 및 비디오와 같은 Dynamic Media 자산을 제공할 수 있습니다.

Dynamic Media 뷰어, 사이트 페이지 및 정적 컨텐츠와 같은 기타 컨텐츠는 AEM 게시 노드에서 계속 제공됩니다.

Dynamic Media의 고객인 경우 모든 Dynamic Media 컨텐츠의 전달 메커니즘으로 하이브리드 배달을 사용해야 합니다.

## 비디오용 하이브리드 게시 아키텍처 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## 이미지를 위한 하이브리드 출판 아키텍처 {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## 지원되는 Dynamic Media 구성 {#supported-dynamic-media-configurations}

다음 용어를 참조하는 구성 작업:

| **용어** | **Dynamic Media 사용** | **설명** |
|---|---|---|
| AEM 작성자 노드 | 녹색 원의 흰색 확인 표시 | 온프레미스 또는 Managed Services를 통해 배포하는 작성자 노드입니다. |
| AEM 게시 노드 | 흰색 &quot;X&quot;가 빨간색 사각형입니다. | 온프레미스 또는 Managed Services를 통해 배포하는 게시 노드입니다. |
| 이미지 서비스 게시 노드 | 흰색 체크 표시는 녹색 원으로 되어 있습니다. | Adobe에서 관리하는 데이터 센터에서 실행하는 게시 노드입니다. 이미지 서비스 URL을 참조합니다. |

이미징용, 비디오용 또는 이미징 및 비디오 모두에 대해 Dynamic Media을 구현할 수 있습니다. 특정 시나리오에 대한 Dynamic Media 구성 단계를 결정하려면 다음 표를 참조하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>시나리오</strong></td>
   <td ><strong>사용 방법</strong></td>
   <td><strong>구성 단계</strong></td>
  </tr>
  <tr>
   <td>프로덕션에 이미지만 제공</td>
   <td>이미지는 Adobe의 전 세계 데이터 센터의 서버를 통해 배달된 다음 CDN에서 캐시하여 확장 가능한 성능과 글로벌 접근을 가능하게 합니다.</td>
   <td>
    <ol>
     <li>AEM <strong>작성자</strong> 노드에서 다이내믹 미디어를 <a href="#enabling-dynamic-media">활성화합니다</a>.</li>
     <li>Dynamic Media Cloud Service에서 <a href="#configuring-dynamic-media-cloud-services">이미징을 구성합니다</a>.</li>
     <li><a href="#configuring-image-replication">이미지 복제를 구성합니다</a>.</li>
     <li><a href="#replicating-catalog-settings">카탈로그 설정</a>복제</li>
     <li><a href="#replicating-viewer-presets">뷰어 사전 설정 복제</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">복제에 기본 자산 필터를 사용합니다</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media 이미지 서버 설정을 구성합니다</a>.</li>
     <li><a href="#delivering-assets">자산</a>전달</li>
    </ol> </td>
  </tr>
  <tr>
   <td>프리 프로덕션(Dev, QE, Stage 등)으로 이미지만 제공</td>
   <td>이미지는 AEM 게시 노드를 통해 전달됩니다. 이 시나리오에서는 트래픽이 최소적이기 때문에 Adobe 데이터 센터로 이미지를 전달할 필요가 없습니다. 또한 프로덕션 시작 전에 컨텐츠를 안전하게 미리 볼 수 있습니다</td>
   <td>
    <ol>
     <li>AEM <strong>작성자</strong> 노드에서 다이내믹 미디어를 <a href="#enabling-dynamic-media">활성화합니다</a>.</li>
     <li>AEM <strong>게시</strong> 노드에서 <a href="#enabling-dynamic-media">다이내믹 미디어를 활성화합니다</a>.</li>
     <li><a href="#replicating-viewer-presets">뷰어 사전 설정 복제</a>.</li>
     <li>비프로덕션 이미지에 대한 <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">자산 필터를 설정합니다</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media 이미지 서버 설정을 구성합니다.</a></li>
     <li><a href="#delivering-assets">자산 전달</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>모든 환경(프로덕션, 개발, QE, 스테이지 등)에서 비디오만 전달</td>
   <td>CDN은 비디오를 전달하고 캐시하여 확장 가능한 성능과 글로벌 범위를 지원합니다. 비디오 포스터 이미지(재생을 시작하기 전에 표시되는 비디오 축소판)는 AEM 게시 인스턴스에서 전달됩니다.</td>
   <td>
    <ol>
     <li>AEM <strong>작성자</strong> 노드에서 다이내믹 미디어를 <a href="#enabling-dynamic-media">활성화합니다</a>.</li>
     <li>AEM <strong>게시</strong> 노드에서 다이내믹 미디어 <a href="#enabling-dynamic-media">를</a> 활성화합니다(게시 인스턴스는 비디오 포스터 이미지를 제공하고 비디오 재생을 위한 메타데이터를 제공합니다).</li>
     <li>Dynamic Media Cloud Service에서 비디오를 <a href="#configuring-dynamic-media-cloud-services">구성합니다.</a></li>
     <li><a href="#replicating-viewer-presets">뷰어 사전 설정 복제</a>.</li>
     <li>비디오 전용 <a href="#setting-up-asset-filters-for-video-only-deployments">자산 필터를 설정합니다</a>.</li>
     <li><a href="#delivering-assets">자산 전달</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>프로덕션에 이미지와 비디오 모두 전달</td>
   <td><p>CDN은 비디오를 전달하고 캐시하여 확장 가능한 성능과 글로벌 범위를 지원합니다. 이미지 및 비디오 포스터 이미지는 Adobe의 전세계 데이터 센터의 서버를 통해 배달된 다음 CDN에서 캐시하여 확장 가능한 성능과 글로벌 접근을 가능하게 합니다.</p> <p>사전 제작 시 이미지 또는 비디오를 설정하려면 이전 섹션을 참조하십시오. </p> </td>
   <td>
    <ol>
     <li>AEM <strong>작성자</strong> 노드에서 다이내믹 미디어를 <a href="#enabling-dynamic-media">활성화합니다</a>.</li>
     <li>Dynamic Media Cloud Service에서 비디오를 <a href="#configuring-dynamic-media-cloud-services">구성합니다.</a></li>
     <li>Dynamic Media Cloud Service에서 <a href="#configuring-dynamic-media-cloud-services">이미징 구성</a></li>
     <li><a href="#configuring-image-replication">이미지 복제를 구성합니다</a>.</li>
     <li><a href="#replicating-catalog-settings">카탈로그 설정</a>복제</li>
     <li><a href="#replicating-viewer-presets">뷰어 사전 설정 복제</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">복제에 기본 자산 필터를 사용합니다.</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media 이미지 서버 설정을 구성합니다.</a></li>
     <li><a href="#delivering-assets">자산 전달</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Dynamic Media 활성화 {#enabling-dynamic-media}

[다이내믹 미디어](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) 기능은 기본적으로 비활성화됩니다. 다이내믹 미디어 기능을 활용하려면 실행 모드와 같이 `dynamicmedia` 실행 모드를 사용하여 다이내믹 미디어를 `publish` 활성화해야 합니다. 활성화하기 전에 [기술 요구 사항을 검토하십시오.](/help/sites-deploying/technical-requirements.md#dynamicmediaaddonprerequisites)

>[!NOTE]
>
>실행 모드를 통해 동적 미디어를 활성화하는 것은 플래그를 `dynamicMediaEnabled` true로 설정하여 동적 미디어를 활성화한 AEM 6.1 및 AEM 6.0의 기능을 대체합니다 ****. 이 플래그는 AEM 6.2 이상 버전에 기능이 없습니다. 또한 다이내믹 미디어를 활성화하기 위해 빠른 시작을 다시 시작할 필요가 없습니다.

Dynamic Media을 활성화하면 UI에서 다이내믹 미디어 기능을 사용할 수 있고 업로드된 모든 이미지 자산은 다이내믹 이미지 표현물을 신속하게 전달하는 데 사용되는 *cqdam.pyramid.tiff* 표현물을 받습니다. 이러한 PTIFF는 (1) 추가 저장 공간 없이 단일 기본 소스 이미지만을 관리하고 무한 변환을 즉석에서 생성할 수 있는 기능, (2) 확대/축소, 이동, 회전 등과 같은 대화형 시각화를 사용할 수 있는 기능 등 많은 이점을 제공합니다.

AEM에서 Dynamic Media Classic(Scene7)을 사용하려면 [특정 시나리오를 사용하지 않는 한 Dynamic Media을 활성화하지 말아야 합니다](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). 실행 모드를 통해 다이내믹 미디어를 활성화하지 않으면 Dynamic Media이 비활성화됩니다.

다이내믹 미디어를 활성화하려면 명령줄 또는 빠른 시작 파일 이름에서 다이내믹 미디어 실행 모드를 활성화해야 합니다.

**다이내믹 미디어를 활성화하려면**

1. 명령줄에서 quickstart를 시작할 때 다음을 수행합니다.

   * jar 파일 `-r dynamicmedia` 을 시작할 때 명령줄 끝에 추가합니다.

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   s7delivery에 게시하는 경우 다음 trustStore 인수도 포함해야 합니다.

   ```
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. 이미지 서버 `https://localhost:4502/is/image` 가 실행 중인지 요청하고 확인합니다.

   >[!NOTE]
   >
   >Dynamic Media 관련 문제를 해결하려면 다음 로그를 `crx-quickstart/logs/` 참조하십시오.
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log - ImageServer 로그는 내부 ImageServer 프로세스의 동작을 분석하는 데 사용되는 통계 및 분석 정보를 제공합니다.

   이미지 서버 로그 파일 이름의 예: `ImageServer-57346-2020-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - s7access 로그는 `/is/image` 및 를 통해 Dynamic Media에 대한 각 요청을 기록합니다 `/is/content`.

   이러한 로그는 Dynamic Media이 활성화된 경우에만 사용됩니다. 페이지에서 생성된 전체 **다운로드** 패키지에 `system/console/status-Bundlelist` 포함되지 않습니다. Dynamic Media 문제가 있는 경우 고객 지원에 문의할 때 이 두 로그를 모두 문제에 추가하십시오.

### 다른 포트 또는 컨텍스트 경로에 AEM을 설치한 경우.. {#if-you-installed-aem-to-a-different-port-or-context-path}

응용 프로그램 서버에 [AEM을 배포하고 Dynamic Media](/help/sites-deploying/application-server-install.md) 을 활성화한 경우 외부 **에서 자체** 도메인을 구성해야 합니다. 그렇지 않으면 다이내믹 미디어 에셋에 대해 축소판 생성이 제대로 작동하지 않습니다.

또한 다른 포트나 컨텍스트 경로에서 빠른 시작을 실행하는 경우 **자체** 도메인도 변경해야 합니다.

Dynamic Media이 활성화되면 이미지 자산에 대한 정적 축소판 표현물은 Dynamic Media을 사용하여 생성됩니다. 동적 미디어에 대해 축소판 생성이 제대로 작동하려면 AEM에서 URL 요청을 자체에 수행해야 하며 포트 번호와 컨텍스트 경로를 모두 알고 있어야 합니다.

AEM에서:

* 외부 **도우미의** 자체 [도메인은](/help/sites-developing/externalizer.md) 포트 번호와 컨텍스트 경로를 모두 검색하는 데 사용됩니다.
* 자체 **도메인이 구성되지** 않으면 포트 번호와 컨텍스트 경로가 Jetty HTTP 서비스에서 검색됩니다.

AEM QuickStart WAR 배포에서는 포트 번호와 컨텍스트 경로를 파생할 수 없으므로 **자체** 도메인을 구성해야 합니다. 자체 [도메인을 구성하는](/help/sites-developing/externalizer.md) 방법은 externalizer 설명서를 **참조하십시오** .

>[!NOTE]
AEM [Quickstart 독립](/help/sites-deploying/deploy.md)실행형 배포에서는 포트 번호와 컨텍스트 경로를 자동으로 구성할 수 있으므로 **자체** 도메인을 구성할 필요가 없습니다. 그러나 모든 네트워크 인터페이스가 꺼져 있으면 자체 **도메인을** 구성해야 합니다.

## Dynamic Media 비활성화  {#disabling-dynamic-media}

다이내믹 미디어는 기본적으로 활성화되어 있지 않습니다. 하지만, 이전에 다이내믹 미디어를 활성화한 경우 나중에 끌 수도 있습니다.

동적 미디어를 활성화한 후 비활성화하려면 `-r dynamicmedia` 실행 모드 플래그를 제거합니다.

**Dynamic Media을 활성화한 후 비활성화하려면**

1. 명령줄에서 quickstart를 시작할 때 다음 중 하나를 수행할 수 있습니다.

   * jar 파일 `-r dynamicmedia` 을 시작할 때는 명령줄에 추가하지 마십시오.

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. 요청 `https://localhost:4502/is/image`. Dynamic Media을 사용할 수 없다는 메시지가 표시됩니다.

   >[!NOTE]
   Dynamic Media 실행 모드가 비활성화되면 변환을 생성하는 워크플로우 단계가 자동으로 `cqdam.pyramid.tiff` 생략됩니다. 또한 동적 변환 지원 및 기타 Dynamic Media 기능이 비활성화됩니다.
   또한 AEM 서버를 구성한 후 Dynamic Media 실행 모드가 비활성화된 경우 해당 실행 모드에서 업로드된 모든 자산이 이제 유효하지 않습니다.

## (선택 사항) 6.3에서 6.5 가동 중지 시간 제로 Dynamic Media 사전 설정 및 구성 마이그레이션 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

AEM Dynamic Media을 6.3에서 6.5로 업그레이드하는 경우(이제 가동 중지 시간 없이 배포할 수 있는 기능이 포함), 다음 curl 명령을 실행하여 모든 사전 설정 및 구성을 CRXDE Lite에서 `/etc` 로 마이그레이션해야 `/conf` 합니다.

**참고**: 호환성 모드에서 AEM 인스턴스를 실행하는 경우, 호환성 패키지가 설치되어 있으므로 이러한 명령을 실행할 필요가 없습니다.

호환성 패키지 유무와 상관없이 모든 업그레이드의 경우 다음 Linux 말림 명령을 실행하여 원래 Dynamic Media과 함께 제공된 기본 기본 기본 기본 뷰어 사전 설정을 복사할 수 있습니다.

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

에서 사용자 정의 뷰어 사전 설정과 구성을 마이그레이션하려면 다음 Linux `/etc` curl 명령을 `/conf`실행하십시오.

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 이미지 복제 구성 {#configuring-image-replication}

Dynamic Media 이미지 전달은 AEM Author에서 비디오 축소판과 같은 이미지 자산을 게시하여 Adobe의 on-demand 복제 서비스(Replication Service URL)에 복제하는 방식으로 작동합니다. 그런 다음 On-Demand 이미지 전달 서비스(이미지 서비스 URL)를 통해 에셋이 전달됩니다.

다음을 수행해야 합니다.

1. [인증을 설정합니다](#setting-up-authentication).
1. [복제 에이전트를 구성합니다](#configuring-the-replication-agent).

복제 에이전트는 이미지, 비디오 메타데이터 및 세트와 같은 Dynamic Media 자산을 게시하고 Adobe 호스팅 이미지 서비스에 설정합니다. 기본적으로 복제 에이전트가 활성화되지 않습니다.

복제 에이전트를 구성한 후에는 [성공적으로 설정되었는지 확인하고 테스트해야 합니다](#validating-the-replication-agent-for-dynamic-media). 이 섹션에서는 이러한 절차에 대해 설명합니다.

>[!NOTE]
PTIFF 작성의 기본 메모리 제한은 모든 워크플로우에서 3GB입니다. 예를 들어, 다른 워크플로가 일시 정지되는 동안 3GB의 메모리가 필요한 하나의 이미지를 처리하거나 각 이미지에 300MB의 메모리가 필요한 10개의 이미지를 동시에 처리할 수 있습니다.
메모리 제한은 구성 가능하고 시스템 리소스 사용 가능 여부 및 처리 중인 이미지 컨텐츠 유형에 적합해야 합니다. 시스템에 매우 큰 에셋이 있고 메모리가 충분하면 이 제한을 늘려 이미지가 동시에 처리되도록 할 수 있습니다.
최대 메모리 제한을 초과하는 이미지가 거부됩니다.
PTIFF 만들기의 메모리 제한을 변경하려면 **[!UICONTROL 도구 > 작업 > 웹 콘솔 > Adobe CQ Scene7 PTiffManager로]** 이동하여 **[!UICONTROL maxMemory]** 값을 변경합니다.

### 인증 설정 {#setting-up-authentication}

Dynamic Media 이미지 배달 서비스에 이미지를 복제하려면 작성자에 대한 복제 인증을 설정해야 합니다. 이렇게 하려면 KeyStore를 가져온 다음 **[!UICONTROL dynamic-media-replication]** 사용자 아래에 저장하고 구성합니다. 제공 프로세스 중에 회사 관리자가 KeyStore 파일과 필요한 자격 증명이 포함된 환영 이메일을 수신해야 합니다. 수신하지 못한 경우 고객 지원 센터에 문의하십시오.

**인증을 설정하려면**

1. 아직 KeyStore 파일 및 암호를 보유하고 있지 않은 경우 고객 지원 센터에 문의하십시오. 이 설정은 프로비저닝의 일부이며 해당 키를 계정에 연결합니다.
1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구 > 보안 > 사용자를 누릅니다]**.
1. 사용자 관리 페이지에서 **[!UICONTROL 다이내믹 미디어 복제]** 사용자로 이동한 다음 을 눌러 엽니다.

   ![dm-replication](assets/dm-replication.png)

1. Edit User Settings For Dynamic-media-replication 페이지에서 Keystore **[!UICONTROL 탭을]** 누른 다음 KeyStore **[!UICONTROL 만들기를 클릭합니다]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. [KeyStore 액세스 암호 설정] 대화 상자에서 **[!UICONTROL 암호를 입력하고 암호를]** 확인합니다.

   >[!NOTE]
   입력한 암호를 기억하십시오. 나중에 복제 에이전트를 구성할 때 다시 입력해야 합니다.

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. [ **[!UICONTROL 동적 미디어 복제를 위한 사용자 설정 편집]** ] 페이지에서 KeyStore 파일 **** 영역에서 개인 키 추가 영역을 확장하고 다음을 추가합니다(다음 이미지 참조).

   * 새 **[!UICONTROL 별칭]** 필드에 나중에 복제 구성에서 사용할 별칭의 이름을 입력합니다. 예를 들면 다음과 같습니다 `replication`.
   * KeyStore **[!UICONTROL 파일을 누릅니다]**. Adobe에서 제공한 KeyStore 파일로 이동하여 선택한 다음 **[!UICONTROL 열기를 누릅니다]**.
   * KeyStore **[!UICONTROL 파일 암호]** 필드에 KeyStore 파일 암호를 입력합니다. 이 암호는 5단계에서 만든 KeyStore 암호가 **아니지만** Adobe에서 제공하는 KeyStore 파일 암호입니다. KeyStore 파일 암호를 받지 못한 경우 Adobe 고객 지원 센터에 문의하십시오.
   * 개인 **[!UICONTROL 키 암호]** 필드에 개인 키 암호를 입력합니다(이전 단계에서 제공한 개인 키 암호와 동일할 수 있음). Adobe는 제공하는 동안 사용자에게 보낸 환영 이메일에 개인 키 암호를 제공합니다. 개인 키 암호를 받지 않은 경우 Adobe 고객 지원 센터에 문의하십시오.
   * 개인 **[!UICONTROL 키 별칭]** 필드에 개인 키 별칭을 입력합니다. 예, `*companyname*-alias`. Adobe는 제공하는 동안 귀하에게 보낸 환영 이메일에 개인 키 별칭을 제공합니다. 개인 키 별칭을 받지 않은 경우 Adobe 고객 지원 센터에 문의하십시오.

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. 저장 **[!UICONTROL 및 닫기를]** 눌러 변경 사항을 이 사용자에게 저장합니다.

   다음으로 복제 에이전트를 [구성해야 합니다.](#configuring-the-replication-agent)

### 복제 에이전트 구성 {#configuring-the-replication-agent}

1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구 > 배포 > 복제 > 작성자의 에이전트를 누릅니다]**.
1. 작성자 페이지의 에이전트 페이지에서 **[!UICONTROL Dynamic Media 하이브리드 이미지 복제(s7delivery)를 누릅니다]**.
1. 편집을 **[!UICONTROL 누릅니다]**.
1. 설정 **[!UICONTROL 탭을]** 누른 다음 다음을 입력합니다.

   * **[!UICONTROL 활성화됨]** - 복제 에이전트를 활성화하려면 이 확인란을 선택합니다.
   * **[!UICONTROL 지역]** - 해당 지역으로 설정합니다. 북미, 유럽 또는 아시아
   * **[!UICONTROL 테넌트 ID]** - 이 값은 Replication Service에 게시되는 회사/테넌트의 이름입니다. 이 값은 프로비전 중에 Adobe가 사용자에게 보낸 환영 이메일에서 제공하는 테넌트 ID입니다. 받지 못한 경우 Adobe 고객 지원 센터에 문의하십시오.
   * **[!UICONTROL 키 저장소 별칭]** - 이 값은 인증 설정에서 키를 생성할 때 설정된** 새 별칭** 값 [과 같습니다](#setting-up-authentication). 예를 들면 다음과 같습니다 `replication`. (인증 [설정의 7단계를 참조하십시오](#setting-up-authentication).)
   * **[!UICONTROL 키 저장소 암호]** - 키 저장소 만들기를 탭했을 때 만들어진 키 **[!UICONTROL 스토어 암호입니다]**. Adobe는 이 암호를 제공하지 않습니다. 인증 [설정의 5단계를 참조하십시오](#setting-up-authentication).

   다음 이미지는 샘플 데이터가 있는 복제 에이전트를 보여줍니다.

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. 확인을 **[!UICONTROL 누릅니다]**.

### Dynamic Media에 대한 복제 에이전트 유효성 확인 {#validating-the-replication-agent-for-dynamic-media}

다이내믹 미디어용 복제 에이전트의 유효성을 확인하려면 다음을 수행하십시오.

연결 **[!UICONTROL 테스트를 누릅니다]**. 출력의 예는 다음과 같습니다.

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
다음 중 하나를 수행하여 확인할 수도 있습니다.
* 복제 로그를 확인하여 자산이 복제되었는지 확인합니다.
* 이미지를 게시합니다. 이미지를 누르고 **[!UICONTROL 드롭다운 메뉴에서]** 뷰어를 선택합니다. 뷰어 사전 설정을 선택한 다음 URL을 클릭하고 브라우저에서 URL을 복사/붙여 넣어 이미지가 표시되는지 확인합니다.



### 인증 문제 해결 {#troubleshooting-authentication}

인증을 설정할 때 솔루션 관련 몇 가지 문제가 있습니다. 이러한 사항을 확인하기 전에 복제를 설정했는지 확인하십시오.

#### 문제: HTTP 상태 코드 401(메시지 포함) - 인증 필요 {#problem-http-status-code-with-message-authorization-required}

이 문제는 `dynamic-media-replication` 사용자에 대해 KeyStore를 설정하지 못하여 발생할 수 있습니다.

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

**솔루션**: 이 `KeyStore` 가 **다이내믹 미디어 복제** 사용자에게 저장되고 올바른 암호가 제공되는지 확인하십시오.

#### 문제: 키를 해독할 수 없습니다. 데이터의 암호를 해독할 수 없습니다. {#problem-could-not-decrypt-key-could-not-decrypt-data}

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

**솔루션**: 암호를 확인합니다. 복제 에이전트에 저장된 암호가 키 저장소를 만드는 데 사용한 암호와 다릅니다.

#### 문제: InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

이 문제는 AEM Author 인스턴스의 구성 오류로 인해 발생합니다. 작성자의 Java 프로세스가 정확하지 않습니다 `javax.net.ssl.trustStore`. 복제 로그에 다음 오류가 표시됩니다.

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

**솔루션**: AEM Author의 java 프로세스에 시스템 속성이 유효한 truststore `-Djavax.net.ssl.trustStore=` 로 설정되어 있는지 확인하십시오.

#### 문제: KeyStore가 설정되지 않았거나 초기화되지 않았습니다. {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

이 문제는 핫픽스 또는 기능 팩이 dynamic-media-user 또는 keystore 노드를 덮어쓰는 경우 발생할 수 있습니다.

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

**솔루션**:

1. 사용자 관리 페이지로 이동합니다.
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. 사용자 관리 페이지에서 사용자를 탐색한 다음 을 눌러 `dynamic-media-replication` 엽니다.
1. Click the **[!UICONTROL KeyStore]** tab. KeyStore **[!UICONTROL 만들기]** 단추가 나타나면 이전에 인증 [설정](#setting-up-authentication) 단계를 다시 실행해야 합니다.
1. KeyStore 설정을 다시 실행해야 하는 경우 복제 에이전트 [를 다시](/help/assets/config-dynamic.md#configuring-the-replication-agent) 구성해야 할 수도 있습니다.

   s7delivery 복제 에이전트를 다시 구성하십시오.
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. 연결 **[!UICONTROL 테스트를]** 눌러 구성이 유효한지 확인합니다.

#### 문제: 게시 에이전트가 OAuth 대신 SSL을 사용하고 있습니다. {#problem-publish-agent-is-using-ssl-instead-of-oauth}

이 문제는 핫픽스 또는 설정이 올바르게 설치되지 않았거나 잘못 쓴 기능 팩으로 인해 발생할 수 있습니다.

복제 로그 예:

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

1. AEM에서 도구 > **[!UICONTROL 일반 > CRXDE Lite를 클릭합니다]**.

   `localhost:4502/crx/de/index.jsp`

1. s7delivery 복제 에이전트 노드로 이동합니다.
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. 복제 에이전트에 이 설정을 추가합니다(값이 **[!UICONTROL True로 설정된 부울]**).

   `enableOauth=true`

1. 페이지의 왼쪽 위 모서리 근처에 있는 **[!UICONTROL 모두 저장을 탭합니다]**.

### 구성 테스트 {#testing-your-configuration}

구성에 대한 엔드 투 엔드 테스트를 수행하는 것이 좋습니다.

이 테스트를 시작하기 전에 다음을 이미 수행했는지 확인하십시오.

* 이미지 사전 설정이 추가되었습니다.
* Cloud Service에서 **[!UICONTROL Dynamic Media 구성(6.3 이전)]** 구성 이 테스트에 필요한 이미지 서비스 URL

**구성을 테스트하려면**

1. 이미지 자산을 업로드합니다. (자산에서 **[!UICONTROL 만들기 > 파일]** 을 누르고 파일을 선택합니다.)
1. 워크플로가 완료될 때까지 기다립니다.
1. 이미지 자산을 게시합니다. 자산을 선택하고 빠른 게시 **[!UICONTROL 를 누릅니다]**.
1. 이미지를 열고 표현물을 눌러 해당 이미지의 표현물로 **[!UICONTROL 이동합니다]**.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. 동적 변환을 선택합니다.
1. 이 **[!UICONTROL 자산의 URL을]** 얻으려면 URL을 클릭합니다.
1. 선택한 URL로 이동하고 이미지가 예상대로 작동하는지 확인합니다.

자산이 배달되었는지 테스트하는 또 다른 방법은 URL에 req=exists를 추가하는 것입니다.

## Configuring Dynamic Media Cloud Services {#configuring-dynamic-media-cloud-services}

Dynamic Media 클라우드 서비스는 다양한 이미지 및 비디오 게시, 비디오 분석, 비디오 인코딩 등 클라우드 서비스를 지원합니다.

구성의 일부로 등록 ID, 비디오 서비스 URL, 이미지 서비스 URL, 복제 서비스 URL 및 인증을 설정해야 합니다. 이 모든 정보는 계정 프로비저닝 프로세스의 일부로 수신되어야 합니다. 이 정보를 받지 못한 경우 Adobe Experience Manager 관리자나 Adobe 기술 지원 센터에 문의하여 정보를 얻으십시오.

>[!NOTE]
Dynamic Media 클라우드 서비스를 설정하기 전에 게시 인스턴스를 설정해야 합니다. 또한 Dynamic Media 클라우드 서비스를 구성하기 전에 복제를 설정해야 합니다.

다이내믹 미디어 클라우드 서비스를 구성하려면:

1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스하고 **[!UICONTROL 도구 > Cloud Service > Dynamic Media 구성(Pre-6.3)을 누릅니다]**.
1. Dynamic Media 구성 브라우저 페이지의 왼쪽 창에서 **[!UICONTROL 전역]**&#x200B;을 선택한 다음 **[!UICONTROL 만들기를 누릅니다]**.
1. Dynamic Media **[!UICONTROL 구성]** 만들기 대화 상자의 제목 필드에 제목을 입력합니다.
1. 비디오용 Dynamic Media을 구성하는 경우

   * 등록 **[!UICONTROL ID]** 필드에 등록 ID를 입력합니다.
   * [ **[!UICONTROL 비디오 서비스 URL ]**] 필드에 Dynamic Media 게이트웨이의 비디오 서비스 URL을 입력합니다.

1. 이미징을 위한 Dynamic Media을 구성하는 경우 **[!UICONTROL 이미지 서비스 URL]** 필드에 Dynamic Media 게이트웨이의 이미지 서비스 URL을 입력합니다.
1. 저장 **[!UICONTROL 을]** 눌러 Dynamic Media 구성 브라우저 페이지로 돌아갑니다.
1. AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스합니다.

## 비디오 보고 구성 {#configuring-video-reporting}

Dynamic Media Hybrid를 사용하여 AEM의 여러 설치 간에 비디오 보고를 구성할 수 있습니다.

**사용 시기:** Dynamic Media 구성(6.3 이전)을 구성할 때 비디오 보고를 포함하여 다양한 기능이 시작됩니다. 구성은 지역 Analytics 회사에 보고서 세트를 만듭니다. 여러 작성자 노드를 구성하는 경우 각각에 대해 별도의 보고서 세트를 만듭니다. 따라서 보고서 데이터가 설치 간에 일치하지 않습니다. 또한 각 작성자 노드가 동일한 하이브리드 게시 서버를 참조하는 경우 마지막 작성자 설치는 모든 비디오 보고에 대한 대상 보고서 세트를 변경합니다. 이 문제는 보고서 세트가 너무 많은 Analytics 시스템을 오버로드합니다.

**시작하기:** 다음 세 가지 작업을 완료하여 비디오 보고를 구성합니다.

1. 첫 번째 작성자 노드에서 Dynamic Media 구성(6.3 이전)을 구성한 후 비디오 Analytics 사전 설정 패키지를 만듭니다. 이 초기 작업은 새 구성이 동일한 보고서 세트를 계속 사용할 수 있도록 하기 때문에 중요합니다.
1. Dynamic Media 구성(Pre 6.3)을 구성하기 ***전에*** 새로운 ****** 작성자 노드에 비디오 Analytics 사전 설정 패키지를 설치합니다.
1. 패키지 설치를 확인하고 디버깅합니다.

### 첫 번째 작성자 노드를 구성한 후 비디오 Analytics 사전 설정 패키지 생성 {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

이 작업을 마치면 비디오 Analytics 사전 설정이 포함된 패키지 파일이 있게 됩니다. 이러한 사전 설정에는 보고서 세트, 추적 서버, 추적 네임스페이스 및 Marketing Cloud 조직 ID가 포함되어 있습니다(가능한 경우).

1. 아직 설정하지 않은 경우 Dynamic Media 구성(6.3 이전)을 구성하십시오.
1. (선택 사항) 보고서 세트 ID를 보고 복사합니다. JCR에 액세스할 수 있어야 합니다. 보고서 세트 ID가 필요하지 않지만 유효성 검사가 더 쉬워집니다.
1. 패키지 관리자를 사용하여 패키지를 만듭니다.
1. 필터를 포함하도록 패키지를 편집합니다.

   AEM에서: `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. 패키지를 빌드합니다.
1. 비디오 Analytics 사전 설정 패키지를 다운로드하거나 공유하여 이후 새로운 작성자 노드와 공유할 수 있습니다.

### 추가 작성자 노드를 구성하기 전에 비디오 Analytics 사전 설정 패키지 설치 {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

Dynamic Media 구성을 구성하기 ***전에*** 이 작업을 완료해야 합니다(6.3 이전). 이렇게 하지 않으면 다른 사용되지 않은 보고서 세트가 생성됩니다. 또한 비디오 보고가 계속 제대로 작동하지만 데이터 수집은 최적화되지 않습니다.

첫 번째 작성자 노드의 비디오 Analytics 사전 설정 패키지가 새 작성자 노드에서 액세스할 수 있는지 확인합니다.

1. 이전에 만든 비디오 Analytics 사전 설정 패키지를 패키지 관리자로 업로드합니다.
1. 비디오 Analytics 사전 설정 패키지를 설치합니다.
1. Dynamic Media 구성(6.3 이전).

### 패키지 설치 확인 및 디버깅 {#verifying-and-debugging-the-package-installation}

1. 다음 중 하나를 수행하여 확인하고 필요한 경우 패키지 설치를 디버깅합니다.

   * **JCR을 통해 비디오 Analytics 사전 설정을 확인합니다.** JCR을 통해 비디오 Analytics 사전 설정을 확인하려면 CRXDE Lite에 액세스할 수 있어야 합니다.

      AEM - CRXDE Lite에서 `/conf/global/settings/
dam/dm/presets/analytics/jcr:content/userdata`

      그건 `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

      작성자 노드에서 CRXDE Lite에 대한 액세스 권한이 없는 경우 게시 서버를 통해 사전 설정을 확인할 수 있습니다.

   * **이미지 서버를 통해 비디오 Analytics 사전 설정 확인**

      이미지 서버 req=userdata 요청을 만들어 비디오 Analytics 사전 설정의 유효성을 직접 확인할 수 있습니다.
예를 들어 작성자 노드에서 Analytics 사전 설정을 보려면 다음 요청을 할 수 있습니다.

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      게시 서버에서 사전 설정의 유효성을 검사하기 위해 게시 서버와 유사한 직접 요청할 수 있습니다. 응답은 작성자 및 게시 노드에서 동일합니다. 응답은 다음과 비슷합니다.**

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **AEM 도구 > 자산 > 비디오 보고**&#x200B;에서 비디오 보고 도구를 통해 비디오 Analytics 사전 **[!UICONTROL 설정을 확인합니다.]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      다음 오류 메시지가 표시되면 보고서 세트를 사용할 수 있지만 채울 수 없습니다. 이 오류는 시스템이 데이터를 수집하기 전에 새 설치에서 올바른 것입니다.
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   보고 데이터를 생성하려면 하나의 비디오를 업로드하고 게시하십시오. URL **[!UICONTROL 복사를]** 사용하고 비디오를 한 번 이상 실행합니다.

   비디오 뷰어 사용에서 보고 데이터를 채우려면 최대 12시간이 걸릴 수 있습니다.

   오류가 발생하여 보고서 세트가 올바로 설정되지 않으면 다음 경고가 표시됩니다.

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   이 오류는 Dynamic Media 구성(6.3 이전) 서비스를 구성하기 전에 비디오 보고를 실행하는 경우에도 표시됩니다.

### 비디오 보고 구성 문제 해결 {#troubleshooting-the-video-reporting-configuration}

* 설치하는 동안 Analytics API 서버에 연결하는 경우 시간이 초과되는 경우가 있습니다. 설치는 연결을 20번 재시도하지만 여전히 실패합니다. 이 경우 로그 파일에 여러 개의 오류가 기록됩니다. Search for `SiteCatalystReportService`.
* 먼저 Analytics 사전 설정 패키지를 설치하지 않으면 새 보고서 세트가 생성될 수 있습니다.
* AEM 6.3에서 AEM 6.4 또는 AEM 6.4.1로 업그레이드한 다음 Dynamic Media 구성(6.3 이전)을 구성해도 여전히 보고서 세트가 생성됩니다. 이 문제는 AEM 6.4.2에 대해 알려져 해결됩니다.

### 비디오 Analytics 사전 설정 정보 {#about-the-video-analytics-preset}

비디오 Analytics 사전 설정(때로 분석 사전 설정이라고도 함)은 Dynamic Media의 뷰어 사전 설정 옆에 저장됩니다. 이것은 기본적으로 뷰어 사전 설정과 동일하지만 AppMeasurement 및 비디오 하트비트 보고를 구성하는 데 사용되는 정보입니다.

사전 설정 속성은 다음과 같습니다.

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (이전 AEM 버전에 없음)

AEM 6.4 이상 버전은 이 사전 설정을 `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## 카탈로그 설정 복제 {#replicating-catalog-settings}

JCR을 통해 설정 프로세스의 일부로 고유한 기본 카탈로그 설정을 게시해야 합니다. 카탈로그 설정을 복제하려면

1. 터미널 창에서 다음을 실행합니다.

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. AEM에서 CRXDE Lite의 다음 위치로 이동합니다(관리자 권한 필요).

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. 복제 **[!UICONTROL 탭을]** 누릅니다.
1. 복제를 **[!UICONTROL 누릅니다]**.

## 뷰어 사전 설정 복제 {#replicating-viewer-presets}

뷰어 사전 설정 *으로 자산을 제공하려면 뷰어 사전 설정을 복제/게시해야* 합니다. 자산에 대한 URL 또는 포함 코드를 얻으려면 모든 뷰어 사전 설정 *을* 활성화하고 복제해야 합니다.
자세한 내용은 [Publishing Viewer](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) 사전 설정을 참조하십시오.

>[!NOTE]
기본적으로, 자산 세부 정보 보기에서 뷰어 **[!UICONTROL 를]** 선택하면 시스템은 표현물 **** 및 다양한 뷰어 사전 설정을선택할 때 다양한 표현물을 보여줍니다. 보이는 숫자를 늘리거나 줄일 수 있습니다. 표시되는 [이미지 사전](/help/assets/managing-image-presets.md#increasingthenumberofimagepresetsthatdisplay) 설정 수 증가 [또는 표시되는](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)뷰어 사전 설정 수 증가를 참조하십시오.

## 복제용 자산 필터링 {#filtering-assets-for-replication}

비Dynamic Media 배포에서는 AEM 작성 환경에서 *모든* 자산(이미지와 비디오 모두)을 AEM 게시 노드로 복제합니다. AEM 게시 서버도 자산을 제공하므로 이 워크플로우가 필요합니다.

하지만 Dynamic Media 배포에서는 자산이 클라우드를 통해 제공되므로 이러한 동일한 자산을 AEM 게시 노드에 복제할 필요가 없습니다. 이러한 &quot;하이브리드 퍼블리싱&quot; 워크플로우는 에셋을 복제하는 데 필요한 추가 스토리지 비용과 더 긴 처리 시간을 방지합니다. Dynamic Media 뷰어, 사이트 페이지 및 정적 컨텐츠와 같은 기타 컨텐츠는 AEM 게시 노드에서 계속 제공됩니다.

자산 복제 외에도 다음과 같은 비자산도 복제됩니다.

* Dynamic Media 배달 구성: `/conf/global/settings/dam/dm/imageserver/jcr:content`
* 이미지 사전 설정: `/conf/global/settings/dam/dm/presets/macros`
* 뷰어 사전 설정: `/conf/global/settings/dam/dm/presets/viewer`

필터는 AEM 게시 노드로 *자산이 복제되지* 않도록 하는 방법을 제공합니다.

### 복제에 기본 자산 필터 사용 {#using-default-asset-filters-for-replication}

프로덕션 **또는** (2) 이미징 및 비디오에서 (1) 이미징에 Dynamic Media을 사용하는 경우, Adobe가 제공하는 기본 필터를 그대로 사용할 수 있습니다. 다음 필터는 기본적으로 활성화됩니다.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>필터</strong></td>
   <td><strong>MIME 유형</strong></td>
   <td><strong>표현물</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media 이미지 배달</td>
   <td><p>필터 이미지</p> <p>필터 세트</p> <p> </p> </td>
   <td><p>이미지로 <strong>시작/</strong></p> <p>응용 프로그램/ <strong>응용 프로그램</strong> /를 포함하며 다음으로 <strong>끝납니다</strong>.</p> </td>
   <td>곧바로 사용할 수 있는 "필터 이미지"(대화형 이미지를 포함하여 단일 이미지 에셋에 적용) 및 "필터 세트"(스핀 세트, 이미지 세트, 혼합 미디어 집합 및 캐러셀 세트에 적용)는 다음과 같습니다.
    <ul>
     <li>복제용 PTIFF 이미지 및 메타데이터 포함(cqdam으로 시작하는 모든 변환 <strong></strong>).</li>
     <li>복제에서 원본 이미지 및 정적 이미지 표현물을 제외합니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media 비디오 전달</td>
   <td>필터 비디오</td>
   <td>비디오로 <strong>시작/</strong></td>
   <td>곧바로 사용할 수 있는 "필터 비디오"는 다음과 같습니다.
    <ul>
     <li>복제를 위한 프록시 비디오 변환, 비디오 축소판/포스터 이미지, 메타데이터(부모 비디오 및 비디오 표현물 모두에서) 포함(cqdam으로 시작하는 모든 변환 <strong></strong>)</li>
     <li>원본 비디오 및 정적 축소판 변환의 복제에서 제외합니다.<br /> <br /> <strong>참고:</strong> 프록시 비디오 변환에는 바이너리가 포함되지 않고 노드 속성만 포함됩니다. 따라서 게시자 저장소 크기에는 영향을 주지 않습니다.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Classic(Scene7) 통합</td>
   <td><p>필터 이미지</p> <p>필터 세트</p> <p>필터 비디오</p> </td>
   <td><p>이미지로 <strong>시작/</strong></p> <p>응용 프로그램/ <strong>응용 프로그램</strong> /를 포함하며 다음으로 <strong>끝납니다</strong>.</p> <p>비디오로 <strong>시작/</strong></p> </td>
   <td><p>Adobe Dynamic Media 클라우드 복제 서비스 URL 대신 AEM 게시 서버를 가리키도록 전송 URI를 구성합니다. 이 필터를 설정하면 Dynamic Media Classic에서 AEM 게시 인스턴스 대신 자산을 전달할 수 있습니다.</p> <p>곧바로 사용할 수 있는 "필터 이미지", "필터 세트" 및 "필터 비디오"는 다음과 같습니다.</p>
    <ul>
     <li>복제용 PTIFF 이미지, 프록시 비디오 변환 및 메타데이터를 포함할 수 있습니다. 하지만 AEM을 실행하는 사용자의 JCR에 존재하지 않으므로 Dynamic Media Classic 통합이 실제로 아무런 작업을 하지 않습니다.</li>
     <li>원본 이미지, 정적 이미지 변환, 원본 비디오 및 정적 축소판 변환에서 제외합니다. 대신, Dynamic Media Classic은 이미지 및 비디오 에셋을 제공합니다.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
필터는 MIME 유형에 적용되며 경로 특수일 수 없습니다.

### 비디오 전용 배포에 대한 자산 필터 설정 {#setting-up-asset-filters-for-video-only-deployments}

비디오 전용 Dynamic Media을 사용하는 경우 다음 단계에 따라 복제를 위한 자산 필터를 설정합니다.

1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스하고 **[!UICONTROL 도구 > 배포 > 복제 > 작성자의 에이전트를 누릅니다]**.
1. 작성자 페이지의 에이전트 **[!UICONTROL 에서 기본 에이전트(게시)를 누릅니다]**.
1. 편집을 **[!UICONTROL 누릅니다]**.
1. [ **[!UICONTROL 에이전트 설정]** ] 대화 상자의 [ **[!UICONTROL 설정]** ] 탭에서 **[!UICONTROL [사용]** ]을 선택하여에이전트를 켜십시오.
1. 확인을 **[!UICONTROL 누릅니다]**.
1. AEM에서 **[!UICONTROL 도구 > 일반 > CRXDE Lite를 누릅니다]**.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. 필터 **[!UICONTROL 비디오를]**&#x200B;찾아 마우스 오른쪽 버튼으로 클릭한 다음 **[!UICONTROL 복사를 선택합니다]**.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/publish`
1. jcr: **[!UICONTROL content]**&#x200B;를 찾아 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 붙여넣기를 선택합니다]**.

비디오 자체는 Dynamic Media 클라우드 서비스에서 전달하는 동안 비디오 포스터 이미지 및 재생에 필요한 비디오 메타데이터를 제공하는 AEM 게시 인스턴스를 설정합니다. 또한 이 필터는 원본 비디오와 정적 축소판 표현물 복제에서 제외되며, 게시 인스턴스에는 필요하지 않습니다.

### 비프로덕션 배포에서 이미징을 위한 자산 필터 설정 {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

비프로덕션 배포의 이미징에 Dynamic Media을 사용하는 경우 다음 단계에 따라 복제를 위한 자산 필터를 설정합니다.

1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스하고 **[!UICONTROL 도구 > 배포 > 복제 > 작성자의 에이전트를 누릅니다]**.
1. 작성자 페이지의 에이전트 **[!UICONTROL 에서 기본 에이전트(게시)를 누릅니다]**.
1. 편집을 **[!UICONTROL 누릅니다]**.
1. [ **[!UICONTROL 에이전트 설정]** ] 대화 상자의 [ **[!UICONTROL 설정]** ] 탭에서 **[!UICONTROL [사용]** ]을 선택하여에이전트를 켜십시오.
1. 확인을 **[!UICONTROL 누릅니다]**.
1. AEM에서 **[!UICONTROL 도구 > 일반 > CRXDE Lite를 누릅니다]**.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. 필터 **[!UICONTROL 이미지를]**&#x200B;찾아 마우스 오른쪽 버튼으로 클릭한 다음 **[!UICONTROL 복사를 선택합니다]**.
1. 왼쪽 폴더 트리에서 `/etc/replication/agents.author/publish`
1. jcr: **[!UICONTROL content]**&#x200B;를 찾아 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 만들기 > 노드 만들기를 선택합니다]**. 유형 `damRenditionFilters` 의 이름을 입력합니다 `nt:unstructured`.
1. 위치를 `damRenditionFilters`찾아 마우스 오른쪽 단추로 클릭하고 **[!UICONTROL 붙여넣기를 선택합니다]**.

비프로덕션 환경에 이미지를 전달하는 AEM 게시 인스턴스를 설정합니다. 또한 이 필터는 원본 이미지 및 정적 표현물 복제에서 제외되며, 게시 인스턴스에는 필요하지 않습니다.

>[!NOTE]
작성자에 서로 다른 필터가 많이 있는 경우 각 에이전트에는 다른 사용자가 할당됩니다. [MOCK] The granite code enforcing one-filter-per-user model. 각 필터에 대해 항상 다른 사용자가 설정되어 있어야 합니다.
서버에 둘 이상의 필터를 사용하는 경우(예: 게시할 복제 필터 하나, s7delivery에 대한 두 번째 필터) 이 두 필터가 **jcr:content** 노드에서 다른 userId **** 를 할당했는지 확인해야 합니다. 다음과 같은 이미지를 참조하십시오.

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### 복제용 자산 필터 사용자 정의 {#customizing-asset-filters-for-replication}

선택적으로 복제용 자산 필터를 사용자 정의하려면

1. AEM에서 AEM 로고를 눌러 글로벌 탐색 콘솔에 액세스하고 도구 > **[!UICONTROL 일반 > CRXDE Lite를 누릅니다]**.
1. 왼쪽 폴더 트리에서 필터 `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` 로 이동합니다.

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. 필터에 대한 MIME 유형을 정의하려면 다음과 같이 MIME 형식을 찾을 수 있습니다.

   왼쪽 레일에서 확장한 다음 표 `content > dam > <locate_your_asset> >  jcr:content > metadata` 에서 **[!UICONTROL dc:format을 찾습니다]**.

   다음 그래픽은 자산의 dc:format 경로의 예입니다.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   에셋 `dc:format` 에 대한 내용 `Fiji Red.jpg` 이 표시됩니다 `image/jpeg`.

   형식에 상관없이 이 필터가 모든 이미지에 적용되도록 하려면 모든 형식의 모든 이미지에 적용되는 정규 표현식 `image/*` `*` 의 위치에 값을 설정합니다.

   필터가 JPEG 유형의 이미지에만 적용되도록 하려면 값을 입력합니다 `image/jpeg`.

1. 복제에서 포함하거나 제외할 변환을 정의합니다.

   복제를 위해 필터링하는 데 사용할 수 있는 문자는 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <td><strong>사용할 문자</strong></td>
   <td><strong>복제용 에셋을 필터링하는 방법</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>와일드카드 문자<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>복제용 에셋을 포함합니다.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>복제에서 자산을 제외합니다.</td>
  </tr>
 </tbody>
</table>

다음으로 이동 `content/dam/<locate your asset>/jcr:content/renditions`.

다음 그래픽은 자산의 표현물의 예입니다.

![chlimage_1-513](assets/chlimage_1-4.png)

위의 예를 사용하여 PTIFF(Pyramid TIFF)만 복제하려는 경우 다음으로 시작하는 모든 표현물을 포함하는 `+cqdam,*` 곳에 입력합니다 `cqdam`. 이 예에서, 이 변환은 입니다 `cqdam.pyramid.tiff`.

원본을 복제하려는 경우 해당 위치에 `+original`들어갑니다.

## Dynamic Media 이미지 서버 설정 구성 {#configuring-dynamic-media-image-server-settings}

Dynamic Media 이미지 서버 구성에는 Adobe CQ Scene7 ImageServer 번들 및 Adobe CQ Scene7 PlatformServer 번들 편집이 포함됩니다.

>[!NOTE]
Dynamic Media은 활성화한 [후 즉시 작동합니다](#enabling-dynamic-media). 그러나 특정 사양 또는 요구 사항을 충족하도록 Dynamic Media 이미지 서버를 구성하여 설치를 세밀하게 조정할 수도 있습니다.

**필수 조건**: *Dynamic Media 이미지 서버를 구성하기 전에* Windows VM에 Microsoft Visual C++ 라이브러리 설치가 포함되어 있는지 확인하십시오. Dynamic Media 이미지 서버를 실행하려면 라이브러리가 필요합니다. 여기에서 Microsoft Visual C++ 2010 재배포 가능 패키지(x64)를 [다운로드할 수 있습니다](https://www.microsoft.com/en-us/download/details.aspx?id=14632).

Dynamic Media 이미지 서버 설정을 구성하려면:

1. AEM의 왼쪽 위 모서리에서 **[!UICONTROL Adobe Experience Manager]** 를 탭하여 글로벌 탐색 콘솔에 액세스한 다음 **[!UICONTROL 도구 > 작업 > 웹 콘솔을 탭합니다]**.
1. Adobe Experience Manager 웹 콘솔 구성 페이지에서 **[!UICONTROL OSGi > 구성을]** 탭하여 현재 AEM 내에서 실행 중인 모든 번들을 나열합니다.

   Dynamic Media 배달 서버는 목록의 다음 이름 아래에 있습니다.

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. 번들 목록에서 Adobe CQ Scene7 ImageServer 오른쪽의 편집 아이콘을 누릅니다.
1. Adobe CQ Scene7 ImageServer 대화 상자에서 다음 구성 값을 설정합니다.

   >[!NOTE]
   대부분의 경우 기본값을 변경할 필요가 없습니다. 하지만 기본값을 변경하는 경우 변경 사항이 적용되려면 번들을 다시 시작해야 합니다.

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>기본값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>TcpPort.name</td>
   <td><code><em>empty</em></code></td>
   <td>ImageServer 프로세스와의 통신에 사용할 포트 번호입니다. 기본적으로 무료 포트가 자동으로 검색됩니다.</td>
  </tr>
  <tr>
   <td>AllowRemoteAccess.name</td>
   <td><code><em>empty</em></code></td>
   <td><p>ImageServer 프로세스에 대한 원격 액세스를 허용하거나 허용하지 않습니다. false인 경우 이미지 서버는 localhost에서만 수신합니다.</p> <p>localhost를 가리키는 기본 외부화 설정은 특정 VM 인스턴스의 실제 도메인 또는 IP 주소를 지정해야 합니다. 로컬 호스트가 VM의 상위 시스템을 가리키기 때문입니다.</p> <p>VM에 대한 도메인 또는 IP 주소는 자체적으로 해결할 수 있도록 호스트 파일 항목이 있어야 할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td>MaxRenderRgnPixels</td>
   <td>16픽셀</td>
   <td>렌더링되는 최대 크기(메가픽셀)</td>
  </tr>
  <tr>
   <td>MaxMessageSize</td>
   <td>16MB바이트</td>
   <td>배달되는 최대 메시지 크기(MB)입니다.</td>
  </tr>
  <tr>
   <td>RandomAccessUrlTimeout</td>
   <td>20</td>
   <td>ImageServer가 JCR이 범위 타일 요청에 응답할 때까지 대기하는 시간(초)에 대한 시간 초과 값입니다.</td>
  </tr>
  <tr>
   <td>WorkerThreads</td>
   <td>10</td>
   <td>작업자 스레드 수입니다.</td>
  </tr>
 </tbody>
</table>

1. 저장을 **[!UICONTROL 누릅니다]**.
1. Adobe CQ Scene7 PlatformServer의 오른쪽에 있는 번들 목록에서 **[!UICONTROL 편집]** 아이콘을 누릅니다.
1. Adobe CQ Scene7 PlatformServer 대화 상자에서 다음 기본 값 옵션을 설정합니다.

   >[!NOTE]
   Dynamic Media 이미지 서버는 자체 디스크 캐시를 사용하여 응답을 캐시합니다. AEM HTTP 캐시 및 표시는 Dynamic Media 이미지 서버의 응답을 캐시하는 데 사용할 수 없습니다.

   | **속성** | **기본값** | **설명** |
   |---|---|---|
   | 캐시 사용 | 선택됨 | 응답 캐시가 활성화되어 있는지 여부. |
   | 캐시 루트 | 캐시 | 응답 캐시 폴더에 대한 하나 이상의 경로. 상대 경로는 내부 s7imaging bundle 폴더에 대해 해결됩니다. |
   | 캐시 최대 크기 | 200000000 | 응답 캐시의 최대 크기(바이트)입니다. |
   | 최대 항목 캐시 | 100000 | 캐시에 허용되는 최대 항목 수입니다. |

### 기본 매니페스트 설정 {#default-manifest-settings}

기본 매니페스트를 사용하면 Dynamic Media 배달 응답을 생성하는 데 사용되는 기본값을 구성할 수 있습니다. 품질(JPEG 품질, 해상도, 리샘플링 모드), 캐싱(만료) 및 너무 큰 이미지(defaultpix, defaultththumpix, maxpix)의 렌더링을 방지할 수 있습니다.

기본 매니페스트 구성 위치는 **[!UICONTROL Adobe CQ Scene7 PlatformServer 번들의]** 카탈로그 루트 **[!UICONTROL 기본값]** 에서 가져옵니다. 기본적으로 이 값은 [ **[!UICONTROL 도구] > [일반] > [CRXDE Lite] 내의 다음 경로에 있습니다]**.

`/conf/global/settings/dam/dm/imageserver/`

![confiagimageservercrxdelite](assets/configimageservercrxdelite.png)

아래 표에 설명된 대로 새 값을 입력하여 속성 값을 변경할 수 있습니다.

기본 매니페스트의 변경 작업이 끝나면 페이지의 왼쪽 위 모서리에서 모두 **[!UICONTROL 저장을 탭합니다]**.

속성 탭 오른쪽에 있는 **[!UICONTROL 액세스 제어]** 탭을 누른 다음 모든 사용자 및 동적 미디어 복제 사용자에 대해 액세스 제어 권한을 `jcr:read` 설정합니다.

![confiagimageservercrxdeliteaccescontroltab](assets/configimageservercrxdeliteaccesscontroltab.png)

매니페스트 설정 및 그 기본값 표:

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>기본값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>bgcolor</td>
   <td>FFFFFF</td>
   <td><p>기본 배경색입니다. 실제 이미지 데이터를 포함하지 않는 회신 이미지의 모든 영역을 채우는 데 사용되는 RGB 값입니다.</p> <p>Image <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_bkgcolor.html">Serving API의 BkgColor</a> 를 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>defaultpix</td>
   <td>300,300</td>
   <td><p>기본 보기 크기입니다. 요청이 wid=, hei= 또는 scl=를 사용하여 보기 크기를 명시적으로 지정하지 않을 경우 서버는 응답 이미지를 이 너비와 높이보다 크지 않게 제한합니다.</p> <p>0보다 큰 2개의 정수로 지정하여 쉼표로 구분합니다. 너비 및 높이(픽셀 단위) 두 값 중 하나 또는 둘 다 0으로 설정하여 제약이 없도록 할 수 있습니다. 중첩/포함된 요청에 적용되지 않습니다.</p> <p>이미지 제공 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_defaultpix.html">API에서</a> DefaultPix를 참조하십시오.</p> <p>그러나 일반적으로 뷰어 사전 설정 또는 이미지 사전 설정을 사용하여 자산을 제공하고 있습니다. Defaultpix는 뷰어 사전 설정 또는 이미지 사전 설정을 사용하지 않는 자산에만 적용됩니다.</p> </td>
  </tr>
  <tr>
   <td>defaulthumpix</td>
   <td>100,100</td>
   <td><p>기본 축소판 크기 축소판 요청에 대해 attribute::DefaultPix 대신 사용됩니다(req=tmb).</p> <p>서버는 축소판 요청(req=tmb)이 wid=, hei= 또는 scl=을 사용하여 명시적으로 보기 크기를 지정하지 않는 경우 응답 이미지를 이 너비와 높이보다 크지 않게 제한합니다.</p> <p>0보다 큰 2개의 정수로 지정하여 쉼표로 구분합니다. 너비 및 높이(픽셀 단위) 두 값 중 하나 또는 둘 다 0으로 설정하여 제약이 없도록 할 수 있습니다. </p> <p>중첩/포함된 요청에 적용되지 않습니다.</p> <p>이미지 제공 API에서 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_defaultthumbpix.html">DefaultThumbPix</a> 를 참조하십시오. </p> </td>
  </tr>
  <tr>
   <td>만료</td>
   <td>36000000</td>
   <td><p>기본 클라이언트 캐시 시간을 라이브로 설정합니다. 특정 카탈로그 레코드에 유효한 카탈로그::Expiration 값이 없는 경우 기본 만료 간격을 제공합니다.</p> <p>실수, 0 이상 회신 데이터가 생성된 이후 만료까지 남은 시간(밀리초)입니다. 응답 이미지를 항상 즉시 만료되도록 0으로 설정하면 클라이언트 캐시를 효과적으로 사용할 수 없습니다. 기본적으로 이 값은 10시간으로 설정되며, 즉 새 이미지가 게시된 경우 이전 이미지가 사용자의 캐시를 나가는 데 10시간이 걸립니다. 캐시를 더 빨리 지워야 한다면 고객 지원 센터에 문의하십시오.</p> <p>이미지 제공 API에서 <a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_expiration.html">만료도</a> 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>jpegquality</td>
   <td>80</td>
   <td><p>기본 JPEG 인코딩 속성입니다. JPEG 회신 이미지의 기본 속성을 지정합니다.</p> <p>정수 번호와 플래그는 쉼표로 구분됩니다. 첫 번째 값은 1.100 범위에 있고 품질을 정의합니다. 두 번째 값은 일반 동작의 경우 0이거나, JPEG 인코더에 사용되는 RGB 색도 다운샘플링을 비활성화하려면 1일 수 있습니다.</p> <p>이미지 제공 API에서 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_jpegquality.html">JpegQuality</a> 를 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>maxpix</td>
   <td>2000,2000</td>
   <td><p>회신 이미지 크기 제한. 클라이언트에 반환되는 최대 응답 이미지 폭과 높이입니다.</p> <p>요청 시 너비 또는 높이가 특성::MaxPix보다 큰 응답 이미지가 요청되면 서버가 오류를 반환합니다.</p> <p>이미지 제공 API에서 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_maxpix.html">MaxPix</a> 를 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>resmode</td>
   <td>SHARP2</td>
   <td><p>기본 리샘플링 모드. 이미지 데이터의 크기 조정에 사용할 기본 리샘플링 및 보간 속성을 지정합니다.</p> <p>resMode=가 요청에 지정되지 않은 경우에 사용됩니다.</p> <p>허용되는 값에는 BILIN, BICUB 또는 SHARP2가 포함됩니다.</p> <p>열거형. 빌린의 경우 2로, 바이큐의 경우 3으로, 샤프2 보간 모드의 경우 4로 설정합니다. sharp2를 사용하면 최상의 결과를 얻을 수 있습니다.</p> <p>이미지 제공 API에서 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_is_cat_resmode.html">ResMode</a> 를 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>해상도</td>
   <td>72</td>
   <td><p>기본 개체 해상도입니다. 특정 카탈로그 레코드에 유효한 카탈로그::Resolution 값이 포함되어 있지 않을 경우 기본 개체 해상도를 제공합니다.</p> <p>0보다 큰 실수 일반적으로 인치당 픽셀로 표현되지만 미터당 픽셀과 같은 다른 단위로 표현될 수도 있습니다.</p> <p>이미지 제공 API의 <a href="https://microsite.omniture.com/t2/help/en_US/s7/is_ir_api/is_api/image_catalog/r_resolution.html">해상도도</a> 참조하십시오.</p> </td>
  </tr>
  <tr>
   <td>thumbnailatime</td>
   <td>1%,11%,21%,31%,41%,51%,61%,71%,81%,91%</td>
   <td>이러한 값은 비디오 재생 시간의 스냅샷을 나타내며 <a href="https://encoding.com/">encoding.com으로 전달됩니다</a>. 자세한 <a href="/help/assets/video.md#aboutvideothumbnails">내용은 비디오 축소판</a> 정보를 참조하십시오.</td>
  </tr>
 </tbody>
</table>

## Dynamic Media 색상 관리 구성 {#configuring-dynamic-media-color-management}

다이내믹 미디어 색상 관리를 사용하면 미리 보기 위해 올바른 에셋에 색상을 적용할 수 있습니다.

색상 교정을 통해 인제스트된 에셋은 생성된 피라미드 TIFF 변환에 색상 공간(RGB, CMYK, 회색)과 임베드된 색상 프로파일을 유지합니다. 동적 변환을 요청하면 이미지 색상이 대상 색상 공간으로 교정됩니다. JCR의 다이내믹 미디어 게시 설정에서 출력 색상 프로파일을 구성합니다.

Adobe 색상 관리는 ICC(International Color Consortium)에서 정의한 포맷인 ICC 프로필을 사용합니다.

CMYK, RGB 또는 회색 출력을 사용하여 다이내믹 미디어 색상 관리를 구성하고 이미지 사전 설정을 구성할 수 있습니다. See [Configuring Image Presets](/help/assets/managing-image-presets.md).

고급 사용 사례에서는 수동 구성 `icc=` 수정자를 사용하여 출력 색상 프로파일을 명시적으로 선택할 수 있습니다.

* `icc` - [https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/r_icc.html](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/r_icc.html)

* `iccEmbed` - [https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/r_iccembed.html](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/http_ref/r_iccembed.html)

>[!NOTE]
Adobe 표준 색상 프로파일은 소프트웨어 배포의 패키지 공유 [또는](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) 기능 팩 12445의 기능 팩 1245 [가 설치되어 있는 경우에만 사용할 수](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) 있습니다. 모든 기능 팩과 서비스 팩은 [패키지 공유](https://www.adobeaemcloud.com/content/packageshare.html) 및 [소프트웨어 배포를 통해 사용할 수 있습니다](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). Feature Pack 12445는 Adobe 색상 프로필을 제공합니다.

### Feature Pack 12445 설치 {#installing-feature-pack}

다이내믹 미디어 색상 관리 기능을 사용하려면 기능 팩 12445를 설치해야 합니다.

**기능 팩 12445를 설치하려면**

1. 패키지 공유 [또는 소프트웨어 배포](https://www.adobeaemcloud.com/content/packageshare.html) 로 [이동하여](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 다운로드하십시오 `cq-6.3.0-featurepack-12445`.

   AEM [에서 패키지 공유 및 패키지 사용에 대한 자세한 내용은 패키지](/help/sites-administering/package-manager.md) 사용 방법을 참조하십시오.

1. 기능 팩을 설치합니다.

### 기본 색상 프로파일 구성 {#configuring-the-default-color-profiles}

Feature Pack을 설치한 후 RGB 또는 CMYK 이미지 데이터를 요청할 때 색상 교정을 사용하도록 적절한 기본 색상 프로파일을 구성해야 합니다.

**기본 색상 프로파일을 구성하려면**

1. [ **[!UICONTROL 도구] > [일반] > [CRXDE]** Lite]에서 기본 Adobe 색상 프로필이 `/conf/global/settings/dam/dm/imageserver/jcr:content` 포함된 위치로 이동합니다.

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. 다음 표에 설명된 속성 탭 아래쪽으로 스크롤하고 **[!UICONTROL 속성]** 이름, 유형 및 값을 직접 입력하여 색상 교정 속성을 추가합니다. 값을 입력한 후 **[!UICONTROL 추가를]** 누른 다음 **[!UICONTROL 모두]** 저장을 눌러 값을 저장합니다.

   색상 교정 속성은 색상 교정 **속성 표에 설명되어** 있습니다. 색상 교정 속성에 지정할 수 있는 값은 **색상 프로파일** 표에 있습니다.

   예를 들어 **[!UICONTROL 이름]**&#x200B;에서 `iccprofilecmyk`추가 **[!UICONTROL 를]** 선택한 `String`다음 `WebCoated` a **[!UICONTROL Value]**&#x200B;를으로 추가합니다. 그런 다음 **[!UICONTROL 추가를]** 누른 다음 **[!UICONTROL 모두를]** 저장하여 값을 저장합니다.

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **색상 교정 속성 표**

<table>
 <tbody>
  <tr>
   <td><strong>속성</strong></td>
   <td><strong>유형</strong></td>
   <td><strong>기본값</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td><a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_iccprofilergb.html">iccprofilergb</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>기본 RGB 색상 프로파일의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_iccprofilecmyk.html">iccprofilecmyk</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>기본 CMYK 색상 프로파일의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_iccprofilegray.html">iccprofilegray</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>기본 회색 색상 프로파일의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_iccprofilesrcrgb.html">iccprofilesrcrgb</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>포함된 색상 프로필이 없는 RGB 이미지에 사용되는 기본 RGB 색상 프로필의 이름</td>
  </tr>
  <tr>
   <td><a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_iccprofilesrccmyk.html">iccprofilesrccmyk</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>포함된 색상 프로필이 없는 CMYK 이미지에 사용되는 기본 CMYK 색상 프로필의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_iccprofilesrcgray.html">iccprofilesrcgray</a></td>
   <td>문자열</td>
   <td>&lt;비어 있음&gt;</td>
   <td>포함된 색상 프로필이 없는 CMYK 이미지에 사용되는 기본 회색 색상 프로필의 이름입니다.</td>
  </tr>
  <tr>
   <td><a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_iccblackpointcompensation.html">icblackpointcompensation</a></td>
   <td>부울</td>
   <td>True</td>
   <td>색상 교정 중에 검은 점 보상을 수행할지 여부를 지정합니다. Adobe에서는 이 설정을 사용하는 것이 좋습니다.</td>
  </tr>
  <tr>
   <td><a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_iccdither.html">시디더</a></td>
   <td>부울</td>
   <td>False</td>
   <td>색상 교정 중에 디더링을 수행할지 여부를 지정합니다.</td>
  </tr>
  <tr>
   <td><a href="https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/r_iccrenderintent.html">icenderintent</a></td>
   <td>문자열</td>
   <td>상대적</td>
   <td><p>렌더링 의도를 지정합니다. 허용되는 값은 다음과 같습니다. <strong>지각, 상대, 채도, 절대. </strong><i></i>Adobe에서는 <strong>상대 </strong><i></i>를 기본값으로 권장합니다.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
속성 이름은 대/소문자를 구분하며 모두 소문자여야 합니다.

**색상 프로파일 표**

다음 색상 프로필이 설치되어 있습니다.

<table>
 <tbody>
  <tr>
   <th><p>이름</p> </th>
   <th><p>색상 공간</p> </th>
   <th><p>설명</p> </th>
  </tr>
  <tr>
   <td>AdobeRGB</td>
   <td>RGB</td>
   <td>Adobe RGB(1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
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
   <td>Coated FOGRA27(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>Coated FOGRA39(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>코팅 GRACoL 2006(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>ColorMatch RGB</td>
  </tr>
  <tr>
   <td>유럽 ISOCoated</td>
   <td>CMYK</td>
   <td>유럽 ISO 코팅 FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Euroscale Coated v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncoated</td>
   <td>CMYK</td>
   <td>Euroscale Uncoated v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>일본 컬러 2001 코팅</td>
  </tr>
  <tr>
   <td>JapanColorNewspaper</td>
   <td>CMYK</td>
   <td>일본 컬러 2002 신문</td>
  </tr>
  <tr>
   <td>JapanColorUncoated</td>
   <td>CMYK</td>
   <td>Japan Color 2001 Uncoated</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>일본 웹 코팅(광고)</td>
  </tr>
  <tr>
   <td>NewsprintSNAP2007</td>
   <td>CMYK</td>
   <td>미국 신문(SNAP 2007)</td>
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
   <td>SheetfedCoated</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Coated v2</td>
  </tr>
  <tr>
   <td>SheetfedUncoated</td>
   <td>CMYK</td>
   <td>US Sheetfed Uncoated v2</td>
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
   <td>Uncoated FOGRA29(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoated</td>
   <td>CMYK</td>
   <td>미국 웹 코팅(SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>Web Coated FOGRA28(ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Web Coated SWOP 2006년 3학년 용지</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Web Coated SWOP 2006년 5급 용지</td>
  </tr>
  <tr>
   <td>WebUncoated</td>
   <td>CMYK</td>
   <td>U.S. Web Uncoated v2</td>
  </tr>
  <tr>
   <td>광범위RGB</td>
   <td>RGB</td>
   <td>넓은 색상 영역 RGB</td>
  </tr>
 </tbody>
</table>

1. 모두 **[!UICONTROL 저장을 누릅니다]**.

예를 들어 iccprofilergb를 **[!UICONTROL 로]** 설정하고 `sRGB`iccprofilecmyk **[!UICONTROL 를]** WebCoated로 설정할 수 **[!UICONTROL 있습니다]**.

이렇게 하면 다음이 수행됩니다.

* RGB 및 CMYK 이미지의 색상 교정을 활성화합니다.
* 색상 프로필이 없는 RGB 이미지는 *sRGB* 색상 공간에 있는 것으로 간주됩니다.
* 색상 프로필이 없는 CMYK 이미지는 *WebCoated* 색상 공간에 있다고 가정합니다.
* RGB 출력을 반환하는 동적 변환은 *sRGB *색상 공간에 반환됩니다.
* CMYK 출력을 반환하는 동적 변환은 *WebCoated* 색상 공간에 반환됩니다.

## 자산 제공 {#delivering-assets}

위의 모든 작업을 완료하면 활성화된 Dynamic Media 에셋이 이미지 또는 비디오 서비스에서 제공됩니다. AEM에서 이 기능은 이미지 **[!UICONTROL 복사 URL]**, 뷰어 URL **[!UICONTROL 복사]**, 뷰어 코드 **[!UICONTROL 포함]**&#x200B;및 WCM에표시됩니다.

See [Delivering Dynamic Media Assets](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>네가..</strong></td>
   <td><strong>결과</strong></td>
  </tr>
  <tr>
   <td>이미지 URL 복사</td>
   <td><p>[URL 복사] 대화 상자에는 다음과 유사한 URL이 표시됩니다(URL은 데모용으로만 사용됩니다).</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>이미지 서비스 URL을 참조하는 <code>IMAGESERVICEPUBLISHNODE</code> 위치.</p> <p>Dynamic Media 자산 <a href="/help/assets/delivering-dynamic-media-assets.md">전달을 참조하십시오</a>.</p> </td>
  </tr>
  <tr>
   <td>뷰어 URL 복사</td>
   <td><p>[URL 복사] 대화 상자에는 다음과 유사한 URL이 표시됩니다(URL은 데모용으로만 사용됩니다).</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>여기서 <code>PUBLISHNODE</code> 는 일반적인 AEM 게시 노드를 참조하며 이미지 서비스 URL을 <code>IMAGESERVICEPUBLISHNODE</code> 참조합니다.</p> <p>Dynamic Media 자산 <a href="/help/assets/delivering-dynamic-media-assets.md">전달을 참조하십시오</a>.</p> </td>
  </tr>
  <tr>
   <td>뷰어의 포함 코드 복사</td>
   <td><p>포함 코드 복사 대화 상자에는 다음과 유사한 코드 조각이 표시됩니다(코드 샘플은 데모용으로만 사용).</p> <p><code class="code">&lt;style type="text/css"&gt;
       #s7basiczoom_div.s7basiczoomviewer{
       width:100%;
       height:auto;
       }
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer({
       "containerId" : "s7basiczoom_div",
       "params" : {
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" }
       }).init();
       &lt;/script&gt;</code></p> <p>여기서 <code>PUBLISHNODE</code> 는 일반적인 AEM 게시 노드를 참조하며 이미지 서비스 URL을 <code>IMAGESERVICEPUBLISHNODE</code> 참조합니다.</p> <p>Dynamic Media 자산 <a href="/help/assets/delivering-dynamic-media-assets.md">전달을 참조하십시오</a>.</p> </td>
  </tr>
 </tbody>
</table>

### WCM Dynamic Media 및 인터랙티브 미디어 구성 요소 {#wcm-dynamic-media-and-interactive-media-components}

Dynamic Media 및 대화형 미디어 구성 요소를 참조하는 WCM 페이지는 배달 서비스를 참조합니다.
