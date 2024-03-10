---
title: PDF 서비스 Java&trade 변환, API 빠른 시작(SOAP)
description: PDF 변환 서비스에서 PDF 문서를 PostScript 또는 이미지 파일(JPEG, JPEG 2000, PNG 및 TIFF)로 변환하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
exl-id: 8974c468-ff2b-431d-96fb-e987698619bc
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# PDF 서비스 Java™ API 빠른 시작(SOAP) 변환 {#convert-pdf-service-java-api-quickstart-soap}

PDF 서비스 API 변환에 사용할 수 있는 빠른 시작은 다음과 같습니다.

[빠른 시작(SOAP 모드): Java를 사용하여 PDF 문서를 PostScript로 변환](convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[빠른 시작(SOAP 모드): Java를 사용하여 PDF 문서를 JPEG 파일로 변환](convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드를 SOAP로 설정해야 합니다.

>[!NOTE]
>
>AEM Forms를 사용한 프로그래밍의 빠른 시작은 JBoss® Application Server 및 Microsoft® Windows 운영 체제에 배포되는 Forms 서버를 기반으로 합니다. 그러나 UNIX®와 같은 다른 운영 체제를 사용하는 경우에는 Windows 특정 경로를 해당 운영 체제에서 지원하는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. 다음을 참조하십시오 [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 빠른 시작(SOAP 모드): Java™ API를 사용하여 PDF 문서를 PostScript로 변환 {#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api}

다음 코드 예제에서는 이라는 PDF 문서를 *Loan.pdf* 을 호출한 PostScript 문서로 *Loan.ps*. (참조: [PDF 문서를 포스트스크립트로 변환](/help/forms/developing/converting-pdf-postscript-image-files.md#converting-pdf-documents-to-postscript).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-convertpdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.convertpdfservice.client.ConvertPdfServiceClient;
 import com.adobe.livecycle.convertpdfservice.client.ToPSOptionsSpec;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.Color;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.LineWeight;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.PSLevel;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.PageSize;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.Color;
 
 public class JavaAPIConvertPDFtoPSSOAP
 {
     public static void main(String[] args)
     {
     try
         {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a ConvertPdfServiceClient object
         ConvertPdfServiceClient convertPDFClient= new ConvertPdfServiceClient(myFactory);
 
         //Get a PDF file document to convert to a PS document
         //and populate a com.adobe.idp.Document object
         String inputFileName = "C:\\Adobe\Loan.pdf";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);
 
         //Create a ToPSOptionsSpec object that defines run-time options
         ToPSOptionsSpec psSpec = new ToPSOptionsSpec();
         psSpec.setPsLevel(PSLevel.LEVEL_3);
         psSpec.setShrinkToFit(true);
         psSpec.setPageSize(PageSize.A4);
         psSpec.setRotateAndCenter(true);
         psSpec.setColor(Color.compositeGray);
         psSpec.setLineWeight(LineWeight.point25);
 
         //Convert the PDF document to a PostScript file
         Document createdDocument =convertPDFClient.toPS2(
             inDoc,
             psSpec
             );
 
         //Save the PostScript file
         createdDocument.copyToFile(new File("C:\\Adobe\Loan.ps"));
         }
     catch (Exception e)
         {
             e.printStackTrace();
         }
     }
 }
```

## 빠른 시작(SOAP 모드): Java™ API를 사용하여 PDF 문서를 JPEG 파일로 변환 {#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api}

다음 Java™ 코드 예제는 이라는 PDF 문서를 변환합니다. *Loan.pdf* JPEG 파일 집합에 연결한 다음 C:\Adobe 디렉터리에 저장합니다. 각 파일의 이름은 다음과 같습니다 `tempFile[index].jpg`: 여기서 첫 번째 이미지 파일의 이름은 입니다 *tempFile0.jpg*. (참조: [PDF 문서를 이미지 형식으로 변환](/help/forms/developing/converting-pdf-postscript-image-files.md#converting-pdf-documents-to-image-formats).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-convertpdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Iterator;
 import java.util.List;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.convertpdfservice.client.ConvertPdfServiceClient;
 import com.adobe.livecycle.convertpdfservice.client.ToImageOptionsSpec;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.CMYKPolicy;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.ColorCompression;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.ColorSpace;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.GrayScaleCompression;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.GrayScalePolicy;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.ImageConvertFormat;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.Interlace;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.JPEGFormat;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.MonochromeCompression;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.PNGFilter;
 import com.adobe.livecycle.convertpdfservice.client.enumeration.RGBPolicy;
 
 public class JavaAPIConvertPDFtoImageSOAP {
 
     public static void main(String[] args)
     {
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create the ConvertPDF service client
         ConvertPdfServiceClient serviceClient = new ConvertPdfServiceClient(myFactory);
 
         //Get a PDF file document to convert to a JPEG document and populate a com.adobe.idp.Document object
         String inputFileName = "C:\\Adobe\Loan.pdf";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);
 
         // Set up the runtime options for the new JPEG file to be created
         ToImageOptionsSpec spec = new ToImageOptionsSpec();
         spec.setImageConvertFormat(ImageConvertFormat.JPEG);
         spec.setGrayScaleCompression(GrayScaleCompression.Low);
         spec.setColorCompression(ColorCompression.Low);
         spec.setFormat(JPEGFormat.BaselineOptimized);
         spec.setRgbPolicy(RGBPolicy.Off);
         spec.setCmykPolicy(CMYKPolicy.Off);
         spec.setColorSpace(ColorSpace.RGB);
         spec.setResolution("72");
         spec.setMonochrome(MonochromeCompression.None);
         spec.setFilter(PNGFilter.Sub);
         spec.setInterlace(Interlace.Adam7);
         spec.setTileSize(180);
         spec.setGrayScalePolicy(GrayScalePolicy.Off);
 
         //Perform the conversion and get the containing the newly created JPEG files
         List allImages = serviceClient.toImage2(
             inDoc,
             spec
         );
 
         //Create an Iterator object and iterate through
         //the List object to get all images
         Iterator iter = allImages.iterator();
         int i = 0 ;
         while (iter.hasNext()) {
             Document file = (Document)iter.next();
             file.copyToFile(new File("C:\\Adobe\tempFile"+i+".jpg"));
             i++;
         }
     }
     catch (Exception e) {
         e.printStackTrace();
         }
     }
 }
```
