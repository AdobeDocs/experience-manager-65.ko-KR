---
title: HTML5 양식 디버깅
seo-title: HTML5 양식 디버깅
description: 문서 목록 단계에서는 알려진 다양한 문제를 해결합니다.
seo-description: 문서 목록 단계에서는 알려진 다양한 문제를 해결합니다.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# HTML5 양식 디버깅 {#debugging-html-forms}

이 문서에는 몇 가지 문제 해결 시나리오가 포함되어 있습니다. 각 시나리오에 대해 문제 해결을 위한 일부 단계가 제공됩니다. 다음 단계에 따라 문제가 지속되면 로거 로그를 가져와 오류/경고를 검토하도록 구성합니다. HTML5 양식 로깅에 대한 자세한 내용은 HTML5 [양식에](/help/forms/using/enable-logs.md)대한 로그 생성을 참조하십시오.

## 문제:양식을 렌더링할 때 org.apache.sling.api.SlingException 예외 페이지가 표시됩니다. {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

예외 세부 사항에서 **발생한 단어를 검색합니다**.

가능한 이유는 URL에 있는 하나 이상의 매개 변수가 잘못되었기 때문입니다.

다음 매개 변수를 확인하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>매개 변수</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>템플릿</td>
   <td>템플릿의 파일 이름</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>템플릿 및 관련 리소스가 있는 경로</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>템플릿과 병합된 데이터 파일의 절대 경로입니다.<br /> 참고:경로는 데이터 파일의 절대 경로를 정의합니다.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>템플릿과 병합된 UTF-8 인코딩 데이터 바이트.</td>
  </tr>
 </tbody>
</table>

## 문제:양식을 렌더링할 수 없습니다(오류 메시지가 표시됨). {#problem-unable-to-render-a-form-an-error-message-is-displayed}

1. 지정된 매개 변수가 올바른지 확인합니다. 매개 변수에 대한 자세한 내용은 매개 변수 [렌더링을 참조하십시오](/help/forms/using/debug.md#main-pars-table).
1. CRX 패키지 관리자(https://&lt;server>:&lt;port>/crx/packmgr/index.jsp)에 로그인하고 다음 패키지가 올바르게 설치되었는지 확인합니다.

   * adobe-lc-forms-content-pkg-&lt;버전>.zip
   * adobe-lc-forms-runtime-pkg-&lt;버전>.zip

1. https://&lt;server>:&lt;port>/system/console/bundles에서 CQ 웹 콘솔(Felix Console)에 로그인합니다.

   다음 번들의 상태가 &quot;활성&quot;인지 확인합니다.

   * scala-lang.bundle [osgi]
   (com.adobe.livecyclescala-lang.bundle)

   * Adobe XFA Forms Renderer
   (com.adobe.livecycle.adobe-lc-forms-core)

   * Adobe XFA Forms LC Connector
   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 문제:스타일이 없는 양식 렌더링 {#problem-form-renders-without-styles}

1. 브라우저에서 개발자 도구를 **엽니다**. profile.css를 사용할 수 있는지 확인합니다.
1. profile.css 파일을 사용할 수 없는 경우 https://&lt;server>:&lt;port>/crx/de에서 CRX DE에 로그인합니다.
1. 왼쪽의 폴더 계층 구조에서 /etc/clientlibs/fd/xfaforms/로 이동합니다. 폴더에 나열된 css.txt 파일을 엽니다.

   * 프로필
   * 런타임
   * scronav
   * 도구 모음
   * xfalib

1. css.txt 내에 언급된 파일이 /libs/fd/xfaforms/clientlibs/xfalib/css의 CRX DE lite에 있는지 확인합니다.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. 언급된 파일을 사용할 수 없는 경우 adobe-lc-forms-runtime-pkg-&lt;버전>.zip 패키지를 다시 설치합니다.

### 문제:예기치 않은 오류가 발생했습니다. {#problem-unexpected-error-encountered}

1. 양식 URL 파섹https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path>&amp;template=&lt;name of xdp file>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. 크롬과 같은 데스크탑 브라우저에서 개발자 도구 -> 콘솔로 이동합니다.
1. 로그를 열어 오류 유형을 식별합니다. 로그에 대한 자세한 내용은 HTML5 양식의 [로그를](/help/forms/using/enable-logs.md)참조하십시오.
1. 개발자 도구 -> 콘솔로 이동합니다. 스택 추적을 사용하여 오류를 일으키는 코드를 찾습니다. 오류를 디버그하여 문제를 해결하십시오.

   >[!NOTE]
   >
   >스크립팅이 실패한 경우 양식의 PDF 변환 중에도 동일한 문제가 발생하는지 확인하십시오. 예인 경우 양식 스크립팅 논리에 문제가 있습니다.

## 문제:양식을 제출할 수 없습니다. {#problem-unable-to-submit-the-form}

1. AEM 서버에 액세스할 권한이 있고 서버에 연결되어 있는지 확인합니다.
1. submitUrl 매개 변수가 올바른지 확인하십시오.
1. 디버그 옵션을 [1-a5-b5-c5로](/help/forms/using/enable-logs.md) 사용하여 HTML5 양식의 ****&#x200B;로그 파일에 설명된 대로 클라이언트측 로그를 활성화합니다. 양식을 렌더링하고 제출을 클릭합니다. 브라우저 디버그 콘솔을 열고 오류가 있는지 확인합니다.
1. HTML5 양식의 [로그에](/help/forms/using/enable-logs.md)언급된 대로 서버 로그를 찾습니다. 전송 중에 서버 로그에 오류가 있는지 확인합니다.

## 문제:현지화된 오류 메시지가 표시되지 않음 {#problem-localized-error-messages-do-not-display}

1. 데스크톱 브라우저에서 추가 쿼리 매개 변수 **debugClientLibs=true** 로 양식을 렌더링한 다음 개발자 도구 -> 리소스로 이동하여 I18N.css 파일을 확인합니다.
1. 파일을 사용할 수 없는 경우 https://&lt;server>:&lt;port>/crx/de에서 CRX DE에 로그인합니다.
1. 왼쪽의 폴더 계층 구조에서 /libs/fd/xfaforms/clientlibs/I18N으로 이동하여 다음 파일 및 폴더가 있는지 확인합니다.

   * Namespace.js
   * LogMessages.js
   * 언어 폴더

1. 위의 파일 또는 폴더가 없는 경우 **adobe-lc-forms-runtime-pkg-&lt;버전>.zip** 패키지를 다시 설치합니다.
1. 로케일 이름과 동일한 이름의 폴더를 탐색하고 해당 컨텐츠를 확인합니다. 폴더에는 다음 파일이 있어야 합니다.

   * I18N.js
   * js.txt

1. js.txt의 컨텐츠를 확인하고 다음 항목이 있는지 확인합니다.

   ```
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 문제:이미지가 표시되지 않음 {#problem-image-not-showing-up}

1. 이미지 URL이 올바른지 확인합니다.
1. 브라우저가 이 유형의 이미지를 지원하는지 확인합니다.
1. 예외 세부 사항에서 **발생한 단어를 검색합니다**.

   가능한 이유는 URL에 있는 하나 이상의 매개 변수가 잘못되었기 때문입니다.

   다음 매개 변수를 확인하십시오.단계 텍스트

<table>
 <tbody>
  <tr>
   <td><strong>매개 변수</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>템플릿</td>
   <td>템플릿의 파일 이름</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>템플릿 및 관련 리소스가 있는 경로</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>템플릿과 병합된 데이터 파일의 절대 경로입니다.<br /> 참고:경로는 데이터 파일의 절대 경로를 정의합니다.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>템플릿과 병합된 UTF-8 인코딩 데이터 바이트.</td>
  </tr>
 </tbody>
</table>

1. 데스크탑 브라우저에서 개발자 도구 -> 리소스로 이동합니다.

   이미지가 표시되는 경우 [프레임]의 왼쪽에서 선택합니다.

[지원 문의](https://www.adobe.com/account/sign-in.supportportal.html)
