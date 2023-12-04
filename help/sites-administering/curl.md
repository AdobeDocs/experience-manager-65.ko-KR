---
title: AEM에서 cURL 사용
seo-title: Using cURL with AEM
description: 일반적인 Adobe Experience Manager 작업에 cURL을 사용하는 방법에 대해 알아봅니다.
seo-description: Learn how to use cURL with AEM.
uuid: 771b9acc-ff3a-41c9-9fee-7e5d2183f311
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d4ceb82e-2889-4507-af22-b051af83be38
exl-id: e3f018e6-563e-456f-99d5-d232f1a4aa55
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 3%

---

# AEM에서 cURL 사용{#using-curl-with-aem}

관리자는 어떤 시스템에서든 일반적인 작업을 자동화하거나 단순화해야 하는 경우가 많습니다. 예를 들어 AEM에서 사용자 관리, 패키지 설치 및 OSGi 번들 관리는 일반적으로 수행해야 하는 작업입니다.

AEM이 빌드되는 Sling 프레임워크의 RESTful 특성으로 인해 대부분의 작업은 URL 호출로 수행할 수 있습니다. cURL은 이러한 URL 호출을 실행하는 데 사용할 수 있으며 AEM 관리자에게 유용한 도구가 될 수 있습니다.

## cURL이란 {#what-is-curl}

cURL은 URL 조작을 수행하는 데 사용되는 오픈 소스 명령줄 도구입니다. HTTP, HTTPS, FTP, FTPS, SCP, SFTP, TFTP, LDAP, DAP, DICT, TELNET, FILE, IMAP, POP3, SMTP, RTSP 등 다양한 인터넷 프로토콜을 지원합니다.

cURL은 URL 구문을 사용하여 데이터를 가져오거나 보내는 데 널리 사용되는 도구로서 1997년에 처음 출시되었습니다. cURL이라는 이름은 원래 &quot;URL 참조&quot;를 의미했습니다.

AEM이 빌드되는 Sling 프레임워크의 RESTful 특성으로 인해 대부분의 작업은 cURL로 실행할 수 있는 URL 호출로 줄일 수 있습니다. [컨텐츠 조작 작업](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) 페이지 활성화, 워크플로우 시작 및 [운영 작업](/help/sites-administering/curl.md#common-operational-aem-curl-commands) 패키지 관리 및 사용자 관리와 같은 기능은 cURL을 사용하여 자동화할 수 있습니다. 또한 다음을 수행할 수 있습니다. [자신만의 cURL 만들기](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) AEM의 대부분의 작업에 대한 명령입니다.

>[!NOTE]
>
>cURL을 통해 실행되는 모든 AEM 명령은 AEM에 대한 모든 사용자와 마찬가지로 인증되어야 합니다. cURL을 사용하여 AEM 명령을 실행할 때는 모든 ACL 및 액세스 권한이 유지됩니다.

## cURL 다운로드 중 {#downloading-curl}

cURL은 macOS 및 일부 Linux 배포판의 표준 부분입니다. 그러나 대부분의 모든 운영 체제에서 사용할 수 있습니다. 최신 다운로드 목록은 다음에서 확인할 수 있습니다. [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

cURL의 소스 리포지토리는 GitHub에서도 찾을 수 있습니다.

## cURL 준비 AEM 명령 작성 {#building-a-curl-ready-aem-command}

워크플로우 트리거, OSGi 구성 확인, JMX 명령 트리거, 복제 에이전트 생성 등과 같은 AEM의 대부분의 작업을 위해 cURL 명령을 작성할 수 있습니다.

특정 작업에 필요한 정확한 명령을 찾으려면 브라우저에서 개발자 도구를 사용하여 AEM 명령을 실행할 때 서버에 대한 POST 호출을 캡처해야 합니다.

다음 단계에서는 Chrome 브라우저 내에서 새 페이지를 만드는 방법을 예로 들어 설명합니다.

1. AEM 내에서 호출할 작업을 준비합니다. 이 경우 의 끝까지 진행했습니다. **페이지 만들기** 마법사지만 아직 클릭하지 않음 **만들기**.

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. 개발자 도구를 시작하고 다음을 선택합니다. **네트워크** 탭. 다음을 클릭합니다. **로그 유지** 옵션을 선택한 다음 콘솔을 지웁니다.

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. 클릭 **만들기** 다음에서 **페이지 만들기** 실제로 워크플로를 만드는 마법사.
1. 결과 POST 작업을 마우스 오른쪽 단추로 클릭하고 를 선택합니다 **복사** > **cURL로 복사**.

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. cURL 명령을 텍스트 편집기에 복사하고 명령에서 시작하는 모든 헤더를 제거합니다. `-H` (아래 이미지에서 파란색으로 강조 표시됨) 및 과 같은 적절한 인증 매개 변수를 추가합니다. `-u <user>:<password>`.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 명령줄을 통해 cURL 명령을 실행하고 응답을 확인합니다.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## 일반적인 운영 AEM cURL 명령 {#common-operational-aem-curl-commands}

다음은 일반적인 관리 및 운영 작업에 대한 AEM cURL 명령 목록입니다.

>[!NOTE]
>
>다음 예에서는 AEM이에서 실행 중이라고 가정합니다. `localhost` 포트 내 `4502` 및 사용자를 사용합니다 `admin` 암호 포함 `admin`. 추가 명령 자리 표시자는 꺾쇠 괄호로 설정됩니다.

### 패키지 관리 {#package-management}

#### 설치된 모든 패키지 나열

```shell
curl -u <user>:<password> http://<host>:<port>/crx/packmgr/service.jsp?cmd=ls
```

#### 패키지 만들기 {#create-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### 패키지 미리 보기 {#preview-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### 패키지 콘텐츠 나열 {#list-package-content}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### 패키지 빌드 {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### 패키지 다시 래핑 {#rewrap-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### 패키지 이름 바꾸기 {#rename-a-package}

```shell
curl -u <user>:<password> -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### 패키지 업로드 {#upload-a-package}

```shell
curl -u <user>:<password> -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### 패키지 설치 {#install-a-package}

```shell
curl -u <user>:<password> -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 패키지 제거 {#uninstall-a-package}

```shell
curl -u <user>:<password> -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 패키지 삭제 {#delete-a-package}

```shell
curl -u <user>:<password> -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 패키지 다운로드 {#download-a-package}

```shell
curl -u <user>:<password> http://localhost:4502/etc/packages/my_packages/test.zip
```

#### 패키지 복제 {#replicate-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip?cmd=replicate
```

### 사용자 관리 {#user-management}

#### 새 사용자 만들기 {#create-a-new-user}

```shell
curl -u <user>:<password> -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### 새 그룹 만들기 {#create-a-new-group}

```shell
curl -u <user>:<password> -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### 기존 사용자에게 속성 추가 {#add-a-property-to-an-existing-user}

```shell
curl -u <user>:<password> -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### 프로필로 사용자 만들기 {#create-a-user-with-a-profile}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### 새 사용자를 그룹의 구성원으로 만들기 {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### 그룹에 사용자 추가 {#add-a-user-to-a-group}

```shell
curl -u <user>:<password> -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 그룹에서 사용자 제거 {#remove-a-user-from-a-group}

```shell
curl -u <user>:<password> -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 사용자의 그룹 멤버십 설정 {#set-a-user-s-group-membership}

```shell
curl -u <user>:<password> -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### 사용자 삭제 {#delete-a-user}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser
```

#### 그룹 삭제 {#delete-a-group}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### 백업 {#backup}

다음을 참조하십시오 [백업 및 복원](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup) 을 참조하십시오.

### OSGi {#osgi}

#### 번들 시작 {#starting-a-bundle}

```shell
curl -u <user>:<password> -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### 번들 중지 {#stopping-a-bundle}

```shell
curl -u <user>:<password> -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### 캐시 무효화 {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### 캐시 제거 {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### 복제 에이전트 {#replication-agent}

#### 에이전트 상태 확인 {#check-the-status-of-an-agent}

```shell
curl -u <user>:<password> "http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish
```

#### 에이전트 삭제 {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u <user>:<password>
```

#### 에이전트 만들기 {#create-an-agent}

```shell
curl -u <user>:<password> -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### 에이전트 일시 중지 {#pause-an-agent}

```shell
curl -u <user>:<password> -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

#### 에이전트 큐 지우기 {#clear-an-agent-queue}

```shell
curl -u <user>:<password> -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

### 커뮤니티 {#communities}

#### 배지 할당 및 취소 {#assign-and-revoke-badges}

다음을 참조하십시오 [커뮤니티 점수 및 배지](/help/communities/implementing-scoring.md#assign-and-revoke-badges) 을 참조하십시오.

다음을 참조하십시오 [채점 및 배지 핵심 사항](/help/communities/configure-scoring.md#example-setup) 을 참조하십시오.

#### MSRP 리인덱싱 {#msrp-reindexing}

다음을 참조하십시오 [MSRP - MongoDB 저장소 리소스 공급자](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command) 을 참조하십시오.

### 보안 {#security}

#### CRX DE Lite 활성화 및 비활성화 {#enabling-and-disabling-crx-de-lite}

다음을 참조하십시오 [AEM에서 CRXDE Lite 활성화](/help/sites-administering/enabling-crxde-lite.md) 을 참조하십시오.

### 데이터 저장소 가비지 컬렉션 {#data-store-garbage-collection}

다음을 참조하십시오 [데이터 저장소 가비지 수집](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 을 참조하십시오.

### Analytics 및 Target 통합 {#analytics-and-target-integration}

다음을 참조하십시오 [Adobe Analytics 및 Adobe Target 선택](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script) 을 참조하십시오.

### 단일 사인온 {#single-sign-on}

#### 테스트 헤더 보내기 {#send-test-header}

다음을 참조하십시오 [단일 사인온](/help/sites-deploying/single-sign-on.md) 을 참조하십시오.

## 일반 컨텐츠 조작 AEM cURL 명령 {#common-content-manipulation-aem-curl-commands}

다음은 컨텐츠 조작을 위한 AEM cURL 명령 목록입니다.

>[!NOTE]
>
>다음 예에서는 AEM이에서 실행 중이라고 가정합니다. `localhost` 포트 내 `4502` 및 사용자를 사용합니다 `admin` 암호 포함 `admin`. 추가 명령 자리 표시자는 꺾쇠 괄호로 설정됩니다.

### 페이지 관리 {#page-management}

#### 페이지 활성화 {#page-activation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### 페이지 비활성화 {#page-deactivation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### 트리 활성화 {#tree-activation}

```shell
curl -u <user>:<password> -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### 페이지 잠금 {#lock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 페이지 잠금 해제 {#unlock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 페이지 복사 {#copy-page}

```shell
curl -u <user>:<password> -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### 워크플로 {#workflows}

다음을 참조하십시오 [프로그래밍 방식으로 워크플로우와 상호 작용](/help/sites-developing/workflows-program-interaction.md) 을 참조하십시오.

### Sling 콘텐츠 {#sling-content}

#### 폴더 만들기 {#create-a-folder}

```shell
curl -u <user>:<password> -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### 노드 삭제 {#delete-a-node}

```shell
curl -u <user>:<password> -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### 노드 이동 {#move-a-node}

```shell
curl -u <user>:<password> -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### 노드 복사 {#copy-a-node}

```shell
curl -u <user>:<password> -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Sling PostServlet을 사용하여 파일 업로드 {#upload-files-using-sling-postservlet}

```shell
curl -u <user>:<password> -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### Sling PostServlet 및 노드 이름 지정을 사용하여 파일 업로드 {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u <user>:<password> -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### 컨텐츠 유형을 지정하는 파일 업로드 {#upload-files-specifying-a-content-type}

```shell
curl -u <user>:<password> -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### 자산 조작 {#asset-manipulation}

다음을 참조하십시오 [Assets HTTP API](/help/assets/mac-api-assets.md) 을 참조하십시오.
