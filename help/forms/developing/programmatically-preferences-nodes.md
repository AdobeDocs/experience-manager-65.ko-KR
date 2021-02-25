---
title: 프로그래밍 방식으로 PreferencesNodes 관리
seo-title: 프로그래밍 방식으로 PreferencesNodes 관리
description: 환경 설정 관리자 서비스 API(Java)를 사용하여 환경 설정 노드를 프로그래밍 방식으로 관리합니다.
seo-description: 환경 설정 관리자 서비스 API(Java)를 사용하여 환경 설정 노드를 프로그래밍 방식으로 관리합니다.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 환경 설정 노드 {#programmatically-managing-the-preferencesnodes} 프로그래밍 방식으로 관리

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

이 항목에서는 환경 설정 관리자 서비스 API(Java)를 사용하여 환경 설정 노드를 프로그래밍 방식으로 관리하는 방법에 대해 설명합니다.

관리자 UI에서 구성 설정을 수동으로 변경할 수 있습니다. 옵션을 변경하려면 `Home>Settings>User Management> Configuration>Manual Configuration`으로 이동합니다. 변경 작업을 수행한 후 `config.xml`을(를) 가져오면 노드 `/Adobe/Adobe Experience Manager Forms/Config/UM persist`에서 변경한 내용을 제외한 모든 변경 내용이 손실됩니다. 사용자 관리 가져오기 및 내보내기의 미리 보기는 다른 구성 요소에 대한 구성 설정 변경을 지원하지 않습니다. 이제 `PreferencesManagerServiceClient` API를 사용하여 변경할 수 있습니다.

**단계**&#x200B;요약기본 설정 노드를 프로그래밍 방식으로 관리하려면 다음 단계를 수행합니다.

1. 프로젝트 파일 포함
1. PreferencesManagerService 클라이언트 만들기
1. 적절한 역할 또는 권한 작업을 호출합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함할 수 있습니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**PreferencesManagerService 클라이언트 만들기**

사용자 관리 환경 설정 관리자 서비스 작업을 프로그래밍 방식으로 수행하려면 먼저 PreferencesManagerService 클라이언트를 만들어야 합니다. Java API를 사용하면 PreferencesManagerServiceClient 객체를 만들어 이 작업을 수행할 수 있습니다.

**적절한 역할 또는 권한 작업을 호출합니다.**

서비스 클라이언트를 만들었으면 환경 설정 관리자 작업을 호출할 수 있습니다. 서비스 클라이언트를 통해 권한을 읽고 설정할 수 있습니다.
