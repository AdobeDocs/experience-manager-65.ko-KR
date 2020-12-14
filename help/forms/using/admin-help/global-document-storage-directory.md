---
title: 전역 문서 저장소 디렉토리
seo-title: 전역 문서 저장소 디렉토리
description: GDS(Global Document Storage) 디렉토리는 프로세스 내에서 사용되는 긴 파일 저장에 사용되는 디렉토리입니다.
seo-description: GDS(Global Document Storage) 디렉토리는 프로세스 내에서 사용되는 긴 파일 저장에 사용되는 디렉토리입니다.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 1%

---


# 전역 문서 저장소 디렉터리{#global-document-storage-directory}

*글로벌 문서 저장소(GDS)* 디렉토리는 프로세스 내에서 사용되는 긴 파일 저장 데 사용되는 디렉토리입니다. 이러한 파일에는 PDF, 정책 및 양식 템플릿이 포함되어 있습니다. 긴 기간 파일은 많은 AEM 양식 배포의 전반적인 상태에 있어 매우 중요한 부분입니다. 긴 문서의 일부 또는 전체가 손실되거나 손상되면 양식 서버가 불안정해질 수 있습니다. 비동기 작업 호출을 위한 입력 문서도 GDS 디렉토리에 저장되므로 요청을 처리하는 데 사용할 수 있어야 합니다. GDS 디렉토리를 호스팅하는 파일 시스템의 신뢰성을 고려해야 합니다. RAID(Independent Disks) 또는 기타 기술을 사용자 요구 사항에 맞게 이중화하여 서비스 품질과 수준에 맞게 구성할 수 있습니다.

오래 지속되는 파일에는 중요한 사용자 정보가 포함될 수 있습니다. 이 정보는 AEM 양식 API 또는 사용자 인터페이스를 사용하여 액세스할 때 특별한 자격 증명이 필요할 수 있습니다. GDS 디렉토리는 운영 체제를 통해 올바르게 보호되어야 합니다. 응용 프로그램 서버를 실행하는 데 사용되는 관리자 계정만 GDS 디렉토리에 대한 읽기/쓰기 액세스 권한을 가져야 합니다.

GDS에 대한 고가용성 보안 디렉토리를 선택하는 것 외에도 데이터베이스에서 문서 저장소를 사용하도록 선택할 수 있습니다. 문서 저장소에 AEM 양식 데이터베이스를 사용하더라도 AEM 양식에는 GDS 디렉토리가 필요합니다. (문서 저장소](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage)에 데이터베이스가 사용되는 경우 [백업 옵션을 참조하십시오.)

AEM 양식 애플리케이션 데이터는 GDS 디렉토리 및 AEM 양식 데이터베이스에 있습니다. 다음 표에서는 데이터 및 해당 위치에 대해 설명합니다.

<table>
 <thead>
  <tr>
   <th><p>AEM 양식 데이터</p></th>
   <th><p>데이터베이스</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>응용 프로그램 데이터(사용자, 역할, 프로세스, 정책, 끝점, 이벤트 등)</p></td>
   <td><p>예</p></td>
   <td><p>아니오</p></td>
  </tr>
  <tr>
   <td><p>배포된 서비스 컨테이너</p></td>
   <td><p>예</p></td>
   <td><p>아니오</p></td>
  </tr>
  <tr>
   <td><p>Document Manager </p></td>
   <td><p>아니오</p></td>
   <td><p>예</p></td>
  </tr>
  <tr>
   <td><p>Forms 저장소</p></td>
   <td><p>예</p></td>
   <td><p>아니오</p></td>
  </tr>
  <tr>
   <td><p>시스템 구성</p></td>
   <td><p>예</p></td>
   <td><p>아니오</p></td>
  </tr>
  <tr>
   <td><p>감시 폴더</p></td>
   <td><p>아니오</p></td>
   <td><p>예</p></td>
  </tr>
 </tbody>
</table>

## GDS 디렉터리 {#configuring-the-gds-directory} 구성

AEM 양식을 설치하는 동안 GDS 디렉토리의 위치를 수동으로 구성할 수 있습니다. 설치 중에 위치 설정이 비어 있으면 응용 프로그램 서버 설치 아래에 다음과 같이 해당 위치가 기본적으로 디렉터리로 설정됩니다.

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## 기본 GDS 위치 {#change-the-default-gds-location} 변경

AEM 양식 설치가 완료된 후 관리 콘솔에서 GDS 위치를 변경할 수 있습니다. 프로세스를 완료하려면 데이터를 수동으로 재배치해야 합니다.

>[!NOTE]
>
>다음 방법으로 데이터를 마이그레이션하거나 데이터가 손실됩니다.

1. 관리 콘솔에 로그인하고 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
1. 글로벌 문서 저장소 디렉토리 상자에서 새 GDS 디렉토리의 전체 경로를 입력한 다음 확인을 클릭합니다.
1. 응용 프로그램 서버를 즉시 종료합니다.
1. 기존 GDS 디렉토리에서 새 위치로 모든 파일을 이동하여 내부 디렉토리 구조를 유지합니다.
1. 응용 프로그램 서버를 다시 시작합니다.

## 배포 파일 정보 {#about-deployment-files}

AEM 양식은 서비스 컨테이너와 Java 2 Platform, Enterprise Edition(J2EE) EAR 파일 등 두 가지 유형의 배포 파일로 구성됩니다. EAR 파일은 AEM 양식의 핵심 기능을 포함하는 표준 J2EE 애플리케이션 번들로 구성됩니다. 응용 프로그램 서버별 EAR 파일은 다음과 같습니다.

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

AEM 양식 구현은 조립된 EAR 파일과 지원 파일을 AEM 양식 솔루션을 실행할 계획 있는 애플리케이션 서버에 배포합니다. 여러 모듈을 구성하고 어셈블한 경우 배포 가능한 모듈은 배포 가능한 EAR 파일 내에 패키지됩니다. 이러한 파일을 배포하려면 *[appserver 홈]*\server\all\deploy directory에 복사합니다.

모듈 및 AEM 양식 아카이브 파일은 JAR 파일로 패키지화됩니다. J2EE 형식 파일이 아니므로 응용 프로그램 서버에 배포되지 않습니다. 대신 GDS 디렉토리에 복사되고 해당 위치에 대한 참조가 AEM 양식 데이터베이스에 저장됩니다. 이러한 이유로 GDS 디렉토리는 클러스터의 모든 노드 간에 공유되어야 합니다. 모든 노드는 DSC의 중앙 저장소 디렉토리에 액세스할 수 있어야 합니다.

>[!NOTE]
>
>서비스 컨테이너를 배포하기 전에 GDS 디렉토리를 만들고 구성했는지 확인하십시오. ([GDS 디렉토리 구성](global-document-storage-directory.md#configuring-the-gds-directory) 참조)

