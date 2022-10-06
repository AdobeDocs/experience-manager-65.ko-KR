---
title: VLT 도구 사용 방법
seo-title: How to use the VLT Tool
description: Jackrabbit FileVault 도구(VLT)는 Jackrabbit/AEM 인스턴스의 컨텐츠를 파일 시스템에 매핑하는 Apache Foundation에서 개발되었습니다
seo-description: The Jackrabbit FileVault tool (VLT) is developed by The Apache Foundation that maps the content of a Jackrabbit/AEM instance to your file system
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
exl-id: efbba312-9fc8-4670-b8f1-d2a86162d075
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2718'
ht-degree: 2%

---

# VLT 도구 사용 방법 {#how-to-use-the-vlt-tool}

Jackrabbit FileVault 도구(VLT)는 [Apache Foundation](https://www.apache.org/) 는 Jackrabbit/AEM 인스턴스의 컨텐츠를 파일 시스템에 매핑합니다. VLT 툴은 소스 제어 시스템 클라이언트(예: 서브버전(SVN) 클라이언트)와 유사한 기능을 가지며 일반 체크인, 체크아웃 및 관리 작업을 제공하며 프로젝트 컨텐츠의 유연한 표현을 위한 구성 옵션을 제공합니다.

명령줄에서 VLT 도구를 실행합니다. 이 문서에서는 시작하기 및 도움말 방법, 그리고 모든 항목의 목록을 포함하여 도구 사용 방법에 대해 설명합니다 [명령](#vlt-commands) 사용 가능 [옵션](#vlt-global-options).

## 개념 및 아키텍처 {#concepts-and-architecture}

자세한 내용은 [파일 개요](https://jackrabbit.apache.org/filevault/overview.html) 및 [Vault FS](https://jackrabbit.apache.org/filevault/vaultfs.html) 공식 페이지의 페이지 [Apache Jackrabbit Filerabbit 설명서](https://jackrabbit.apache.org/filevault/index.html) 를 참조하십시오.

## VLT 시작하기 {#getting-started-with-vlt}

VLT 사용을 시작하려면 다음을 수행해야 합니다.

1. VLT를 설치하고, 환경 변수를 업데이트하고, 무시된 글로벌 하위 버전 파일을 업데이트합니다.
1. AEM 저장소를 설정합니다(아직 설정하지 않은 경우).
1. AEM 저장소를 확인합니다.
1. 리포지토리와 동기화합니다.
1. 동기화가 작동하는지 테스트합니다.

### VLT 도구 설치 {#installing-the-vlt-tool}

VLT 도구를 사용하려면 먼저 설치해야 합니다. 추가 도구이므로 기본적으로 설치되지 않습니다. 또한 시스템의 환경 변수를 설정해야 합니다.

1. FileVault 아카이브 파일을 [Maven 객체 저장소.](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/vault-cli/)
   >[!NOTE]
   >
   >VLT 도구의 소스는 다음과 같습니다 [gitHub에서 사용할 수 있습니다.](https://github.com/apache/jackrabbit-filevault)
1. 아카이브를 추출합니다.
1. 추가 `<archive-dir>/vault-cli-<version>/bin` 환경에 `PATH` 명령 파일이 `vlt` 또는 `vlt.bat` 은 적절히 액세스됩니다. 예:

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. 명령줄 셸을 열고 실행 `vlt --help`. 출력이 다음 도움말 화면과 유사한지 확인합니다.

   ```shell
   vlt --help
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Usage:
     vlt [options] <command> [arg1 [arg2 [arg3] ..]]
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
   Global options:
   
     -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
     -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
     --credentials <arg>      The default credentials to use
     --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
     --config <arg>           The JcrFs config to use
     -v (--verbose)           verbose output
     -q (--quiet)             print as little as possible
     --version                print the version information and exit
     --log-level <level>      the log4j log level
     -h (--help) <command>    print this help
   ```

설치한 후 전역 무시된 하위 버전 파일을 업데이트해야 합니다. 저장 설정을 편집하고 다음을 추가합니다.

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### 줄 끝 문자 구성 {#configuring-the-end-of-line-character}

VLT는 다음 규칙에 따라 EOF(라인 끝)를 자동으로 처리합니다.

* Windows에서 체크 아웃한 파일 줄이 `CRLF`
* Linux/Unix에서 체크 아웃된 파일 줄 `LF`
* 저장소에 연결된 파일 줄이 `LF`

VLT 및 SVN 구성이 일치하는지 확인하려면 `svn:eol-style` 속성 대상 `native` 저장소에 저장된 파일의 확장명을 지정합니다. 저장 설정을 편집하고 다음을 추가합니다.

```xml
[auto-props]
*.css = svn:eol-style=native
*.cnd = svn:eol-style=native
*.java = svn:eol-style=native
*.js = svn:eol-style=native
*.json = svn:eol-style=native
*.xjson = svn:eol-style=native
*.jsp = svn:eol-style=native
*.txt = svn:eol-style=native
*.html = svn:eol-style=native
*.xml = svn:eol-style=native
*.properties = svn:eol-style=native
```

### 저장소 체크 아웃 {#checking-out-the-repository}

소스 제어 시스템을 사용하여 저장소를 체크 아웃합니다. 예를 들어, svn에 URI와 경로를 리포지토리로 대체)를 입력합니다.

```shell
svn co https://svn.server.com/repos/myproject
```

### 저장소와 동기화 {#synchronizing-with-the-repository}

파일을 리포지토리와 동기화해야 합니다. 이를 위해 진행되는 작업:

1. 명령줄에서 `content/jcr_root`.
1. 다음을 입력하여 저장소를 체크 아웃합니다(포트 번호 대체). **4502년** 및 관리자 암호):

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >자격 증명은 초기 체크아웃 시 한 번만 지정해야 합니다. 그러면 홈 디렉토리에 저장됩니다 `.vault/auth.xml`.

### 동기화가 수행되었는지 테스트 {#testing-whether-the-synchronization-worked}

리포지토리를 체크 아웃하고 동기화한 후에는 모든 것이 제대로 작동하는지 테스트해야 합니다. 이렇게 하는 간단한 방법은 **.jsp** 파일에서 변경 내용을 적용한 후 변경 내용이 반영되었는지 확인합니다.

동기화를 테스트하려면

1. 다음으로 이동 `.../jcr_content/libs/foundation/components/text`.
1. 에서 항목 편집 `text.jsp`.
1. 입력하여 수정된 파일을 확인합니다. `vlt st`
1. 입력하여 변경 내용을 확인합니다 `vlt diff text.jsp`
1. 변경 사항을 커밋합니다. `vlt ci test.jsp`.
1. 텍스트 구성 요소가 포함된 페이지를 다시 로드하고 변경 사항이 있는지 확인합니다.

## VLT 도구 도움말 {#getting-help-with-the-vlt-tool}

VLT 도구를 설치한 후 명령줄에서 해당 도움말 파일에 액세스할 수 있습니다.

```shell
vlt --help
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Usage:
  vlt [options] <command> [arg1 [arg2 [arg3] ..]]
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Global options:
  -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
  -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
  --credentials <arg>      The default credentials to use
  --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
  --config <arg>           The JcrFs config to use
  -v (--verbose)           verbose output
  -q (--quiet)             print as little as possible
  --version                print the version information and exit
  --log-level <level>      the log4j log level
  -h (--help) <command>    print this help
Commands:
  export                   Export the Vault filesystem
  import                   Import a Vault filesystem
  checkout (co)            Checkout a Vault file system
  status (st)              Print the status of working copy files and directories.
  update (up)              Bring changes from the repository into the working copy.
  info                     Displays information about a local file.
  commit (ci)              Send changes from your working copy to the repository.
  revert (rev)             Restore pristine working copy file (undo most local edits).
  resolved (res)           Remove 'conflicted' state on working copy files or directories.
  propget (pg)             Print the value of a property on files or directories.
  proplist (pl)            Print the properties on files or directories.
  propset (ps)             Set the value of a property on files or directories.
  add                      Put files and directories under version control.
  delete (del,rm)          Remove files and directories from version control.
  diff (di)                Display the differences between two paths.
  rcp                      Remote copy of repository content.
  sync                     Control vault sync service
  console                  Run an interactive console
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

특정 명령에 대한 도움말을 보려면 help 명령을 입력하고 그 뒤에 명령 이름을 입력합니다. 예:

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified in order to export just a sub tree.
  Example:
    vlt export http://localhost:4502/crx /apps/geometrixx myproject

Options:
  -v (--verbose)          verbose output
  -t (--type) <arg>       specifies the export type. either 'platform' or 'jar'.
  -p (--prune-missing)    specifies if missing local files should be deleted.
  <uri>                   mountpoint uri
  <jcr-path>              the jcr path
  <local-path>            the local path
```

## VLT에서 수행되는 일반적인 작업 {#common-tasks-performed-in-vlt}

다음은 VLT에서 수행되는 몇 가지 일반적인 작업입니다. 각 명령에 대한 자세한 내용은 [명령](#vlt-commands).

### 하위 트리 체크 아웃 {#checking-out-a-subtree}

예를 들어 리포지토리의 하위 트리만 체크 아웃하려는 경우 `/apps/geometrixx`이렇게 하려면 다음을 입력합니다.

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

이렇게 하면 새 내보내기 루트가 만들어집니다 `geo` 사용 `META-INF` 및 `jcr_root` 디렉토리 및 모든 파일 아래에 `/apps/geometrixx` in `geo/jcr_root`.

### 필터링된 체크아웃 수행 {#performing-a-filtered-checkout}

기존 작업 공간 필터가 있고 체크 아웃에 사용하려는 경우, 먼저 `META-INF/vault` 디렉토리에 필터를 배치하거나 다음과 같이 명령줄에 지정합니다.

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

예제 필터:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### .vlt 컨트롤 대신 가져오기/내보내기 사용 {#using-import-export-instead-of-vlt-control}

제어 파일을 사용하지 않고 JCR 리포지토리와 로컬 파일 시스템 간에 컨텐츠를 가져오고 내보낼 수 있습니다.

를 사용하지 않고 컨텐츠를 가져오고 내보내려면 `.vlt` 제어:

1. 처음에 리포지토리를 설정합니다.

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. 원격 복사본을 변경하고 JCR을 업데이트합니다.

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. 원격 복사본을 변경하고 파일 서버를 업데이트합니다.

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## VLT 사용 {#using-vlt}

VLT에서 명령을 실행하려면 명령줄에 다음을 입력합니다.

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

옵션 및 명령은 다음 섹션에서 자세히 설명합니다.

## VLT 글로벌 옵션 {#vlt-global-options}

다음은 모든 명령에 사용할 수 있는 VLT 옵션 목록입니다. 사용 가능한 추가 옵션에 대한 자세한 내용은 개별 명령을 참조하십시오.

|  |  |
|--- |--- |
| 옵션 | 설명 |
| `-Xjcrlog <arg>` | 확장된 JcrLog 옵션 |
| `-Xdavex <arg>` | 확장된 JCR 원격 옵션 |
| `--credentials <arg>` | 사용할 기본 자격 증명 |
| `--config <arg>` | 사용할 JcrFs 구성 |
| `-v (--verbose)` | 자세한 출력 |
| `-q (--quiet)` | 가능한 한 적은 양의 인쇄 |
| `--version` | 버전 정보 및 종료 VLT를 인쇄합니다. |
| `--log-level <level>` | 로그 수준(예: log4j 로그 수준)을 나타냅니다. |
| `-h (--help) <command>` | 특정 명령에 대한 도움말을 인쇄합니다. |

## VLT 명령 {#vlt-commands}

다음 표에서는 사용 가능한 모든 VLT 명령을 설명합니다. 구문, 사용 가능한 옵션 및 예제에 대한 자세한 내용은 개별 명령을 참조하십시오.

|  |  |  |
|--- |--- |--- |
| Command | 단축 명령 | 설명 |
| `export` |  | 제어 파일 없이 JCR 저장소(저장소 파일 시스템)에서 로컬 파일 시스템으로 내보냅니다. |
| `import` |  | 로컬 파일 시스템을 JCR 저장소(저장소 파일 시스템)로 가져옵니다. |
| `checkout` | `co` | Vault 파일 시스템을 체크 아웃합니다. 로컬 파일 시스템에 대한 초기 JCR 저장소에 사용합니다. (참고: 먼저 하위 버전의 저장소를 체크 아웃해야 합니다.) |
| `analyze` |  | 패키지를 분석합니다. |
| `status` | `st` | 작업 복사 파일 및 디렉토리의 상태를 인쇄합니다. |
| `update` | `up` | 저장소의 변경 내용을 작업 복사본으로 가져옵니다. |
| `info` |  | 로컬 파일에 대한 정보를 표시합니다. |
| `commit` | `ci` | 작업 복사본에서 저장소로 변경 내용을 보냅니다. |
| `revert` | `rev` | 작업 복사본 파일을 원래 상태로 복원하고 대부분의 로컬 편집 내용을 취소합니다. |
| `resolved` | `res` | 작업 복사 파일 또는 디렉터리에서 충돌하는 상태를 제거합니다. |
| `propget` | `pg` | 파일 또는 디렉터리에 속성 값을 인쇄합니다. |
| `proplist` | `pl` | 파일 또는 디렉토리에 대한 속성을 인쇄합니다. |
| `propset` | `ps` | 파일 또는 디렉터리에 대한 속성 값을 설정합니다. |
| `add` |  | 파일 및 디렉터리를 버전 제어에 둡니다. |
| `delete` | `del` 또는 `rm` | 버전 제어에서 파일 및 디렉터리를 제거합니다. |
| `diff` | `di` | 두 경로 간의 차이점을 표시합니다. |
| `console` |  | 대화형 콘솔을 실행합니다. |
| `rcp` |  | 한 원격 리포지토리에서 다른 리포지토리로 노드 트리를 복사합니다. |
| `sync` |  | 저장소 동기화 서비스를 제어할 수 있습니다. |

### 내보내기 {#export}

에 마운트된 Vault 파일 시스템을 내보냅니다. &lt;uri> 로컬 파일 시스템 &lt;local-path>. 선택 사항입니다 &lt;jcr-path> 하위 트리만 내보내도록 지정할 수 있습니다.

#### 구문 {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### 옵션 {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | 자세한 출력 |
| `-t (--type) <arg>` | 플랫폼 또는 jar로 내보내기 유형을 지정합니다. |
| `-p (--prune-missing)` | 누락된 로컬 파일을 삭제할 것인지 지정합니다. |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | JCR 경로 |
| `<localPath>` | 로컬 경로 |

#### 예제 {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### 가져오기 {#import}

로컬 파일 시스템 가져오기(시작 위치 `<local-path>` 의 저장소 파일 시스템으로 이동합니다. `<uri>`. 을(를) 지정할 수 있습니다 `<jcr-path>` 를 가져오기 루트로 사용합니다. If `--sync` 이 지정되면 가져온 파일이 자동으로 보관소 제어에 놓입니다.

#### 구문 {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### 옵션 {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | 자세한 출력 |
| `-s (-- sync)` | 로컬 파일을 볼팅(vaulting) 제어 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | JCR 경로 |
| `<localPath>` | 로컬 경로 |

#### 예제 {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### 체크아웃(co) {#checkout-co}

JCR 저장소에서 로컬 파일 시스템으로 초기 체크 아웃을 수행합니다. &lt;uri> 로컬 파일 시스템 &lt;local-path>. 을(를) 추가할 수도 있습니다 &lt;jcrpath> 원격 트리의 하위 디렉터리를 체크 아웃하는 인수입니다. META-INF 디렉터리에 복사되는 작업 공간 필터를 지정할 수 있습니다.

#### 구문 {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### 옵션 {#options-2}

|  |  |
|--- |--- |
| `--force` | 로컬 파일이 이미 있는 경우 체크 아웃이 로컬 파일을 덮어쓰도록 합니다. |
| `-v (--verbose)` | 자세한 출력 |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `-f (--filter) <file>` | 정의된 필터가 없는 경우 자동 필터를 지정합니다. |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | (선택 사항) 원격 경로 |
| `<localPath>` | (선택 사항) 로컬 경로 |

#### 예제 {#examples-2}

JCR Remoting 사용:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

기본 작업 공간 사용:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

URI가 완료되지 않으면 확장됩니다.

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### 분석 {#analyze}

패키지를 분석합니다.

#### 구문 {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### 옵션 {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | 핫픽스 링크의 printf 형식(예: name,id) `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | 자세한 출력 |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `<localPaths> [<localPaths> ...]` | 로컬 경로 |

### 상태 {#status}

작업 복사 파일 및 디렉토리의 상태를 인쇄합니다.

If `--show-update` 가 지정되면 각 파일이 원격 버전과 비교하여 확인됩니다. 그런 다음 두 번째 문자는 업데이트 작업에서 수행할 작업을 지정합니다.

#### 구문 {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### 옵션 {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | 자세한 출력 |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `-u (--show-update)` | 업데이트 정보 표시 |
| `-N (--non-recursive)` | 단일 디렉터리에서 작동합니다. |
| `<file> [<file> ...]` | 상태를 표시할 파일 또는 디렉터리 |

### 업데이트 {#update}

리포지토리의 변경 내용을 작업 복사본으로 복사합니다.

#### 구문 {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### 옵션 {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | 자세한 출력 |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `--force` | 로컬 파일을 강제로 덮어씁니다. |
| `-N (--non-recursive)` | 단일 디렉터리에서 작동합니다. |
| `<file> [<file> ...]` | 업데이트할 파일 또는 디렉터리 |

### 정보 {#info}

로컬 파일에 대한 정보를 표시합니다.

#### 구문 {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### 옵션 {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | 자세한 출력 |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `-R (--recursive)` | 순환 |
| `<file> [<file> ...]` | 정보를 표시할 파일 또는 디렉터리 |

### 커밋 {#commit}

작업 복사본에서 저장소로 변경 내용을 보냅니다.

#### 구문 {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### 옵션 {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | 자세한 출력 |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `--force` | 원격 복사본이 수정되더라도 커밋을 강제 적용합니다. |
| `-N (--non-recursive)` | 단일 디렉터리에서 작동합니다. |
| `<file> [<file> ...]` | 커밋할 파일 또는 디렉터리 |

### 되돌리기 {#revert}

작업 복사 파일을 원래 상태로 복원하고 대부분의 로컬 편집 내용을 취소합니다.

#### 구문 {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### 옵션 {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `-R (--recursive)` | 반복적인 언급 |
| `<file> [<file> ...]` | 커밋할 파일 또는 디렉터리 |

### 해결됨 {#resolved}

제거 **충돌** 작업 복사 파일 또는 디렉터리에 대한 상태입니다.

>[!NOTE]
>
>이 명령은 충돌을 의미적으로 해결하거나 충돌 마커를 제거하지 않습니다. 충돌 관련 아티팩트 파일을 제거하고 PATH를 다시 커밋할 수 있습니다.

#### 구문 {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### 옵션 {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `-R (--recursive)` | 반복적인 언급 |
| `--force` | 충돌 마커가 있어도 해결됨 |
| `<file> [<file> ...]` | 확인할 파일 또는 디렉터리 |

### Prop {#propget}

파일 또는 디렉터리에 속성 값을 인쇄합니다.

#### 구문 {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### 옵션 {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `-R (--recursive)` | 반복적인 언급 |
| `<propname>` | 속성 이름 |
| `<file> [<file> ...]` | 속성을 가져올 파일 또는 디렉터리 |

### Proplist {#proplist}

파일 또는 디렉토리에 대한 속성을 인쇄합니다.

#### 구문 {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### 옵션 {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `-R (--recursive)` | 반복적인 언급 |
| `<file> [<file> ...]` | 속성을 나열할 파일 또는 디렉터리 |

### Propset {#propset}

파일 또는 디렉터리에 대한 속성 값을 설정합니다.

>[!NOTE]
>
>VLT는 다음의 특수한 버전 관리 속성을 인식합니다.
>
>`vlt:mime-type`
>
>파일의 MIME 유형입니다. 파일을 병합할지 여부를 결정하는 데 사용됩니다. &#39;text/&#39;(또는 누락된 MIME 유형)로 시작하는 MIME 유형은 텍스트로 처리됩니다. 다른 것은 모두 바이너리로 처리됩니다.

#### 구문 {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### 옵션 {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `-R (--recursive)` | 반복적인 언급 |
| `<propname>` | 속성 이름 |
| `<propval>` | 속성 값 |
| `<file> [<file> ...]` | 속성을 로 설정할 파일 또는 디렉터리 |

### 페이지 URL에 {#add}

파일 및 디렉토리를 버전 제어 하에 두고 리포지토리 외에 예약합니다. 다음 커밋에 추가됩니다.

#### 구문 {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### 옵션 {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | 자세한 출력 |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `-N (--non-recursive)` | 단일 디렉터리에서 작동합니다. |
| `--force` | 작업을 강제로 실행합니다. |
| `<file> [<file> ...]` | 추가할 로컬 파일 또는 디렉터리 |

### 삭제 {#delete}

버전 제어에서 파일 및 디렉터리를 제거합니다.

#### 구문 {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### 옵션 {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | 자세한 출력 |
| `-q (--quiet)` | 가능한 한 적은 인화 |
| `--force` | 작업을 강제로 실행합니다. |
| `<file> [<file> ...]` | 삭제할 로컬 파일 또는 디렉터리 |

### 차이 {#diff}

두 경로 간의 차이점을 표시합니다.

#### 구문 {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### 옵션 {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | 단일 디렉터리에서 작동합니다. |
| `<file> [<file> ...]` | 파일 또는 디렉토리 |

### 콘솔 {#console}

대화형 콘솔을 실행합니다.

#### 구문 {#syntax-16}

```shell
console -F <file>
```

#### 옵션 {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | 콘솔 설정 파일을 지정합니다. 기본 파일은 console.properties입니다. |

### Rcp {#rcp}

한 원격 리포지토리에서 다른 리포지토리로 노드 트리를 복사합니다. `<src>` 소스 노드를 가리키고 `<dst>` 상위 노드가 있어야 하는 대상 경로를 지정합니다. Rcp는 데이터를 스트리밍하여 노드를 처리합니다.

#### 구문 {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### 옵션 {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | 가능한 한 적은 인쇄를 합니다. |
| `-r (--recursive)` | 반복적으로 설명됩니다. |
| `-b (--batchSize) <size>` | 중간 저장 전에 처리할 노드 수입니다. |
| `-t (--throttle) <seconds>` | 중간 저장 후 대기할 시간(초)입니다. |
| `-u (--update)` | 기존 노드를 덮어쓰기/삭제합니다. |
| `-n (--newer)` | 업데이트할 lastModified 속성을 준수합니다. |
| `-e (--exclude) <arg> [<arg> ...]` | 제외된 소스 경로의 등록 확장입니다. |
| `<src>` | 소스 트리의 저장소 주소입니다. |
| `<dst>` | 대상 노드의 저장소 주소입니다. |

#### 예제 {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>다음 `--exclude` 옵션 뒤에 다른 옵션이 와야 합니다 `<src>` 및 `<dst>` 인수. 예:
>
>`vlt rcp -e ".*\.txt" -r`

### 동기화 {#sync}

저장소 동기화 서비스를 제어할 수 있습니다. 인수 없이 이 명령은 현재 작업 디렉터리를 동기화 제어에 둡니다. Vlt 체크 아웃 내에서 실행되는 경우 각각의 필터와 호스트를 사용하여 동기화를 구성합니다. vlt 체크 아웃 외부에서 실행되는 경우 디렉토리가 비어 있는 경우에만 동기화를 위해 현재 폴더가 등록됩니다.

#### 구문 {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### 옵션 {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | 자세한 출력입니다. |
| `--force` | 특정 명령을 강제로 실행합니다. |
| `-u (--uri) <uri>` | 동기화 호스트의 URI를 지정합니다. |
| `<command>` | 실행할 sync 명령 |
| `<localPath>` | 동기화할 로컬 폴더입니다. |

### 상태 코드 {#status-codes}

VLT에서 사용하는 상태 코드는 다음과 같습니다.

* &#39; 수정 안 함
* &#39;A&#39;가 추가되었습니다.
* &#39;C&#39; 충돌
* &#39;D&#39; 삭제됨
* &#39;I&#39; 무시됨
* &#39;M&#39;이 수정됨
* &#39;R&#39; 대체됨
* &#39;?&#39; 항목이 버전 제어에 있지 않습니다.
* &#39;!&#39; 항목이 없거나(svn 명령에 의해 제거됨) 불완전함
* &#39;~&#39; 버전이 지정된 항목이 다른 종류의 항목으로 가려집니다.

## FileVault 동기화 설정 {#setting-up-filevault-sync}

저장소 동기화 서비스는 저장소 컨텐츠를 로컬 파일 시스템 표현과 동기화하거나 그 반대로 동기화하는 데 사용됩니다. 저장소 변경 사항을 수신하고 파일 시스템 컨텐츠를 주기적으로 스캔하는 OSGi 서비스를 설치하면 이러한 작업이 수행됩니다. 저장소 컨텐츠를 디스크에 매핑하기 위해 저장소와 동일한 직렬화 형식을 사용합니다.

>[!NOTE]
>
>저장소 동기화 서비스는 개발 도구이며 운영 시스템에서 사용하는 것이 매우 어렵습니다. 또한 이 서비스는 로컬 파일 시스템에서만 동기화할 수 있으며 원격 개발에 사용할 수 없습니다.

### vlt를 사용하여 서비스 설치 {#installing-the-service-using-vlt}

다음 `vlt sync install` 명령을 사용하여 vault sync 서비스 번들과 구성을 자동으로 설치할 수 있습니다.

이 번들은 아래에 설치되어 있습니다 `/libs/crx/vault/install` 구성 노드는 `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. 처음에는 서비스가 활성화되었지만 동기화 루트가 구성되지 않았습니다.

다음 예제에서는 지정된 uri에서 액세스할 수 있는 CRX 인스턴스에 동기화 서비스를 설치합니다.

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### 서비스 상태 표시 {#displaying-the-service-status}

다음 `status` 명령을 사용하여 실행 중인 동기화 서비스에 대한 정보를 표시할 수 있습니다. &quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>다음 `status` 명령은 서비스에서 라이브 데이터를 가져오지 않고 의 구성을 읽습니다. `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`.

### 동기화 폴더 추가 {#adding-a-sync-folder}

다음 `register` 명령은 구성에 동기화할 폴더를 추가하는 데 사용됩니다.

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>다음 `register` 명령을 사용하여 `sync-once` 구성.

### 동기화 폴더 제거 {#removing-a-sync-folder}

다음 `unregister` 명령은 구성에서 동기화할 폴더를 제거하는 데 사용됩니다.

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>폴더 자체를 삭제하기 전에 동기화 폴더의 등록을 취소해야 합니다.

### 동기화 구성 {#configuring-synchronization}

#### 서비스 구성 {#service-configuration}

서비스가 실행되면 다음 매개 변수로 구성할 수 있습니다.

* `vault.sync.syncroots`: 동기화 루트를 정의하는 하나 이상의 로컬 파일 시스템 경로

* `vault.sync.fscheckinterval`: 파일 시스템에서 변경 사항을 검사할 빈도(초)입니다. 기본값은 5초입니다.
* `vault.sync.enabled`: 서비스를 활성화/비활성화하는 일반 플래그입니다.

>[!NOTE]
>
>이 서비스는 웹 콘솔 또는 `sling:OsgiConfig` 노드(이름 포함) `com.day.jcr.sync.impl.VaultSyncServiceImpl`) 내의 아무 곳에나 삽입할 수 있습니다.
>
>AEM을 사용하여 작업하는 경우 이러한 서비스에 대한 구성 설정을 관리하는 방법에는 몇 가지가 있습니다. 참조 [OSGi 구성](/help/sites-deploying/configuring-osgi.md) 자세한 내용

#### 동기화 폴더 구성 {#sync-folder-configuration}

각 동기화 폴더는 구성 및 상태를 세 개의 파일에 저장합니다.

* `.vlt-sync-config.properties`: 구성 파일.

* `.vlt-sync.log`: 동기화 중에 수행한 작업에 대한 정보가 들어 있는 로그 파일입니다.
* `.vlt-sync-filter.xml`: 저장소의 어떤 부분이 동기화되는지를 정의하는 필터입니다. 이 파일의 형식은 [필터링된 체크아웃 수행](#performing-a-filtered-checkout) 섹션을 참조하십시오.

다음 `.vlt-sync-config.properties` 파일에서 다음 속성을 구성할 수 있습니다.

**비활성화됨** 동기화를 켜거나 끕니다. 기본적으로 이 매개 변수는 동기화를 허용하도록 false 로 설정됩니다.

**sync-once** 비어 있지 않으면 다음 검사 시 지정된 방향으로 폴더를 동기화하면 매개 변수가 지워집니다. 두 값이 지원됩니다.

* `JCR2FS`: JCR 저장소의 모든 컨텐츠를 내보내고 로컬 디스크에 씁니다.
* `FS2JCR`: 디스크의 모든 컨텐츠를 JCR 저장소로 가져옵니다.

**sync-log** 로그 파일 이름을 정의합니다. 기본적으로 값은 .vlt-sync.log입니다

### 개발에 VLT 동기화 사용 {#using-vlt-sync-for-development}

동기화 폴더를 기반으로 개발 환경을 설정하려면 다음과 같이 진행합니다.

1. vlt 명령줄을 사용하여 리포지토리 체크아웃:

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >필터를 사용하여 적절한 경로를 체크아웃만 할 수 있습니다. 자세한 내용은 [필터링된 체크아웃 수행](#performing-a-filtered-checkout) 섹션에 자세히 설명되어 있습니다.

1. 작업 복사본의 루트 폴더로 이동합니다.

   ```shell
   $ cd dev/jcr_root/
   ```

1. 저장소에 동기화 서비스 설치:

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. 동기화 서비스 초기화:

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. 편집 `.vlt-sync-config.properties` 숨겨진 파일 및 동기화를 구성하여 저장소의 컨텐츠를 동기화합니다.

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >이 단계에서는 필터 구성에 따라 전체 저장소를 다운로드합니다.

1. 로그 파일을 확인합니다 `.vlt-sync.log` 진행 상황을 보려면 다음을 수행하십시오.

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

이제 로컬 폴더가 리포지토리와 동기화됩니다. 동기화는 양방향 이므로 리포지토리에서 수정한 내용이 로컬 동기화 폴더에 적용되거나 그 반대의 경우도 마찬가지입니다.

>[!NOTE]
>
>VLT 동기화 기능은 간단한 파일과 폴더만 지원하지만 특별한 자격 증명 모음 직렬화된 파일(.content.xml, dialog.xml 등)을 감지하여 자동으로 무시합니다. 따라서 기본 종료 체크 아웃에서 저장소 동기화를 사용할 수 있습니다.
