---
title: IBM FileNet용 커넥터 구성
description: AEM Forms와 IBM FileNet 간의 통신을 활성화하도록 IBM FileNet용 커넥터를 구성하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORM
exl-id: f4045df5-a35b-41d7-910e-971017148597
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '742'
ht-degree: 100%

---

# IBM FileNet용 커넥터 구성 {#configuring-connector-for-ibm-filenet}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

IBM FileNet용 커넥터를 사용하면 AEM Forms와 IBM FileNet 간의 통신이 가능합니다. 추가 배경 정보는 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)의 &#39;ECM용 커넥터&#39;를 참조하십시오.

>[!NOTE]
>
>이전 릴리스에서는 자산을 ECM 저장소에 저장할 수 있었습니다. 이 릴리스에서는 자산이 AEM Forms 기본 저장소에 저장되고 저장소 공급자 서비스는 더 이상 사용되지 않습니다. ECM 저장소에서 AEM Forms 저장소로 자산을 마이그레이션하는 작업은 AEM Forms를 업그레이드할 때 수행됩니다. 자세한 내용은 애플리케이션 서버의 AEM Forms 업그레이드 안내서를 참조하십시오.

## Content Engine에 대한 연결 구성 {#configure-the-connection-to-the-content-engine}

IBM FileNet P8 Content Engine은 FileNet 콘텐츠 저장소에서 엔터프라이즈 콘텐츠와 고객 정의 비즈니스 오브젝트를 관리하기 위한 소프트웨어 서비스를 제공합니다.

1. 관리 콘솔에서 서비스 > IBM FileNet용 커넥터를 클릭합니다.
1. Content Engine URL 상자에 전체 연결 URL을 입력합니다. 예:

   CEWS 전송 기능이 포함된 FileNet Content Engine 4.x를 사용하는 경우 다음을 입력합니다.

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   WebLogic에서만 지원되는 EJB 전송 기능이 포함된 FileNet Content Engine 4.x를 사용하는 경우 다음을 입력합니다.

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 자격 증명 보호 체계 목록에서 다음과 같은 보호 수준 중 하나를 선택합니다.

   * **암호화되지 않음:** 자격 증명을 보호되지 않은 모드로 네트워크를 통해 전송합니다.
   * **대칭:** 암호화된 자격 증명을 네트워크를 통해 전송합니다.

1. 암호화 파일 위치 상자에 암호화 파일 경로를 입력합니다.

   * 자격 증명 보호 체계로 암호화되지 않음을 선택한 경우 이 키워드와 해당 값은 무시됩니다.
   * 자격 증명 보호 체계로 대칭을 선택한 경우 입력하는 경로는 Forms 서버에서 사용할 암호화 키가 포함된 암호화 파일 위치를 가리킵니다.

1. 기본 오브젝트 저장소 상자에 AEM Forms가 기본적으로 연결하는 오브젝트 저장소 커넥터를 입력합니다.
1. 사용자 이름 상자에 이전 단계에서 지정한 기본 오브젝트 저장소에 액세스할 수 있는 권한이 있는 사용자의 사용자 이름을 입력합니다.
1. 암호 상자에 사용자의 암호를 입력하고 저장을 클릭합니다.

## Process Engine 설정 구성 {#configure-the-process-engine-settings}

IBM FileNet용 커넥터에는 IBM FileNet용 Process Engine 커넥터 서비스가 포함되어 있으며 이 서비스를 사용하여 IBM FileNet Process Engine과 상호 작용할 수 있습니다. 이 서비스에 대한 설정을 구성할 수 있습니다.

1. 관리 콘솔에서 서비스 > IBM FileNet용 커넥터를 클릭합니다.
1. IBM FileNet용 Process Engine 커넥터 서비스를 사용하도록 활성화하려면 Process Engine 커넥터 서비스 사용을 선택합니다.
1. 프로세스 라우터/연결 지점 상자에 호스트 이름 또는 IP 주소와 포트 번호를 입력한 후 프로세스 라우터 이름을 입력합니다. 예:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 사용자 이름 상자에 Process Engine에 연결하는 데 사용되는 사용자 이름을 입력합니다.
1. 암호 상자에 Process Engine에 연결하는 데 사용되는 암호를 입력하고 저장을 클릭합니다.

## 서비스 설정에 대한 유효성 검사 {#validation-of-service-settings}

Content Engine 또는 Process Engine 설정에 대한 연결을 구성할 때 잘못된 사용자 이름 또는 암호를 입력하면 서비스가 현재 실행 중인지 여부에 따라 다음과 같은 결과가 나타납니다.

* IBM FileNet용 저장소 공급자 서비스와 IBM FileNet용 콘텐츠 저장소 커넥터 서비스가 모두 중지된 경우 서비스 구성 정보를 저장하면 오류가 나타나지 않습니다. 하지만 다음에 서비스를 시작하면 예외가 발생하고 서비스가 시작되지 않습니다.
* IBM FileNet용 저장소 공급자 서비스 또는 IBM FileNet용 콘텐츠 저장소 커넥터 서비스가 시작된 경우 서비스 구성 정보를 저장하면 해당 서비스에서 즉시 자격 증명 정보의 유효성을 검사하려고 시도합니다. 이 경우 오류가 발생하고 구성 정보가 저장되지 않습니다.

## 저장소 서비스 공급자 변경 {#change-the-repository-service-provider}

FileNet에서 사용할 저장소 서비스 공급자를 구성할 수 있습니다. 저장소 서비스 호출은 사용자가 구성한 공급자에게 위임됩니다.

다음 옵션을 사용할 수 있습니다.

**현재 저장소 공급자 이름:** 현재 저장소 서비스 공급자의 이름입니다.

**IBM FileNet 저장소 공급자:** FileNet 저장소 공급자를 저장소 공급자로 설정합니다. 이 옵션은 더 이상 사용되지 않습니다.

**저장소 공급자:** 기본 저장소 공급자를 저장소 공급자로 설정합니다.

>[!NOTE]
>
>나열된 저장소 서비스 공급자가 아닌 다른 공급자를 선택하려면 애플리케이션 및 서비스에서 RepositoryService를 구성하십시오. <!-- Fix broken link(See Managing Services) -->

1. 관리 콘솔에서 서비스 > IBM FileNet용 커넥터를 클릭합니다.
1. 저장소 서비스 공급자 정보 영역에서 대체 저장소 서비스 공급자를 선택한 후 저장을 클릭합니다.
