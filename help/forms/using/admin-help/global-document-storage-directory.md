---
title: 전역 문서 스토리지 디렉터리
description: 전역 문서 스토리지(GDS) 디렉터리는 프로세스 내에서 사용되는 장기 파일을 저장하는 데 사용되는 디렉터리입니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '684'
ht-degree: 100%

---

# 전역 문서 스토리지 디렉터리{#global-document-storage-directory}

*전역 문서 스토리지(GDS)* 디렉터리는 프로세스 내에서 사용되는 장기 파일을 저장하는 데 사용되는 디렉터리입니다. 이러한 파일에는 PDF, 정책, 양식 템플릿이 포함됩니다. 장기 파일은 많은 AEM Forms 배포의 전반적인 상태에서 중요한 부분입니다. 장기 문서 중 일부 또는 전부가 손실되거나 손상되면 Forms 서버가 불안정해질 수 있습니다. 비동기 작업 호출을 위한 입력 문서도 GDS 디렉터리에 저장되며 요청을 처리하는 데 사용할 수 있어야 합니다. GDS 디렉터리를 호스팅하는 파일 시스템의 안정성을 고려하는 것이 중요합니다. 서비스 품질 및 수준 요구 사항에 적합한 독립 디스크의 중복 배열(RAID)이나 기타 기술을 사용하십시오.

장기 파일에는 민감한 사용자 정보가 포함되어 있을 수 있습니다. AEM Forms API나 사용자 인터페이스를 사용하여 이 정보에 액세스하는 경우 특수 자격 증명이 필요할 수 있습니다. 운영 체제를 통해 GDS 디렉터리를 적절하게 보호하는 것이 중요합니다. 애플리케이션 서버를 실행하는 데 사용되는 관리자 계정만 GDS 디렉터리에 대한 읽기/쓰기 액세스 권한이 있어야 합니다.

GDS에 대한 안전하고 가용성이 높은 디렉터리를 선택하는 것 외에도 데이터베이스에서 문서 저장을 활성화할 수도 있습니다. AEM Forms 데이터베이스를 문서 저장에 사용하더라도 AEM Forms에는 여전히 GDS 디렉터리가 필요합니다. ([데이터베이스를 사용하여 문서 저장 시 백업 옵션](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage)을 참조하십시오.)

AEM Forms 애플리케이션 데이터는 GDS 디렉터리와 AEM Forms 데이터베이스에 있습니다. 다음 표에서는 데이터와 해당 위치를 설명합니다.

<table>
 <thead>
  <tr>
   <th><p>AEM Forms 데이터</p></th>
   <th><p>데이터베이스</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>애플리케이션 데이터(사용자, 역할, 프로세스, 정책, 엔드포인트, 이벤트 등)</p></td>
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

## GDS 디렉터리 구성 {#configuring-the-gds-directory}

GDS 디렉터리 위치는 AEM Forms 설치 프로세스 중에 수동으로 구성할 수 있습니다. 설치 중에 위치 설정이 비어 있으면 해당 위치는 다음과 같이 기본적으로 애플리케이션 서버 설치 아래의 디렉터리로 설정됩니다.

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## 기본 GDS 위치 변경 {#change-the-default-gds-location}

AEM Forms 설치가 완료된 후 관리 콘솔에서 GDS 위치를 변경할 수 있습니다. 데이터 위치를 수동으로 변경하여 프로세스를 완료합니다.

>[!NOTE]
>
> * 다음과 같은 방식으로 데이터를 마이그레이션하지 않으면 데이터가 손실됩니다.
> * 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.


1. 관리 콘솔에 로그인하고 설정 > 핵심 시스템 설정 > 구성을 클릭합니다.
2. 전역 문서 스토리지 디렉터리 상자에 새 GDS 디렉터리의 전체 경로를 입력한 후 확인을 클릭합니다.
3. 즉시 애플리케이션 서버를 종료합니다.
4. 내부 디렉터리 구조를 유지하면서 이전 GDS 디렉터리의 모든 파일을 새 위치로 이동합니다.
5. 애플리케이션 서버를 다시 시작합니다.

## 배포 파일 정보 {#about-deployment-files}

AEM Forms는 서비스 컨테이너와 Java 2 Platform, Enterprise Edition(J2EE) EAR 파일이라는 두 가지 유형의 배포 파일로 구성됩니다. 이 EAR 파일은 AEM Forms의 핵심 기능을 포함하는 표준 J2EE 애플리케이션 번들로 구성됩니다. 애플리케이션 서버별 EAR 파일은 다음과 같습니다.

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

AEM Forms를 구현하려면 어셈블된 EAR 파일과 지원 파일을 AEM Forms 솔루션을 실행할 애플리케이션 서버에 배포해야 합니다. 여러 모듈을 구성하고 어셈블한 경우 배포 가능한 모듈은 배포 가능한 EAR 파일 내에 패키징됩니다. 이러한 파일을 배포하려면 해당 파일을 *[appserver home]*\server\all\deploy 디렉터리에 복사합니다.

모듈과 AEM Forms 보관 파일은 JAR 파일에 패키징됩니다. 해당 파일은 J2EE 유형 파일이 아니므로 애플리케이션 서버에 배포되지 않습니다. 대신 GDS 디렉터리에 복사되고 해당 위치에 대한 참조는 AEM Forms 데이터베이스에 저장됩니다. 이러한 이유로 GDS 디렉터리는 클러스터의 모든 노드에서 공유되어야 합니다. 모든 노드는 DSC의 중앙 저장 디렉터리에 액세스할 수 있어야 합니다.

>[!NOTE]
>
>서비스 컨테이너를 배포하기 전에 GDS 디렉터리를 만들고 구성했는지 확인하십시오. ([GDS 디렉터리 구성](global-document-storage-directory.md#configuring-the-gds-directory) 참조)
