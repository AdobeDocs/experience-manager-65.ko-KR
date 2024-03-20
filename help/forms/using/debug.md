---
title: HTML 5 양식 디버깅
description: 이 문서에는 알려진 다양한 문제를 해결하는 단계가 나열되어 있습니다.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: HTML5 Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# HTML 5 양식 디버깅 {#debugging-html-forms}

이 문서에는 몇 가지 문제 해결 시나리오가 포함되어 있습니다. 각 시나리오에 대해 문제를 해결하기 위한 몇 가지 단계가 제공됩니다. 다음 단계를 수행하고 문제가 지속되면 로그를 가져오고 오류/경고를 검토하도록 로거를 구성합니다. HTML5 양식 로깅에 대한 자세한 내용은 [HTML5 양식에 대한 로그 생성](/help/forms/using/enable-logs.md).

## 문제: 양식을 렌더링할 때 org.apache.sling.api.SlingException 예외 페이지가 표시됩니다 {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

예외 세부 정보에서 단어를 검색합니다. **원인:**.

가능한 이유는 URL에 있는 하나 이상의 매개 변수가 올바르지 않기 때문입니다.

다음 매개 변수를 확인하십시오.

<table>
 <tbody>
  <tr>
   <td><strong>매개변수</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>템플릿</td>
   <td>템플릿의 파일 이름입니다.</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>템플릿 및 관련 리소스가 있는 경로</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>템플릿과 병합되는 데이터 파일의 절대 경로입니다.<br /> 참고: 경로는 데이터 파일의 절대 경로를 정의합니다.</td>
  </tr>
  <tr>
   <td>데이터</td>
   <td>템플릿과 병합되는 UTF-8 인코딩 데이터 바이트입니다.</td>
  </tr>
 </tbody>
</table>

## 문제: 양식을 렌더링할 수 없음(오류 메시지가 표시됨) {#problem-unable-to-render-form}

1. 지정된 매개 변수가 올바른지 확인하십시오. 매개 변수에 대한 자세한 내용은 [렌더링 매개 변수](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. CRX 패키지 관리자(https://)에 로그인합니다&lt;server>:&lt;port>/crx/packmgr/index.jsp)을 방문하여 다음 패키지가 올바르게 설치되었는지 확인하십시오.

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. https://에서 CQ 웹 콘솔(Felix 콘솔)에 로그인합니다.&lt;server>:&lt;port>/system/console/bundles.

   다음 번들의 상태가 &quot;활성&quot;인지 확인하십시오.

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclecala-lang.bundle)

   * Adobe XFA Forms 렌더러

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Adobe XFA Forms LC 커넥터

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 문제: 스타일이 없는 양식 렌더링 {#problem-form-renders-without-styles}

1. 브라우저에서 을 엽니다. **개발자 도구**. profile.css를 사용할 수 있는지 확인합니다.
1. profile.css 파일을 사용할 수 없는 경우 https://에서 CRX DE에 로그인합니다.&lt;server>:&lt;port>/crx/de.
1. 왼쪽의 폴더 계층에서 /etc/clientlibs/fd/xfaforms/ 로 이동합니다. 폴더에 나열된 css.txt 파일을 엽니다.

   * 프로필
   * 런타임
   * scrollnav
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

1. 언급된 파일을 사용할 수 없는 경우 adobe-lc-forms-runtime-pkg-를 설치합니다.&lt;version>.zip 패키지가 다시 업데이트되었습니다.

### 문제: 예기치 않은 오류가 발생했습니다. {#problem-unexpected-error-encountered}

1. 양식 URL에서 쿼리 매개 변수 debugClientLibs를 추가하고 값을 true로 설정합니다(예: https://).&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path=&quot;&quot;>템플릿(&amp;t)=&lt;name of=&quot;&quot; xdp=&quot;&quot; file=&quot;&quot;>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. chrome과 같은 데스크탑 브라우저에서 개발자 도구 > 콘솔로 이동합니다.
1. 로그를 열어 오류 유형을 식별합니다. 로그에 대한 자세한 내용은 [HTML 5 양식 로그](/help/forms/using/enable-logs.md).
1. 개발자 도구 > 콘솔로 이동합니다. 스택 추적을 사용하여 오류의 원인이 되는 코드를 찾습니다. 오류를 디버깅하여 문제를 해결합니다.

   >[!NOTE]
   >
   >스크립팅에 실패한 경우 양식의 PDF 렌디션에서도 동일한 문제가 발생하는지 확인하십시오. 그렇다면 양식 스크립팅 논리에 문제가 있습니다.

## 문제: 양식을 제출할 수 없음 {#problem-unable-to-submit-the-form}

1. AEM 서버에 액세스할 수 있는 권한이 있고 서버에 연결되어 있는지 확인하십시오.
1. 매개 변수 submitUrl이 올바른지 확인합니다.
1. 에 언급된 대로 클라이언트측 로그 활성화 [HTML 5 양식에 대한 로그](/help/forms/using/enable-logs.md) 디버그 옵션 사용 **1-a5-b5-c5**. 그런 다음 양식을 렌더링하고 제출을 클릭합니다. 브라우저 디버그 콘솔을 열고 오류가 있는지 확인합니다.
1. 에 언급된 대로 서버 로그를 찾습니다. [HTML 5 양식에 대한 로그](/help/forms/using/enable-logs.md). 제출 중에 서버 로그에 오류가 있는지 확인하십시오.

## 문제: 현지화된 오류 메시지가 표시되지 않음 {#problem-localized-error-messages-do-not-display}

1. 추가 쿼리 매개 변수를 사용하여 양식 렌더링 **debugClientLibs=true** 데스크탑 브라우저에서 개발자 도구 > 리소스로 이동한 다음 I18N.css 파일을 확인합니다.
1. 파일을 사용할 수 없는 경우 https://에서 CRX DE에 로그인합니다.&lt;server>:&lt;port>/crx/de.
1. 왼쪽의 폴더 계층에서 /libs/fd/xfaforms/clientlibs/I18N으로 이동하여 다음 파일과 폴더가 있는지 확인합니다.

   * Namespace.js
   * LogMessages.js
   * 언어용 폴더

1. 위의 파일 또는 폴더가 없는 경우 **adobe-lc-forms-runtime-pkg-&lt;version>.zip** 다시 패키지.
1. 로케일 이름과 동일한 이름의 폴더로 이동하고 해당 콘텐츠를 확인합니다. 폴더에는 다음 파일이 포함되어야 합니다.

   * I18N.js
   * js.txt

1. js.txt의 콘텐츠를 확인하고 다음 항목이 있는지 확인합니다.

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 문제: 이미지가 표시되지 않음 {#problem-image-not-showing-up}

1. 이미지 URL이 올바른지 확인합니다.
1. 브라우저가 이 유형의 이미지를 지원하는지 확인하십시오.
1. 예외 세부 정보에서 단어를 검색합니다. **원인:**.

   가능한 이유는 URL에 있는 하나 이상의 매개 변수가 올바르지 않기 때문입니다.

   다음 매개 변수를 확인하십시오. 단계 텍스트

<table>
 <tbody>
  <tr>
   <td><strong>매개변수</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>템플릿</td>
   <td>템플릿의 파일 이름입니다.</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>템플릿 및 관련 리소스가 있는 경로</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>템플릿과 병합되는 데이터 파일의 절대 경로입니다.<br /> 참고: 경로는 데이터 파일의 절대 경로를 정의합니다.</td>
  </tr>
  <tr>
   <td>데이터</td>
   <td>템플릿과 병합되는 UTF-8 인코딩 데이터 바이트입니다.</td>
  </tr>
 </tbody>
</table>

1. 데스크탑 브라우저에서 개발자 도구 > 리소스로 이동합니다.

   이미지가 표시되면 [프레임]에서 왼쪽을 선택합니다.
