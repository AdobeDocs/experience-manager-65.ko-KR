---
title: 글로벌 문서 스토리지 디렉터리
description: GDS(전역 문서 저장소) 디렉터리는 프로세스 내에서 사용되는 장기 파일을 저장하는 데 사용되는 디렉터리입니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 1%

---

# 글로벌 문서 스토리지 디렉터리{#global-document-storage-directory}

다음 *GDS(글로벌 문서 저장소)* directory 는 프로세스 내에서 사용되는 장기 파일을 저장하는 데 사용되는 디렉토리입니다. 이러한 파일에는 PDF, 정책 및 양식 템플릿이 포함되어 있습니다. 장기 파일은 여러 AEM Forms 배포의 전체 상태에서 중요한 부분입니다. 일부 또는 모든 장기 사용 문서가 손실되거나 손상되면 Forms 서버가 불안정해질 수 있습니다. 비동기 작업 호출에 대한 입력 문서는 GDS 디렉터리에도 저장되므로 요청을 처리할 수 있어야 합니다. GDS 디렉토리를 호스팅하는 파일 시스템의 안정성을 고려하는 것이 중요합니다. 사용자의 서비스 품질 및 수준에 적합한 RAID(Redundant Array of Independent Disks) 또는 기타 기술을 사용합니다.

장기 보존 파일에는 중요한 사용자 정보가 포함될 수 있습니다. 이 정보는 AEM Forms API 또는 사용자 인터페이스를 사용하여 액세스할 때 특수 자격 증명이 필요할 수 있습니다. GDS 디렉토리는 운영 체제를 통해 적절하게 보호되는 것이 중요하다. 응용 프로그램 서버를 실행하는 데 사용되는 관리자 계정만 GDS 디렉터리에 대한 읽기/쓰기 액세스 권한을 가져야 합니다.

GDS에 대해 안전하고 가용성이 높은 디렉토리를 선택할 수 있을 뿐만 아니라 데이터베이스에서 문서 저장을 활성화하도록 선택할 수도 있습니다. 문서 저장을 위해 AEM Forms 데이터베이스를 사용하는 경우에도 AEM Forms에는 여전히 GDS 디렉토리가 필요합니다. (참조: [데이터베이스를 문서 저장소로 사용할 때의 백업 옵션](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM forms 응용 프로그램 데이터는 GDS 디렉토리와 AEM forms 데이터베이스에 있습니다. 다음 표에서는 데이터 및 해당 위치에 대해 설명합니다.

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
   <td><p>애플리케이션 데이터(사용자, 역할, 프로세스, 정책, 끝점, 이벤트 등)</p></td>
   <td><p>예</p></td>
   <td><p>아니요</p></td>
  </tr>
  <tr>
   <td><p>배포된 서비스 컨테이너</p></td>
   <td><p>예</p></td>
   <td><p>아니요</p></td>
  </tr>
  <tr>
   <td><p>문서 관리자 </p></td>
   <td><p>아니요</p></td>
   <td><p>예</p></td>
  </tr>
  <tr>
   <td><p>Forms 저장소</p></td>
   <td><p>예</p></td>
   <td><p>아니요</p></td>
  </tr>
  <tr>
   <td><p>시스템 구성</p></td>
   <td><p>예</p></td>
   <td><p>아니요</p></td>
  </tr>
  <tr>
   <td><p>감시 폴더</p></td>
   <td><p>아니요</p></td>
   <td><p>예</p></td>
  </tr>
 </tbody>
</table>

## GDS 디렉토리 구성 {#configuring-the-gds-directory}

AEM Forms 설치 프로세스 중에 GDS 디렉토리의 위치를 수동으로 구성할 수 있습니다. 설치하는 동안 위치 설정이 비어 있으면 다음과 같이 기본 위치가 응용 프로그램 서버 설치 아래의 디렉토리로 설정됩니다.

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## 기본 GDS 위치 변경 {#change-the-default-gds-location}

AEM Forms 설치가 완료된 후 관리 콘솔에서 GDS 위치를 변경할 수 있습니다. 수동으로 데이터를 재배치하여 프로세스를 완료합니다.

>[!NOTE]
>
>다음과 같은 방식으로 데이터를 마이그레이션하지 않으면 데이터가 손실됩니다.

1. 관리 콘솔에 로그인하고 설정 > 핵심 시스템 설정 > 구성 을 클릭합니다.
1. 글로벌 문서 저장 디렉토리 상자에 새 GDS 디렉토리의 전체 경로를 입력한 다음 확인을 누릅니다.
1. 응용 프로그램 서버를 즉시 종료합니다.
1. 모든 파일을 이전 GDS 디렉토리에서 새 위치로 이동하여 내부 디렉토리 구조를 유지합니다.
1. 응용 프로그램 서버를 다시 시작합니다.

## 배포 파일 정보 {#about-deployment-files}

AEM forms는 서비스 컨테이너와 Java 2 Platform, Enterprise Edition(J2EE) EAR 파일의 두 가지 유형의 배포 파일로 구성됩니다. EAR 파일은 AEM Forms의 핵심 기능이 포함된 표준 J2EE 애플리케이션 번들로 구성됩니다. 애플리케이션 서버별 EAR 파일은 다음과 같습니다.

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

AEM Forms 구현에는 어셈블된 EAR 파일과 지원 파일을 AEM Forms 솔루션을 실행하려는 애플리케이션 서버에 배포하는 작업이 포함됩니다. 여러 모듈을 구성하고 조합한 경우 배포 가능한 모듈은 배포 가능한 EAR 파일 내에 패키지화됩니다. 이러한 파일을 배포하려면 *[appserver 홈]*\server\all\deploy 디렉토리입니다.

모듈 및 AEM Forms 아카이브 파일은 JAR 파일로 패키지됩니다. J2EE 유형 파일이 아니므로 응용 프로그램 서버에 배포되지 않습니다. 대신 GDS 디렉터리에 복사되고 해당 위치에 대한 참조가 AEM Forms 데이터베이스에 저장됩니다. 따라서 GDS 디렉토리는 클러스터의 모든 노드 간에 공유되어야 합니다. 모든 노드는 DSC의 중앙 스토리지 디렉터리에 액세스할 수 있어야 합니다.

>[!NOTE]
>
>서비스 컨테이너를 배포하기 전에 GDS 디렉터리를 만들고 구성했는지 확인하십시오. (참조: [GDS 디렉토리 구성](global-document-storage-directory.md#configuring-the-gds-directory))
