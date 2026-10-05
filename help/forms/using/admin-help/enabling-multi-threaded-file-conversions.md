---
title: 다중 스레드 파일 변환 사용
description: 다중 스레드 파일 변환을 활성화하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 4a55f87d3b8aa9944f0b32760aa645c42efd93e8
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%
---
# 다중 스레드 파일 변환 사용 {#enabling-multi-threaded-file-conversions}

PDF Generator은 여러 파일 변환을 동시에 실행하여 변환 처리량을 향상시킬 수 있습니다. 적용 가능한 변환 모드를 선택합니다.

| 전환 모드 | 동시 변환을 지원하는 애플리케이션 | 사용자 계정 모델 |
|---|---|---|
| 다중 사용자 모드 | OpenOffice | 각 OpenOffice 인스턴스는 별도의 사용자 계정으로 실행됩니다. |
| 단일 사용자 모드 | ® Word 및 Microsoft® Excel | 하나의 사용자 계정이 여러 개의 Word 및 Excel 인스턴스를 실행합니다. PowerPoint 변환은 계속 직렬화됩니다. |

두 모드를 활성화하기 전에 사용하는 응용 프로그램 및 운영 체제에 대한 [PDF Generator 사전 설치 구성](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations)을 완료하십시오. 지원되는 응용 프로그램 버전에 대해서는 [PDF Generator에 대한 소프트웨어 지원](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)을 참조하십시오.

## 다중 사용자 모드 {#multi-user-mode}

다중 사용자 모드에서 PDF Generator은 별도의 사용자 계정으로 각 OpenOffice 인스턴스를 시작합니다. 필요한 동시 전환 수에 대해 유효한 관리 사용자 계정을 충분히 구성합니다. 클러스터에서 모든 노드에 동일한 계정을 구성합니다.

Windows에서는 PDF Generator 사용자에게 [프로세스 수준 토큰 바꾸기](/help/forms/using/install-configure-document-services.md#grant-the-replace-a-process-level-token-privilege) 권한이 있는지 확인하고 [문서 서비스 구성](/help/forms/using/install-configure-document-services.md#disable-user-account-control-uac)에 설명된 해당 사용자 계정 컨트롤 구성을 완료하십시오.

### OpenOffice 전환 {#openoffice-conversions}

동시에 실행할 수 있는 각 OpenOffice 인스턴스에 대해 하나의 PDF Generator 사용자 계정을 구성합니다. 구성된 모든 사용자가 액세스할 수 있는 위치에 OpenOffice를 설치하고 각 사용자에 대한 초기 OpenOffice 활성화 대화 상자를 닫습니다.

UNIX 기반 시스템의 경우 [문서 서비스 구성](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations)에서 OpenOffice 설치 및 사용자 권한 요구 사항을 완료하십시오.

## Windows의 단일 사용자 모드 {#single-user-mode-on-windows}

단일 사용자 모드를 사용하면 PDF Generator에서 구성된 하나의 사용자 계정에서 동시 변환을 실행할 수 있습니다.

이 모드에서는 ® Word(DOC 및 DOCX) 및 Excel(XLS 및 XLSX)의 여러 인스턴스가 동일한 사용자 아래에서 실행됩니다. ® PowerPoint(PPT 및 PPTX)는 단일 사용자 모드를 지원하지 않습니다. PDF Generator은 한 번에 하나의 PowerPoint 인스턴스만 시작하므로 PowerPoint 전환이 직렬화됩니다.

Word 및 Excel 변환에 단일 사용자 모드를 활성화하려면 다음을 수행합니다.

1. 관리 콘솔에서 **홈 > 서비스 > 응용 프로그램 및 서비스 > 서비스 관리**&#x200B;로 이동합니다.
1. **PDF Generator**&#x200B;을(를) 필터링하고 **GeneratePDFService**&#x200B;을(를) 선택하십시오.
1. **구성** 탭에서 다음 옵션을 구성합니다.

   * **PDFMaker에 대한 단일 사용자 모드 사용**&#x200B;을 **true**(으)로 설정합니다.
   * 전환을 동시에 실행할 수 있는 최대 Word 인스턴스 수로 **PDFMaker 풀 크기**&#x200B;를 설정하십시오.
   * **Native2PDF에 대해 단일 사용자 모드 사용**&#x200B;을 **true**(으)로 설정합니다.
   * 전환을 동시에 실행할 수 있는 최대 Excel 인스턴스 수로 **Native2PDF 풀 크기**&#x200B;를 설정합니다.

1. AEM Forms 서버를 다시 시작합니다.
