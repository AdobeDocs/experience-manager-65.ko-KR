---
title: CRX2Oak 마이그레이션 도구 사용
description: Adobe Experience Manager과 함께 CRX2Oak 마이그레이션 도구를 사용하는 방법을 알아봅니다. 이 도구는 다른 저장소 간에 데이터를 마이그레이션하는 데 도움이 되도록 설계되었습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: ef3895b9-8d35-4881-8188-c864ae3f0b4c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# CRX2Oak 마이그레이션 도구 사용{#using-the-crx-oak-migration-tool}

## 소개 {#introduction}

CRX2Oak은 다른 저장소 간에 데이터를 마이그레이션하도록 설계된 도구입니다.

Apache Jackrabbit 2를 기반으로 하는 이전 CQ 버전에서 Oak으로 데이터를 마이그레이션하는 데 사용할 수 있으며 Oak 저장소 간에 데이터를 복사하는 데에도 사용할 수 있습니다.

이 위치의 공개 Adobe 저장소에서 최신 버전의 crx2oak를 다운로드할 수 있습니다.
[https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

>[!NOTE]
>
>Apache Oak 및 AEM(Adobe Experience Manager) 지속성의 주요 개념에 대한 자세한 내용은 [AEM 플랫폼 소개](/help/sites-deploying/platform.md)를 참조하십시오.

## 마이그레이션 사용 사례 {#migration-use-cases}

이 도구는 다음 용도로 사용할 수 있습니다.

* 이전 CQ 5 버전에서 AEM 6으로 마이그레이션
* 여러 Oak 저장소 간 데이터 복사
* 다양한 Oak MicroKernel 구현 간에 데이터를 변환합니다.

외부 Blob 저장소(일반적으로 데이터 저장소로 알려짐)를 사용하는 저장소 마이그레이션에 대한 지원은 여러 가지 조합으로 제공됩니다. 가능한 마이그레이션 경로 중 하나는 외부 `FileDataStore`을(를) 사용하는 CRX2 리포지토리에서 `S3DataStore`을(를) 사용하는 Oak 리포지토리로의 경로입니다.

아래 다이어그램은 CRX2Oak에서 지원하는 모든 가능한 마이그레이션 조합을 보여 줍니다.

![chlimage_1-151](assets/chlimage_1-151.png)

## 기능 {#features}

CRX2Oak은 사용자가 지속성 모드의 재구성을 자동화하는 사전 정의된 마이그레이션 프로필을 지정할 수 있는 방식으로 AEM 업그레이드 중에 호출됩니다. 이를 빠른 시작 모드라고 합니다.

추가 맞춤화가 필요한 경우 별도로 실행할 수도 있습니다. 그러나 이 모드에서는 저장소만 변경되며 AEM의 추가 재구성은 수동으로 수행해야 합니다. 이를 독립형 모드라고 합니다.

또한 독립 실행형 모드의 기본 설정을 사용하면 노드 저장소만 마이그레이션되고 새 저장소가 이전 바이너리 저장소를 재사용한다는 점을 주의해야 합니다.

### 자동 빠른 시작 모드 {#automated-quickstart-mode}

AEM 6.3부터 CRX2Oak은 이미 사용 가능한 모든 마이그레이션 옵션으로 구성할 수 있는 사용자 정의 마이그레이션 프로필을 처리할 수 있습니다. 이를 통해 보다 높은 유연성과 AEM 구성을 자동화할 수 있습니다. 이 기능은 독립형 모드로 도구를 사용하는 경우에는 사용할 수 없습니다.

CRX2Oak을 빠른 시작 모드로 전환하려면 이 운영 체제 환경 변수를 사용하여 AEM 설치 디렉토리의 crx-quickstart 폴더에 대한 경로를 정의합니다.

**UNIX 기반 시스템 및 macOS의 경우:**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Windows용:**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### 지원 다시 시작 {#resume-support}

마이그레이션은 나중에 다시 시작할 수 있으므로 언제든지 중단될 수 있습니다.

#### 사용자 정의 가능한 업그레이드 논리 {#customizable-upgrade-logic}

`CommitHooks`을(를) 사용하여 사용자 지정 Java™ 논리를 구현할 수 있습니다. 사용자 지정 값으로 저장소를 초기화하기 위해 사용자 지정 `RepositoryInitializer` 클래스를 구현할 수 있습니다.

#### 메모리 매핑 작업 지원 {#support-for-memory-mapped-operations}

CRX2Oak은 기본적으로 메모리 매핑 작업도 지원합니다. 메모리 매핑은 성능을 크게 향상하므로 가능한 한 사용해야 합니다.

>[!CAUTION]
>
>그러나 Windows 플랫폼에서는 메모리 매핑 작업이 지원되지 않습니다. 따라서 Windows에서 마이그레이션을 수행할 때 **—disable-mmap** 매개 변수를 추가하는 것이 좋습니다.

#### 선택적 컨텐츠 마이그레이션 {#selective-migration-of-content}

기본적으로 이 도구는 `"/"` 경로 아래의 전체 저장소를 마이그레이션합니다. 그러나 마이그레이션해야 하는 콘텐츠를 완벽하게 제어할 수 있습니다.

새 인스턴스에 필요하지 않은 콘텐츠 부분이 있는 경우 `--exclude-path` 매개 변수를 사용하여 콘텐츠를 제외하고 업그레이드 절차를 최적화할 수 있습니다.

#### 경로 병합 {#path-merging}

두 저장소 간에 데이터를 복사해야 하는데 두 인스턴스에 모두 다른 콘텐츠 경로가 있는 경우 `--merge-path` 매개 변수에서 이를 정의할 수 있습니다. 이 경우 CRX2Oak은 새 노드만 대상 저장소에 복사하고 이전 노드만 제자리에 유지합니다.

![chlimage_1-152](assets/chlimage_1-152.png)

#### 버전 지원 {#version-support}

기본적으로 AEM은 수정되는 각 노드 또는 페이지의 버전을 만들어 저장소에 저장합니다. 그런 다음 버전을 사용하여 페이지를 이전 상태로 복원할 수 있습니다.

그러나 이러한 버전은 원래 페이지가 삭제되더라도 삭제되지 않습니다. 오랫동안 작동된 저장소를 처리할 때 마이그레이션은 고립된 버전으로 인해 발생하는 중복 데이터를 재처리할 수 있습니다.

이러한 유형의 상황에 유용한 기능은 `--copy-versions` 매개 변수를 추가하는 것입니다. 저장소를 마이그레이션하거나 복사하는 동안 버전 노드를 건너뛰는 데 사용할 수 있습니다.

`--copy-orphaned-versions=true`을(를) 추가하여 분리된 버전을 복사할지 여부를 선택할 수도 있습니다.

두 매개 변수 모두 `YYYY-MM-DD` 날짜 형식을 지원합니다. 특정 날짜 이후에 버전을 복사하려는 경우.

![chlimage_1-153](assets/chlimage_1-153.png)

#### Source 버전 열기 {#open-source-version}

CRX2Oak의 오픈 소스 버전은 oak 업그레이드 형식으로 사용할 수 있습니다. 다음을 제외한 모든 기능을 지원합니다.

* CRX2 지원
* 마이그레이션 프로필 지원
* 자동 AEM 재구성 지원

자세한 내용은 [Apache 설명서](https://jackrabbit.apache.org/oak/docs/migration.html)를 참조하십시오.

## 매개변수 {#parameters}

### 노드 저장소 옵션 {#node-store-options}

* `--cache`: 캐시 크기(MB)(기본값: `256`)

* `--mmap`: 세그먼트 저장소에 대해 메모리 매핑 파일 액세스 사용
* 원본 RDB 데이터베이스에 대한 `--src-password:` 암호

* 원본 RDB의 `--src-user:` 사용자

* `--user`: 대상 RDB의 사용자

* `--password`: 대상 RDB의 암호입니다.

### 마이그레이션 옵션 {#migration-options}

* `--early-shutdown`: 노드가 복사된 후 커밋 후크가 적용되기 전에 소스 JCR2 저장소를 종료합니다.
* `--fail-on-error`: 소스 리포지토리에서 노드를 읽을 수 없는 경우 강제로 마이그레이션에 실패합니다.
* `--ldap`: LDAP 사용자를 CQ 5.x 인스턴스에서 Oak 기반 인스턴스로 마이그레이션합니다. 이를 수행하려면 Oak 구성의 ID 공급자 이름을 ldap로 지정해야 합니다. 자세한 내용은 [LDAP 설명서](/help/sites-administering/ldap-config.md)를 참조하세요.

* `--ldap-config:` 인증에 여러 LDAP 서버를 사용한 CQ 5.x 저장소의 `--ldap` 매개 변수와 함께 사용합니다. CQ 5.x `ldap_login.conf` 또는 `jaas.conf` 구성 파일을 가리키도록 설정할 수 있습니다. 형식은 `--ldapconfig=path/to/ldap_login.conf`입니다.

### 버전 저장소 옵션 {#version-store-options}

* `--copy-orphaned-versions`: 분리된 버전 복사를 건너뜁니다. 지원되는 매개 변수는 `true`, `false` 및 `yyyy-mm-dd`입니다. 기본값은 `true`입니다.

* `--copy-versions:` 버전 저장소를 복사합니다. 매개 변수: `true`, `false`, `yyyy-mm-dd`. 기본값은 `true`입니다.

#### 경로 옵션 {#path-options}

* 복사하는 동안 포함할 경로를 쉼표로 구분한 `--include-paths:` 목록
* `--merge-paths`: 복사하는 동안 병합할 경로를 쉼표로 구분한 목록
* 복사하는 동안 제외할 경로를 쉼표로 구분한 `--exclude-paths:` 목록입니다.

### Source Blob 저장소 옵션 {#source-blob-store-options}

* `--src-datastore:` 원본 `FileDataStore`(으)로 사용할 데이터 저장소 디렉터리입니다.

* `--src-fileblobstore`: 원본 `FileBlobStore`(으)로 사용할 데이터 저장소 디렉터리입니다.

* `--src-s3datastore`: 원본 `S3DataStore`에 사용할 데이터 저장소 디렉터리입니다.

* `--src-s3config`: 원본 `S3DataStore`에 대한 구성 파일입니다.

### 대상 BlobStore 옵션 {#destination-blobstore-options}

* `--datastore:` 대상 `FileDataStore`(으)로 사용할 데이터 저장소 디렉터리

* `--fileblobstore:` 대상 `FileBlobStore`(으)로 사용할 데이터 저장소 디렉터리

* `--s3datastore`: 대상 `S3DataStore`에 사용할 데이터 저장소 디렉터리

* `--s3config`: 대상 `S3DataStore`에 대한 구성 파일입니다.

### 도움말 옵션 {#help-options}

* `-?, -h, --help:`에 도움말 정보가 표시됩니다.

## 디버깅 {#debugging}

마이그레이션 프로세스에 대한 디버그 정보를 사용하여 프로세스 중에 나타날 수 있는 문제를 해결할 수도 있습니다. 다음에서 도구를 실행하려는 모드에 따라 이 작업을 다르게 수행할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>CRX2Oak 모드</strong></td>
   <td><strong>작업</strong></td>
  </tr>
  <tr>
   <td>빠른 시작 모드</td>
   <td>CRX2Oak을 실행할 때 <strong>(로그 수준 TRACE</strong> 또는 <strong>) 로그 수준 DEBUG </strong> 옵션을 명령줄에 추가할 수 있습니다. 이 모드에서는 로그가 <strong>upgrade.log 파일</strong>(으)로 자동으로 리디렉션됩니다.</td>
  </tr>
  <tr>
   <td>독립형 모드</td>
   <td><p>표준 출력에서 TRACE 이벤트를 표시할 수 있도록 <strong>—trace</strong> 옵션을 CRX2Oak 명령줄에 추가합니다(나중에 검사하려면 리디렉션 문자 '&gt;' 또는 'tee' 명령을 사용하여 로그를 직접 리디렉션해야 함).</p> </td>
  </tr>
 </tbody>
</table>

## 기타 고려 사항 {#other-considerations}

MongoDB 복제 집합으로 마이그레이션할 때 Mongo 데이터베이스에 대한 모든 연결에서 `WriteConcern` 매개 변수를 `2`(으)로 설정해야 합니다.

다음과 같이 연결 문자열 끝에 `w=2` 매개 변수를 추가하여 이 작업을 수행할 수 있습니다.

```xml
java -Xmx4092m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>자세한 내용은 [문제 기록](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options)에 대한 MongoDB 연결 문자열 설명서를 참조하십시오.
