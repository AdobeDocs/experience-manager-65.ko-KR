---
title: 명령줄 시작 및 중지
seo-title: 명령줄 시작 및 중지
description: 명령줄에서 AEM을 시작 및 중지하는 방법을 알아봅니다.
seo-description: 명령줄에서 AEM을 시작 및 중지하는 방법을 알아봅니다.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---


# 명령줄 시작 및 중지{#command-line-start-and-stop}

## 명령줄 {#starting-adobe-experience-manager-from-the-command-line}에서 Adobe Experience Manager 시작

`start` 스크립트는 *&lt;cq-installation>/bin* 디렉토리에서 사용할 수 있습니다. Unix 버전과 Windows 버전이 모두 제공됩니다. 스크립트는 *&lt;cq-installation>* 디렉토리에 설치된 인스턴스를 시작합니다.

이러한 두 버전은 AEM 인스턴스를 시작하고 조정하는 데 사용할 수 있는 환경 변수 목록을 지원합니다.

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
   <td>이 서버가<br />에 수신해야 하는 인터페이스 </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>쉼표<br />로 구분된 실행 모드 </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>jarfile<br /> 이름 </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>JAAS 사용(true인 경우)<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>JAAS 구성 경로<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>기본 JVM 옵션<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>작성자 및 게시 중 일부 실행 모드는 AEM을 처음 시작하기 전에 설정해야 하며 이후에 변경할 수 없습니다. 프로덕션에서 사용할 AEM 인스턴스를 설정하기 전에 자세한 내용은 [실행 모드 설명서](/help/sites-deploying/configure-runmodes.md)를 참조하십시오.

### Windows 플랫폼 start.bat 스크립트 예 {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Unix 플랫폼 시작 스크립트 예 {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>시작 스크립트는 *&lt;cq-installation>/app* 폴더 아래에 설치된 AEM Quickstart를 시작합니다.

## Adobe Experience Manager {#stopping-adobe-experience-manager} 중지

AEM을 중지하려면 다음 중 하나를 수행합니다.

* 사용 중인 플랫폼에 따라:

   * 스크립트 또는 명령줄에서 AEM을 시작한 경우 **Ctrl+C**&#x200B;를 눌러 서버를 종료합니다.
   * UNIX에서 시작 스크립트를 사용한 경우 중지 스크립트를 사용하여 AEM을 중지해야 합니다.

* jar 파일을 두 번 클릭하여 AEM을 시작한 경우 시작 창에서 **On** 단추를 클릭하여 서버를 종료합니다(그런 다음 **Off**).

   ![chlimage_1-63](assets/chlimage_1-63.png)

## 명령줄 {#stopping-adobe-experience-manager-from-the-command-line}에서 Adobe Experience Manager 중지

`stop` 스크립트는 *&lt;cq-installation>/bin* 디렉토리에서 사용할 수 있습니다. Unix 버전과 Windows 버전이 모두 제공됩니다. 스크립트는 *&lt;cq-installation>* 디렉토리에 설치된 실행 중인 인스턴스를 중지합니다.

### Unix 플랫폼 중지 스크립트 예 {#unix-platform-stop-script-example}

```shell
./stop
```

### Windows 플랫폼 stop.bat 스크립트 예 {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

저장소를 재배치하지 않고 미리 구성하려는 경우 다음을 수행해야 합니다.

* 필요한 위치에 `repository.xml` 추출

* 필요에 따라 `repository.xml` 업데이트

* `bootstrap.properties` 만들기 및 `repository.config` 정의

다시 한 번 실제 설치를 시작하기 전에

