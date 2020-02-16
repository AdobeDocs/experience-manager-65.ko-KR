---
title: CRX2Oak 마이그레이션 도구 사용
seo-title: CRX2Oak 마이그레이션 도구 사용
description: CRX2Oak 마이그레이션 툴을 사용하는 방법을 살펴볼 수 있습니다.
seo-description: CRX2Oak 마이그레이션 툴을 사용하는 방법을 살펴볼 수 있습니다.
uuid: 9b788981-4ef0-446e-81f0-c327cdd3214b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: e938bdc7-f8f5-4da5-81f6-7f60c6b4b8e6
translation-type: tm+mt
source-git-commit: 24290b65a126822eb918fbecc978372394b5b655

---


# CRX2Oak 마이그레이션 도구 사용{#using-the-crx-oak-migration-tool}

## 소개 {#introduction}

CRX2Oak은 서로 다른 저장소 간에 데이터를 마이그레이션하도록 설계된 툴입니다.

Apache Jackrabbit 2를 기반으로 이전 CQ 버전에서 Oak로 데이터를 마이그레이션하는 데 사용할 수 있으며 Oak 저장소 간에 데이터를 복사하는 데에도 사용할 수 있습니다.

다음 위치의 공용 Adobe 저장소에서 최신 버전의 crx2oak을 다운로드할 수 있습니다.[https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak/)

최신 버전의 변경 사항 및 수정 사항은 CRX2Oak 릴리스 [정보에서 확인할 수 있습니다](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/crx2oak.html).

>[!NOTE]
>
>Apache Oak 및 AEM 지속형에 대한 주요 개념에 대한 자세한 내용은 AEM [플랫폼 소개를 참조하십시오](/help/sites-deploying/platform.md).

## 마이그레이션 사용 사례 {#migration-use-cases}

이 도구는 다음 용도로 사용할 수 있습니다.

* 이전 CQ 5 버전에서 AEM 6으로 마이그레이션
* 여러 Oak 저장소 간 데이터 복사
* 서로 다른 Oak MicroKernel 구현 간 데이터 변환

외부 Blob 저장소(일반적으로 데이터 저장소라고 함)를 사용한 저장소 마이그레이션은 서로 다른 조합으로 제공됩니다. 한 가지 가능한 마이그레이션 경로는 CRX2 저장소에서 외부 저장소를 사용하여 Oak `FileDataStore` 저장소로 이동하는 `S3DataStore`것입니다.

아래 다이어그램은 CRX2Oak에서 지원되는 모든 가능한 마이그레이션 조합을 보여 줍니다.

![chlimage_1-151](assets/chlimage_1-151.png)

## 기능 {#features}

CRX2Oak는 사용자가 지속성 모드 재구성을 자동화하는 사전 정의된 마이그레이션 프로필을 지정할 수 있는 방식으로 AEM 업그레이드 중에 호출됩니다. 이를 빠른 시작 모드라고 합니다.

또한 사용자 정의가 더 필요한 경우에 한하여 별도로 실행할 수 있습니다. 그러나 이 모드에서는 저장소만 변경되며 AEM의 추가 재구성은 수동으로 수행해야 합니다. 이를 독립 실행형 모드라고 합니다.

또 다른 주목해야 할 점은 독립형 모드의 기본 설정을 사용하면 노드 저장소만 마이그레이션되고 새 저장소는 이전 이진 저장소를 다시 사용하게 된다는 것입니다.

### 자동화된 빠른 시작 모드 {#automated-quickstart-mode}

AEM 6.3부터 CRX2Oak은 이미 사용 가능한 모든 마이그레이션 옵션으로 구성할 수 있는 사용자 정의 마이그레이션 프로필을 처리할 수 있습니다. 이를 통해 AEM의 구성을 자동화할 수 있으며, 독립 실행형 모드에서 도구를 사용하는 경우 사용할 수 없는 기능을 사용할 수 있습니다.

CRX2Oak를 빠른 시작 모드로 전환하려면 이 운영 체제 환경 변수를 통해 AEM 설치 디렉토리의 crx-quickstart 폴더에 대한 경로를 정의해야 합니다.

**UNIX 기반 시스템 및 macOS의 경우:**

```shell
export SLING_HOME="/path/to/crx-quickstart"
```

**Windows의 경우:**

```shell
SET "SLING_HOME=/path/to/crx-quickstart"
```

#### 지원 재개 {#resume-support}

마이그레이션은 언제든지 중단되고 이후에 다시 시작할 수 있습니다.

#### 맞춤형 업그레이드 로직 {#customizable-upgrade-logic}

사용자 지정 Java 로직을 사용하여 구현할 수도 `CommitHooks`있습니다. 사용자 정의 `RepositoryInitializer` 클래스를 구현하여 사용자 정의 값으로 저장소를 초기화할 수 있습니다.

#### 메모리 매핑 작업 지원 {#support-for-memory-mapped-operations}

또한 CRX2Oak은 기본적으로 메모리 매핑 작업을 지원합니다. 메모리 매핑은 성능을 크게 향상시키며 가능한 한 사용해야 합니다.

>[!CAUTION]
>
>그러나 메모리 매핑 작업은 Windows 플랫폼에서 지원되지 않습니다. 따라서 Windows에서 마이그레이션을 수행할 때 **—disable-mmap** 매개 변수를 추가하는 것이 좋습니다.

#### 선택적 컨텐츠 마이그레이션 {#selective-migration-of-content}

기본적으로 이 도구는 경로 아래의 전체 저장소를 `"/"` 마이그레이션합니다. 그러나 마이그레이션해야 하는 컨텐츠를 완벽하게 제어할 수 있습니다.

새 인스턴스에서 필요하지 않은 컨텐츠의 일부가 있는 경우 `--exclude-path` 매개 변수를 사용하여 컨텐츠를 제외하고 업그레이드 절차를 최적화할 수 있습니다.

#### 경로 병합 {#path-merging}

두 아카이브 간에 데이터를 복사해야 하고 두 인스턴스에 서로 다른 컨텐츠 경로가 있는 경우 `--merge-path` 매개변수에서 정의할 수 있습니다. CRX2Oak은 새 노드만 대상 저장소에 복사하고 이전 노드를 그대로 유지합니다.

![chlimage_1-152](assets/chlimage_1-152.png)

#### 버전 지원 {#version-support}

기본적으로 AEM은 수정되는 각 노드 또는 페이지의 버전을 만들어 저장소에 저장합니다. 그런 다음 버전을 사용하여 페이지를 이전 상태로 복원할 수 있습니다.

그러나 원본 페이지가 삭제되더라도 이러한 버전은 삭제되지 않습니다. 오랫동안 작동 중인 저장소를 처리할 때, 마이그레이션은 분리된 버전으로 인해 발생한 많은 중복 데이터를 처리해야 할 수 있습니다.

이러한 유형의 경우 `--copy-versions` 매개 변수를 추가하는 것이 유용한 기능입니다. 저장소를 마이그레이션하거나 복사하는 동안 버전 노드를 건너뛰는 데 사용할 수 있습니다.

또한 고아 버전을 추가함으로써 복사할지 여부를 선택할 수 `--copy-orphaned-versions=true`있습니다.

또한 두 매개 변수 모두 `YYYY-MM-DD` 날짜 형식을 지원합니다. 이 경우 특정 날짜보다 나중에 버전을 복사할 수 있습니다.

![chlimage_1-153](assets/chlimage_1-153.png)

#### 오픈 소스 버전 {#open-source-version}

CRX2Oak의 오픈 소스 버전은 oak-upgrade의 형태로 제공됩니다. 다음을 제외한 모든 기능을 지원합니다.

* CRX2 지원
* 마이그레이션 프로필 지원
* 자동화된 AEM 재구성 지원

See the [Apache Documentation](https://jackrabbit.apache.org/oak/docs/migration.html) for more information.

## 매개 변수 {#parameters}

### 노드 저장소 옵션 {#node-store-options}

* `--cache`:캐시 크기(MB)(기본값 `256`)

* `--mmap`:세그먼트 저장소에 대해 메모리 매핑 파일 액세스 사용
* `--src-password:` 소스 RDB 데이터베이스의 암호

* `--src-user:` 소스 RDB용 사용자

* `--user`:타깃팅된 RDB의 사용자

* `--password`:대상 RDB의 암호입니다.

### 마이그레이션 옵션 {#migration-options}

* `--early-shutdown`:노드가 복사되고 커밋 후크가 적용되기 전에 소스 JCR2 저장소를 종료합니다.
* `--fail-on-error`:소스 저장소에서 노드를 읽을 수 없는 경우 마이그레이션 오류가 발생합니다.
* `--ldap`:LDAP 사용자를 CQ 5.x 인스턴스에서 Oak 기반 인스턴스로 마이그레이션합니다. 이를 수행하려면 Oak 구성의 ID 공급자 이름을 ldap로 지정해야 합니다. For more information, see the [LDAP documentation](/help/sites-administering/ldap-config.md).

* `--ldap-config:` 인증을 위해 여러 LDAP 서버를 사용한 CQ 5.x 저장소의 `--ldap` 매개 변수와 함께 사용합니다. CQ 5.x `ldap_login.conf` 또는 `jaas.conf` 구성 파일을 가리키는 데 사용할 수 있습니다. 형식은 `--ldapconfig=path/to/ldap_login.conf`입니다.

### 버전 저장소 옵션 {#version-store-options}

* `--copy-orphaned-versions`:분리된 버전 복사를 건너뜁니다. 지원되는 매개 변수는 다음과 같습니다. `true`및 `false` 를 `yyyy-mm-dd`참조하십시오. Defaults to `true`.

* `--copy-versions:` 버전 저장소를 복사합니다. Parameters: `true`, `false`, `yyyy-mm-dd`. Defaults to `true`.

#### 경로 옵션 {#path-options}

* `--include-paths:` 복사 중에 포함할 경로 쉼표로 구분된 목록
* `--merge-paths`:복사하는 동안 병합할 패스의 쉼표로 구분된 목록
* `--exclude-paths:` 복사하는 동안 제외할 경로 목록이 쉼표로 구분되어 있습니다.

### 소스 Blob 저장소 옵션 {#source-blob-store-options}

* `--src-datastore:` 소스로 사용할 데이터 저장소 디렉토리 `FileDataStore`

* `--src-fileblobstore`:소스로 사용할 데이터 저장소 디렉토리 `FileBlobStore`

* `--src-s3datastore`:소스에 사용할 데이터 저장소 디렉토리 `S3DataStore`

* `--src-s3config`:소스의 구성 파일입니다 `S3DataStore`.

### 대상 BlobStore 옵션 {#destination-blobstore-options}

* `--datastore:` 대상으로 사용할 데이터 저장소 디렉토리 `FileDataStore`

* `--fileblobstore:` 대상으로 사용할 데이터 저장소 디렉토리 `FileBlobStore`

* `--s3datastore`:대상에 사용할 데이터 저장소 디렉토리 `S3DataStore`

* `--s3config`:대상에 대한 구성 파일입니다 `S3DataStore`.

### 도움말 옵션 {#help-options}

* `-?, -h, --help:` 도움말 정보를 표시합니다.

## 디버깅 {#debugging}

프로세스 중에 나타날 수 있는 문제를 해결하기 위해 마이그레이션 프로세스에 대한 디버그 정보를 활성화할 수도 있습니다. 도구를 실행할 모드에 따라 다음과 같이 다르게 수행할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>CRX2Oak 모드</strong></td>
   <td><strong>작업</strong></td>
  </tr>
  <tr>
   <td>빠른 시작 모드</td>
   <td>CRX2Oak를 실행할 때 <strong>—로그 수준 TRACE</strong> 또는 <strong>—로그 수준 DEBUG </strong>옵션을 명령줄에 추가할 수 있습니다. 이 모드에서는 로그가 자동으로 <strong>upgrade.log 파일로</strong>리디렉션됩니다.</td>
  </tr>
  <tr>
   <td>독립 실행형 모드</td>
   <td><p>CRX2Oak 명령줄에 <strong>—trace</strong> 옵션을 추가하여 표준 출력에 TRACE 이벤트를 표시합니다(리디렉션 문자를 사용하여 직접 로그를 리디렉션해야 함:나중에 검사할 수 있도록 '&gt;' 또는 'tee' 명령).</p> </td>
  </tr>
 </tbody>
</table>

## 기타 고려 사항 {#other-considerations}

MongoDB 복제본 세트로 마이그레이션할 때 Mongo 데이터베이스에 대한 모든 연결에 대해 `WriteConcern` 매개 변수를 `2` 로 설정해야 합니다.

다음과 같이 연결 문자열 끝에 `w=2` 매개 변수를 추가하면 됩니다.

```xml
java -Xmx4092m -XX:MaxPermSize=1024m -jar crx2oak.jar crx-quickstart/repository/ mongodb://localhost:27017/aem-author?replicaset=replica1&w=2
```

>[!NOTE]
>
>자세한 내용은 쓰기 관련 사항에 대한 MongoDB 연결 문자열 설명서를 [참조하십시오](https://docs.mongodb.org/manual/reference/connection-string/#write-concern-options).

