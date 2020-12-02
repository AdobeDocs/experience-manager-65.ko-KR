---
title: AEM 6에서 LDAP 구성
seo-title: AEM 6에서 LDAP 구성
description: AEM에서 LDAP를 구성하는 방법을 알아봅니다.
seo-description: AEM에서 LDAP를 구성하는 방법을 알아봅니다.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 0%

---


# AEM 6 {#configuring-ldap-with-aem}에서 LDAP 구성

LDAP(**L**&#x200B;오른쪽 **D**&#x200B;디렉토리 **액세스** P **프로토콜)은 중앙 디렉토리 서비스에 액세스하는 데 사용됩니다.** 따라서 여러 애플리케이션에서 액세스할 수 있으므로 사용자 계정을 관리하는 데 필요한 노력을 줄일 수 있습니다. 이러한 LDAP 서버 중 하나가 Active Directory입니다. LDAP는 사용자가 한 번 로그인한 후에 여러 애플리케이션에 액세스할 수 있는 단일 사인온 생성 기능을 수행하는 데 사용됩니다.

LDAP 서버와 저장소 간에 사용자 계정을 동기화할 수 있으며 LDAP 계정 세부 사항을 저장소에 저장할 수 있습니다. 이를 통해 필요한 권한 및 권한을 할당하기 위해 계정을 저장소 그룹에 할당할 수 있습니다.

보관소는 LDAP 인증을 사용하여 이러한 사용자를 인증하며 유효성 검사를 위해 LDAP 서버로 전달되는 자격 증명을 통해 저장소에 대한 액세스를 허용하기 전에 필요합니다. 성능을 향상시키기 위해, 성공적으로 검증된 자격 증명은 저장소에서 캐시할 수 있으며, 만료 시간 초과를 사용하여 적절한 기간 후에 재유효성 검사가 수행되는지 확인할 수 있습니다.

LDAP 서버 검증에서 계정이 제거되면 더 이상 부여되지 않으므로 저장소에 대한 액세스가 거부됩니다. 저장소에 저장된 LDAP 계정에 대한 세부 사항도 삭제할 수 있습니다.

이러한 계정 사용은 사용자에게 투명하게 제공되므로 LDAP에서 만든 사용자 및 그룹 계정과 저장소에 단독으로 생성된 계정 간에 아무런 차이가 없습니다.

AEM 6에서 LDAP 지원은 이전 버전과 다른 유형의 구성이 필요한 새로운 구현과 함께 제공됩니다.

이제 모든 LDAP 구성을 OSGi 구성으로 사용할 수 있습니다. 웹 관리 콘솔을 통해 다음 링크를 구성할 수 있습니다.
`https://serveraddress:4502/system/console/configMgr`

AEM에서 LDAP를 사용하려면 세 개의 OSGi 구성을 만들어야 합니다.

1. IDP(LDAP Identity Provider).
1. 동기화 핸들러.
1. 외부 로그인 모듈입니다.

>[!NOTE]
>
>외부 로그인 모듈을 자세히 살펴보려면 [Oak의 외부 로그인 모듈 - LDAP와 Beyond](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#)을 사용하여 인증
>
>Apache DS를 사용하여 Experience Manager을 구성하는 예를 보려면 [Adobe Experience Manager 6.5를 구성하여 Apache Directory Service를 사용하십시오.](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## LDAP ID 공급자 구성 {#configuring-the-ldap-identity-provider}

LDAP ID 공급자는 LDAP 서버에서 사용자를 검색하는 방법을 정의하는 데 사용됩니다.

관리 콘솔에서 **Apache Jackrabbit Oak LDAP Identity Provider** 이름 아래에 있습니다.

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
   <td>연결에서 TLS를 시작할지 여부를 나타냅니다.</td>
  </tr>
  <tr>
   <td><strong>인증서 확인 비활성화</strong></td>
   <td>서버 인증서 유효성 검사를 비활성화해야 하는지 여부를 나타냅니다.</td>
  </tr>
  <tr>
   <td><strong>바인딩 DN</strong></td>
   <td>인증에 사용할 사용자의 DN입니다. 비워 두면 익명 바인딩이 수행됩니다.</td>
  </tr>
  <tr>
   <td><strong>바인딩 암호</strong></td>
   <td>인증을 위한 사용자의 암호</td>
  </tr>
  <tr>
   <td><strong>검색 시간 초과</strong></td>
   <td>검색 시간이 초과될 때까지</td>
  </tr>
  <tr>
   <td><strong>관리 풀 최대 활성</strong></td>
   <td>관리 연결 풀의 최대 활성 크기입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 풀 최대 활성</strong></td>
   <td>사용자 연결 풀의 최대 활성 크기입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 기본 DN</strong></td>
   <td>사용자 검색에 대한 DN</td>
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
   <td>사용자를 검색할 때 사용할 추가 LDAP 필터입니다. 최종 필터는 다음과 같이 형식이 지정됩니다.'(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'(user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>사용자 DN 경로</strong></td>
   <td>중간 경로의 부분을 계산하는 데 DN을 사용해야 하는지 여부를 제어합니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 기본 DN</strong></td>
   <td>그룹 검색에 대한 기본 DN입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 개체 클래스</strong></td>
   <td>그룹 항목에 포함되어야 하는 개체 클래스 목록입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 이름 속성</strong></td>
   <td>그룹 이름을 포함하는 속성의 이름입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 추가 필터</strong></td>
   <td>그룹을 검색할 때 사용할 추가 LDAP 필터입니다. 최종 필터는 다음과 같이 형식이 지정됩니다.'(&amp;(&lt;nameAttr&gt;=&lt;groupName&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>그룹 DN 경로</strong></td>
   <td>중간 경로의 부분을 계산하는 데 DN을 사용해야 하는지 여부를 제어합니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 구성원 속성</strong></td>
   <td>그룹의 구성원을 포함하는 그룹 속성입니다.</td>
  </tr>
 </tbody>
</table>

## 동기화 처리기 구성 {#configuring-the-synchronization-handler}

동기화 처리기는 Indentity Provider 사용자 및 그룹이 저장소로 동기화되는 방식을 정의합니다.

관리 콘솔의 **Apache Jackrabbit Oak 기본 동기화 처리기** 이름 아래에 있습니다.

동기화 처리기에 다음 구성 옵션을 사용할 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>처리기 이름 동기화</strong></td>
   <td>동기화 구성 이름입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 만료 시간</strong></td>
   <td>동기화된 사용자가 만료될 때까지 지속 시간입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 자동 멤버십</strong></td>
   <td>동기화된 사용자가 자동으로 추가되는 그룹 목록입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 속성 매핑</strong></td>
   <td>외부 속성의 로컬 속성의 목록 매핑 정의입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 경로 접두사</strong></td>
   <td>새 사용자를 만들 때 사용되는 경로 접두사입니다.</td>
  </tr>
  <tr>
   <td><strong>사용자 멤버십 만료</strong></td>
   <td>멤버십이 만료되는 시간입니다.<br /> </td>
  </tr>
  <tr>
   <td><strong>사용자 멤버십 중첩 깊이</strong></td>
   <td>구성원 관계가 동기화될 때 그룹 중첩의 최대 깊이를 반환합니다. 0이면 그룹 구성원 조회를 효과적으로 사용하지 않습니다. 값이 1이면 사용자의 직접 그룹만 추가됩니다. 사용자 멤버십 조상을 동기화할 때만 개별 그룹을 동기화할 때 이 값은 영향을 주지 않습니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 만료 시간</strong></td>
   <td>동기화된 그룹이 만료될 때까지 지속 시간입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 자동 멤버십</strong></td>
   <td>동기화된 그룹이 자동으로 추가되는 그룹 목록입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 속성 매핑</strong></td>
   <td>외부 속성의 로컬 속성의 목록 매핑 정의입니다.</td>
  </tr>
  <tr>
   <td><strong>그룹 경로 접두사</strong></td>
   <td>새 그룹을 만들 때 사용되는 경로 접두사입니다.</td>
  </tr>
 </tbody>
</table>

## 외부 로그인 모듈 {#the-external-login-module}

외부 로그인 모듈은 관리 콘솔 아래의 **Apache Jackrabbit Oak 외부 로그인 모듈** 아래에 있습니다.

>[!NOTE]
>
>Apache Jackrabbit Oak 외부 로그인 모듈은 JAAS(Java Authentication and Authorization Service) 사양을 구현합니다. 자세한 내용은 [공식 Oracle Java 보안 참조 안내서](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html)를 참조하십시오.

이 두 모듈을 효과적으로 바인딩하여 사용할 ID 공급자와 동기화 핸들러를 정의하는 것이 이들의 역할입니다.

다음 구성 옵션을 사용할 수 있습니다.

| **JAAS 순위** | 이 로그인 모듈 항목의 등급(정렬 순서) 지정. 항목은 내림차순으로 정렬됩니다(즉, 값이 더 높은 구성이 먼저 표시됨). |
|---|---|
| **JAAS 컨트롤 플래그** | LoginModule이 필수, 필수, SUITABLE 또는 OPTIONAL인지 여부를 지정하는 속성입니다. 이러한 플래그의 의미에 대한 자세한 내용은 JAS 구성 설명서를 참조하십시오. |
| **JAAS 영역** | LoginModule을 등록할 영역 이름(또는 응용 프로그램 이름)입니다. 영역 이름이 제공되지 않으면 Felix JAAS 구성에 구성된 대로 LoginModule이 기본 영역에 등록됩니다. |
| **ID 공급자 이름** | ID 공급자의 이름입니다. |
| **처리기 이름 동기화** | 동기화 처리기 이름입니다. |

>[!NOTE]
>
>AEM 인스턴스와 두 개 이상의 LDAP 구성을 가질 계획이면 각 구성에 대해 별도의 ID 제공자와 동기화 처리기를 만들어야 합니다.

## SSL {#configure-ldap-over-ssl}을 통해 LDAP 구성

AEM 6은 아래 절차에 따라 SSL을 통해 LDAP를 인증하도록 구성할 수 있습니다.

1. [LDAP ID 공급자](#configuring-the-ldap-identity-provider)를 구성할 때 **SSL** 또는 **TLS** 확인란을 선택합니다.
1. 설정에 따라 동기화 핸들러와 외부 로그인 모듈을 구성합니다.
1. 필요한 경우 Java VM에 SSL 인증서를 설치합니다. 이 작업은 키 도구를 사용하여 수행할 수 있습니다.

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. LDAP 서버에 대한 연결을 테스트합니다.

### SSL 인증서 {#creating-ssl-certificates} 만들기

자체 서명된 인증서는 AEM을 SSL을 통해 LDAP에 인증하도록 구성할 때 사용할 수 있습니다. 다음은 AEM에서 사용할 인증서를 생성하기 위한 작업 절차의 예입니다.

1. SSL 라이브러리를 설치하고 작동하는지 확인합니다. 이 절차에서는 OpenSSL을 예로 사용합니다.

1. 사용자 지정된 OpenSSL 구성(cnf) 파일을 만듭니다. 기본 **openssl.cnf **구성 파일을 복사하고 사용자 정의하여 수행할 수 있습니다. UNIX 시스템의 경우 일반적으로 `/usr/lib/ssl/openssl.cnf`에 있습니다.

1. 터미널에서 아래 명령을 실행하여 CA 루트 키를 만드는 작업을 계속 수행합니다.

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. 다음으로 자체 서명된 새 인증서를 만듭니다.

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Inspect이 새로 생성된 인증서를 사용하여 모든 것이 제대로 작동하는지 확인합니다.

   `openssl x509 -noout -text -in root-ca.crt`

1. 인증서 구성(.cnf) 파일에 지정된 모든 폴더가 있는지 확인합니다. 없는 경우 만듭니다.
1. 다음과 같이 실행함으로써 임의 시드 만들기

   `openssl rand -out private/.rand 8192`

1. 생성된 .pem 파일을 .cnf 파일에 구성된 위치로 이동합니다.

1. 마지막으로 Java 키 저장소에 인증서를 추가합니다.

## 디버그 로깅 사용 {#enabling-debug-logging}

연결 문제를 해결하기 위해 LDAP ID 공급자와 외부 로그인 모듈 모두에 대해 디버그 로깅을 설정할 수 있습니다.

디버그 로깅을 사용하려면 다음을 수행해야 합니다.

1. 웹 관리 콘솔로 이동합니다.
1. &quot;Apache Sling Logging Logger Configuration&quot;을 찾아 다음 옵션을 사용하여 두 개의 로거를 만듭니다.

* 로그 수준:디버그
* 로그 파일 logs/ldap.log
* 메시지 패턴:{0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* 로거:org.apache.jackrabbit.oak.security.authentication.ldap

* 로그 수준:디버그
* 로그 파일:logs/external.log
* 메시지 패턴:{0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast;{2} {3} {5}
* 로거:org.apache.jackrabbit.oak.spi.security.authentication.external

## 그룹 계열에 대한 단어 {#a-word-on-group-affiliation}

LDAP를 통해 동기화된 사용자는 AEM의 다른 그룹에 포함될 수 있습니다. 이러한 그룹은 동기화 프로세스의 일부로 AEM에 추가될 외부 LDAP 그룹일 수 있지만, 별도로 추가되는 그룹일 수도 있고 원본 LDAP 그룹 제휴 구성표에 속하지 않을 수도 있습니다.

대부분의 경우, 이러한 그룹은 로컬 AEM 관리자 또는 다른 ID 공급자가 추가하는 그룹일 수 있습니다.

LDAP 서버의 그룹에서 사용자를 제거하면 동기화 시 AEM 측에도 변경 사항이 반영됩니다. 그러나 LDAP에 추가되지 않은 사용자의 다른 모든 그룹 제휴는 그대로 유지됩니다.

AEM은 `rep:externalId` 속성을 사용하여 외부 그룹에서 사용자 제거를 감지하고 처리합니다. 이 속성은 동기화 처리기에 의해 동기화된 사용자 또는 그룹에 자동으로 추가되며 원래 ID 공급자에 대한 정보가 포함됩니다.

자세한 내용은 [사용자 및 그룹 동기화](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html)의 Apache Oak 설명서를 참조하십시오.

## 알려진 문제 {#known-issues}

SSL을 통해 LDAP를 사용할 계획인 경우 Netscape 주석 옵션 없이 사용 중인 인증서를 만들어야 합니다. 이 옵션을 활성화하면 SSL 핸드셰이크 오류가 발생하여 인증이 실패합니다.

