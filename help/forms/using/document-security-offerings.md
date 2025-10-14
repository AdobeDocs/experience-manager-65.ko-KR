---
title: 문서 보안 서비스
description: AEM Document Security의 다양한 도구 및 기능에 대해 알아봅니다.
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 0%

---

# 문서 보안 서비스{#document-security-offerings}

Adobe Experience Manager Forms document security는 인증된 사용자만 문서를 사용할 수 있도록 합니다. 문서 보안을 사용하면 저장한 모든 정보를 지원되는 형식으로 안전하게 배포할 수 있습니다. 지원되는 파일 형식에는 Adobe PDF(Portable Document Format) 및 Microsoft® Word, Excel, PowerPoint 파일이 포함됩니다.

정책을 사용하여 문서를 보호할 수 있습니다. 정책에 지정하는 기밀 유지 설정은 정책이 적용되는 문서를 수신자가 사용할 수 있는 방법을 결정합니다. 예를 들어 수신자가 텍스트를 인쇄 또는 복사하거나 텍스트를 편집하거나 보호된 문서에 서명과 주석을 추가할 수 있는지 여부를 지정할 수 있습니다.

정책은 Document Security 서버에 저장됩니다. 사용자는 클라이언트 애플리케이션을 통해 문서에 정책을 적용합니다. 문서에 정책을 적용하면 정책에 지정된 기밀 유지 설정이 문서에 포함된 정보를 보호합니다. 정책으로 보호된 문서를 정책에 의해 승인된 수신자에게 배포할 수 있습니다.

다음 다이어그램은 AEM Forms Document Security에 대한 일반적인 아키텍처를 보여 줍니다.

![문서 보안 - 권장 아키텍처](do-not-localize/document_security_architecture.png)

## Document Security 클라이언트 {#document-security-clients}

Document Security는 문서를 보호하고, 보호된 문서를 보고 편집할 수 있는 다양한 클라이언트와, 보호된 문서에 대한 전체 텍스트 검색을 가능하게 하는 인덱서를 제공합니다. 요구 사항 및 클라이언트의 기능을 기반으로 클라이언트를 선택할 수 있습니다.

Document Security 서버는 Document Security가 사용자 인증, 정책 실시간 관리 및 기밀 적용 등의 트랜잭션을 수행하는 중앙 구성 요소입니다. 또한 서버는 정책, 감사 레코드 및 기타 관련 정보를 위한 중앙 저장소를 제공합니다.

Document Security 서버는 정책을 만들고, 정책으로 보호된 문서를 관리하고, 정책으로 보호된 문서와 관련된 이벤트를 모니터링하는 웹 기반 인터페이스(웹 페이지)를 제공합니다. 또한 관리자는 사용자 인증, 감사 및 초대된 사용자에 대한 메시지와 같은 글로벌 옵션을 구성하고 초대된 사용자 계정을 관리할 수 있습니다.

서버는 AEM Forms Document Security 추가 기능 오퍼링에 포함되어 있습니다. Document Security 추가 기능을 구매하려면 AEM Forms [영업팀](https://business.adobe.com/request-consultation/experience-cloud.html?s_osc=70114000002JNwKAAW&s_iid=70114000002JHs3AAG)에 문의하십시오.

### Protect 문서 {#protect-documents}

AEM Forms Document Security는 보안 정책을 적용하는 다양한 도구를 제공합니다. 요구 사항 및 사양에 따라 도구를 선택할 수 있습니다.

![문서 보안 서비스](assets/document-security-offerings.png)

Document Security SDK, Adobe Acrobat, Microsoft® Office용 Document Security Extension 또는 Portable Protection Library를 사용하여 보안 정책을 적용하고 추적할 수 있습니다.

* **Document Security SDK:** SDK는 기능이 풍부한 클라이언트입니다. Document Security SDK를 사용하여 문서 서버 기능에 액세스하고, 정책으로 보호된 문서를 열고, 사용자 지정 확장 프로그램, 플러그인 또는 애플리케이션을 개발할 수 있습니다. 예를 들어 확장을 개발하여 사용자 지정 파일 형식을 보호하거나 SDK를 DLP(데이터 손실 방지) 솔루션과 통합할 수 있습니다. Document Security SDK를 사용하여 문서를 지정된 AEM Forms 서버로 전송하기 위해 개발된 확장, 애플리케이션 및 플러그인이며 정책은 서버에 적용됩니다. AEM Forms CSDK(Document Security Client SDK)는 PPL(Portable Protection Library)을 사용하여 보호되는 문서의 보호를 해제할 수 없으며, 이와 반대도 마찬가지입니다.

  Document Security SDK는 Java™ 및 C++ 모두에서 사용할 수 있습니다. Java™ SDK는 AEM Forms Document Security 오퍼링에 포함되어 있으며 JEE에 AEM Forms를 배포할 때 설치됩니다. C++ SDK를 조달하려면 [AEM 고객 지원 센터](https://experienceleague.adobe.com/ko?support-solution=General&support-tab=home#support)에 문의하십시오. C++ SDK는 Microsoft® Visual Studio 2013을 사용하여 컴파일할 수 있습니다. SDK의 기능을 배우고 사용할 수 있는 [Document Security API 설명서](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) 사이트를 방문하십시오.

* **Adobe Acrobat:** Adobe Acrobat을 사용하여 Microsoft® Office, 웹 브라우저와 같이 인기 있는 데스크톱 응용 프로그램을 사용하여 만든 PDF 문서 또는 PDF 형식으로 인쇄를 지원하는 모든 응용 프로그램에 보안 정책을 적용할 수 있습니다.

  [Adobe 웹 사이트](https://www.adobe.com/acrobat/free-trial-download.html)에서 Adobe Acrobat을 구입하고 다운로드할 수 있습니다. Adobe Acrobat 문서 [PDF에 대한 보안 정책 설정](https://helpx.adobe.com/kr/acrobat/using/setting-security-policies-pdfs.html)에서는 Adobe Acrobat에서 정책을 만들고 적용하는 방법에 대한 자세한 정보를 제공합니다.

* **Microsoft® Office용 Document Security Extension**: Microsoft® Office용 Document Security Extension을 사용하여 Microsoft® Office 프로그램 내에서 Microsoft® Office 파일에 사전 정의된 정책을 적용할 수 있습니다. 확장은 승인된 사용자만 정책으로 보호된 Microsoft® Word, Excel 및 PowerPoint 파일을 사용할 수 있도록 합니다. 플러그인이 설치된 승인된 사용자만 정책으로 보호된 파일을 사용할 수 있습니다.

  Document Security 확장은 Microsoft® Office 플러그인으로 사용할 수 있습니다. 확장을 얻으려면 [AEM 고객 지원 센터](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html)에 문의하십시오. 나중에 [Microsoft® Office용 Document Security Extension](https://experienceleague.adobe.com/docs/experience-manager-document-security/using/download-installer.html?lang=ko) 도움말을 방문하여 확장 기능 설치, 구성 및 사용에 대해 알아볼 수 있습니다.

* **이식 가능한 보호 라이브러리:** PPL은 AEM Forms 서버로 문서를 보내지 않고 로컬로 문서를 보호합니다. 보안 자격 증명과 정책 세부 정보만 네트워크를 통해 전달됩니다. 또한 PPL을 사용하면 로그인한 사용자만 정책 검색 액세스를 제한할 수 있습니다. AEM 사용자에 로그인한 사용자의 컨텍스트가 있는 정책을 가져올 수 있습니다.

  위와 함께 PPL에는 Document Security SDK의 모든 기능이 포함되어 있습니다. Document Security SDK를 사용하여 문서 서버 기능에 액세스하고, 정책으로 보호된 문서를 열고, 사용자 지정 확장 프로그램, 플러그인 또는 애플리케이션을 개발할 수 있습니다. PPL은 CSDK(AEM Forms document security client SDK)를 사용하여 보호된 문서를 보호 해제할 수 없으며 이와 반대로 보호할 수도 없습니다.

  PPL은 32비트 및 64비트 버전의 Java™ 및 C++ 언어에서 사용할 수 있습니다. 또한 OSGi에서 AEM Forms용 OSGi 번들로 사용할 수 있습니다. C++ PPL은 Microsoft® Visual Studio 2013으로 컴파일할 수 있습니다. AEM Forms Document Security 추가 기능에 라이선스를 부여한 경우 [AEM Forms Document Security](https://experienceleague.adobe.com/ko?support-solution=General&support-tab=home#support) 지원 팀에 연락하여 PPL을 확보할 수 있습니다. 나중에 PPL 도움말(라이브러리와 함께 제공됨)을 사용하여 PPL을 설정하고 사용할 수 있습니다.

### 보호된 문서 보기 또는 편집 {#view-or-edit-protected-documents}

* **PDF 문서**&#x200B;의 경우 Adobe Acrobat DC, Acrobat Reader 및 Acrobat Reader Mobile을 사용하여 보호된 PDF 문서를 볼 수 있습니다. 대부분의 사용자는 장치에 Acrobat Reader이 이미 설치되어 있으므로 보호된 문서를 보기 위해 추가 소프트웨어를 가져오거나 학습할 필요가 없습니다. [Acrobat Reader 다운로드 웹 사이트](https://get.adobe.com/reader/)에서 Acrobat Reader을 다운로드할 수도 있습니다.

* **Microsoft® Office 문서**&#x200B;의 경우 Microsoft® Office 및 Microsoft® Office용 AEM Forms Document Security 확장이 필요합니다. Document Security 확장은 Microsoft® Office 플러그인으로 사용할 수 있습니다. 확장 프로그램은 Adobe 웹 사이트에서 다운로드할 수 있습니다.

### 보호된 문서 색인 지정 {#index-protected-documents}

Microsoft® Windows 전체 텍스트 검색 엔진(SharePoint 인덱스 서버) 및 Adobe Experience Manager(AEM)은 일반 텍스트 파일, Microsoft® Office 문서 및 PDF 문서와 같이 일반적으로 사용되는 문서 형식에 대해 전체 텍스트 검색을 수행할 수 있습니다. Document Security 인덱서를 사용하여 전체 텍스트 검색 엔진이 보호된 PDF 문서를 검색할 수 있도록 할 수 있습니다.

* **iFilter 인덱서:** iFilter 인덱서를 사용하여 보호된 PDF 문서를 인덱싱하고 Microsoft® Windows 전체 텍스트 검색 엔진(데스크톱 인덱싱 서비스 및 SharePoint 인덱스 서버)에서 보호된 PDF 문서를 검색할 수 있도록 설정할 수 있습니다. 자세한 내용은 [보호된 문서에 대한 AEM SharePoint IFilter](assets/sharepoint-ifilter-doc-security.pdf)를 참조하십시오.

* **AEM Forms Document Security Indexer:** AEM Forms Document Security Indexer를 사용하여 보호된 PDF 문서를 인덱싱하고 Adobe Experience Manager에서 보호된 PDF 문서를 검색할 수 있습니다. 인덱서는 AEM Forms Document Security 서비스의 일부입니다. 이러한 기능은 JEE 설치 프로그램의 AEM Forms에 포함되어 있습니다.
