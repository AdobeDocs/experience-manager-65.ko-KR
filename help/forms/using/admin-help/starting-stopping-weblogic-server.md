---
title: WebLogic Server 시작 및 중지
seo-title: WebLogic Server 시작 및 중지
description: 몇 가지 절차에 따라 AEM 양식 모듈을 배포할 WebLogic Server 인스턴스를 시작하거나 중지해야 합니다. 이 문서에서는 WebLogic Server를 시작 및 중지하는 방법에 대해 설명합니다.
seo-description: 몇 가지 절차에 따라 AEM 양식 모듈을 배포할 WebLogic Server 인스턴스를 시작하거나 중지해야 합니다. 이 문서에서는 WebLogic Server를 시작 및 중지하는 방법에 대해 설명합니다.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# WebLogic Server 시작 및 중지 {#starting-and-stopping-weblogic-server}

몇 가지 절차에 따라 AEM 양식 모듈을 배포할 WebLogic Server 인스턴스를 시작하거나 중지해야 합니다. 수행 중인 작업에 따라 WebLogic Server가 중지되거나 실행 중인지 확인합니다.

<table>
 <thead>
  <tr>
   <th><p>활동</p></th>
   <th><p>필수 WebLogic 상태</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>WebLogic 도메인 만들기</p></td>
   <td><p>중지됨</p></td>
  </tr>
  <tr>
   <td><p>WebLogic 관리 서버 만들기</p></td>
   <td><p>실행 중</p></td>
  </tr>
  <tr>
   <td><p>서버 스레드 수 증가</p></td>
   <td><p>실행 중</p></td>
  </tr>
  <tr>
   <td><p>AEM 양식 제품 배포</p></td>
   <td><p>실행 중</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Red Hat® Enterprise Linux Advanced Server 4.0에서 WebLogic Server를 실행하는 경우 `LD_ASSUME_KERNEL` `export LD_ASSUME_KERNEL=2.4.19` 명령을 사용하여 환경 변수를 2.4.19로 설정합니다. 그런 다음 이 환경 변수를 설정한 동일한 셸에서 WebLogic Server를 실행합니다.

## WebLogic Server 시작 {#start-weblogic-server}

1. 명령 프롬프트에서 appserver root/ *[user_projects]*/domains/*[appserverdomain으로 이동합니다]*.
1. 다음 명령을 입력합니다.

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## WebLogic Server 중지 {#stop-weblogic-server}

1. 웹 브라우저의 URL `https://[host name]:7001/console` 줄에 입력하여 WebLogic Server 관리 콘솔을 시작합니다.
1. 이 WebLogic 구성을 만들 때 사용한 사용자 이름과 암호를 입력하여 로그인한 다음 로그인을 클릭합니다.
1. 변경 센터에서 잠금 및 편집을 클릭합니다.
1. 도메인 구조에서 환경 > 서버를 클릭합니다.
1. AdminServer를 클릭하고 AdminServer 설정 창에서 컨트롤 탭을 클릭합니다.
1. 서버 상태 테이블에서 AdminServer가 선택되었는지 확인하고 종료를 클릭합니다.
1. [작업 완료 시]를 선택하여 서버를 정상적으로 종료하거나 [지금 강제 종료]를 선택하여 진행 중인 작업을 완료하지 않고 서버를 즉시 중지합니다.
1. Server Life Cycle Assistant 창에서 Yes 를 클릭하여 종료를 완료합니다.

WebLogic Server 관리 콘솔을 더 이상 사용할 수 없으며 시작 명령을 실행했다는 명령 프롬프트를 사용할 수 있습니다.

## WebLogic 관리 콘솔 시작 {#start-weblogic-administration-console}

1. WebLogic Admin Server가 아직 실행되고 있지 않은 경우 명령 프롬프트에서 *[appserver 루트]\user_projects\domains\[도메인 이름]*디렉토리로 이동하여 다음 명령을 입력합니다.

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Port가 `https://*[host name]:`[비보안 수신] 포트인 웹 브라우저의 URL `/console` 행에 Port를 입력하여 *[WebLogic Server 관리 콘솔에]* 액세스합니다. 기본적으로 이 포트 값은 7001입니다.
1. 로그인 화면에서 관리자 사용자 이름과 암호를 입력하고 로그인을 클릭합니다.

## 시작 노드 관리자 {#start-node-manager}

1. WebLogic Server가 실행 중인지 확인합니다.
1. 새 명령 프롬프트에서 appserver root *[]*/server/bin으로 이동합니다.
1. 다음 명령을 입력합니다.

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## 노드 관리자 중지 {#stop-node-manager}

WebLogic Server를 종료한 후 노드 관리자를 호출한 명령 프롬프트를 닫을 수 있습니다.

## WebLogic 관리 서버 시작 {#start-a-weblogic-managed-server}

>[!NOTE]
>
>이 작업은 WebLogic 도메인 및 관리 서버를 만든 후에만 수행할 수 있습니다.

1. WebLogic Server 및 노드 관리자가 실행 중인지 확인합니다.
1. 웹 브라우저의 URL 행에 `https://`*[호스트 이름]:[port ]*를 입력하여 WebLogic Server 관리 콘솔을`/console`시작합니다.
1. 도메인 구조에서 환경 > 서버를 클릭합니다.
1. 오른쪽 창에서 컨트롤 탭을 클릭합니다.
1. 시작할 관리 서버를 선택합니다.
1. 시작할 관리 대상 서버 아래의 시작 단추를 클릭합니다.

## WebLogic 관리 서버 중지 {#stop-a-weblogic-managed-server}

1. 웹 브라우저의 URL 행에 `https://`*[호스트 이름]:[port ]*를 입력하여 WebLogic Server 관리 콘솔을`/console`시작합니다.
1. 도메인 구조에서 환경 > 서버를 클릭합니다.
1. 오른쪽 창에서 컨트롤 탭을 클릭합니다.
1. 중지할 관리 대상 서버를 선택합니다.
1. 중지할 관리 대상 서버 아래의 [종료] 단추를 클릭합니다.
1. [작업 완료 시]를 선택하여 서버를 정상적으로 종료하거나 [지금 강제 종료]를 선택하여 진행 중인 작업을 완료하지 않고 서버를 즉시 중지합니다.
1. Server Life Cycle Assistant 창에서 Yes 를 클릭하여 종료를 완료합니다.

