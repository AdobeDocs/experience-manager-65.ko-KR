---
title: SRP에 대한 Solr 구성
description: Apache Solr 설치를 다른 컬렉션을 사용하여 노드 저장소(Oak)와 공통 저장소(SRP) 간에 공유할 수 있습니다
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 2%

---

# SRP에 대한 Solr 구성 {#solr-configuration-for-srp}

## AEM Platform용 Solr {#solr-for-aem-platform}

[Apache Solr](https://solr.apache.org/) 설치는 다른 컬렉션을 사용하여 [노드 저장소](../../help/sites-deploying/data-store-config.md)(Oak)와 [공통 저장소](working-with-srp.md)(SRP) 간에 공유할 수 있습니다.

Oak 및 SRP 컬렉션을 모두 집중적으로 사용하는 경우 성능상의 이유로 두 번째 Solr을 설치할 수 있습니다.

프로덕션 환경의 경우 [SolrCloud 모드](#solrcloud-mode)는 독립 실행형 모드(단일 로컬 Solr 설정)보다 향상된 성능을 제공합니다.

### 요구 사항 {#requirements}

Apache Solr 다운로드 및 설치:

* [버전 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr에는 Java™ 1.7 이상이 필요합니다.
* 서비스가 필요하지 않습니다.
* 실행 모드 선택:

   * 독립형 모드
   * [SolrCloud 모드](#solrcloud-mode)(프로덕션 환경에 권장)

* 다국어 검색(MLS) 선택

   * [표준 MLS 설치](#installing-standard-mls)
   * [고급 MLS 설치](#installing-advanced-mls)

## SolrCloud 모드 {#solrcloud-mode}

프로덕션 환경에는 [SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html) 모드가 권장됩니다. SolrCloud 모드에서 실행하는 경우 MLS(다국어 검색)를 설치하기 전에 SolrCloud를 설치하고 구성해야 합니다.

SolrCloud 지침에 따라 설치하는 것이 좋습니다.

* 동일한 서버에 SolrCloud 노드 3개
* 외부 Apache Zookeeper.

또한 메모리 사용량 및 가비지 수집을 조정하도록 JVM을 구성하는 것이 좋습니다.

### JVM 구성 예 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud 설정 명령 {#solrcloud-setup-commands}

SolrCloud 모드에서 실행할 때 MLS 설치 전에 다음 SolrCloud 설정 명령에 대한 사용 및 지식이 필요합니다.

#### 1. ZooKeeper에 구성 업로드 {#upload-a-configuration-to-zookeeper}

참조:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

사용:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2. 컬렉션 만들기 {#create-a-collection}

참조:
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

사용:
./bin/solr 만들기 \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *포트*\
-s *조각 수* \
-rf *복제본 수*

#### 3. 구성 세트에 컬렉션 연결 {#link-a-collection-to-a-configuration-set}

ZooKeeper에 이미 업로드된 구성에 컬렉션을 연결합니다.

참조:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

사용:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### 표준 및 고급 MLS 비교 {#comparison-of-standard-and-advanced-mls}

AEM Communities용 다국어 검색(MLS)은 영어를 포함하여 지원되는 모든 언어에서 향상된 검색을 제공하기 위해 Solr 플랫폼용으로 빌드되었습니다.

AEM Communities용 MLS는 표준 MLS 또는 고급 MLS로 사용할 수 있습니다. 표준 MLS는 Solr 구성 설정만 포함하며 플러그인 또는 리소스 파일은 제외합니다. 고급 MLS는 보다 포괄적인 솔루션이며 Solr 구성 설정, 플러그인 및 관련 리소스를 포함합니다

표준 MLS에는 다음 언어에 대한 콘텐츠 검색 기능이 개선되었습니다.

* 영어: 단어 파생과 일치시키기 위해 향상된 스템머.
* 일본어: 반자 문자에 대한 일본어 토큰화가 개선되었습니다.

고급 MLS에는 다음 언어에 대한 콘텐츠 검색 기능이 개선되었습니다.

* English: Stemmer를 lemmatizer로 대체했습니다.
* 독일어: decompounder를 추가했습니다.
* 프랑스어: 제거 처리가 추가되었습니다.
* 중국어 (간체): 더 스마트한 토큰화기를 추가했습니다.
* 다양한 언어: 압축기, 정지어 목록 및 정규화기를 추가했습니다.

고급 MLS에서는 모두 다음 33개 언어가 지원됩니다.

| 아랍어 | 독일어 | 노르웨이어 |
|---|---|---|
| 불가리아어 | 그리스어 | 폴란드어 |
| 중국어 (간체) | 아이티 크리올 | 포르투갈어 |
| 중국어(번체) | 히브리어 | 루마니아어 |
| 체코어 | 헝가리어 | 러시아어 |
| 덴마크어 | 인도네시아어 | 슬로바키아어 |
| 네덜란드어 | 이탈리아어 | 슬로베니아어 |
| 영어 | 일본어 | 스페인어 |
| 에스토니아어 | 한국어 | 스웨덴어 |
| 핀란드어 | 라트비아어 | 태국어 |
| 프랑스어 | 리투아니아어 | 터키어 |

#### AEM 6.1 Solr 검색, 표준 MLS 및 고급 MLS 비교 {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**참고**: AEM 6.1은 AEM 6.1 커뮤니티 FP3 및 이전 버전을 참조합니다.

![compare-solr-mls](assets/compare-solr-mls.png)

### 표준 MLS 설치 {#installing-standard-mls}

SRP 컬렉션(MSRP 또는 DSRP)의 경우 표준 다국어 검색(MLS)을 지원하려면 Solr의 구성 파일 중 두 개를 수정해야 합니다.

* **schema.xml**
* **solrconfig.xml**

Solr 4.10용 표준 MLS 파일(schema.xml, solrconfig.xml)입니다.

Solr 5.x용 표준 MLS 파일(schema.xml, solrconfig.xml)입니다.

표준 MLS 파일은 AEM 저장소에 저장됩니다.

**참고**: Solr 파일이 msrp/ 폴더에 저장되어 있는 동안에는 DSRP용이기도 합니다(변경 필요 없음).

**다운로드 지침**: `solrX`을(를) `solr4` 또는 `solr5`(으)로 적절하게 바꿉니다.

1. CRXDE|Lite를 사용하여 다음을 찾습니다.

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Solr이 배포된 로컬 서버로 다운로드합니다.

   * `jcr:content` 노드의 `jcr:data` 속성을 찾습니다.
   * 다운로드를 시작하려면 `view`을(를) 선택합니다.
   * 파일이 적절한 이름과 인코딩(UTF8)으로 저장되었는지 확인합니다.

1. 독립 실행형 또는 SolrCloud 모드에 대한 설치 지침을 따르십시오.

#### SolrCloud 모드 - 표준 MLS {#solrcloud-mode-standard-mls}

1. SolrCloud 모드에서 Solr을 설치하고 구성합니다.
1. 새 구성 준비:

   1. `solr-install-dir*/myconfig/`과(와) 같은 new-config-dir* 만들기

   1. 기존 Solr 구성 디렉터리의 내용을 *new-config-dir*&#x200B;에 복사합니다.

      * Solr4의 경우: `solr-install-dir/example/solr/collection1/conf/` 복사
      * Solr5의 경우: `solr-install-dir/server/solr/configsets/data_driven_schema_configs/` 복사

   1. 다운로드한 **schema.xml** 및 **solrconfig.xml**&#x200B;을(를) *new-config-dir*&#x200B;에 복사하여 기존 파일을 덮어씁니다.

1. [새 구성을 업로드](#upload-a-configuration-to-zookeeper)합니다.
1. [조각 수, 복제본 수 및 구성 이름 등 필요한 매개 변수를 지정하는 컬렉션을 만듭니다](#create-a-collection).
1. 컬렉션을 만드는 동안 구성 이름이 *제공되지 않은 경우, 새로 만든 이 컬렉션을 [연결](#link-a-collection-to-a-configuration-set)하여 ZooKeeper에 업로드된 구성을 만드십시오.

1. MSRP의 경우 새로 설치하지 않으면 [MSRP 색인 재지정 도구](msrp.md#msrp-reindex-tool)를 실행하십시오.

#### 독립형 모드 - 표준 MLS {#standalone-mode-standard-mls}

1. 독립 실행형 모드로 Solr을 설치합니다.
1. Solr5를 실행하는 경우 Solr4와 유사한 collection1을 생성합니다.

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Solr 구성 디렉터리의 **schema.xml** 및 **solrconfig.xml**&#x200B;을(를) 백업합니다. 예:

   * Solr4의 경우: `solr-install-dir/example/solr/collection1/conf/`
   * Solr5에 대해 생성됨: `solr-install-dir/server/solr/collection1/conf/`

1. 다운로드한 **schema.xml** 및 **solrconfig.xml**&#x200B;을(를) 동일한 디렉터리에 복사합니다.

1. Solr을 다시 시작합니다.
1. MSRP의 경우 새로 설치하지 않으면 [MSRP 색인 재지정 도구](#msrpreindextool)를 실행하십시오.

### 고급 MLS 설치 {#installing-advanced-mls}

SRP 컬렉션(MSRP 또는 DSRP)이 고급 MLS를 지원하려면 사용자 지정 스키마 및 Solr 구성 외에 새로운 Solr 플러그인이 필요합니다. 모든 필수 항목은 다운로드 가능한 zip 파일로 패키지됩니다. 또한 Solr이 독립형 모드로 배포될 때 사용할 설치 스크립트가 포함됩니다.

고급 MLS 패키지를 얻으려면 설명서의 배포 섹션에서 [AEM 고급 MLS](deploy-communities.md#aem-advanced-mls)을(를) 참조하십시오.

SolrCloud 또는 독립 실행형 모드에 대한 설치를 시작하려면 다음을 수행하십시오.

* Solr을 호스팅하는 서버에 AEM-SOLR-MLS zip 아카이브를 다운로드합니다.
* 아카이브 압축을 풉니다.

#### SolrCloud 모드 - 고급 MLS {#solrcloud-mode-advanced-mls}

설치 지침 - Solr4 및 Solr5의 몇 가지 차이점에 유의하십시오.

1. SolrCloud 모드에서 Solr을 설치하고 구성합니다.
1. 디스크에 고급 MLS 패키지의 내용을 추출합니다. 컨텐츠는 다음과 같아야 합니다.

   * **schema.xml**
   * **solrconfig.xml**
   * **중지 단어/** 폴더
   * **프로필/** 폴더
   * **extra-libs/** 폴더

1. 새 구성 준비:

   1. *new-config-dir* 만들기

      * 예: `solr-install-dir/myconfig/`
      * `stopwords/` 및 `lang/` 하위 폴더 만들기

   1. 기존 Solr 구성 디렉터리의 내용을 *new-config-dir*&#x200B;에 복사합니다.

      * Solr4의 경우: `solr-install-dir/example/solr/collection1/conf/` 복사
      * Solr5의 경우: `solr-install-dir/server/solr/configsets/data_driven_schema_configs/` 복사

   1. 기존 파일을 덮어쓰려면 추출한 **schema.xml** 및 **solrconfig.xml**&#x200B;을(를) *new-config-dir*&#x200B;에 복사하십시오.
   1. Solr5의 경우: `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt`을(를) `new-config-dir/lang/`에 복사
   1. 추출된 **stopwords/** 폴더를 *new-config-dir*&#x200B;에 복사하여 `new-config-dir/stopwords/*.txt`을(를) 만듭니다.

1. ZooKeeper에 [새 구성 업로드](#upload-a-configuration-to-zookeeper)
1. 새 **프로필/** 폴더 복사...

   * Solr4의 경우: 각 노드의 리소스/폴더에 복사
   * Solr5의 경우: 각 Solr 설치의 서버/리소스/ 폴더로 복사합니다. 모든 노드가 동일한 Solr 설치 디렉토리에 있는 경우 이 단계는 한 번만 수행됩니다.

1. SolrCloud에 있는 각 노드의 solr-home 디렉터리(solr.xml 포함)에 **lib/** 폴더를 만듭니다. 다음 위치에서 각 노드의 새 라이브러리/폴더로 jar를 복사합니다.

   * 고급 MLS 패키지에서 **extra-libs/** 추출됨
   * *solr-install-dir/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [조각 수, 복제본 수 및 구성 이름 등 필요한 매개 변수를 지정하는 컬렉션을 만듭니다](#create-a-collection).
1. 컬렉션을 만드는 동안 구성 이름이 *제공되지 않음*&#x200B;인 경우 새로 만든 이 컬렉션을 [연결](#link-a-collection-to-a-configuration-set)하여 ZooKeeper에 업로드된 구성을 사용하세요.

1. MSRP의 경우 새로 설치하지 않으면 [MSRP 색인 재지정 도구](#msrpreindextool)를 실행하십시오.

#### 독립형 모드 - 고급 MLS {#standalone-mode-advanced-mls}

설치 스크립트는 고급 MLS 패키지에 포함되어 있습니다.

패키지의 내용이 독립형 Solr 서버를 호스팅하는 서버로 추출된 후 설치 스크립트를 실행하여 필요한 리소스 및 구성 파일을 설치합니다.

* 독립 실행형 모드로 Solr을 설치합니다.
* Solr5를 실행하는 경우 Solr4와 유사한 collection1을 생성합니다.

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* 설치 스크립트 실행: [-v 4|5] [-d solrhome] [-c collectionpath] 설치
여기서:

   * -d solrhome

     Solr 설치 디렉토리

   * -c collectionpath

     Solr의 컬렉션 경로

   * —도움말

     인쇄 명령줄 옵션

   * -v [4|5]

     Solr 버전 설정

* Solr 4.10.4의 예:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0의 예:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**참고**:

* 설치 스크립트는 &quot;.orig&quot;를 추가하여 새 버전을 설치하기 전에 schema.xml 및 solrconfig.xml을 백업합니다

### solrconfig.xml 정보 {#about-solrconfig-xml}

**solrconfig.xml** 파일은 자동 커밋 간격 및 검색 가시성을 제어하며 테스트 및 조정이 필요합니다.

`<autoCommit>`: 기본적으로 안정적인 저장소에 대한 하드 커밋인 AutoCommit 간격은 15초로 설정됩니다. 검색 가시성은 기본적으로 사전 커밋 인덱스 사용으로 설정됩니다.

커밋으로 인한 변경 내용을 반영하도록 업데이트된 인덱스를 사용하도록 검색을 변경하려면 포함된 `openSearcher`을(를) true로 변경하십시오.

`autoSoftCommit`: &#39;소프트&#39; 커밋은 변경 내용을 표시(색인 업데이트)하지만 변경 내용이 안정적인 저장소(하드 커밋)에 동기화되지 않도록 합니다. 그 결과 성능이 향상되었습니다. 기본적으로 `autoSoftCommit`은(는) 포함된 `maxTime`이(가) -1로 설정되어 비활성화되어 있습니다.
