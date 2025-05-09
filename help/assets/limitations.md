---
title: Dynamic Media 제한 사항
description: 이미지 세트 또는 회전 세트를 만들거나 PDF을 업로드할 때 모범 사례 및 적용된 제한에 대해 알아봅니다. 또한 Dynamic Media에서 지원되지 않는 웹 브라우저 및 운영 체제 조합에 대해 알아봅니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 8%

---

# Dynamic Media 제한 사항

다음 섹션에서는 Dynamic Media의 제한 사항에 대해 설명합니다.

이 항목에는 다음 섹션이 포함됩니다.

* [자산 유형에 대한 Dynamic Media의 모범 사례 및 강제 제한](#best-practice-enforced-limits)
* [Dynamic Media에서 지원되지 않는 웹 브라우저 및 운영 체제 조합](#unsupported-browser-os)

## 자산 유형에 대한 Dynamic Media의 모범 사례 및 강제 제한 {#best-practice-enforced-limits}

회전 집합 또는 이미지 집합을 만들거나 페이지 추출을 위해 PDF을 업로드할 때 Adobe은 다음 모범 사례를 권장하며 다음 제한을 적용합니다.

| 에셋 - 제한 유형 | 모범 사례 | 제한 적용됨 |
| --- | --- | --- |
| **이미지** - 이미지당 스마트 자르기 수 | 5 | 100 |
| **모든 집합** - 집합당 중복 에셋 수 | 중복 항목 없음 | 20‡ |
| **모든 집합** - 집합당 최대 자산 수 | 세트당 5-10개 이미지 | 1000년 |
| **회전 집합** - 2D 집합당 최대 행/열 수 | 세트당 12~18개 이미지 | 1000 |
| **PDF** - 추출할 PDF의 최대 페이지 수 |  | 100(모든 PDF) |

‡ 가장 좋은 방법은 집합에 중복 에셋이 없는 것입니다. 단일 자산에 대한 중복 횟수는 20회로 제한됩니다. 해당 에셋에 대해 다른 중복을 추가하면 해당 세트 내에서 요청에 오류가 발생하거나 중복을 무시합니다.
<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Dynamic Media에서 지원되지 않는 웹 브라우저 및 운영 체제 조합 {#unsupported-browser-os}

Dynamic Media은 다음 웹 브라우저 및 운영 체제 조합을 지원하지 않습니다.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 업데이트
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## Secure Socket Layer 2.0 및 3.0 과 Transport Layer Security 1.0 및 1.1 지원 종료 {#tls}

<!-- CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->

2024년 4월 30일부터 Dynamic Media Adobe은 다음 사항에 대한 지원을 종료합니다.

* SSL(보안 소켓 계층) 2.0
* SSL 3.0
* TLS(전송 계층 보안) 1.0 및 1.1
* TLS 1.2의 다음과 같은 약한 암호:
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_RSA_WITH_AES_256_GCM_SHA384`
   * `TLS_RSA_WITH_AES_256_CBC_SHA256`
   * `TLS_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_AES_128_GCM_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
   * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

