---
title: HTML5 양식용 양식 템플릿 렌더링
description: HTML5 양식 프로필은 프로필 렌더링과 연결됩니다. 프로필 렌더링은 Forms OSGi 서비스를 호출하여 양식의 HTML 표시를 생성하는 JSP 페이지입니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# HTML5 양식용 양식 템플릿 렌더링 {#rendering-form-template-for-html-forms}

## 렌더링 끝점 {#render-endpoint}

HTML5 양식에는 다음과 같은 개념이 있습니다 **프로필** 양식 템플릿을 모바일 렌더링할 수 있도록 REST 끝점으로 노출됩니다. 이 프로필은 **프로필 렌더러**. Forms OSGi 서비스를 호출하여 양식의 HTML 표시를 생성하는 JSP 페이지입니다. 프로필 노드의 JCR 경로는 렌더링 끝점의 URL을 결정합니다. &#39;default&#39; 프로필을 가리키는 폼의 기본 렌더링 끝점은 다음과 같습니다.

https://&lt;*호스트*>:&lt;*포트*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*양식 xdp가 포함된 폴더의 경로*>&amp;template=&lt;*xdp 이름*>

예, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

사용자 지정 프로필의 경우 끝점이 그에 따라 변경됩니다. 예를 들어, 사용자 지정 프로필의 중단점은 다음과 같습니다.

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
   <td>이 매개 변수는 템플릿 및 관련 리소스가 있는 경로를 지정합니다. 이 경로는 서버 파일 시스템 경로이거나 저장소 경로이거나 http 또는 ftp 경로일 수 있습니다.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>이 매개 변수는 양식 데이터 xml이 게시되는 URL을 지정합니다.<br /> </td>
  </tr>
 </tbody>
</table>

### 양식 템플릿과 데이터 병합 {#merge-data-with-form-template}

| 매개변수 | 설명 |
|---|---|
| dataRef | 이 매개 변수는 **절대 경로** 템플릿과 병합되는 데이터 파일의 경우입니다. 이 매개 변수는 데이터를 xml 형식으로 반환하는 나머지 서비스의 URL일 수 있습니다. |
| 데이터 | 이 매개 변수는 템플릿과 병합되는 UTF-8 인코딩 데이터 바이트를 지정합니다. 이 매개 변수를 지정하면 dataRef 매개 변수를 HTML5 양식에서 무시합니다. |

### 렌더링 매개 변수 전달 {#passing-the-render-parameter}

HTML5 양식은 렌더링 매개 변수를 전달하는 세 가지 메서드를 지원합니다. URL, 키-값 쌍 및 프로필 노드를 통해 매개 변수를 전달할 수 있습니다. 렌더링 매개 변수에서 키-값 쌍은 프로필 노드 다음에 오는 가장 높은 우선 순위를 갖습니다. URL 요청 매개 변수가 가장 우선합니다.

* **URL 요청 매개 변수**: URL에서 렌더링 매개 변수를 지정할 수 있습니다. URL 요청 매개 변수에서 매개 변수는 최종 사용자에게 표시됩니다. 예를 들어 다음 제출 URL은 URL의 템플릿 매개 변수를 포함합니다. `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **SetAttribute 요청 매개변수**: 렌더링 매개 변수를 키-값 쌍으로 지정할 수 있습니다. SetAttribute 요청 매개 변수에서 매개 변수는 최종 사용자에게 표시되지 않습니다. 다른 JSP의 요청을 HTML5 양식 프로필 렌더러 JSP로 전달하고 를 사용할 수 있습니다 *setAttribute* 요청 개체에서 모든 렌더링 매개 변수를 전달합니다. 이 방법의 우선 순위가 가장 높습니다.

* **프로필 노드 요청 매개 변수:** 렌더링 매개 변수를 프로필 노드의 노드 속성으로 지정할 수 있습니다. 프로필 노드 요청 매개 변수에서 매개 변수는 최종 사용자에게 표시되지 않습니다. 프로필 노드는 요청이 전송되는 노드입니다. 매개 변수를 노드 속성으로 지정하려면 CRXDE lite를 사용합니다.

### 매개 변수 제출 {#submit-parameters}

HTML5 forms는 데이터를 제출하고, AEM 서버에서 서버측 스크립트 및 웹 서비스를 실행합니다. AEM 서버에서 서버측 스크립트 및 웹 서비스를 실행하는 데 사용되는 매개 변수에 대한 자세한 내용은 [HTML5 forms 서비스 프록시](/help/forms/using/service-proxy.md).
