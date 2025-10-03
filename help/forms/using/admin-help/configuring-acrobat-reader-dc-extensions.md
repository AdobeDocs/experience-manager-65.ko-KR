---
title: 데이터 캡처를 위한 Acrobat Reader DC 확장 프로그램 구성
description: 데이터 캡처를 위한 Acrobat Reader DC 확장 프로그램을 구성하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0f8e1e46-4fc5-43f6-abb1-19a3f20e1f1d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '327'
ht-degree: 100%

---

# 데이터 캡처를 위한 Acrobat Reader DC 확장 프로그램 구성 {#configuring-acrobat-reader-dc-extensions-for-data-capture}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

AEM Forms 설치 사용자가 콘텐츠 서비스(더 이상 사용되지 않음)의 데이터 캡처 기능을 사용하는 경우 해당 사용자에게 읽기 전용 액세스 권한이 있는 역할을 만드는 것이 좋습니다.

***참고&#x200B;**: Adobe® LiveCycle® Content Services ES(더 이상 사용되지 않음)는 LiveCycle과 함께 설치되는 콘텐츠 관리 시스템입니다. 이를 통해 사용자는 인간 중심 프로세스를 설계, 관리, 모니터링 및 최적화할 수 있습니다. 콘텐츠 서비스(더 이상 사용되지 않음) 지원은 2014년 12월 31일에 종료되었습니다. [Adobe 제품 수명 주기 문서](https://helpx.adobe.com/kr/support/programs/eol-matrix.html)를 참조하십시오.*

데이터 캡처를 수행하려면 SampleReaderExtensionsCredential에 액세스하기 위한 사용자 역할을 할당해야 합니다. 표준 신뢰 관리자 역할을 할당할 수도 있습니다. 하지만 이 역할은 관리자가 아닌 일반 사용자에게 PKI 신뢰 설정을 제어하고 PKI 자격 증명을 관리하는 관리자 권한을 부여하므로 프로덕션 환경에서 AEM Forms 설치 보안이 손상될 수 있습니다. AEM Forms 시스템 관리자가 Trust Store에 대한 읽기 전용 액세스 권한만 부여하는 역할을 만들고 데이터 캡처를 사용하는 관리자가 아닌 사용자에게 이 새 역할을 할당하는 것이 좋습니다.

## 데이터 캡처 사용자를 위한 역할 만들기 {#create-a-role-for-data-capture-users}

1. 관리 콘솔에서 설정 > 사용자 관리 > 역할 관리를 클릭한 후 새 역할을 클릭합니다.
1. 해당 필드에 역할 이름(예: 데이터 캡처 사용자)과 설명을 입력한 후 다음을 클릭합니다.
1. 역할 권한 화면에서 권한 찾기를 클릭한 후 사용 가능한 권한 목록에서 자격 증명 읽기를 선택합니다.
1. 확인을 클릭한 후 완료를 클릭합니다.

## 데이터 캡처 역할 할당 {#assign-the-data-capture-role}

1. 관리 콘솔에서 설정 > 사용자 관리 > 역할 관리를 클릭한 후 찾기를 클릭합니다.
1. 생성한 데이터 캡처 사용자 역할을 클릭합니다.
1. 역할 사용자/그룹 탭에서 사용자/그룹 찾기를 클릭합니다.
1. 사용자 및 그룹 찾기 화면에서 찾기를 클릭하고 데이터 캡처 사용자 역할이 필요한 사용자를 선택한 후 확인을 클릭합니다.
1. 역할 편집 화면에서 저장을 클릭합니다.
