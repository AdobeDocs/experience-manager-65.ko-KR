---
title: EMC Documentum용 커넥터 구성
description: AEM Forms와 EMC Documentum 간의 통신을 활성화하도록 EMC Documentum용 커넥터를 구성하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1032'
ht-degree: 100%

---

# EMC Documentum용 커넥터 구성 {#configuring-connector-for-emc-documentum}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

EMC Documentum용 커넥터는 AEM Forms와 EMC Documentum 간의 통신을 가능하게 합니다. 추가 배경 정보는 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)의 &#39;ECM용 커넥터&#39;를 참조하십시오.

EMC Documentum용 커넥터를 설정하려면 서버 연결과 저장소 자격 증명을 구성해야 합니다.

>[!NOTE]
>
>이전 릴리스에서는 자산을 ECM 저장소에 저장할 수 있었습니다. 현재 릴리스에서는 자산이 AEM Forms 기본 저장소에 저장되고 저장소 공급자 서비스는 더 이상 사용되지 않습니다. ECM 저장소에서 AEM Forms 저장소로 자산을 마이그레이션하는 작업은 AEM Forms를 업그레이드할 때 수행됩니다. 자세한 내용은 애플리케이션 서버의 AEM Forms 업그레이드 안내서를 참조하십시오.

## 서버 연결 구성 {#configuring-the-server-connection}

이 항목에서는 구성 설정 페이지에서 수행할 수 있는 EMC Documentum용 커넥터에 대한 작업을 설명합니다.

>[!NOTE]
>
>모든 설정을 동시에 구성하는 경우 저장을 한 번만 클릭하면 됩니다.

### 서버 구성 {#configure-the-server}

연결 브로커 서버 정보를 구성해야 합니다. 이 정보는 Documentum 콘텐츠 저장소에 연결하고 EMC Documentum용 커넥터를 시작하는 데 필요합니다.

1. 관리 콘솔에서 서비스 > EMC Documentum용 커넥터 > 구성 설정을 클릭합니다.
1. Documentum 구성 정보 영역에서 호스트 이름 또는 IP 주소와 연결 브로커의 포트 번호를 입력합니다. 포트 번호는 양의 정수여야 합니다(예: 1489).
1. 저장을 클릭합니다.

### 주체 자격 증명 구성 {#configure-principal-credentials}

주체 자격 증명을 구성할 때 제공하는 저장소 이름은 로그인 중에 명시적인 저장소 이름이 제공되는지 여부에 따라 달라집니다.

잘못된 사용자 이름 또는 암호를 입력하면 서비스가 현재 실행 중인지 여부에 따라 다음과 같은 결과가 표시됩니다.

* EMC Documentum 저장소 공급자 서비스와 EMC Documentum 콘텐츠 저장소 커넥터 서비스가 모두 중지된 경우 서비스 구성 정보를 저장하면 오류가 나타나지 않습니다. 하지만 다음에 서비스를 시작하면 예외가 발생하고 서비스가 시작되지 않습니다.
* EMC Documentum 저장소 공급자 서비스 또는 EMC Documentum 콘텐츠 저장소 커넥터 서비스가 시작된 경우 서비스 구성 정보를 저장하면 해당 서비스에서 즉시 자격 증명 정보의 유효성을 검사하려고 시도합니다. 이 경우 오류가 발생하고 구성 정보가 저장되지 않습니다.

1. 관리 콘솔에서 서비스 > EMC Documentum용 커넥터 > 구성 설정을 클릭합니다.
1. Documentum 주체 자격 증명 정보 영역에서 슈퍼 관리자 권한이 있는 사용자의 사용자 이름 및 암호를 입력합니다.
1. 로그인 중에 명시적인 저장소 이름이 제공되지 않으면 자격 증명과 연결된 저장소 이름을 입력합니다.
1. 저장을 클릭합니다.

### 저장소 서비스 공급자 변경 {#change-the-repository-service-provider}

Documentum에서 사용할 저장소 서비스 공급자를 구성할 수 있습니다. 저장소 서비스 호출은 사용자가 구성한 공급자에게 위임됩니다. 다음 옵션을 사용할 수 있습니다.

**현재 저장소 서비스 공급자 이름:** 현재 저장소 서비스 공급자의 이름입니다.

**ECM Documentum 저장소 공급자:** Documentum 저장소 공급자를 저장소 공급자로 설정합니다. 이 옵션은 더 이상 사용되지 않습니다.

**저장소 공급자:** 기본 저장소 공급자를 저장소 공급자로 설정합니다.

>[!NOTE]
>
>나열된 저장소 서비스 공급자가 아닌 다른 공급자를 선택하려면 애플리케이션 및 서비스 > 서비스 관리에서 RepositoryService를 구성하십시오. <!-- Fix broken link (See Managing Services) -->

1. 관리 콘솔에서 서비스 > EMC Documentum용 커넥터 > 구성 설정을 클릭합니다.
1. 저장소 서비스 공급자 정보 영역에서 대체 저장소 서비스 공급자를 선택합니다.
1. 저장을 클릭합니다.

## 저장소 자격 증명 구성 {#configuring-repository-credentials}

Documentum 자격 증명 정보는 AEM Forms 시스템 컨텍스트에서 사용됩니다. 저장소 자격 증명은 Documentum의 특정 저장소에만 적용됩니다. 저장소 수와 관계없이 자격 증명을 제공할 수는 있어도 저장소당 하나의 자격 증명 집합만 지정할 수 있습니다.

### 저장소 자격 증명 추가 {#add-a-repository-credential}

1. 관리 콘솔에서 서비스 > EMC Documentum용 커넥터 > 저장소 자격 증명 설정을 클릭합니다.
1. 추가를 클릭합니다. Documentum 시스템 자격 증명 정보 페이지가 나타납니다.
1. 저장소 이름을 입력합니다.
1. 사용자 이름 및 암호를 입력합니다.
1. 저장을 클릭합니다.

EMC Documentum용 콘텐츠 저장소 커넥터 서비스 및/또는 EMC Documentum용 저장소 서비스가 실행 중인 경우 자격 증명 정보는 데이터베이스에 저장되기 전에 지정된 저장소와 대조하여 확인됩니다. 자격 증명이 잘못되거나 이미 있는 경우 오류 메시지가 표시됩니다.

### 저장소 자격 증명 제거 {#remove-a-repository-credential}

1. 관리 콘솔에서 서비스 > EMC Documentum용 커넥터 > 구성 설정을 클릭합니다.
1. 자격 증명을 제거할 저장소 옆에 있는 확인란을 선택하고 제거를 클릭합니다. 선택한 저장소의 자격 증명이 데이터베이스에서 제거됩니다.

### 저장소 자격 증명의 사용자 이름 및 암호 변경 {#change-the-user-name-and-password-for-a-repository-credential}

1. 관리 콘솔에서 서비스 > EMC Documentum용 커넥터 > 구성 설정을 클릭합니다.
1. 자격 증명을 편집할 저장소 이름을 클릭합니다.
1. 저장소의 사용자 이름이나 암호 또는 둘 다를 변경합니다. (저장소 이름은 읽기 전용입니다.)
1. 저장을 클릭합니다.

EMC Documentum용 콘텐츠 저장소 커넥터 서비스 및/또는 EMC Documentum용 저장소 서비스가 실행 중인 경우 자격 증명 정보는 데이터베이스에 저장되기 전에 지정된 저장소와 대조하여 확인됩니다. 자격 증명이 잘못되거나 이미 있는 경우 오류 메시지가 표시됩니다.

## Workspace 작업 대기열 공유 요청 활성화 {#enable-the-request-for-sharing-of-workspace-task-queues}

Workspace의 작업 대기열 공유 요청 기능이 EMC Documentum용 커넥터와 함께 제대로 작동하도록 하려면 몇 가지 수동 단계가 필요합니다.

1. AEM Forms가 배포되고 워크벤치가 설치된 후 워크벤치에 로그인하여 리소스 보기를 엽니다. 이 보기에서 QueueSharing.swf 파일의 위치를 확인할 수 있습니다.
1. 운영 체제에 따라 리소스 보기에서 QueueSharing.swf 파일을 Windows 데스크탑이나 동등한 위치로 끌어다 놓습니다.
1. 관리 콘솔에서 서비스 > EMC Documentum용 커넥터 > 구성 설정을 클릭합니다.
1. 저장소 서비스 공급자 정보에서 구성된 저장소 공급자를 EMC Documentum 저장소 공급자로 변경합니다.
1. 워크벤치를 시작하고 원래 복사한 위치(예: Windows 데스크탑이나 다른 위치)에서 QueueSharing.swf 파일을 EMC Documentum 저장소 내의 기존 디렉터리로 복사합니다.
1. 워크벤치 프로세스 보기에서 대기열 공유 프로세스를 엽니다.
1. 변수 보기에서 &#39;theForm&#39; 변수의 속성을 열고 5단계에서 QueueSharing.swf 파일을 배치한 경로와 일치하도록 URI를 변경합니다.
1. 프로세스를 저장합니다.
1. 조직 정책에 따라 해당 프로세스를 프로덕션 환경으로 마이그레이션합니다.
