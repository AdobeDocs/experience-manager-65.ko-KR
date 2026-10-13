---
title: JBoss® Linux® 환경의 AEM Forms JEE 6.5.15.0 서비스 팩 설치 문제
description: AEM Forms JEE 6.5.15.0 서비스 팩이 JBoss® Linux® 환경에 제대로 설치되지 않아 패치 변경 사항이 애플리케이션 서버에 적용되지 않습니다. XML 디렉토리에 'RUP_BOM.xml' 파일을 추가합니다.
SEO Description: AEM Forms JEE 6.5.15.0 service pack  is not installed properly on the JBoss Linux environment.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 1%
---
# JBoss® 환경의 AEM Forms 6.5.15.0 JEE 서비스 팩 설치 문제 {#aem-forms-installation-issue-environment}

## 문제 {#issue}

AEM Forms JEE 6.5.15.0 서비스 팩이 JBoss® Linux® 환경에 제대로 설치되지 않았습니다. `PatchInstallerProcessing[1-9*].log` 파일에 로그 항목 `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`이(가) 기록되었습니다. 이 항목은 AEM Forms JEE 6.5.15.0 서비스 팩을 설치하지 않았음을 나타냅니다.

## 적용 대상 {#applies-to}

이 솔루션은 다음에 적용됩니다.
* JBoss® Linux® 환경

>[!NOTE]
>
> [RUP_BOM.xml 파일을 XML 디렉터리에 추가](#solution-solution)하는 단계를 수행하기 전에 응용 프로그램 서버에 AEM Forms JEE 6.5.15.0 서비스 팩이 한 번 이상 설치되어 있는지 확인하십시오.

## 솔루션 {#solution}

AEM Forms JEE 6.5.15.0 서비스 팩의 설치 문제를 해결하려면 `RUP_BOM.xml` 파일을 XML 디렉터리에 추가하십시오.
1. `AEMForms-6.5.0-0057_jboss_linux.tar.gz` 패치를 추출한 폴더로 이동합니다.
1. `/CDROM_Installers/Linux/Disk1/InstData` 위치로 이동하여 `Resource1.zip` 파일을 찾습니다.
1. 추출된 폴더 외부의 다른 위치에 `Resource1.zip` 파일을 복사하고 `Resource1.zip` 파일의 압축을 풉니다.
1. `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml`(으)로 이동하여 `RUP_BOM.xml` 파일을 복사합니다.
1. `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`에 RUP_BOM.xml 파일을 붙여 넣습니다.
1. [AEM Forms JEE 6.5.15.0 서비스 팩을 다시 설치합니다](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ko).
