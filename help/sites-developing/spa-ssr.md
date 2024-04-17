---
title: SPA 및 서버측 렌더링
description: Adobe Experience Manager의 SPA 및 서버측 렌더링에 대해 알아봅니다.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: a80bc883-e0f6-4714-bd28-108262f96d77
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 1%

---

# SPA 및 서버측 렌더링{#spa-and-server-side-rendering}

>[!NOTE]
>
>SPA 편집기는 SPA 프레임워크 기반의 클라이언트측 렌더링(예: React 또는 Angular)이 필요한 프로젝트에 권장되는 솔루션입니다.

>[!NOTE]
>
>이 문서에 설명된 대로 SPA 서버측 렌더링 기능을 사용하려면 AEM(Adobe Experience Manager) 6.5.1.0 이상이 필요합니다.

## 개요 {#overview}

단일 페이지 애플리케이션(SPA)은 종종 기본 애플리케이션처럼 익숙한 방식으로 반응하고 작동하는 풍부하고 동적인 경험을 사용자에게 제공할 수 있습니다. [이는 클라이언트에 의존하여 콘텐츠를 맨 앞에 로드한 다음 사용자 상호 작용을 처리하는 대규모 작업을 수행함으로써 수행됩니다](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 따라서 클라이언트와 서버 사이에 필요한 통신량을 최소화하여 앱의 반응성을 높입니다.

그러나 SPA의 크기가 크고 컨텐츠가 풍부한 경우 특히 초기 로드 시간이 길어질 수 있습니다. 로드 시간을 최적화하기 위해 일부 콘텐츠를 서버측에서 렌더링할 수 있습니다. SSR(서버측 렌더링)을 사용하면 페이지의 초기 로드를 가속화한 다음 추가적인 렌더링을 클라이언트에 전달할 수 있습니다.

## SSR 사용 시기 {#when-to-use-ssr}

SSR이 모든 프로젝트에서 필수는 아닙니다. AEM은 SPAAdobe 용 JS SSR을 완전히 지원하지만 모든 프로젝트에 대해 체계적으로 구현하는 것은 권장되지 않습니다.

SSR을 구현하기로 결정할 때는 먼저 장기 유지 관리를 포함하여 SSR을 추가하는 것이 프로젝트에 현실적으로 나타내는 추가적인 복잡성, 노력 및 비용을 추정해야 합니다. SSR 아키텍처는 부가 가치가 예상 비용을 확실히 초과하는 경우에만 선택해야 합니다.

SSR은 일반적으로 다음 질문 중 하나에 명확한 &quot;예&quot;가 있을 때 일부 값을 제공합니다.

* **SEO:** 트래픽을 가져오는 검색 엔진에 의해 사이트가 제대로 인덱싱되려면 여전히 SSR이 필요합니까? 이제 기본 검색 엔진 크롤러가 JS를 평가한다는 점을 기억하십시오.
* **페이지 속도:** SSR이 실제 환경에서 측정 가능한 속도 개선을 제공하고 전반적인 사용자 경험을 추가합니까?

프로젝트에 대해 이 두 가지 질문 중 하나 이상이 명확한 &quot;예&quot;로 답변되는 경우에만 SSR을 구현하는 것이 Adobe에 좋습니다. 다음 섹션에서는 Adobe I/O Runtime을 사용하여 이 작업을 수행하는 방법에 대해 설명합니다.

## Adobe I/O Runtime {#adobe-i-o-runtime}

다음을 수행하는 경우 [프로젝트에 SSR 구현이 필요하다고 확신함](/help/sites-developing/spa-ssr.md#when-to-use-ssr), Adobe의 권장 솔루션은 Adobe I/O Runtime을 사용하는 것입니다.

Adobe I/O Runtime에 대한 자세한 내용은 다음을 참조하십시오.

* [https://developer.adobe.com/runtime/](https://developer.adobe.com/runtime/) - 서비스 개요
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs/) - 플랫폼에 대한 자세한 설명서

다음 섹션에서는 Adobe I/O Runtime을 사용하여 두 가지 다른 모델에서 SPA용 SSR을 구현하는 방법에 대해 자세히 설명합니다.

* [AEM 기반 통신 흐름](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime 기반 통신 흐름](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe은 환경(단계, 프로덕션, 테스트 등)별로 별도의 Adobe I/O Runtime 작업공간을 권장합니다. 이를 통해 서로 다른 환경에 배포된 단일 애플리케이션의 서로 다른 버전을 사용하는 일반적인 SDLC(시스템 개발 수명 주기) 패턴을 사용할 수 있습니다. 문서 보기 [Project App Builder 애플리케이션용 CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) 추가 정보.
>
>인스턴스 유형별 런타임 구현에 차이가 없는 한 인스턴스(작성자, 게시)별로 별도의 작업 영역이 필요하지 않습니다.

## 원격 렌더러 구성 {#remote-renderer-configuration}

AEM은 원격으로 렌더링된 콘텐츠를 검색할 수 있는 위치를 알고 있어야 합니다. 에 상관없이 [ssr에 대해 구현하도록 선택한 모델,](#adobe-i-o-runtime)이 원격 렌더링 서비스에 액세스하는 방법을 AEM에 지정해야 합니다.

이 작업은 다음을 통해 수행됩니다. **RemoteContentRenderer - Configuration Factory OSGi 서비스**. 웹 콘솔 구성 콘솔에서 문자열 &quot;RemoteContentRenderer&quot;를 검색합니다. `http://<host>:<port>/system/console/configMgr`.

![렌더러 구성](assets/rendererconfig.png)

구성에 사용할 수 있는 필드는 다음과 같습니다.

* **컨텐츠 경로 패턴** - 필요한 경우 컨텐츠의 일부와 일치하는 정규 표현식
* **원격 끝점 URL** - 콘텐츠 생성을 담당하는 엔드포인트의 URL
   * 로컬 네트워크에 없는 경우 보안 HTTPS 프로토콜을 사용합니다.
* **추가 요청 헤더** - 원격 끝점으로 전송된 요청에 추가할 추가 헤더
   * 패턴: `key=value`
* **요청 시간 초과** - 원격 호스트 요청 시간 제한(밀리초)

>[!NOTE]
>
>를 구현할지 여부에 관계없이 [AEM 기반 통신 흐름](#aem-driven-communication-flow) 또는 [Adobe I/O Runtime 기반 플로우,](#adobe-i-o-runtime-driven-communication-flow) 원격 콘텐츠 렌더러 구성을 정의해야 합니다.
>
>다음을 선택하는 경우에도 이 구성을 정의해야 합니다. [사용자 지정 Node.js 서버를 사용합니다.](#using-node-js)

>[!NOTE]
>
>이 구성은 [원격 콘텐츠 렌더러,](#remote-content-renderer) 추가 확장 및 사용자 정의 옵션을 사용할 수 있습니다.

## AEM 기반 통신 흐름 {#aem-driven-communication-flow}

SSR을 사용하는 경우 [구성 요소 상호 작용 워크플로](/help/sites-developing/spa-overview.md#workflow) AEM의 SPA에는 앱의 초기 콘텐츠가 Adobe I/O Runtime에서 생성되는 단계가 포함됩니다.

1. 브라우저가 AEM에서 SSR 콘텐츠를 요청합니다.

1. AEM은 모델을 Adobe I/O Runtime에 게시합니다.

1. Adobe I/O Runtime은 생성된 콘텐츠를 반환합니다.

1. AEM은 백엔드 HTML 구성 요소의 HTL 템플릿을 통해 Adobe I/O Runtime에서 반환되는 페이지를 제공합니다.

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime 기반 통신 흐름 {#adobe-i-o-runtime-driven-communication-flow}

이전 섹션에서는 AEM에서 SPA에 대한 서버측 렌더링의 표준 및 권장 구현에 대해 설명합니다. 여기서 AEM은 콘텐츠의 부트스트래핑 및 서비스를 수행합니다.

또는 Adobe I/O Runtime이 부트스트래핑을 담당하도록 SSR을 구현하여 통신 흐름을 효과적으로 반전시킬 수 있다.

두 모델 모두 유효하며 AEM에서 지원합니다. 다만, 특정 모델을 구현하기 전에 각각의 장단점을 고려해야 한다.

<table>
 <tbody>
  <tr>
   <th><strong>부트스트랩</strong></th>
   <th><strong>장점</strong></th>
   <th><strong>단점</strong></th>
  </tr>
  <tr>
   <th><strong>AEM의 방식으로</strong><br /> </th>
   <td>
    <ul>
     <li>AEM은 필요한 경우 라이브러리 삽입을 관리합니다</li>
     <li>AEM에서만 리소스 유지 관리<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA 개발자에게 생소할 수 있음<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>Adobe I/O Runtime을 통해<br /> </strong></th>
   <td>
    <ul>
     <li>SPA 개발자에게 더 친숙함<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>CSS 및 JavaScript와 같이 애플리케이션에 필요한 Clientlib 리소스는 AEM 개발자가 <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> 속성<br /> </li>
     <li>AEM과 Adobe I/O Runtime 간에 리소스를 동기화해야 합니다.<br /> </li>
     <li>SPA 작성을 활성화하려면 Adobe I/O Runtime용 프록시 서버가 필요할 수 있습니다</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSR 계획 {#planning-for-ssr}

응용 프로그램의 일부만 서버측에서 렌더링해야 합니다. 일반적인 예는 렌더링된 서버측에서 페이지의 초기 로드 시 접힌 부분 위에 표시되는 콘텐츠입니다. 이렇게 하면 이미 렌더링된 콘텐츠를 클라이언트에 전달하여 시간을 절약할 수 있습니다. 사용자가 SPA과 상호 작용할 때 추가 콘텐츠는 클라이언트에 의해 렌더링됩니다.

SPA에 대한 서버측 렌더링을 구현할 때 필요한 앱 부분을 검토하십시오.

## SSR을 사용하여 SPA 개발 {#developing-an-spa-using-ssr}

SPA 구성 요소는 클라이언트(브라우저에서) 또는 서버측에서 렌더링할 수 있습니다. 서버측에서 렌더링될 때 창 크기 및 위치와 같은 브라우저 속성이 없습니다. 따라서 SPA 구성 요소는 렌더링될 위치에 대해 가정하지 않고 동형이어야 합니다.

SSR을 사용하려면 서버측 렌더링을 담당하는 AEM 및 Adobe I/O Runtime에 코드를 배포합니다. 대부분의 코드는 동일하지만 서버별 작업은 다릅니다.

## AEM의 SPA용 SSR {#ssr-for-spas-in-aem}

AEM의 SPA용 SSR에는 앱 콘텐츠 서버측 렌더링에 대해 호출되는 Adobe I/O Runtime이 필요합니다. 앱의 HTL 내에서 콘텐츠를 렌더링하기 위해 Adobe I/O Runtime의 리소스가 호출됩니다.

AEM이 Angular 및 React SPA 프레임워크를 기본적으로 지원하는 것처럼 Angular 및 React 앱에 대해서도 서버측 렌더링이 지원됩니다. 자세한 내용은 두 프레임워크에 대한 NPM 설명서 를 참조하십시오.

* React: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

간단한 예를 보려면 다음을 참조하십시오. [We.Retail 저널 앱](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). 전체 애플리케이션 서버측을 렌더링합니다. 이는 실제 예는 아니지만 SSR을 구현하는 데 필요한 사항을 보여 줍니다.

>[!CAUTION]
>
>다음 [We.Retail 저널 앱](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 는 데모용으로만 사용되므로 권장 Adobe I/O Runtime 대신 Node.js를 간단한 예로 사용합니다. 프로젝트 작업에는 이 예제를 사용하지 마십시오.

>[!NOTE]
>
>AEM 프로젝트는 React 또는 Angular를 통해 SPA 프로젝트를 지원하고 SPA SDK를 사용하는 [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)을 사용해야 합니다.

## Node.js 사용 {#using-node-js}

Adobe I/O Runtime은 AEM에서 SPA용 SSR을 구현하기 위한 권장 솔루션입니다.

온-프레미스 AEM 인스턴스의 경우 위에서 설명한 것과 동일한 방식으로 사용자 지정 Node.js 인스턴스를 사용하여 SSR을 구현할 수도 있습니다. 이는 Adobe에서 지원되지만 권장되지 않습니다.

>[!NOTE]
>
>Node.js는 Adobe 호스팅 AEM 인스턴스에 대해 지원되지 않습니다.

>[!NOTE]
>
>Node.js를 통해 SSR을 구현해야 하는 경우, Adobe은 모든 AEM 환경(작성자, 게시, 스테이지 등)에 대해 별도의 Node.js 인스턴스를 권장합니다.

## 원격 콘텐츠 렌더러 {#remote-content-renderer}

다음 [원격 콘텐츠 렌더러 구성](#remote-content-renderer-configuration) AEM에서 SPA과 함께 SSR을 사용하는 것이 필요하며, 필요에 따라 확장 및 사용자 정의할 수 있는 보다 일반적인 렌더링 서비스를 제공합니다.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 는 Adobe I/O과 같은 원격 서버에 렌더링된 컨텐츠를 검색하는 OSGi 서비스입니다. 원격 서버로 전송된 콘텐츠는 전달된 요청 매개 변수를 기반으로 합니다.

`RemoteContentRenderingService` 추가적인 컨텐츠 조작이 필요한 경우 종속성 반전 을 통해 사용자 지정 Sling 모델 또는 서블릿에 삽입할 수 있습니다.

이 서비스는 내부적으로 [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

다음 `RemoteContentRendererRequestHandlerServlet` 를 사용하여 프로그래밍 방식으로 요청 구성을 설정할 수 있습니다. `DefaultRemoteContentRendererRequestHandlerImpl`제공된 기본 요청 처리기 구현에서는 콘텐츠 구조의 위치를 원격 끝점에 매핑하기 위한 여러 OSGi 구성을 만들 수 있습니다.

사용자 지정 요청 핸들러를 추가하려면 `RemoteContentRendererRequestHandler` 인터페이스. 다음을 설정하십시오. `Constants.SERVICE_RANKING` 구성 요소 속성을 100보다 큰 정수로 지정합니다. 이 값은 `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 기본 핸들러의 OSGi 구성 구성 {#configure-default-handler}

섹션에 설명된 대로 기본 핸들러의 구성을 구성해야 합니다 [원격 콘텐츠 렌더러 구성](#remote-content-renderer-configuration).

### 원격 콘텐츠 렌더러 사용 {#usage}

서블릿이 페이지에 삽입할 수 있는 일부 콘텐츠를 가져와서 반환하도록 하려면 다음 작업을 수행하십시오.

1. 원격 서버에 액세스할 수 있는지 확인합니다.
1. AEM 구성 요소의 HTL 템플릿에 다음 코드 조각 중 하나를 추가합니다.
1. OSGi 구성을 생성 또는 수정합니다(선택적).
1. 사이트 콘텐츠 검색

일반적으로 페이지 구성 요소의 HTL 템플릿은 이러한 기능의 주요 수신자입니다.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 요구 사항 {#requirements}

서블릿은 슬링 모델 익스포터를 사용하여 구성 요소 데이터를 직렬화합니다. 기본적으로 `com.adobe.cq.export.json.ContainerExporter` 및 `com.adobe.cq.export.json.ComponentExporter` 슬링 모델 어댑터로 지원됩니다. 필요한 경우 요청을 조정할 클래스를 추가할 수 있습니다. `RemoteContentRendererServlet` 및 구현 `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. 추가 클래스는 `ComponentExporter`.
