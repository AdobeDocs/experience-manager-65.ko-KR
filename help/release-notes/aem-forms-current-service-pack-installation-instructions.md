---
title: AEM Forms용 AEM Forms 패치 설치 지침
description: OSGi 및 JEE 환경을 위한 AEM Forms 서비스 팩 설치 지침
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 0083de8ba459662d04ba80d8c63f21735d82ac82
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 19%

---

# AEM 6.5 Forms 서비스 팩 설치 지침 {#aem-form-patch-installation-instructions}

## 릴리스 정보

| 제품 | Adobe Experience Manager 6.5 Forms |
|---|---|
| 버전 | 6.5.15.0 |
| 유형 | 서비스 팩 릴리스 |
| 날짜 | 2022년 12월 01일 |
| 다운로드 URL | [최신 AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>최신 항목 보기 [AEM 서비스 팩 릴리스 노트](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html) 를 참조하십시오.

## Experience Manager Forms 6.5에 포함된 제품

Adobe Experience Manager(AEM) Forms 서비스 팩에는 고객이 요청한 주요 개선 사항, 성능, 안정성 및 보안 개선 사항과 같은 새로운 기능과 업그레이드된 기능이 포함되어 있습니다. AEM Forms 릴리스 서비스 팩은 정기적으로 배포하여 최신 기능과 개선 사항을 제공합니다. 스택에 따라 다음 경로 중 하나를 선택하여 환경에 서비스 팩을 다운로드하고 설치합니다.

* [JEE 환경의 AEM Forms에 서비스 팩 다운로드 및 설치](#download-and-install-for-jee-service-pack)
* [OSGi 환경의 AEM 양식에 서비스 팩을 다운로드하여 설치합니다](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> Adobe은 모든 6번째 서비스 팩 후에 전체 설치 프로그램을 릴리스합니다. JEE의 AEM 6.5 Forms 서비스 팩 12(6.5.12.0)이 마지막 전체 설치 프로그램입니다. 전체 설치 프로그램은 새 플랫폼에 대한 지원을 제공하는 반면 일반 서비스 팩 설치 프로그램에는 버그 수정 및 일반 개선 사항만 포함되어 있습니다. JEE 환경에서 AEM 6.5 Forms용 최신 소프트웨어를 새로 설치하거나 사용하려는 경우, Adobe이 2019년 4월 8일에 릴리스된 AEM 6.5 Forms 설치 프로그램 대신 2022년 3월 3일에 릴리스된 JEE 전체 설치 프로그램에서 AEM 6.5.12.0 Forms을 사용하는 것이 좋습니다. 전체 설치 관리자를 사용한 후 최신 서비스 팩을 설치합니다.

## JEE 환경의 AEM Forms에 서비스 팩 다운로드 및 설치 {#download-and-install-for-jee-service-pack}

![JEE 설치](/help/forms/using/assets/jeeinstallation.png)

+++1. 기존 환경의 백업 수행:

1. 백업 [CRX 저장소, 데이터베이스 스키마 및 GDS(글로벌 문서 저장소)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. &lt;*AEM_forms_root*>/deploy 폴더를 만듭니다. 서비스 팩을 제거하려면 필요합니다.

>[!NOTE]
>
> AEM 서비스 팩 설치 관리자를 실행하기 전에 AEM 설치 디렉터리에 대한 쓰기 액세스 권한이 있는지 확인하십시오.

+++

+++2.필요한 소프트웨어를 다운로드합니다.

* [JEE 6.5.15.0 서비스 팩의 AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 추가 기능 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [조각 서블릿](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. JEE 서비스 팩에 AEM Forms 설치:

1. 애플리케이션 서버를 중지합니다.
1. 추출 **JEE 6.5.15.0 서비스 팩 설치 프로그램 아카이브의 AEM Forms** 하드 드라이브에

   * **Windows**
설치 프로그램을 복사한 하드 디스크의 설치 미디어 또는 폴더로 이동한 다음 
`aemforms65_cfp_install.exe` 파일.

      * (Windows 32비트) `Windows\Disk1\InstData\VM`
      * (Windows 64비트) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
해당 디렉토리로 이동하고 쉘과 유형에서 
`./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   설치 과정을 안내하는 설치 마법사가 시작됩니다.

1. 소개 패널에서 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.
1. 설정 **설치 폴더 선택** 화면에서 표시되는 기본 위치가 기존 설치에 맞는지 확인하거나 **[!UICONTROL 찾아보기]** AEM Forms가 설치된 대체 폴더를 선택하려면 **[!UICONTROL 다음]**.
1. 서비스 팩 요약 정보를 읽고 **[!UICONTROL 다음]**.
1. 사전 설치 요약 정보를 읽고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.
1. 설치가 완료되면 **[!UICONTROL 다음]**&#x200B;을 클릭하여 설치된 파일에 빠른 수정 업데이트를 적용합니다.
1. **[Windows 전용]:** 다음 단계 중 하나를 수행합니다.

   * 선택 취소 **구성 관리자 시작** 누르기 전에 옵션 **[!UICONTROL 완료]**. 실행 **구성 관리자** 사용 **ConfigurationManager.bat** 에 있는 파일 `[aem-forms root]\configurationManager\bin`.

   * 또는 **구성 관리자 시작** 누르기 전에 옵션 **[!UICONTROL 완료]**. 실행 전 **구성 관리자** 사용 **ConfigurationManager.exe** 또는 **ConfigurationManager_IPv6.exe**, 다음 위치로 이동합니다. *`<AEMForms_Install_Dir>\configurationManager\bin`* 디렉토리 및 바꾸기 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 및 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 파일.

      >[!NOTE]
      >
      >* 업데이트 또는 바꾸기 **ConfigurationManager.bat** 파일을 사용하면 .lax 파일의 이름을 수동으로 업데이트하지 않아도 됩니다.


1. **[Unix 기반 전용]:** 다음 **구성 관리자 시작** 기본적으로 확인란이 선택됩니다. 클릭 **[!UICONTROL 완료]** 구성 관리자를 즉시 실행하거나 **구성 관리자** 나중에 선택을 취소합니다 **구성 관리자 시작** 누르기 전에 옵션 **[!UICONTROL 완료]**. 시작할 수 있습니다 **구성 관리자** 나중에 에서 적절한 스크립트를 사용하여 `[AEM_forms_root]/configurationManager/bin` 디렉토리.

1. 애플리케이션 서버에 따라 다음 문서 중 하나를 선택하고 *AEM 양식 구성 및 배포* 섹션을 참조하십시오.

   * [JBoss®용 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [WebSphere용 AEM Forms 설치 및 배포®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [WebLogic용 AEM Forms 설치 및 배포](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [JBoss® 클러스터용 AEM Forms 설치 및 배포](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [WebSphere® 클러스터용 AEM Forms 설치 및 배포](https://helpx.adobe.com/content/dam/help/kr/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [WebLogic 클러스터용 AEM Forms 설치 및 배포](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> JEE 서비스 팩에 AEM Forms을 설치한 후에서 Forms 추가 기능 패키지를 제거해야 합니다 `crx-repository\install` 폴더를 클릭한 후 appserver를 다시 시작합니다. 에서 최신 Forms 추가 기능 패키지를 다운로드합니다. [소프트웨어 배포 포털](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

+++4. 서블릿 조각 설치

반드시 설치해야 합니다. **서블릿 조각** JBoss® EAP 7.4.0에서 실행 중인 서버를 제외한 모든 애플리케이션 서버에 대해. 서블릿 조각을 다운로드하여 설치하려면 다음을 수행하십시오.

1. 조각을 다운로드하지 않은 경우 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. 애플리케이션 서버를 시작하고 로그가 안정화될 때까지 기다렸다가 번들 상태를 확인합니다.

1. 웹 콘솔 번들을 엽니다. 기본 URL은 `http://[Server]:[Port]/system/console/bundles`.

1. 설치/업데이트를 클릭합니다. 다운로드한 조각을 선택합니다. `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. 클릭 **설치** 또는 **업데이트**. 애플리케이션 서버가 안정화될 때까지 대기

1. 응용 프로그램 서버를 중지합니다.

+++

+++5. AEM 서비스 팩 을 설치합니다.

1. 인스턴스가 업데이트 모드(이전 버전에서 인스턴스가 업데이트되었을 때)인 경우 설치하기 전에 인스턴스를 다시 시작합니다. Adobe은 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작할 것을 권장합니다.
1. 설치하기 전에 스냅샷 또는 새 백업 [!DNL Experience Manager] 인스턴스.
1. 에서 서비스 팩 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]** 를 눌러 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md).
1. 패키지를 선택한 다음 을 선택합니다 **[!UICONTROL 설치]**.
1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾸고 인스턴스를 다시 시작합니다. 자세한 내용은 [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**자동 설치**

자동으로 설치하는 데 사용할 수 있는 방법에는 두 가지가 있습니다 [!DNL ExperienceManager] 6.5.15.0.<!--       UPDATE FOR EACH NEW RELEASE -->

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다.
패키지가 자동으로 설치됩니다.

* [패키지 관리자에서 HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

   >[!NOTE]
   >
   >Experience Manager 6.5.15.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACHNEW RELEASE -->

**설치 확인**

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`)에는 `Adobe Experience      Manager (6.5.15.0)`설치된 제품[!UICONTROL  아래에 업데이트된 버전 문자열 ]이 표시됩니다.<!-- UPDATE FOR EACH NEW RELEASE -->
1. 모든 OSGi 번들은 다음 중 하나입니다 **[!UICONTROL 활성]** 또는 **[!UICONTROL 조각]** OSGi 콘솔에서(웹 콘솔 사용): `/system/console/bundles`).
1. OSGi 번들 `org.apache.jackrabbit.oak-core` 버전 1.22.13 이상(WebConsole 사용: `/system/console/     bundles`).

+++

+++6. AEM Experience Manager Forms 추가 기능 패키지 설치

1. 를 설치했는지 확인합니다. [!DNL Experience Manager] 서비스 팩.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.
1. Experience Manager 6.5 Forms에서 문자를 사용하는 경우 [최신 AEMFD 호환성 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++


<!-- 1. (JBoss only) After installing the patch and configuring the server, delete  tmp  and work directories of JBoss application server.

>[!IMPORTANT]
>
>Before installing [AEM 6.5.15.0 service pack](#install-the-aem-service-pack-install-aem-service-pack), for all the AEM Forms on JEE environments using any application servers other than JBoss EAP 7.4.0: 
> * Install  the [org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) servlet fragment and wait for the application server to stabilize.
>* If you install the latest [AEM service pack (6.5.15.0)](#install-the-aem-service-pack-install-aem-service-pack), prior to the fragment servlet `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` on JEE environment, the CRX/bundle and the start page show service unavailable errors, [click here](/help/forms/using/aem-service-pack-installation-solution.md) to know the troubleshooting steps. 

### !-->


## OSGi 환경의 AEM 양식에 서비스 팩을 다운로드하여 설치합니다 {#download-and-install-for-osgi-service-pack}

![OSGi 설치 단계](/help/forms/using/assets/osgiinstallation.png)


+++1. 기존 환경의 백업 수행:

1. 백업 [CRX 저장소 및 데이터베이스 스키마](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
> 관계형 데이터베이스에 대한 AEM Forms 서비스 팩을 설치하는 경우 DB_schema를 백업해야 합니다.

+++

+++2.필요한 소프트웨어를 다운로드합니다.

* [AEM 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 추가 기능 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++3. AEM 서비스 팩 을 설치합니다.

1. 인스턴스가 업데이트 모드(이전 버전에서 인스턴스가 업데이트되었을 때)인 경우 설치하기 전에 인스턴스를 다시 시작합니다. Adobe은 인스턴스에 대한 현재 가동 시간이 높은 경우 다시 시작할 것을 권장합니다.
1. 설치하기 전에 스냅샷 또는 새 백업 [!DNL Experience Manager] 인스턴스.
1. 에서 서비스 팩 다운로드 [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 패키지 관리자를 연 다음 **[!UICONTROL 패키지 업로드]** 를 눌러 패키지를 업로드합니다. 자세한 내용은 [패키지 관리자](/help/sites-administering/package-manager.md).
1. 패키지를 선택한 다음 을 선택합니다 **[!UICONTROL 설치]**.
1. S3 커넥터를 업데이트하려면 서비스 팩을 설치한 후 인스턴스를 중지하고 기존 커넥터를 설치 폴더에 제공된 새 이진 파일로 바꾸고 인스턴스를 다시 시작합니다. 자세한 내용은 [Amazon S3 데이터 저장소](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**자동 설치**

자동으로 설치하는 데 사용할 수 있는 방법에는 두 가지가 있습니다 [!DNL Experience Manager] 6.5.15.0.<!--       UPDATE FOR EACH NEW RELEASE -->

* 서버가 온라인 상태일 때 패키지를 `../crx-quickstart/install` 폴더에 넣습니다. 패키지가 자동으로 설치됩니다.
* [패키지 관리자에서 HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)를 사용합니다. 중첩된 패키지가 설치되도록 `cmd=install&recursive=true`을(를) 사용합니다.

   >[!NOTE]
   >
   >Experience Manager 6.5.15.0은 Bootstrap 설치를 지원하지 않습니다. <!-- UPDATE FOR EACH NEW RELEASE -->

**설치 확인**

이번 릴리스에서 사용할 수 있는 인증된 플랫폼을 확인하려면 [기술 요구 사항](/help/sites-deploying/technical-requirements.md).

1. 제품 정보 페이지(`/system/console/productinfo`)에 업데이트된 버전 문자열 표시 `Adobe Experience      Manager (6.5.15.0)` 아래에 [!UICONTROL 설치된 제품]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 모든 OSGI 번들은 OSGi 콘솔에서 **[!UICONTROL ACTIVE]**&#x200B;이거나 **[!UICONTROL FRAGMENT]**&#x200B;입니다(웹 콘솔 사용: `/system/console/bundles`).

   1. OSGi 번들 `org.apache.jackrabbit.oak-core` 버전 1.22.13 이상(웹 콘솔 사용: `/system/console/bundles`).

+++

+++4. AEM Experience Manager Forms 추가 기능 패키지 설치

1. 를 설치했는지 확인합니다. [!DNL Experience Manager] 서비스 팩.
1. 운영 체제에 대한 [AEM Forms 릴리스](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에 나열된 해당 양식 추가 기능 패키지를 다운로드합니다.
1. [AEM Forms 추가 기능 패키지 설치](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)에 설명된 대로 양식 추가 기능 패키지를 설치합니다.
1. Experience Manager 6.5 Forms에서 문자를 사용하는 경우 [최신 AEMFD 호환성 패키지](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## 문제 해결

* If **패키지 관리자 UI의 대화 상자** 서비스 팩을 설치하는 동안 종료되고 배포에 액세스하기 전에 오류 로그가 안정될 때까지 기다립니다. 업데이터 번들 제거와 관련된 특정 로그를 기다린 후 설치가 성공했는지 확인합니다. 일반적으로 이 문제는 Safari 브라우저에서 발생하지만 모든 브라우저에서 간헐적으로 발생할 수 있습니다.

* 설치가 완료되면 모니터 로그(error.log)를 확인합니다. 로그에 활동이 없을 때까지 몇 분 동안 기다립니다. AEM 인스턴스를 다시 시작합니다.

* 혹시라도 **서비스를 사용할 수 없는 오류** 최신 AEM Forms 6.5.15.0 서비스 팩을 설치한 후, [서블릿 조각 및 번들 설치](/help/forms/using/aem-service-pack-installation-solution.md) 오류를 수정하려면 다음을 수행합니다.
