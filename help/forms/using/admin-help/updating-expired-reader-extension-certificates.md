---
title: Reader 확장 인증서 만료 및 영향
description: Reader 확장 인증서 만료 및 영향
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---


# Reader 확장 인증서 만료 및 영향 {#expiration-of-reader-extensions-certificates-and-its-impact}

Adobe Managed Services 또는 온프레미스 엔터프라이즈 베이스 라이선스가 있는 Adobe Experience Manager Forms(AEM Forms) 고객은 Acrobat Reader DC 확장 서비스를 사용할 수 있습니다. 이 서비스를 통해 조직은 추가적인 사용 권한과 함께 Acrobat Reader의 기능을 확장하여 대화형 PDF 문서를 쉽게 공유할 수 있습니다. 이 서비스는 PDF 문서에 사용 권한을 추가하고, Adobe Acrobat Reader을 사용하여 PDF 문서를 열 때 사용할 수 없는 기능(문서에 주석 추가, 양식 채우기, 문서 저장 등)을 활성화합니다. 서드파티 사용자는 권한이 활성화된 문서에서 작동하는 데 추가 소프트웨어나 플러그인이 필요하지 않습니다. 사용 권한이 추가된 PDF 문서를 권한 사용 문서라고 합니다. Acrobat Reader에서 권한이 활성화된 PDF 문서를 여는 사용자는 해당 문서에 대해 활성화된 작업을 수행할 수 있습니다.

Adobe은 PKI(공개 키 인프라)를 사용하여 라이선싱 및 기능 활성화에 사용할 디지털 인증서를 발행합니다. Adobe이 인증 기관 **Adobe 루트 CA**&#x200B;에서 인증서를 발급하고 있습니다. 이 인증서는 2023년 1월 7일에 만료되도록 설정되어 있습니다. 인증서 만료는 **Adobe 루트 CA** 기반 인증서(이전 인증서)에서 발급된 프로덕션 인증서를 사용하여 확장된 PDF 문서에는 영향을 주지 않습니다. 2023년 1월 7일 이전에 이전 인증서를 사용하여 확장된 모든 PDF 문서 및 고객이 다운로드한 문서를 포함하여 Reader은 적용되는 모든 사용 권한으로 계속 작동하며 업데이트가 필요하지 않습니다.

이제 새 인증 기관, **Adobe 루트 CA G2** 및 새 인증 기관을 기반으로 하는 인증서를 사용할 수 있습니다. 2023년 1월 7일 또는 그 이전에 **Adobe 루트 CA G2**&#x200B;를 기반으로 하는 새 인증서를 사용하여 새 PDF 문서를 Reader 확장하십시오.  [Adobe 라이선스 웹 사이트](https://licensing.adobe.com/) 또는 Adobe 지원에서 새 인증서를 얻을 수 있습니다.

## 자주 묻는 질문

**Q. Adobe 루트 인증서와 Acrobat Reader 확장 인증서 간의 차이점은 무엇입니까? Adobe 루트 인증서가 Acrobat Reader 확장 인증서에 종속됩니까? 이 두 인증서가 모두 2023년 1월에 만료됩니까?**

A. Adobe 루트 CA는 Acrobat Reader 확장 인증서를 발급하는 인증 기관입니다. 2023년 1월 7일, &quot;Adobe 루트 CA&quot; 및 그로부터 발행된 모든 인증서가 만료됩니다.

**Q. 인증서 만료, PDF 문서 사용/열기에 미치는 영향 등에 대해 이전 Adobe에서 설명한 내용이 있습니다. 해당 커뮤니케이션을 무시해야 합니까?**

A. 상황 재평가에 따라 2023년 1월 7일 이전에 구 &quot;Adobe 루트 CA&quot;에서 발급한 생산 인증서를 사용하여 확장된 모든 PDF 문서는 2023년 1월 7일 이후에도 변경 없이 계속 작동합니다. PDF 문서를 이미 업데이트했다면 경험에는 변경 사항이 없습니다.

**Q. 추가 질문이 있는 경우 누구에게 문의해야 합니까?**

A. [Adobe 지원](https://experienceleague.adobe.com/ko?support-solution=Experience+Manager#support)에 문의하거나 지원 티켓을 올릴 수 있습니다.

**Q. 2023년 1월 7일 이전에 인증서를 업데이트하지 않으면 어떻게 됩니까?**

A. 2023년 1월 7일 이전에 기존 &#39;Adobe 루트 CA&#39;에서 발급한 프로덕션 인증서를 사용하여 확장된 모든 PDF 문서는 2023년 1월 7일 이후에도 변경 없이 계속 작동합니다. 평가 인증서로 확장된 PDF은 만료일 이후 작동하지 않습니다.

**Q. 새 인증서에 대한 설명이 이전 인증서와 다릅니까?**

A. 새 Acrobat Reader 확장 인증서에 대한 설명에 프로그램 이름으로 **G3-P24**&#x200B;이(가) 언급되어 있습니다. 이전 인증서(&quot;Adobe 루트 CA&quot;를 기반으로 한 인증서)에 대한 설명에서 **P24**&#x200B;이(가) 프로그램 이름으로 언급되어 있습니다.

**Q. 최신 인증서를 얻는 방법은 무엇입니까?**

A. 자격이 있는 모든 Forms 고객(활성 라이선스가 있음)은 [Adobe 라이선스 웹 사이트](https://licensing.adobe.com/)에서 새 인증서(&quot;Adobe 루트 CA G2&quot;를 기반으로 하는 인증서)를 다운로드할 수 있습니다. Adobe 라이선스 웹 사이트에서 인증서를 찾을 수 없는 경우 [Adobe 지원](https://experienceleague.adobe.com/ko?support-solution=Experience+Manager&amp;lang=en#support)에 문의하거나 지원 티켓을 받으십시오.

**Q. &quot;Adobe 루트 CA&quot;(이전 인증 기관)에서 발급한 인증서를 사용하여 확장된 PDF 문서가 2023년 1월 7일 이후에도 계속 작동합니까?**

A. 예. 2023년 1월 7일 이전에 &quot;Adobe 루트 CA&quot;(이전 인증 기관)에서 발급한 프로덕션 인증서를 사용하여 확장된 모든 PDF 문서는 2023년 1월 7일 이후에도 변경 없이 계속 작동합니다. 평가 인증서로 확장된 PDF 문서가 만료 날짜 이후에 작동하지 않습니다.

**Q. &quot;Adobe 루트 CA&quot;(이전 인증 기관)에서 발급한 인증서로 확장된 PDF 문서를 계속 사용하려면 어떤 Adobe Acrobat Reader 버전이 필요합니까?**

A. Adobe Acrobat Reader 2020 이상 버전은 &quot;Adobe 루트 CA&quot;(이전 인증 기관)로 확장된 PDF 문서를 사용해야 합니다. 이 문서를 게시할 때 지원되는 Acrobat Reader 버전입니다. [지원되지 않는 버전의 Adobe Acrobat Adobe](https://helpx.adobe.com/kr/support/programs/eol-matrix.html)을(를) 사용하는 경우 [최신 버전의 Adobe Acrobat Reader을 다운로드하여 설치](https://get.adobe.com/reader/)하는 것이 좋습니다.

**Q. &quot;Adobe 루트 CA 2&quot;(새 인증 기관)에서 발급한 인증서로 확장된 PDF 문서를 계속 사용하려면 어떤 Adobe Acrobat Reader 버전이 필요합니까?**

A. &quot;Adobe 루트 CA 2&quot;(새 인증 기관)를 사용하여 확장된 PDF 문서를 사용하려면 Adobe Acrobat Reader 2020 이상이 필요합니다. [지원되지 않는 버전의 Adobe Acrobat Reader Adobe](https://helpx.adobe.com/kr/support/programs/eol-matrix.html)을(를) 사용하는 경우 [최신 버전의 Adobe Acrobat Reader을 다운로드하여 설치](https://get.adobe.com/reader/)하는 것이 좋습니다.

**Q. 기존 별칭을 계속 사용하면서 이전 Acrobat Reader 확장 인증서를 삭제하고 Adobe Experience Manager Forms 서버에 새 인증서를 추가할 수 있습니까?**

A. 예. 이전 Acrobat Reader 확장 인증서를 삭제하고 기존 별칭이 있는 새 인증서를 Adobe Experience Manager Forms 서버에 추가할 수 있습니다.

**Q. Adobe Experience Manager Forms Server에 새 Acrobat Reader 확장 인증서와 이전 확장 인증서를 모두 유지할 수 있습니까?**

A. 예. 두 인증서를 모두 유지할 수 있지만 Adobe Experience Manager Forms 서버에 서로 다른 별칭을 사용할 수 있습니다. Post 2023년 1월 7일에는 새 인증서만 사용하여 PDF 문서를 Reader 확장할 수 있습니다.

**Q. 모든 Adobe Experience Manager Forms 환경에 동일한 Acrobat Reader 확장 인증서를 가져올 수 있습니까?**

A. 예. 동일한 Acrobat Reader 확장 인증서를 여러 환경에서 사용할 수 있습니다.

**Q. PDF 문서에 적용된 사용 권한을 확인하려면 어떻게 해야 합니까?**

A. [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=ko#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API를 사용하여 PDF 문서에 적용된 사용 권한에 대한 정보를 검색할 수 있습니다.

**Q. Acrobat Reader 확장 인증서 파일의 암호를 변경하려면 어떻게 해야 합니까?**

A. Microsoft Windows에서 인증서 암호를 변경하려면 MMC(Microsoft 관리 콘솔)를 사용하여 인증서를 설치하고 **키를 내보낼 수 있도록 표시**&#x200B;를 선택합니다. 설치 후 개인 키로 인증서를 내보내고 PFX 파일에 다른 암호를 사용합니다.


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
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html?lang=ko) and has access to it.
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

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html?lang=ko).  -->
