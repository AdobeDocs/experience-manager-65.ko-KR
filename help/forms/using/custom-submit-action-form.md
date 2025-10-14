---
title: 적응형 양식에 대한 사용자 정의 제출 액션 작성
description: AEM Forms을 사용하면 적응형 양식에 대한 사용자 지정 제출 액션을 만들 수 있습니다. 이 문서에서는 적응형 양식에 대한 사용자 지정 제출 액션을 추가하는 절차에 대해 설명합니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c3d0dac-4e19-4eb3-a43d-909d526acd55
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components,Form Data Model
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 1%

---

# 적응형 양식에 대한 사용자 정의 제출 액션 작성{#writing-custom-submit-action-for-adaptive-forms}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/custom-submit-action-form.html?lang=ko) |
| AEM 6.5 | 이 문서 |

적응형 양식을 처리하려면 제출 액션이 필요합니다. 제출 액션은 적응형 양식을 사용하여 제출하는 데이터에 대해 수행되는 작업을 결정합니다. Adobe Experience Manager(AEM)에는 사용자가 제출한 데이터를 사용하여 수행할 수 있는 사용자 지정 작업을 보여 주는 [기본 제출 작업](../../forms/using/configuring-submit-actions.md)이 포함되어 있습니다. 예를 들어 이메일 전송 또는 데이터 저장과 같은 작업을 수행할 수 있습니다.

## 제출 액션 워크플로우 {#workflow-for-a-submit-action}

순서도는 적응형 양식에서 **[!UICONTROL 제출]** 단추를 클릭할 때 트리거되는 제출 작업의 워크플로를 보여 줍니다. 첨부 파일 구성 요소의 파일이 서버에 업로드되고 양식 데이터가 업로드된 파일의 URL로 업데이트됩니다. 클라이언트 내에서 데이터는 JSON 형식으로 저장됩니다. 클라이언트가 지정한 데이터를 마사지하고 XML 형식으로 반환하는 Ajax 요청을 내부 서블릿에 보냅니다. 클라이언트는 이 데이터를 작업 필드와 대조합니다. 양식 제출 액션을 통해 최종 서블릿(안내서 제출 서블릿)에 데이터를 제출합니다. 그런 다음 서블릿이 컨트롤을 제출 동작으로 전달합니다. 제출 액션은 요청을 다른 sling 리소스에 전달하거나 브라우저를 다른 URL로 리디렉션할 수 있습니다.

![제출 액션에 대한 워크플로를 보여 주는 흐름도](assets/diagram1.png)

### XML 데이터 형식 {#xml-data-format}

XML 데이터가 **`jcr:data`** 요청 매개 변수를 사용하여 서블릿으로 전송됩니다. 제출 액션은 매개변수에 액세스하여 데이터를 처리할 수 있습니다. 다음 코드에서는 XML 데이터의 형식을 설명합니다. 양식 모델에 바인딩된 필드가 **`afBoundData`** 섹션에 나타납니다. 바인딩되지 않은 필드가 `afUnoundData` 섹션에 나타납니다. `data.xml` 파일의 형식에 대한 자세한 내용은 [적응형 양식 필드 미리 채우기 소개](../../forms/using/prepopulate-adaptive-form-fields.md)를 참조하십시오.

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### 작업 필드 {#action-fields}

제출 액션은 숨겨진 입력 필드([input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input) HTML 태그 사용)를 렌더링된 양식 HTML에 추가할 수 있습니다. 이러한 숨겨진 필드에는 양식 제출을 처리하는 동안 필요한 값이 포함될 수 있습니다. 양식을 제출할 때 이러한 필드 값은 제출 작업 시 제출 처리 시 사용할 수 있는 요청 매개 변수로 다시 게시됩니다. 입력 필드를 작업 필드라고 합니다.

예를 들어 양식을 채우는 데 걸린 시간도 캡처하는 제출 작업은 숨겨진 입력 필드 `startTime` 및 `endTime`을(를) 추가할 수 있습니다.

스크립트는 양식을 렌더링할 때와 양식을 제출하기 전에 각각 `startTime` 및 `endTime` 필드의 값을 제공할 수 있습니다. 그런 다음 제출 ActionScript `post.jsp`은(는) 요청 매개 변수를 사용하여 이러한 필드에 액세스하고 양식을 채우는 데 필요한 총 시간을 계산할 수 있습니다.

### 첨부 파일 {#file-attachments}

제출 액션은 첨부 파일 구성 요소를 사용하여 업로드한 첨부 파일을 사용할 수도 있습니다. 제출 액션 스크립트는 sling [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html)를 사용하여 이러한 파일에 액세스할 수 있습니다. API의 [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) 메서드는 요청 매개 변수가 파일인지 양식 필드인지를 식별하는 데 도움이 됩니다. 제출 작업에서 요청 매개 변수를 반복하여 파일 첨부 매개 변수를 식별할 수 있습니다.

다음 샘플 코드는 요청의 첨부 파일을 식별합니다. 그런 다음 [API 가져오기](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get())를 사용하여 데이터를 파일로 읽습니다. 마지막으로 데이터를 사용하여 Document 객체를 만들고 목록에 추가합니다.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### 전달 경로 및 리디렉션 URL {#forward-path-and-redirect-url}

필요한 작업을 수행한 후 제출 서블릿은 요청을 전달 경로로 전달합니다. 작업은 setForwardPath API를 사용하여 안내서 제출 서블릿에서 전달 경로를 설정합니다.

작업이 전달 경로를 제공하지 않으면 제출 서블릿이 리디렉션 URL을 사용하여 브라우저를 리디렉션합니다. 작성자는 적응형 양식 편집 대화 상자에서 감사 페이지 구성을 사용하여 리디렉션 URL을 구성합니다. 제출 액션 또는 안내서 제출 서블릿의 setRedirectUrl API를 통해 리디렉션 URL을 구성할 수도 있습니다. 안내서 제출 서블릿에서 setRedirectParameters API를 사용하여 리디렉션 URL로 전송된 요청 매개 변수를 구성할 수도 있습니다.

>[!NOTE]
>
>작성자는 리디렉션 URL(감사 페이지 구성 사용)을 제공합니다. [기본 전송 작업](../../forms/using/configuring-submit-actions.md) 리디렉션 URL을 사용하여 전달 경로가 참조하는 리소스에서 브라우저를 리디렉션합니다.
>
>요청을 리소스 또는 서블릿에 전달하는 사용자 지정 제출 액션을 작성할 수 있습니다. Adobe은 전달 경로에 대한 리소스 처리를 수행하는 스크립트가 처리가 완료될 때 요청을 리디렉션 URL로 리디렉션하도록 권장합니다.

## 제출 액션 {#submit-action}

제출 액션은 다음을 포함하는 sling:Folder입니다.

* **addfields.jsp**: 이 스크립트는 변환 중에 HTML 파일에 추가된 작업 필드를 제공합니다. 이 스크립트를 사용하여 post.user.jsp 스크립트에서 제출 중에 필요한 숨겨진 입력 POST을 추가합니다.
* **dialog.xml**: 이 스크립트는 CQ 구성 요소 대화 상자와 유사합니다. 작성자가 맞춤화하는 구성 정보를 제공합니다. 제출 액션을 선택하면 적응형 양식 편집 대화 상자의 제출 액션 탭에 필드가 표시됩니다.
* POST **post.submit.jsp**: 제출 서블릿은 제출한 데이터와 이전 섹션의 추가 데이터를 사용하여 이 스크립트를 호출합니다. POST 이 페이지에서 작업을 실행하는 것에 대한 언급은 post.user.jsp 스크립트를 실행하는 것을 의미합니다. 제출 액션을 적응형 양식 편집 대화 상자에 표시할 적응형 양식에 등록하려면 다음 속성을 `sling:Folder`에 추가하십시오.

   * 문자열 및 값 **fd/af/components/guidesubmittype**&#x200B;의 **guideComponentType**
   * 제출 액션을 적용할 수 있는 적응형 양식의 형식을 지정하는 String 형식의 **guideDataModel**. **xfa**&#x200B;은(는) XFA 기반 적응형 양식에 대해 지원되지만 **xsd**&#x200B;은(는) XSD 기반 적응형 양식에 대해 지원됩니다. **basic**&#x200B;은(는) XDP 또는 XSD를 사용하지 않는 적응형 양식에 대해 지원됩니다. 여러 유형의 적응형 양식에 작업을 표시하려면 해당 문자열을 추가합니다. 각 문자열은 쉼표로 구분합니다. 예를 들어 XFA 및 XSD 기반 적응형 양식에 작업을 표시하려면 각각 **xfa** 및 **xsd** 값을 지정하십시오.

   * String 형식의 **jcr:description**. 이 속성의 값은 적응형 양식 편집 대화 상자의 제출 액션 탭에 있는 제출 액션 목록에 표시됩니다. 기본 작업은 위치 **/libs/fd/af/components/guidesubmittype**&#x200B;의 CRX 저장소에 있습니다.

## 사용자 지정 제출 액션 만들기 {#creating-a-custom-submit-action}

CRX 저장소에 데이터를 저장한 다음 이메일을 보내는 사용자 지정 제출 작업을 만들려면 다음 단계를 수행하십시오. 적응형 양식에는 CRX 저장소에 데이터를 저장하는 기본 제출 액션 저장소 콘텐츠(더 이상 사용되지 않음)가 포함되어 있습니다. 또한 CQ는 전자 메일을 보내는 데 사용할 수 있는 [메일](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko-KR) API를 제공합니다. 메일 API를 사용하기 전에 시스템 콘솔을 통해 일별 CQ 메일 서비스를 [구성](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko&wcmmode=disabled)합니다. 콘텐츠 저장(더 이상 사용되지 않음) 작업을 다시 사용하여 저장소에 데이터를 저장할 수 있습니다. 컨텐츠 저장(더 이상 사용되지 않음) 작업은 CRX 저장소의 /libs/fd/af/components/guidesubmittype/store에서 사용할 수 있습니다.

1. URL https://&lt;server>:&lt;port>/crx/de/index.jsp에서 CRXDE Lite에 로그인합니다. /apps/custom_submit_action 폴더에 sling:Folder 및 name store_and_mail 속성을 사용하여 노드를 만듭니다. custom_submit_action 폴더가 아직 없는 경우 만듭니다.

   ![sling:Folder 속성을 사용하여 노드를 만드는 것을 보여 주는 스크린샷](assets/step1.png)

1. **필수 구성 필드를 제공합니다.**

   스토어 작업에 필요한 구성을 추가합니다. /libs/fd/af/components/guidesubmittype/store에서 저장소 작업의 **cq:dialog** 노드를 /apps/custom_submit_action/store_and_email의 작업 폴더로 복사합니다.

   ![대화 상자 노드를 작업 폴더로 복사하는 스크린샷](assets/step2.png)

1. **작성자에게 전자 메일 구성을 묻는 메시지를 표시하는 구성 필드를 제공합니다.**

   또한 적응형 양식은 사용자에게 이메일을 보내는 이메일 작업을 제공합니다. 요구 사항에 따라 이 작업을 사용자 지정합니다. /libs/fd/af/components/guidesubmittype/email/dialog로 이동합니다. cq:dialog 노드 내의 노드를 제출 작업의 cq:dialog 노드(/apps/custom_submit_action/store_and_email/dialog)에 복사합니다.

   ![전자 메일 작업 사용자 지정](assets/step3.png)

1. **적응형 양식 편집 대화 상자에서 작업을 사용할 수 있도록 합니다.**

   store_and_email 노드에 다음 속성을 추가합니다.

   * **String** 형식의 **guideComponentType** 및 값 **fd/af/components/guidesubmittype**

   * **문자열** 유형 및 값 **xfa, xsd, basic**&#x200B;의 **guideDataModel**

   * **문자열** 유형 및 값 **저장 및 전자 메일 동작**&#x200B;의 **jcr:description**

1. 적응형 양식을 엽니다. **시작** 옆에 있는 **편집** 단추를 클릭하여 적응형 양식 컨테이너의 **편집** 대화 상자를 엽니다. 새 작업이 **작업 제출** 탭에 표시됩니다. **저장 및 전자 메일 작업**&#x200B;을 선택하면 대화 상자 노드에 추가된 구성이 표시됩니다.

   ![작업 구성 전송 대화 상자](assets/store_and_email_submit_action_dialog.jpg)

1. **작업을 완료하려면 작업을 사용하십시오.**

   작업에 post.user.jsp POST을 추가합니다. (/apps/custom_submit_action/store_and_mail/).

   기본 제공 저장 작업(post.store.jsp POST)을 실행합니다. CQ가 코드에 제공하는 [FormsHelper.runAction](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ko-KR)(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse) API를 사용하여 스토어 작업을 실행하십시오. JSP 파일에 다음 코드를 추가합니다.

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   이메일을 보내기 위해 코드는 구성에서 수신자 이메일 주소를 읽습니다. 작업 스크립트에서 구성 값을 가져오려면 다음 코드를 사용하여 현재 리소스의 속성을 읽으십시오. 마찬가지로 다른 구성 파일을 읽을 수 있습니다.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   마지막으로 CQ Mail API를 사용하여 이메일을 보냅니다. [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) 클래스를 사용하여 아래와 같이 전자 메일 개체를 만듭니다.

   >[!NOTE]
   >
   >POST JSP 파일에 post.user.jsp라는 이름이 있는지 확인합니다.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   적응형 양식에서 작업을 선택합니다. 이 작업은 이메일을 보내고 데이터를 저장합니다.
