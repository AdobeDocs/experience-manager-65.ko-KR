---
title: 인증을 위한 평가 순서 변경
seo-title: 인증을 위한 평가 순서 변경
description: AEM Forms가 여러 인증 공급자를 평가하는 순서를 변경할 수 있습니다.
seo-description: AEM Forms가 여러 인증 공급자를 평가하는 순서를 변경할 수 있습니다.
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 인증 {#change-the-order-of-evaluation-for-authentication} 평가 순서 변경

여러 인증 공급자를 구성한 경우 AEM Forms에서 인증을 위해 인증 순서를 변경할 수 있습니다. config.xml 파일에 나열된 인증 공급자의 순서에 따라 인증 평가 순서가 결정됩니다.

1. 관리 콘솔에서 설정 > 사용자 관리 > 구성 > 구성 파일 가져오기 및 내보내기 를 클릭합니다.
1. 현재 구성 설정을 파일로 내보내려면 내보내기 를 클릭하고 구성 파일을 다른 위치에 저장합니다.
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

   `<entry key="order" value="3" />`에서 각 노드의 값을 편집하여 인증 평가의 순서를 설정합니다.

1. 업데이트된 파일을 가져오려면 사용자 관리에서 구성 > 구성 파일 가져오기 및 내보내기를 클릭합니다.
1. 찾아보기 를 클릭하여 파일을 찾고 가져오기를 클릭한 다음 확인을 클릭합니다.
