---
title: Form Bridge와 HTML5 양식의 맞춤형 포털 통합
seo-title: Form Bridge와 HTML5 양식의 맞춤형 포털 통합
description: FormBridge API 파섹
seo-description: FormBridge API 파섹
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# Form Bridge와 HTML5 양식의 맞춤형 포털 통합{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge는 양식과 상호 작용할 수 있는 HTML5 양식 브리지 API입니다. FormBridge API 참조를 보려면 FormBridge [API 참조를](/help/forms/using/form-bridge-apis.md)참조하십시오.

FormBridge API 파섹 예를 들어 API를 사용하여 마법사와 같은 경험을 만들 수 있습니다.

기존 HTML 응용 프로그램은 FormBridge API를 활용하여 양식과 상호 작용하고 이를 HTML 페이지에 포함할 수 있습니다. 다음 단계에 따라 양식 브리지 API를 사용하여 필드 값을 설정할 수 있습니다.

## 웹 페이지에 HTML5 양식 통합 {#integrating-html-forms-to-a-web-page}

1. **프로필 선택 또는 프로필 만들기**

   1. CRX DE 인터페이스에서 다음 항목으로 이동합니다. `https://[server]:[port]/crx/de`Adobe
   1. 관리자 자격 증명으로 로그인합니다.
   1. 프로파일을 만들거나 기존 프로파일을 선택합니다.

      프로필을 만드는 방법에 대한 자세한 내용은 새 프로필 [만들기를 참조하십시오](/help/forms/using/custom-profile.md).

1. **HTML 프로필 수정**

   프로필 렌더러에 XFA 런타임, XFA 로케일 라이브러리 및 XFA 양식 HTML 조각을 포함시키고 웹 페이지를 디자인하고 웹 페이지 안에 양식을 배치할 수 있습니다.

   예를 들어 다음 코드 조각을 사용하여 두 개의 입력 필드와 양식을 포함하는 앱을 제작하여 양식과 외부 앱 간의 상호 작용을 보여 줍니다.

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/>
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >9 **행**: 페이지를 디자인할 CSS 스타일 및 JavaScript 파일에 대한 추가 JSP 참조가 포함되어 있습니다.
   >
   >
   >18 **줄의 &lt;div id=&quot;righdiv&quot;> 태그에는** XFA 양식의 HTML 조각이 포함되어 있습니다.
   페이지의 스타일이 두 개의 컨테이너로 지정됩니다. **왼쪽** , **오른쪽**. 올바른 컨테이너에는 양식이 있습니다. 왼쪽 컨테이너에는 두 개의 입력 필드와 외부 HTML 페이지의 일부가 있습니다.
   다음 스크린샷은 브라우저에서 양식이 표시되는 방식을 보여줍니다.

   ![포털](assets/portal.jpg)

   왼쪽은 HTML **페이지의**&#x200B;일부입니다. 필드를 포함하는 오른쪽은 **xfa 양식입니다**.

1. **페이지에서 양식 필드 액세스**

   다음은 양식 필드에 값을 설정하기 위해 추가할 수 있는 샘플 스크립트입니다.

   예를 들어 Fields First Name 및 **Last Name의** 값을 사용하여 EmployeeName을 **설정하려면** **window.formBridge.setFieldValue 함수를****** 호출합니다.

   마찬가지로 **window.formBridge.getFieldValue API를 호출하여 값을 읽을 수** 있습니다.

   ```javascript
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```

[지원 문의](https://www.adobe.com/account/sign-in.supportportal.html)
