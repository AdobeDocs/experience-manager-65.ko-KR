---
title: Reader 확장 프로그램 인증서 만료 및 영향
description: Reader 확장 프로그램 인증서 만료 및 영향
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '1088'
ht-degree: 100%

---


# Reader 확장 프로그램 인증서 만료 및 영향 {#expiration-of-reader-extensions-certificates-and-its-impact}

Adobe Managed Services 또는 On-premise Enterprise Base 라이선스를 보유한 AEM Forms(Adobe Experience Manager Forms) 고객은 Acrobat Reader DC 확장 프로그램 서비스를 사용할 수 있습니다. 이 서비스를 이용하면 조직에서 Acrobat Reader의 기능을 추가 사용 권한으로 확장하여 대화형 PDF 문서를 쉽게 공유할 수 있습니다. 이 서비스는 PDF 문서에 사용 권한을 추가하고 Adobe Acrobat Reader를 사용하여 PDF 문서를 열 때 사용할 수 없는 기능(예: 문서에 주석 추가, 양식 작성, 문서 저장)을 활성화합니다. 서드파티 사용자는 권한이 활성화된 문서를 사용하는 데 추가 소프트웨어나 플러그인이 필요하지 않습니다. 사용 권한이 추가된 PDF 문서를 권한이 활성화된 문서라고 합니다. Acrobat Reader에서 권한이 활성화된 PDF 문서를 여는 사용자는 해당 문서에 대해 활성화된 작업을 수행할 수 있습니다.

Adobe는 PKI(공개 키 인프라)를 활용하여 라이선스 및 기능 활성화에 사용할 디지털 인증서를 발급합니다. Adobe는 **Adobe Root CA** 인증서를 발급해 왔으나, 해당 인증서는 2023년 1월 7일에 만료됩니다. **Adobe Root CA**&#x200B;에서 발급된 프로덕션 인증서(구 인증서)를 사용하는 확장 PDF 문서는 인증서 만료의 영향을 받지 않습니다. 2023년 1월 7일 이전에 발급된 구 인증서를 사용하는 모든 Reader 확장 PDF 문서(고객이 다운로드한 문서 포함)는 적용된 모든 사용 권한과 함께 계속 정상적으로 작동하며 별도의 업데이트가 필요하지 않습니다.

새로운 인증 기관인 **Adobe Root CA G2**&#x200B;와 새로운 인증 기관을 기반으로 하는 인증서를 지금 사용할 수 있습니다. 2023년 1월 7일 또는 그 이전에 새 인증서(**Adobe Root CA G2** 기반 인증서)를 사용하여 Reader에서 새 PDF 문서를 확장하십시오.  Adobe 지원이나 [Adobe 라이선스 웹 사이트에서 새 인증서를 받을 수 있습니다](https://licensing.adobe.com/).

## 자주 묻는 질문

**질문: Adobe Root 인증서와 Acrobat Reader 확장 프로그램 인증서의 차이점은 무엇입니까? Adobe Root 인증서는 Acrobat Reader 확장 프로그램 인증서에 종속됩니까? 두 인증서 모두 2023년 1월에 만료됩니까?**

답변: Adobe Root CA는 Acrobat Reader 확장 프로그램 인증서를 발급하는 인증 기관입니다. 2023년 1월 7일이 되면 &#39;Adobe Root CA&#39;와 해당 기관에서 발급된 모든 인증서가 만료됩니다.

**질문: 이전에 Adobe에서 인증서 만료 및 PDF 문서 사용/열기에 대한 영향과 관련해 공지한 적이 있습니다. 해당 공지를 무시해도 됩니까?**

답변: 상황을 재평가한 결과, 2023년 1월 7일 이전에 구 &#39;Adobe Root CA&#39;에서 발급된 프로덕션 인증서를 사용하는 모든 PDF 확장 문서는 2023년 1월 7일 이후에도 별도의 변경 없이 계속 작동합니다. 이미 PDF 문서를 업데이트한 경우에도 사용 환경에는 변화가 없습니다.

**질문: 추가로 궁금한 점이 있으면 어디로 문의해야 합니까?**

답변: [Adobe 지원](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support)에 문의하거나 지원 티켓을 제출해 주십시오.

**질문: 2023년 1월 7일 이전에 인증서를 업데이트하지 않으면 어떻게 됩니까?**

답변: 2023년 1월 7일 이전에 구 &#39;Adobe Root CA&#39;에서 발급된 프로덕션 인증서를 사용하는 모든 확장 PDF 문서는 2023년 1월 7일 이후에도 별도의 변경 사항 없이 계속 작동합니다. 평가판 인증서를 사용하는 확장 PDF는 만료 일자가 지나면 작동하지 않습니다.

**질문: 새 인증서에 대한 설명이 기존 인증서에 대한 설명과 다릅니까?**

답변: 새로운 Acrobat Reader 확장 프로그램 인증서 설명에는 프로그램 이름으로 **G3-P24**&#x200B;가 명시되어 있습니다. 구 인증서(&#39;Adobe Root CA&#39; 기반 인증서) 설명에는 프로그램 이름으로 **P24**&#x200B;가 명시되어 있습니다.

**질문: 최신 인증서를 받으려면 어떻게 해야 합니까?**

답변: 권한이 있는 모든 Forms 고객(활성 라이선스 보유)은 [Adobe 라이선스 웹 사이트](https://licensing.adobe.com/)에서 새 인증서(&#39;Adobe Root CA G2&#39; 기반 인증서)를 다운로드할 수 있습니다. Adobe 라이선스 웹 사이트에서 해당 인증서를 찾을 수 없는 경우 [Adobe 지원](https://experienceleague.adobe.com/?support-solution=Experience+Manager&lang=en#support)에 문의하거나 지원 티켓을 제출해 주십시오.

**질문: &#39;Adobe Root CA&#39;(구 인증 기관)에서 발급된 인증서를 사용하는 확장 PDF 문서는 2023년 1월 7일 이후에도 계속 작동합니까?**

답변: 예, 2023년 1월 7일 이전에 &#39;Adobe Root CA&#39;(구 인증 기관)에서 발급된 프로덕션 인증서를 사용하는 모든 확장 PDF 문서는 2023년 1월 7일 이후에도 별도의 변경 사항 없이 계속 작동합니다. 평가판 인증서를 사용하는 확장 PDF 문서는 만료 일자가 지나면 더 이상 작동하지 않습니다.

**질문: &#39;Adobe Root CA&#39;(기존 인증 기관)에서 발급된 인증서를 사용하는 확장 PDF 문서를 계속 사용하려면 어떤 버전의 Adobe Acrobat Reader가 필요합니까?**

답변: &#39;Adobe Root CA&#39;(구 인증 기관) 기반의 확장 PDF 문서를 사용하려면 Adobe Acrobat Reader 2020 이상이 필요합니다. 본 문서의 게시 시점을 기준으로 지원되는 Acrobat Reader 버전입니다. [지원되지 않는 Adobe Acrobat 버전](https://helpx.adobe.com/kr/support/programs/eol-matrix.html)을 사용 중이라면 [최신 버전의 Adobe Acrobat Reader를 다운로드하고 설치](https://get.adobe.com/reader/)하는 것이 좋습니다.

**질문: &#39;Adobe Root CA 2&#39;(새 인증 기관)에서 발급된 인증서를 사용하는 확장 PDF 문서를 계속 사용하려면 어떤 버전의 Adobe Acrobat Reader가 필요합니까?**

답변: &#39;Adobe Root CA 2&#39;(새 인증 기관) 기반의 확장 PDF 문서를 사용하려면 Adobe Acrobat Reader 2020 이상이 필요합니다. [지원되지 않는 Adobe Acrobat Reader 버전](https://helpx.adobe.com/kr/support/programs/eol-matrix.html)을 사용 중이라면 [최신 버전의 Adobe Acrobat Reader를 다운로드하고 설치](https://get.adobe.com/reader/)하는 것이 좋습니다.

**질문: 기존 별칭을 계속 사용하면서 기존 Acrobat Reader 확장 프로그램 인증서를 삭제하고 Adobe Experience Manager Forms 서버에 새 인증서를 추가할 수 있습니까?**

답변: 예, 기존 Acrobat Reader 확장 프로그램 인증서를 삭제하고 기존 별칭을 사용하여 새 인증서를 Adobe Experience Manager Forms 서버에 추가할 수 있습니다.

**질문: Adobe Experience Manager Forms 서버에서 새로운 Acrobat Reader 확장 프로그램 인증서와 기존 Acrobat Reader 확장 프로그램 인증서를 모두 보관할 수 있습니까?**

답변: 예, 두 인증서를 모두 Adobe Experience Manager Forms 서버에 보관할 수 있지만, 다른 별칭을 사용해야 합니다. 2023년 1월 7일 이후에는 새 인증서만 사용하여 Reader에서 PDF 문서를 확장할 수 있습니다.

**질문: 동일한 Acrobat Reader 확장 프로그램 인증서를 모든 Adobe Experience Manager Forms 환경으로 가져올 수 있습니까?**

답변: 예, 동일한 Acrobat Reader 확장 프로그램 인증서를 여러 환경에서 사용할 수 있습니다.

**질문: PDF 문서에 적용된 사용 권한을 어떻게 확인할 수 있습니까?**

답변: [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=ko#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API를 사용하여 PDF 문서에 적용된 사용 권한에 대한 정보를 가져올 수 있습니다.

**질문: Acrobat Reader 확장 프로그램 인증서 파일의 암호를 변경하려면 어떻게 해야 합니까?**

답변: Microsoft Windows에서 인증서 암호를 변경하려면 MMC(Microsoft Management Console)를 사용하여 인증서를 설치하고 **키를 내보낼 수 있음으로 표시**&#x200B;를 선택합니다. 설치가 완료되면 개인 키와 함께 인증서를 내보내고 PFX 파일에 다른 암호를 사용합니다.


<!-- 
## Applying the certificates {#obtaning-and-applying-the-certificates} 

You can choose one of the following paths to apply latest certificates:

* [Updating certificates for an AEM Forms on JEE environment](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment) 
* [Updating certificates for an AEM Forms on OSGi environment](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>The document uses the term certificates and credentials interchangeably.

### Pre-requisites {#Pre-requisites}

Updating the certificates requires using actions available on AEM Forms administrator console and Reader Extension APIs provided by AEM Forms. The document is intended for users and administrators with knowledge of using Adobe Experience Manger Forms APIs. Before you start, ensure that: 

* the user has administrator rights on underlying AEM Forms environment. 
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) and has access to it.
* [obtain the certificates](#obtain-the-certificates).


### Obtain the certificates {#obtain-the-certificates}

The Rights credential is delivered as a digital certificate that contains the public key, the private key, and the password used to access the credential.

If your organization purchases a production version of Reader Extensions, the production Rights credential is delivered by Adobe Licensing Website (LWS). A production Rights credential is unique to your organization and can enable the specific usage rights that you require.

If you obtained Reader Extensions through a partner or software provider who integrated Reader Extensions into their software, the Rights credential is provided to you by that partner who, in turn, receives this credential from Adobe.

>[!NOTE]
>
>The Rights credential cannot be used for typical document signing or assertion of identity. For these applications, you can use a self-sign certificate or acquire an identity certificate from a Certificate Authority (CA).

The following types of Rights credentials are available:

**Customer Evaluation**: A credential with a short validity period that is provided to customers who want to evaluate Reader Extensions. Usage rights applied to documents using this credential expire when the credential expires. This type of credential is valid only for two to three months.

**Production**: A credential with a long validity period that is provided to customers who purchased the full product. Production credentials are unique to each customer but can be installed on multiple systems.

If you have already used certificates to reader extend PDF files, download a production certificate from [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

### Applying certificates for an AEM Forms on JEE environment {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment} 

Applying new certificates on AEM Forms on JEE stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import and configure credentials 

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. Designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

* If you import a Reader Extensions credential and the Trust Store contains no other Reader Extensions credentials, it is set as the default.
* If you import a Reader Extensions credential with the Default option selected, the default type is removed from an existing default credential. The imported credential becomes the default.
* You cannot delete a default Reader Extensions credential. To delete the default credential, first set another credential as the default. An exception to this rule is that if there is only one credential, you can delete it even though it is the default.
* You cannot update a default Reader Extensions credential.

To import the credentials: 

1. In administration console, click Settings > Trust Store Management > Local Credentials.
1. Click Import and, under Trust Store Type, select Acrobat Reader DC extensions Credential.
1. (Optional) To indicate that this credential is the default credential to use with Acrobat Reader DC extensions, select Default.
1. In the Alias box, type an identifier for the credential. This identifier is used as the display name for the credential in Acrobat Reader DC extensions. This alias is also used to access the credential programmatically using the AEM forms SDK.
1. Click Choose File to locate the credential, type the password of the credential, and then click OK.

If the error message "Failed to import credential due to either incorrect file format, or incorrect password" appears, verify that the password is valid.

You can also import and delete credentials programmatically. (See [Programming with AEM forms](../../developing/credentials.md).)

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. AEM Forms on JEE provides APIs to remove usage rights. For detailed instructions, see [Removing Usage Rights from PDF Documents](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

To remove usage rights for AEM Forms on JEE processes developed in Workbench, see [Workbench Help](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf). 

#### Apply the usage rights to PDF documents 

After importing new credentials, you can apply usage rights to PDF documents using the Acrobat Reader DC extensions Java Client API and web service.  For details, see [Applying Usage Rights to PDF Documents](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents). 


### Applying certificates for an AEM Forms on OSGi environment {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Applying new certificates on AEM Forms on OSGi stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import credentials {#Import-credentials}

In an AEM Forms on OSGi environment, a Reader Extension credential is associated with fd-service user. Before adding credentials for fd-user key store, perform the following steps to create a key store: 

1. Log in to your AEM Author instance as an Administrator.
1. Go to **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Scroll down the list of users until you find fd-service user account.
1. Click **[!UICONTROL fd-service]** user.
1. Click keystore tab.
1. Click **[!UICONTROL Create KeyStore]**.
1. Set the KeyStore Access Password and save your settings to create the KeyStore password.

After creating the key-store, add credentials to fd-service user. The following video explains the steps: 

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

The following command list the details of the pfx file. Before running the command, navigate to the directory that contains the .pfx file.

`keytool -v -list -storetype pkcs12 -keystore [name of your .pfx file]`

For example, keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
