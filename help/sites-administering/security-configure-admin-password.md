---
title: 설치 시 관리자 암호 구성
description: Adobe Experience Manager 설치에서 관리자 암호를 변경하는 방법에 대해 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 설치 시 관리자 암호 구성{#configure-the-admin-password-on-installation}

## 개요 {#overview}

버전 6.3부터 Adobe Experience Manager(AEM)에서 새 인스턴스를 설치할 때 명령줄을 사용하여 관리자 암호를 설정할 수 있습니다.

이전 버전의 AEM에서는 설치 후 관리자 계정의 암호와 다양한 다른 콘솔의 암호를 변경해야 했습니다.

이 기능은 AEM 인스턴스를 설치하는 동안 저장소 및 서블릿 엔진에 대한 새 관리자 암호를 설정하는 기능을 추가하므로 나중에 수동으로 수행할 필요가 없습니다.

>[!CAUTION]
>
>이 기능은 Felix 콘솔을 다루지 않으며, 이 콘솔에서 암호를 수동으로 변경해야 합니다. 자세한 내용은 관련 [보안 검사 목록 섹션](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)을 참조하세요.

## 어떻게 사용하나요? {#how-do-i-use-it}

이 기능은 파일 시스템 탐색기에서 JAR을 두 번 클릭하는 대신 명령줄을 통해 AEM을 설치하도록 선택하면 자동으로 트리거됩니다.

명령줄에서 AEM 인스턴스를 실행하는 일반 구문은 다음과 같습니다.

```shell
java -jar aem6.3.jar
```

명령줄에서 인스턴스를 실행하면 설치 프로세스 중에 관리자 암호를 변경할 수 있는 옵션이 표시됩니다.

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>새 AEM 인스턴스를 설치하는 동안에만 관리자 암호를 변경하라는 메시지가 표시됩니다.

## -nointeractive 플래그 사용 {#using-the-nointeractive-flag}

속성 파일에서 암호를 지정하도록 선택할 수도 있습니다. 이 작업은 `-Dadmin.password.file` 시스템 속성과 결합된 `-nointeractive` 플래그를 사용하여 수행됩니다.

아래는 한 예입니다.

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

`passwordfile.properties` 파일 내의 암호는 아래 형식이어야 합니다.

```xml
admin.password = 12345678
```

>[!NOTE]
>
>`-Dadmin.password.file` 시스템 속성 없이 `-nointeractive` 매개 변수만 사용하는 경우 AEM은 사용자에게 변경을 요청하지 않고 기본 관리자 암호를 사용하며, 기본적으로 이전 버전의 동작을 복제합니다. 이 비대화형 모드는 설치 스크립트에서 명령줄을 사용하여 자동 설치에 사용할 수 있습니다.
