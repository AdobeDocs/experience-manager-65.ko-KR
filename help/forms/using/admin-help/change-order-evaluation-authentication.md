---
title: 인증 평가 순서 변경
description: AEM Forms에서 여러 인증 제공자를 평가하는 순서를 변경할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '159'
ht-degree: 100%

---

# 인증 평가 순서 변경 {#change-the-order-of-evaluation-for-authentication}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

여러 인증 제공자를 구성한 경우 AEM Forms에서 인증을 위해 해당 인증 제공자를 평가하는 순서를 변경할 수 있습니다. config.xml 파일에 나열된 인증 제공자의 순서에 따라 인증 평가 순서가 결정됩니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기를 클릭합니다.
1. 현재 구성 설정을 파일로 내보내려면 내보내기를 클릭하고 해당 구성 파일을 다른 위치에 저장합니다.
1. 파일에서 다음 노드를 찾습니다.

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   `<entry key="order" value="3" />`에서 각 노드의 값을 편집하여 인증 평가 순서를 설정합니다.

1. 업데이트된 파일을 가져오려면 사용자 관리에서 구성 > 구성 파일 가져오기 및 내보내기를 클릭합니다.
1. 찾아보기를 클릭하여 파일을 찾은 후 가져오기를 클릭하고 확인을 클릭합니다.
