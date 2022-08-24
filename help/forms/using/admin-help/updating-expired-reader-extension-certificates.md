---
title: 만료된 Reader 확장 서비스 인증서를 업데이트하는 중
description: Reader 확장 문서가 작동하지 않습니다. 인증서 업데이트
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---

# 만료된 Reader 확장 서비스 인증서를 업데이트하는 중 {#Updating-expired-Reader-Extension-service-certificates}

Adobe Managed Services 또는 온-프레미스 엔터프라이즈 기본 라이선스를 사용하는 Adobe Experience Manager Forms(AEM Forms) 고객은 Reader 확장 서비스를 사용할 수 있습니다. 이 서비스를 사용하면 조직에서 추가 사용 권한과 함께 Adobe Reader의 기능을 확장하여 대화형 PDF 문서를 쉽게 공유할 수 있습니다. 이 서비스는 PDF 문서에 사용 권한을 추가하고, 문서에 주석 추가, 양식 채우기, 문서 저장과 같이 Adobe Acrobat Reader DC을 사용하여 PDF 문서를 열 때 일반적으로 사용할 수 없는 기능을 활성화합니다. 타사 사용자는 권한이 활성화된 문서에서 작업할 추가 소프트웨어 또는 플러그인이 필요하지 않습니다. 사용 권한이 추가된 PDF 문서를 권한 사용 문서라고 합니다. Adobe Reader에서 권한이 활성화된 PDF 문서를 여는 사용자는 해당 문서에 대해 활성화된 작업을 수행할 수 있습니다.

Adobe은 PKI(공개 키 인프라)를 활용하여 라이센스 및 기능 활성화에서 사용할 디지털 인증서를 발행합니다. Adobe이 인증 기관 &quot;Adobe 루트 CA&quot;에 따라 인증서를 발급했으며, 2023년 1월 7일에 만료됩니다. 이 경우 이 인증 기관에서 발급한 모든 인증서가 만료됩니다. 인증서가 만료되면 인증서에 종속된 모든 기능이 더 이상 작동하지 않습니다. 예를 들어 Adobe Acrobat Reader을 사용하여 주석을 추가할 수 있는 리더 확장 PDF 문서는 2023년 1월 7일 이후 고객에 대해 작동하지 않습니다. 이 문제를 해결하려면 이전 인증서를 사용하여 Reader 확장 서비스 관리자가 새 Adobe 루트 CA G2에서 발행한 새 인증서를 가져와 해당 PDF 문서에 다시 적용해야 합니다(리더기는 새 인증서로 PDF 문서를 확장).

인증서 만료는 OSGi 스택에서 AEM Forms과 AEM Forms의 모두에 영향을 줍니다. 두 스택 모두 서로 다른 일련의 지침이 있습니다. 회의 후 [사전 요구 사항](#Pre-requisites) 및 [새 인증서 받기](#obtain-the-certificates)스택에 따라 다음 경로 중 하나를 선택합니다.

* [JEE 환경에서 AEM Forms용 인증서 업데이트](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment)
* [OSGi 환경에서 AEM Forms에 대한 인증서 업데이트](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>이 문서는 용어 인증서와 자격 증명을 서로 교환하여 사용합니다.

## 전제 조건 {#Pre-requisites}

인증서를 업데이트하려면 AEM Forms 관리자 콘솔에서 사용할 수 있는 작업 및 AEM Forms에서 제공하는 Reader 확장 API를 사용해야 합니다. 이 문서는 Adobe Experience Manager Forms API 사용에 대한 지식이 있는 사용자 및 관리자를 위한 것입니다. 시작하기 전에 다음을 확인하십시오.

* 사용자는 기본 AEM Forms 환경에 대한 관리자 권한이 있습니다.
* 사용자가 [개발 환경](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) 액세스할 수 있습니다.
* 인증서를 받습니다.

### 인증서 받기 {#obtain-the-certificates}

권한 자격 증명은 공개 키, 개인 키 및 자격 증명에 액세스하는 데 사용되는 암호를 포함하는 디지털 인증서로 전달됩니다.

조직에서 프로덕션 버전의 Reader 확장을 구매하는 경우 프로덕션 권한 자격 증명은 LWS(Domain Licensing Website)를 통해 전달됩니다. 프로덕션 권한 자격 증명은 조직에 고유하며 필요한 특정 사용 권한을 활성화할 수 있습니다.

Reader 확장을 해당 소프트웨어에 통합한 파트너 또는 소프트웨어 공급자를 통해 Reader 확장을 가져온 경우 권한 자격 증명은 해당 파트너가 제공하며, 이 자격 증명은 Adobe에서 이 자격 증명을 받습니다.

>[!NOTE]
>
>권한 자격 증명은 일반적인 문서 서명 또는 ID 검증에 사용할 수 없습니다. 이러한 응용 프로그램의 경우 자체 서명 인증서를 사용하거나 CA(인증 기관)에서 ID 인증서를 얻을 수 있습니다.

다음 유형의 권한 자격 증명을 사용할 수 있습니다.

**고객 평가**: Reader 확장을 평가하려는 고객에게 제공되는 짧은 유효 기간이 있는 자격 증명입니다. 이 자격 증명을 사용하여 문서에 적용된 사용 권한은 자격 증명이 만료되면 만료됩니다. 이 유형의 자격 증명은 2-3개월 동안만 유효합니다.

**프로덕션**: 전체 제품을 구입한 고객에게 제공되는 유효 기간이 긴 자격 증명입니다. 프로덕션 자격 증명은 각 고객마다 고유하지만 여러 시스템에 설치할 수 있습니다.

PDF 파일을 읽는 데 이미 인증서를 사용한 경우 프로덕션 인증서를 [LWS(Adobe 라이선스 웹 사이트)](https://licensing.adobe.com/).

## JEE 환경에서 AEM Forms에 대한 인증서 업데이트 및 적용 {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

JEE 스택의 AEM Forms에서 새 인증서를 업데이트하고 적용하려면 새 자격 증명을 가져오고, 기존 PDF 문서에서 사용 권한을 제거하고, 사용 권한을 적용해야 합니다. Admin Console을 사용하여 자격 증명과 AEM Forms Reader 확장 API를 가져와 사용 권한을 제거하고 적용할 수 있습니다.

### 자격 증명 가져오기 및 구성

저장소 관리 페이지에서 새 자격 증명 또는 교체 자격 증명을 가져올 수 있습니다. 트러스트 저장소에 둘 이상의 Reader 확장 자격 증명이 포함될 수 있습니다. 이러한 자격 증명 중 하나를 기본 Reader 확장 자격 증명으로 지정해야 합니다. 기본 자격 증명은 Workbench 사용자가 프로세스 생성 중에 사용할 자격 증명을 결정할 수 없을 때 사용됩니다. 이러한 규칙은 기본 자격 증명에 적용됩니다.

* Reader 확장 자격 증명을 가져오고 트러스트 저장소에 다른 Reader 확장 자격 증명이 포함되어 있지 않으면 기본값으로 설정됩니다.
* 기본 옵션을 선택한 상태로 Reader 확장 자격 증명을 가져오는 경우 기본 유형은 기존 기본 자격 증명에서 제거됩니다. 가져온 자격 증명이 기본값이 됩니다.
* 기본 Reader 확장 자격 증명은 삭제할 수 없습니다. 기본 자격 증명을 삭제하려면 먼저 다른 자격 증명을 기본값으로 설정합니다. 이 규칙의 예외는 자격 증명이 하나만 있으면 기본값이지만 삭제할 수 있습니다.
* 기본 Reader 확장 자격 증명을 업데이트할 수 없습니다.

자격 증명을 가져오려면 다음을 수행하십시오.

1. 관리 콘솔에서 설정 > 신뢰 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 가져오기를 클릭하고 Trust Store 유형에서 Acrobat Reader DC 확장 자격 증명을 선택합니다.
1. (선택 사항) 이 자격 증명이 Acrobat Reader DC 확장에서 사용할 기본 자격 증명임을 나타내려면 기본값 을 선택합니다.
1. 별칭 상자에 자격 증명의 식별자를 입력합니다. 이 식별자는 Acrobat Reader DC 확장에서 자격 증명의 표시 이름으로 사용됩니다. 이 별칭은 AEM Forms SDK를 사용하여 프로그래밍 방식으로 자격 증명에 액세스하는 데에도 사용됩니다.
1. 파일 선택 을 클릭하여 자격 증명을 찾고 자격 증명의 암호를 입력한 다음 확인을 클릭합니다.

&quot;잘못된 파일 형식 또는 잘못된 암호로 인해 자격 증명을 가져오지 못했습니다&quot;라는 오류 메시지가 나타나면 암호가 유효한지 확인하십시오.

자격 증명을 프로그래밍 방식으로 가져오고 삭제할 수도 있습니다. (자세한 내용은 [AEM 양식을 사용한 프로그래밍](../../developing/credentials.md))

### 기존 권한이 활성화된 PDF 문서에서 사용 권한 제거

최신 자격 증명으로 사용 권한을 적용하기 전에 기존 권한 사용 PDF 문서에서 사용 권한을 제거합니다. JEE의 AEM Forms에서는 사용 권한을 제거하는 API를 제공합니다. 자세한 지침은 [PDF 문서에서 사용 권한 제거](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

Workbench에서 개발된 JEE 프로세스에서 AEM Forms에 대한 사용 권한을 제거하려면 다음을 참조하십시오 [Workbench 도움말](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### PDF 문서에 사용 권한 적용

새 자격 증명을 가져오고 기존 권한이 활성화된 PDF 문서에서 사용 권한을 제거한 후 새 자격 증명을 사용하여 PDF 문서에 사용 권한을 적용합니다. Acrobat Reader DC 확장 Java Client API 및 웹 서비스를 사용하여 PDF 문서에 사용 권한을 적용할 수 있습니다.  자세한 내용은 [PDF 문서에 사용 권한 적용](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## OSGi 환경에서 AEM Forms에 대한 인증서 업데이트 및 적용 {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

OSGi 스택에서 AEM Forms에 새 인증서를 업데이트하고 적용하려면 새 자격 증명을 가져오고, 기존 PDF 문서에서 사용 권한을 제거하고 사용 권한을 적용해야 합니다. Admin Console을 사용하여 자격 증명과 AEM Forms Reader 확장 API를 가져와 사용 권한을 제거하고 적용할 수 있습니다.

### 자격 증명 가져오기 {#Import-credentials}

OSGi 환경의 AEM Forms에서 Reader 확장 자격 증명은 fd-service 사용자와 연결됩니다. fd-user 키 저장소에 대한 자격 증명을 추가하기 전에 다음 단계를 수행하여 키 저장소를 만듭니다.

1. 관리자로 AEM 작성자 인스턴스에 로그인합니다.
1. 이동 **[!UICONTROL 도구]**> **[!UICONTROL 보안]**>**[!UICONTROL 사용자]**.
1. fd-service 사용자 계정을 찾을 때까지 사용자 목록을 아래로 스크롤합니다.
1. 클릭 **[!UICONTROL fd 서비스]** 사용자.
1. 키 저장소 탭을 클릭합니다.
1. 클릭 **[!UICONTROL 키 저장소 만들기]**.
1. KeyStore 액세스 암호를 설정하고 설정을 저장하여 KeyStore 암호를 만듭니다.

키 저장소를 만든 후 fd 서비스 사용자에게 자격 증명을 추가합니다. 다음 비디오에서는 단계에 대해 설명합니다.

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

다음 명령은 pfx 파일의 세부 정보를 나열합니다. 명령을 실행하기 전에 .pfx 파일이 포함된 디렉터리로 이동합니다.

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

예: keytool -v -list -storetype pkcs12 -keystore 1005566.pfx 여기서 1005566.pfx는 내 pfx 파일의 이름입니다.

### 기존 권한이 활성화된 PDF 문서에서 사용 권한 제거

최신 자격 증명으로 사용 권한을 적용하기 전에 기존 권한 사용 PDF 문서에서 사용 권한을 제거합니다. docAssuranceServiceAPI 내에서 removeUsageRights API를 호출하여 문서의 사용 권한을 제거할 수 있습니다. 자세한 내용은 [사용 권한 제거](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) 문서.

### PDF 문서에 사용 권한 적용

OSGi 환경의 AEM Forms에서 사용 권한을 적용하려면 해당 문서에 대한 사용 권한에 대한 사용자 지정 OSGi 서비스를 만드십시오. POST 방법이 있는 서블릿을 만들어 사용자에게 Reader 확장 PDF을 반환할 수도 있습니다. 자세한 지침은 [Reader 확장 적용](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).

## 자주 묻는 질문

**추가 질문이 있는 경우 누구에게 문의해야 합니까?**

연락하시면 됩니다 [Adobe 지원](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 또는 지원 티켓을 인상합니다.

**2023년 1월 7일 이전에 인증서를 업데이트하지 않으면 어떻게 됩니까?**

이전 인증서로 PDF 문서 Reader Extended를 열려고 하면 사용자에게 오류 메시지가 표시되고 더 이상 Reader 확장 기능에 액세스할 수 없습니다. 오류 예는 입니다.

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**새로운 설명이라는 이름에 변경이 있나요?**

새 Reader 확장 인증서에 설명에서 프로그램 이름으로 G3-P24가 언급되었습니다. 이전 인증서에서 설명에서 프로그램 이름 P24가 언급되었습니다.
