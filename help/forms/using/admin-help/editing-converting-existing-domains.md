---
title: 기존 도메인 편집 및 변환
description: 도메인 관리 페이지에서 기존 도메인 설정을 변경하는 방법을 알아봅니다. 기존 엔터프라이즈 도메인을 하이브리드 도메인으로 변환하거나 그 반대로 변환합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '321'
ht-degree: 100%

---

# 기존 도메인 편집 및 변환{#editing-and-converting-existing-domains}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

도메인 관리 페이지에서 기존 도메인 설정을 변경할 수 있습니다. 기존 엔터프라이즈 도메인을 하이브리드 도메인으로 변환할 수도 있습니다.

## 기존 도메인 편집 {#edit-an-existing-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 편집할 도메인 이름을 클릭합니다.
1. 도메인 이름을 변경하려면 이름 상자의 텍스트를 변경합니다.
1. 엔터프라이즈 또는 하이브리드 도메인의 인증 정보를 변경하려면 페이지 하단에서 해당 인증 이름을 클릭합니다. 인증 편집 페이지에서 필요에 따라 설정을 변경합니다. ([인증 설정](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)을 참조하십시오.)
1. 엔터프라이즈 도메인의 디렉터리 정보를 변경하려면 페이지 하단에서 해당 디렉터리 이름을 클릭합니다. 디렉터리 편집 페이지에서 필요에 따라 설정을 변경합니다. ([디렉터리 또는 사용자 정의 SPI 추가](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)를 참조하십시오.)
1. 변경을 완료하면 확인을 클릭합니다.

## 엔터프라이즈 도메인을 하이브리드 도메인으로 변환 {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 변환할 엔터프라이즈 도메인의 이름을 클릭합니다.
1. 하이브리드 도메인으로 변환을 클릭합니다.
1. 사용자 및 그룹 데이터와 사용자 인증에 관해 표시되는 정보를 검토하고 확인을 클릭합니다.
1. 하이브리드 도메인 설정을 편집하고 확인을 클릭합니다.

>[!NOTE]
>
>변환하는 엔터프라이즈 도메인에 디렉터리 설정이 포함되어 있지 않으면 모든 LDAP 인증 설정이 손실됩니다.

## 하이브리드 도메인을 엔터프라이즈 도메인으로 변환 {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. 관리 콘솔에서 설정 > 사용자 관리 > 도메인 관리를 클릭합니다.
1. 변환할 하이브리드 도메인의 이름을 클릭합니다.
1. 엔터프라이즈 도메인으로 변환을 클릭합니다.
1. 사용자 및 그룹 데이터와 사용자 인증에 관해 표시되는 정보를 검토하고 확인을 클릭합니다.
1. 디렉터리 추가를 클릭하고 필수 디렉터리 정보를 구성합니다. ([디렉터리 또는 사용자 정의 SPI 추가](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)를 참조하십시오.)
