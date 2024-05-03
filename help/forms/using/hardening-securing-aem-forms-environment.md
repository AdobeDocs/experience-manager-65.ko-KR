---
title: OSGi 환경에서 AEM Forms 강화 및 보안
description: OSGi 서버에서 AEM Forms을 보호하기 위한 권장 사항과 모범 사례를 알아봅니다.
topic-tags: Security
role: Admin,User
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# OSGi 환경에서 AEM Forms 강화 및 보안 {#hardening-and-securing-aem-forms-on-osgi-environment}

OSGi 서버에서 AEM Forms을 보호하기 위한 권장 사항과 모범 사례를 알아봅니다.

조직에서는 서버 환경을 보호하는 것이 가장 중요합니다. 이 문서에서는 AEM Forms을 실행하는 서버 보안을 위한 권장 사항 및 모범 사례에 대해 설명합니다. 이 문서는 운영 체제에 대한 포괄적인 호스트 강화 문서가 아닙니다. 대신, 이 문서에서는 배포된 응용 프로그램의 보안을 강화하기 위해 구현해야 하는 다양한 보안 강화 설정에 대해 설명합니다. 그러나 애플리케이션 서버의 보안을 유지하려면 이 문서에 제공된 권장 사항 외에 보안 모니터링, 감지 및 응답 절차도 구현해야 합니다. 이 문서에는 PII(개인 식별 정보) 보안을 위한 모범 사례와 지침도 포함되어 있습니다.

이 문서는 AEM Forms의 애플리케이션 또는 인프라 개발 및 배포 계획을 담당하는 컨설턴트, 보안 전문가, 시스템 설계자 및 IT 전문가를 대상으로 합니다. 이러한 역할에는 다음과 같은 공통 역할이 포함됩니다.

* 자체 또는 고객 조직에 보안 웹 애플리케이션과 서버를 배포해야 하는 IT 및 운영 엔지니어
* 고객 조직의 건축적 노력을 계획하는 설계자 및 계획자
* IT 보안 전문가는 조직 내 플랫폼 전반에 걸쳐 보안을 제공하는 데 주력합니다.
* 고객 및 파트너를 위한 자세한 리소스가 필요한 Adobe 및 파트너의 컨설턴트.

다음 이미지는 적절한 방화벽 토폴로지를 포함하여 일반적인 AEM Forms 배포에 사용되는 구성 요소와 프로토콜을 표시합니다.

![전형적 아키텍처](assets/typical-architecture.png)

AEM Forms은 사용자 정의가 용이하며 다양한 환경에서 작업할 수 있습니다. 일부 권장 사항은 조직에 적용되지 않을 수 있습니다.

## 보안 전송 계층 {#secure-transport-layer}

전송 계층 보안 취약성은 인터넷 연결 또는 인트라넷 연결 응용 프로그램 서버에 가장 먼저 위협되는 사항입니다. 이 섹션에서는 이러한 취약점에 대해 네트워크의 호스트를 강화하는 프로세스에 대해 설명합니다. 네트워크 세그멘테이션, TCP/IP(Transmission Control Protocol/Internet Protocol) 스택 강화 및 호스트 보호를 위한 방화벽 사용을 해결합니다.

### 열린 엔드포인트 제한  {#limit-open-endpoints}

조직에는 최종 사용자와 AEM Forms 게시 팜 간의 액세스를 제한하는 외부 방화벽이 있을 수 있습니다. 또한 조직에는 게시 팜과 조직 요소(예: 작성자 인스턴스, 처리 인스턴스, 데이터베이스) 내의 다른 팜과의 액세스를 제한하는 내부 방화벽이 있을 수 있습니다. 방화벽이 최종 사용자 및 조직 요소 내에서 제한된 수의 AEM Forms URL에 액세스할 수 있도록 허용:

#### 외부 방화벽 구성  {#configure-external-firewall}

특정 AEM Forms URL이 인터넷에 액세스할 수 있도록 외부 방화벽을 구성할 수 있습니다. 다음 URL에 액세스하려면 적응형 양식, HTML 5, 서신 관리 편지를 작성하거나 제출하거나 AEM Forms 서버에 로그인해야 합니다.

<table> 
 <tbody>
  <tr>
   <td>구성 요소</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>적응형 양식</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>HTML5 양식</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>서신 관리 </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Forms 포털 </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> AEM Forms 앱</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### 내부 방화벽 구성  {#configure-internal-firewall}

특정 AEM Forms 구성 요소(예: 작성자 인스턴스, 처리 인스턴스, 데이터베이스)가 게시 팜 및 토폴로지 다이어그램에 언급된 기타 내부 구성 요소와 통신할 수 있도록 내부 방화벽을 구성할 수 있습니다.

<table> 
 <tbody>
  <tr>
   <td>호스트<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>팜 게시(노드 게시)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>처리 서버</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Forms Workflow 추가 기능 서버(JEE 서버의 AEM Forms)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### 저장소 권한 및 ACL(액세스 제어 목록) 설정 {#setup-repository-permissions-and-access-control-lists-acls}

기본적으로 게시 노드에서 사용할 수 있는 에셋은 모든 사용자가 액세스할 수 있습니다. 모든 자산에 대해 읽기 전용 액세스가 활성화됩니다. 익명 액세스를 활성화해야 합니다. 인증된 사용자에 대해서만 양식 보기 및 제출 액세스를 제한하려는 경우 일반 그룹을 사용하여 인증된 사용자만 게시 노드에서 사용할 수 있는 에셋에 대한 읽기 전용 액세스를 허용하십시오. 다음 위치/디렉토리에는 강화(인증된 사용자의 경우 읽기 전용 액세스)가 필요한 양식 자산이 포함되어 있습니다.

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## 양식 데이터를 안전하게 처리  {#securely-handle-forms-data}

AEM Forms은 사전 정의된 위치 및 임시 폴더에 데이터를 저장합니다. 무단 사용을 방지하기 위해 데이터를 보호해야 합니다.

### 임시 폴더의 주기적 정리 설정 {#setup-periodic-cleanup-of-temporary-folder}

첨부 파일에 대한 양식을 구성하거나 구성 요소를 확인하거나 미리 볼 때 해당 데이터가 /tmp/fd/ 의 게시 노드에 저장됩니다. 데이터는 정기적으로 삭제됩니다. 보다 적극적으로 기본 데이터 제거 작업을 수정할 수 있습니다. 데이터를 제거하도록 예약된 작업을 수정하려면 AEM 웹 콘솔을 열고 AEM Forms 임시 저장소 정리 작업을 열고 Cron 표현식을 수정합니다.

위에서 언급한 시나리오에서 데이터는 인증된 사용자에 대해서만 저장됩니다. 또한 데이터는 ACL(액세스 제어 목록)을 통해 보호됩니다. 따라서 데이터 삭제를 수정하는 것은 정보를 보호하기 위한 추가적인 단계입니다.

### Forms 포털 제출 액션에 의해 저장된 데이터 보안 {#secure-data-saved-by-forms-portal-submit-action}

기본적으로 적응형 양식의 Forms 포털 제출 액션은 게시 노드의 로컬 저장소에 데이터를 저장합니다. 데이터는 /content/forms/fp에 저장됩니다. **게시 인스턴스에 데이터를 저장하지 않는 것이 좋습니다.**

게시 노드에 로컬로 저장하지 않고 처리 클러스터로 유선으로 보내도록 저장소 서비스를 구성할 수 있습니다. 처리 클러스터는 전용 방화벽 뒤의 보안 영역에 있으며 데이터는 안전하게 유지됩니다.

AEM DS 설정 서비스에 대한 처리 서버의 자격 증명을 사용하여 게시 노드에서 처리 서버로 데이터를 게시합니다. 처리 서버의 저장소에 대한 읽기-쓰기 액세스 권한이 있는 제한된 비관리 사용자의 자격 증명을 사용합니다. 자세한 내용은 [초안 및 제출을 위한 스토리지 서비스 구성](/help/forms/using/configuring-draft-submission-storage.md).

### 양식 데이터 모델(FDM)로 처리된 보안 데이터 {#secure-data-handled-by-form-data-model-fdm}

필요한 최소 권한이 있는 사용자 계정을 사용하여 FDM(양식 데이터 모델)에 대한 데이터 소스를 구성합니다. 관리 계정을 사용하면 권한이 없는 사용자에게 메타데이터 및 스키마 엔티티에 대한 개방형 액세스를 제공할 수 있습니다.\
데이터 통합은 FDM 서비스 요청을 승인하는 방법도 제공합니다. 사전 및 사후 실행 권한 부여 메커니즘을 삽입하여 요청의 유효성을 검사할 수 있습니다. 서비스 요청은 양식을 미리 채우고, 양식을 제출하고, 규칙을 통해 서비스를 호출하는 동안 생성됩니다.

**사전 처리 권한 부여:** 실행 전 프로세스 인증을 사용하여 요청의 신뢰성을 검증할 수 있습니다. 입력, 서비스 및 요청 세부 정보를 사용하여 요청 실행을 허용하거나 중지할 수 있습니다. 실행이 중지된 경우 데이터 통합 예외 OPERATION_ACCESS_DENIED를 반환할 수 있습니다. 실행을 위해 클라이언트 요청을 보내기 전에 수정할 수도 있습니다. 예: 입력 변경 및 추가 정보 추가.

**사후 프로세스 인증:** 요청자에게 결과를 반환하기 전에 사후 프로세스 인증을 사용하여 결과를 검증하고 제어할 수 있습니다. 추가 데이터를 필터링하고, 정리하고, 결과에 삽입할 수도 있습니다.

### 사용자 액세스 제한 {#limit-user-access}

작성자, 게시 및 처리 인스턴스에는 다른 사용자 가상 사용자 세트가 필요합니다. 관리자 자격 증명으로 인스턴스를 실행하지 마십시오.

**게시 인스턴스에서 다음을 수행합니다.**

* Forms-Users 그룹의 사용자만 양식을 미리 보고, 초안을 만들고, 제출할 수 있습니다.
* cm-사용자-에이전트 그룹의 사용자만 서신 관리 문자를 미리 볼 수 있습니다.
* 필수적이지 않은 모든 익명 액세스를 비활성화합니다.

**작성자 인스턴스에서 다음을 수행합니다.**

* 모든 담당자에 대해 특정 권한을 가진 사전 정의된 다른 그룹 세트가 있습니다. 그룹에 사용자를 할당합니다.

   * forms-user 그룹의 사용자:

      * 양식을 작성, 작성, 게시 및 제출할 수 있습니다.
      * xdp 기반 적응형 양식을 만들 수 없습니다.
      * 적응형 양식용 스크립트를 작성할 수 있는 권한이 없습니다.
      * xdp 또는 XDP가 포함된 패키지를 가져올 수 없음

   * forms-power-user 그룹의 사용자는 모든 유형의 양식을 작성, 작성, 게시 및 제출하고, 적응형 양식에 대한 스크립트를 작성하고, XDP가 포함된 패키지를 가져옵니다.
   * 템플릿 작성자 및 템플릿 고급 사용자는 템플릿을 미리 보고 만들 수 있습니다.
   * fdm-authors 사용자는 양식 데이터 모델을 만들고 수정할 수 있습니다.
   * cm-user-agent 그룹의 사용자는 서신 관리 문자를 만들고, 미리 보고, 게시할 수 있습니다.
   * 워크플로우 편집기 그룹의 사용자는 받은 편지함 애플리케이션 및 워크플로우 모델을 만들 수 있습니다.

**작성자 처리 시:**

* 원격 저장 및 제출 사용 사례의 경우 crx-repository의 content/form/fp 경로에 대한 읽기, 만들기 및 수정 권한이 있는 사용자를 만듭니다.
* 워크플로우 사용자 그룹에 사용자를 추가하여 사용자가 AEM 받은 편지함 애플리케이션을 사용할 수 있도록 합니다.

## AEM Forms 환경의 인트라넷 요소 보안 {#secure-intranet-elements-of-an-aem-forms-environment}

일반적으로 처리 클러스터 및 Forms Workflow 추가 기능(JEE의 AEM Forms)은 방화벽 뒤에서 실행됩니다. 따라서 이러한 기능은 안전한 것으로 간주됩니다. 이러한 환경을 강화하기 위해 몇 가지 단계를 수행할 수 있습니다.

### 보안 처리 클러스터 {#secure-processing-cluster}

처리 클러스터는 작성자 모드에서 실행되지만 개발 활동에는 사용되지 않습니다. 일반 사용자를 처리 클러스터의 콘텐츠 작성자 및 양식 사용자 그룹에 포함할 수 없습니다.

### AEM 모범 사례를 사용하여 AEM Forms 환경 보호 {#use-aem-best-practices-to-secure-an-aem-forms-environment}

이 문서에서는 AEM Forms 환경에 대한 지침을 제공합니다. 배포 시 기본 AEM 설치가 안전한지 확인해야 합니다. 자세한 지침은 [AEM Security 검사 목록](/help/sites-administering/security-checklist.md) 설명서를 참조하십시오.
