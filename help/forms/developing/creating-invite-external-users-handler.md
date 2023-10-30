---
title: 외부 사용자 초대 핸들러 만들기
description: 외부 사용자 초대 핸들러를 만드는 방법을 알아봅니다. 이를 통해 Rights Management 서비스는 외부 사용자를 Rights Management 사용자로 초대할 수 있습니다.
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# 외부 사용자 초대 핸들러 만들기 {#create-invite-external-users-handler}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

Rights Management 서비스에 대한 외부 사용자 초대 핸들러를 만들 수 있습니다. 외부 사용자 초대 핸들러를 사용하면 Rights Management 서비스에서 외부 사용자를 초대하여 Rights Management 사용자가 되도록 할 수 있습니다. 사용자가 Rights Management 사용자가 되면 사용자는 정책으로 보호된 PDF 문서를 여는 것과 같은 작업을 수행할 수 있습니다. 외부 사용자 초대 핸들러가 AEM Forms에 배포되면 관리 콘솔을 사용하여 이 핸들러와 상호 작용할 수 있습니다.

>[!NOTE]
>
>외부 사용자 초대 핸들러는 AEM Forms 구성 요소입니다. 외부 사용자 초대 핸들러를 만들기 전에 구성 요소 만들기에 익숙해지는 것이 좋습니다.

**단계 요약**

외부 사용자 초대 핸들러를 개발하려면 다음 단계를 수행해야 합니다.

1. 개발 환경을 설정합니다.
1. 외부 사용자 초대 핸들러 구현을 정의합니다.
1. 구성 요소 XML 파일을 정의합니다.
1. 외부 사용자 초대 핸들러를 배포합니다.
1. 외부 사용자 초대 핸들러를 테스트합니다.

## 개발 환경 설정 {#setting-up-development-environment}

개발 환경을 설정하려면 Eclipse 프로젝트와 같은 새 Java 프로젝트를 만들어야 합니다. 지원되는 Eclipse 버전은 입니다 `3.2.1` 나중에

Rights Management SPI에는 `edc-server-spi.jar` 프로젝트의 클래스 경로에 설정할 파일입니다. 이 JAR 파일을 참조하지 않으면 Java 프로젝트에서 Rights Management SPI를 사용할 수 없습니다. 이 JAR 파일은 의 AEM Forms SDK와 함께 설치됩니다. `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` 폴더를 삭제합니다.

을(를) 추가하는 것 외에도 `edc-server-spi.jar` 프로젝트의 클래스 경로에 파일을 추가하려면 Rights Management 서비스 API를 사용하는 데 필요한 JAR 파일도 추가해야 합니다. 이러한 파일은 외부 사용자 초대 핸들러에서 Rights Management 서비스 API를 사용하는 데 필요합니다.

## 외부 사용자 초대 핸들러 구현 정의 {#define-invite-external-users-handler}

외부 사용자 초대 핸들러를 개발하려면 다음을 구현하는 Java 클래스를 만들어야 합니다 `com.adobe.edc.server.spi.ersp.InvitedUserProvider` 인터페이스. 이 클래스에는 이름이 인 메서드가 포함되어 있습니다. `invitedUser`를 사용하여 이메일 주소를 제출할 때 Rights Management 서비스가 호출하는 **초대된 사용자 추가** 관리 콘솔을 통해 액세스할 수 있는 페이지입니다.

다음 `invitedUser` 메서드가 을 수락합니다 `java.util.List` 인스턴스는에서 제출된 문자열 형식의 이메일 주소를 포함합니다. **초대된 사용자 추가** 페이지를 가리키도록 업데이트하는 중입니다. 다음 `invitedUser` 메서드는 배열을 반환합니다. `InvitedUserProviderResult` 일반적으로 이메일 주소를 사용자 오브젝트에 매핑하는 오브젝트(null을 반환하지 않음).

>[!NOTE]
>
>이 섹션에서는 외부 사용자 초대 핸들러를 만드는 방법을 보여 주는 것 외에도 AEM Forms API를 사용합니다.

외부 사용자 초대 핸들러의 구현에는 이름이 인 사용자 정의 메서드가 포함됩니다 `createLocalPrincipalAccount`. 이 메서드는 이메일 주소를 매개 변수 값으로 지정하는 문자열 값을 수락합니다. 다음 `createLocalPrincipalAccount` 메서드는 라는 로컬 도메인이 있다고 가정합니다. `EDC_EXTERNAL_REGISTERED`. 이 도메인 이름을 원하는 대로 구성할 수 있습니다. 하지만 프로덕션 애플리케이션의 경우 엔터프라이즈 도메인과 통합할 수 있습니다.

다음 `createUsers` 메서드는 모든 이메일 주소에 대해 반복하고 해당 사용자 개체(에서 로컬 사용자)를 만듭니다. `EDC_EXTERNAL_REGISTERED` domain). 마지막으로 `doEmails` 메서드가 호출됩니다. 이 방법은 의도적으로 시료에 스터브로 남겨 둔다. 프로덕션 구현에서는 새로 생성된 사용자에게 초대 이메일 메시지를 보내는 애플리케이션 논리를 포함합니다. 실제 응용 프로그램의 응용 프로그램 논리 흐름을 보여 주기 위해 샘플에 남습니다.

### 외부 사용자 초대 핸들러 구현 정의 {#user-handler-implementation}

다음 외부 사용자 초대 핸들러 구현은 관리 콘솔을 통해 액세스할 수 있는 초대된 사용자 추가 페이지에서 제출된 이메일 주소를 수락합니다.

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>이 Java 클래스는 InviteExternalUsersSample.java라는 JAVA 파일로 저장됩니다.

## 권한 부여 처리기의 구성 요소 XML 파일 정의 {#define-component-xml-authorization-handler}

외부 사용자 초대 처리기 구성 요소를 배포하려면 구성 요소 XML 파일을 정의해야 합니다. 구성 요소 XML 파일은 각 구성 요소에 대해 존재하며 구성 요소에 대한 메타데이터를 제공합니다.

다음 `component.xml` 외부 사용자 초대 핸들러에 파일이 사용됩니다. 서비스 이름은 입니다. `InviteExternalUsersSample` 및 이 서비스가 노출하는 작업 이름은 입니다. `invitedUser`. 입력 매개 변수는 `java.util.List` 인스턴스와 출력 값은 `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` 인스턴스.

### 외부 사용자 초대 핸들러에 대한 구성 요소 XML 파일 정의 {#component-xml-invite-external-users-handler}

```as3
<component xmlns="https://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## 외부 사용자 초대 핸들러 패키징 {#packaging-invite-external-users-handler}

AEM Forms에 외부 사용자 초대 핸들러를 배포하려면 Java 프로젝트를 JAR 파일로 패키징해야 합니다. 외부 사용자 초대 핸들러의 비즈니스 논리가 종속된 외부 JAR 파일(예: )이 있는지 확인해야 합니다. `edc-server-spi.jar` 및 `adobe-rightsmanagement-client.jar` 파일도 JAR 파일에 포함됩니다. 구성 요소 XML 파일도 있어야 합니다. 다음 `component.xml` 파일 및 외부 JAR 파일은 JAR 파일의 루트에 있어야 합니다.

>[!NOTE]
>
>아래 그림에서 `BootstrapImpl` 클래스가 표시됩니다. 이 섹션에서는 다음을 만드는 방법에 대해 논의하지 않습니다. `BootstrapImpl` 클래스.

다음 그림은 외부 사용자 초대 핸들러의 JAR 파일에 패키지된 Java 프로젝트의 콘텐츠를 보여줍니다.

![사용자 초대](assets/ci_ci_InviteUsers.png)

A. 구성 요소 B. JAVA 파일에 필요한 외부 JAR 파일

외부 사용자 초대 핸들러를 JAR 파일로 패키징해야 합니다. 이전 다이어그램에서는 .JAVA 파일이 나열되어 있습니다. JAR 파일에 패키지된 후에는 해당 .CLASS 파일도 지정해야 합니다. .CLASS 파일이 없으면 권한 부여 처리기가 작동하지 않습니다.

>[!NOTE]
>
>외부 인증 핸들러를 JAR 파일로 패키징한 후 구성 요소를 AEM Forms에 배포할 수 있습니다. 외부 사용자 초대 핸들러는 한 번에 하나만 배포할 수 있습니다.

>[!NOTE]
>
>구성 요소를 프로그래밍 방식으로 배포할 수도 있습니다.

## 외부 사용자 초대 핸들러 테스트 {#testing-invite-external-users-handler}

외부 사용자 초대 핸들러를 테스트하려면 관리 콘솔을 사용하여 초대할 외부 사용자를 추가할 수 있습니다.

관리 콘솔을 사용하여 초대할 외부 사용자를 추가하려면 다음 작업을 수행하십시오.

1. Workbench를 사용하여 외부 사용자 초대 핸들러의 JAR 파일을 배포합니다.
1. 응용 프로그램 서버를 다시 시작합니다.
1. 관리 콘솔에 로그인합니다.
1. 클릭 **[!UICONTROL 서비스]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 구성]** > 초대됨 **[!UICONTROL 사용자 등록]**.
1. 다음을 확인하여 초대된 사용자 등록 활성화 **[!UICONTROL 초대된 사용자 등록 활성화]** 상자. 아래 **[!UICONTROL 기본 제공 등록 시스템 사용]**, 클릭 **[!UICONTROL 아니요]**. 설정을 저장합니다.
1. 관리 콘솔 홈 페이지에서 **[!UICONTROL 설정]** > **[!UICONTROL 사용자 관리]** > **[!UICONTROL 도메인 관리]**.
1. 클릭 **[!UICONTROL 새 로컬 도메인]**. 다음 페이지에서 의 이름 및 식별자 값으로 도메인을 만듭니다. `EDC_EXTERNAL_REGISTERED`. 변경 사항을 저장합니다.
1. 관리 콘솔 홈 페이지에서 **[!UICONTROL 서비스]** > **[!UICONTROL Rights Management]** > **[!UICONTROL 초대된 사용자 및 로컬 사용자]**. 다음 **[!UICONTROL 초대된 사용자 추가]** 페이지가 나타납니다.
1. 이메일 주소를 입력합니다(현재 외부 사용자 초대 핸들러가 실제로 이메일 메시지를 보내지 않으므로 이메일 주소가 유효하지 않아도 됨). **[!UICONTROL 확인]**&#x200B;을 클릭합니다. 사용자가 시스템에 초대됩니다.
1. 관리 콘솔 홈 페이지에서 **[!UICONTROL 설정]** > **[!UICONTROL 사용자 관리]** > **[!UICONTROL 사용자 및 그룹]**.
1. 다음에서 **[!UICONTROL 찾기]** 필드에 지정한 이메일 주소를 입력합니다. 클릭 **[!UICONTROL 찾기]**. 초대한 사용자가 로컬 의 사용자로 표시됩니다. `EDC_EXTERNAL_REGISTERED` 도메인.

>[!NOTE]
>
>구성 요소가 중지되거나 제거된 경우 외부 사용자 초대 핸들러가 실패합니다.
