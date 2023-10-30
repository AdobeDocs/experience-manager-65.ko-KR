---
title: AEM Forms JEE 패치 설치 관리자
description: AEM 6.5 Forms 구성 요소의 문제를 해결하기 위한 AEM Forms JEE 패치 설치 관리자
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 19%

---

# AEM Forms JEE 패치 설치 관리자 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[지원 문의](https://www.adobe.com/kr/account/sign-in.supportportal.html) 를 참조하십시오.

## 패치 설치 관리자 정보 {#about-the-patch-installer}

AEM 6.5 Forms JEE 패치 설치 프로그램에는 이 패치가 릴리스될 때까지 사용할 수 있는 AEM 6.5 Forms JEE의 모든 구성 요소에 대한 모든 해결된 문제가 포함되어 있습니다. 최신 항목 보기  [서비스 팩 릴리스 노트](release-notes.md) 해결된 문제의 전체 목록.

## 패치 설치 사전 요구 사항 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## 패치 설치 및 구성 {#installing-and-configuring-the-patch}

1. &lt;*AEM_forms_root*>/폴더 배포 빠른 수정 사항을 제거하려는 경우 필요합니다.
1. 애플리케이션 서버를 중지합니다.
1. 패치 설치 관리자 아카이브 파일을 하드 드라이브에 추출합니다.
1. 사용 중인 운영 체제에 따라 이름이 지정된 디렉터리에서 다음 작업을 수행합니다.

   * **Windows**
설치 관리자를 복사한 하드 디스크의 설치 미디어 또는 폴더로 이동하고 aemforms65_cfp_install.exe 파일을 두 번 클릭합니다.

      * (Windows 32비트) `Windows\Disk1\InstData\VM`
      * (Windows 64비트) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **리눅스**
적절한 디렉터리로 이동한 다음 명령 프롬프트에서 `./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   설치 과정을 안내하는 설치 마법사가 시작됩니다.

1. 소개 패널에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 다음에서 **설치 폴더 선택** 화면에 표시되는 기본 위치가 기존 설치에 맞는지 확인하거나 **[!UICONTROL 찾아보기]** AEM forms가 설치된 대체 폴더를 선택하려면 **[!UICONTROL 다음]**.
1. 빠른 수정 패치 요약 정보를 읽고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 사전 설치 요약 정보를 읽고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.
1. 설치가 완료되면 **[!UICONTROL 다음]**&#x200B;을 클릭하여 설치된 파일에 빠른 수정 업데이트를 적용합니다.

1. **[Windows 전용]:** 다음 단계 중 하나를 수행합니다.
   * 다음 중 하나를 선택 해제합니다. **구성 관리자 시작** 클릭 전 옵션 **[!UICONTROL 완료]**. 실행 **구성 관리자** 를 사용하여 **ConfigurationManager.bat** 파일 위치: `[aem-forms root]\configurationManager\bin`.

   * 또는 을 선택 해제합니다. **구성 관리자 시작** 클릭 전 옵션 **[!UICONTROL 완료]**. 실행 전 **구성 관리자** 사용 **ConfigurationManager.exe** 또는 **ConfigurationManager_IPv6.exe**, 다음으로 이동 *`<AEMForms_Install_Dir>\configurationManager\bin`* 디렉터리 및 바꾸기 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 및 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 파일.

   >>
   [!NOTE]
   >>
   사용 **ConfigurationManager.bat** 파일은 .lax 파일의 이름을 수동으로 업데이트하지 않도록 도와줍니다.
   >

1. **[Unix 기반 전용]:**

   * 다음 **구성 관리자 시작** 기본적으로 확인란이 선택되어 있습니다. 클릭 **[!UICONTROL 완료]** 구성 관리자를 즉시 실행하거나 를 실행하려면 **구성 관리자** 나중에 를 선택 취소합니다. **구성 관리자 시작** 클릭 전 옵션 **[!UICONTROL 완료]**. 시작할 수 있습니다. **구성 관리자** 나중에 적절한 스크립트를 `[AEM_forms_root]/configurationManager/bin` 디렉토리.

1. 애플리케이션 서버에 따라 다음 문서 중 하나를 선택하고 *AEM 양식 구성 및 배포* 섹션.

   * [JBoss용 AEM 양식 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [WebSphere용 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (JBoss만 해당) 패치를 설치하고 서버를 구성한 후 JBoss 애플리케이션 서버의 tmp 및 작업 디렉토리를 삭제합니다.

## 배포 후 구성 {#post-deployment-configurations}

### SAML 구성 {#saml-configurations}

SAML 인증이 구성되어 있고 큰 IDP 메타데이터와 관련된 문제가 있는 경우 패치를 설치한 후 다음을 수행하십시오.

1. 응용 프로그램 서버에서 다음 시스템 속성을 설정합니다.\
   `um.saml.enable.large.xml=true`
1. 서버를 다시 시작합니다.
1. 기존 SAML 인증 공급자를 삭제하고 SAML 설정에 설명된 대로 기존 도메인에 대해 다시 추가합니다.

## 영향을 받는 모듈 {#impacted-modules}

* 문서 서비스
* 문서 보안
* Foundation JEE

[지원 문의](https://www.adobe.com/kr/account/sign-in.supportportal.html)
