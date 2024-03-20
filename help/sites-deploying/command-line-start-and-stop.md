---
title: 명령줄 시작 및 중지
description: 명령줄에서 Adobe Experience Manager을 시작 및 중지하는 방법에 대해 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 명령줄 시작 및 중지{#command-line-start-and-stop}

## 명령줄에서 Adobe Experience Manager 시작 {#starting-adobe-experience-manager-from-the-command-line}

다음 `start` 스크립트는에서 사용할 수 있습니다. *다음 &lt;cq-installation>/bin* 디렉토리. UNIX® 및 Windows 버전이 모두 제공됩니다. 스크립트는에 설치된 인스턴스를 시작합니다. *&lt;cq-installation>* 디렉토리.

이 두 버전은 AEM(Adobe Experience Manager) 인스턴스를 시작 및 조정하는 데 사용할 수 있는 환경 변수 목록을 지원합니다.

<table>
 <tbody>
  <tr>
   <td><strong>환경 변수 </strong></td>
   <td><strong>설명 </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>중지 및 상태 스크립트에 사용되는 TCP 포트<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>호스트 이름<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>이 서버가 수신할 인터페이스<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>쉼표로 구분된 모드 실행<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>jarfile 이름<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>JAAS 사용(true인 경우)<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>JAS 구성 경로<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>기본 JVM 옵션<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>일부 실행 모드(작성자 및 게시 포함)는 AEM을 처음 시작하기 전에 설정해야 하며 나중에 변경할 수 없습니다. 프로덕션에 사용되는 AEM 인스턴스를 설정하기 전에 다음을 참조하십시오. [실행 모드 설명서](/help/sites-deploying/configure-runmodes.md) 을 참조하십시오.

### Windows platform start.bat 스크립트 예 {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### UNIX® 플랫폼 시작 스크립트 예 {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>시작 스크립트는 아래에 설치된 AEM 빠른 시작을 실행합니다. *다음 &lt;cq-installation>/app* 폴더를 삭제합니다.

## Adobe Experience Manager 중지 중 {#stopping-adobe-experience-manager}

AEM을 중지하려면 다음 중 하나를 수행하십시오.

* 사용하는 플랫폼에 따라 다음 작업을 수행하십시오.

   * 스크립트나 명령줄에서 AEM을 시작한 경우 **Ctrl+C** 서버를 종료합니다.
   * UNIX®에서 시작 스크립트를 사용한 경우 중지 스크립트를 사용하여 AEM을 중지해야 합니다.

* jar 파일을 두 번 클릭하여 AEM을 시작한 경우 **날짜** 시작 창의 단추(그러면 단추가 다음으로 변경됨) **끔**)을 클릭하여 서버를 종료합니다.

  ![chlimage_1-63](assets/chlimage_1-63.png)

## 명령줄에서 Adobe Experience Manager 중지 {#stopping-adobe-experience-manager-from-the-command-line}

다음 `stop` 스크립트는에서 사용할 수 있습니다. *다음 &lt;cq-installation>/bin* 디렉토리. UNIX® 및 Windows 버전이 모두 제공됩니다. 스크립트가에 설치된 실행 중인 인스턴스 중지 *&lt;cq-installation>* 디렉토리.

### UNIX® 플랫폼 중지 스크립트 예 {#unix-platform-stop-script-example}

```shell
./stop
```

### Windows platform stop.bat 스크립트 예 {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

저장소를 재배치하지 않고 사전 구성만 하려는 경우 다음 작업만 하면 됩니다.

* Extract `repository.xml` 필요한 위치로

* 업데이트 `repository.xml` 필요에 따라

* 만들기 `bootstrap.properties` 및 정의 `repository.config`

실제 설치를 시작하기 전에 다시 시도하십시오.
