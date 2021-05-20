---
title: 기존 도메인 편집 및 변환
seo-title: 기존 도메인 편집 및 변환
description: 도메인 관리 페이지에서 기존 도메인의 설정을 변경하는 방법을 배웁니다. 기존 엔터프라이즈 도메인을 하이브리드 도메인으로 변환하거나 그 반대로 변환합니다.
seo-description: 도메인 관리 페이지에서 기존 도메인의 설정을 변경하는 방법을 배웁니다. 기존 엔터프라이즈 도메인을 하이브리드 도메인으로 변환하거나 그 반대로 변환합니다.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 기존 도메인 편집 및 변환{#editing-and-converting-existing-domains}

도메인 관리 페이지에서 기존 도메인에 대한 설정을 변경할 수 있습니다. 기존 엔터프라이즈 도메인을 하이브리드 도메인으로 변환할 수도 있습니다.

## 기존 도메인 편집 {#edit-an-existing-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 편집할 도메인의 이름을 클릭합니다.
1. 도메인 이름을 변경하려면 이름 상자에서 텍스트를 변경합니다.
1. Enterprise 또는 hybrid 도메인에 대한 인증 정보를 변경하려면 페이지 하단에서 해당 인증 이름을 클릭합니다. [인증 편집] 페이지에서 필요에 따라 설정을 변경합니다. ([인증 설정](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)을 참조하십시오.)
1. 엔터프라이즈 도메인의 디렉토리 정보를 변경하려면 페이지 하단에 있는 해당 디렉토리 이름을 누릅니다. [디렉토리 편집] 페이지에서 필요에 따라 설정을 변경합니다. ( [디렉토리 또는 사용자 지정 SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis) 추가 참조).
1. 변경을 완료하면 확인을 클릭합니다.

## 엔터프라이즈 도메인을 하이브리드 도메인 {#convert-an-enterprise-domain-to-a-hybrid-domain}으로 변환

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 변환할 엔터프라이즈 도메인의 이름을 클릭합니다.
1. 하이브리드 도메인으로 변환 을 클릭합니다.
1. 사용자 및 그룹 데이터 및 사용자 인증과 관련된 정보를 검토하고 확인을 클릭합니다.
1. 하이브리드 도메인의 설정을 편집하고 확인을 클릭합니다.

>[!NOTE]
>
>변환하려는 엔터프라이즈 도메인에 디렉토리 설정이 없는 경우 LDAP 인증 설정이 손실됩니다.

## 하이브리드 도메인을 엔터프라이즈 도메인으로 변환 {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리 를 클릭합니다.
1. 변환할 하이브리드 도메인의 이름을 클릭합니다.
1. Enterprise 도메인으로 변환을 클릭합니다.
1. 사용자 및 그룹 데이터 및 사용자 인증과 관련된 정보를 검토하고 확인을 클릭합니다.
1. 디렉토리 추가 를 클릭하고 필요한 디렉토리 정보를 구성합니다. ( [디렉토리 또는 사용자 지정 SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis) 추가 참조).
