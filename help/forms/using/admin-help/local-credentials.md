---
title: 로컬 자격 증명 관리
description: Trust Store 관리를 사용하여 로컬 자격 증명을 관리하는 방법을 알아봅니다. AEM Forms는 표준 PKCS12 양식의 RSA 및 DSA 자격 증명을 지원합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c5905272-7d09-47e4-8b35-4cc25a148477
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '533'
ht-degree: 100%

---

# 로컬 자격 증명 관리 {#managing-local-credentials}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

로컬 자격 증명은 Trust Store 관리에서 호스팅된 개인 키 자격 증명입니다. *로컬 자격 증명*&#x200B;은 사용자의 DES 자격 증명이 저장된 위치를 식별합니다. Trust Store 관리를 사용하면 기존 PFX 파일 등을 사용하여 로컬 자격 증명을 가져오고 관리할 수 있으므로 로컬 자격 증명을 가져오고, 편집하고, 삭제할 수 있습니다.

AEM Forms는 표준 PKCS12 형식(.pfx 및 .p12 파일)에서 최대 4096비트의 RSA 및 DSA 자격 증명을 지원합니다.

자격 증명을 원하는 수만큼 가져오고 내보낼 수 있습니다. 동일한 별칭을 사용하여 만료된 자격 증명을 바꾸려면 해당 자격 증명을 삭제한 후 동일한 별칭을 사용하여 새 자격 증명을 가져옵니다.

Acrobat Reader DC 확장 프로그램과 관련된 정보 및 지침은 [Acrobat Reader DC 확장 프로그램에서 사용할 자격 증명 구성](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)을 참조하십시오.

## 자격 증명 가져오기 {#import-a-credential}

1. 관리 콘솔에서 설정 > Trust Store 관리 > 로컬 자격 증명을 클릭합니다.
1. 가져오기를 클릭합니다. Trust Store 유형에서 다음 옵션 중 하나를 선택합니다.

   * **문서 서명 자격 증명:** 문서에 디지털 서명을 발급하는 데 사용되는 자격 증명입니다.
   * **Acrobat Reader DC 확장 프로그램 자격 증명:** Acrobat Reader DC 확장 프로그램과 관련된 디지털 인증서로, 이를 통해 생성된 PDF 문서에서 Adobe Reader 사용 권한을 활성화할 수 있습니다.
   * **기본:** Acrobat Reader DC 확장 프로그램에서 사용할 기본 자격 증명임을 나타냅니다.

   자격 증명 획득에 대한 자세한 내용은 [AEM Forms 설치 준비](https://helpx.adobe.com/kr/pdf/aem-forms/6-3/prepare-install-single-server.pdf)를 참조하십시오.

1. 별칭 상자에 자격 증명에 대한 식별자를 입력합니다. 이 식별자는 Acrobat Reader DC 확장 프로그램과 서명 서비스에서 자격 증명의 표시 이름으로 사용됩니다. 이 별칭은 AEM Forms SDK를 사용하여 자격 증명에 프로그래밍 방식으로 액세스하는 데에도 사용됩니다.

   >[!NOTE]
   >
   >별칭은 표시 목적에 따라 대문자로 자동 변환됩니다. 프로세스에서 별칭을 참조할 때는 대소문자를 구분하지 않습니다.

1. 찾아보기를 클릭하여 자격 증명을 찾고 자격 증명의 암호를 입력한 후 확인을 클릭합니다.

   “잘못된 파일 형식 또는 잘못된 암호로 인해 자격 증명을 가져오지 못했습니다.”라는 오류 메시지가 나타나면 암호가 유효한지 확인합니다.

## 자격 증명 내보내기 {#export-a-credential}

자격 증명은 PKCS#12 형식의 P12 파일로 내보내집니다.

1. 관리 콘솔에서 설정 > Trust Store 관리 > 로컬 자격 증명을 클릭합니다.
1. 내보내낼 자격 증명의 별칭을 클릭한 후 내보내기를 클릭합니다.
1. 암호 상자에 암호를 입력합니다. 이 암호는 새 암호이며 내보낸 자격 증명을 암호화하는 데 사용됩니다.
1. 내보내기를 클릭하고 지침에 따라 자격 증명을 내보낸 후 확인을 클릭합니다.

## 자격 증명의 별칭 또는 Trust Store 유형 편집 {#edit-a-credential-s-alias-or-trust-store-type}

자격 증명을 가져온 후에는 별칭과 Trust Store 유형을 편집할 수 있습니다.

1. 관리 콘솔에서 설정 > Trust Store 관리 > 로컬 자격 증명을 클릭합니다.
1. 편집할 자격 증명의 별칭을 클릭합니다.
1. 자격 증명 업데이트를 클릭합니다.
1. 필요에 따라 별칭과 Trust Store 유형을 편집하고 확인을 클릭합니다.

## 자격 증명 삭제 {#delete-a-credential}

1. 관리 콘솔에서 설정 > Trust Store 관리 > 로컬 자격 증명을 클릭합니다.
1. 삭제할 자격 증명의 확인란을 선택합니다.
1. 삭제를 클릭한 후 확인을 클릭합니다.
