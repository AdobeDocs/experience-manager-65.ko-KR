---
title: HTML5 forms 서비스 프록시
description: HTML5 forms 서비스 프록시는 제출 서비스에 대한 프록시를 등록하는 구성입니다. 서비스 프록시를 구성하려면 요청 매개 변수 submissionServiceProxy를 통해 제출 서비스의 URL을 지정합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# HTML5 forms 서비스 프록시{#html-forms-service-proxy}

HTML5 forms 서비스 프록시는 제출 서비스에 대한 프록시를 등록하는 구성입니다. 서비스 프록시를 구성하려면 요청 매개 변수를 통해 제출 서비스의 URL을 지정합니다 *submissionServiceProxy*.

## 서비스 프록시의 이점 {#benefits-of-service-proxy-br}

서비스 프록시는 다음을 제거합니다.

* HTML 5 forms 워크플로우를 사용하려면 HTML 5 forms 사용자에 대한 제출 서비스 &quot;/content/xfaforms/submission/default&quot;를 열어야 합니다. 의도하지 않은 대상에 AEM 서버를 더 많이 노출합니다.
* 서비스 URL이 양식의 런타임 모델에 포함되어 있습니다. 서비스 URL 경로를 변경할 수 없습니다.
* 제출은 2단계 프로세스입니다. 양식 데이터를 제출하려면 서버에 대한 여정이 두 개 이상 필요합니다. 따라서 서버의 로드가 증가합니다.
* HTML 5 Forms는 PDF 요청 대신 POST 요청에 데이터를 보냅니다. PDF 및 HTML 5 양식과 관련된 워크플로우의 경우 제출을 처리하는 두 가지 다른 방법이 필요합니다.

### 토폴로지 {#topologies-br}

HTML5 양식은 다음 토폴로지를 사용하여 AEM 서버에 연결할 수 있습니다.

* AEM Server 또는 HTML 5 Forms가 POST을 통해 서버에 데이터를 전송하는 토폴로지입니다.
* 프록시 서버가 서버에 POST 데이터를 전송하는 토폴로지입니다.

![HTML5 forms 서비스 프록시 토폴로지](assets/topology.png)

HTML5 forms 서비스 프록시 토폴로지

HTML5 양식은 AEM 서버에 연결하여 서버측 스크립트, 웹 서비스 및 제출을 실행합니다. HTML5 Forms의 XFA 런타임은 다양한 매개 변수와 함께 &quot;/bin/xfaforms/submitaction&quot; 끝점의 Ajax 호출을 사용하여 AEM 서버에 연결합니다. HTML5 forms는 AEM 서버를 연결하여 다음 작업을 수행합니다.

#### 서버측 스크립트 및 웹 서비스 실행 {#execute-server-sided-scripts-and-web-services}

서버에서 실행되도록 표시된 스크립트를 서버측 스크립트라고 합니다. 다음 표에는 서버측 스크립트 및 웹 서비스에 사용되는 모든 매개 변수가 나열되어 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>매개변수</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p>활동</p> </td>
   <td><p>활동에는 요청을 트리거하는 이벤트가 포함됩니다. 클릭, 종료 또는 변경 등</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom에는 이벤트가 실행되는 개체의 SOM 식이 포함되어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>템플릿에는 양식을 렌더링하는 데 사용되는 템플릿이 들어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot는 양식을 렌더링하는 데 사용되는 템플릿 루트 디렉터리를 포함합니다.</p> </td>
  </tr>
  <tr>
   <td><p>데이터</p> </td>
   <td><p>데이터에는 양식을 렌더링하는 데 사용되는 bata 바이트가 포함되어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom에는 JSON 형식으로 된 HTML5 양식의 DOM이 포함되어 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>패킷</p> </td>
   <td><p>패킷이 양식으로 지정됩니다.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir에는 양식을 렌더링하는 데 사용되는 디버그 디렉터리가 포함되어 있습니다.</p> </td>
  </tr>
 </tbody>
</table>

#### 데이터 제출 {#submit-data}

제출 단추를 클릭하면 HTML5 양식에서 서버로 데이터를 보냅니다. 다음 표에는 HTML5 양식에서 서버로 보내는 모든 매개 변수가 나열되어 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>매개변수</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p>템플릿</p> </td>
   <td><p>양식 렌더링에 사용된 템플릿.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>양식을 렌더링하는 데 사용되는 템플릿 루트 디렉터리입니다.</p> </td>
  </tr>
  <tr>
   <td><p>데이터</p> </td>
   <td><p>양식을 렌더링하는 데 사용되는 bata 바이트입니다.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>JSON 형식의 HTML5 양식 DOM.</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>데이터 XML이 게시되는 URL입니다.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>양식을 렌더링하는 데 사용되는 디버그 디렉터리입니다.</p> </td>
  </tr>
 </tbody>
</table>

#### 제출 프록시는 어떻게 작동합니까? {#how-nbsp-the-nbsp-submit-proxy-works}

제출 서비스 프록시는 제출 URL이 요청 매개 변수에 없는 경우 전달 역할을 합니다. 패스스루 역할을 합니다. 이 메서드는 /bin/xfaforms/submitaction 끝점에 요청을 보내고 XFA 런타임에 응답을 보냅니다.

제출 서비스 프록시는 제출 URL이 요청 매개 변수에 있는 경우 토폴로지를 선택합니다.

* AEM 서버가 데이터를 게시하는 경우 프록시 서비스는 통과 역할을 합니다. 이 메서드는 /bin/xfaforms/submitaction 끝점에 요청을 보내고 XFA 런타임에 응답을 보냅니다.
* 프록시가 데이터를 게시하는 경우 프록시 서비스는 submitUrl을 제외한 모든 매개 변수를 */bin/xfaforms/submitaction* 끝점 및 응답 스트림에서 xml 바이트를 수신합니다. 그런 다음 프록시 서비스는 데이터 xml 바이트를 submitUrl에 게시하여 처리합니다.

* 서버에 데이터(POST 요청)를 보내기 전에 HTML 5 양식에서 서버의 연결 및 가용성을 확인합니다. 연결 및 가용성을 확인하기 위해 HTML 양식은 서버에 빈 head 요청을 보냅니다. 서버를 사용할 수 있는 경우 HTML 5 양식은 서버에 데이터(POST 요청)를 보냅니다. 서버를 사용할 수 없는 경우 다음과 같은 오류 메시지가 표시됩니다. *서버에 연결할 수 없습니다.* 이 표시됩니다. 사전 감지는 사용자가 양식을 다시 채우는 번거로움을 방지합니다. 프록시 서블릿은 head 요청을 처리하고 예외를 throw하지 않습니다.
