---
title: Brand Portal에서 AEM Assets 구성
seo-title: Brand Portal에서 AEM Assets 구성
description: Brand Portal에 자산 및 컬렉션을 게시하기 위해 Brand Portal에서 AEM Assets을 구성하는 방법을 알아봅니다.
seo-description: Brand Portal에 자산 및 컬렉션을 게시하기 위해 Brand Portal에서 AEM Assets을 구성하는 방법을 알아봅니다.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: ht
source-git-commit: e5e918c0b971159bc99bdcf604c89439c2b08244

---


# Brand Portal에서 AEM Assets 구성 {#configure-integration-65}

이제 AEM(Adobe Experience Manager) Assets은 Adobe I/O를 통해 Brand Portal에 구성되며, Brand Portal은 Brand Portal 임차인의 인증을 위해 IMS 토큰을 받습니다.

>[!NOTE]
>
>AEM 6.5.4.0 이상에서 Adobe I/O를 통해 Brand Portal에 AEM Assets을 구성할 수 있습니다.
>
>이전에는 Brand Portal이 기존 OAuth 게이트웨이를 통해 클래식 UI에 구성되었으며, 이 게이트웨이는 인증을 위해 IMS 액세스 토큰을 가져오는 데 JWT 토큰 교환을 사용합니다.
>
>기존 OAuth를 통한 구성은 2020년 4월 6일부터 더 이상 지원되지 않으며, Adobe I/O를 통한 구성으로 변경되었습니다.


>[!TIP]
>
>***기존 고객 전용***
>
>기존 OAuth 게이트웨이 구성을 계속 사용하는 것이 좋습니다. 기존 OAuth 게이트웨이 구성 문제가 발생하는 경우 기존 구성을 삭제하고 Adobe I/O를 통해 새 구성을 만드십시오.



이 도움말은 다음 두 가지 사용 사례에 대해 설명합니다.
* [새 구성](#configure-new-integration-65): 새 Brand Portal 사용자가 Brand Portal에서 AEM Assets 작성자 인스턴스를 구성하려는 경우 Adobe I/O에 새 구성을 만들 수 있습니다.
* [업그레이드 구성](#upgrade-integration-65): 기존 OAuth 게이트웨이에 Brand Portal로 구성된 AEM Assets 작성자 인스턴스를 사용하는 기존 Brand Portal 사용자인 경우 기존 구성을 삭제하고 Adobe I/O에 새 구성을 만드는 것이 좋습니다.

제공된 정보는 이 도움말을 읽는 사람이 다음 기술을 잘 알고 있다는 가정을 기반으로 합니다.

* Adobe Experience Manager 및 AEM 패키지 설치, 구성 및 관리

* Linux 및 Microsoft Windows 운영 체제 사용

## 전제 조건 {#prerequisites}

Brand Portal에 AEM Assets을 구성하려면 다음이 필요합니다.

* 최신 서비스 팩으로 실행 중인 AEM Assets 작성자 인스턴스.
* Brand Portal 임차인 URL.
* Brand Portal 임차인의 IMS 조직에 대한 시스템 관리자 권한이 있는 사용자.


[AEM 6.5 다운로드 및 설치](#aemquickstart)

[최신 AEM 서비스 팩 다운로드 및 설치](#servicepack)

### AEM 6.5 다운로드 및 설치 {#aemquickstart}

AEM 작성자 인스턴스를 설정하려면 AEM 6.5가 있어야 합니다. AEM을 실행하지 않은 경우 다음 위치에서 다운로드하십시오.

* 기존 AEM 고객의 경우 [Adobe 라이선스 웹 사이트](http://licensing.adobe.com)에서 AEM 6.5를 다운로드합니다.

* Adobe 파트너인 경우 [Adobe 파트너 교육 프로그램](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q)을 사용하여 AEM 6.5를 요청합니다.

AEM을 다운로드한 후 AEM 작성자 인스턴스를 설정하는 방법은 [배포 및 유지 관리](https://helpx.adobe.com/kr/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall)를 참조하십시오.

### AEM 최신 서비스 팩 다운로드 및 설치 {#servicepack}

세부 지침은 다음을 참조하십시오.

* [AEM 6.5 서비스 팩 릴리스 노트](https://helpx.adobe.com/kr/experience-manager/6-5/release-notes/sp-release-notes.html)

최신 AEM 패키지 또는 서비스 팩을 찾을 수 없는 경우 **지원 센터에 문의**&#x200B;하십시오.

## 구성 만들기 {#configure-new-integration-65}

Brand Portal에 AEM Assets을 처음 구성하는 경우 단계를 나열된 순서로 수행합니다.
1. [공개 인증서 받기](#public-certificate)
1. [Adobe I/O 통합 만들기](#createnewintegration)
1. [IMS 계정 구성 만들기](#create-ims-account-configuration)
1. [클라우드 서비스 구성](#configure-the-cloud-service)
1. [구성 테스트](#test-integration)

### IMS 구성 만들기 {#create-ims-configuration}

IMS 구성은 AEM Assets 작성자 인스턴스로 Brand Portal 임차인을 인증합니다.

IMS 구성에는 다음 두 단계가 포함됩니다.

* [공개 인증서 받기](#public-certificate)
* [IMS 계정 구성 만들기](#create-ims-account-configuration)

### 공개 인증서 받기 {#public-certificate}

공개 인증서를 사용하여 Adobe I/O에서 프로필을 인증할 수 있습니다.

1. AEM Assets 작성자 인스턴스에 로그인
기본 URL: http:// localhost:4502/aem/start.html
1. **도구** ![도구](assets/tools.png) 패널에서 **[!UICONTROL 보안]** >> **[!UICONTROL Adobe IMS 구성]**&#x200B;으로 이동합니다.

   ![Adobe IMS 계정 구성 UI](assets/ims-config1.png)

1. Adobe IMS 구성 페이지가 열립니다.

   **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

   그러면 **[!UICONTROL Adobe IMS 기술 계정 구성]** 페이지로 이동합니다.

1. 기본적으로 **인증서** 탭이 열립니다.

   **클라우드 솔루션**&#x200B;에서 **[!UICONTROL Adobe Brand Portal]**&#x200B;을 선택합니다.

1. **[!UICONTROL 새 인증서 만들기]** 확인란에 표시하고 인증서에 대한 **별칭**&#x200B;을 지정합니다. 별칭은 대화 상자의 이름 역할을 합니다.

1. **[!UICONTROL 인증서 만들기]**&#x200B;를 클릭합니다. 대화 상자가 나타납니다. **[!UICONTROL 확인]**&#x200B;을 클릭하여 공개 인증서를 생성합니다.

   ![인증서 만들기](assets/ims-config2.png)

1. **[!UICONTROL 공개 키 다운로드]**&#x200B;를 클릭하고 컴퓨터에 *AEM-Adobe-IMS.crt* 인증서 파일을 저장합니다. 이 인증서 파일은 [Adobe I/O 통합을 만드는](#createnewintegration) 데 사용됩니다.

   ![인증서 다운로드](assets/ims-config3.png)

1. **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

   **계정** 탭에서 Adobe IMS 계정을 만듭니다. 이를 위해서는 통합 세부 정보가 필요합니다. 지금은 이 페이지를 열어 두십시오.

   새 탭을 열고 [Adobe I/O 통합을 만들어](#createnewintegration) IMS 계정 구성에 대한 통합 세부 정보를 가져옵니다.

### Adobe I/O 통합 만들기 {#createnewintegration}

Adobe I/O 통합은 IMS 계정 구성을 설정하는 데 필요한 API 키, 클라이언트 암호 및 페이로드(JWT)를 생성합니다.

1. Brand Portal 임차인의 IMS 조직에 대한 시스템 관리자 권한으로 Adobe I/O 콘솔에 로그인합니다.

   기본 URL: [https://console.adobe.io/](https://console.adobe.io/)

1. **[!UICONTROL 통합 만들기]**&#x200B;를 클릭합니다.

1. **[!UICONTROL API에 액세스]**&#x200B;를 선택하고 **[!UICONTROL 계속]**&#x200B;을 클릭합니다.

   ![새 통합 만들기](assets/create-new-integration1.png)

1. 새 통합 페이지 만들기가 열립니다.

   드롭다운 목록에서 조직을 선택합니다.

   **[!UICONTROL Experience Cloud]**&#x200B;에서 **[!UICONTROL AEM Brand Portal]**&#x200B;을 선택하고 **[!UICONTROL 계속]**&#x200B;을 클릭합니다.

   Brand Portal 옵션이 비활성화되어 있는 경우 **[!UICONTROL Adobe 서비스]** 옵션 위의 드롭다운 상자에서 올바른 조직을 선택했는지 확인합니다. 조직을 모르는 경우 관리자에게 문의하십시오.

   ![통합 만들기](assets/create-new-integration2.png)

1. 통합의 이름과 설명을 지정합니다. **[!UICONTROL 컴퓨터에서 파일 선택]**&#x200B;을 클릭하고 [공개 인증서 받기](#public-certificate) 섹션에서 다운로드한 `AEM-Adobe-IMS.crt` 파일을 업로드합니다.

1. 조직의 프로필을 선택합니다.

   또는 기본 프로필 **[!UICONTROL Assets Brand Portal]**&#x200B;을 선택하고 **[!UICONTROL 통합 만들기]**&#x200B;를 클릭합니다. 통합이 생성됩니다.

1. 통합 정보를 보려면 **[!UICONTROL 통합 세부 사항 계속]**&#x200B;을 클릭합니다.

   **[!UICONTROL API 키]**&#x200B;를 복사합니다.

   **[!UICONTROL 클라이언트 암호 검색]**&#x200B;을 클릭하고 클라이언트 암호 키를 복사합니다.

   ![통합 API 키, 클라이언트 암호 및 페이로드 정보](assets/create-new-integration3.png)

1. **[!UICONTROL JWT]** 탭으로 이동하고 **[!UICONTROL JWT 페이로드]**&#x200B;를 복사합니다.

   API 키, 클라이언트 암호 키 및 JWT 페이로드 정보를 사용하여 IMS 계정 구성을 만듭니다.

### IMS 계정 구성 만들기 {#create-ims-account-configuration}

다음 단계를 수행했는지 확인합니다.

* [공개 인증서 받기](#public-certificate)
* [Adobe I/O 통합 만들기](#createnewintegration)

**IMS 계정 구성을 만드는 단계:**

1. IMS 구성 페이지를 열고 **[!UICONTROL 계정]** 탭을 엽니다. [공개 인증서 받기](#public-certificate)섹션의 끝에 페이지를 열어 두었습니다.

1. IMS 계정의 **[!UICONTROL 직책]**&#x200B;을 지정합니다.

   **[!UICONTROL 인증 서버]**&#x200B;에 URL [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)을 입력합니다.

   [Adobe I/O 통합 만들기](#createnewintegration)에서 마지막에 복사한 API 키, 클라이언트 암호 및 JWT 페이로드를 붙여 넣습니다.

   **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

   통합이 생성됩니다.

   ![IMS 계정 구성](assets/create-new-integration6.png)


1. IMS 구성을 선택하고 **[!UICONTROL 상태 확인]**&#x200B;을 클릭합니다. 대화 상자가 나타납니다.

   ]**확인**[!UICONTROL &#x200B;을 클릭합니다. 연결이 성공하면 *토큰이 검색되었습니다.* 메시지가 나타납니다.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>IMS 구성은 하나만 있어야 합니다. IMS 구성을 여러 개 만들지 마십시오.
>
>IMS 구성이 상태 검사를 통과하는지 확인합니다. 구성이 상태 검사를 통과하지 않으면 구성이 잘못된 것입니다. 이 구성을 삭제하고 유효한 새 구성을 만들어야 합니다.


### 클라우드 서비스 구성 {#configure-the-cloud-service}

Brand Portal 클라우드 서비스 구성을 만들려면 다음 단계를 수행하십시오.

1. AEM Assets 작성자 인스턴스에 로그인합니다.

   기본 URL: http:// localhost:4502/aem/start.html
1. **도구** ![도구](assets/tools.png) 패널에서 **[!UICONTROL 클라우드 서비스 >> AEM Brand Portal]**&#x200B;로 이동합니다.

   Brand Portal 구성 페이지가 열립니다.

1. **[!UICONTROL 만들기]**&#x200B;를 클릭합니다.

1. 구성의 **[!UICONTROL 제목]**&#x200B;을 지정합니다.

   [IMS 계정 구성 만들기](#create-ims-account-configuration) 단계에서 생성한 IMS 구성을 선택합니다.

   **[!UICONTROL 서비스 URL]**&#x200B;에 Brand Portal 임차인 URL을 입력합니다.

   ![](assets/create-cloud-service.png)

1. **[!UICONTROL 저장 후 닫기]**&#x200B;를 클릭합니다. 클라우드 구성이 생성됩니다. 이제 AEM Assets 작성자 인스턴스가 Brand Portal 임차인과 통합됩니다.

### 구성 테스트 {#test-integration}

1. AEM Assets 작성자 인스턴스에 로그인합니다.

   기본 URL: http:// localhost:4502/aem/start.html

1. **도구** ![도구](assets/tools.png) 패널에서 **[!UICONTROL 배포 >> 복제]**&#x200B;로 이동합니다.

   ![](assets/test-integration1.png)

1. 복제 페이지가 열립니다.

   **[!UICONTROL 작성자의 에이전트]**&#x200B;를 클릭합니다.

   ![](assets/test-integration2.png)

1. 각 임차인에 대해 4개의 복제 에이전트가 작성됩니다.

   Brand Portal 임차인의 복제 에이전트를 찾습니다.

   복제 에이전트 URL을 클릭합니다.

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >복제 에이전트가 동시에 작동하여 작업 분포를 동일하게 공유하므로 게시 속도가 원래 속도보다 4배 더 빨라집니다. 클라우드 서비스가 구성된 후에는 여러 자산의 병렬 게시를 활성화하기 위해 기본적으로 활성화된 복제 에이전트를 활성화하는 데 추가 구성이 필요하지 않습니다.

   >[!NOTE]
   >
   >일부 자산의 복제가 실패할 수 있으므로 복제 에이전트를 비활성화하지 마십시오.


1. AEM Assets 작성자와 Brand Portal 간의 연결을 확인하려면 **[!UICONTROL 연결 테스트]**&#x200B;를 클릭합니다.

   ![](assets/test-integration4.png)

1. 테스트 결과 맨 아래에서 복제가 성공했는지 확인합니다.

   ![](assets/test-integration5.png)

   >[!NOTE]
   >
   >복제 에이전트가 동시에 작동하여 작업 분포를 동일하게 공유하므로 게시 속도가 원래 속도보다 4배 더 빨라집니다. 클라우드 서비스가 구성된 후에는 여러 자산의 병렬 게시를 활성화하기 위해 기본적으로 활성화된 복제 에이전트를 활성화하는 데 추가 구성이 필요하지 않습니다.

1. 4개의 복제 에이전트 모두에 대한 테스트 결과를 하나씩 확인합니다.


   >[!NOTE]
   >
   >일부 자산의 복제가 실패할 수 있으므로 복제 에이전트를 비활성화하지 마십시오.

Brand Portal이 AEM Assets 작성자 인스턴스로 구성되었습니다. 이제 다음을 수행할 수 있습니다.

* [AEM Assets에서 Brand Portal에 자산 게시](../assets/brand-portal-publish-assets.md)
* [AEM Assets에서 Brand Portal에 폴더 게시](../assets/brand-portal-publish-folder.md)
* [AEM Assets에서 Brand Portal에 컬렉션 게시](../assets/brand-portal-publish-collection.md)
* Brand Portal 사용자가 AEM Assets에 자산을 제공하고 게시할 수 있도록 [자산 소싱](https://docs.adobe.com/content/help/ko-KR/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)을 구성합니다.

## 구성 업그레이드 {#upgrade-integration-65}

다음 단계를 나열된 순서로 수행하여 기존 구성을 업그레이드합니다.
1. [실행 중인 작업 확인](#verify-jobs)
1. [기존 구성 삭제](#delete-existing-configuration)
1. [구성 만들기](#configure-new-integration-65)

### 실행 중인 작업 확인 {#verify-jobs}

수정하기 전에 AEM Assets 작성자 인스턴스에서 게시 작업이 실행되고 있지 않은지 확인합니다. 이러한 경우 4개의 복제 에이전트를 모두 확인하고 큐가 유휴 상태인지/비어 있는지 확인할 수 있습니다.

1. AEM Assets 작성자 인스턴스에 로그인합니다.

   기본 URL: http:// localhost:4502/aem/start.html

1. **도구** ![도구](assets/tools.png) 패널에서 **[!UICONTROL 배포 >> 복제]**&#x200B;로 이동합니다.

1. 복제 페이지가 열립니다.

   **[!UICONTROL 작성자의 에이전트]**&#x200B;를 클릭합니다.

   ![](assets/test-integration2.png)

1. Brand Portal 임차인의 복제 에이전트를 찾습니다.

   모든 복제 에이전트에 대해 **큐가 유휴 상태**&#x200B;인지, 활성 상태인 게시 작업이 없는지 확인합니다.

   ![](assets/test-integration3.png)

### 기존 구성 삭제 {#delete-existing-configuration}

기존 구성을 삭제하는 동안 다음 확인 목록을 실행해야 합니다.
* 4개의 복제 에이전트 모두 삭제
* 클라우드 서비스 삭제
* MAC 사용자 삭제

1. AEM Assets 작성자 인스턴스에 로그인하고 CRX Lite를 관리자로 엽니다.

   기본 URL: http:// localhost:4502/crx/de/index.jsp

1. `/etc/replications/agents.author`로 이동하고 Brand Portal 임차인의 4개 복제 에이전트를 모두 삭제합니다.

   ![](assets/delete-replication-agent.png)

1. `/etc/cloudservices/mediaportal`로 이동하여 **클라우드 서비스 구성**&#x200B;을 삭제합니다.

   ![](assets/delete-cloud-service.png)

1. `/home/users/mac`로 이동하고 Brand Portal 임차인의 **MAC 사용자**&#x200B;를 삭제합니다.

   ![](assets/delete-mac-user.png)


이제 Adobe I/O에서 AEM 6.5 작성자 인스턴스에서 [구성을 만들 수](#configure-new-integration-65) 있습니다.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

복제가 성공하면 자산, 폴더 및 컬렉션을 Brand Portal에 게시할 수 있습니다. 자세한 내용은 다음을 참조하십시오.

* [자산을 Brand Portal에 게시](/help/assets/brand-portal-publish-assets.md)
* [폴더를 Brand Portal에 게시](/help/assets/brand-portal-publish-folder.md)
* [컬렉션을 Brand Portal에 게시](/help/assets/brand-portal-publish-collection.md)
