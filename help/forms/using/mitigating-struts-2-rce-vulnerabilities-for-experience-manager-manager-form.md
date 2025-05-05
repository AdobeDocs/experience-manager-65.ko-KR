---
title: JEE에서 Experience Manager Forms의 Struts 2 취약성 완화
description: JEE에서 Experience Manager Forms의 Struts 2 취약성 완화
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 73b5aff2-1320-4d9a-8972-54c4fdd3a2c2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Experience Manager Forms의 Struts 2 취약성 완화 {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## 문제

Java EE 웹 애플리케이션 개발을 위한 인기 있는 오픈 소스 웹 애플리케이션 프레임워크인 Struts 2에 심각한 보안 취약성이 보고되었습니다. 다음 취약성이 분석되었습니다.

| 취약성 | 영향을 받는 사항 | 영향을 받지 않는 것은? |
|---|---|---|
| [CVE-2023-50164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-50164) | JEE의 6.5 Forms Experience Manager(6.5GA에서 6.5.19.0으로 바뀐 모든 버전) | <ul><li> Experience Manager Forms Workbench (모든 버전)</li> <li> OSGi의 Experience Manager Forms(모든 버전) </li> <li> Experience Manager Forms as a Cloud Service </li> <ul> |

## 해결 방법

다음 표에는 영향을 받는 모든 버전에 대한 해결 방법이 나와 있습니다.

| 릴리스 | 현재 버전 | 사용자 작업 |
|---|---|---|
| JEE의 6.5 Forms Experience Manager | 6.5.19.0 | [최신 서비스 팩 설치](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=ko) |
| JEE의 6.5 Forms Experience Manager | 6.5.13.0 - 6.5.18.0 | 다음 방법 중 하나를 사용하십시오. <ul><li>  <a href="https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=ko"> 최신 서비스 팩 </a> 설치 </li> <li> <a href ="#use-manual-mitigation-steps"> 수동 완화 단계 사용 </a> |
| JEE의 6.5 Forms Experience Manager | 6.5 - 6.5.12.0 | [최신 서비스 팩 설치](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=ko) </br> </br> **참고:** AEM Forms은 현재 6.5.13.0부터 6.5.19.0까지 버전을 지원합니다. 이전 버전을 사용 중인 경우 6.5.13.0 이상 릴리스로 업그레이드하는 것이 좋습니다. AEM 6.5.13.0 이상 릴리스를 설치하는 방법은 릴리스 노트를 참조하십시오. |

### 수동 완화 단계 사용 {#use-manual-mitigation-steps}

수동 완화 단계를 사용하여 서비스 팩 13을 실행하는 AEM 6.5 Form Server에서 서비스 팩 18을 실행하는 AEM 6.5 Form Server(6.5.13.0 - 6.5.18.0)로 문제를 해결할 수 있습니다.

1. 로컬 폴더에 [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar)을(를) 다운로드합니다. 예: C:\Users\labuser\Desktop\struts2-core-2.5.33.jar.
1. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip)에서 AEM Forms on JEE 수동 패치 도구를 다운로드합니다.
1. 수동 패치 작업 도구 아카이브의 압축을 해제합니다. 예를 들어 `/Users/labuser/Desktop/archive-patcher-1.0.0 folder`에 압축을 풉니다. 다음 파일이 추출됩니다.
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh

>[!BEGINTABS]

>[!TAB Windows]

1. 모든 서버 인스턴스 및 로케이터를 종료합니다.

1. 터미널 창을 열고 AEM Forms on JEE 수동 패치 도구(추출된 파일)가 포함된 폴더로 이동합니다.

1. 이전 struts2 라이브러리가 있는 모든 파일을 검색하려면 다음 명령을 실행하십시오. 명령을 실행하기 전에 명령의 경로를 AEM Forms 서버의 경로로 바꿉니다.


   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >이 도구는 런타임 시 종속성을 다운로드하므로 인터넷 연결이 필요합니다. 따라서 도구를 실행하기 전에 인터넷에 연결되어 있는지 확인하십시오.

1. 재귀 즉석 교체에 대해 나열된 순서로 다음 명령을 실행합니다. 명령을 실행하기 전에 명령의 경로를 AEM Forms 서버 및 `struts2-core-2.5.33.jar` 파일의 경로로 바꾸십시오.



   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$ -action=replace C:\Users\labuser\Desktop\struts2-core-2.5.33.jar
   ```

   위의 단계는 이전 struts2 라이브러리로 모든 귀 파일을 패치합니다.

1. 이전 EAR의 배포를 취소하고 내보내기 폴더에서 사용할 수 있는 패치된 EAR 파일을 애플리케이션 서버에 배포합니다.

1. AEM Forms 서버를 시작합니다.

>[!TAB Linux]

1. 모든 서버 인스턴스 및 로케이터를 종료합니다.

1. 터미널 창을 열고 AEM Forms on JEE 수동 패치 도구(추출된 파일)가 포함된 폴더로 이동합니다.

1. 이전 struts2 라이브러리가 있는 모든 파일을 검색하려면 다음 명령을 실행하십시오. 명령을 실행하기 전에 명령의 경로를 AEM Forms 서버의 경로로 바꿉니다.


   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >이 도구는 런타임 시 종속성을 다운로드하므로 인터넷 연결이 필요합니다. 따라서 도구를 실행하기 전에 인터넷에 연결되어 있는지 확인하십시오.

1. 재귀 즉석 교체에 대해 나열된 순서로 다음 명령을 실행합니다. 명령을 실행하기 전에 명령의 경로를 AEM Forms 서버 및 `struts2-core-2.5.33.jar` 파일의 경로로 바꾸십시오.



   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$ -action=replace /opt/struts2-core-2.5.33.jar
   ```

   위의 단계는 이전 struts2 라이브러리로 모든 귀 파일을 패치합니다.

1. 이전 EAR의 배포를 취소하고 내보내기 폴더에서 사용할 수 있는 패치된 EAR 파일을 애플리케이션 서버에 배포합니다.

1. AEM Forms 서버를 시작합니다.

>[!ENDTABS]




<!-- 
### Manual patching tool 


>[!BEGINTABS]

>[!TAB Windows]

    ```
    
    patch-archive.bat [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.

>[!TAB macOS]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  

>[!TAB Linux]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  



>[!ENDTABS]









-->
