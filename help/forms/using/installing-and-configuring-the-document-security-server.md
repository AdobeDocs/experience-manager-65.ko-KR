---
title: 문서 보안 서버 설치 및 구성
seo-title: 문서 보안 서버 설치 및 구성
description: '문서 보안을 사용하여 지원되는 형식으로 저장한 모든 정보를 안전하게 배포할 수 있습니다. 보호된 문서에는 승인된 사용자만 액세스할 수 있습니다. '
seo-description: '문서 보안을 사용하여 지원되는 형식으로 저장한 모든 정보를 안전하게 배포할 수 있습니다. 보호된 문서에는 승인된 사용자만 액세스할 수 있습니다. '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# 문서 보안 서버 {#installing-and-configuring-the-document-security-server} 설치 및 구성

문서 보안을 사용하여 지원되는 형식으로 저장한 모든 정보를 안전하게 배포할 수 있습니다. 보호된 문서에는 승인된 사용자만 액세스할 수 있습니다.

Adobe Experience Manager Forms 문서 보안을 통해 인증된 사용자만 문서를 사용할 수 있습니다. 문서 보안을 사용하면 지원되는 형식으로 저장한 모든 정보를 안전하게 배포할 수 있습니다. 지원되는 파일 형식으로는 Adobe PDF(Portable Document Format) 및 Microsoft Word, Excel 및 PowerPoint 파일이 있습니다.

정책을 사용하여 문서를 보호할 수 있습니다. 정책에서 지정하는 기밀 설정에 따라 정책을 적용하는 문서를 받는 사람이 사용할 수 있는 방법이 결정됩니다. 예를 들어 받는 사람이 텍스트를 인쇄 또는 복사하거나 텍스트를 편집하거나 서명 및 주석을 보호된 문서에 추가할 수 있는지 여부를 지정할 수 있습니다.

정책은 Document Security 서버에 저장됩니다.클라이언트 애플리케이션을 통해 문서에 정책을 적용합니다. 문서에 정책을 적용하면 정책에 지정된 기밀 설정이 문서에 포함된 정보를 보호합니다. 정책으로 보호된 문서를 정책에 의해 권한이 부여된 수신자에게 배포할 수 있습니다.

또한 문서 보안은 클라이언트, 뷰어 및 인덱서를 제공하여 문서를 보호하고 보호된 문서를 보고 보호된 문서를 색인화합니다. 문서 보안에 대한 자세한 내용은 [문서 보안 정보](/help/forms/using/admin-help/document-security.md)를 참조하십시오.

## 배포 토폴로지 {#deployment-topology}

문서 보안 기능은 JEE의 AEM Forms에서만 사용할 수 있습니다. JEE에서 AEM Forms의 단일 인스턴스가 필요합니다. 필요한 경우 AEM Forms 서버의 클러스터 또는 팜을 만들 수도 있습니다. 다음 토폴로지는 문서 보안 기능을 실행하기 위한 토폴로지를 나타냅니다. 토폴로지에 대한 자세한 내용은 [AEM Forms](aem-forms-architecture-deployment.md)용 아키텍처 및 배포 토폴로지를 참조하십시오.

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

다음 다이어그램은 AEM Forms Document Security의 일반적인 아키텍처를 보여 줍니다.

![](do-not-localize/document-security-typical-environment.png)

## JEE {#installing-aem-forms-on-jee}에 AEM Forms 설치

JEE에 AEM Forms을 설치하고 구성하려면 다음 단계를 수행하십시오.

1. [LWS(Adobe Licensing Website)](https://licensing.adobe.com/)에서 JEE 설치 관리자의 AEM 6.5 Forms을 다운로드합니다. 설치 프로그램을 다운로드하려면 유효한 유지 관리 및 지원 계약이 필요합니다.
1. [AEM Forms on JEE 지원 플랫폼 문서](/help/forms/using/aem-forms-jee-supported-platforms.md)를 읽고 소프트웨어, 하드웨어, 운영 체제, 응용 프로그램 서버, 데이터베이스, JDK 및 기타 인프라가 JEE에 AEM Forms을 설치할 준비가 되었는지 확인합니다.
1. (턴키가 설치되지 않은 경우) [AEM Forms 단일 서버 설치 준비](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) 또는 [AEM Forms 서버 클러스터 설치 준비](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64)를 읽고 JEE에 AEM Forms을 설치하고 구성할 환경을 준비하십시오.
1. 환경 및 응용 프로그램 서버에 따라 다음 문서 중 하나를 선택하고 지침에 따라 설치를 완료하십시오

   * [JBoss 턴키를 사용하여 JEE에 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [JBoss용 JEE에 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [WebLogic용 JEE에 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [WebSphere용 JEE에 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [JBoss 클러스터의 JEE에서 AEM Forms 구성](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [WebLogic 클러스터의 JEE에서 AEM Forms 구성](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [WebSphere 클러스터의 JEE에서 AEM Forms 구성](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >JEE 구성 관리자의 AEM Forms의 모듈 선택 화면에서 Document Security 옵션을 선택합니다. Document Security 옵션은 다른 모듈을 선택할 필요가 없습니다.

## 다음 단계 {#next-steps}

* [클라이언트 및 서버 옵션 구성](/help/forms/using/admin-help/configuring-client-server-options.md)
* [정책 만들기 및 관리](/help/forms/using/admin-help/creating-policies.md)
* [정책 집합 만들기 및 관리](/help/forms/using/admin-help/creating-policy-sets.md)
