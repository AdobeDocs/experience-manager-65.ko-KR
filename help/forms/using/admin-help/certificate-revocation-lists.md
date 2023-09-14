---
title: 인증서 해지 목록 관리
description: 인증서 해지 목록을 관리하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---

# 인증서 해지 목록 관리{#managing-certificate-revocationlists}

Trust Store Management를 사용하여 CRL(인증서 해지 목록)을 가져오고, 편집하고, 삭제할 수 있습니다. Base64 및 DER로 인코딩된 인증서 해지 목록이 지원됩니다.

## CRL 가져오기 {#import-a-crl}

1. 관리 콘솔에서 설정 > Trust Store Management > 인증서 해지 목록 을 클릭한 다음 가져오기를 클릭합니다.
1. 별칭 상자에 CRL의 식별자를 입력합니다.
1. 찾아보기 를 클릭하여 CRL을 찾은 다음 확인 을 클릭합니다.

## CRL 내보내기 {#export-a-crl}

1. 관리 콘솔에서 설정 > 보안 저장소 관리 > 인증서 해지 목록 을 클릭합니다.
1. 내보낼 수 있도록 CRL의 별칭 이름을 클릭한 다음 내보내기를 클릭합니다.
1. CRL을 내보낼 수 있도록 지침을 따르십시오. CRL은 Base64 인코딩으로 내보냅니다.
1. 확인을 클릭합니다.

## CRL 삭제 {#delete-a-crl}

1. 관리 콘솔에서 설정 > 보안 저장소 관리 > 인증서 해지 목록 을 클릭합니다.
1. 삭제할 CRL의 확인란을 선택하고 삭제를 누른 다음 확인을 누릅니다.
