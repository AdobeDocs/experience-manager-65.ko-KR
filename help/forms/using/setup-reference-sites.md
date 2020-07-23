---
title: We.Finance 및 Employee 셀프 서비스 참조 사이트 설정 및 구성
seo-title: We.Finance 및 Employee 셀프 서비스 참조 사이트 설정 및 구성
description: AEM Forms 참조 사이트는 AEM Forms을 사용하여 조직에서 엔드 투 엔드 워크플로우를 구현하는 방법을 보여줍니다.
seo-description: AEM Forms 참조 사이트는 AEM Forms을 사용하여 조직에서 엔드 투 엔드 워크플로우를 구현하는 방법을 보여줍니다.
uuid: 199349b7-97bd-4eca-a2e7-19d6708fcbee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 03886dd3-5873-4908-912b-fbbddb26c322
docset: aem65
translation-type: tm+mt
source-git-commit: 371ecbdaad97b7111353f40d1ddfb686e99d46c5
workflow-type: tm+mt
source-wordcount: '2878'
ht-degree: 0%

---


# We.Finance 및 Employee 셀프 서비스 참조 사이트 설정 및 구성{#set-up-and-configure-we-finance-and-employee-self-service-reference-sites}

AEM Forms은 AEM Forms이 금융 서비스 산업 및 공공 기관에서 언제 어디에서나 모든 디바이스에서 복잡한 거래를 간단하고 매력적인 디지털 경험으로 전환하는 데 어떻게 도움이 되는지 보여주는 참조 사이트 구현을 제공합니다.

Adobe.Finance 참조 사이트는 실제 사용 사례를 활용하여 기존 고객과 잠재 고객의 참여를 유도하고, 첫 번째 접촉에서부터 개인화되고 비용 효과적인 방법으로 통신과 거래를 관리한다.

참조 사이트를 통해 다음과 같은 AEM Forms의 주요 기능을 살펴보고 선보일 수 있습니다.

* 매력적이고 응답성이 높은 적응형 양식 및 인터랙티브한 커뮤니케이션의 저작 경험을 간소화할 수 있습니다.
* 인터랙티브한 커뮤니케이션을 통해 디바이스 설정 및 레이아웃에 맞는 인터랙티브하고 개인화된 반응형 고객 커뮤니케이션을 제작할 수 있습니다.
* 데이터 통합을 통해 서로 다른 데이터 소스에 연결하여 양식 데이터 모델을 통해 양식 데이터를 미리 채우고 제출할 수 있습니다.
* 양식 워크플로우를 통해 비즈니스 프로세스 및 워크플로우 자동화
* 고급 사용자 데이터 관리 및 처리 기능
* Adobe Sign과 통합하여 적응형 양식에 안전하게 서명하고 제출할 수 있습니다.
* Adobe Target과 통합하여 타깃팅된 추천을 제공하고 A/B 테스트를 실시하여 양식에서 ROI를 극대화할 수 있습니다.
* Adobe Analytics과 통합하여 양식과 캠페인의 성과를 측정하고 현명한 의사 결정을 내릴 수 있습니다.
* 향상된 양식 채우기 경험

참조 사이트에서는 재사용 가능한 자산을 제공하여 사용자 고유의 자산을 만드는 템플릿으로 사용할 수 있습니다.

* Adobe Sign과 통합하여 적응형 양식에 안전하게 서명하고 제출할 수 있습니다.

* Adobe Sign과 통합하여 적응형 양식에 안전하게 서명하고 제출할 수 있습니다.

## 참조 사이트를 설정하는 사전 요구 사항 및 단계 {#prerequisites-and-steps-to-set-up-reference-sites}

참조 사이트를 설정하기 전에 다음을 보유해야 합니다.

* **AEM Essentials** AEM QuickStart, AEM Forms 추가 기능 패키지 및 참조 사이트 패키지. Add-on 및 참조 사이트 패키지 세부 정보는 [AEM Forms 릴리스를](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 참조하십시오.

* **SMTP 서비스** SMTP 서비스를 사용할 수 있습니다.

* **Adobe Sign 개발자 계정 및 Adobe Sign API 애플리케이션** 디지털 서명 기능을 사용하려면 Adobe Sign 개발자 계정이 필요합니다. Adobe [Sign을 참조하십시오](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html).

* AEM Forms과 통합되는 Microsoft Dynamics 365의 실행 인스턴스입니다. 참조 사이트를 실행하려면 샘플 데이터를 Microsoft Dynamics 인스턴스로 가져와서 참조 사이트에 사용되는 대화형 통신을 미리 채웁니다.
* Forms 추가 기능 패키지가 있는 AEM의 실행 중인 인스턴스입니다. 자세한 내용은 AEM Forms [설치 및 구성을 참조하십시오](../../forms/using/installing-configuring-aem-forms-osgi.md).

권장 시퀀스에서 다음 단계를 수행하여 참조 사이트를 설정하고 구성합니다.

<table>
 <tbody>
  <tr>
   <th><strong>단계</strong></th>
   <th><strong>구성</strong></th>
   <th><strong>메모</strong></th>
  </tr>
  <tr>
   <td><a href="#installandconfigureaemform">AEM Forms 설치 및 구성</a></td>
   <td>작성 및 게시</td>
   <td>AEM Forms 작성자 및 게시 인스턴스를 설치하고 구성합니다.</td>
  </tr>
  <tr>
   <td><a href="#ssl">SSL 구성</a></td>
   <td>Author and Publish<br /> </td>
   <td>Adobe Sign을 사용하여 안전한 커뮤니케이션을 위해 SSL을 통해 HTTP를 활성화합니다.</td>
  </tr>
  <tr>
   <td><p><a href="#externalizer">일 CQ 링크 외부라이저 구성 구성</a></p> </td>
   <td>Author and Publish<br /> </td>
   <td><p>참조 사이트 사용 사례에서는 다른 거래에 대한 이메일을 전달합니다. 이 설정은 이메일을 통한 뉴스레터 전달에 필요합니다. URL과 이미지가 게시 인스턴스를 가리키는지 확인합니다. </p> </td>
  </tr>
  <tr>
   <td><a href="#cqmail">일 CQ 메일 서비스 구성</a></td>
   <td>작성 및 게시</td>
   <td>이메일 통신에 필요합니다.</td>
  </tr>
  <tr>
   <td><a href="#xss">기본 XSS 구성 재정의</a></td>
   <td>게시</td>
   <td>xss 보안에 의해 차단된 $, { 및 } 문자를 무시하는 데 사용됩니다.</td>
  </tr>
  <tr>
   <td><a href="#aemds">AEM DS 설정 구성</a></td>
   <td>작성</td>
   <td>작성 인스턴스의 게시 인스턴스 및 처리 워크플로우에 대한 양식 제출용 AEM DS를 구성합니다.</td>
  </tr>
  <tr>
   <td><a href="#refsite">참조 사이트 패키지 배포</a></td>
   <td>작성</td>
   <td>AEM Forms 작성자 인스턴스에 참조 사이트 패키지를 배포합니다.</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">Microsoft Dynamics로 샘플 데이터 가져오기</a></td>
   <td>작성 및 게시</td>
   <td>신용 카드 신청서, 주택 담보 대출 신청서 및 주택 보험 신청 연습 샘플 데이터 가져오기</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">Microsoft Dynamics용 OAuth 클라우드 서비스 구성</a></td>
   <td>작성 및 게시</td>
   <td>AEM Forms과 Microsoft Dynamics 간의 통신을 사용하도록 AEM Forms에서 OAuth 클라우드 서비스를 구성합니다. </td>
  </tr>
  <tr>
   <td><a href="#scheduler">Adobe Sign 스케줄러 구성</a></td>
   <td>Author and Publish<br /> </td>
   <td>2분마다 상태를 확인하도록 스케줄러의 구성을 변경합니다.</td>
  </tr>
  <tr>
   <td><a href="#sign-service">참조 사이트 구성 Adobe Sign Cloud Service</a></td>
   <td>Author and Publish<br /> </td>
   <td>참조 사이트 패키지와 함께 제공되는 구성이며 유효한 자격 증명으로 재구성해야 합니다.</td>
  </tr>
  <tr>
   <td><a href="#anonymous">익명 사용자를 위한 Forms Common Configuration Service 구성</a></td>
   <td>게시</td>
   <td>이 구성을 통해 익명 사용자를 위해 기록 문서를 제출, 서명 및 생성할 수 있습니다.</td>
  </tr>
  <tr>
   <td><a href="#fdm">양식 데이터 모델에 대한 Rest 서비스 Swagger 파일 수정</a></td>
   <td>Author and Publish<br /> </td>
   <td>환경에 맞는 서비스를 수정합니다.</td>
  </tr>
 </tbody>
</table>

## AEM Forms 설치 및 구성 {#installandconfigureaemform}

OSGi에 AEM Forms 설치 및 구성에 설명된 [대로 AEM Forms을 설치하고 배포합니다](../../forms/using/installing-configuring-aem-forms-osgi.md).

>[!NOTE]
>
>다른 컴퓨터에 둘 이상의 게시 인스턴스 또는 작성자 및 게시 인스턴스가 있는 경우 복제 및 역 복제 에이전트를 구성합니다.

## SSL 구성 {#ssl}

Adobe Sign 서버와 통신하려면 SSL 구성이 필요합니다. 자세한 내용은 SSL을 [통해 HTTP 활성화를 참조하십시오](/help/sites-administering/ssl-by-default.md).

>[!CAUTION]
>
>폴더에 강제 SSL을 구성하지 `/etc/map` 마십시오.

## 일 CQ 링크 외부라이저 구성 구성 {#externalizer}

AEM에서 Externalizer **는** 리소스 경로(예: 사전 구성된 DNS로 경로를 미리 수정하여 /path/to/my/page)를 외부 및 절대 URL(예: https://www.mycompany.com/path/to/my/page)으로 변환합니다. URL [외부화를 참조하십시오](/help/sites-developing/externalizer.md).

>[!CAUTION]
>
>SSL에 대해 자체 서명된 인증서를 사용하는 경우 HTTPS URL로 외부화하지 마십시오.
>
>또한 로컬 서버의 호스트 이름 대신 localhost를 사용하십시오.

작성자 및 게시 인스턴스 모두에서 다음 단계를 수행합니다.

1. https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr의 OSGi 구성으로 이동합니다.
1. Day CQ **Link Externalizer 구성을 찾아** 탭합니다.
구성을 편집하기 위해 [일 CQ 링크 외부라이저] 대화 상자가 열립니다.
1. [CQ 연결 외부 도우미]일 대화 상자의 [도메인] 필드에 있습니다.

   * 작성 인스턴스에서 외부 시스템에서 액세스할 수 있는 게시 URL을 지정합니다. 예를 들어 호스트 이름 또는 게시 웹 서버 등이 있습니다.
   * 게시 인스턴스에서 작성자 및 게시 URL을 모두 지정합니다.

1. 작성자 및 게시 인스턴스 모두에서 도메인 필드에 로컬 서버 URL이 지정되어 있는지 확인합니다.
1. 저장을 **누릅니다**. 모든 서비스가 다시 시작될 때까지 잠시 기다려 주십시오.

## 일 CQ 메일 서비스 구성 {#cqmail}

사이트 구현을 참조하려면 샘플 사용자가 양식을 채우고 제출할 때 이메일을 보내야 합니다. 요일 CQ 메일 서비스를 구성하면 SMTP 서비스 세부 사항을 제공하여 고객에게 자동화된 이메일을 보낼 수 있습니다. See [Configuring Email Notifications](/help/sites-administering/notification.md).

게시 인스턴스에서 메일 서비스를 구성하려면 다음 단계를 수행하십시오.

1. https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr의 OSGi 구성으로 이동합니다.
1. Day CQ **Mail Service를 찾아 탭하여** 열어서 구성합니다.
1. SMTP 서버 호스트 이름 및 포트 값을 제공합니다.
1. 저장을 **누릅니다.**

>[!NOTE]
>
>회사 SMTP 서비스 또는 Gmail과 같은 공용 서비스를 사용할 수 있습니다. SMTP 서비스를 구성하려면 SMTP 서비스 설명서를 참조하십시오.

## 기본 XSS 구성 재정의 {#xss}

We.Finance 참조 사이트에 대한 이메일 템플릿에는 이메일에 개인화된 링크가 포함되어 있습니다. 이러한 링크에는 자리 표시자가 있습니다 `${placeholder}`. 이러한 자리 표시자는 이메일을 보내기 전에 실제 값으로 대체됩니다. AEM에 대한 기본 XSS 보호 구성에서는 HTML 컨텐츠의 URL에 중괄호(**{ }**)를 허용하지 않습니다. 하지만 게시 인스턴스에서 다음 단계를 수행하여 기본 구성을 재정의할 수 있습니다.

1. 복사 `/libs/cq/xssprotection/config.xml` 를 `/apps/cq/xssprotection/config.xml`참조하십시오.
1. 열기 `/apps/cq/xssprotection/config.xml`.
1. 섹션에서 `common-regexps` 항목을 `onsiteURL` 다음과 같이 수정하고 파일을 저장합니다.

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>중괄호(**{ }**)는 HTML 컨텐츠의 URL에 허용되는 문자로 포함됩니다.

SMTP 서버를 구성한 후 사라 로즈 가상 사용자를 사용하여 양식을 채우고 초안으로 저장해 봅니다. 초안으로 저장할 때 이메일을 사용하여 초안을 수신할 수 있는 옵션이 표시됩니다. [ **이메일** 보내기] 단추를 누르면 응용 프로그램 초안으로 연결되는 링크가 포함된 이메일을 수신하면 이메일 구성이 성공합니다. 초안을 보려면 Sarah의 자격 증명을 사용하여 로그인해야 합니다.

## AEM DS 설정 구성 {#aemds}

참조 사이트 사용 사례의 이메일 커뮤니케이션을 위한 게시 인스턴스에 AEM DS 서비스 설정이 필요합니다. 게시 인스턴스에서 AEM DS 서비스 설정을 구성하는 자세한 단계는 AEM DS 설정 [구성을 참조하십시오](../../forms/using/configuring-the-processing-server-url-.md).

AEM Forms 참조 사이트의 경우 AEM DS 설정 서비스에서 처리 서버의 URL 대신 게시 서버의 URL을 지정합니다.

>[!CAUTION]
>
>AEM Forms OSGi `/lc` 에 대해 처리 서버 URL을 구성하는 경우에는 처리 서버 URL에 넣지 마십시오.

## 참조 사이트 패키지 배포 {#refsite}

소프트웨어 배포를 사용하여 참조 사이트 패키지 [를 설치합니다](https://docs.adobe.com/content/help/en/experience-cloud/software-distribution/home.html).

* [AEM Forms FSI 참조 사이트 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2FAEM-FORMS-6.5-FSI-REF-SITE)
* [AEM Forms Gov Reference 사이트 패키지](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2FAEM-FORMS-6.5-GOV-REF-SITE)

패키지 사용 방법에 대한 자세한 내용은 패키지 [를 사용한 작업 방법을 참조하십시오](/help/sites-administering/package-manager.md).

패키지를 설치하고 작성자 및 게시 인스턴스를 시작한 후 브라우저에서 다음 URL을 참조하십시오.

* `https://'[server]:[port]'/wegov`
* `https://'[server]:[port]'/wefinance`

설치가 성공하면 및 We.Finance 참조 사이트 랜딩 페이지에 액세스할 수 있습니다.

## (선택 사항) 샘플 데이터를 Microsoft Dynamics로 가져오기 {#optional-import-sample-data-into-microsoft-dynamics}

Microsoft Dynamics의 레코드를 사용하도록 가정용 대출 응용 프로그램 및 자동 보험 응용 프로그램 참조 사이트가 구성됩니다. 참조 사이트 패키지는 참조 사이트를 실행하기 위해 Microsoft Dynamics로 가져올 수 있는 사용자 지정 엔터티 및 샘플 레코드를 설치합니다. 샘플 데이터를 마이그레이션하고 설정하려면 다음 단계를 수행하십시오.

자동 보험 적용을 위한 사용자 지정 엔티티를 가져오려면 다음을 수행하십시오.

1. AEM 작성자 **인스턴스의 WeFinanceAutoInsurance_1_0.zip** 솔루션 패키지 `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip` 를 다운로드합니다.
1. Microsoft Dynamics 인스턴스에서 **설정 > 솔루션으로** 이동하여 가져오기를 **클릭합니다**. 패키지를 선택하고 가져옵니다.

자동 보험 적용을 위한 사용자 지정 엔티티를 가져오려면 다음을 수행하십시오.

1. AEMForms **FSIResite_1_0.zip** 패키지를 다음에서 다운로드합니다 `https://[author]:'port'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`. 패키지를 선택하고 가져옵니다.

1. Microsoft Dynamics 인스턴스에서 **설정 > 솔루션으로** 이동하여 가져오기를 **클릭합니다**. 패키지를 선택하고 가져옵니다.

고객 및 보험 정책 레코드를 가져오려면

1. AEM **작성자 인스턴스의 다음 위치에서 We.Finance Customers.csv, We.Finance Auto Insurance Reneals.csv**&#x200B;및 **홈 저당** 데이터 파일을 다운로드합니다.

   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv`
   * `https://'server':[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv`
   * `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

1. Microsoft Dynamics 인스턴스에서 다음을 수행합니다.

   * 판매 **> We** . **Finance 고객으로** 이동하고 가져오기를 **클릭합니다**.

   * 판매 **> We** . **Finance 자동 보험** 으로 이동하여 가져오기를 **클릭합니다**.

   * 판매 **> We** . **Finance 홈 저당권으로** 이동하여 가져오기를 **클릭합니다**.

## Microsoft Dynamics용 OAuth 클라우드 서비스 구성 {#configure-oauth-cloud-service-for-microsoft-dynamics}

AEM Forms과 Microsoft Dynamics 간의 통신을 사용하도록 AEM Forms에서 OAuth 클라우드 서비스를 구성합니다. AEM 작성자 및 게시 인스턴스에 대해 OAuth Cloud Service을 구성하려면 다음 단계를 수행하십시오.

1. AEM 작성자 인스턴스의 경우 **도구** > Cloud Service ******>** 데이터 소스 **>**&#x200B;글로벌으로이동합니다. Refsite **Dynamics 통합** 아이콘을 누르고 속성을 누릅니다.
1. Microsoft Azure Active Directory 계정으로 이동합니다. 등록된 응용 프로그램에 대한 회신 URL **설정에** 복사된 클라우드 서비스 구성 URL을 추가합니다. 구성을 저장합니다.
1. [인증 설정] 탭에서 **서비스 루트**, **클라이언트 ID**, **클라이언트 암호**&#x200B;및 **Microsoft Dynamics 인스턴스의 리소스 URL을 지정합니다** . Microsoft Dynamics **로그인** 페이지로 리디렉션하는 OAuth에 연결을 클릭합니다.
1. 로그인 자격 증명을 제공합니다. 로그인하면 AEM Forms 클라우드 서비스 구성 페이지로 리디렉션됩니다. **저장 후 닫기**&#x200B;를 클릭합니다. 클라우드 서비스 구성이 저장됩니다.
1. 양식 > **데이터** 통합 **>** We. **Finance로**&#x200B;이동합니다. 자동 보험(Dynamics)을 선택하고 편집을 클릭합니다. Microsoft Dynamics 엔티티는 데이터 소스 탭 아래에 나열됩니다. 모든 개체가 Microsoft Dynamics에서 반입되고 데이터 소스 탭 아래에 나열될 때까지 기다립니다.
1. AutoInsuranceRenewal **엔티티를** 선택하고 **Test Model Object를 클릭합니다**. 입력 요청 섹션에서 고객 ID에 대한 값을 &quot;900001&quot;로 지정하고 **테스트를 클릭합니다**. 출력 섹션에는 고객 ID 90001에 대해 Microsoft Dynamics에서 가져온 레코드가 표시됩니다.
1. 입력 요청 섹션에서 고객 ID에 대한 값을 &quot;900001&quot;로 지정하고 **테스트를 클릭합니다**. 출력 섹션에는 고객 ID 90001에 대해 Microsoft Dynamics에서 가져온 레코드가 표시됩니다.
1. 게시 인스턴스에 대해 1-6단계를 반복합니다.

## Adobe Sign 스케줄러 구성 {#scheduler}

작성자 및 게시 인스턴스 모두에서 다음을 수행합니다.

1. 의 AEM 웹 구성 콘솔로 이동합니다 `https://'[server]:[port]'system/console/configMgr`.
1. Adobe Sign 구성 서비스 **[!UICONTROL 를 찾아 탭하여]** 열어서 구성합니다.
1. 상태 **[!UICONTROL 업데이트 스케줄러 표현식]** 을 **0/2 * * * ?로 구성합니다**.

   >[!NOTE]
   >
   >위의 스케줄러 구성은 2분마다 Adobe Sign 서비스의 상태를 확인합니다.

1. 저장을 **[!UICONTROL 누릅니다]**.

## 참조 사이트 구성 Adobe Sign 클라우드 서비스 {#sign-service}

작성자 및 게시 인스턴스 모두에서 다음을 수행합니다.

1. 도구 > **Cloud Service****** > **Adobe Sign** **>** globalblacknowledge로이동합니다. [ **AEM Forms 참조 사이트 서명** ]을 선택하고 속성을 누릅니다.

   >[!CAUTION]
   >
   >URL이 Adobe Sign API 응용 프로그램의 OAuth 구성의 리디렉션 URL 목록에 추가되었는지 확인합니다. `https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html`

1. Adobe Sign 응용 프로그램 OAuth 구성의 클라이언트 ID와 암호를 지정합니다.
1. (선택 사항) 첨부 **[!UICONTROL 파일에 대해 Adobe Sign 사용 옵션을]** 선택하고 **[!UICONTROL Connect를 Adobe Sign에 누릅니다]**. 응용 양식에 첨부된 파일을 서명을 위해 전송된 해당 Adobe Sign 문서에 첨부합니다.
1. Adobe **[!UICONTROL Sign에 연결을]** 누르고 Adobe Sign 자격 증명으로 로그인합니다.

## 양식 일반 구성 서비스 구성 {#anonymous}

익명 사용자에 대한 액세스를 허용하려면 게시 인스턴스에서 다음을 수행합니다.

1. 의 AEM 웹 구성 콘솔로 이동합니다 `https://'[server]:[port]'/system/console/configMgr`.
1. Forms Common Configuration Service를 **[!UICONTROL 찾아 탭하여]** 열어서 구성합니다.
1. 모든 사용자에 **[!UICONTROL 대한]** 허용 **[!UICONTROL 필드를 구성합니다]**.
1. 저장을 **[!UICONTROL 누릅니다]**.

## 양식 데이터 모델에 대한 Rest 서비스 수정 {#fdm}

작성자 및 게시 인스턴스 모두에서 다음을 수행합니다.

1. CRXDE로 이동합니다 `https://'[server]:[port]'/crx/de/index.jsp`.
1. /conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile **으로 이동하여** Swagger 파일을 엽니다.
1. 환경에 따라 호스트 및 포트 설정을 업데이트합니다.
1. 설정을 저장합니다.
1. (**작성자 인스턴스만**&#x200B;해당 **) 도구** > **Cloud Service****> 데이터 소스** >전역 ****&#x200B;으로 이동합니다. Select **Rest** and tap **Properties**.Tap **Authentication Settings** and set **Authentication TypeToBasic Authentication** ****&#x200B;을 선택합니다. 서비스 `admin`에 `admin`액세스하려면 /를 사용자 이름/암호로 지정합니다. 저장 **및 닫기를 누릅니다**.

## Marketing Cloud와 통합 {#integrate-with-marketing-cloud}

AEM Forms을 Adobe Analytics 및 Adobe Target과 통합할 수 있습니다. Adobe Analytics을 사용하면 보고서를 생성하고 적응형 양식의 성능을 분석할 수 있지만 Adobe Target을 사용하면 개인화된 경험을 전달하고 적응형 양식에 대한 A/B 테스트를 수행할 수 있습니다.

AEM Forms에서 Adobe Analytics 및 Adobe Target을 구성하려면 다음을 수행합니다.

### Adobe Analytics 구성 {#configureanalytics}

Adobe Analytics과 AEM Forms의 통합을 통해 고객이 양식이나 문서를 어떻게 이용하고 있는지 모니터링하고 분석할 수 있습니다. 문제 영역을 식별하고 수정하고 전환율을 높이는 데 도움이 됩니다.

참조 사이트에서 이 기능을 경험하려면 분석 및 보고서 구성에 설명된 대로 Analytics 계정 [을 구성하십시오](../../forms/using/configure-analytics-forms-documents.md).

보고서를 생성하기 위해 시드 데이터는 참조 사이트와 번들로 제공됩니다. 시드 데이터를 사용하기 전에 다음을 수행합니다.

1. AEM cloud services에서 We.Finance 분석 구성을 사용할 수 있는지 확인합니다. 다음 방법 중 하나를 사용하여 클라우드 서비스를 찾을 수 있습니다.

   * 도구> **[!UICONTROL Cloud Service>레거시 Cloud Service]** 로 이동하거나 https://&lt;host>:&lt;port>/libs/cq/core/content/tools/cloudservices.html으로 이동합니다.
   * Cloud Service **[!UICONTROL 페이지의]** Adobe Analytics **[!UICONTROL 섹션에서 를]** 클릭합니다 `Show Configurations`. 사용 가능한 We.Finance 구성이 표시됩니다. 구성을 열려면 을 클릭합니다. 구성 페이지에서 편집을 **[!UICONTROL 클릭합니다]**. 유효한 회사, 사용자 이름, 공유 암호(암호) 및 데이터 센터를 입력하고 Analytics에 **[!UICONTROL 연결을 클릭합니다]**. 연결 성공 대화 상자가 표시되면 구성 대화 상자에서 **[!UICONTROL 확인]** 을 클릭합니다. Analytics 및 보고서 구성에 설명된 대로 Analytics 구성 [아래에 프레임워크를 구성합니다](../../forms/using/configure-analytics-forms-documents.md).

1. https://&lt;*host*>:&lt;*port*>/system/console/configMgr로 이동하여 다음을 수행합니다.

   * [ **[!UICONTROL 웹 콘솔 구성]** ] 페이지에서 **[!UICONTROL AEM Forms Analytics 구성을 찾아 클릭합니다]**.

   * AEM Forms Analytics 구성 대화 상자의 **[!UICONTROL SiteCatalyst 프레임워크]** 필드에서 we-finance(we-finance) 또는 we-gov(we-gov)를 선택합니다.
   * 저장을 **[!UICONTROL 클릭하고]** 페이지를 새로 고칩니다.

1. https://&lt;host>:&lt;port>/aem/forms에서 양식 관리자로 이동하고 다음을 수행합니다.

   * We.Finance 폴더를 열고 보고서를 볼 양식을 선택합니다.
   * 작업 도구 모음에서 Analytics 활성화를 클릭합니다. 양식에 대한 분석을 활성화한 후 Analytics 보고서를 클릭합니다. 빈 보고서가 생성될 수 있습니다. 빈 보고서가 생성된 후 데모를 위해 분석 보고서를 생성하려면 참조 사이트 패키지와 함께 제공된 시드 데이터를 제공해야 합니다.

   참조 사이트에서는 신용 카드, 집 대출 및 자녀 지원 사례에 대한 시드 데이터를 사용하여 분석 보고를 제공합니다.

### Target 구성 {#configure-target}

참조 사이트에서는 적응형 문서에 타깃팅되고 개인화된 컨텐츠를 포함할 수 있는 Adobe Target과 AEM Forms의 통합을 보여줍니다. 적응형 양식에 대한 A/B 테스트를 만들 수도 있습니다.

참조 사이트에서 통합을 경험하려면 다음을 수행하여 AEM에서 Target을 구성합니다.

1. 서버에서 A/B 테스트를 활성화하려면 jvm 인수 `-Dabtesting.enabled=true` 로 author quickstart를 시작합니다.

   >[!NOTE]
   >
   >턴키 설치에서 서비스로 시작된 JBoss에서 AEM 인스턴스가 실행 중인 경우 파일의 다음 항목에 매개 변수를 `-Dabtesting.enabled=true` `jboss\bin\standalone.conf.bat` 추가합니다.
   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. 액세스 `https://<hostname>:<port>/libs/cq/core/content/tools/cloudservices.html`.

1. Adobe Target **** 섹션에서 구성 **[!UICONTROL 표시를 클릭합니다]**. 사용 가능한 We.Finance Target 구성을 볼 수 있습니다. 구성을 열려면 을 클릭합니다. 구성 페이지에서 편집을 **[!UICONTROL 클릭합니다]**. 구성에 **[!UICONTROL 대한 구성 요소]** 편집 대화 상자가 열립니다.

1. Target 계정과 관련된 클라이언트 코드, 이메일 및 암호를 지정합니다. API 유형을 REST로 **[!UICONTROL 선택합니다]**.
1. Click **[!UICONTROL Connect to Adobe target]**. Target 계정이 성공적으로 구성되면 **[!UICONTROL 확인을 클릭합니다]**. 패키지된 구성에 Target 프레임워크이 있음을 확인할 수 있습니다.

1. 이동 `https://<hostname>:<port>/system/console/configMgr`.

1. AEM Forms Target **[!UICONTROL 구성을 클릭합니다]**.
1. Target 프레임워크을 선택합니다.
1. Target **[!UICONTROL URL]** 필드에서 AEM Forms에 대한 URL을 지정합니다. 예: `https://<hostname>:<port>/`.

1. **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

신용 카드 응용 프로그램 및 가정용 담보 대출 신청 사용 사례는 A/B 테스트를 수행하고 데모 목적으로 보고서를 보여주는 방법을 보여줍니다. 자세한 내용은 [We.Finance 참조 사이트 연습을 참조하십시오](../../forms/using/finance-reference-site-walkthrough.md).

## Next step {#next-step}

이제 모두 참조 사이트를 탐구할 수 있습니다. 참조 사이트 워크플로우 및 단계에 대한 자세한 내용은 다음을 참조하십시오.

* [We.Finance 참조 사이트 연습](../../forms/using/finance-reference-site-walkthrough.md)
* [직원 셀프 서비스 참조 사이트 연습](../../forms/using/employee-self-service-reference-site.md)

