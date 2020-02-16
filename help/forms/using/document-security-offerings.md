---
title: 문서 보안 솔루션
seo-title: 문서 보안 솔루션
description: AEM Document Security의 다양한 도구 및 기능에 대해 알아봅니다.
seo-description: AEM Document Security의 다양한 도구 및 기능에 대해 알아봅니다.
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 문서 보안 솔루션{#document-security-offerings}

Adobe Experience Manager Forms 문서 보안을 통해 인증된 사용자만 문서를 사용할 수 있습니다. 문서 보안을 사용하면 지원되는 형식으로 저장한 모든 정보를 안전하게 배포할 수 있습니다. 지원되는 파일 포맷에는 Adobe PDF(Portable Document Format), Microsoft Word, Excel 및 PowerPoint 파일이 있습니다.

정책을 사용하여 문서를 보호할 수 있습니다. 정책에서 지정하는 기밀 설정에 따라 수신자가 정책을 적용할 문서를 사용할 수 있는 방법이 결정됩니다. 예를 들어 수신자가 텍스트를 인쇄 또는 복사하거나 텍스트를 편집하거나 서명 및 주석을 보호된 문서에 추가할 수 있는지 여부를 지정할 수 있습니다.

정책은 Document Security 서버에 저장됩니다.클라이언트 애플리케이션을 통해 문서에 정책을 적용합니다. 문서에 정책을 적용하면 정책에 지정된 기밀 설정이 문서에 포함된 정보를 보호합니다. 정책으로 보호된 문서를 정책에 의해 권한이 부여된 수신자에게 배포할 수 있습니다.

다음 다이어그램은 AEM Forms Document Security의 일반적인 아키텍처를 보여줍니다.

![Document Security - 권장 아키텍처](do-not-localize/document_security_architecture.png)

## Document Security 클라이언트 {#document-security-clients}

Document Security는 문서를 보호하고, 보호된 문서를 보고 편집할 수 있는 다양한 클라이언트와 보호된 문서에서 전체 텍스트를 검색할 수 있는 인덱서를 제공합니다. 클라이언트의 요구 사항과 기능을 기반으로 클라이언트를 선택할 수 있습니다.

Document Security Server는 Document Security에서 사용자 인증, 정책 실시간 관리, 기밀 적용 등의 트랜잭션을 수행하는 중앙 구성 요소입니다. 또한 서버는 정책, 감사 기록 및 기타 관련 정보에 대한 중앙 저장소를 제공합니다.

Document Security 서버는 웹 기반 인터페이스(웹 페이지)를 제공하여 정책을 만들고, 정책으로 보호된 문서를 관리하며, 정책으로 보호된 문서와 관련된 이벤트를 모니터링합니다. 관리자는 초대된 사용자에 대한 사용자 인증, 감사 및 메시지와 같은 글로벌 옵션을 구성하고 초대된 사용자 계정을 관리할 수도 있습니다.

서버는 AEM Forms Document Security Add-on 제공에 포함되어 있습니다. AEM Forms [세일즈 팀에](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&s_iid=70114000002JHs3AAG) 연락하여 Document Security Add-on을 구입할 수 있습니다.

### 문서 보호 {#protect-documents}

AEM Forms Document Security는 보안 정책을 적용하는 다양한 도구를 제공합니다. 요구 사항 및 사양에 따라 도구를 선택할 수 있습니다.

![문서 보안 솔루션](assets/document-security-offerings.png)

Document Security SDK, Adobe Acrobat, Document Security Extension for Microsoft Office 또는 Portable Protection Library를 사용하여 보안 정책을 적용하고 추적할 수 있습니다.

* **** Document Security SDK:SDK는 기능이 풍부한 클라이언트입니다. Document Security SDK를 사용하여 문서 서버 기능에 액세스하고, 정책으로 보호된 문서를 열고, 사용자 정의 확장, 플러그인 또는 응용 프로그램을 개발할 수 있습니다. 예를 들어 사용자 정의 파일 형식을 보호하기 위한 익스텐션을 개발하거나 SDK를 DLP(Data Loss Prevention) 솔루션과 통합할 수 있습니다. Document Security SDK를 사용하여 개발한 확장 프로그램, 응용 프로그램 및 플러그인은 지정된 AEM Forms 서버로 문서를 전송하고 정책이 서버에 적용됩니다. 또한 AEM Forms CSDK(Document Security Client SDK)는 PPL(Portable Protection Library)을 사용하여 보호된 문서의 보호를 해제할 수 없습니다.

   Document Security SDK 파섹 Java SDK 파섹 AEM 지원 [팀에](https://helpx.adobe.com/marketing-cloud/contact-support.html) 문의하여 C++ SDK를 구할 수 있습니다. C++ SDK 파섹 Document Security API [설명서](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) 사이트를 방문하여 SDK 기능을 배우고 사용할 수 있습니다.

* **** Adobe Acrobat:Adobe Acrobat을 사용하면 Microsoft Office, 웹 브라우저 또는 PDF 포맷으로 인쇄할 수 있는 모든 애플리케이션과 같이 널리 사용되는 데스크탑 애플리케이션을 사용하여 만든 PDF 문서에 보안 정책을 적용할 수 있습니다.

   Adobe 웹 사이트에서 Adobe Acrobat을 구입하고 다운로드할 [수 있습니다](https://acrobat.adobe.com/us/en/free-trial-download.html). PDF에 대한 보안 정책 [설정](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) 문서는 Adobe Acrobat에서 정책 작성 및 적용에 대한 자세한 정보를 제공합니다.

* **Document Security Extension for Microsoft Office**:Document Security Extension for Microsoft Office를 사용하여 Microsoft Office 프로그램 내에서 미리 정의된 정책을 Microsoft Office 파일에 적용할 수 있습니다. 이 확장 기능을 통해 권한이 있는 사용자만 정책으로 보호된 Microsoft Word, Excel 및 PowerPoint 파일을 사용할 수 있습니다. 플러그인을 설치한 인증된 사용자만 정책으로 보호된 파일을 사용할 수 있습니다.

   Document Security 익스텐션은 Microsoft Office 플러그인으로 사용할 수 있습니다. AEM [지원 팀에](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) 문의하여 익스텐션을 받을 수 있습니다. 나중에 Document Security Extension for [Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/aem-document-security-extension-help.html) 도움말에서 익스텐션의 설치, 구성 및 사용에 대해 알아볼 수 있습니다.

* **** Portable Protection Library:PPL(Portable Protection Library)은 문서를 AEM Forms 서버로 보내지 않고 로컬에서 문서를 보호합니다. 보안 자격 증명과 정책 세부 사항만 네트워크를 통해 이동합니다. 또한 PPL을 사용하면 로그인한 사용자만 정책 검색 액세스를 제한할 수 있습니다. AEM 사용자에 로그인한 사용자의 컨텍스트에서 정책을 가져올 수 있습니다.

   상기와 함께 ReportTable Protection Library에는 Document Security SDK의 모든 기능이 포함되어 있습니다. Document Security SDK를 사용하여 문서 서버 기능에 액세스하고, 정책으로 보호된 문서를 열고, 사용자 정의 확장, 플러그인 또는 응용 프로그램을 개발할 수 있습니다. 또한 PPL(Portable Protection Library)은 AEM Forms CSDK(Document Security Client SDK)를 사용하여 보호된 문서의 보호를 해제할 수 없습니다.

   PDF(Portable Protection Library)는 32비트 및 64비트 버전의 Java 및 C++ 언어로 제공됩니다. OSGi에서 AEM Forms용 OSGi 번들로 사용할 수도 있습니다. C++ PPL은 Microsoft Visual Studio 2013에서 컴파일할 수 있습니다. AEM Forms Document Security Add-on에 라이선스를 부여받은 경우 AEM Forms Document [Security](https://helpx.adobe.com/marketing-cloud/contact-support.html) 지원 팀에 문의하여 Portable Protection Library를 구할 수 있습니다. 나중에 PDF(Portable Protection Library) 도움말(라이브러리와 함께 번들로 제공)을 사용하여 PDF(Portable Protection Library)를 설정하고 사용할 수 있습니다.

### 보호된 문서 보기 또는 편집 {#view-or-edit-protected-documents}

* PDF **문서의**&#x200B;경우 Adobe Acrobat DC, Acrobat Reader 및 Acrobat Reader Mobile을 사용하여 보호된 PDF 문서를 볼 수 있습니다. 대부분의 사용자는 이미 Acrobat Reader가 설치되어 있으므로 보호된 문서를 보기 위해 추가 소프트웨어를 구입하거나 학습하지 않아도 됩니다. 또한 Acrobat Reader 다운로드 웹 사이트에서 [Acrobat Reader를 다운로드할](https://get.adobe.com/reader/)수 있습니다.

* Microsoft **Office 문서의**&#x200B;경우 Microsoft Office용 Microsoft Office 및 AEM Forms Document Security 익스텐션이 필요합니다. Document Security 익스텐션은 Microsoft Office 플러그인으로 사용할 수 있습니다. Adobe 웹 사이트에서 익스텐션을 다운로드할 수 있습니다.

### 보호된 문서 색인 지정 {#index-protected-documents}

Microsoft Windows 전체 텍스트 검색 엔진(SharePoint Index 서버) 및 Adobe Experience Manager(AEM)는 일반 텍스트 파일, Microsoft Office 문서 및 PDF 문서와 같이 일반적으로 사용되는 문서 형식에서 전체 텍스트 검색을 수행할 수 있습니다. Document Security 인덱서를 사용하여 전체 텍스트 검색 엔진을 사용하여 보호된 PDF 문서를 검색할 수 있습니다.

* **** iFilter 인덱서:iFilter 인덱서를 사용하여 보호된 PDF 문서를 색인화하고 Microsoft Windows 전체 텍스트 검색 엔진(데스크탑 인덱싱 서비스 및 SharePoint Indexserver)을 활성화하여 보호된 PDF 문서를 검색할 수 있습니다. 자세한 내용은 보호된 [문서용 AEM SharePoint IFilter를 참조하십시오](assets/sharepoint-ifilter-doc-security.pdf).

* **** AEM Forms Document Security Indexer:AEM Forms Document Security 인덱서를 사용하여 보호된 PDF 문서를 색인화하고 Adobe Experience Manager를 사용하여 보호된 PDF 문서를 검색할 수 있습니다. 인덱서는 AEM Forms Document Security 서비스의 일부입니다. JEE 설치 관리자의 AEM Forms에 포함되어 있습니다.

