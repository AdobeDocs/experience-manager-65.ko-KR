---
title: HTML5 양식 서비스 프록시
seo-title: HTML5 양식 서비스 프록시
description: HTML5 양식 서비스 프록시는 제출 서비스에 대한 프록시를 등록하는 구성입니다. 서비스 프록시를 구성하려면 요청 매개 변수 submissionServiceProxy를 통해 제출 서비스의 URL을 지정합니다.
seo-description: HTML5 양식 서비스 프록시는 제출 서비스에 대한 프록시를 등록하는 구성입니다. 서비스 프록시를 구성하려면 요청 매개 변수 submissionServiceProxy를 통해 제출 서비스의 URL을 지정합니다.
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---


# HTML5 양식 서비스 프록시{#html-forms-service-proxy}

HTML5 양식 서비스 프록시는 제출 서비스에 대한 프록시를 등록하는 구성입니다. 서비스 프록시를 구성하려면 요청 매개 변수 *submissionServiceProxy*&#x200B;를 통해 제출 서비스의 URL을 지정합니다.

## 서비스 프록시의 이점 {#benefits-of-service-proxy-br}

서비스 프록시는 다음을 제거합니다.

* HTML5 양식 작업 과정을 사용하려면 HTML5 양식 사용자를 위한 제출 서비스 &quot;/content/xfaforms/submission/default&quot;를 열어야 합니다. 의도하지 않은 광범위한 사용자에게 AEM 서버를 노출합니다.
* 서비스 URL은 양식의 런타임 모델에 포함됩니다. 서비스 URL 경로를 변경할 수 없습니다.
* 제출은 2단계 프로세스입니다. 양식 데이터를 제출하려면 서버에 2개 이상의 여정이 필요합니다. 따라서 서버의 로드를 증가시킵니다.
* HTML5 양식은 PDF 요청 대신 POST 요청에 데이터를 전송합니다. PDF 양식 및 HTML5 양식을 모두 포함하는 워크플로우의 경우 제출 작업을 처리하는 두 가지 방법이 필요합니다.

### 토폴로지 {#topologies-br}

HTML5 양식은 다음 토폴로지를 사용하여 AEM 서버에 연결할 수 있습니다.

* AEM Server 또는 HTML5 양식이 POST을 통해 데이터를 서버로 보내는 토폴로지입니다.
* 프록시 서버가 POST 데이터를 서버로 보내는 토폴로지.

![HTML5 양식 서비스 프록시 토폴로지](assets/topology.png)

HTML5 양식 서비스 프록시 토폴로지

HTML5 양식은 AEM 서버에 연결하여 서버측 스크립트, 웹 서비스 및 제출을 실행할 수 있습니다. HTML5 양식의 XFA 런타임은 다양한 매개 변수를 사용하여 &quot;/bin/xfaforms/submitaction&quot; 끝점에 대한 Ajax 호출을 사용하여 AEM 서버에 연결합니다. HTML5 양식은 AEM 서버를 연결하여 다음 작업을 수행합니다.

#### 서버측 스크립트 및 웹 서비스 실행 {#execute-server-sided-scripts-and-web-services}

서버에서 실행되도록 표시된 스크립트를 서버측 스크립트라고 합니다. 다음 표에는 서버 측 스크립트 및 웹 서비스에 사용되는 모든 매개 변수가 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>매개 변수</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p>활동</p> </td>
   <td><p>활동에는 요청을 트리거하는 이벤트가 포함됩니다. 클릭, 종료 또는 변경 등</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom에는 이벤트가 실행되는 객체의 SOM 식이 포함되어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>템플릿에는 양식을 렌더링하는 데 사용되는 템플릿이 포함되어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot에는 양식을 렌더링하는 데 사용되는 템플릿 루트 디렉토리가 포함되어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>데이터</p> </td>
   <td><p>데이터에는 양식을 렌더링하는 데 사용되는 일괄 바이트 수가 포함됩니다.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom에는 HTML5 양식의 DOM이 JSON 형식으로 포함되어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>패킷</p> </td>
   <td><p>패킷이 양식으로 지정됩니다.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir에는 양식을 렌더링하는 데 사용되는 디버그 디렉토리가 포함되어 있습니다.</p> </td>
  </tr>
 </tbody>
</table>

#### 데이터 제출 {#submit-data}

제출 단추를 클릭하면 HTML5 양식이 데이터를 서버로 보냅니다. 다음 표에는 HTML5 양식이 서버로 전송하는 모든 매개 변수가 나와 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>매개 변수</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>양식을 렌더링하는 데 사용되는 템플릿입니다.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>양식을 렌더링하는 데 사용되는 템플릿 루트 디렉토리.</p> </td>
  </tr>
  <tr>
   <td><p>데이터</p> </td>
   <td><p>양식을 렌더링하는 데 사용되는 bata 바이트 수입니다.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>JSON 형식의 HTML5 양식의 DOM.</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>데이터 XML이 게시된 URL.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>양식을 렌더링하는 데 사용되는 디버그 디렉토리입니다.</p> </td>
  </tr>
 </tbody>
</table>

#### 제출 프록시는 어떻게 작동합니까?{#how-nbsp-the-nbsp-submit-proxy-works}

제출 서비스 프록시는 제출 URL이 요청 매개 변수에 없는 경우 통과(pass through) 역할을 합니다. 그것은 통과 작용을 한다. 요청을 /bin/xfaforms/submitaction 끝점으로 보내고 XFA 런타임에 응답을 보냅니다.

제출 서비스 프록시는 요청 매개 변수에 제출 URL이 있는 경우 토폴로지를 선택합니다.

* AEM 서버가 데이터를 게시하면 프록시 서비스가 패스스루 역할을 합니다. 요청을 /bin/xfaforms/submitaction 끝점으로 보내고 XFA 런타임에 응답을 보냅니다.
* 프록시가 데이터를 게시하면 프록시 서비스는 submitUrl을 제외한 모든 매개 변수를 */bin/xfaforms/submitaction* 종료 지점에 전달하며 응답 스트림에서 XML 바이트를 받습니다. 그런 다음 프록시 서비스는 처리를 위해 데이터 xml 바이트를 submitUrl에 게시합니다.

* 데이터(POST 요청)를 서버로 보내기 전에 HTML5 양식이 서버의 연결 및 가용성을 확인합니다. 연결 및 가용성을 확인하기 위해 HTML 양식은 빈 헤드 요청을 서버로 보냅니다. 서버가 사용 가능한 경우 HTML5 양식이 서버에 데이터(POST 요청)를 전송합니다. 서버를 사용할 수 없는 경우 *서버에 연결할 수 없습니다.*&#x200B;이(가) 표시됩니다. 사전 감지 기능을 사용하면 사용자가 양식을 다시 채우는 번거로운 작업을 방지할 수 있습니다. 프록시 서블릿은 헤드 요청을 처리하며 예외를 throw하지 않습니다.
