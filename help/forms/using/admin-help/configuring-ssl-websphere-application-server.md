---
title: WebSphere 애플리케이션 서버에 대한 SSL 구성
seo-title: Configuring SSL for WebSphere Application Server
description: WebSphere Application Server용 SSL을 구성하는 방법에 대해 알아봅니다.
seo-description: Learn how to configure SSL for WebSphere Application Server.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# WebSphere 애플리케이션 서버에 대한 SSL 구성 {#configuring-ssl-for-websphere-application-server}

이 섹션에는 IBM WebSphere Application Server를 사용하여 SSL을 구성하는 다음 단계가 포함됩니다.

## WebSphere에서 로컬 사용자 계정 만들기 {#creating-a-local-user-account-on-websphere}

SSL을 사용하려면 WebSphere는 시스템을 관리할 권한이 있는 로컬 OS 사용자 레지스트리의 사용자 계정에 액세스해야 합니다.

* (Windows) Administrators 그룹에 속하고 운영 체제의 일부로 사용할 수 있는 권한을 가진 새 Windows 사용자를 만듭니다. (참조: [WebSphere용 Windows 사용자 만들기](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) 사용자는 루트 사용자이거나 루트 권한이 있는 다른 사용자일 수 있습니다. WebSphere에서 SSL을 활성화할 때 이 사용자의 서버 ID와 암호를 사용합니다.

### WebSphere용 Linux 또는 UNIX 사용자 생성 {#create-a-linux-or-unix-user-for-websphere}

1. 루트 사용자로 로그인
1. 명령 프롬프트에 다음 명령을 입력하여 사용자를 만듭니다.

   * (Linux 및 Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. 다음을 입력하여 새 사용자의 암호 설정 `passwd` 를 입력합니다.
1. (Linux 및 Solaris) 다음을 입력하여 섀도 암호 파일을 생성합니다. `pwconv` (매개 변수 없음)을 사용합니다.

   >[!NOTE]
   >
   >(Linux 및 Solaris) WebSphere Application Server 로컬 OS 보안 레지스트리가 작동하려면 섀도 암호 파일이 있어야 합니다. 섀도 암호 파일의 이름은 일반적으로 다음과 같습니다 **/etc/shadow** /etc/passwd 파일을 기반으로 합니다. 섀도 암호 파일이 없는 경우 글로벌 보안을 활성화하고 사용자 레지스트리를 로컬 OS로 구성한 후 오류가 발생합니다.

1. 텍스트 편집기의 /etc 디렉토리에서 그룹 파일을 엽니다.
1. 2단계에서 만든 사용자를 `root` 그룹입니다.
1. 파일을 저장하고 닫습니다.
1. (SSL이 활성화된 UNIX) 루트 사용자로 WebSphere를 시작 및 중지합니다.

### WebSphere용 Windows 사용자 만들기 {#create-a-windows-user-for-websphere}

1. 관리자 사용자 계정을 사용하여 Windows에 로그인합니다.
1. 선택 **시작 > Campaign 컨트롤 패널 > 관리 도구 > 컴퓨터 관리 > 로컬 사용자 및 그룹**.
1. 사용자 를 마우스 오른쪽 단추로 클릭하고 를 선택합니다. **새 사용자**.
1. 해당 상자에 사용자 이름과 암호를 입력하고 나머지 상자에 필요한 다른 정보를 입력합니다.
1. 선택 취소 **사용자는 다음 로그인 시 암호를 변경해야 합니다.**, 클릭 **만들기**&#x200B;을 클릭한 다음 을 클릭합니다 **닫기**.
1. 클릭 **사용자**&#x200B;을 클릭하고 방금 만든 사용자를 마우스 오른쪽 단추로 클릭한 다음 를 선택합니다 **속성**.
1. 다음을 클릭합니다. **구성원** tab을 누른 다음 **추가**.
1. 선택할 개체 이름 입력 상자에 `Administrators`그룹 이름이 올바른지 확인하려면 이름 확인 을 클릭합니다.
1. 클릭 **확인** 그런 다음 을 클릭합니다. **확인** 다시.
1. 선택 **시작 > Campaign 컨트롤 패널 > 관리 도구 > 로컬 보안 정책 > 로컬 정책**.
1. 사용자 권한 할당을 클릭한 다음 운영 체제의 일부로 작업 을 마우스 오른쪽 단추로 클릭하고 속성을 선택합니다.
1. 클릭 **사용자 또는 그룹 추가**.
1. 선택할 개체 이름 입력 상자에 4단계에서 만든 사용자 이름을 입력하고 **이름 확인** 이름이 올바른지 확인한 다음 **확인**.
1. 클릭 **확인** 운영 체제 속성의 일부로 사용 대화 상자를 닫습니다.

### 새로 생성된 사용자를 관리자로 사용하도록 WebSphere 구성 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. WebSphere가 실행 중인지 확인합니다.
1. WebSphere 관리 콘솔에서 을 선택합니다. **보안 > 전역 보안**.
1. 관리 보안에서 **관리자 역할**.
1. 추가 를 클릭하고 다음을 수행합니다.

   1. 유형 **&amp;ast;** 검색 상자에서 검색을 클릭합니다.
   1. 클릭 **관리자** 역할 아래에 있어야 합니다.
   1. 새로 생성된 사용자를 매핑된 역할에 추가하고 관리자에게 매핑합니다.

1. 클릭 **확인** 변경 내용을 저장합니다.
1. WebSphere 프로필을 다시 시작합니다.

## 관리 보안 활성화 {#enable-administrative-security}

1. WebSphere 관리 콘솔에서 을 선택합니다. **보안 > 전역 보안**.
1. 클릭 **보안 구성 마법사**.
1. 확인 **응용 프로그램 보안 활성화** 확인란이 활성화되어 있습니다. **다음**&#x200B;을 클릭합니다.
1. 선택 **연합된 저장소** 및 클릭 **다음**.
1. 설정할 자격 증명을 지정하고 **다음**.
1. 클릭 **완료**.
1. WebSphere 프로필을 다시 시작합니다.

   WebSphere는 기본 키 저장소 및 인증서 저장소를 사용하여 시작됩니다.

## SSL 활성화(사용자 지정 키 및 Truststore) {#enable-ssl-custom-key-and-truststore}

ikeyman 유틸리티 또는 관리 콘솔을 사용하여 Truststore 및 keystores를 만들 수 있습니다. ikeyman이 제대로 작동하도록 하려면 WebSphere 설치 경로에 괄호가 포함되어 있지 않아야 합니다.

1. WebSphere 관리 콘솔에서 을 선택합니다. **보안 > SSL 인증서 및 키 관리**.
1. 클릭 **키스톤 및 인증서** 관련 항목 아래의 제품에서 사용할 수 있습니다.
1. 다음에서 **키 저장소 사용** 드롭다운, 다음을 확인합니다. **SSL 키스톤** 이(가) 선택되어 있습니다. 클릭 **신규**.
1. 논리적 이름과 설명을 입력합니다.
1. 키 저장소를 만들 경로를 지정합니다. ikeyman을 통해 이미 키 저장소를 생성한 경우 키 저장소 파일의 경로를 지정합니다.
1. 암호를 지정하고 확인합니다.
1. 키 저장소 유형을 선택하고 **적용**.
1. 마스터 구성을 저장합니다.
1. 클릭 **개인 인증서**.
1. 이미 ikeyman을 사용하여 키 저장소를 생성한 를 추가한 경우 인증서가 나타납니다. 그렇지 않으면 다음 단계를 수행하여 새 자체 서명된 인증서를 추가해야 합니다.

   1. 선택 **만들기 > 자체 서명된 인증서**.
   1. 인증서 양식에서 적절한 값을 지정합니다. 별칭 및 일반 이름을 시스템의 정규화된 도메인 이름으로 유지해야 합니다.
   1. 클릭 **적용**.

1. 인증서 보관함을 만들려면 2단계부터 10단계까지 반복합니다.

## 서버에 사용자 지정 키 저장소 및 인증서 저장소 적용 {#apply-custom-keystore-and-truststore-to-the-server}

1. WebSphere 관리 콘솔에서 을 선택합니다. **보안 > SSL 인증서 및 키 관리**.
1. 클릭 **끝점 보안 구성 관리**. 로컬 토폴로지 맵이 열립니다.
1. 인바운드 아래에서 직접 노드 하위를 선택합니다.
1. 관련 항목에서 다음을 선택합니다. **SSL 구성**.
1. 선택 **NodeDefaultSSLetting**.
1. 인증서 보관함 이름 및 인증서 보관함 이름 드롭다운 목록에서 생성한 사용자 지정 인증서 보관함 및 인증서 보관함을 선택합니다.
1. 클릭 **적용**.
1. 마스터 구성을 저장합니다.
1. WebSphere 프로필을 다시 시작합니다.

   이제 프로필이 사용자 정의 SSL 설정 및 인증서에서 실행됩니다.

## AEM Forms Native에 대한 지원 활성화 {#enabling-support-for-aem-forms-natives}

1. WebSphere 관리 콘솔에서 을 선택합니다. **보안 > 전역 보안**.
1. Authentication 섹션에서 다음을 확장합니다. **RMI/IIOP 보안** 및 클릭 **CSIv2 인바운드 통신**.
1. 다음을 확인합니다. **SSL 지원** 전송 드롭다운 목록에서 을(를) 선택합니다.
1. WebSphere 프로필을 다시 시작합니다.

## https로 시작하는 URL을 변환하도록 WebSphere 구성 {#configuring-websphere-to-convert-urls-that-begins-with-https}

https로 시작하는 URL을 변환하려면 해당 URL에 대한 서명자 인증서를 WebSphere 서버에 추가합니다.

**https가 활성화된 사이트에 대한 서명자 인증서 만들기**

1. WebSphere가 실행 중인지 확인합니다.
1. WebSphere 관리 콘솔에서 서명자 인증서로 이동한 다음 보안 > SSL 인증서 및 키 관리 > 키 저장소 및 인증서 > NodeDefaultTrustStore > 서명자 인증서 를 클릭합니다.
1. 포트에서 검색 을 클릭하고 다음 작업을 수행합니다.

   * 호스트 상자에 URL을 입력합니다. 예, 유형 `www.paypal.com`.
   * 포트 상자에 을 입력합니다 `443`. 이 포트는 기본 SSL 포트입니다.
   * 별칭 상자에 별칭을 입력합니다.

1. 서명자 정보 가져오기 를 클릭한 다음 정보가 검색되었는지 확인합니다.
1. 적용 을 클릭한 다음 저장 을 클릭합니다.

인증서가 추가된 사이트의 HTML-PDF 전환은 이제 PDF 생성 서비스에서 작동합니다.

>[!NOTE]
>
>응용 프로그램이 WebSphere 내에서 SSL 사이트에 연결하려면 서명자 인증서가 필요합니다. JSSE(Java Secure Socket Extensions)에서 SSL 핸드셰이크 중에 연결의 원격 쪽이 보낸 인증서의 유효성을 검사하는 데 사용됩니다.

## 동적 포트 구성 {#configuring-dynamic-ports}

글로벌 보안이 활성화된 경우 IBM WebSphere에서 ORB.init()에 대한 여러 호출을 허용하지 않습니다. 영구적 제한 사항은 https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704에서 읽어볼 수 있습니다.

다음 단계를 수행하여 포트를 동적으로 설정하고 문제를 해결합니다.

1. WebSphere 관리 콘솔에서 을 선택합니다. **서버** > **서버 유형** > **WebSphere 애플리케이션 서버**.
1. 기본 설정 섹션에서 서버를 선택합니다.
1. 다음에서 **구성** 탭, 아래 **통신** 섹션, 확장 **포트**, 및 클릭 **세부 사항**.
1. 다음 포트 이름을 클릭하고 **포트 번호** 을 0으로 설정하고 **확인**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## sling.properties 파일 구성 {#configure-the-sling-properties-file}

1. 열기 `[aem-forms_root]`편집할 \crx-repository\launchpad\sling.properties 파일입니다.
1. 를 찾습니다. `sling.bootdelegation.ibm` 속성 및 추가 `com.ibm.websphere.ssl.*`값 필드로 이동합니다. 업데이트된 필드는 다음과 같습니다.

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 파일을 저장하고 서버를 다시 시작합니다.
