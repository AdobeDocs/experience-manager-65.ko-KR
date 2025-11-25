---
title: AEM Forms JEE 패치 설치 관리자
description: AEM Forms JEE 패치 설치 관리자를 사용하여 AEM 6.5 Forms 구성 요소의 문제를 해결하는 방법에 대해 알아봅니다.
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
hidefromtoc: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 24%

---

# AEM Forms JEE 패치 설치 관리자 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>자세한 내용을 보거나 패치를 얻으려면 [지원 팀에 문의](https://experienceleague.adobe.com/?support-solution=General&support-tab=home#support)하십시오.

## 패치 설치 관리자 정보 {#about-the-patch-installer}

AEM 6.5 Forms JEE 패치 설치 프로그램에는 이 패치가 릴리스될 때까지 사용할 수 있는 AEM 6.5 Forms JEE의 모든 구성 요소에 대한 모든 해결된 문제가 포함되어 있습니다. 해결된 문제의 전체 목록은 최신 [서비스 팩 릴리스 정보](release-notes.md)를 참조하세요.

## 패치 설치 사전 요구 사항 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## 패치 설치 및 구성 {#installing-and-configuring-the-patch}

1. &lt;*AEM_forms_root*>/deploy 폴더를 백업합니다. 빠른 수정 사항을 제거하려는 경우 필요합니다.
1. 애플리케이션 서버를 중지합니다.
1. 패치 설치 관리자 아카이브 파일을 하드 드라이브에 추출합니다.
1. 사용 중인 운영 체제에 따라 이름이 지정된 디렉터리에서 다음 작업을 수행합니다.

   * **Windows**
설치 관리자를 복사한 하드 디스크의 설치 미디어 또는 폴더로 이동하고 aemforms65_cfp_install.exe 파일을 두 번 클릭합니다.

      * (Windows 32비트) `Windows\Disk1\InstData\VM`
      * (Windows 64비트) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
적절한 디렉터리로 이동한 다음 명령 프롬프트에서 `./aem65_cfp_install.bin`을(를) 입력합니다.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   설치 과정을 안내하는 설치 마법사가 시작됩니다.

1. 소개 패널에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. **설치 폴더 선택** 화면에서 표시되는 기본 위치가 기존 설치에 맞는지 확인하거나 **[!UICONTROL 찾아보기]**&#x200B;를 클릭하여 AEM Forms가 설치된 대체 폴더를 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 빠른 수정 패치 요약 정보를 읽고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 사전 설치 요약 정보를 읽고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.
1. 설치가 완료되면 **[!UICONTROL 다음]**&#x200B;을 클릭하여 설치된 파일에 빠른 수정 업데이트를 적용합니다.

1. **[Windows 전용]:** 다음을 수행합니다.
   * **완료**&#x200B;를 클릭하기 전에 **[!UICONTROL 구성 관리자 시작]** 옵션을 선택 취소하십시오. **의** ConfigurationManager.bat **파일을 사용하여**&#x200B;구성 관리자`[aem-forms root]\configurationManager\bin`를 실행하십시오.

   * 또는 **완료**&#x200B;를 클릭하기 전에 **[!UICONTROL 구성 관리자 시작]** 옵션을 선택 취소하십시오. **ConfigurationManager.exe** 또는 **ConfigurationManager_IPv6.exe**&#x200B;를 사용하여 **Configuration Manager**&#x200B;을(를) 실행하기 전에 *`<AEMForms_Install_Dir>\configurationManager\bin`* 디렉터리로 이동하여 **ConfigurationManager.lax** 및 **ConfigurationManager_IPV6.lax**&#x200B;을(를) 최신 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 및 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 파일로 바꾸고, 검색하고 이 두 파일에서 **axis-1.4.1.1.jar**&#x200B;을(를) **axis-1.4.1.2.jar**(으)로 바꿉니다.

   >[!NOTE]
   >
   >**ConfigurationManager.bat** 파일을 사용하면 .lax 파일의 이름을 수동으로 업데이트하지 않아도 됩니다.
   >

1. **[Unix 기반 전용]:**

   * 기본적으로 **구성 관리자 시작** 확인란이 선택됩니다. **[!UICONTROL 완료]**&#x200B;를 클릭하여 구성 관리자를 즉시 실행하거나 **구성 관리자**&#x200B;를 나중에 실행하려면 **완료**&#x200B;를 클릭하기 전에 **[!UICONTROL 구성 관리자 시작]** 옵션을 선택 취소하십시오. **디렉터리에 있는 적절한 스크립트를 사용하여 나중에**&#x200B;구성 관리자`[AEM_forms_root]/configurationManager/bin`를 시작할 수 있습니다.

1. 응용 프로그램 서버에 따라 다음 문서 중 하나를 선택하고 *AEM 양식 구성 및 배포* 섹션의 지침을 따릅니다.

   * [JBoss용 AEM 양식 설치 및 배포®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [WebSphere용 AEM 양식 설치 및 배포®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (JBoss®만 해당) 패치를 설치하고 서버를 구성한 후 JBoss® 애플리케이션 서버의 tmp 및 작업 디렉토리를 삭제합니다.

## 배포 후 구성 {#post-deployment-configurations}

### SAML 구성 {#saml-configurations}

SAML 인증이 구성되어 있고 큰 IDP 메타데이터와 관련된 문제가 있는 경우 패치를 설치한 후 다음 작업을 수행하십시오.

1. 응용 프로그램 서버에서 다음 시스템 속성을 설정합니다.\
   `um.saml.enable.large.xml=true`
1. 서버를 다시 시작합니다.
1. 기존 SAML 인증 공급자를 삭제하고 SAML 설정에 설명된 대로 기존 도메인에 대해 다시 추가합니다.

>[!NOTE]
>
> SDK를 다시 시작하려면 &#39;Ctrl+C&#39; 명령을 사용하는 것이 좋습니다. 예를 들어 Java 프로세스를 중지하는 것과 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 수 있습니다.

## 영향을 받는 모듈 {#impacted-modules}

* 문서 서비스
* 문서 보안
* Foundation JEE

[지원팀에 문의](https://experienceleague.adobe.com/?support-solution=General&support-tab=home#support)
