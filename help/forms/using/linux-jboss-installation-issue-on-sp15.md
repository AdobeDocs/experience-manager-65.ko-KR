---
title: JBoss® Linux® 환경의 AEM Forms JEE 6.5.15.0 서비스 팩 설치 문제
description: AEM Forms JEE 6.5.15.0 서비스 팩이 JBoss® Linux® 환경에 제대로 설치되지 않아 패치 변경 사항이 애플리케이션 서버에 적용되지 않습니다. XML 디렉토리에 'RUP_BOM.xml' 파일을 추가합니다.
source-git-commit: 76a3a87408ceb13023737379c20fb44ce5fb180a
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---


# JBoss® 환경의 AEM Forms 6.5.15.0 JEE 서비스 팩 설치 문제 {#aem-forms-installation-issue-environment}

## 문제 {#issue}

AEM Forms JEE 6.5.15.0 서비스 팩이 JBoss® Linux® 환경에 제대로 설치되지 않았습니다. 위치 `PatchInstallerProcessing[1-9*].log` 로그 항목을 파일링합니다. `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component isn't in the installation. Skipping Processing`: 기록됩니다. 이 항목은 AEM Forms JEE 6.5.15.0 서비스 팩 설치가 실패했음을 나타냅니다.

## 적용 대상 {#applies-to}

이 솔루션은 다음에 적용됩니다.
* JBoss® Linux® 환경

>[!NOTE]
>
> 다음 단계를 수행하기 전에 AEM Forms JEE 6.5.15.0 서비스 팩이 응용 프로그램 서버에 최소 한 번 이상 설치되어 있는지 확인하십시오. [XML 디렉토리에 RUP_BOM.xml 파일 추가](#solution-solution).

## 솔루션 {#solution}

AEM Forms JEE 6.5.15.0 서비스 팩의 설치 문제를 해결하려면 다음을 추가하십시오. `RUP_BOM.xml` 파일을 XML 디렉토리에 추가합니다.
1. 패치를 추출한 폴더로 이동합니다 `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. 다음으로 이동 `/CDROM_Installers/Linux/Disk1/InstData` 위치 및 위치 `Resource1.zip` 파일.
1. 다음을 복사합니다. `Resource1.zip` 압축을 푼 폴더 외부의 다른 위치에 있는 파일 `Resource1.zip` 파일.
1. 다음으로 이동 `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` 및 복사 `RUP_BOM.xml` 파일.
1. 다음 위치에 RUP_BOM.xml 파일 붙여넣기 `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. 재설치 [AEM Forms JEE 6.5.15.0 서비스 팩](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).