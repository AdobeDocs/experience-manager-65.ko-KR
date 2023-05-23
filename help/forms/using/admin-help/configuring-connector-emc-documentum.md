---
title: EMC Documentum용 커넥터 구성
seo-title: Configuring Connector for EMC Documentum
description: AEM Forms와 EMC Documentum 간의 통신이 가능하도록 Connector for EMC Documentum을 구성하는 방법에 대해 알아봅니다.
seo-description: Learn how to configure the Connector for EMC Documentum to enable communication between AEM forms and EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# EMC Documentum용 커넥터 구성 {#configuring-connector-for-emc-documentum}

EMC Documentum용 커넥터를 사용하면 AEM Forms와 EMC Documentum 간의 통신이 가능합니다. 추가 배경 정보는 의 &quot;ECM용 커넥터&quot;를 참조하십시오. [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

EMC Documentum용 커넥터 설정에는 서버 접속 및 저장소 자격 증명 구성이 포함됩니다.

>[!NOTE]
>
>이전 릴리스에서는 자산을 ECM 저장소에 저장할 수 있었습니다. 현재 릴리스에서 에셋은 AEM Forms 기본 저장소에 저장되고 Repository Provider 서비스는 더 이상 사용되지 않습니다. ECM 저장소에서 AEM Forms 저장소로 에셋을 마이그레이션하는 작업은 AEM Forms로 업그레이드를 수행할 때 수행됩니다. 자세한 내용은 애플리케이션 서버에 대한 AEM forms 업그레이드 안내서를 참조하십시오.

## 서버 연결 구성 {#configuring-the-server-connection}

이 항목에서는 구성 설정 페이지에서 수행할 수 있는 EMC Documentum용 Connector 작업에 대해 설명합니다.

>[!NOTE]
>
>모든 설정을 동시에 구성하는 경우 한 번만 저장 을 클릭하면 됩니다.

### 서버 구성 {#configure-the-server}

연결 브로커 서버 정보를 구성해야 합니다. 이 정보는 Documentum 컨텐츠 저장소에 연결하고 Connector for EMC Documentum을 시작하는 데 필요합니다.

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정 을 클릭합니다.
1. Documentum Configuration Information 영역에 호스트 이름이나 IP 주소 및 연결 브로커의 포트 번호를 입력합니다. 포트 번호는 양의 정수(예: 1489)여야 합니다.
1. 저장을 클릭합니다.

### 사용자 자격 증명 구성 {#configure-principal-credentials}

주도자 자격 증명을 구성할 때 제공하는 저장소 이름은 로그인 중에 명시적 저장소 이름을 제공했는지 여부에 따라 달라집니다.

잘못된 사용자 이름 또는 암호를 입력하면 서비스가 현재 실행 중인지 여부에 따라 다음과 같은 결과를 얻을 수 있습니다.

* EMC Documentum Repository Provider 서비스와 EMC Documentum Content Repository Connector 서비스가 모두 중지된 경우 서비스 구성 정보를 저장하면 오류가 나타나지 않습니다. 하지만 다음에 서비스를 시작할 때는 예외가 발생하고 서비스가 시작되지 않습니다.
* EMC Documentum Repository Provider Service 또는 EMC Documentum Content Repository Connector Service가 시작되면 서비스 구성 정보를 저장하면 서비스가 즉시 자격 증명 정보의 유효성을 검사합니다. 이 경우 오류가 발생하여 구성 정보가 저장되지 않습니다.

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정 을 클릭합니다.
1. Documentum Principal Credentials Information 영역에 수퍼 관리자 권한을 가진 사용자의 사용자 이름과 암호를 입력합니다.
1. 로그인 중에 명시적 저장소 이름이 제공되지 않으면 자격 증명과 연관된 저장소 이름을 입력합니다.
1. 저장을 클릭합니다.

### 저장소 서비스 공급자 변경 {#change-the-repository-service-provider}

Documentum에서 사용할 저장소 서비스 공급자를 구성할 수 있습니다. 저장소 서비스 호출은 사용자가 구성하는 공급자에게 위임됩니다. 다음 옵션을 사용할 수 있습니다.

**현재 저장소 서비스 공급자 이름:** 현재 저장소 서비스 공급자의 이름입니다.

**ECM Documentum Repository Provider:** Documentum 저장소 공급자를 저장소 공급자로 지정합니다. 이 옵션은 더 이상 사용되지 않습니다

**저장소 공급자:** 기본 리포지토리 공급자를 리포지토리 공급자로 만듭니다.

>[!NOTE]
>
>나열된 저장소 서비스 공급자 이외의 저장소 서비스 공급자를 선택하려면 응용 프로그램 및 서비스 > 서비스 관리에서 RepositoryService를 구성합니다. <!-- Fix broken link (See Managing Services) -->.

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정 을 클릭합니다.
1. 저장소 서비스 공급자 정보 영역에서 대체 저장소 서비스 공급자를 선택합니다.
1. 저장을 클릭합니다.

## 저장소 자격 증명 구성 {#configuring-repository-credentials}

Documentum 자격 증명 정보는 AEM Forms 시스템 컨텍스트에서 사용됩니다. 저장소 자격 증명은 Documentum의 특정 저장소에 한정됩니다. 여러 저장소에 대한 자격 증명을 제공할 수 있지만 저장소당 하나의 자격 증명 집합만 지정할 수 있습니다.

### 저장소 자격 증명 추가 {#add-a-repository-credential}

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 저장소 자격 증명 설정 을 클릭합니다.
1. 추가를 클릭합니다. Documentum 시스템 인증서 정보 페이지가 나타납니다.
1. 저장소 이름을 입력합니다.
1. 사용자 이름과 암호를 입력합니다.
1. 저장을 클릭합니다.

EMC Documentum Service용 Content Repository Connector 및/또는 EMC Documentum용 Repository Service가 실행 중인 경우 데이터베이스에 저장되기 전에 지정된 저장소에 대해 자격 증명 정보를 확인합니다. 자격 증명이 유효하지 않거나 존재하는 경우 오류 메시지가 표시됩니다.

### 저장소 자격 증명 제거 {#remove-a-repository-credential}

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정 을 클릭합니다.
1. 자격 증명을 제거할 저장소 옆의 확인란을 선택하고 제거를 클릭합니다. 선택한 저장소의 자격 증명이 데이터베이스에서 제거됩니다.

### 저장소 자격 증명의 사용자 이름 및 암호 변경 {#change-the-user-name-and-password-for-a-repository-credential}

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정 을 클릭합니다.
1. 자격 증명을 편집할 저장소의 이름을 클릭합니다.
1. 저장소의 사용자 이름, 암호 또는 둘 다를 변경합니다. 저장소 이름은 읽기 전용입니다.
1. 저장을 클릭합니다.

EMC Documentum Service용 Content Repository Connector 및/또는 EMC Documentum용 Repository Service가 실행 중인 경우 데이터베이스에 저장되기 전에 지정된 저장소에 대해 자격 증명 정보를 확인합니다. 자격 증명이 유효하지 않거나 존재하는 경우 오류 메시지가 표시됩니다.

## 작업 영역 작업 큐 공유 요청 활성화 {#enable-the-request-for-sharing-of-workspace-task-queues}

Workspace의 작업 대기열 공유 요청 기능이 Connector for EMC Documentum에서 제대로 작동하도록 하려면 몇 가지 수동 단계가 필요합니다.

1. AEM Forms가 배포되고 Workbench가 설치되면 Workbench에 로그인하고 리소스 보기를 엽니다. 이 보기에서 QueueSharing.swf 파일의 위치를 확인합니다.
1. 리소스 보기에서 QueueSharing.swf 파일을 운영 체제에 따라 Windows 바탕 화면이나 이와 동등한 위치로 드래그합니다.
1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정 을 클릭합니다.
1. Repository Service Provider 정보에서 구성된 저장소 공급자를 EMC Documentum 저장소 공급자로 변경합니다.
1. Workbench를 시작하고 QueueSharing.swf 파일을 원래 복사한 위치(예: Windows 데스크톱 또는 다른 위치)에서 EMC Documentum 저장소 내의 기존 디렉토리로 복사합니다.
1. 워크벤치 프로세스 뷰에서 대기열 공유 프로세스를 엽니다.
1. 변수 보기에서 &quot;theForm&quot; 변수의 속성을 열고 5단계에서 QueueSharing.swf 파일을 만든 경로와 일치하도록 URI를 변경합니다.
1. 프로세스를 저장합니다.
1. 조직의 정책에 따라 프로세스를 프로덕션 환경으로 마이그레이션합니다.
