---
title: 인증서 해지 목록 관리
description: 인증서 해지 목록을 관리하는 방법을 알아봅니다. Trust Store 관리를 사용하여 CRL(인증서 해지 목록)을 가져오고, 편집하고, 삭제할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '179'
ht-degree: 100%

---

# 인증서 해지 목록 관리{#managing-certificate-revocationlists}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

Trust Store 관리를 사용하여 CRL(인증서 해지 목록)을 가져오고, 편집하고, 삭제할 수 있습니다. Base64 및 DER로 인코딩된 인증서 해지 목록이 지원됩니다.

## CRL 가져오기 {#import-a-crl}

1. 관리 콘솔에서 설정 > Trust Store 관리 > 인증서 해지 목록을 클릭한 후 가져오기를 클릭합니다.
1. 별칭 상자에 CRL에 대한 식별자를 입력합니다.
1. 찾아보기를 클릭하여 CRL을 찾은 후 확인을 클릭합니다.

## CRL 내보내기 {#export-a-crl}

1. 관리 콘솔에서 설정 > Trust Store 관리 > 인증서 해지 목록을 클릭합니다.
1. CRL의 별칭을 클릭하여 내보낼 수 있도록 준비한 후 내보내기를 클릭합니다.
1. 지침에 따라 CRL을 내보냅니다. CRL은 Base64 인코딩으로 내보내집니다.
1. 확인을 클릭합니다.

## CRL 삭제 {#delete-a-crl}

1. 관리 콘솔에서 설정 > Trust Store 관리 > 인증서 해지 목록을 클릭합니다.
1. 삭제할 CRL의 확인란을 선택하고 삭제를 클릭한 후 확인을 클릭합니다.
