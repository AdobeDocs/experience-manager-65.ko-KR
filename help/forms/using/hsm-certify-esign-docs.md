---
title: HSM을 사용하여 문서에 디지털 서명 또는 인증
seo-title: HSM을 사용하여 e서명 문서 인증
description: HSM 또는 전자 서명 디바이스를 사용하여 e서명 문서 인증
seo-description: HSM 또는 전자 서명 디바이스를 사용하여 e서명 문서 인증
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---


# HSM을 사용하여 문서 {#use-hsm-to-digitally-sign-or-certify-documents} 디지털 서명 또는 인증

HSM(Hardware Security Module) 및 에셋은 디지털 키를 안전하게 관리, 처리 및 저장하도록 설계된 전용, 고정 및 변조 방지 컴퓨팅 디바이스입니다. 이러한 장치는 컴퓨터나 네트워크 서버에 직접 연결됩니다.

Adobe Experience Manager Forms은 HSM 또는 eSign에 저장된 자격 증명을 사용하거나 문서에 서버측 디지털 서명을 적용할 수 있습니다. AEM Forms에서 HSM 또는 토큰 디바이스를 사용하려면

1. DocAssurance 서비스를 활성화합니다.
1. Reader 확장을 위한 인증서를 설정합니다.
1. AEM Web Console에서 HSM 또는 토큰 디바이스에 대한 별칭을 생성합니다.
1. DocAssurance 서비스 API를 사용하여 장치에 저장된 디지털 키로 문서에 서명하거나 인증합니다.

## AEM Forms {#configurehsmetoken}을 사용하여 HSM 또는 토큰 디바이스를 구성하기 전에

* [AEM Forms add-on](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 패키지를 설치합니다.
* AEM 서버와 동일한 컴퓨터에 HSM 또는 토큰 클라이언트 소프트웨어를 설치하고 구성합니다. 클라이언트 소프트웨어는 HSM 및 토큰 디바이스와 통신해야 합니다.
* (Microsoft Windows 전용) JAVA_HOME_32 환경 변수를 설정하여 32비트 버전의 JDK 8 Development Kit(Java 8 Development Kit)가 설치된 디렉토리를 가리킵니다. 디렉토리의 기본 경로는 C:\Program Files(x86)\Java\jdk&lt;version>입니다.
* (OSGi에만 해당) 신뢰 저장소에 루트 인증서를 설치합니다. 서명된 PDF를 확인하는 데 필요합니다.

>[!NOTE]
>
>Microsoft Windows의 경우 32비트 LunaSA 또는 ETken 클라이언트만 지원됩니다.

## DocAssurance 서비스 {#configuredocassurance} 활성화

기본적으로 DocAssurance 서비스는 활성화되지 않습니다. 서비스를 활성화하려면 다음 단계를 수행합니다.

1. AEM Forms 환경의 작성자 인스턴스를 중지합니다.

1. 편집을 위해 [AEM_root]\crx-quickstart\conf\sling.properties 파일을 엽니다.

   >[!NOTE]
   >
   >AEM 인스턴스를 시작하기 위해 [AEM_root]\crx-quickstart\bin\start.bat 파일을 사용한 경우 편집을 위해 [AEM_root]\crx-quickstart\sling.properties 파일을 엽니다.

1. sling.properties 파일에 다음 속성을 추가하거나 바꿉니다.

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. sling.properties 파일을 저장하고 닫습니다.
1. AEM 인스턴스를 다시 시작합니다.

## Reader 확장 {#set-up-certificates-for-reader-extensions}에 대한 인증서 설정

인증서를 설정하려면 다음 단계를 수행합니다.

1. AEM 작성자 인스턴스에 관리자로 로그인합니다.

1. 전역 탐색 막대에서 **Adobe Experience Manager**&#x200B;을 클릭합니다. **도구** > **보안** > **사용자**&#x200B;로 이동합니다.
1. 사용자 계정의 **이름** 필드를 클릭합니다. **사용자 설정 편집** 페이지가 열립니다.
1. AEM 작성자 인스턴스에서 인증서는 KeyStore에 상주합니다. 이전에 KeyStore를 만들지 않은 경우 **Create KeyStore**&#x200B;를 클릭하고 KeyStore에 대한 새 암호를 설정합니다. 서버에 이미 KeyStore가 포함되어 있으면 이 단계를 건너뜁니다.

1. **사용자 설정 편집** 페이지에서 **키 저장소 관리**&#x200B;를 클릭합니다.

1. KeyStore 관리 대화 상자에서 키 저장소 파일&#x200B;**옵션에서**&#x200B;개인 키 추가 옵션을 확장하고 별칭을 제공합니다. 별칭은 Reader 확장 작업을 수행하는 데 사용됩니다.
1. 인증서 파일을 업로드하려면 **키 저장소 파일 선택**&#x200B;을 클릭하고 `.pfx` 파일을 업로드합니다.
1. 각각의 필드에 인증서에 연결된 **키 저장소 암호**,**개인 키 암호** 및 **개인 키 별칭**&#x200B;을 추가합니다. **제출**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >인증서의 P **개인 키 별칭**&#x200B;을(를) 확인하려면 Java 키 도구 명령을 사용합니다.`keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >**키 저장소 암호** 및 **개인 키 암호** 필드에서 인증서 파일과 함께 제공된 암호를 지정합니다.

>[!NOTE]
>
>OSGi의 AEM Forms에서 서명된 PDF를 확인하려면 Trust Store에 설치된 루트 인증서를 확인합니다.

>[!NOTE]
>
>프로덕션 환경으로 이동할 때 평가 자격 증명을 프로덕션 자격 증명으로 바꿉니다. 만료되거나 평가 자격 증명을 업데이트하기 전에 이전 Reader 확장 자격 증명을 삭제해야 합니다.

## {#configuredeviceinaemconsole} 장치의 별칭 만들기

별칭에는 HSM 또는 프로토콜에 필요한 모든 매개 변수가 포함되어 있습니다. eSign 또는 Digital Signatures에서 사용하는 각 HSM 또는 전자 인증 자격 증명을 위한 별칭을 만들려면 아래 지침을 수행하십시오.

1. AEM 콘솔을 엽니다. AEM 콘솔의 기본 URL은 https://&lt;host>:&lt;port>/system/console/configMgr입니다.
1. **HSM 자격 증명 구성 서비스**&#x200B;를 열고 다음 필드에 값을 지정합니다.

   * **자격 증명 별칭**:별칭을 식별하는 데 사용되는 문자열을 지정합니다. 이 값은 서명 필드 작업과 같은 일부 디지털 서명 작업의 속성으로 사용됩니다.
   * **DLL 경로**:서버에 있는 HSM 또는 전자 토큰 클라이언트 라이브러리의 정규화된 경로를 지정합니다. 예: C:\Program Files\LunaSA\cryptoki.dll. 클러스터 환경에서는 이 경로가 클러스터의 모든 서버와 동일해야 합니다.
   * **HSM Pin**:장치 키에 액세스하는 데 필요한 암호를 지정합니다.
   * **HSM 슬롯 ID**:정수 유형의 슬롯 식별자를 지정합니다. 슬롯 ID는 클라이언트별로 설정됩니다. 다른 파티션(예: 동일한 HSM 장치의 HSMPART2)에 두 번째 시스템을 등록하는 경우 슬롯 1은 클라이언트에 대한 HSMPART2 파티션과 연결됩니다.

   >[!NOTE]
   >
   >Etken을 구성하는 동안 HSM 슬롯 ID 필드에 숫자 값을 지정합니다. 서명 작업이 작동하도록 하려면 숫자 값이 필요합니다.

   * **인증서 SHA1**:사용 중인 자격 증명을 위한 공개 키(.cer) 파일의 SHA1 값(지문)을 지정하십시오. SHA1 값에 사용된 공백이 없는지 확인합니다. 실제 인증서를 사용하는 경우에는 필요하지 않습니다.
   * **HSM 디바이스 유형**:HSM(Luna 또는 기타) 또는 eToken 장치의 제조업체를 선택합니다.

   **저장**&#x200B;을 클릭합니다. 하드웨어 보안 모듈은 AEM Forms용으로 구성됩니다. 이제 AEM Forms에서 하드웨어 보안 모듈을 사용하여 문서에 서명하거나 인증할 수 있습니다.

## DocAssurance 서비스 API를 사용하여 장치에 저장된 디지털 키로 문서에 서명하거나 인증합니다.  {#programatically}

다음 샘플 코드에서는 HSM 또는 전자 필기장을 사용하여 문서에 서명하거나 인증할 수 있습니다.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
  }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

AEM 6.0 Form 또는 AEM 6.1 Forms에서 업그레이드했고 이전 버전에서 DocAssurance 서비스를 사용했다면 다음을 수행합니다.

* HSM 또는 토큰 디바이스 없이 DocAssurance 서비스를 사용하려면 기존 코드를 계속 사용하십시오.
* DocAssurance 서비스를 HSM 또는 토큰 디바이스와 함께 사용하려면 기존 CredentialContext 개체 코드를 아래 나열된 API로 바꾸십시오.

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

DocAssurance 서비스의 API 및 샘플 코드에 대한 자세한 내용은 [프로그래밍 방식으로 AEM Document Services 사용](/help/forms/using/aem-document-services-programmatically.md)을 참조하십시오.
