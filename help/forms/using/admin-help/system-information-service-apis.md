---
title: 시스템 정보 서비스 API
description: 이 문서에는 시스템 정보 서비스에서 제공하는 API에 대한 자세한 정보가 나와 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '325'
ht-degree: 100%

---

# 시스템 정보 서비스 API {#system-information-service-apis}

시스템 정보 서비스에서는 정보를 가져오기 위한 일련의 REST API를 제공합니다. 다음 표에는 각 API에 대한 자세한 정보가 나와 있습니다.

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
   <td><p>이 API는 <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system. getProperties</a> Java API의 래퍼입니다. 현재 작업 환경의 구성을 가져옵니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>호스트 운영 체제의 모든 환경 변수를 가져옵니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>애플리케이션 서버 로그가 포함된 zip 파일을 다운로드합니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>config.xml 파일의 모든 내용을 가져옵니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>AEM Forms 서비스의 상태 및 구성 매개변수를 가져옵니다.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>서버 가동 시간, JVM 인수, 시스템 메모리, 힙 크기, 운영 체제 이름, 활성 스레드 수, 스레드 수를 가져옵니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>다음과 같은 속성 값을 가져옵니다.</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposalTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>데이터베이스에 대한 자세한 정보를 가져옵니다.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>설치된 AEM Forms 구성 요소의 버전 및 라이선스 정보를 가져옵니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>호스트 애플리케이션 서버의 구성 파일을 다운로드합니다. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>활성 스레드의 개수와 스택 추적을 가져옵니다. 다음 매개변수를 허용합니다.</p>
    <ul>
     <li><p>iterations=[n]: 반복 횟수를 지정합니다. n을 숫자로 바꾸십시오. </p></li>
     <li><p>Delay=[n]: 다음 반복을 시작하기 전에 대기하는 시간(밀리초)을 지정합니다. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>이 API는 모든 시스템 정보 서비스 API에 대한 래퍼입니다. 내부적으로는 모든 시스템 정보 API를 실행하고 정보를 zip 형식으로 다운로드합니다. </p><p><i><strong>참고</strong>: SystemInfo.info는 활성 스레드의 개수와 스택 추적을 제공하지 않습니다. </i></p></td>
  </tr>
 </tbody>
</table>
