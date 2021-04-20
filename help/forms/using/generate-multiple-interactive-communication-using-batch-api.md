---
title: 일괄 처리 API를 사용하여 인터랙티브한 여러 커뮤니케이션 생성
description: 일괄 처리 API를 사용하여 인터랙티브한 여러 커뮤니케이션 생성
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2239'
ht-degree: 4%

---


# Batch API {#use-batch-api-to-generate-multiple-ic}를 사용하여 인터랙티브한 여러 커뮤니케이션 생성

배치 API를 사용하여 템플릿에서 여러 대화형 커뮤니케이션을 생성할 수 있습니다. 템플릿은 데이터가 없는 대화형 커뮤니케이션입니다. 배치 API는 데이터를 템플릿과 결합하여 대화형 커뮤니케이션을 생성합니다. API는 대량의 대화형 커뮤니케이션 제작 시 유용합니다. 예를 들면 여러 고객을 위한 전화 요금 청구서, 신용 카드 명세서 등이 있습니다.

일괄 처리 API는 JSON 형식 및 양식 데이터 모델의 레코드(데이터)를 허용합니다. 생성된 대화형 통신 수는 구성된 양식 데이터 모델의 입력 JSON 파일에 지정된 레코드와 같습니다. API를 사용하여 인쇄 및 웹 출력을 모두 생성할 수 있습니다. [인쇄] 옵션은 PDF 문서를 만들고 [웹] 옵션은 각 개별 레코드에 대해 JSON 형식으로 데이터를 생성합니다.

## 배치 API {#using-the-batch-api} 사용

일괄 처리 API를 감시 폴더 또는 독립형 Rest API와 함께 사용할 수 있습니다. 배치 API를 사용할 수 있도록 생성된 대화형 통신에 대한 템플릿, 출력 유형(HTML, PRINT 또는 둘 다), 로케일, 프리플라이트 서비스 및 이름을 구성합니다.

레코드와 인터랙티브한 커뮤니케이션 템플릿을 결합하면 인터랙티브한 커뮤니케이션을 제작할 수 있습니다. 일괄 처리 API는 JSON 파일 또는 양식 데이터 모델을 통해 액세스하는 외부 데이터 소스에서 직접 레코드(인터랙티브한 통신 템플릿의 데이터)를 읽을 수 있습니다. 각 레코드를 별도의 JSON 파일에 보관하거나 JSON 배열을 만들어 모든 레코드를 단일 파일에 유지할 수 있습니다.

**JSON 파일의 단일 레코드**

```json
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**JSON 파일의 여러 레코드**

```json
[{
   "employee": {
       "name": "John",
       "id": 1,
       "mobileNo": 9871996461,
       "age": 39
   }
},{
   "employee": {
       "name": "Jacob",
       "id": 2,
       "mobileNo": 9871996462,
       "age": 38
   }
},{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}]
```

### 감시 폴더 {#using-the-batch-api-watched-folders}와 함께 일괄 처리 API 사용

API를 쉽게 경험할 수 있도록 AEM Forms은 곧바로 배치 API를 사용하도록 구성된 감시 폴더 서비스를 제공합니다. AEM Forms UI를 통해 서비스에 액세스하여 여러 대화형 통신을 생성할 수 있습니다. 요구 사항에 따라 맞춤형 서비스를 만들 수도 있습니다. 아래 나열된 메서드를 사용하여 감시 폴더와 함께 배치 API를 사용할 수 있습니다.

* JSON 파일 형식으로 입력 데이터(레코드)를 지정하여 대화형 통신을 만듭니다.
* 외부 데이터 소스에 저장되어 양식 데이터 모델을 통해 액세스하는 입력 데이터(레코드)를 사용하여 인터랙티브한 커뮤니케이션을 제작할 수 있습니다.

#### JSON 파일 형식으로 입력 데이터 레코드를 지정하여 대화형 통신 {#specify-input-data-in-JSON-file-format} 제작

레코드와 인터랙티브한 커뮤니케이션 템플릿을 결합하면 인터랙티브한 커뮤니케이션을 제작할 수 있습니다. 각 레코드에 대해 별도의 JSON 파일을 만들거나 JSON 배열을 만들어 모든 레코드를 단일 파일에 유지할 수 있습니다.

JSON 파일에 저장된 레코드로부터 대화형 통신을 만들려면:

1. [감시 폴더](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html)를 만들고 배치 API를 사용하도록 구성합니다.
   1. AEM Forms 작성자 인스턴스에 로그인합니다.
   1. **[!UICONTROL 도구]** > **[!UICONTROL Forms]** > **[!UICONTROL 감시 폴더 구성]**&#x200B;으로 이동합니다. **[!UICONTROL 새로 만들기]**&#x200B;를 누릅니다.
   1. 폴더의 **[!UICONTROL 이름]** 및 실제 **[!UICONTROL 경로]**&#x200B;를 지정합니다. 예, `c:\batchprocessing`.
   1. **[!UICONTROL 파일을 사용하여 처리]** 필드에서 **[!UICONTROL 서비스]** 옵션을 선택합니다.
   1. **[!UICONTROL 서비스 이름]** 필드에서 **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 서비스를 선택합니다.
   1. **[!UICONTROL 출력 파일 패턴]**&#x200B;을 지정합니다. 예를 들어 %F/ [패턴](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns)은 감시 폴더가 감시 폴더\input 폴더의 하위 폴더에서 입력 파일을 찾을 수 있도록 지정합니다.
1. 고급 매개 변수 구성:
   1. **[!UICONTROL 고급]** 탭을 열고 다음 사용자 지정 속성을 추가합니다.

      | 속성 | 유형 | 설명 |
      |--- |--- |--- |
      | templatePath | 문자열 | 사용할 대화형 통신 템플릿의 경로를 지정합니다. 예: /content/dam/formsanddocuments/tesample/mediumic. 필수 속성입니다. |
      | recordPath | 문자열 | recordPath 필드의 값은 대화형 통신 이름을 설정하는 데 도움이 됩니다. 레코드 필드의 경로를 recordPath 필드의 값으로 설정할 수 있습니다. 예를 들어 /employee/Id를 지정하면 id 필드의 값이 해당 대화형 통신에 대한 이름이 됩니다. 기본값은 임의 [임의 UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())입니다. |
      | usePrefillService | 부울 | 값을 False로 설정합니다. usePrefillService 매개 변수를 사용하여 해당 대화형 통신용으로 구성된 자동 완성 서비스에서 가져온 데이터로 대화형 통신을 미리 채울 수 있습니다. usePrefillService를 true로 설정하면 입력 JSON 데이터(각 레코드에 대해)가 FDM 인수로 처리됩니다. 기본값은 false입니다. |
      | batchType | 문자열 | 값을 PRINT, WEB 또는 WEB_AND_PRINT로 설정합니다. 기본값은 WEB_AND_PRINT입니다. |
      | 로케일 | 문자열 | 대화형 통신 출력 로케일을 지정합니다. 기본 서비스는 로케일 옵션을 사용하지 않지만 사용자 지정 서비스를 만들어 지역화된 대화형 통신을 생성할 수 있습니다. 기본값은 en_US입니다. |

   1. **[!UICONTROL 만들기]**&#x200B;를 누릅니다. 감시 폴더가 생성됩니다.
1. 감시 폴더를 사용하여 대화형 통신을 생성합니다.
   1. 감시 폴더를 엽니다. 입력 폴더로 이동합니다.
   1. 입력 폴더에 폴더를 만들고 새로 만든 폴더에 JSON 파일을 배치합니다.
   1. 감시 폴더가 파일을 처리할 때까지 기다립니다. 처리가 시작되면 파일이 포함된 입력 파일과 하위 폴더가 스테이징 폴더로 이동됩니다.
   1. 출력 폴더를 열어 출력을 봅니다.
      * [감시 폴더 구성]에서 [인쇄] 옵션을 지정하면 대화형 통신에 대한 PDF 출력이 생성됩니다.
      * [감시 폴더 구성]에서 [웹] 옵션을 지정하면 레코드당 JSON 파일이 생성됩니다. JSON 파일을 사용하여 [웹 템플릿](#web-template)을 미리 채울 수 있습니다.
      * [인쇄] 및 [웹] 옵션을 모두 지정하면 PDF 문서와 레코드당 JSON 파일이 모두 생성됩니다.

#### 외부 데이터 소스에 저장되고 양식 데이터 모델을 통해 액세스하는 입력 데이터를 사용하여 대화형 통신 {#use-fdm-as-data-source} 만들기

외부 데이터 소스에 저장된 데이터(레코드)를 대화형 통신 템플릿과 결합하여 대화형 통신을 생성합니다. 대화형 통신을 만들 때 FDM(양식 데이터 모델)을 통해 외부 데이터 소스에 연결하여 데이터에 액세스합니다. 외부 데이터 소스에서 동일한 양식 데이터 모델을 사용하여 데이터를 가져오도록 감시 폴더 일괄 처리 서비스를 구성할 수 있습니다. [외부 데이터 소스](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/work-with-form-data-model.html)에 저장된 레코드에서 대화형 통신을 만들려면:

1. 템플릿의 양식 데이터 모델을 구성합니다.
   1. 대화형 통신 템플릿과 연결된 양식 데이터 모델을 엽니다.
   1. 최상위 레벨 모델 객체를 선택하고 속성 편집을 누릅니다.
   1. 속성 편집 창의 읽기 서비스 필드에서 가져오기 또는 서비스 가져오기를 선택합니다.
   1. 읽기 서비스 인수의 연필 아이콘을 눌러 인수를 요청 속성에 바인딩하고 바인딩 값을 지정합니다. 서비스 인수를 지정된 바인딩 특성 또는 리터럴 값에 바인딩합니다. 이 값은 인수로 서비스에 전달되어 데이터 소스의 지정된 값과 관련된 세부 정보를 가져옵니다.

      <br>
        이 예에서 id 인수는 사용자 프로필의 id 속성 값을 가져와서 읽기 서비스에 인수로 전달합니다. 지정된 id에 대해 직원 데이터 모델 개체에서 연결된 속성의 값을 읽고 반환합니다. 따라서 양식의 id 필드에 00250을 지정하면 읽기 서비스는 00250 직원 id가 있는 직원의 세부 정보를 읽습니다.
        <br>

      ![요청 속성 구성](assets/request-attribute.png)

   1. 속성 및 양식 데이터 모델을 저장합니다.
1. 요청 속성에 대한 값 구성:
   1. 파일 시스템에 .json 파일을 만들고 편집을 위해 엽니다.
   1. JSON 배열을 만들고 양식 데이터 모델에서 데이터를 가져올 기본 속성을 지정합니다. 예를 들어 다음 JSON은 FDM에 id가 27126 또는 27127인 레코드의 데이터를 전송하도록 요청합니다.

      ```json
          [
              {
                  "id": 27126
              },
              {
                  "id": 27127
              }
          ]
      ```

   1. 파일을 저장하고 닫습니다.

1. [감시 폴더](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html)를 만들고 배치 API 서비스를 사용하도록 구성합니다.
   1. AEM Forms 작성자 인스턴스에 로그인합니다.
   1. **[!UICONTROL 도구]** > **[!UICONTROL Forms]** > **[!UICONTROL 감시 폴더 구성]**&#x200B;으로 이동합니다. **[!UICONTROL 새로 만들기]**&#x200B;를 누릅니다.
   1. 폴더의 **[!UICONTROL 이름]** 및 실제 **[!UICONTROL 경로]**&#x200B;를 지정합니다. 예, `c:\batchprocessing`.
   1. **[!UICONTROL 파일을 사용하여 처리]** 필드에서 **[!UICONTROL 서비스]** 옵션을 선택합니다.
   1. **[!UICONTROL 서비스 이름]** 필드에서 **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 서비스를 선택합니다.
   1. **[!UICONTROL 출력 파일 패턴]**&#x200B;을 지정합니다. 예를 들어 %F/ [패턴](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns)은 감시 폴더가 감시 폴더\input 폴더의 하위 폴더에서 입력 파일을 찾을 수 있도록 지정합니다.
1. 고급 매개 변수 구성:
   1. **[!UICONTROL 고급]** 탭을 열고 다음 사용자 지정 속성을 추가합니다.

      | 속성 | 유형 | 설명 |
      |--- |--- |--- |
      | templatePath | 문자열 | 사용할 대화형 통신 템플릿의 경로를 지정합니다. 예: /content/dam/formsanddocuments/tesample/mediumic. 필수 속성입니다. |
      | recordPath | 문자열 | recordPath 필드의 값은 대화형 통신 이름을 설정하는 데 도움이 됩니다. 레코드 필드의 경로를 recordPath 필드의 값으로 설정할 수 있습니다. 예를 들어 /employee/Id를 지정하면 id 필드의 값이 해당 대화형 통신에 대한 이름이 됩니다. 기본값은 임의 [임의 UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())입니다. |  |
      | usePrefillService | 부울 | 값을 True로 설정합니다. 기본값은 false입니다.  값이 true로 설정되면 일괄 처리 API는 구성된 양식 데이터 모델에서 데이터를 읽고 대화형 통신으로 채웁니다. usePrefillService를 true로 설정하면 입력 JSON 데이터(각 레코드에 대해)가 FDM 인수로 처리됩니다. |
      | batchType | 문자열 | 값을 PRINT, WEB 또는 WEB_AND_PRINT로 설정합니다. 기본값은 WEB_AND_PRINT입니다. |
      | 로케일 | 문자열 | 대화형 통신 출력 로케일을 지정합니다. 기본 서비스는 로케일 옵션을 사용하지 않지만 사용자 지정 서비스를 만들어 지역화된 대화형 통신을 생성할 수 있습니다. 기본값은 en_US입니다. |

   1. **[!UICONTROL 만들기]**&#x200B;를 누릅니다. 감시 폴더가 생성됩니다.
1. 감시 폴더를 사용하여 대화형 통신을 생성합니다.
   1. 감시 폴더를 엽니다. 입력 폴더로 이동합니다.
   1. 입력 폴더에 폴더를 만듭니다. 2단계에서 만든 JSON 파일을 새로 만든 폴더에 배치합니다.
   1. 감시 폴더가 파일을 처리할 때까지 기다립니다. 처리가 시작되면 파일이 포함된 입력 파일과 하위 폴더가 스테이징 폴더로 이동됩니다.
   1. 출력 폴더를 열어 출력을 봅니다.
      * [감시 폴더 구성]에서 [인쇄] 옵션을 지정하면 대화형 통신에 대한 PDF 출력이 생성됩니다.
      * [감시 폴더 구성]에서 [웹] 옵션을 지정하면 레코드당 JSON 파일이 생성됩니다. JSON 파일을 사용하여 [웹 템플릿](#web-template)을 미리 채울 수 있습니다.
      * [인쇄] 및 [웹] 옵션을 모두 지정하면 PDF 문서와 레코드당 JSON 파일이 모두 생성됩니다.

## REST 요청을 사용하여 일괄 처리 API 호출

REST(Representational State Transfer) 요청을 통해 [일괄 API](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html)를 호출할 수 있습니다. 이를 통해 다른 사용자에게 REST 끝점을 제공하여 API에 액세스하고 대화형 통신을 처리, 저장 및 사용자 지정하기 위한 자신만의 방법을 구성할 수 있습니다. 고유한 사용자 지정 Java 서블릿을 개발하여 AEM 인스턴스에 API를 배포할 수 있습니다.

Java 서블릿을 배포하기 전에 인터랙티브한 커뮤니케이션과 해당 데이터 파일이 준비되었는지 확인합니다. Java 서블릿을 만들고 배포하려면 다음 단계를 수행합니다.

1. AEM 인스턴스에 로그인하고 대화형 통신을 만듭니다. 아래 제공된 샘플 코드에 언급된 대화형 통신을 사용하려면 [여기](assets/SimpleMediumIC.zip)를 클릭하십시오.
1. [AEM 인스턴스에서 Apache Mavenon을 사용하여 AEM ](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) 프로젝트를 빌드하고 배포합니다.
1. AEM 프로젝트의 POM 파일 종속성 목록에 [AEM Forms Client SDK 버전 6.0.12](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/) 이상을 추가합니다. 예,

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. Java 프로젝트를 열고 .java 파일을 만듭니다(예: CCMBatchServlet.java). 파일에 다음 코드를 추가합니다.

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import javax.servlet.Servlet;
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.fd.ccm.multichannel.batch.api.builder.BatchConfigBuilder;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
           import java.util.Date;
   
   
           @Component(service=Servlet.class,
           property={
                   "sling.servlet.methods=GET",
                   "sling.servlet.paths="+ "/bin/batchServlet"
           })
           public class CCMBatchServlet extends SlingAllMethodsServlet {
   
               @Reference
               private BatchGeneratorService batchGeneratorService;
               @Reference
               private BatchComponentBuilderFactory batchBuilderFactory;
               public void doGet(SlingHttpServletRequest req, SlingHttpServletResponse resp) {
                   try {
                       executeBatch(req,resp);
                   } catch (Exception e) {
                       e.printStackTrace();
                   }
               }
               private void executeBatch(SlingHttpServletRequest req, SlingHttpServletResponse resp) throws Exception {
                   int count = 0;
                   JSONArray inputJSONArray = new JSONArray();
                   String filePath = req.getParameter("filePath");
                   InputStream is = new FileInputStream(filePath);
                   String data = IOUtils.toString(is);
                   try {
                       // If input file is json object, then create json object and add in json array, if not then try for json array
                       JSONObject inputJSON = new JSONObject(data);
                       inputJSONArray.put(inputJSON);
                   } catch (Exception e) {
                       try {
                           // If input file is json array, then iterate and add all objects into inputJsonArray otherwise throw exception
                           JSONArray inputArray = new JSONArray(data);
                           for(int i=0;i<inputArray.length();i++) {
                               inputJSONArray.put(inputArray.getJSONObject(i));
                           }
                       } catch (Exception ex) {
                           throw new Exception("Invalid JSON Data. File name : " + filePath, ex);
                       }
                   }
                   BatchInput batchInput = batchBuilderFactory.getBatchInputBuilder().setData(inputJSONArray).setTemplatePath("/content/dam/formsanddocuments/[path of the interactive communcation]").build();
                   BatchConfig batchConfig = batchBuilderFactory.getBatchConfigBuilder().setBatchType(BatchType.WEB_AND_PRINT).build();
                   BatchResult batchResult = batchGeneratorService.generateBatch(batchInput, batchConfig);
                   List<RecordResult> recordList = batchResult.getRecordResults();
                   JSONObject result = new JSONObject();
                   for (RecordResult recordResult : recordList) {
                       String recordId = recordResult.getRecordID();
                       for (RenditionResult renditionResult : recordResult.getRenditionResults()) {
                           if (renditionResult.isRecordPassed()) {
                               InputStream output = renditionResult.getDocumentStream().getInputStream();
                               result.put(recordId +"_"+renditionResult.getContentType(), output);
   
                               Date date= new Date();
                               long time = date.getTime();
   
                               // Print output
                               if(getFileExtension(renditionResult.getContentType()).equalsIgnoreCase(".json")) {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               } else
                               {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               }
                           }
                       }
                   }
                   PrintWriter writer = resp.getWriter();
                   JSONObject resultObj = new JSONObject();
                   resultObj.put("result", result);
                   writer.write(resultObj.toString());
               }
   
   
               private static void copyInputStreamToFile(InputStream inputStream, File file)
                       throws IOException {
   
                       try (FileOutputStream outputStream = new FileOutputStream(file)) {
   
                           int read;
                           byte[] bytes = new byte[1024];
   
                           while ((read = inputStream.read(bytes)) != -1) {
                               outputStream.write(bytes, 0, read);
                           }
   
                       }
   
                   }
   
   
               private String getFileExtension(String contentType) {
                   if (contentType.endsWith(BatchConstants.JSON)) {
                       return ".json";
                   } else return ".pdf";
               }
   
   
           }
   ```

1. 위의 코드에서 템플릿 경로(setTemplatePath)를 템플릿 경로로 바꾸고 setBatchType API의 값을 설정합니다.
   * [인쇄] 옵션을 지정하면 대화형 통신에 대한 PDF 출력이 생성됩니다.
   * 웹 옵션을 지정하면 레코드당 JSON 파일이 생성됩니다. JSON 파일을 사용하여 [웹 템플릿](#web-template)을 미리 채울 수 있습니다.
   * [인쇄] 및 [웹] 옵션을 모두 지정하면 PDF 문서와 레코드당 JSON 파일이 모두 생성됩니다.

1. [업데이트된 코드를 AEM 인스턴스에 배포하려면 maven을 사용합니다](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven).
1. 일괄 처리 API를 호출하여 대화형 통신을 생성합니다. 일괄 처리 API는 레코드 수에 따라 PDF 및 .json 파일 스트림을 반환합니다. JSON 파일을 사용하여 [웹 템플릿](#web-template)을 미리 채울 수 있습니다. 위 코드를 사용하는 경우 API는 `http://localhost:4502/bin/batchServlet`에 배포됩니다. 이 코드는 PDF 및 JSON 파일의 스트림을 인쇄하고 반환합니다.

### 웹 템플릿 {#web-template} 사전 채우기

웹 채널을 렌더링하도록 batchType을 설정하면 API는 모든 데이터 레코드에 대한 JSON 파일을 생성합니다. 다음 구문을 사용하여 JSON 파일을 해당 웹 채널과 병합하여 대화형 통신을 생성할 수 있습니다.

**구문**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**예**
JSON 파일이 다음 위치에  `C:\batch\mergedJsonPath.json` 있고 아래 대화형 통신 템플릿을 사용하는 경우:  `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

그런 다음 게시 노드의 다음 URL에 대화형 커뮤니케이션의 웹 채널이 표시됩니다
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

파일 시스템에 데이터를 저장하는 것 외에도 JSON 파일을 CRX 저장소, 파일 시스템, 웹 서버에 저장하거나 OSGI 프리플라이트 서비스를 통해 데이터에 액세스할 수 있습니다. 다양한 프로토콜을 사용하여 데이터를 병합하는 구문은 다음과 같습니다.

* **CRX 프로토콜**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **파일 프로토콜**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **프리플라이트 서비스 프로토콜**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME은 OSGI 미리 채우기 서비스의 이름을 나타냅니다. 미리 채우기 서비스 만들기 및 실행을 참조하십시오.

   IDENTIFIER는 OSGI 프리플라이트 서비스에서 프리플라이트 데이터를 가져오는 데 필요한 메타데이터를 나타냅니다. 로그인한 사용자의 식별자는 사용할 수 있는 메타데이터의 예입니다.

* **HTTP 프로토콜**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>기본적으로 CRX 프로토콜만 활성화됩니다. 지원되는 다른 프로토콜을 활성화하려면 구성 관리자](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager)을(를) 사용하여 프리플라이트 서비스 구성을 참조하십시오.[
