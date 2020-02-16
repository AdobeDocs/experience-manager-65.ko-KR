---
title: 로컬 자격 증명 관리
seo-title: 로컬 자격 증명 관리
description: 로컬 자격 증명을 관리하는 방법을 알아봅니다.
seo-description: 로컬 자격 증명을 관리하는 방법을 알아봅니다.
uuid: 3c4358e0-aaff-4e94-a6b2-04b463fca260
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 598a9a03-3773-4620-8867-1f754d8ca031
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 로컬 자격 증명 관리 {#managing-local-credentials}

로컬 자격 증명은 Trust Store 관리에서 호스팅되는 개인 키 자격 증명입니다. 로컬 자격 증명은 ** 사용자의 DES 자격 증명이 저장된 위치를 식별합니다. Trust Store Management를 사용하여 로컬 자격 증명을 가져오고, 편집하고, 삭제할 수 있도록 기존 PFX 파일과 같은 기능을 사용하여 로컬 자격 증명을 가져오고 관리할 수 있습니다.

AEM 양식은 표준 PKCS12 형식(.pfx 및 .p12 파일)에서 최대 4096비트의 RSA 및 DSA 자격 증명을 지원합니다.

자격 증명을 가져오거나 내보낼 수 있습니다. 동일한 별칭을 사용하여 만료된 자격 증명을 교체하려면 자격 증명을 삭제한 다음 동일한 별칭으로 새 자격 증명을 가져옵니다.

Acrobat Reader DC 익스텐션과 관련된 정보 및 지침은 Acrobat [Reader DC 익스텐션에서](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)사용할 자격 증명 구성을 참조하십시오.

## 자격 증명 가져오기 {#import-a-credential}

1. 관리 콘솔에서 설정 > 트러스트 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 가져오기를 클릭합니다. [Trust Store 유형] 아래에서 다음 옵션 중 하나를 선택합니다.

   * **** 문서 서명 자격 증명:문서에서 디지털 서명을 발행하는 데 사용되는 자격 증명입니다.
   * **** Acrobat Reader DC 확장 자격 증명:Acrobat Reader DC 익스텐션에만 사용되는 디지털 인증서로서 Adobe Reader 사용 권한이 제작된 PDF 문서에서 활성화됩니다.
   * **** 기본값:Acrobat Reader DC 익스텐션에서 사용할 수 있는 기본 자격 증명임을 나타냅니다.
   자격 증명을 얻는 방법에 대한 자세한 내용은 AEM [양식](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)설치 준비를 참조하십시오.

1. 별칭 상자에 자격 증명의 식별자를 입력합니다. 이 식별자는 Acrobat Reader DC 확장 및 서명 서비스의 자격 증명을 위한 표시 이름으로 사용됩니다. 이 별칭은 AEM 양식 SDK를 사용하여 프로그래밍 방식으로 자격 증명에 액세스하는 데에도 사용됩니다.

   >[!NOTE]
   >
   >표시 목적으로 별칭 이름이 자동으로 대문자로 변환됩니다. 프로세스에서 별칭 이름을 참조할 때는 별칭 이름을 대/소문자를 구분하지 않습니다.

1. [탐색]을 클릭하여 자격 증명을 찾고 자격 증명의 암호를 입력한 다음 [확인]을 클릭합니다.

   &quot;잘못된 파일 형식 또는 잘못된 암호로 인해 자격 증명을 가져오지 못했습니다&quot; 오류 메시지가 표시되는 경우 암호가 올바른지 확인하십시오.

## 자격 증명 내보내기 {#export-a-credential}

자격 증명은 PKCS#12 형식으로 P12 파일로 내보내집니다.

1. 관리 콘솔에서 설정 > 트러스트 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 내보낼 자격 증명의 별칭 이름을 클릭한 다음 내보내기를 클릭합니다.
1. 암호 상자에 암호를 입력합니다. 이 암호는 새로운 암호이며 내보낸 자격 증명을 암호화하는 데 사용됩니다.
1. 내보내기를 클릭하고 지침에 따라 자격 증명을 내보낸 다음 확인을 클릭합니다.

## 자격 증명의 별칭 또는 신뢰 저장소 유형 편집 {#edit-a-credential-s-alias-or-trust-store-type}

자격 증명을 가져온 후 별칭 이름과 신뢰 저장소 유형을 편집할 수 있습니다.

1. 관리 콘솔에서 설정 > 트러스트 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 편집할 자격 증명의 별칭 이름을 클릭합니다.
1. 자격 증명 업데이트를 클릭합니다.
1. 필요에 따라 별칭 이름과 트러스트 저장소 유형을 편집하고 확인을 클릭합니다.

## 자격 증명 삭제 {#delete-a-credential}

1. 관리 콘솔에서 설정 > 트러스트 저장소 관리 > 로컬 자격 증명을 클릭합니다.
1. 삭제할 자격 증명의 확인란을 선택합니다.
1. 삭제를 클릭한 다음 확인을 클릭합니다.

