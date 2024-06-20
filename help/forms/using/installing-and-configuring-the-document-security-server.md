---
title: Document Security 서버 설치 및 구성
description: 문서 보안을 사용하여 지원되는 형식으로 저장한 정보를 안전하게 배포합니다. 승인된 사용자만 보호된 문서에 액세스할 수 있습니다.
contentOwner: khsingh
role: Admin
exl-id: 4a4bad4a-3e68-43cb-b55c-03b509a5d304
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: 939a2efa64c853928a9082aa30d7338e98deb695
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Document Security 서버 설치 및 구성 {#installing-and-configuring-the-document-security-server}

문서 보안을 사용하여 지원되는 형식으로 저장한 정보를 안전하게 배포합니다. 승인된 사용자만 보호된 문서에 액세스할 수 있습니다.

Adobe Experience Manager Forms document security는 인증된 사용자만 문서를 사용할 수 있도록 합니다. 문서 보안을 사용하면 저장한 모든 정보를 지원되는 형식으로 안전하게 배포할 수 있습니다. 지원되는 파일 형식에는 Adobe PDF 및 Microsoft Word, Excel, PowerPoint 파일이 포함됩니다.

정책을 사용하여 문서를 보호할 수 있습니다. 정책에 지정하는 기밀 유지 설정은 정책이 적용되는 문서를 수신자가 사용할 수 있는 방법을 결정합니다. 예를 들어 수신자가 텍스트를 인쇄 또는 복사하거나 텍스트를 편집하거나 보호된 문서에 서명과 주석을 추가할 수 있는지 여부를 지정할 수 있습니다.

정책은 Document Security 서버에 저장됩니다. 사용자는 클라이언트 애플리케이션을 통해 문서에 정책을 적용합니다. 문서에 정책을 적용하면 정책에 지정된 기밀 유지 설정이 문서에 포함된 정보를 보호합니다. 정책으로 보호된 문서를 정책에 의해 승인된 수신자에게 배포할 수 있습니다.

또한 Document Security는 클라이언트, 뷰어 및 인덱서를 제공하여 문서를 보호하고 보호된 문서를 보고 보호된 문서를 인덱싱합니다. 문서 보안에 대한 자세한 내용은 [문서 보안 기본 정보](/help/forms/using/admin-help/document-security.md).

## 배포 토폴로지  {#deployment-topology}

문서 보안 기능은 JEE의 AEM Forms에서만 사용할 수 있습니다. JEE에서 단일 AEM Forms 인스턴스가 필요합니다. 필요한 경우 AEM Forms 서버의 클러스터 또는 팜을 만들 수도 있습니다. 다음 토폴로지는 문서 보안 기능을 실행하는 토폴로지를 나타냅니다. 토폴로지에 대한 자세한 내용은 [AEM Forms의 아키텍처 및 배포 토폴로지](aem-forms-architecture-deployment.md).

<!--fix above link-->

![Document Security 서버 토폴로지](do-not-localize/document-security-server_topology.png)

다음 다이어그램은 AEM Forms Document Security에 대한 일반적인 아키텍처를 보여 줍니다.

![문서 보안 일반 환경](do-not-localize/document-security-typical-environment.png)

## JEE에 AEM Forms 설치 {#installing-aem-forms-on-jee}

JEE에 AEM Forms을 설치하고 구성하려면 다음 단계를 수행하십시오.

1. 에서 AEM 6.5 Forms on JEE 설치 프로그램을 다운로드합니다. [Adobe 라이선스 웹 사이트(LWS)](https://licensing.adobe.com/). 설치 관리자를 다운로드하려면 유효한 유지 관리 및 지원 계약이 필요합니다.
1. 읽기 [JEE의 AEM Forms 지원 플랫폼 문서](/help/forms/using/aem-forms-jee-supported-platforms.md) 또한 소프트웨어, 하드웨어, 운영 체제, 애플리케이션 서버, 데이터베이스, JDK 및 기타 인프라가 JEE에 AEM Forms을 설치할 준비가 되어 있는지 확인합니다.
1. (Non-Turnkey 설치만 해당) [AEM Forms 단일 서버 설치 준비](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) 또는 [AEM Forms 서버 클러스터 설치 준비 중](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) 환경에서 JEE에 AEM Forms을 설치하고 구성할 수 있도록 준비하십시오.
1. 사용 중인 환경과 애플리케이션 서버에 따라 다음 문서 중 하나를 선택하고 지침에 따라 설치를 완료합니다

   * [JBoss 턴키를 사용하여 JEE에 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [JBoss용 JEE에 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [WebLogic용 JEE에 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [WebSphere용 JEE에 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [JBoss 클러스터의 JEE에서 AEM Forms 구성](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [WebLogic 클러스터에서 JEE의 AEM Forms 구성](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [WebSphere 클러스터에서 JEE의 AEM Forms 구성](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >JEE 구성 관리자의 AEM Forms에 있는 모듈 선택 화면에서 Document Security 옵션을 선택합니다. Document Security 옵션에서는 다른 모듈을 선택할 필요가 없습니다.

## 다음 단계 {#next-steps}

* [클라이언트 및 서버 옵션 구성](/help/forms/using/admin-help/configuring-client-server-options.md)
* [정책 생성 및 관리](/help/forms/using/admin-help/creating-policies.md)
* [정책 집합 만들기 및 관리](/help/forms/using/admin-help/creating-policy-sets.md)
