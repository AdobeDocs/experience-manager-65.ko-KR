---
title: HTML5 양식에 대한 로깅 사용
seo-title: HTML5 양식에 대한 로깅 사용
description: 로거 유틸리티를 사용하면 양식에 대한 로깅을 설정할 수 있으며 양식 관련 문제를 디버깅할 수 있습니다.
seo-description: 로거 유틸리티를 사용하면 양식에 대한 로깅을 설정할 수 있으며 양식 관련 문제를 디버깅할 수 있습니다.
uuid: 322306ba-8ad7-463d-8a9d-4cea5a0c4b55
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 973806f8-fb44-4d52-ad3f-bfbf335f60a1
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# HTML5 양식에 대한 로깅 사용{#enable-logging-for-html-forms}

로거 유틸리티를 구성하여 HTML5 양식에 대한 로그 작성을 시작할 수 있습니다. 로거 유틸리티에는 다양한 수준이 있으므로 요구 사항에 따라 수준을 설정할 수 있습니다. HTML5 양식에는 서버 및 클라이언트 구성 요소가 있습니다. 두 구성 요소 모두에 대한 로그를 구성할 수 있습니다.

## 서버측 로깅 구성 {#configuring-server-side-logging}

서버측 로그를 구성하려면 다음 단계를 수행하십시오.

1. 이동 `https://'[server]:[port]'/system/console/configMgr`. Apace Sling 로깅 *로거 구성* 옵션을 찾아 엽니다. 대화 상자가 나타납니다.

   ![ Apace Sling 로깅 로거 구성 옵션 대화 상자](assets/logconfig.png)

   Apace Sling 로깅 로거 구성 옵션

1. 로그 수준을 **디버그로** 변경합니다 ****.

1. 로그 파일의 이름과 경로를 **지정합니다**.

   >[!NOTE]
   >
   >HTML5 양식 로그 디렉토리에서 로그를 생성하려면 파일 이름 앞에 ../logs/를 추가합니다.

1. 로거를 **HTMLForms** PerfLogger **로 변경합니다**. **저장**&#x200B;을 클릭합니다.

## 클라이언트 로깅 구성 {#configuring-client-logging}

다음 방법을 사용하여 HTML5 양식에서 클라이언트측 로깅을 활성화할 수 있습니다.

* 요청 매개 변수 사용 `log`
* CQ 구성 관리자 사용

### 요청 매개 변수를 사용하여 로깅 활성화 {#enabling-logging-using-request-parameter}

이 방법을 사용하면 특정 요청에 대한 로그를 생성할 수 있습니다. 요청 매개 변수의 이름은 &#39;log&#39;입니다. 로그 URL은 다음과 같습니다.

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

로그 구성은 로그 수준과 로거 범주로 구성됩니다.

#### 로그 대상 {#log-destination}

<table>
 <tbody>
  <tr>
   <th><strong>로그 대상</strong></th>
   <th><strong>설명</strong></th>
  </tr>
  <tr>
   <td>1</td>
   <td>로그는 브라우저 콘솔로 <strong>전달됩니다</strong></td>
  </tr>
  <tr>
   <td>2</td>
   <td>로그는 클라이언트 쪽의 JavaScript 개체에서 수집되며 서버에 게시할 수 <strong>있습니다</strong> </td>
  </tr>
  <tr>
   <td>3</td>
   <td>위 옵션 모두<br /> </td>
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
   <td>치명적인<br type="_moz" /> </td>
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
   <td>DEBUG<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>6</td>
   <td>추적<br type="_moz" /> </td>
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
   <td>대상:서버<br /> xfa 수준:INFO<br /> xfaView 수준:디버그<br /> xfaPerf 수준:추적</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>각 로그 카테고리 a(xfa), b(xfaView) 및 c(xfaPerf)의 기본 로그 수준은 2(ERROR)입니다. 따라서 로그 구성의 경우:2-b6, 다른 카테고리에 대한 로그 수준은 다음과 같습니다.
>a (xfa):2(기본 수준 오류)
>b(xfaView):6(사용자 지정 추적)
>a (xfaPerf):2(기본 수준 오류)

### Configuration Manager를 사용하여 로깅 활성화 {#enabling-logging-using-configuration-manager}

Configuration Manager를 사용하여 로깅을 활성화하면 로깅이 다시 비활성화될 때까지 모든 렌더링 요청에 대해 로그가 생성됩니다.

1. 에서 CQ Configuration Manager에 로그인하고 관리자 자격 증명으로 `https://'[server]:[port]'/system/console/configMgr` 로그인합니다.
1. 모바일 양식 구성을 검색하고 **클릭합니다**.
1. 디버그 옵션 텍스트 상자에 이전 섹션에 설명된 대로 로그 구성을 입력합니다(예: **2-a4-b5-c6).**

   ![양식 구성](assets/forms_configuration.png)

   양식 구성

## 로그 업로드 {#uploading-logs}

대상이 1로 설정된 경우 모든 클라이언트 스크립트 로그 메시지가 콘솔로 전달됩니다. 관리자가 서버 로그와 함께 이러한 로그를 필요로 하는 경우 대상 수준을 2로 설정합니다. 이 수준에서는 모든 로그가 클라이언트 쪽의 JS 개체에 수집되며, 양식이 기본 프로필로 렌더링되면 도구 **모음의 [기존 필드 강조 표시** ] **단추 왼쪽에** [로그 보내기] 단추가 나타납니다. 사용자가 링크를 클릭하면 수집된 모든 로그가 서버에 게시되고 서버의 구성된 오류 로그 파일에 기록됩니다.

기본적으로 모든 정보는 /crx-repository/logs/ 디렉토리의 error.log 파일에 추가됩니다.

로그 파일의 위치와 이름을 변경하려면 다음을 수행합니다.

1. Configuration Manager에 관리자로 로그인합니다. Configuration Manager의 기본 URL은 `https://'[server]:[port]'/system/console/configMgr`입니다.
1. Apache **Sling 로깅 로거 구성을 클릭합니다**. 대화 상자가 나타납니다.

   ![logconfig-1](assets/logconfig-1.png)

1. 로그 수준을 **디버그로** 변경합니다.

1. 로그 파일의 경로와 이름을 **지정합니다**.

   >[!NOTE]
   >
   >다른 로그 파일이 보관되는 동일한 디렉토리에 로그를 만들려면 [로그 파일] 속성에 ../logs/&lt;filename>을 지정합니다.

1. Logger를 **HTMLFormsPerfLogger** 로 **변경하고** 저장을 **클릭합니다**.
