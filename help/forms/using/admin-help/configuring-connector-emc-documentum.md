---
title: EMC Documentum용 커넥터 구성
seo-title: EMC Documentum용 커넥터 구성
description: AEM 양식과 EMC Documentum 간 통신을 지원하기 위해 Connector for EMC Documentum을 구성하는 방법을 알아봅니다.
seo-description: AEM 양식과 EMC Documentum 간 통신을 지원하기 위해 Connector for EMC Documentum을 구성하는 방법을 알아봅니다.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 1%

---


# EMC Documentum {#configuring-connector-for-emc-documentum}용 커넥터 구성

EMC Documentum용 커넥터로 AEM 양식과 EMC Documentum 간의 통신이 가능합니다. 자세한 배경 정보는 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)의 &quot;ECM용 커넥터&quot;를 참조하십시오.

EMC Documentum용 Connector를 설정하면 서버 연결 및 저장소 자격 증명을 구성할 수 있습니다.

>[!NOTE]
>
>이전 릴리스에서 자산은 ECM 저장소에 저장될 수 있습니다. 현재 릴리스에서는 자산이 AEM 양식 기본 저장소에 저장되고 저장소 공급자 서비스는 더 이상 사용되지 않습니다. ECM 저장소에서 AEM 양식 저장소로 에셋을 마이그레이션하는 작업은 AEM 양식으로 업그레이드하는 경우 수행됩니다. 자세한 내용은 응용 프로그램 서버에 대한 AEM 양식 업그레이드 안내서를 참조하십시오.

## 서버 연결 {#configuring-the-server-connection} 구성

이 항목에서는 구성 설정 페이지에서 수행할 수 있는 Connector for EMC Documentum 작업에 대해 설명합니다.

>[!NOTE]
>
>모든 설정을 동시에 구성하는 경우 [저장]을 한 번만 클릭하면 됩니다.

### 서버 {#configure-the-server} 구성

연결 브로커 서버 정보를 구성해야 합니다. 이 정보는 Documentum 컨텐츠 저장소에 연결하고 Connector for EMC Documentum 을 시작하는 데 필요합니다.

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정을 클릭합니다.
1. Documentum 구성 정보 영역에 연결 브로커의 호스트 이름 또는 IP 주소와 포트 번호를 입력합니다. 포트 번호는 양의 정수여야 합니다(예: 1489).
1. 저장을 클릭합니다.

### 주체 자격 증명 {#configure-principal-credentials} 구성

보안 인증서를 구성할 때 제공하는 저장소 이름은 로그인 중에 명시적 저장소 이름을 제공하는지에 따라 다릅니다.

잘못된 사용자 이름 또는 암호를 입력하면 현재 서비스가 실행 중인지 여부에 따라 다음 결과가 표시됩니다.

* EMC Documentum Repository Provider Service와 EMC Documentum Content Repository Connector 서비스를 모두 중지한 경우 서비스 구성 정보를 저장할 때 오류가 표시되지 않습니다. 그러나 다음 번에 서비스를 시작하면 예외가 발생하고 서비스가 시작되지 않습니다.
* EMC Documentum Repository Provider 서비스 또는 EMC Documentum Content Repository Connector 서비스가 시작된 경우 서비스 구성 정보를 저장하면 서비스가 자격 증명 정보를 즉시 검증하려고 합니다. 이 경우 오류가 발생하고 구성 정보가 저장되지 않습니다.

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정을 클릭합니다.
1. Documentum Principal Credentials Information 영역에 super-administrator 권한이 있는 사용자의 사용자 이름과 암호를 입력합니다.
1. 로그인하는 동안 명시적 저장소 이름이 제공되지 않으면 자격 증명이 연결된 저장소 이름을 입력합니다.
1. 저장을 클릭합니다.

### 저장소 서비스 공급자 {#change-the-repository-service-provider} 변경

Documentum에서 사용할 저장소 서비스 공급자를 구성할 수 있습니다. 리포지토리 서비스 호출은 구성한 공급자에게 위임됩니다. 다음 옵션을 사용할 수 있습니다.

**현재 저장소 서비스 공급자 이름:** 현재 저장소 서비스 공급자의 이름입니다.

**ECM Documentum Repository Provider:** Documentum 저장소 공급자를 저장소의 공급자로 만듭니다. 이 옵션은 사용되지 않습니다.

**저장소 공급자:** 기본 저장소 공급자를 저장소의 공급자로 만듭니다.

>[!NOTE]
>
>나열된 저장소 서비스 공급자 이외의 저장소 서비스 공급자를 선택하려면 응용 프로그램 및 서비스 > 서비스 관리에서 RepositoryService를 구성합니다.<!-- Fix broken link (See Managing Services) -->.

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정을 클릭합니다.
1. 저장소 서비스 공급자 정보 영역에서 대체 저장소 서비스 공급자를 선택합니다.
1. 저장을 클릭합니다.

## 저장소 자격 증명 {#configuring-repository-credentials} 구성

Documentum 자격 증명 정보는 AEM 양식 시스템 컨텍스트에서 사용됩니다. 저장소 자격 증명은 Documentum의 특정 저장소에만 적용됩니다. 원하는 수의 저장소에 대한 인증서를 제공할 수 있습니다.그러나 저장소당 하나의 인증서 세트만 지정할 수 있습니다.

### 저장소 자격 증명 추가 {#add-a-repository-credential}

1. 관리 콘솔에서 서비스 > EMC Documentum용 커넥터 > 저장소 자격 증명 설정을 클릭합니다.
1. 추가를 클릭합니다. Documentum System Credentials Information 페이지가 나타납니다.
1. 저장소의 이름을 입력합니다.
1. 사용자 이름과 암호를 입력합니다.
1. 저장을 클릭합니다.

Content Repository Connector for EMC Documentum 서비스 및/또는 Repository Service for EMC Documentum이 실행 중인 경우 데이터베이스에 저장하기 전에 지정된 저장소에 대해 자격 증명 정보가 확인됩니다. 자격 증명이 잘못되었거나 있으면 오류 메시지가 표시됩니다.

### 저장소 자격 증명 제거 {#remove-a-repository-credential}

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정을 클릭합니다.
1. 저장소 옆에 있는 확인란을 선택하여 자격 증명을 제거하고 제거를 클릭합니다. 선택한 저장소에 대한 자격 증명이 데이터베이스에서 제거됩니다.

### 저장소 자격 증명 {#change-the-user-name-and-password-for-a-repository-credential}에 대한 사용자 이름 및 암호 변경

1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정을 클릭합니다.
1. 자격 증명을 편집할 저장소 이름을 클릭합니다.
1. 저장소의 사용자 이름 또는 암호 또는 둘 다를 변경합니다. (저장소 이름은 읽기 전용입니다.)
1. 저장을 클릭합니다.

Content Repository Connector for EMC Documentum 서비스 및/또는 Repository Service for EMC Documentum이 실행 중인 경우 데이터베이스에 저장하기 전에 지정된 저장소에 대해 자격 증명 정보가 확인됩니다. 자격 증명이 잘못되었거나 있으면 오류 메시지가 표시됩니다.

## 작업 공간 작업 큐 {#enable-the-request-for-sharing-of-workspace-task-queues}의 공유 요청 사용

작업 공간의 공유 요청 기능이 EMC Documentum용 Connector와 제대로 연동되도록 하려면 몇 가지 수동 단계가 필요합니다.

1. AEM 양식이 배포되고 워크벤치가 설치된 후 Workbench에 로그인하고 리소스 보기를 엽니다. 이 보기에서 QueueSharing.swf 파일의 위치를 결정합니다.
1. QueueSharing.swf 파일을 [리소스 보기]의 Windows 바탕 화면이나 운영 체제에 따라 동일한 위치로 드래그합니다.
1. 관리 콘솔에서 서비스 > Connector for EMC Documentum > 구성 설정을 클릭합니다.
1. 저장소 서비스 공급자 정보 아래에서 구성된 저장소 공급자를 EMC Documentum 저장소 공급자로 변경합니다.
1. Workbench를 시작하고 QueueSharing.swf 파일을 원래 복사한 위치(예: Windows 데스크톱 또는 다른 위치)에서 EMC Documentum 저장소 내의 기존 디렉토리로 복사합니다.
1. 워크벤치 프로세스 보기에서 대기열 공유 프로세스를 엽니다.
1. 변수 보기에서 &quot;theForm&quot; 변수의 속성을 열고 5단계에서 QueueSharing.swf 파일을 배치한 경로와 일치하도록 URI를 변경합니다.
1. 프로세스를 저장합니다.
1. 조직의 정책에 따라 프로세스를 프로덕션 환경으로 마이그레이션합니다.

