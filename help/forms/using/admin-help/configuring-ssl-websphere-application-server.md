---
title: WebSphere Application Server에 대한 SSL 구성
description: WebSphere Application Server에 대한 SSL을 구성하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '1220'
ht-degree: 100%

---

# WebSphere Application Server에 대한 SSL 구성 {#configuring-ssl-for-websphere-application-server}

이 섹션에는 IBM WebSphere Application Server에서 SSL을 구성하는 다음 단계가 포함되어 있습니다.

## WebSphere에서 로컬 사용자 계정 만들기 {#creating-a-local-user-account-on-websphere}

SSL을 활성화하려면 WebSphere가 로컬 OS 사용자 레지스트리에서 시스템을 관리할 수 있는 권한을 보유한 사용자 계정에 액세스해야 합니다.

* (Windows) 관리자 그룹에 속하고 운영 체제의 일부로 작동할 수 있는 권한을 보유한 Windows 사용자를 만듭니다. ([WebSphere용 Windows 사용자 만들기](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere)를 참조하십시오.)
* (Linux, UNIX) 사용자는 루트 사용자이거나 루트 권한을 보유한 다른 사용자일 수 있습니다. WebSphere에서 SSL을 활성화하는 경우 이 사용자의 서버 식별 및 암호를 사용합니다.

### WebSphere용 Linux 또는 UNIX 사용자 만들기 {#create-a-linux-or-unix-user-for-websphere}

1. 루트 사용자로 로그인합니다.
1. 명령 프롬프트에 다음 명령을 입력하여 사용자를 만듭니다.

   * (Linux 및 Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. 명령 프롬프트에 `passwd`를 입력하여 새 사용자의 암호를 설정합니다.
1. (Linux 및 Solaris) 명령 프롬프트에 `pwconv`(매개변수 미포함)를 입력하여 섀도 암호 파일을 만듭니다.

   >[!NOTE]
   >
   >(Linux 및 Solaris) WebSphere Application Server 로컬 OS 보안 레지스트리가 작동하려면 섀도 암호 파일이 있어야 합니다. 섀도 암호 파일은 일반적으로 **/etc/shadow**&#x200B;라는 이름이 지정되어 있으며 /etc/passwd 파일을 기반으로 합니다. 섀도 암호 파일이 없으면 전역 보안을 활성화하고 사용자 레지스트리를 로컬 OS로 구성한 후 오류가 발생합니다.

1. 텍스트 편집기에서 /etc 디렉터리의 그룹 파일을 엽니다.
1. 2단계에서 만든 사용자를 `root` 그룹에 추가합니다.
1. 파일을 저장하고 닫습니다.
1. (SSL이 활성화된 UNIX) 루트 사용자로 WebSphere를 시작하고 중지합니다.

### WebSphere용 Windows 사용자 만들기 {#create-a-windows-user-for-websphere}

1. 관리자 사용자 계정을 사용하여 Windows에 로그인합니다.
1. **시작 > 제어판 > 관리 도구 > 컴퓨터 관리 > 로컬 사용자 및 그룹**&#x200B;을 선택합니다.
1. 사용자를 마우스 오른쪽 버튼으로 클릭하고 **새 사용자**&#x200B;를 선택합니다.
1. 해당 상자에 사용자 이름 및 암호를 입력하고 나머지 상자에는 필요한 다른 정보를 입력합니다.
1. **다음 로그인 시 사용자가 암호를 변경해야 함**&#x200B;을 선택 취소하고 **만들기**&#x200B;를 클릭한 후 **닫기**&#x200B;를 클릭합니다.
1. **사용자**&#x200B;를 클릭하고 생성한 사용자를 마우스 오른쪽 버튼으로 클릭한 후 **속성**&#x200B;을 선택합니다.
1. **멤버** 탭을 클릭한 후 **추가**&#x200B;를 클릭합니다.
1. 선택할 오브젝트 이름 입력 상자에 `Administrators`를 입력하고 이름 확인을 클릭하여 그룹 이름이 올바른지 확인합니다.
1. **확인**&#x200B;을 클릭한 후 다시 **확인**&#x200B;을 클릭합니다.
1. **시작 > 제어판 > 관리 도구 > 로컬 보안 정책 > 로컬 정책**&#x200B;을 선택합니다.
1. 사용자 권한 할당을 클릭한 후 운영 체제의 일부로 작동을 마우스 오른쪽 버튼으로 클릭하고 속성을 선택합니다.
1. **사용자 또는 그룹 추가**&#x200B;를 클릭합니다.
1. 선택할 오브젝트 이름 입력 상자에 4단계에서 만든 사용자 이름을 입력하고 **이름 확인**&#x200B;을 클릭하여 이름이 올바른지 확인한 후 **확인**&#x200B;을 클릭합니다.
1. **확인**&#x200B;을 클릭하여 운영 체제의 일부로 작동 속성 대화 상자를 닫습니다.

### 새로 만든 사용자를 관리자로 사용하도록 WebSphere 구성 {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. WebSphere가 실행 중인지 확인합니다.
1. WebSphere 관리 콘솔에서 **보안 > 전역 보안**&#x200B;을 선택합니다.
1. 관리 보안에서 **관리 사용자 역할**&#x200B;을 선택합니다.
1. 추가를 클릭하고 다음 작업을 수행합니다.

   1. 검색 상자에 **&amp;ast;**&#x200B;를 입력하고 검색을 클릭합니다.
   1. 역할에서 **관리자**&#x200B;를 클릭합니다.
   1. 새로 만든 사용자를 역할에 매핑됨에 추가하고 해당 사용자를 관리자에 매핑합니다.

1. **확인**&#x200B;을 클릭하고 변경 사항을 저장합니다.
1. WebSphere 프로필을 다시 시작합니다.

## 관리 보안 활성화 {#enable-administrative-security}

1. WebSphere 관리 콘솔에서 **보안 > 전역 보안**&#x200B;을 선택합니다.
1. **보안 구성 마법사**&#x200B;를 클릭합니다.
1. **애플리케이션 보안 활성화** 확인란이 활성화되어 있는지 확인합니다. **다음**&#x200B;을 클릭합니다.
1. **페더레이션된 저장소**&#x200B;를 선택하고 **다음**&#x200B;을 클릭합니다.
1. 설정할 자격 증명을 지정하고 **다음**&#x200B;을 클릭합니다.
1. **마침**&#x200B;을 클릭합니다.
1. WebSphere 프로필을 다시 시작합니다.

   WebSphere에서 기본 키 저장소와 TrustStore를 사용하기 시작합니다.

## SSL(사용자 정의 키 및 TrustStore) 활성화 {#enable-ssl-custom-key-and-truststore}

TrustStore와 키 저장소는 iKeyman 유틸리티나 Admin Console을 사용하여 만들 수 있습니다. iKeyman이 제대로 작동하려면 WebSphere 설치 경로에 괄호가 포함되어서는안 됩니다.

1. WebSphere 관리 콘솔에서 **보안 > SSL 인증서 및 키 관리**&#x200B;를 선택합니다.
1. 관련 항목에서 **키 저장소 및 인증서**&#x200B;를 클릭합니다.
1. **키 저장소 사용** 드롭다운에서 **SSL 키 저장소**&#x200B;가 선택되어 있는지 확인합니다. **새로 만들기**&#x200B;를 클릭합니다.
1. 논리적인 이름과 설명을 입력합니다.
1. 키 저장소를 만들 경로를 지정합니다. 이미 iKeyman을 통해 키 저장소를 만든 경우 키 저장소 파일의 경로를 지정합니다.
1. 암호를 지정하고 확인합니다.
1. 키 저장소 유형을 선택하고 **적용**&#x200B;을 클릭합니다.
1. 마스터 구성을 저장합니다.
1. **개인 증명서**&#x200B;를 클릭합니다.
1. 이미 iKeyman을 사용하여 만든 키 저장소를 추가한 경우 인증서가 나타납니다. 그렇지 않으면 다음 단계를 수행하여 새로운 자체 서명 인증서를 추가해야 합니다.

   1. **만들기 > 자체 서명 인증서**&#x200B;를 선택합니다.
   1. 인증서 양식에 적절한 값을 지정합니다. 별칭과 일반 이름을 컴퓨터의 정규화된 도메인 이름으로 유지해야 합니다.
   1. **적용**&#x200B;을 클릭합니다.

1. 2~10단계를 반복하여 TrustStore를 만듭니다.

## 서버에 사용자 정의 키 저장소 및 TrustStore 적용 {#apply-custom-keystore-and-truststore-to-the-server}

1. WebSphere 관리 콘솔에서 **보안 > SSL 인증서 및 키 관리**&#x200B;를 선택합니다.
1. **엔드포인트 보안 구성 관리**&#x200B;를 클릭합니다. 로컬 토폴로지 맵이 열립니다.
1. 인바운드에서 노드의 직계 하위 항목을 선택합니다.
1. 관련 항목에서 **SSL 구성**&#x200B;을 선택합니다.
1. **NodeDeafultSSLSetting**&#x200B;을 선택합니다.
1. TrustStore 이름 및 키 저장소 이름 드롭다운 목록에서 사용자가 만든 사용자 정의 TrustStore와 키 저장소를 선택합니다.
1. **적용**&#x200B;을 클릭합니다.
1. 마스터 구성을 저장합니다.
1. WebSphere 프로필을 다시 시작합니다.

   이제 프로필이 사용자 정의 SSL 설정과 인증서를 기반으로 실행됩니다.

## AEM Forms 네이티브에 대한 지원 활성화 {#enabling-support-for-aem-forms-natives}

1. WebSphere 관리 콘솔에서 **보안 > 전역 보안**&#x200B;을 선택합니다.
1. 인증 섹션에서 **RMI/IIOP 보안**&#x200B;을 확장하고 **CSIv2 인바운드 통신**&#x200B;을 클릭합니다.
1. 전송 드롭다운 목록에서 **SSL 지원됨**&#x200B;이 선택되어 있는지 확인합니다.
1. WebSphere 프로필을 다시 시작합니다.

## https로 시작하는 URL을 변환하도록 WebSphere 구성 {#configuring-websphere-to-convert-urls-that-begins-with-https}

https로 시작하는 URL을 변환하려면 해당 URL에 대한 서명자 인증서를 WebSphere 서버에 추가합니다.

**https가 활성화된 사이트에 대한 서명자 인증서 만들기**

1. WebSphere가 실행 중인지 확인합니다.
1. WebSphere 관리 콘솔에서 서명자 인증서로 이동한 후 보안 > SSL 인증서 및 키 관리 > 키 저장소 및 인증서 > NodeDefaultTrustStore > 서명자 인증서를 클릭합니다.
1. 포트에서 가져오기를 클릭하고 다음 작업을 수행합니다.

   * 호스트 상자에 URL을 입력합니다. 예를 들어 `www.paypal.com`을 입력합니다.
   * 포트 상자에 `443`을 입력합니다. 이 포트는 기본 SSL 포트입니다.
   * 별칭 상자에 별칭을 입력합니다.

1. 서명자 정보 가져오기 클릭한 후 해당 정보를 가져왔는지 확인합니다.
1. 적용을 클릭한 후 저장을 클릭합니다.

인증서가 추가된 사이트의 HTML-PDF 변환 기능이 이제 PDF 생성 서비스에서 작동합니다.

>[!NOTE]
>
>WebSphere 내부에서 애플리케이션이 SSL 사이트에 연결하려면 서명자 인증서가 필요합니다. 이 인증서는 JSSE(Java Secure Socket Extension)에서 SSL 핸드셰이크 중에 연결의 원격 측에서 보낸 인증서의 유효성을 검사하는 데 사용됩니다.

## 동적 포트 구성 {#configuring-dynamic-ports}

전역 보안이 활성화된 경우 IBM WebSphere는 ORB.init()에 대한 여러 호출을 허용하지 않습니다. 영구 제한 사항에 대한 자세한 내용은 https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.에서 확인할 수 있습니다.

다음 단계를 수행하여 포트를 동적으로 설정하고 문제를 해결합니다.

1. WebSphere 관리 콘솔에서 **서버** > **서버 유형** > **WebSphere Application Server**&#x200B;를 선택합니다.
1. 환경 설정 섹션에서 해당 서버를 선택합니다.
1. **구성** 탭의 **통신** 섹션에서 **포트**&#x200B;를 확장하고 **세부 정보**&#x200B;를 클릭합니다.
1. 다음과 같은 포트 이름을 클릭하고 **포트 번호**&#x200B;를 0으로 변경한 후 **확인**&#x200B;을 클릭합니다.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## sling.properties 파일 구성 {#configure-the-sling-properties-file}

1. 편집을 위해 `[aem-forms_root]`\crx-repository\launchpad\sling.properties 파일을 엽니다.
1. `sling.bootdelegation.ibm` 속성을 찾아 해당 값 필드에 `com.ibm.websphere.ssl.*`를 추가합니다. 업데이트된 필드는 다음과 같습니다.

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. 파일을 저장하고 서버를 다시 시작합니다.
