---
title: HTML 5 양식에 대한 로깅 활성화
seo-title: Enable logging for HTML5 forms
description: 로거 유틸리티는 양식에 대한 로깅을 활성화하고 양식 관련 문제를 디버깅하는 데 도움이 됩니다.
seo-description: The logger utility enables logging for a form and helps you debug form-related issues.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
feature: Mobile Forms
exl-id: 2f574c98-550c-4b84-be1e-46a2700e7277
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 6%

---

# HTML 5 양식에 대한 로깅 활성화{#enable-logging-for-html-forms}

HTML 5 양식에 대한 로그 작성을 시작하도록 로거 유틸리티를 구성할 수 있습니다. 로거 유틸리티에는 다양한 수준이 있으므로 요구 사항에 따라 수준을 설정할 수 있습니다. HTML 5 forms에는 서버 및 클라이언트 구성 요소가 있습니다. 두 구성 요소에 대해 로그를 구성할 수 있습니다.

## 서버측 로깅 구성 {#configuring-server-side-logging}

서버측 로그를 구성하려면 다음 단계를 수행하십시오.

1. 이동 `https://'[server]:[port]'/system/console/configMgr`. 을(를) 찾아 엽니다. *Apace Sling 로깅 로거 구성* 옵션을 선택합니다. 대화 상자가 나타납니다:

   ![ Api Sling 로깅 로거 구성 옵션 대화 상자](assets/logconfig.png)

   Api Sling 로깅 로거 구성 옵션

1. 변경 **로그 수준** 끝 **디버그**.

1. 의 이름 및 경로 지정 **로그 파일**.

   >[!NOTE]
   >
   >HTML5 양식 로그 디렉터리에 로그를 생성하려면 파일 이름 앞에 ../logs/를 추가합니다.

1. 변경 **Logger** 끝 **HTMLFormsPerfLogger**. **저장**&#x200B;을 클릭합니다.

## 클라이언트 로깅 구성 {#configuring-client-logging}

다음 방법을 사용하여 HTML5 양식에서 클라이언트측 로깅을 활성화할 수 있습니다.

* 라는 요청 매개 변수 사용 `log`
* CQ 구성 관리자 사용

### 요청 매개 변수를 사용하여 로깅 활성화 {#enabling-logging-using-request-parameter}

이 방법을 사용하면 특정 요청에 대한 로그를 생성할 수 있습니다. 요청 매개 변수의 이름은 입니다. `log`. 로그 URL은 다음과 같습니다.

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
   <td>로그가 브라우저로 이동됨 <strong>콘솔</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>로그는 클라이언트측의 JavaScript 개체에 수집되어 <strong>서버</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>위의 두 옵션 모두<br /> </td>
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
   <td>1</td>
   <td>치명<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>2</td>
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

#### 로거 범주 {#logger-categories}

<table>
 <tbody>
  <tr>
   <th>로그 범주</th>
   <th>설명</th>
  </tr>
  <tr>
   <td>a</td>
   <td>xfa(스크립팅 엔진 관련 로그)</td>
  </tr>
  <tr>
   <td>b</td>
   <td>xfaView(레이아웃 엔진 관련 로그)<br type="_moz" /> </td>
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
   <td>대상: 서버<br /> xfa 수준: 정보<br /> xfaView 수준: 디버그<br /> xfaPerf 수준: TRACE</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>각 로그 범주 a(xfa), b(xfaView) 및 c(xfaPerf)의 기본 로그 수준은 2(ERROR)입니다. 따라서 로그 구성: 2-b6의 경우 다른 범주에 대한 로그 수준은 다음과 같습니다.
>a(xfa): 2(기본 수준 오류)
>b(xfaView): 6(사용자 지정 TRACE)
>a(xfaPerf): 2(기본 수준 오류)

### Configuration Manager를 사용하여 로깅 활성화 {#enabling-logging-using-configuration-manager}

로깅을 활성화하기 위해 Configuration Manager를 사용하는 경우 로깅을 다시 비활성화할 때까지 모든 렌더링 요청에 대해 로그가 생성됩니다.

1. 에서 CQ 구성 관리자에 로그인합니다. `https://'[server]:[port]'/system/console/configMgr` 관리자 자격 증명으로 로그인합니다.
1. 을(를) 검색하고 **모바일 Forms 구성**.
1. 디버그 옵션 텍스트 상자에 이전 섹션에 설명된 대로 로그 구성을 입력합니다(예: **2-a4-b5-c6**

   ![양식 구성](assets/forms_configuration.png)

   양식 구성

## 로그 업로드 중 {#uploading-logs}

대상이 1로 설정되면 모든 클라이언트 스크립트 로그 메시지가 콘솔로 전달됩니다. 관리자가 이러한 로그를 서버 로그와 함께 필요로 하는 경우 대상 수준을 2로 설정하십시오. 이 수준에서 모든 로그는 클라이언트측의 JS 개체에 수집되며, 양식이 기본 프로필로 렌더링되는 경우 **로그 전송** 버튼은 의 왼쪽에 나타납니다. **기존 필드 강조 표시** 단추를 클릭합니다. 사용자가 링크를 클릭하면 수집된 모든 로그가 서버에 게시되고 서버에 구성된 오류 로그 파일에 기록됩니다.

기본적으로 모든 정보는 /crx-repository/logs/ 디렉토리에 있는 error.log 파일에 추가됩니다.

로그 파일의 위치 및 이름을 변경하려면 다음을 수행합니다.

1. 관리자로 Configuration Manager에 로그인합니다. 구성 관리자의 기본 URL은 입니다. `https://'[server]:[port]'/system/console/configMgr`.
1. 클릭 **Apache Sling 로깅 로거 구성**. 대화 상자가 나타납니다.

   ![logconfig-1](assets/logconfig-1.png)

1. 변경 **로그 수준** 을 디버그합니다.

1. 경로 및 이름 지정 **로그 파일**.

   >[!NOTE]
   >
   >다른 로그 파일이 보관된 동일한 디렉터리에 로그를 만들려면 ../logs/&lt;filename> 로그 파일 속성에서 참조할 수 있습니다.

1. 변경 **Logger** 끝 **HTMLFormsPerfLogger** 및 클릭 **저장**.
