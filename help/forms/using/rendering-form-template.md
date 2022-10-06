---
title: HTML5 양식의 양식 템플릿 렌더링
seo-title: Rendering form template for HTML5 forms
description: HTML5 양식 프로필은 프로필 렌더링과 연결됩니다. 프로필 렌더링은 Forms OSGi 서비스를 호출하여 양식의 HTML 표현을 생성하는 JSP 페이지입니다.
seo-description: HTML5 forms profiles are associated with profile renders. Profile Renders are JSP pages responsible for generating HTML representation of the form by calling the Forms OSGi service.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# HTML5 양식의 양식 템플릿 렌더링 {#rendering-form-template-for-html-forms}

## 렌더링 끝점 {#render-endpoint}

HTML5 양식에는 **프로필** 양식 템플릿의 모바일 렌더링을 활성화하기 위해 REST 엔드포인트로 노출되는 URL입니다. 이 프로필들은 **프로필 렌더러**. Forms OSGi 서비스를 호출하여 양식의 HTML 표현을 생성하는 JSP 페이지입니다. 프로파일 노드의 JCR 경로는 렌더링 끝점의 URL을 결정합니다. &#39;default&#39; 프로필을 가리키는 양식의 기본 렌더링 끝점 모양은 다음과 같습니다.

https://&lt;*호스트*>:&lt;*포트*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*xdp 양식을 포함하는 폴더의 경로*>&amp;template=&lt;*xdp 이름*>

예, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

사용자 지정 프로필의 경우 종단점이 그에 따라 변경됩니다. 예를 들어 이라는 이름의 사용자 지정 프로필의 종료 지점은 다음과 같습니다.

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

템플릿이 FormSubmission이라는 응용 프로그램의 AEM 저장소에 있는 경우 URI는 다음과 같습니다.

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## 렌더링 매개 변수 {#render-parameters}

양식을 HTML으로 렌더링하는 동안 지원되는 요청 매개 변수는 다음과 같습니다.

<table>
 <tbody>
  <tr>
   <th><strong>매개변수 </strong></th>
   <th><strong>설명</strong></th>
  </tr>
  <tr>
   <td>템플릿<br /> </td>
   <td>이 매개 변수는 템플릿 파일의 이름을 지정합니다.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>이 매개 변수는 템플릿과 관련 리소스가 상주하는 경로를 지정합니다. 이 경로는 서버 파일 시스템 경로나 저장소 경로 또는 http 또는 ftp 경로일 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>이 매개 변수는 양식 데이터 xml이 게시되는 URL을 지정합니다.<br /> </td>
  </tr>
 </tbody>
</table>

### 데이터 병합 을 양식 서식 파일로 {#merge-data-with-form-template}

| 매개변수 | 설명 |
|---|---|
| dataRef | 이 매개 변수는 **절대 경로** 템플릿과 병합되는 데이터 파일의 형식입니다. 이 매개 변수는 XML 형식으로 데이터를 반환하는 rest 서비스의 URL일 수 있습니다. |
| 데이터 | 이 매개 변수는 템플릿과 병합되는 UTF-8 인코딩 데이터 바이트를 지정합니다. 이 매개 변수를 지정하면 HTML5 양식에서 dataRef 매개 변수를 무시합니다. |

### 렌더링 매개 변수 전달 {#passing-the-render-parameter}

HTML5 양식은 렌더링 매개 변수를 전달하는 세 가지 방법을 지원합니다. URL, 키-값 쌍 및 프로필 노드를 통해 매개 변수를 전달할 수 있습니다. render 매개 변수에서 키-값 쌍은 가장 높은 우선 순위를 가지며 그 뒤에는 프로필 노드가 옵니다. URL 요청 매개 변수가 우선순위가 가장 낮습니다.

* **URL 요청 매개 변수**: URL에 렌더링 매개 변수를 지정할 수 있습니다. URL 요청 매개 변수에서 매개 변수가 최종 사용자에게 표시됩니다. 예를 들어 다음 제출 URL에는 URL의 템플릿 매개 변수가 포함되어 있습니다. `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute 요청 매개 변수**: 렌더링 매개 변수를 키-값 쌍으로 지정할 수 있습니다. SetAttribute 요청 매개 변수에서 매개 변수가 최종 사용자에게 표시되지 않습니다. 다른 JSP의 요청을 HTML5 양식 프로필 렌더러 JSP로 전달하여 사용할 수 있습니다 *setAttribute* 요청 개체에서 모든 렌더링 매개 변수를 전달하십시오. 이 메서드의 우선 순위가 가장 높습니다.

* **프로필 노드 요청 매개 변수:** 렌더링 매개 변수를 프로필 노드의 노드 속성으로 지정할 수 있습니다. 프로필 노드 요청 매개 변수에서 매개 변수가 최종 사용자에게 표시되지 않습니다. 프로필 노드는 요청이 전송되는 노드입니다. 매개 변수를 노드 속성으로 지정하려면 CRXDE Lite를 사용합니다.

### 매개 변수 제출 {#submit-parameters}

HTML5 양식 데이터 제출 AEM 서버에서 서버측 스크립트 및 웹 서비스를 실행합니다. AEM 서버에서 서버측 스크립트 및 웹 서비스를 실행하는 데 사용되는 매개 변수에 대한 자세한 내용은 [HTML5 양식 서비스 프록시](/help/forms/using/service-proxy.md).
