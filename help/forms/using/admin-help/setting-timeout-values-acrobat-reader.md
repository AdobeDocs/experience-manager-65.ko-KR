---
title: Acrobat Reader DC 확장 프로그램에서 사용할 시간 초과 값 설정
description: Acrobat Reader DC 확장 프로그램에서 사용할 시간 초과 값을 설정하는 방법을 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
source-wordcount: '190'
ht-degree: 100%
---
# Acrobat Reader DC 확장 프로그램에서 사용할 시간 초과 값 설정  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

Acrobat Reader DC 확장 프로그램에서 많은 PDF 파일을 작업할 때 작업 시간이 초과되어 작업이 실패하는 것을 방지하기 위해 다음과 같은 시간 초과 값이 적절하게 설정되어 있는지 확인합니다.

**문서 폐기 시간 초과**

이 값은 관리 콘솔에서 설정할 수 있습니다. 설정 > 핵심 시스템 설정 > 구성을 클릭하고 기본 문서 폐기 시간 초과 값을 지정합니다.

**사용자 관리자 AEM Forms 시간 초과:** 이 값은 config.xml 파일을 편집하여 설정할 수 있습니다. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기를 클릭한 후 내보내기를 클릭합니다. 내보낸 config.xml 파일을 열고 다음 줄을 편집합니다.

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

config.xml 파일을 저장한 후 관리 콘솔로 다시 가져옵니다.

**애플리케이션 서버 세션 시간 초과:** 이 값은 애플리케이션 서버에서 설정할 수 있습니다. 자세한 내용은 애플리케이션 서버와 함께 제공된 설명서를 참조하십시오.
