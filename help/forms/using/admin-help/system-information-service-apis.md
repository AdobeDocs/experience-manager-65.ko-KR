---
title: 시스템 정보 서비스 API
seo-title: System information Service APIs
description: 이 문서에서는 시스템 정보 서비스에서 제공하는 API에 대한 자세한 정보를 제공합니다.
seo-description: This document provides detailed information about the APIs provided bythesystem information service.
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 시스템 정보 서비스 API {#system-information-service-apis}

시스템 정보 서비스는 정보를 검색하기 위한 일련의 REST API를 제공합니다. 다음 표는 API에 대한 자세한 정보를 제공합니다.

<table>
 <thead>
  <tr>
   <th><p>이름</p></th>
   <th><p>URL</p></th>
   <th><p>설명</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>이 API는 의 래퍼입니다. <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a> Java API입니다. 현재 작업 환경의 구성을 검색합니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>호스트 운영 체제의 모든 환경 변수를 검색합니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>애플리케이션 서버 로그가 포함된 zip 파일을 다운로드합니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>config.xml 파일의 모든 콘텐츠를 검색합니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>AEM Forms 서비스의 상태 및 구성 매개 변수를 검색합니다.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>서버 가동 시간, JVM 인수, 시스템 메모리, 힙 크기, 운영 체제 이름, 활성 스레드 수 및 스레드 수를 검색합니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>다음 속성의 값을 검색합니다.</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>기본 문서 최대 인라인 크기</p></li>
     <li><p>DefaultDocumentDisposingTimeout</p></li>
     <li><p>EnableDocumentDBtorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>데이터 서비스 구성 파일 </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>데이터베이스에 대한 자세한 정보를 검색합니다.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>설치된 AEM Forms 구성 요소의 버전 및 라이선스 정보를 검색합니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>호스트 응용 프로그램 서버의 구성 파일을 다운로드합니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>활성 스레드의 카운트 및 스택 추적을 검색합니다. 다음과 같은 매개 변수를 사용할 수 있습니다.</p>
    <ul>
     <li><p>iterations= [n]: 반복 수를 지정합니다. n을 숫자로 바꿉니다. </p></li>
     <li><p>Delay= [n]: 다음 반복을 시작하기 전에 대기할 시간(밀리초)을 지정합니다. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>이 API는 모든 시스템 정보 서비스 API의 래퍼입니다. 내부적으로 모든 시스템 정보 API를 실행하고 정보를 zip 형식으로 다운로드합니다. </p><p><i><strong>참고</strong>: SystemInfo.info은 활성 스레드의 수 및 스택 추적을 제공하지 않습니다. </i></p></td>
  </tr>
 </tbody>
</table>
