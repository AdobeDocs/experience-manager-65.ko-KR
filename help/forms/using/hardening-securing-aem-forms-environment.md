---
title: OSGi 환경에서 AEM 양식 강화 및 보안
seo-title: OSGi 환경에서 AEM 양식 강화 및 보안
description: OSGi 서버에서 AEM Forms 보안을 유지하기 위한 권장 사항과 우수 사례를 알아봅니다.
seo-description: OSGi 서버에서 AEM Forms 보안을 유지하기 위한 권장 사항과 우수 사례를 알아봅니다.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
role: 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 0%

---


# OSGi 환경에서 AEM 양식 강화 및 보안 {#hardening-and-securing-aem-forms-on-osgi-environment}

OSGi 서버에서 AEM Forms 보안을 유지하기 위한 권장 사항과 우수 사례를 알아봅니다.

서버 환경의 보안은 조직에 가장 중요합니다. 이 문서에서는 AEM Forms을 실행하는 서버를 보호하기 위한 권장 사항과 우수 사례에 대해 설명합니다. 운영 체제에 대한 포괄적인 호스트 강화 문서가 아닙니다. 대신 이 문서에서는 배포된 응용 프로그램의 보안을 향상시키기 위해 구현해야 하는 다양한 보안 강화 설정에 대해 설명합니다. 그러나 응용 프로그램 서버가 안전한지 확인하려면 이 문서에 제공된 권장 사항 외에 보안 모니터링, 감지 및 응답 절차도 구현해야 합니다. 또한 이 문서에는 PII(개인 식별 정보)를 보호하기 위한 모범 사례와 가이드라인이 포함되어 있습니다.

이 문서는 AEM Forms의 애플리케이션 또는 인프라 개발 및 배포를 계획하는 업무를 담당하는 컨설턴트, 보안 전문가, 시스템 설계자 및 IT 전문가를 대상으로 합니다. 이러한 역할에는 다음과 같은 공통 역할이 포함됩니다.

* 자체 또는 고객 조직에 보안 웹 애플리케이션과 서버를 배포해야 하는 IT 및 운영 엔지니어
* 조직의 고객을 위한 건축 노력을 계획하는 설계자와 기획자
* 조직 내의 플랫폼 전반에서 보안을 제공하는 데 주력하는 IT 보안 전문가
* 고객과 파트너를 위한 세부 리소스가 필요한 Adobe 및 파트너의 컨설턴트

다음 이미지는 적절한 방화벽 토폴로지를 포함하여 일반적인 AEM Forms 배포에서 사용되는 구성 요소 및 프로토콜을 표시합니다.

![전형적인 아키텍처](assets/typical-architecture.png)

AEM Forms은 사용자 요구에 맞게 변경할 수 있으며 다양한 환경에서 작업할 수 있습니다. 추천 중 일부는 조직에 적용되지 않을 수 있습니다.

## 보안 전송 레이어 {#secure-transport-layer}

전송 레이어 보안 취약점은 인터넷 접속 또는 인트라넷 중심의 애플리케이션 서버에 대한 첫 번째 위협 중 하나입니다. 이 섹션에서는 이러한 취약점에 대해 네트워크의 호스트를 강화하는 프로세스에 대해 설명합니다. 네트워크 세분화, 전송 제어 프로토콜/인터넷 프로토콜(TCP/IP) 스택 강화 및 호스트 보호를 위한 방화벽 사용에 대해 다룹니다.

### 열린 끝점 제한 {#limit-open-endpoints}

조직은 최종 사용자와 AEM Forms 게시 팜 간의 액세스를 제한하는 외부 방화벽을 사용할 수 있습니다. 또한 게시 팜과 조직 요소 내 다른 요소(예: 작성 인스턴스, 처리 인스턴스, 데이터베이스) 간의 액세스를 제한하는 내부 방화벽을 조직에 포함할 수 있습니다. 방화벽이 최종 사용자 및 조직 요소 내에서 제한된 수의 AEM Forms URL에 액세스할 수 있도록 허용합니다.

#### 외부 방화벽 구성 {#configure-external-firewall}

특정 AEM Forms URL이 인터넷에 액세스할 수 있도록 외부 방화벽을 구성할 수 있습니다. 적응형 양식, HTML5, 메일 관리 서신 또는 AEM Forms 서버에 로그인하려면 다음 URL에 액세스해야 합니다.

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
   <td>통신 관리 </td> 
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

#### 내부 방화벽 구성 {#configure-internal-firewall}

특정 AEM Forms 구성 요소(예: 작성자 인스턴스, 처리 인스턴스, 데이터베이스)가 게시 팜 및 토폴로지 다이어그램에 언급된 기타 내부 구성 요소와 통신할 수 있도록 내부 방화벽을 구성할 수 있습니다.

<table> 
 <tbody>
  <tr>
   <td>호스트<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>게시 팜(게시 노드)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>처리 서버</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Forms Workflow 추가 서버(JEE 서버의 AEM Forms)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### 저장소 권한 및 ACL(액세스 제어 목록) {#setup-repository-permissions-and-access-control-lists-acls} 설정

기본적으로 게시 노드에서 사용할 수 있는 자산은 모든 사람이 액세스할 수 있습니다. 모든 자산에 대해 읽기 전용 액세스가 활성화됩니다. 익명 액세스를 활성화해야 합니다. 양식 보기를 제한하고 인증된 사용자에게만 액세스 권한을 제출하려는 경우, 공개 노드에서 사용할 수 있는 자산에 대해 인증된 사용자만 읽기 전용 액세스 권한을 갖도록 하려면 공통 그룹을 사용합니다. 다음 위치/디렉토리에는 보강이 필요한 양식 에셋이 포함되어 있습니다(인증된 사용자에 대한 읽기 전용 액세스).

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## 양식 데이터 {#securely-handle-forms-data}의 안전한 처리

AEM Forms은 사전 정의된 위치 및 임시 폴더에 데이터를 저장합니다. 무단 사용을 방지하기 위해 데이터를 보호해야 합니다.

### 임시 폴더 {#setup-periodic-cleanup-of-temporary-folder}의 정기적인 정리 설정

첨부 파일, 확인 또는 미리 보기 구성 요소에 대한 양식을 구성하면 해당 데이터가 /tmp/fd/의 게시 노드에 저장됩니다. 데이터는 정기적으로 삭제됩니다. 기본 데이터 제거 작업을 수정하여 보다 공격적으로 만들 수 있습니다. 데이터 제거로 예약된 작업을 수정하려면 AEM 웹 콘솔을 열고 AEM Forms 임시 저장소 정리 작업을 열고 Cron 표현식을 수정합니다.

위에 언급된 시나리오에서는 데이터가 인증된 사용자에 대해서만 저장됩니다. 또한 데이터는 ACL(액세스 제어 목록)으로 보호됩니다. 따라서 데이터 삭제를 수정하는 것은 정보를 보호하기 위한 추가 단계입니다.

### 양식 포털 제출 작업 {#secure-data-saved-by-forms-portal-submit-action}에 의해 저장된 보안 데이터

기본적으로 양식 포털의 적응형 양식 제출 작업은 게시 노드의 로컬 저장소에 데이터를 저장합니다. 데이터는 /content/forms/fp에 저장됩니다. **게시 인스턴스에 데이터를 저장하는 것은 권장되지 않습니다.**

게시 노드에 있는 아무 것도 저장하지 않고 over-the-wire를 처리 클러스터에 전송하도록 저장소 서비스를 구성할 수 있습니다. 처리 클러스터는 개인 방화벽 뒤에 있는 보안 영역에 있으며 데이터는 안전합니다.

AEM DS 설정 서비스에 대한 처리 서버의 자격 증명을 사용하여 게시 노드에서 처리 서버로 데이터를 게시합니다. 처리 서버 저장소에 대한 읽기-쓰기 액세스 권한이 있는 관리가 아닌 제한된 사용자의 자격 증명을 사용하는 것이 좋습니다. 자세한 내용은 초안 및 제출용 [저장소 서비스 구성을 참조하십시오](/help/forms/using/configuring-draft-submission-storage.md).

### 양식 데이터 모델(FDM) {#secure-data-handled-by-form-data-model-fdm}에 의해 처리되는 보안 데이터

최소 필수 권한이 있는 사용자 계정을 사용하여 양식 데이터 모델(FDM)에 대한 데이터 소스를 구성합니다. 관리 계정을 사용하면 권한이 없는 사용자에게 메타데이터 및 스키마 개체에 대한 오픈 액세스 권한을 제공할 수 있습니다.\
데이터 통합에서는 FDM 서비스 요청을 승인하는 방법을 제공합니다. 요청의 유효성을 확인하기 위해 사전 및 사후 실행 인증 메커니즘을 삽입할 수 있습니다. 양식을 미리 작성하고 양식을 제출하며 규칙을 통해 서비스를 호출하는 동안 서비스 요청이 생성됩니다.

**사전 프로세스 인증:** 사전 프로세스 인증을 사용하여 요청을 실행하기 전에 요청의 신뢰성을 확인할 수 있습니다. 입력, 서비스 및 요청 세부 정보를 사용하여 요청 실행을 허용하거나 중지할 수 있습니다. 실행이 중지된 경우 데이터 통합 예외 OPERATION_ACCESS_DENIED를 반환할 수 있습니다. 실행을 위해 클라이언트 요청을 보내기 전에 클라이언트 요청을 수정할 수도 있습니다. 예를 들어 입력을 변경하고 추가 정보를 추가할 수 있습니다.

**사후 처리 인증:** 결과를 요청자에게 반환하기 전에 사후 처리 권한을 사용하여 결과를 확인하고 제어할 수 있습니다. 결과에 추가 데이터를 필터링, 정리 및 삽입할 수도 있습니다.

### 사용자 액세스 제한 {#limit-user-access}

인스턴스를 작성, 게시 및 처리하려면 다른 사용자 개인 세트가 필요합니다. 관리자 자격 증명이 있는 인스턴스를 실행하지 마십시오.

**게시 인스턴스에서:**

* 양식 사용자 그룹의 사용자만 양식을 미리 보고, 초안을 만들고, 제출할 수 있습니다.
* cm-user-agent 그룹의 사용자만 통신 관리 편지를 미리 볼 수 있습니다.
* 중요하지 않은 익명 액세스를 모두 비활성화합니다.

**작성자 인스턴스에서:**

* 모든 개인 사용자에 대한 특정 권한을 갖는 다른 사전 정의된 그룹 집합이 있습니다. 그룹에 사용자를 할당합니다.

   * 양식 사용자 그룹 사용자:

      * 양식을 만들고 채우고 게시하고 제출할 수 있습니다.
      * XDP 기반 응용 양식을 만들 수 없습니다.
      * 적응형 양식에 대한 스크립트를 작성할 수 있는 권한이 없습니다.
      * XDP 또는 XDP가 포함된 패키지를 가져올 수 없습니다.
   * 양식 파워 유저 그룹의 사용자는 모든 유형의 양식을 작성, 채우기, 게시 및 제출하고 적응형 양식에 대한 스크립트를 작성하며 XDP가 포함된 패키지를 가져올 수 있습니다.
   * 템플릿 작성자 및 템플릿 파워 유저 사용자는 템플릿을 미리 보고 만들 수 있습니다.
   * fdm-authors 사용자는 양식 데이터 모델을 만들고 수정할 수 있습니다.
   * cm-user-agent 그룹의 사용자는 서신 관리 편지를 작성, 미리 보기 및 게시할 수 있습니다.
   * workflow-editors 그룹의 사용자는 받은 편지함 애플리케이션 및 워크플로우 모델을 만들 수 있습니다.


**처리 중인 작성자:**

* 원격 저장 및 제출 사용 사례를 보려면 crx-repository의 content/form/fp 경로에 대한 읽기, 생성 및 수정 권한이 있는 사용자를 만듭니다.
* 사용자가 AEM 받은 편지함 애플리케이션을 사용할 수 있도록 워크플로우 사용자 그룹에 사용자를 추가합니다.

## AEM Forms 환경의 보안 인트라넷 요소 {#secure-intranet-elements-of-an-aem-forms-environment}

일반적으로 처리 클러스터 및 Forms Workflow 추가 기능(JEE의 AEM Forms)은 방화벽 뒤에서 실행됩니다. 그래서, 이것들은 안전한 것으로 간주됩니다. 이러한 환경을 유지하기 위해 몇 가지 단계를 계속 수행할 수 있습니다.

### 보안 처리 클러스터 {#secure-processing-cluster}

처리 클러스터는 작성 모드에서 실행되지만 개발 활동에 사용하지 않습니다. 일반 사용자가 처리 클러스터의 컨텐츠 작성자 및 양식 사용자 그룹에 포함되지 않도록 합니다.

### AEM 모범 사례를 사용하여 AEM Forms 환경 {#use-aem-best-practices-to-secure-an-aem-forms-environment} 보호

이 문서에서는 AEM Forms 환경 관련 지침을 제공합니다. 배포 시 기본 AEM 설치가 안전한지 확인해야 합니다. 자세한 지침은 [AEM 보안 검사 목록](/help/sites-administering/security-checklist.md) 설명서를 참조하십시오.
