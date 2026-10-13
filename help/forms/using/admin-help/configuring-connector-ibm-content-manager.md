---
title: IBM&reg; Content Manager용 커넥터 구성
description: IBM forms와 IBM&reg; Content Manager 간에 통신할 수 있도록 AEM&reg; Content Manager용 커넥터를 구성합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 15%
---
# ® Content Manager용 커넥터 구성{#configuring-connector-for-ibm-content-manager}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

® Content Manager용 커넥터를 사용하면 AEM Forms와 IBM® Content Manager 간에 통신할 수 있습니다. 추가 배경 정보는 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)의 &#39;ECM용 커넥터&#39;를 참조하십시오.

## ® Content Manager 연결 구성 {#configure-the-ibm-content-manager-connection}

1. 관리 콘솔에서 서비스 > ® Content Manager용 커넥터 를 클릭합니다.
1. 데이터 저장소 이름 상자에 연결할 ® Content Manager 데이터 저장소의 이름을 입력합니다. 데이터베이스가 로컬인 경우 데이터베이스 이름을 입력합니다. 데이터베이스가 원격인 경우 별칭 이름을 입력합니다.
1. 사용자 이름 상자에 ® Content Manager 데이터 저장소에 연결할 사용자의 사용자 ID를 입력합니다.
1. 암호 상자에 사용자 암호를 입력합니다.
1. (선택 사항) 별칭 연결 문자열 상자에 추가 연결 인수를 입력합니다. 보통 이 상자는 비어 있어야 합니다. 자세한 내용은 ® 설명서를 참조하십시오.
1. 저장을 클릭합니다.

## 서비스 설정에 대한 유효성 검사 {#validation-of-service-settings}

잘못된 DataStore 별칭, 사용자 이름 또는 암호를 입력하면 ® Content Manager 서비스용 Content Repository Connector가 실행 중인지 여부에 따라 다음과 같은 결과가 표시됩니다.

* 서비스가 중지된 경우 서비스 구성 정보를 저장하면 오류가 나타나지 않습니다. 그러나 다음에 서비스를 시작할 때는 예외가 발생하고 서비스가 시작되지 않습니다.
* 서비스가 시작되면 서비스 구성 정보를 저장할 때 서비스가 즉시 자격 증명 정보의 유효성을 검사합니다. 이 경우 오류가 발생하고 구성 정보가 저장되지 않습니다.
