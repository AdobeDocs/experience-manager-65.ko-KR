---
title: LDAP 바인드 암호 구성
description: 구성 파일을 다른 시스템으로 가져오기 전에 바인드 암호 필드를 구성하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c72794f5-8767-409e-a1df-91a8fdc54d18
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# LDAP 바인드 암호 구성{#configure-the-ldap-bind-password}

보안 위험을 방지하기 위해 내보낸 구성 파일(config.xml)의 바인드 암호 필드가 구성되지 않았습니다. 구성 파일을 다른 시스템으로 가져오기 전에 이 암호를 구성해야 합니다. 이 암호는 데이터베이스에 저장된 기존 암호를 재정의합니다. Null 암호는 Null이 아닌 기존 암호 값을 재정의하지 않습니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기 를 클릭합니다.
1. 현재 구성 설정을 파일로 내보내려면 내보내기(Export)를 클릭하고 구성 파일을 다른 위치에 저장합니다.
1. 파일에서 `Domains` > *[도메인 이름]* > `DirectoryConfigs` > `LDAPGroupConfig` 노드. 예를 들면 다음과 같습니다.

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   다음에 대한 값 입력 `bindpassword` 변경 내용을 저장합니다.

1. 파일에서 `Domains` > *[도메인 이름]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` 노드. 예를 들면 다음과 같습니다.

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   다음에 대한 값 입력 `bindpassword` 변경 내용을 저장합니다.

1. 업데이트된 파일을 가져오려면 사용자 관리에서 구성 > 구성 파일 가져오기 및 내보내기 를 클릭합니다.
1. 찾아보기 를 클릭하여 파일을 찾고 가져오기 를 클릭한 다음 확인 을 클릭합니다.
