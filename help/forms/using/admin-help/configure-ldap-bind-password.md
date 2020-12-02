---
title: LDAP 바인딩 암호 구성
seo-title: LDAP 바인딩 암호 구성
description: 구성 파일을 다른 시스템으로 가져오기 전에 바인딩 암호 필드를 구성하는 방법을 알아봅니다.
seo-description: 구성 파일을 다른 시스템으로 가져오기 전에 바인딩 암호 필드를 구성하는 방법을 알아봅니다.
uuid: 1ab1907c-8b55-4b6f-bd5b-49f22d78b8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 165b3950-b03f-4848-8361-ffb0a26d2658
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# LDAP 바인딩 암호{#configure-the-ldap-bind-password} 구성

보안 위험을 방지하기 위해 내보낸 구성 파일(config.xml)의 바인딩 암호 필드가 구성되지 않았습니다. 구성 파일을 다른 시스템으로 가져오기 전에 이 암호를 구성해야 합니다. 이 비밀번호는 데이터베이스에 저장된 기존 비밀번호를 무시합니다. null 암호는 null이 아닌 기존 암호 값을 덮어쓰지 않습니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기를 클릭합니다.
1. 현재 구성 설정을 파일로 내보내려면 내보내기를 클릭하고 구성 파일을 다른 위치에 저장합니다.
1. 파일에서 `Domains` > *[도메인 이름]* > `DirectoryConfigs` > `LDAPGroupConfig` 노드를 찾습니다. 다음은 한 예입니다.

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

   `bindpassword` 값을 입력하고 변경 내용을 저장합니다.

1. 파일에서 `Domains` > *[도메인 이름]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig` 노드를 찾습니다. 다음은 한 예입니다.

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

   `bindpassword` 값을 입력하고 변경 내용을 저장합니다.

1. 업데이트된 파일을 가져오려면 사용자 관리에서 구성 > 구성 파일 가져오기 및 내보내기를 클릭합니다.
1. 찾아보기를 클릭하여 파일을 찾고 가져오기를 클릭한 다음 확인을 클릭합니다.

