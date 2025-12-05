---
title: AEM Forms용 AEM Forms 패치 설치 지침
description: OSGi 및 JEE 환경에 대한 AEM Forms 서비스 팩 설치 지침
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 69761b38aec51f080e53235ae3cff5d4049427f2
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 11%

---

# AEM 6.5 Forms 서비스 팩 설치 지침 {#aem-form-patch-installation-instructions}

## 릴리스 정보

| 제품 | Adobe Experience Manager 6.5 Forms |
|---|---|
| 버전 | 6.5.24.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2025년 12월 4일 |
| 다운로드 URL | [최신 AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>해결된 문제의 전체 목록은 최신 [AEM 서비스 팩 릴리스 정보](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)를 참조하세요.

## Experience Manager Forms 6.5에 포함된 제품

Adobe Experience Manager(AEM) Forms 서비스 팩에는 고객이 요청한 주요 개선 사항, 성능, 안정성 및 보안 향상과 같은 새로운 기능 및 업그레이드된 기능이 포함되어 있습니다. AEM Forms은 최신 기능과 개선 사항을 제공하기 위해 서비스 팩을 정기적으로 릴리스합니다. 기술 스택에 따라 다음 경로 중 하나를 선택하여 환경에 서비스 팩을 다운로드하고 설치합니다.

* [JEE 환경에서 AEM Form에 서비스 팩 다운로드 및 설치](#download-and-install-for-jee-service-pack)
* [OSGi 환경에서 AEM Form에 서비스 팩 다운로드 및 설치](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe은 여섯 번째 서비스 팩마다 전체 설치 관리자를 릴리스합니다. AEM 6.5 Forms 서비스 팩 18(6.5.18.0)은 최신 JEE 전체 설치 프로그램입니다. 전체 설치 관리자는 새로운 플랫폼을 지원하며 일반 서비스 팩 설치 관리자에는 새로운 기능, 버그 수정 및 일반 개선 사항이 포함되어 있습니다. 새로 설치하거나 JEE의 AEM 6.5 Forms 환경에 최신 소프트웨어를 사용할 계획이라면, Adobe은 2019년 4월 08일에 릴리스된 AEM 6.5 Forms 설치 프로그램이나 2022년 3월 03일에 릴리스된 AEM 6.5.18.0 Forms 설치 프로그램 대신 2023년 8월 31일에 릴리스된 AEM 6.5.12.0 JEE의 Forms 전체 설치 프로그램을 사용하는 것이 좋습니다. 전체 설치 관리자를 사용한 후 최신 서비스 팩을 설치합니다.
> * [AEM 6.5 빠른 시작](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)에서 사용할 수 있는 적응형 Forms과 같은 AEM Forms 기능은 탐색 및 평가 목적으로만 사용됩니다. 프로덕션 용도로 사용하려면 AEM Forms에 대해 유효한 라이선스를 확보해야 합니다.

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## JEE 환경의 AEM Form에 서비스 팩 다운로드 및 설치 {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++&#x200B;1. 기존 환경의 백업 수행

1. [CRX 저장소, 데이터베이스 스키마 및 GDS(전역 문서 저장소)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html)를 백업합니다.
1. &lt;*AEM_forms_root*>/deploy 폴더를 백업합니다.

>[!NOTE]
>
> AEM 서비스 팩 설치 관리자를 실행하기 전에 AEM 설치 디렉터리에 대한 쓰기 액세스 권한이 있는지 확인하십시오.

+++

+++&#x200B;2. 필요한 소프트웨어 다운로드

* JEE 서비스 팩의 [AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

* [조각 서블릿](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

* [AEM 서비스 팩](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 추가 기능 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)


+++

+++&#x200B;3. Microsoft Visual C++ 재배포 가능 패키지 설치

* AEM 6.5 Forms이 설치된 컴퓨터에서 Visual Studio 2015, 2017, 2019 및 2022용 Microsoft Visual C++ 재배포 가능 패키지 [64비트 버전을 다운로드하여 설치하십시오](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022).

>[!NOTE]
>
> 이전 버전이 설치된 경우에도 재배포 가능 패키지를 설치하여 최신 버전의 가용성을 보장해야 합니다.

+++

+++&#x200B;4. JEE 서비스 팩에 AEM Forms 설치:

1. 애플리케이션 서버를 중지합니다.
1. 하드 드라이브에 **JEE 서비스 팩의 AEM Forms 설치 관리자 보관**&#x200B;을(를) 추출합니다.

   * **Windows**
복사한 하드 디스크의 설치 미디어 또는 폴더로 이동합니다     설치 관리자에서 `aemforms65_cfp_install.exe` 파일을 두 번 클릭합니다.

      * (Windows 32비트) `Windows\Disk1\InstData\VM`
      * (Windows 64비트) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
적절한 디렉터리로 이동한 다음 셸에서 `./aem65_cfp_install.bin`을(를) 입력합니다.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   설치 과정을 안내하는 설치 마법사가 시작됩니다.

1. 소개 패널에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. **설치 폴더 선택** 화면에서 표시되는 기본 위치가 기존 설치에 맞는지 확인하거나 **[!UICONTROL 찾아보기]**&#x200B;를 클릭하여 AEM Forms가 설치된 대체 폴더를 선택하고 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 서비스 팩 요약 정보를 읽고 **[!UICONTROL 다음]**&#x200B;을(를) 클릭합니다.
1. 사전 설치 요약 정보를 읽고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.
1. 설치가 완료되면 **[!UICONTROL 다음]**&#x200B;을 클릭하여 설치된 파일에 빠른 수정 업데이트를 적용합니다.
1. **[Windows 전용]:** 다음 단계 중 하나를 수행합니다.

   * **완료**&#x200B;를 클릭하기 전에 **[!UICONTROL 구성 관리자 시작]** 옵션을 선택 취소하십시오. **의** ConfigurationManager.bat **파일을 사용하여**&#x200B;구성 관리자`[aem-forms root]\configurationManager\bin`를 실행하십시오.

   * 또는 **완료**&#x200B;를 클릭하기 전에 **[!UICONTROL 구성 관리자 시작]** 옵션을 선택 취소하십시오. **ConfigurationManager.exe** 또는 **ConfigurationManager_IPv6.exe**&#x200B;를 사용하여 **Configuration Manager**&#x200B;을(를) 실행하기 전에 *`<AEMForms_Install_Dir>\configurationManager\bin`* 디렉터리로 이동하여 **ConfigurationManager.lax** 및 **ConfigurationManager_IPV6.lax**&#x200B;을(를) 최신 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 및 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 파일로 바꾸고, 검색하고 이 두 파일에서 **axis-1.4.1.1.jar**&#x200B;을(를) **axis-1.4.1.2.jar**(으)로 바꿉니다.

     >[!NOTE]
     >
     >* **ConfigurationManager.bat** 파일을 업데이트하거나 바꾸면 .lax 파일을 수동으로 업데이트하지 않아도 됩니다.

1. **[Unix 기반 전용]:** 기본적으로 **구성 관리자 시작** 확인란이 선택됩니다. **[!UICONTROL 완료]**&#x200B;를 클릭하여 구성 관리자를 즉시 실행하거나 **구성 관리자**&#x200B;를 나중에 실행하려면 **완료**&#x200B;를 클릭하기 전에 **[!UICONTROL 구성 관리자 시작]** 옵션을 선택 취소하십시오. **디렉터리에 있는 적절한 스크립트를 사용하여 나중에**&#x200B;구성 관리자`[AEM_forms_root]/configurationManager/bin`를 시작할 수 있습니다.

1. 응용 프로그램 서버에 따라 다음 문서 중 하나를 선택하고 *AEM 양식 구성 및 배포* 섹션의 지침을 따릅니다.

   * [JBoss용 AEM 양식 설치 및 배포®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [WebSphere용 AEM 양식 설치 및 배포®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [WebLogic용 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [JBoss® 클러스터용 AEM 양식 설치 및 배포](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [WebSphere® 클러스터용 AEM 양식 설치 및 배포](https://helpx.adobe.com/kr/content/dam/help/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [WebLogic 클러스터용 AEM Forms 설치 및 배포](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* JEE 서비스 팩에 AEM Forms을 설치한 후 appserver를 다시 시작하기 전에 `crx-repository\install` 폴더에서 Forms 추가 기능 패키지를 제거해야 합니다. [소프트웨어 배포 포털](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에서 최신 Forms 추가 기능 패키지를 다운로드합니다.
>* SDK를 다시 시작하려면 &#39;Ctrl+C&#39; 명령을 사용하는 것이 좋습니다. 예를 들어 Java 프로세스를 중지하는 것과 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경에서 불일치가 발생할 수 있습니다.
>* JEE의 AEM Forms에 대한 스프링 프레임워크 취약점을 완화하기 위한 [핫픽스](/help/release-notes/aem-forms-hotfix.md)의 경우, 클러스터 환경에 배포할 때 로케이터가 JDK 17을 사용하여 시작되었는지 확인해야 합니다.

+++

+++&#x200B;5. 설치되지 않은 경우 서블릿 조각을 설치합니다(**필수 단계**).

<!-- >[!NOTE] > > * If you are upgrading from **AEM Service Pack 6.5.15.0**, the installation of the **servlet fragment** is not required. For versions **AEM Service Pack 6.5.14.0** or earlier, it is **mandatory to install** the servlet fragment. -->

서블릿 조각을 다운로드하여 설치하려면 다음을 수행합니다.

1. 조각을 다운로드하지 않은 경우 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)에서 다운로드하십시오.

2. 애플리케이션 서버를 시작하고 로그가 안정될 때까지 기다린 후 번들 상태를 확인합니다.

3. 웹 콘솔 번들을 엽니다. 기본 URL은 `http://[Server]:[Port]/system/console/bundles`입니다.

4. 설치/업데이트를 클릭합니다. 다운로드한 조각 `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`을(를) 선택합니다. **설치** 또는 **업데이트**&#x200B;를 클릭합니다. 응용 프로그램 서버가 안정될 때까지 대기

5. 응용 프로그램 서버를 중지합니다.

+++

+++&#x200B;6. AEM 서비스 팩 설치

1. 인스턴스가 업데이트 모드에 있는 경우(인스턴스가 이전 버전에서 업데이트된 경우) 설치 전에 인스턴스를 다시 시작하십시오. Adobe은 인스턴스의 현재 가동 시간이 높을 경우 다시 시작할 것을 권장합니다.
1. 설치하기 전에 [!DNL Experience Manager] 인스턴스의 스냅숏 또는 새 백업을 만듭니다.
1. [소프트웨어 배포](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에서 서비스 팩을 다운로드합니다. <!-- UPDATE FOR EACH NEW RELEASE -->
1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]**&#x200B;를 선택하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하세요.
1. 패키지를 선택한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

**자동 설치**

[!DNL ExperienceManager] 서비스 팩을 자동으로 설치하는 데 사용할 수 있는 두 가지 방법이 있습니다.<!--       UPDATE FOR EACH NEW RELEASE -->

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다.
패키지는 입니다.      자동으로 설치됩니다.

* 패키지 관리자에서 [HTTP API 사용](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

  >[!NOTE]
  >
  >Experience Manager 서비스 팩은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

  **설치 확인**

  이 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하세요.

   1. 제품 정보 페이지(`/system/console/productinfo`)에는 `Adobe Experience Manager (spversion)`설치된 제품[!UICONTROL .]에 업데이트된 버전 문자열 <!-- UPDATE FOR EACH NEW RELEASE -->이(가) 표시됩니다.
   1. 모든 OSGi 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]** 또는 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 사용).     콘솔: `/system/console/bundles`).
   1. OSGi 번들 `org.apache.jackrabbit.oak-core`의 버전이 1.22.14 이상입니다(WebConsole 사용: `/system/console/bundles`).

+++

+++&#x200B;7. AEM Experience Manager Forms 추가 기능 패키지 설치

1. [!DNL Experience Manager] 서비스 팩을 설치했는지 확인하십시오.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.
1. Experience Manager 6.5 Forms에서 문자를 사용하는 경우 [최신 AEMFD 호환성 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)를 설치하십시오.

+++

## OSGi 환경의 AEM Form에 서비스 팩 다운로드 및 설치 {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++&#x200B;1. 기존 환경의 백업 수행

1. [CRX 저장소 및 데이터베이스 스키마](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html)를 백업합니다.

>[!NOTE]
>
> 관계형 데이터베이스에 대해 AEM Forms 서비스 팩을 설치하는 경우 DB_schema를 백업해야 합니다.

+++

+++&#x200B;2. 필요한 소프트웨어 다운로드

* [AEM 서비스 팩](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 추가 기능 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++ &#x200B;3. Microsoft Visual C++ 재배포 가능 패키지 설치

* AEM 6.5 Forms이 설치된 컴퓨터에서 Visual Studio 2015, 2017, 2019 및 2022용 Microsoft Visual C++ 재배포 가능 패키지 [64비트 버전을 다운로드하여 설치하십시오](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022).

>[!NOTE]
>
>
> 이전 버전이 설치된 경우에도 재배포 가능 패키지를 설치하여 최신 버전의 가용성을 보장해야 합니다.

+++

+++&#x200B;4. AEM 서비스 팩 설치

1. 인스턴스가 업데이트 모드에 있는 경우(인스턴스가 이전 버전에서 업데이트된 경우) 설치 전에 인스턴스를 다시 시작하십시오. Adobe은 인스턴스의 현재 가동 시간이 높을 경우 다시 시작할 것을 권장합니다.
1. 설치하기 전에 [!DNL Experience Manager] 인스턴스의 스냅숏 또는 새 백업을 만듭니다.
1. [소프트웨어 배포](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에서 서비스 팩을 다운로드합니다. <!-- UPDATE FOR EACH NEW RELEASE -->
1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]**&#x200B;를 선택하여 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md)를 참조하세요.
1. 패키지를 선택한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

**자동 설치**

[!DNL Experience Manager] 서비스 팩을 자동으로 설치하는 데 사용할 수 있는 두 가지 방법이 있습니다.<!--  UPDATE FOR EACH NEW RELEASE -->

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지는 입니다.      자동으로 설치됩니다.
* 패키지 관리자에서 [HTTP API 사용](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

  >[!NOTE]
  >
  >Experience Manager 서비스 팩은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

  **설치 확인**

  이 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md)을 참조하세요.

   1. 제품 정보 페이지(`/system/console/productinfo`)에는 `Adobe Experience Manager (spversion)`설치된 제품[!UICONTROL 에 업데이트된 버전 문자열 &#x200B;]이(가) 표시됩니다. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

      1. OSGi 번들 `org.apache.jackrabbit.oak-core`의 버전이 1.22.14 이상입니다(웹 콘솔 사용: `/system/console/bundles`).

+++

+++&#x200B;5. Adobe Experience Manager Forms(AEM) 추가 기능 패키지 설치

1. [!DNL Experience Manager] 서비스 팩을 설치했는지 확인하십시오.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.
1. Experience Manager 6.5 Forms에서 문자를 사용하는 경우 [최신 AEMFD 호환성 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)를 설치하십시오.

+++

## 문제 해결

* 서비스 팩을 설치하는 동안 **패키지 관리자 UI의 대화 상자**&#x200B;가 종료되면 배포에 액세스하기 전에 오류 로그가 안정화될 때까지 기다리십시오. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 Safari 브라우저에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

* 설치가 완료되면 모니터 로그(error.log)를 확인합니다. 로그에 활동이 없을 때까지 몇 분 동안 기다립니다. AEM 인스턴스를 다시 시작합니다.

* AEM Forms **이상 서비스 팩을 설치한 후**&#x200B;서비스를 사용할 수 없음 오류6.5.15.0가 발생하는 경우 [서블릿 조각 및 번들을 설치](/help/forms/using/aem-service-pack-installation-solution.md)하여 오류를 수정하십시오.
