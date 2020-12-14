---
title: IBM FileNet용 커넥터 구성
seo-title: IBM FileNet용 커넥터 구성
description: AEM 양식과 IBM FileNet 간의 통신을 활성화하기 위해 Connector for IBM FileNet을 구성하는 방법에 대해 알아봅니다.
seo-description: AEM 양식과 IBM FileNet 간의 통신을 활성화하기 위해 Connector for IBM FileNet을 구성하는 방법에 대해 알아봅니다.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---


# IBM FileNet용 커넥터 구성 {#configuring-connector-for-ibm-filenet}

IBM FileNet용 커넥터를 사용하면 AEM 양식과 IBM FileNet 간의 통신이 가능합니다. 자세한 배경 정보는 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)의 &quot;ECM용 커넥터&quot;를 참조하십시오.

>[!NOTE]
>
>이전 릴리스에서 자산은 ECM 저장소에 저장될 수 있습니다. 이번 릴리스에서는 자산이 AEM 양식 기본 저장소에 저장되고 저장소 공급자 서비스는 더 이상 사용되지 않습니다. ECM 저장소에서 AEM 양식 저장소로 에셋을 마이그레이션하는 작업은 AEM 양식으로 업그레이드하는 경우 수행됩니다. 자세한 내용은 응용 프로그램 서버에 대한 AEM 양식 업그레이드 안내서를 참조하십시오.

## 컨텐트 엔진 {#configure-the-connection-to-the-content-engine}에 대한 연결 구성

IBM FileNet P8 Content Engine은 FileNet 컨텐츠 저장소에서 엔터프라이즈 컨텐츠 및 고객이 정의한 비즈니스 객체를 관리하는 소프트웨어 서비스를 제공합니다.

1. 관리 콘솔에서 서비스 > IBM FileNet용 커넥터를 클릭합니다.
1. [컨텐츠 엔진 URL] 상자에 전체 연결 URL을 입력합니다. 예:

   CEWS 전송에 FileNet Content Engine 4.x를 사용하는 경우 다음을 입력합니다.

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   WebLogic에서만 지원되는 EJB 전송과 함께 FileNet Content Engine 4.x를 사용하는 경우 다음을 입력합니다.

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 자격 증명 보호 체계 목록에서 다음 보호 수준 중 하나를 선택합니다.

   * **지우기:** 보호되지 않는 모드에서 네트워크를 통해 자격 증명을 전송합니다.
   * **대칭:** 네트워크를 통해 암호화된 자격 증명을 전송합니다.

1. [암호화 파일 위치] 상자에 암호화 파일의 경로를 입력합니다.

   * [지우기]를 자격 증명 보호 체계로 선택한 경우 이 키워드와 해당 값은 무시됩니다.
   * [대칭]을 자격 증명 보호 체계로 선택한 경우 입력하는 경로는 사용할 암호화 키가 포함된 양식 서버의 암호화 파일 위치를 가리킵니다.

1. 기본 개체 저장소 상자에서 AEM 양식에 기본적으로 연결하는 개체 저장소 커넥터를 입력합니다.
1. 사용자 이름 상자에 이전 단계에서 지정한 기본 개체 저장소에 대한 액세스 권한이 있는 사용자의 사용자 이름을 입력합니다.
1. [암호] 상자에 사용자 암호를 입력하고 [저장]을 클릭합니다.

## 프로세스 엔진 설정 {#configure-the-process-engine-settings} 구성

IBM FileNet용 커넥터에는 IBM FileNet Process Engine Connector for IBM FileNet Process Engine과 상호 작용하는 데 사용되는 Process Engine Connector for IBM FileNet 서비스가 포함되어 있습니다. 이 서비스에 대한 설정을 구성할 수 있습니다.

1. 관리 콘솔에서 서비스 > IBM FileNet용 커넥터를 클릭합니다.
1. IBM FileNet 서비스용 Process Engine Connector 사용을 활성화하려면 Process Engine Connector Service 사용을 선택합니다.
1. [프로세스 라우터/연결 지점] 상자에 호스트 이름 또는 IP 주소 및 포트 번호를 입력하고 프로세스 라우터의 이름을 입력합니다. 예:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 사용자 이름 상자에 프로세스 엔진에 연결하는 데 사용되는 사용자 이름을 입력합니다.
1. [암호] 상자에 프로세스 엔진에 연결하는 데 사용되는 암호를 입력하고 [저장]을 클릭합니다.

## 서비스 설정 유효성 검사 {#validation-of-service-settings}

컨텐트 엔진 또는 프로세스 엔진 설정에 대한 연결을 구성할 때 잘못된 사용자 이름 또는 암호를 입력할 경우 서비스가 현재 실행 중인지 여부에 따라 다음 결과가 표시됩니다.

* IBM FileNet용 저장소 공급자 서비스와 IBM FileNet용 Content Repository Connector 서비스가 모두 중지된 경우 서비스 구성 정보를 저장할 때 오류가 표시되지 않습니다. 그러나 다음 번에 서비스를 시작하면 예외가 발생하고 서비스가 시작되지 않습니다.
* IBM FileNet용 Repository Provider 서비스 또는 IBM FileNet용 Content Repository Connector 서비스가 시작된 경우 서비스 구성 정보를 저장할 때 서비스가 자격 증명 정보의 유효성을 즉시 확인합니다. 이 경우 오류가 발생하고 구성 정보가 저장되지 않습니다.

## 저장소 서비스 공급자 {#change-the-repository-service-provider} 변경

FileNet에서 사용할 저장소 서비스 공급자를 구성할 수 있습니다. 리포지토리 서비스 호출은 구성한 공급자에게 위임됩니다.

다음 옵션을 사용할 수 있습니다.

**현재 저장소 공급자 이름:** 현재 저장소 서비스 공급자의 이름입니다.

**IBM FileNet 저장소 공급자:** FileNet 저장소 공급자를 저장소의 공급자로 만듭니다. 이 옵션은 사용되지 않습니다.

**저장소 공급자:** 기본 저장소 공급자를 저장소의 공급자로 만듭니다.

>[!NOTE]
>
>나열된 저장소 서비스 공급자 이외의 저장소 서비스 공급자를 선택하려면 응용 프로그램 및 서비스에서 RepositoryService를 구성합니다.<!-- Fix broken link(See Managing Services) -->

1. 관리 콘솔에서 서비스 > IBM FileNet용 커넥터를 클릭합니다.
1. 저장소 서비스 공급자 정보 영역에서 대체 저장소 서비스 공급자를 선택한 다음 저장을 클릭합니다.
