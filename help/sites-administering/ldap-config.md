---
title: AEM 6을 사용하여 LDAP 구성
description: AEM을 사용하여 LDAP를 구성하는 방법에 대해 알아봅니다.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---

# AEM 6을 사용하여 LDAP 구성 {#configuring-ldap-with-aem}

LDAP( **L**&#x200B;팔다리 **D**&#x200B;디렉터리 **A**&#x200B;액세스 **P** rotocol)은 중앙 디렉토리 서비스에 액세스하는 데 사용됩니다. 여러 애플리케이션에서 액세스할 수 있으므로 사용자 계정을 관리하는 데 필요한 노력을 줄일 수 있습니다. 이러한 LDAP 서버 중 하나는 Active Directory입니다. LDAP는 종종 사용자가 한 번에 로그인한 후 여러 애플리케이션에 액세스할 수 있는 단일 사인온을 달성하는 데 사용됩니다.

사용자 계정은 LDAP 서버와 저장소 간에 동기화할 수 있으며 LDAP 계정 세부 정보는 저장소에 저장됩니다. 이 기능을 사용하면 필요한 권한 및 권한을 할당하기 위해 저장소 그룹에 계정을 할당할 수 있습니다.

저장소는 LDAP 인증을 사용하여 이러한 사용자를 인증하며, 확인을 위해 LDAP 서버로 자격 증명이 전달됩니다. 이 인증은 저장소에 대한 액세스를 허용하기 전에 필요합니다. 성능을 향상시키기 위해 만료 시간 초과와 함께 성공적으로 검증된 자격 증명을 저장소에 캐시하여 적절한 기간 후에 유효성 재검사가 수행되도록 할 수 있습니다.

계정이 LDAP 서버에서 제거되면 유효성 검사가 더 이상 부여되지 않고 저장소에 대한 액세스가 거부됩니다. 저장소에 저장된 LDAP 계정의 세부 정보도 삭제할 수 있습니다.

이러한 계정의 사용은 사용자에게 투명합니다. 즉, LDAP에서 생성된 사용자 및 그룹 계정과 저장소에서만 생성된 계정 간에 차이가 없습니다.

AEM 6에서 LDAP 지원은 이전 버전과 다른 유형의 구성이 필요한 새로운 구현과 함께 제공됩니다.

이제 모든 LDAP 구성을 OSGi 구성으로 사용할 수 있습니다. 다음 웹 관리 콘솔을 통해 구성할 수 있습니다.
`https://serveraddress:4502/system/console/configMgr`

LDAP가 AEM에서 작동하도록 하려면 세 개의 OSGi 구성을 생성해야 합니다.

1. IDP(LDAP Identity Provider).
1. 동기화 핸들러.
1. 외부 로그인 모듈.

>[!NOTE]
>
>시청 [Oak의 외부 로그인 모듈 - LDAP 및 그 이상으로 인증](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html?lang=en) 외부 로그인 모듈을 자세히 살펴보십시오.
>
>Apache DS를 사용하여 Experience Manager을 구성하는 예를 보려면 를 참조하십시오. [Apache 디렉터리 서비스를 사용하도록 Adobe Experience Manager 6.5를 구성합니다.](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/configuring-adobe-experience-manager-6-to-use-apache-directory/m-p/183805)

## LDAP Id 공급자 구성 {#configuring-the-ldap-identity-provider}

LDAP ID 공급자는 LDAP 서버에서 사용자를 검색하는 방법을 정의하는 데 사용됩니다.

관리 콘솔의 **Apache Jackrabbit Oak LDAP ID 공급자** 이름.

LDAP ID 공급자에 대해 다음 구성 옵션을 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>LDAP 공급자 이름</strong></td>
   <td>이 LDAP 공급자 구성의 이름입니다.</td>
  </tr>
  <tr>
   <td><strong>LDAP 서버 호스트 이름</strong><br /> </td>
   <td>LDAP 서버의 호스트 이름</td>
  </tr>
  <tr>
   <td><strong>LDAP 서버 포트</strong></td>
   <td>LDAP 서버의 포트</td>
  </tr>
  <tr>
   <td><strong>SSL 사용</strong></td>
   <td>SSL(LDAP) 연결을 사용해야 하는지 여부를 나타냅니다.</td>
  </tr>
  <tr>
   <td><strong>TLS 사용</strong></td>
   <td>연결 시 TLS를 시작해야 하는지 여부를 나타냅니다.</td>
  </tr>
  <tr>
   <td><strong>인증서 확인 비활성화</strong></td>
   <td>서버 인증서 유효성 검사를 사용하지 않아야 하는지 여부를 나타냅니다.</td>
  </tr>
  <tr>
   <td><strong>DN 바인딩</strong></td>
   <td>인증용 사용자의 DN입니다. 이 필드를 비워 두면 익명 바인딩이 수행됩니다.</td>
  </tr>
  <tr>
   <td><strong>바인딩 암호</strong></td>
   <td>인증을 위한 사용자의 암호</td>
  </tr>
  <tr>
   <td><strong>검색 시간 초과</strong></td>
   <td>검색 시간이 초과될 때까지의 시간</td>
  </tr>
  <tr>
   <td><strong>최대 활성 관리 풀</strong></td>
   <td>관리자 연결 풀의 최대 활성 크기입니다.</td>
  </tr>
  <tr>
   <td><strong>최대 활성 사용자 풀</strong></td>
   <td>사용자 연결 풀의 최대 활성 크기입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 기본 DN</strong></td>
   <td>사용자 검색 DN</td>
  </tr>
  <tr>
   <td><strong>사용자 객체 클래스</strong></td>
   <td>사용자 항목에 포함되어야 하는 객체 클래스 목록입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 ID 속성</strong></td>
   <td>사용자 ID가 포함된 속성의 이름입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 추가 필터</strong></td>
   <td>사용자를 검색할 때 사용할 추가 LDAP 필터입니다. 최종 필터의 형식은 다음과 같습니다. '(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'(user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>사용자 DN 경로</strong></td>
   <td>중간 경로의 일부를 계산하는 데 DN을 사용해야 하는지 여부를 제어합니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 기본 DN</strong></td>
   <td>그룹 검색을 위한 기본 DN입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 객체 클래스</strong></td>
   <td>그룹 항목에 포함되어야 하는 객체 클래스 목록입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 이름 속성</strong></td>
   <td>그룹 이름이 포함된 속성의 이름입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 추가 필터</strong></td>
   <td>그룹을 검색할 때 사용할 추가 LDAP 필터입니다. 최종 필터의 형식은 다음과 같습니다. '(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>그룹 DN 경로</strong></td>
   <td>중간 경로의 일부를 계산하는 데 DN을 사용해야 하는지 여부를 제어합니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 멤버 속성</strong></td>
   <td>하나 이상의 그룹 멤버가 포함된 그룹 속성입니다.</td>
  </tr>
 </tbody>
</table>

## 동기화 핸들러 구성 {#configuring-the-synchronization-handler}

동기화 처리기는 ID 공급자 사용자 및 그룹이 저장소와 동기화되는 방법을 정의합니다.

아래에 있습니다. **Apache Jackrabbit Oak 기본 동기화 핸들러** management console의 이름입니다.

동기화 핸들러에 다음 구성 옵션을 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>동기화 핸들러 이름</strong></td>
   <td>동기화 구성의 이름입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 만료 시간</strong></td>
   <td>동기화된 사용자가 만료될 때까지의 기간.</td>
  </tr>
  <tr>
   <td><strong>사용자 자동 멤버십</strong></td>
   <td>동기화된 사용자가 자동으로 추가되는 그룹 목록입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 속성 매핑</strong></td>
   <td>외부 로컬 속성의 목록 매핑 정의입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 경로 접두사</strong></td>
   <td>사용자를 만들 때 사용되는 경로 접두사입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 멤버십 만료</strong></td>
   <td>멤버십이 만료된 후 시간입니다.<br /> </td>
  </tr>
  <tr>
   <td><strong>사용자 멤버십 중첩 깊이</strong></td>
   <td>멤버십 관계가 동기화되면 그룹 중첩의 최대 깊이를 반환합니다. 값이 0이면 그룹 멤버십 조회가 효과적으로 비활성화됩니다. 값이 1이면 사용자의 직접 그룹만 추가됩니다. 이 값은 사용자 멤버십 상위 그룹을 동기화할 때만 개별 그룹을 동기화할 때 영향을 주지 않습니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 만료 시간</strong></td>
   <td>동기화된 그룹이 만료될 때까지의 기간.</td>
  </tr>
  <tr>
   <td><strong>그룹 자동 멤버십</strong></td>
   <td>동기화된 그룹이 자동으로 추가되는 그룹 목록입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 속성 매핑</strong></td>
   <td>외부 로컬 속성의 목록 매핑 정의입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 경로 접두사</strong></td>
   <td>그룹을 만들 때 사용되는 경로 접두사입니다.</td>
  </tr>
 </tbody>
</table>

## 외부 로그인 모듈 {#the-external-login-module}

외부 로그인 모듈은 **Apache Jackrabbit Oak 외부 로그인 모듈** 관리 콘솔에서 게시할 수 있습니다.

>[!NOTE]
>
>Apache Jackrabbit Oak 외부 로그인 모듈은 JAAS(Java™ Authentication and Authorization Servi) 사양을 구현합니다. 다음을 참조하십시오. [공식 Oracle Java™ 보안 참조 안내서](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) 추가 정보.

이 작업은 사용할 ID 공급자와 동기화 핸들러를 정의하여 두 모듈을 효과적으로 바인딩하는 것입니다.

다음 구성 옵션을 사용할 수 있습니다.

| **JAAS 순위** | 이 로그인 모듈 항목의 순위(즉, 정렬 순서)를 지정합니다. 항목은 내림차순으로 정렬됩니다(즉, 높은 값의 등급 구성이 우선함). |
|---|---|
| **JAAS 제어 플래그** | LoginModule이 REQUIRED, REQUISITE, EXPECT 또는 OPTIONAL인지 지정하는 속성입니다. 이러한 플래그의 의미에 대한 자세한 내용은 JAAS 구성 설명서 를 참조하십시오. |
| **JAAS 영역** | LoginModule이 등록된 영역 이름(또는 응용 프로그램 이름)입니다. 영역 이름이 제공되지 않으면 LoginModule이 Felix JAS 구성에 구성된 대로 기본 영역에 등록됩니다. |
| **ID 공급자 이름** | ID 공급자의 이름입니다. |
| **동기화 핸들러 이름** | 동기화 처리기의 이름입니다. |

>[!NOTE]
AEM 인스턴스와 함께 LDAP 구성을 두 개 이상 가질 계획이라면 각 구성에 대해 별도의 ID 공급자와 동기화 핸들러를 만들어야 합니다.

## SSL을 통한 LDAP 구성 {#configure-ldap-over-ssl}

AEM 6은 아래 절차에 따라 SSL을 통해 LDAP를 인증하도록 구성할 수 있습니다.

1. 다음 확인: **SSL 사용** 또는 **TLS 사용** 구성 시 확인란 [LDAP ID 공급자](#configuring-the-ldap-identity-provider).
1. 설정에 따라 동기화 핸들러 및 외부 로그인 모듈을 구성합니다.
1. 필요한 경우 Java™ VM에 SSL 인증서를 설치합니다. 이 설치는 keytool을 사용하여 수행할 수 있습니다.

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. LDAP 서버에 대한 연결을 테스트합니다.

### SSL 인증서 생성 {#creating-ssl-certificates}

SSL을 통해 LDAP를 인증하도록 AEM을 구성할 때 자체 서명된 인증서를 사용할 수 있습니다. 다음은 AEM에서 사용할 인증서를 생성하는 작업 절차의 예입니다.

1. SSL 라이브러리가 설치되어 있고 작동하는지 확인합니다. 이 절차에서는 OpenSSL을 예로 사용합니다.

1. 사용자 지정된 OpenSSL 구성(cnf) 파일을 만듭니다. 이 구성은 기본 **openssl.cnf **구성 파일을 복사하고 사용자 지정하여 수행할 수 있습니다. UNIX® 시스템에서는 `/usr/lib/ssl/openssl.cnf`

1. 터미널에서 아래 명령을 실행하여 CA 루트 키를 만듭니다.

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 다음으로 자체 서명된 인증서를 만듭니다.

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. 모든 것이 제대로 되어 있는지 확인하려면 새로 생성된 인증서를 검사하십시오.

   `openssl x509 -noout -text -in root-ca.crt`

1. 인증서 구성(.cnf) 파일에 지정된 모든 폴더가 있는지 확인하십시오. 그렇지 않으면 만듭니다.
1. 다음과 같이 실행하여 무작위 시드 만들기:

   `openssl rand -out private/.rand 8192`

1. 생성된 .pem 파일을 .cnf 파일에 구성된 위치로 이동합니다.

1. 마지막으로 인증서를 Java™ 키 저장소에 추가합니다.

## 디버그 로깅 활성화 {#enabling-debug-logging}

연결 문제를 해결하기 위해 LDAP ID 공급자와 외부 로그인 모듈에 대해 디버그 로깅을 활성화할 수 있습니다.

디버그 로깅을 활성화하려면 다음을 수행해야 합니다.

1. 웹 관리 콘솔로 이동합니다.
1. &quot;Apache Sling Logging Logger 구성&quot;을 찾아 다음 옵션으로 두 개의 로거를 만듭니다.

* 로그 수준: 디버그
* 로그 파일 logs/ldap.log
* 메시지 패턴: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* 로거: org.apache.jackrabbit.oak.security.authentication.ldap

* 로그 수준: 디버그
* 로그 파일: logs/external.log
* 메시지 패턴: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* 로거: org.apache.jackrabbit.oak.spi.security.authentication.external

## 그룹 소속에 대한 단어 {#a-word-on-group-affiliation}

LDAP를 통해 동기화된 사용자는 AEM의 다른 그룹에 속할 수 있습니다. 이러한 그룹은 동기화 프로세스의 일부로 AEM에 추가되는 외부 LDAP 그룹일 수 있습니다. 그러나 별도로 추가되고 원래 LDAP 그룹 제휴 체계의 일부가 아닌 그룹일 수도 있습니다.

일반적으로 이러한 그룹은 로컬 AEM 관리자 또는 다른 ID 공급자에 의해 추가됩니다.

사용자가 LDAP 서버의 그룹에서 제거된 경우 변경 사항은 동기화 시 AEM 측에 반영됩니다. 그러나 LDAP에 의해 추가되지 않은 사용자의 다른 모든 그룹 소속은 그대로 유지됩니다.

AEM은 를 사용하여 외부 그룹에서 사용자 제거를 감지하고 처리합니다. `rep:externalId` 속성. 이 속성은 동기화 핸들러에 의해 동기화되는 모든 사용자 또는 그룹에 자동으로 추가되며 원래 ID 공급자에 대한 정보를 포함합니다.

에서 Apache Oak 설명서 를 참조하십시오. [사용자 및 그룹 동기화](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## 알려진 문제 {#known-issues}

SSL을 통한 LDAP를 사용할 계획이라면 Netscape 주석 옵션 없이 사용 중인 인증서가 작성되었는지 확인하십시오. 이 옵션을 활성화하면 인증이 실패하고 SSL 핸드셰이크 오류가 발생합니다.
