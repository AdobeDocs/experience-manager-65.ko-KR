---
title: WebSphere 응용 프로그램 서버에 대한 SSL 구성
seo-title: WebSphere 응용 프로그램 서버에 대한 SSL 구성
description: WebSphere Application Server에 대한 SSL을 구성하는 방법을 알아봅니다.
seo-description: WebSphere Application Server에 대한 SSL을 구성하는 방법을 알아봅니다.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---


# WebSphere 응용 프로그램 서버에 대한 SSL 구성 {#configuring-ssl-for-websphere-application-server}

이 섹션에는 IBM WebSphere 응용 프로그램 서버와 SSL을 구성하는 다음 단계가 포함됩니다.

## WebSphere에서 로컬 사용자 계정 만들기 {#creating-a-local-user-account-on-websphere}

SSL을 활성화하려면 WebSphere에서 시스템을 관리할 권한이 있는 로컬 OS 사용자 레지스트리의 사용자 계정에 액세스해야 합니다.

* (Windows) 관리자 그룹의 일부이며 운영 체제의 일부로 사용할 권한이 있는 새 Windows 사용자를 만듭니다. WebSphere [용 Windows 사용자 만들기를 참조하십시오](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).
* (Linux, UNIX) 사용자는 루트 권한을 가진 다른 사용자나 루트 사용자일 수 있습니다. WebSphere에서 SSL을 활성화하면 이 사용자의 서버 ID와 암호를 사용하십시오.

### WebSphere용 Linux 또는 UNIX 사용자 생성 {#create-a-linux-or-unix-user-for-websphere}

1. 루트 사용자로 로그인합니다.
1. 명령 프롬프트에서 다음 명령을 입력하여 사용자를 만듭니다.

   * (Linux 및 Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. 명령 프롬프트에 입력하여 새 사용자의 암호 `passwd` 를 설정합니다.
1. (Linux 및 Solaris) 명령 프롬프트에서 매개 변수 없이 `pwconv` 를 입력하여 그림자 암호 파일을 생성합니다.

   >[!NOTE]
   >
   >(Linux 및 Solaris) WebSphere Application Server 로컬 OS 보안 레지스트리가 작동하려면 섀도 암호 파일이 있어야 합니다. 그림자 암호 파일의 이름은 **/etc/shadow** 이며 /etc/passwd 파일을 기반으로 합니다. 섀도 암호 파일이 없는 경우 전역 보안을 설정하고 사용자 레지스트리를 로컬 OS로 구성한 후 오류가 발생합니다.

1. 텍스트 편집기의 /etc 디렉토리에서 그룹 파일을 엽니다.
1. 2단계에서 만든 사용자를 `root` 그룹에 추가합니다.
1. 파일을 저장하고 닫습니다.
1. (SSL이 활성화된 UNIX) 루트 사용자로 WebSphere를 시작 및 중지합니다.

### WebSphere용 Windows 사용자 만들기 {#create-a-windows-user-for-websphere}

1. 관리자 사용자 계정을 사용하여 Windows에 로그인합니다.
1. [ **시작] > [Campaign 컨트롤 패널] > [관리 도구] > [컴퓨터 관리] > [로컬 사용자 및 그룹]을 선택합니다**.
1. 사용자를 마우스 오른쪽 단추로 클릭하고 **새 사용자를 선택합니다**.
1. 해당 상자에 사용자 이름과 암호를 입력하고 필요한 기타 정보는 나머지 상자에 입력합니다.
1. [다음 로그인 **시**&#x200B;사용자가 암호를 변경해야 함]을 선택 취소하고 [ **만들기]를 클릭한**&#x200B;다음 [ **닫기]를**&#x200B;클릭합니다.
1. 사용자 **를**&#x200B;클릭하고 방금 만든 사용자를 마우스 오른쪽 단추로 클릭하고 **속성을 선택합니다**.
1. 멤버 **탭을** 클릭한 다음 **추가를 클릭합니다**.
1. [선택할 개체 이름 입력] 상자에서 이름 확인 `Administrators`을 클릭하여 그룹 이름이 올바른지 확인합니다.
1. 확인 **을** 클릭한 다음 **확인을** 다시 클릭합니다.
1. [ **시작] > [Campaign 컨트롤 패널] > [관리 도구] > [로컬 보안 정책] > [로컬 정책]을 선택합니다**.
1. 사용자 권한 할당을 클릭한 다음 운영 체제의 일부로 역할을 마우스 오른쪽 단추로 클릭하고 속성을 선택합니다.
1. Click **Add User or Group**.
1. 선택할 개체 이름 입력 상자에 4단계에서 만든 사용자의 이름을 입력하고 이름 **확인을** 클릭하여 이름이 올바른지 확인한 다음 **확인을 클릭합니다**.
1. [ **확인** ]을 클릭하여 [운영 체제 속성] 대화 상자의 일부로 작업]을 닫습니다.

### 새로 만든 사용자를 관리자로 사용하도록 WebSphere 구성 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. WebSphere가 실행되고 있는지 확인합니다.
1. WebSphere 관리 콘솔에서 **보안 > 전역 보안을 선택합니다**.
1. 관리 보안 아래에서 관리 **사용자 역할을 선택합니다**.
1. 추가를 클릭하고 다음을 수행합니다.

   1. 입력(&amp; **P);ast;** 검색 상자에서 검색을 클릭합니다.
   1. 역할 **아래에서** 관리자를 클릭합니다.
   1. 새로 만든 사용자를 역할에 매핑합니다. 이 사용자를 관리자에게 매핑합니다.

1. Click **OK** and save your changes.
1. WebSphere 프로필을 다시 시작합니다.

## 관리 보안 활성화 {#enable-administrative-security}

1. WebSphere 관리 콘솔에서 **보안 > 전역 보안을 선택합니다**.
1. 보안 **구성 마법사를 클릭합니다**.
1. [응용 프로그램 **보안** 활성화] 확인란이 활성화되어 있는지 확인합니다. **다음**&#x200B;을 클릭합니다.
1. 통합 **리포지토리를** 선택하고 다음 **을 클릭합니다**.
1. 설정할 자격 증명을 지정하고 다음을 **클릭합니다**.
1. 마침을 **클릭합니다**.
1. WebSphere 프로필을 다시 시작합니다.

   WebSphere는 기본 키 저장소 및 truststore를 사용하기 시작합니다.

## SSL 활성화(사용자 지정 키 및 truststore) {#enable-ssl-custom-key-and-truststore}

ikeyman 유틸리티 또는 관리 콘솔을 사용하여 Truststore 및 keystore를 만들 수 있습니다. ikeyman이 제대로 작동하도록 하려면 WebSphere 설치 경로에 괄호가 포함되어 있지 않은지 확인합니다.

1. WebSphere 관리 콘솔에서 **보안 > SSL 인증서 및 키 관리를 선택합니다**.
1. 관련 항목 **아래의 키 저장소 및 인증서를** 클릭합니다.
1. [ **키 저장소 사용** ] 드롭다운에서 **SSL 키 저장소** 가 선택되어 있는지 확인합니다. **새로 만들기**&#x200B;를 클릭합니다.
1. 논리 이름과 설명을 입력합니다.
1. 키 저장소를 만들 경로를 지정합니다. ikeyman을 통해 키 저장소를 이미 만든 경우 키 저장소 파일의 경로를 지정합니다.
1. 암호를 지정하고 확인합니다.
1. 키 저장소 유형을 선택하고 적용을 **클릭합니다**.
1. 마스터 구성을 저장합니다.
1. 개인 **인증서를 클릭합니다**.
1. ikeyman을 사용하여 키 저장소를 이미 추가한 경우 인증서가 표시됩니다. 그렇지 않으면 다음 단계를 수행하여 자체 서명된 새 인증서를 추가해야 합니다.

   1. Select **Create > Self-signed Certificate**.
   1. 인증서 양식에 적절한 값을 지정합니다. 별칭과 일반 이름을 시스템의 정규화된 도메인 이름으로 유지하는지 확인합니다.
   1. 적용을 **클릭합니다**.

1. truststore를 만들려면 2-10단계를 반복합니다.

## 서버에 사용자 정의 키 스토어 및 truststore 적용 {#apply-custom-keystore-and-truststore-to-the-server}

1. WebSphere 관리 콘솔에서 **보안 > SSL 인증서 및 키 관리를 선택합니다**.
1. 끝점 **보안 구성 관리를 클릭합니다**. 로컬 토폴로지 맵이 열립니다.
1. 인바운드 아래에서 노드의 직접 하위 항목을 선택합니다.
1. 관련 항목 아래에서 **SSL 구성을 선택합니다**.
1. NodeDefaultSSLSetting **을 선택합니다**.
1. truststore 이름 및 keystore 이름 드롭다운 목록에서 만든 사용자 정의 truststore 및 keystore를 선택합니다.
1. 적용을 **클릭합니다**.
1. 마스터 구성을 저장합니다.
1. WebSphere 프로필을 다시 시작합니다.

   이제 사용자 정의 SSL 설정 및 인증서에 대해 프로필이 실행됩니다.

## AEM 양식 기본 지원 활성화 {#enabling-support-for-aem-forms-natives}

1. WebSphere 관리 콘솔에서 **보안 > 전역 보안을 선택합니다**.
1. 인증 섹션에서 **RMI/IIOP 보안을** 확장하고 **CSIv2 인바운드 통신을 클릭합니다**.
1. 전송 드롭다운 목록에서 **SSL이** 지원되는지 확인합니다.
1. WebSphere 프로필을 다시 시작합니다.

## https로 시작하는 URL을 변환하도록 WebSphere 구성 {#configuring-websphere-to-convert-urls-that-begins-with-https}

https로 시작하는 URL을 변환하려면 해당 URL에 대한 서명자 인증서를 WebSphere 서버에 추가합니다.

**https 활성화 사이트에 대한 서명자 인증서 만들기**

1. WebSphere가 실행되고 있는지 확인합니다.
1. WebSphere 관리 콘솔에서 서명자 인증서로 이동한 다음 보안 > SSL 인증서 및 키 관리 > 주요 저장소 및 인증서 > NodeDefaultTrustStore > 서명자 인증서를 클릭합니다.
1. 포트에서 검색을 클릭하고 다음 작업을 수행합니다.

   * 호스트 상자에 URL을 입력합니다. 예를 들어 를 입력합니다 `www.paypal.com`.
   * 포트 상자에 를 입력합니다 `443`. 이 포트는 기본 SSL 포트입니다.
   * 별칭 상자에 별칭을 입력합니다.

1. 서명자 정보 검색을 클릭한 다음 정보가 검색되는지 확인합니다.
1. 적용을 클릭한 다음 저장을 클릭합니다.

이제 인증서가 추가된 사이트에서 HTML을 PDF로 변환하는 기능이 PDF 생성 서비스에서 작동합니다.

>[!NOTE]
>
>응용 프로그램이 WebSphere 내에서 SSL 사이트에 연결하려면 서명자 인증서가 필요합니다. JSSE(Java Secure Socket Extensions)에서 SSL 핸드셰이크 동안 전송된 연결의 원격 측에서 보낸 인증서의 유효성을 검사하는 데 사용됩니다.

## 동적 포트 구성 {#configuring-dynamic-ports}

전역 보안이 활성화된 경우 IBM WebSphere는 ORB.init()에 대한 여러 호출을 허용하지 않습니다. 영구 제한 사항은 https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704에서 확인할 수 있습니다.

포트를 동적으로 설정하고 문제를 해결하려면 다음 단계를 수행하십시오.

1. WebSphere 관리 콘솔에서 **서버** > **서버 유형** > **WebSphere 응용 프로그램 서버를 선택합니다**.
1. 환경 설정 섹션에서 서버를 선택합니다.
1. 구성 **탭** 의 **통신** 섹션 **에서 포트**&#x200B;를 확장하고 **세부 정보**&#x200B;를클릭합니다.
1. 다음 포트 이름을 클릭하고 **포트 번호를** 0으로 변경한 다음 **확인을 클릭합니다**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## sling.properties 파일 구성 {#configure-the-sling-properties-file}

1. \crx-repository\launchpad\sling.properties `[aem-forms_root]`파일을 열어 편집할 수 있습니다.
1. 속성을 `sling.bootdelegation.ibm` 찾아 해당 값 필드 `com.ibm.websphere.ssl.*`에 추가합니다. 업데이트된 필드는 다음과 같습니다.

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 파일을 저장하고 서버를 다시 시작합니다.

