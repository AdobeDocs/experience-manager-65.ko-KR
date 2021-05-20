---
title: HTML5 양식에 대한 로깅 활성화
seo-title: HTML5 양식에 대한 로깅 활성화
description: 로거 유틸리티는 양식에 대한 로깅을 활성화하고 양식 관련 문제를 디버깅하는 데 도움이 됩니다.
seo-description: 로거 유틸리티는 양식에 대한 로깅을 활성화하고 양식 관련 문제를 디버깅하는 데 도움이 됩니다.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
feature: Mobile Forms
exl-id: 2f574c98-550c-4b84-be1e-46a2700e7277
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 6%

---

# HTML5 양식에 대한 로깅 활성화{#enable-logging-for-html-forms}

HTML5 양식에 대한 로그 만들기를 시작하도록 로거 유틸리티를 구성할 수 있습니다. 로거 유틸리티에는 다양한 수준이 있으므로 요구 사항에 따라 수준을 설정할 수 있습니다. HTML5 양식에는 서버 및 클라이언트 구성 요소가 있습니다. 두 구성 요소 모두에 대한 로그를 구성할 수 있습니다.

## 서버 측 로깅 구성 {#configuring-server-side-logging}

서버측 로그를 구성하려면 다음 단계를 수행하십시오.

1. 이동 `https://'[server]:[port]'/system/console/configMgr`. *Apache Sling 로깅 로거 구성* 옵션을 찾아 엽니다. 대화 상자가 나타납니다:

   ![ Apache Sling 로깅 로거 구성 옵션 대화 상자](assets/logconfig.png)

   Apache Sling 로깅 로거 구성 옵션

1. **로그 수준** Debug **로 변경합니다.**

1. **로그 파일**&#x200B;의 이름과 경로를 지정합니다.

   >[!NOTE]
   >
   >HTML5 양식 로그 디렉토리에서 로그를 생성하려면 파일 이름 앞에 ../logs/ 를 추가합니다.

1. **로거**&#x200B;를 **HTMLFormsPerfLogger**&#x200B;로 변경합니다. **저장**&#x200B;을 클릭합니다.

## 클라이언트 로깅 구성 {#configuring-client-logging}

다음 메서드를 사용하여 HTML5 양식에서 클라이언트 측 로깅을 활성화할 수 있습니다.

* `log` 요청 매개 변수 사용
* CQ 구성 관리자 사용

### 요청 매개 변수 {#enabling-logging-using-request-parameter}을 사용하여 로깅 활성화

이 방법을 사용하여 특정 요청에 대한 로그를 생성할 수 있습니다. 요청 매개 변수의 이름은 &#39;log입니다. 로그 URL은 다음과 같습니다.

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

로그 구성은 로그 수준 및 로거 범주로 구성됩니다.

#### 로그 대상 {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>로그 대상</strong></th>
   <th><strong>설명</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>로그는 브라우저 <strong>Console</strong>로 전달됩니다</td>
  </tr>
  <tr>
   <td>2</td>
   <td>로그는 클라이언트 쪽의 JavaScript 개체에 수집되며 <strong>Server</strong>에 게시할 수 있습니다 </td>
  </tr>
  <tr>
   <td>3</td>
   <td>위의 옵션 모두<br /> </td>
  </tr>
 </tbody>
</table>

#### 로그 수준 {#log-levels}

<table>
 <tbody>
  <tr>
   <th>로그 수준</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>0</td>
   <td>끔<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>치명적<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2개</td>
   <td>오류<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>경고<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>4</td>
   <td>정보<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>5</td>
   <td>디버그<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>6</td>
   <td>TRACE<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>7</td>
   <td>모두<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### 로거 카테고리 {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>로그 범주</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>관리</td>
   <td>xfa(스크립팅 엔진 관련 로그)</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView (레이아웃 엔진 관련 로그)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>c</td>
   <td>xfaPerf(성능 관련 로그)<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

#### 로그 구성 {#log-configuration}

로그 URL에서 로그 구성 쿼리 문자열 매개 변수는 다음과 같이 정의됩니다.

`{destination}-{a level}-{b level}-{c level}`

예:

<table>
 <tbody>
  <tr>
   <th>로그 구성</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>2-a4-b5-c6<br type="_moz" /> </td>
   <td>대상:서버<br /> xfa 수준:INFO<br /> xfaView 수준:디버그<br /> xfaPerf 수준:TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>각 로그 카테고리 a(xfa), b(xfaView) 및 c(xfaPerf)에 대한 기본 로그 레벨은 2(ERROR)입니다. 따라서 로그 구성의 경우2-b6, 다양한 카테고리의 로그 수준은 다음과 같습니다.
>a (xfa):2(기본 수준 오류)
>b (xfaView):6(사용자가 지정한 TRACE)
>a(xfaPerf):2(기본 수준 오류)

### 구성 관리자를 사용하여 로깅 활성화 {#enabling-logging-using-configuration-manager}

로깅을 활성화하는 데 Configuration Manager를 사용하는 경우 로깅이 다시 비활성화될 때까지 모든 렌더링 요청에 대해 로그가 생성됩니다.

1. `https://'[server]:[port]'/system/console/configMgr`에서 CQ 구성 관리자에 로그인하고 관리자 자격 증명으로 로그인합니다.
1. 을(를) 검색하고 **모바일 Forms 구성**&#x200B;을 클릭합니다.
1. 디버그 옵션 텍스트 상자에 이전 섹션에 설명된 대로 로그 구성을 입력합니다(예: **2-a4-b5-c6**).

   ![양식 구성](assets/forms_configuration.png)

   양식 구성

## 로그 {#uploading-logs} 업로드

대상이 1로 설정되면 모든 클라이언트 스크립트 로그 메시지가 콘솔에 표시됩니다. 관리자가 서버 로그와 함께 이러한 로그를 필요로 하는 경우 대상 수준을 2로 설정하십시오. 이 수준에서 모든 로그는 클라이언트측의 JS 개체에 수집되며, 양식이 기본 프로필로 렌더링되는 경우 도구 모음에서 **기존 필드 강조** 단추 왼쪽에 **로그 보내기** 단추가 표시됩니다. 사용자가 링크를 클릭하면 수집된 모든 로그가 서버에 게시되고 서버의 구성된 오류 로그 파일에 기록됩니다.

기본적으로 /crx-repository/logs/ 디렉토리의 error.log 파일에 모든 정보가 추가됩니다.

로그 파일의 위치와 이름을 변경하려면

1. 관리자로 구성 관리자에 로그인합니다. 구성 관리자의 기본 URL은 `https://'[server]:[port]'/system/console/configMgr`입니다.
1. **Apache Sling Logging Configuration**&#x200B;을 클릭합니다. 대화 상자가 나타납니다.

   ![logconfig-1](assets/logconfig-1.png)

1. **로그 수준**&#x200B;을 디버그로 변경합니다.

1. **로그 파일**&#x200B;의 경로와 이름을 지정합니다.

   >[!NOTE]
   >
   >다른 로그 파일이 저장되는 동일한 디렉토리에 로그를 만들려면 Log Files 속성에 ../logs/&lt;filename>을 지정합니다.

1. **로거**&#x200B;를 **HTMLFormsPerfLogger**&#x200B;로 변경하고 **저장**&#x200B;을 클릭합니다.
